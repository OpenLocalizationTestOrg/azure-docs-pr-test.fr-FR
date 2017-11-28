---
title: "Didacticiel : Intégration d’Azure Active Directory à Namely | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Namely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 1d7e8fbcfc757853ab909bbb05522f3dc387715d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="ea0a8-103">Didacticiel : Intégration d’Azure Active Directory à Namely</span><span class="sxs-lookup"><span data-stu-id="ea0a8-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="ea0a8-104">Dans ce didacticiel, vous allez apprendre à intégrer Namely avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea0a8-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea0a8-105">L’intégration de Namely à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ea0a8-106">Dans Azure AD, vous pouvez contrôler qui a accès à Namely.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-106">You can control in Azure AD who has access to Namely</span></span>
- <span data-ttu-id="ea0a8-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Namely (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea0a8-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ea0a8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ea0a8-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea0a8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea0a8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ea0a8-110">Prerequisites</span></span>

<span data-ttu-id="ea0a8-111">Pour configurer l’intégration d’Azure AD avec Namely, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

- <span data-ttu-id="ea0a8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea0a8-113">Un abonnement Namely pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ea0a8-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea0a8-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea0a8-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea0a8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea0a8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea0a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea0a8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ea0a8-118">Scenario description</span></span>
<span data-ttu-id="ea0a8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea0a8-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea0a8-121">Ajout de Namely à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ea0a8-121">Adding Namely from the gallery</span></span>
2. <span data-ttu-id="ea0a8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-the-gallery"></a><span data-ttu-id="ea0a8-123">Ajout de Namely à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ea0a8-123">Adding Namely from the gallery</span></span>
<span data-ttu-id="ea0a8-124">Pour configurer l’intégration de Namely avec Azure AD, vous devez ajouter Namely disponible à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea0a8-125">**Pour ajouter Namely à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea0a8-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0a8-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ea0a8-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ea0a8-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ea0a8-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ea0a8-133">Dans la zone de recherche, tapez **Namely**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-133">In the search box, type **Namely**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="ea0a8-135">Dans le panneau des résultats, sélectionnez **Namely**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea0a8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea0a8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Namely, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ea0a8-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ea0a8-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Namely correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span></span> <span data-ttu-id="ea0a8-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Namely associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="ea0a8-141">Dans Namely, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ea0a8-142">Pour configurer et tester l’authentification unique Azure AD avec Namely, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ea0a8-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ea0a8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea0a8-145">**[Création d’un utilisateur de test Namely](#creating-a-namely-test-user)** pour obtenir un équivalent de Britta Simon dans Namely lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea0a8-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea0a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea0a8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea0a8-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Namely.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="ea0a8-150">**Pour configurer l’authentification unique Azure AD avec Namely, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea0a8-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0a8-151">Dans le Portail Azure, sur la page d’intégration de l’application **Namely**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ea0a8-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="ea0a8-155">Dans la section **Domaine et URL Namely**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-155">On the **Namely Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="ea0a8-157">a.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-157">a.</span></span> <span data-ttu-id="ea0a8-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="ea0a8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="ea0a8-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-159">b.</span></span> <span data-ttu-id="ea0a8-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="ea0a8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea0a8-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-161">These values are not real.</span></span> <span data-ttu-id="ea0a8-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ea0a8-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Namely](https://www.namely.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="ea0a8-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="ea0a8-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="ea0a8-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ea0a8-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea0a8-168">Dans la section **Configuration de Namely**, cliquez sur **Configurer Namely** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ea0a8-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="ea0a8-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="ea0a8-171">Dans une autre fenêtre de navigateur, connectez-vous à votre site d’entreprise Namely en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-171">In another browser window, sign on to your Namely company site as an administrator.</span></span>

8. <span data-ttu-id="ea0a8-172">Dans la barre d’outils située en haut, cliquez sur **Company**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-172">In the toolbar on the top, click **Company**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="ea0a8-174">Cliquez sur l'onglet **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="ea0a8-174">Click the **Settings** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="ea0a8-176">Cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-176">Click **SAML**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="ea0a8-178">Sur la page **SAML Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-178">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="ea0a8-180">a.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-180">a.</span></span> <span data-ttu-id="ea0a8-181">Cliquez sur **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="ea0a8-182">b.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-182">b.</span></span> <span data-ttu-id="ea0a8-183">Dans la zone de texte **URL d’authentification unique du fournisseur d’identité**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ea0a8-184">c.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-184">c.</span></span> <span data-ttu-id="ea0a8-185">Ouvrez le certificat que vous avez téléchargé dans le Bloc-notes, copiez son contenu, puis collez-le dans la zone de texte **Certificat du fournisseur d’identité** .</span><span class="sxs-lookup"><span data-stu-id="ea0a8-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="ea0a8-186">d.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-186">d.</span></span> <span data-ttu-id="ea0a8-187">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ea0a8-188">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ea0a8-189">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ea0a8-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea0a8-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea0a8-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0a8-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea0a8-192">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ea0a8-194">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea0a8-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0a8-195">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea0a8-197">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea0a8-199">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea0a8-201">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea0a8-203">a.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-203">a.</span></span> <span data-ttu-id="ea0a8-204">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea0a8-205">b.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-205">b.</span></span> <span data-ttu-id="ea0a8-206">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea0a8-207">c.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-207">c.</span></span> <span data-ttu-id="ea0a8-208">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ea0a8-209">d.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-209">d.</span></span> <span data-ttu-id="ea0a8-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="ea0a8-211">Création d’un utilisateur de test Namely</span><span class="sxs-lookup"><span data-stu-id="ea0a8-211">Creating a Namely test user</span></span>

<span data-ttu-id="ea0a8-212">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Namely.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="ea0a8-213">**Pour créer un utilisateur appelé Britta Simon dans Namely, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea0a8-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0a8-214">Connectez-vous à votre site d’entreprise Namely en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-214">Sign-on to your Namely company site as an administrator.</span></span>

2. <span data-ttu-id="ea0a8-215">Dans la barre d’outils située en haut, cliquez sur **People**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-215">In the toolbar on the top, click **People**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="ea0a8-217">Cliquez sur l’onglet **Directory** .</span><span class="sxs-lookup"><span data-stu-id="ea0a8-217">Click the **Directory** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="ea0a8-219">Cliquez sur **Add New Person**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-219">Click **Add New Person**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="ea0a8-221">Dans la boîte de dialogue **Add New Person** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea0a8-221">On the **Add New Person** dialog, perform the following steps:</span></span>

    <span data-ttu-id="ea0a8-222">a.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-222">a.</span></span> <span data-ttu-id="ea0a8-223">Dans la zone de texte **Prénom**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-223">In the **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="ea0a8-224">b.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-224">b.</span></span> <span data-ttu-id="ea0a8-225">Dans la zone de texte **Nom**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-225">In the **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="ea0a8-226">c.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-226">c.</span></span> <span data-ttu-id="ea0a8-227">Dans la zone de texte **E-mail**, saisissez **l’adresse e-mail** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea0a8-228">d.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-228">d.</span></span> <span data-ttu-id="ea0a8-229">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-229">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ea0a8-230">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea0a8-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ea0a8-231">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Namely.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ea0a8-233">**Pour affecter Britta Simon à Namely, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea0a8-233">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="ea0a8-234">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ea0a8-236">Dans la liste des applications, sélectionnez **Namely**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-236">In the applications list, select **Namely**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="ea0a8-238">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ea0a8-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-240">Click **Add** button.</span></span> <span data-ttu-id="ea0a8-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ea0a8-243">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ea0a8-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea0a8-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea0a8-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ea0a8-246">Testing single sign-on</span></span>

<span data-ttu-id="ea0a8-247">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ea0a8-248">Lorsque vous cliquez sur la vignette Namely dans le panneau d’accès, vous devez êtes automatiquement connecté à votre application Namely.</span><span class="sxs-lookup"><span data-stu-id="ea0a8-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea0a8-249">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ea0a8-249">Additional resources</span></span>

* [<span data-ttu-id="ea0a8-250">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea0a8-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea0a8-251">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ea0a8-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

