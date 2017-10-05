---
title: "Didacticiel : Intégration d’Azure Active Directory à ClickTime | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="8267a-103">Didacticiel : Intégration d’Azure Active Directory à ClickTime</span><span class="sxs-lookup"><span data-stu-id="8267a-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="8267a-104">Dans ce didacticiel, vous allez apprendre à intégrer ClickTime à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8267a-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8267a-105">L’intégration de ClickTime à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8267a-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8267a-106">Dans Azure AD, vous pouvez contrôler qui a accès à Clicktime</span><span class="sxs-lookup"><span data-stu-id="8267a-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="8267a-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à ClickTime (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="8267a-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8267a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8267a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8267a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8267a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8267a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8267a-110">Prerequisites</span></span>

<span data-ttu-id="8267a-111">Pour configurer l’intégration d’Azure AD avec ClickTime, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8267a-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="8267a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8267a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8267a-113">Un abonnement ClickTime pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8267a-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8267a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8267a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8267a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8267a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8267a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8267a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8267a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8267a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8267a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8267a-118">Scenario description</span></span>
<span data-ttu-id="8267a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8267a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8267a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8267a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8267a-121">Ajout de ClickTime à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8267a-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="8267a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8267a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="8267a-123">Ajout de ClickTime à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8267a-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="8267a-124">Pour configurer l’intégration de ClickTime à Azure AD, vous devez ajouter ClickTime à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="8267a-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8267a-125">**Pour ajouter ClickTime à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="8267a-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8267a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8267a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="8267a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8267a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8267a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8267a-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="8267a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8267a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="8267a-133">Dans la zone de recherche, tapez **ClickTime**, sélectionnez **ClickTime** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8267a-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![ClickTime dans la liste des résultats](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8267a-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8267a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8267a-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ClickTime, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8267a-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8267a-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur ClickTime équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8267a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="8267a-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur ClickTime associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="8267a-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="8267a-139">Dans ClickTime, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="8267a-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8267a-140">Pour configurer et tester l’authentification unique Azure AD avec ClickTime, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="8267a-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8267a-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8267a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8267a-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8267a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8267a-143">**[Création d’un utilisateur de test ClickTime](#create-a-clicktime-test-user)** pour avoir un équivalent de Britta Simon dans ClickTime, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="8267a-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8267a-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8267a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8267a-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8267a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8267a-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8267a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8267a-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application ClickTime.</span><span class="sxs-lookup"><span data-stu-id="8267a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="8267a-148">**Pour configurer l’authentification unique Azure AD avec ClickTime, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8267a-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="8267a-149">Dans le Portail Azure, dans la page d’intégration de l’application **ClickTime**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8267a-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="8267a-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8267a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="8267a-153">Dans la section **Domaine et URL ClickTime**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8267a-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="8267a-155">a.</span><span class="sxs-lookup"><span data-stu-id="8267a-155">a.</span></span> <span data-ttu-id="8267a-156">Dans la zone de texte **Identificateur**, tapez une URL comme : `https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="8267a-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="8267a-157">b.</span><span class="sxs-lookup"><span data-stu-id="8267a-157">b.</span></span> <span data-ttu-id="8267a-158">Dans la zone de texte **URL de réponse** , tapez une URL en respectant les formats suivants :</span><span class="sxs-lookup"><span data-stu-id="8267a-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="8267a-159">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8267a-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="8267a-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8267a-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8267a-163">Dans la section **Configuration de ClickTime**, cliquez sur **Configurer ClickTime** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="8267a-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8267a-164">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8267a-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="8267a-166">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise ClickTime en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8267a-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="8267a-167">Dans la barre d’outils située en haut, cliquez sur **Preferences**, puis sur **Security Settings**.</span><span class="sxs-lookup"><span data-stu-id="8267a-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="8267a-168">Dans la section de configuration **Single Sign-On Preferences** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8267a-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="8267a-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span><span class="sxs-lookup"><span data-stu-id="8267a-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="8267a-170">a.</span><span class="sxs-lookup"><span data-stu-id="8267a-170">a.</span></span>  <span data-ttu-id="8267a-171">Sélectionnez **Autoriser** la connexion à l’aide de l’authentification unique (SSO) avec **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="8267a-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="8267a-172">b.</span><span class="sxs-lookup"><span data-stu-id="8267a-172">b.</span></span> <span data-ttu-id="8267a-173">Dans la zone de texte **Identity Provider Endpoint** (Point de terminaison du fournisseur d’identité), collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8267a-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="8267a-174">c.</span><span class="sxs-lookup"><span data-stu-id="8267a-174">c.</span></span>  <span data-ttu-id="8267a-175">Dans le **Bloc-notes**, ouvrez le **certificat codé en base 64** téléchargé dans le portail Azure, copiez son contenu, puis collez-le dans la zone de texte **X.509 Certificate** (Certificat X.509).</span><span class="sxs-lookup"><span data-stu-id="8267a-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="8267a-176">d.</span><span class="sxs-lookup"><span data-stu-id="8267a-176">d.</span></span>  <span data-ttu-id="8267a-177">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8267a-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8267a-178">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="8267a-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8267a-179">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="8267a-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8267a-180">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8267a-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8267a-181">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8267a-181">Create an Azure AD test user</span></span>
<span data-ttu-id="8267a-182">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8267a-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="8267a-184">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8267a-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8267a-185">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8267a-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8267a-187">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8267a-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8267a-189">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8267a-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8267a-191">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8267a-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8267a-193">a.</span><span class="sxs-lookup"><span data-stu-id="8267a-193">a.</span></span> <span data-ttu-id="8267a-194">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8267a-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8267a-195">b.</span><span class="sxs-lookup"><span data-stu-id="8267a-195">b.</span></span> <span data-ttu-id="8267a-196">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8267a-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8267a-197">c.</span><span class="sxs-lookup"><span data-stu-id="8267a-197">c.</span></span> <span data-ttu-id="8267a-198">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8267a-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8267a-199">d.</span><span class="sxs-lookup"><span data-stu-id="8267a-199">d.</span></span> <span data-ttu-id="8267a-200">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8267a-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="8267a-201">Créer un utilisateur de test ClickTime</span><span class="sxs-lookup"><span data-stu-id="8267a-201">Create a ClickTime test user</span></span>

<span data-ttu-id="8267a-202">Pour se connecter à ClickTime, les utilisateurs d’Azure AD doivent être approvisionnés dans ClickTime.</span><span class="sxs-lookup"><span data-stu-id="8267a-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="8267a-203">Dans le cas de ClickTime, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="8267a-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="8267a-204">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur fourni par ClickTime pour approvisionner des comptes d’utilisateurs Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8267a-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="8267a-205">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8267a-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="8267a-206">Connectez-vous à votre client **ClickTime** .</span><span class="sxs-lookup"><span data-stu-id="8267a-206">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="8267a-207">Dans la barre d’outils située en haut, cliquez sur **Company**, puis sur **People**.</span><span class="sxs-lookup"><span data-stu-id="8267a-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="8267a-208">![Personnes](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="8267a-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="8267a-209">Cliquez sur **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="8267a-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="8267a-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span><span class="sxs-lookup"><span data-stu-id="8267a-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="8267a-211">Dans la section New Person, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8267a-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="8267a-212">![Personnes](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="8267a-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="8267a-213">a.</span><span class="sxs-lookup"><span data-stu-id="8267a-213">a.</span></span>  <span data-ttu-id="8267a-214">Dans la zone de texte **Full Name** (Nom complet), tapez le nom complet d’un utilisateur, par exemple, **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8267a-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="8267a-215">b.</span><span class="sxs-lookup"><span data-stu-id="8267a-215">b.</span></span>  <span data-ttu-id="8267a-216">Dans la zone de texte **Email address** (Adresse e-mail), tapez l’adresse e-mail d’un utilisateur, par exemple, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8267a-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="8267a-217">Si vous le souhaitez, vous pouvez définir d’autres propriétés relatives à l’objet de la nouvelle personne.</span><span class="sxs-lookup"><span data-stu-id="8267a-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="8267a-218">c.</span><span class="sxs-lookup"><span data-stu-id="8267a-218">c.</span></span>  <span data-ttu-id="8267a-219">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8267a-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8267a-220">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8267a-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="8267a-221">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à ClickTime.</span><span class="sxs-lookup"><span data-stu-id="8267a-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![Attribuer le rôle utilisateur][200] 

<span data-ttu-id="8267a-223">**Pour attribuer Britta Simon à ClickTime, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="8267a-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="8267a-224">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8267a-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8267a-226">Dans la liste des applications, sélectionnez **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="8267a-226">In the applications list, select **ClickTime**.</span></span>

    ![Lien ClickTime dans la liste des applications](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="8267a-228">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8267a-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="8267a-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8267a-230">Click **Add** button.</span></span> <span data-ttu-id="8267a-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8267a-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="8267a-233">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8267a-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8267a-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8267a-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8267a-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8267a-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8267a-236">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8267a-236">Test single sign-on</span></span>

<span data-ttu-id="8267a-237">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8267a-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8267a-238">Quand vous cliquez sur la vignette ClickTime dans le volet d’accès, vous devez être connecté automatiquement à votre application ClickTime.</span><span class="sxs-lookup"><span data-stu-id="8267a-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="8267a-239">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8267a-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8267a-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8267a-240">Additional resources</span></span>

* [<span data-ttu-id="8267a-241">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8267a-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8267a-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8267a-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

