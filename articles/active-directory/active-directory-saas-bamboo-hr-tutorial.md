---
title: "Didacticiel : Intégration d’Azure Active Directory à BambooHR | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: 06bf91b0e598fd3d8e644378efdb753611ee1ebc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="a92f9-103">Didacticiel : Intégration d’Azure Active Directory à BambooHR</span><span class="sxs-lookup"><span data-stu-id="a92f9-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="a92f9-104">Dans ce didacticiel, vous allez apprendre à intégrer BambooHR à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a92f9-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a92f9-105">L’intégration de BambooHR à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a92f9-105">Integrating BambooHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a92f9-106">Dans Azure AD, vous pouvez contrôler qui a accès à BambooHR.</span><span class="sxs-lookup"><span data-stu-id="a92f9-106">You can control in Azure AD who has access to BambooHR</span></span>
- <span data-ttu-id="a92f9-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à BambooHR (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a92f9-107">You can enable your users to automatically get signed-on to BambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a92f9-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a92f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a92f9-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a92f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a92f9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a92f9-110">Prerequisites</span></span>

<span data-ttu-id="a92f9-111">Pour configurer l’intégration d’Azure AD à BambooHR, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a92f9-111">To configure Azure AD integration with BambooHR, you need the following items:</span></span>

- <span data-ttu-id="a92f9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a92f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a92f9-113">Un abonnement BambooHR pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a92f9-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a92f9-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a92f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a92f9-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a92f9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a92f9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a92f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a92f9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a92f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a92f9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a92f9-118">Scenario description</span></span>
<span data-ttu-id="a92f9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a92f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a92f9-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a92f9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a92f9-121">Ajout de BambooHR à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a92f9-121">Adding BambooHR from the gallery</span></span>
2. <span data-ttu-id="a92f9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a92f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-the-gallery"></a><span data-ttu-id="a92f9-123">Ajout de BambooHR à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a92f9-123">Adding BambooHR from the gallery</span></span>
<span data-ttu-id="a92f9-124">Pour configurer l’intégration de BambooHR à Azure AD, vous devez ajouter BambooHR, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a92f9-124">To configure the integration of BambooHR into Azure AD, you need to add BambooHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a92f9-125">**Pour ajouter BambooHR à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="a92f9-125">**To add BambooHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a92f9-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a92f9-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a92f9-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a92f9-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a92f9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a92f9-133">Dans la zone de recherche, tapez **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-133">In the search box, type **BambooHR**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="a92f9-135">Dans le volet de résultats, sélectionnez **BambooHR**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a92f9-135">In the results panel, select **BambooHR**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a92f9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a92f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a92f9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BambooHR, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a92f9-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a92f9-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur BambooHR correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a92f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BambooHR is to a user in Azure AD.</span></span> <span data-ttu-id="a92f9-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur BambooHR associé.</span><span class="sxs-lookup"><span data-stu-id="a92f9-140">In other words, a link relationship between an Azure AD user and the related user in BambooHR needs to be established.</span></span>

<span data-ttu-id="a92f9-141">Dans BambooHR, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="a92f9-141">In BambooHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a92f9-142">Pour configurer et tester l’authentification unique Azure AD avec BambooHR, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="a92f9-142">To configure and test Azure AD single sign-on with BambooHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a92f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a92f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a92f9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a92f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a92f9-145">**[Création d’un utilisateur de test BambooHR](#creating-a-bamboohr-test-user)** pour avoir un équivalent de Britta Simon dans BambooHR lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a92f9-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - to have a counterpart of Britta Simon in BambooHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a92f9-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a92f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a92f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a92f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a92f9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a92f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a92f9-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application BambooHR.</span><span class="sxs-lookup"><span data-stu-id="a92f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="a92f9-150">**Pour configurer l’authentification unique Azure AD avec BambooHR, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="a92f9-150">**To configure Azure AD single sign-on with BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="a92f9-151">Dans le portail Azure, dans la page d’intégration de l’application **BambooHR**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-151">In the Azure portal, on the **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a92f9-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a92f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="a92f9-155">Dans la section **Domaine et URL BambooHR**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a92f9-155">On the **BambooHR Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="a92f9-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="a92f9-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="a92f9-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="a92f9-158">This value is not real.</span></span> <span data-ttu-id="a92f9-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="a92f9-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a92f9-160">Pour obtenir cette valeur, contactez [l’équipe du support BambooHR](https://www.bamboohr.com/contact.php).</span><span class="sxs-lookup"><span data-stu-id="a92f9-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) to get this value.</span></span> 
 
4. <span data-ttu-id="a92f9-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a92f9-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="a92f9-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a92f9-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a92f9-165">Dans la section **Configuration de BambooHR**, cliquez sur **Configurer BambooHR** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-165">On the **BambooHR Configuration** section, click **Configure BambooHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a92f9-166">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a92f9-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="a92f9-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise BambooHR en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a92f9-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="a92f9-169">Dans la page d’accueil, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a92f9-169">On the homepage, perform the following steps:</span></span>
   
    <span data-ttu-id="a92f9-170">![Authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="a92f9-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="a92f9-171">a.</span><span class="sxs-lookup"><span data-stu-id="a92f9-171">a.</span></span> <span data-ttu-id="a92f9-172">Cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="a92f9-173">b.</span><span class="sxs-lookup"><span data-stu-id="a92f9-173">b.</span></span> <span data-ttu-id="a92f9-174">Dans le menu des applications sur la gauche, cliquez sur **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-174">In the apps menu on the left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="a92f9-175">c.</span><span class="sxs-lookup"><span data-stu-id="a92f9-175">c.</span></span> <span data-ttu-id="a92f9-176">Cliquez sur **SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="a92f9-177">Dans la section **SAML Single Sign-On** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a92f9-177">In the **SAML Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="a92f9-178">![Authentification unique SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="a92f9-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="a92f9-179">a.</span><span class="sxs-lookup"><span data-stu-id="a92f9-179">a.</span></span> <span data-ttu-id="a92f9-180">Collez la valeur de **l’URL du service d’authentification unique SAML** dans la zone de texte **URL de la connexion avec authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-180">Paste the **SAML Single Sign-On Service URL** value into the **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="a92f9-181">b.</span><span class="sxs-lookup"><span data-stu-id="a92f9-181">b.</span></span> <span data-ttu-id="a92f9-182">Ouvrez dans le Bloc-notes votre certificat codé en base 64 téléchargé dans le portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat X.509**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="a92f9-183">c.</span><span class="sxs-lookup"><span data-stu-id="a92f9-183">c.</span></span> <span data-ttu-id="a92f9-184">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a92f9-185">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a92f9-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a92f9-186">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a92f9-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a92f9-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a92f9-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a92f9-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a92f9-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="a92f9-189">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a92f9-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a92f9-191">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a92f9-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a92f9-192">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a92f9-194">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a92f9-196">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a92f9-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a92f9-198">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a92f9-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a92f9-200">a.</span><span class="sxs-lookup"><span data-stu-id="a92f9-200">a.</span></span> <span data-ttu-id="a92f9-201">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a92f9-202">b.</span><span class="sxs-lookup"><span data-stu-id="a92f9-202">b.</span></span> <span data-ttu-id="a92f9-203">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a92f9-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a92f9-204">c.</span><span class="sxs-lookup"><span data-stu-id="a92f9-204">c.</span></span> <span data-ttu-id="a92f9-205">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a92f9-206">d.</span><span class="sxs-lookup"><span data-stu-id="a92f9-206">d.</span></span> <span data-ttu-id="a92f9-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="a92f9-208">Création d’un utilisateur de test BambooHR</span><span class="sxs-lookup"><span data-stu-id="a92f9-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="a92f9-209">Pour permettre aux utilisateurs Azure AD de se connecter à BambooHR, vous devez les attribuer dans BambooHR.</span><span class="sxs-lookup"><span data-stu-id="a92f9-209">To enable Azure AD users to log in to BambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="a92f9-210">En l’occurrence, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="a92f9-210">In the case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="a92f9-211">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a92f9-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a92f9-212">Connectez-vous à votre site **BambooHR** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a92f9-212">Log in to your **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="a92f9-213">Dans la barre d’outils située en haut, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-213">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="a92f9-214">![Paramètre](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Paramètre")</span><span class="sxs-lookup"><span data-stu-id="a92f9-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="a92f9-215">Cliquez sur **Overview**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-215">Click **Overview**.</span></span>

4. <span data-ttu-id="a92f9-216">Dans le volet de navigation de gauche, accédez à **Security \> Users**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-216">In the left navigation pane, go to **Security \> Users**.</span></span>

5. <span data-ttu-id="a92f9-217">Tapez le nom d’utilisateur, le mot de passe et l’adresse e-mail d’un compte AAD valide que vous souhaitez attribuer dans les zones de texte correspondantes.</span><span class="sxs-lookup"><span data-stu-id="a92f9-217">Type the user name, password, and email address of a valid AAD account you want to provision into the related textboxes.</span></span>

6. <span data-ttu-id="a92f9-218">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="a92f9-219">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par BambooHR pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a92f9-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a92f9-220">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a92f9-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a92f9-221">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à BambooHR.</span><span class="sxs-lookup"><span data-stu-id="a92f9-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BambooHR.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a92f9-223">**Pour attribuer Britta Simon à BambooHR, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="a92f9-223">**To assign Britta Simon to BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="a92f9-224">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a92f9-226">Dans la liste des applications, sélectionnez **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-226">In the applications list, select **BambooHR**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="a92f9-228">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a92f9-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-230">Click **Add** button.</span></span> <span data-ttu-id="a92f9-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a92f9-233">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a92f9-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a92f9-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a92f9-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a92f9-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a92f9-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a92f9-236">Testing single sign-on</span></span>

<span data-ttu-id="a92f9-237">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a92f9-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a92f9-238">Lorsque vous cliquez sur la vignette BambooHR dans le volet d’accès, vous devez être connecté automatiquement à votre application BambooHR.</span><span class="sxs-lookup"><span data-stu-id="a92f9-238">When you click the BambooHR tile in the Access Panel, you should get automatically signed-on to your BambooHR application.</span></span>
<span data-ttu-id="a92f9-239">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a92f9-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a92f9-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a92f9-240">Additional resources</span></span>

* [<span data-ttu-id="a92f9-241">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a92f9-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a92f9-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a92f9-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png
