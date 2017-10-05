---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kudos | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 353798fcfd4ad7ce017fc2fddf4110715db3ace2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="d32eb-103">Didacticiel : Intégration d’Azure Active Directory à Kudos</span><span class="sxs-lookup"><span data-stu-id="d32eb-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="d32eb-104">Dans ce didacticiel, vous allez apprendre à intégrer Kudos à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d32eb-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d32eb-105">L’intégration de Kudos à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d32eb-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d32eb-106">Dans Azure AD, vous pouvez contrôler qui a accès à Kudos.</span><span class="sxs-lookup"><span data-stu-id="d32eb-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="d32eb-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Kudos (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d32eb-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d32eb-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d32eb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d32eb-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d32eb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d32eb-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d32eb-110">Prerequisites</span></span>

<span data-ttu-id="d32eb-111">Pour configurer l’intégration d’Azure AD à Kudos, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d32eb-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="d32eb-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d32eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d32eb-113">Un abonnement Kudos pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d32eb-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d32eb-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d32eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d32eb-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d32eb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d32eb-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d32eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d32eb-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d32eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d32eb-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d32eb-118">Scenario description</span></span>
<span data-ttu-id="d32eb-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d32eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d32eb-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d32eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d32eb-121">Ajout de Kudos à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d32eb-121">Adding Kudos from the gallery</span></span>
2. <span data-ttu-id="d32eb-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d32eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="d32eb-123">Ajout de Kudos à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d32eb-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="d32eb-124">Pour configurer l’intégration de Kudos à Azure AD, vous devez ajouter Kudos à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d32eb-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d32eb-125">**Pour ajouter Kudos à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d32eb-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d32eb-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d32eb-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d32eb-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d32eb-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d32eb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d32eb-133">Dans la zone de recherche, tapez **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-133">In the search box, type **Kudos**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="d32eb-135">Dans le panneau de résultats, sélectionnez **Kudos**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d32eb-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d32eb-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d32eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d32eb-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kudos à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d32eb-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d32eb-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Kudos équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d32eb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="d32eb-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Kudos associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="d32eb-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="d32eb-141">Dans Kudos, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="d32eb-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d32eb-142">Pour configurer et tester l’authentification unique Azure AD avec Kudos, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d32eb-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d32eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d32eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d32eb-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d32eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d32eb-145">**[Création d’un utilisateur de test Kudos](#creating-a-kudos-test-user)** pour avoir un équivalent de Britta Simon dans Kudos lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d32eb-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d32eb-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d32eb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d32eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d32eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d32eb-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d32eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d32eb-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Kudos.</span><span class="sxs-lookup"><span data-stu-id="d32eb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="d32eb-150">**Pour configurer l’authentification unique Azure AD avec Kudos, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d32eb-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="d32eb-151">Dans le portail Azure, sur la page d’intégration de l’application **Kudos**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d32eb-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d32eb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="d32eb-155">Dans la section **Kudos Domain and URLs** (Domaine et URL Kudos), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d32eb-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="d32eb-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="d32eb-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="d32eb-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="d32eb-158">This value is not real.</span></span> <span data-ttu-id="d32eb-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="d32eb-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d32eb-160">Contactez [l’équipe de support technique Kudos](http://success.kudosnow.com/home) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="d32eb-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
4. <span data-ttu-id="d32eb-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d32eb-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="d32eb-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d32eb-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d32eb-165">Dans la section **Kudos Configuration** (Configuration de Kudos), cliquez sur **Configure Kudos** (Configurer Kudos) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d32eb-166">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="d32eb-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Kudos en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d32eb-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="d32eb-169">Dans le menu situé en haut, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="d32eb-170">![Paramètres](./media/active-directory-saas-kudos-tutorial/ic787806.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="d32eb-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="d32eb-171">Cliquez sur **Integrations \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="d32eb-172">Dans la section **SSO** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d32eb-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d32eb-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="d32eb-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="d32eb-174">a.</span><span class="sxs-lookup"><span data-stu-id="d32eb-174">a.</span></span> <span data-ttu-id="d32eb-175">Dans la zone de texte **URL de connexion**, collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d32eb-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="d32eb-176">b.</span><span class="sxs-lookup"><span data-stu-id="d32eb-176">b.</span></span> <span data-ttu-id="d32eb-177">Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **X.509 Certificate** .</span><span class="sxs-lookup"><span data-stu-id="d32eb-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="d32eb-178">c.</span><span class="sxs-lookup"><span data-stu-id="d32eb-178">c.</span></span> <span data-ttu-id="d32eb-179">Dans la zone de texte **Logout To URL** (URL de déconnexion), collez la valeur de **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d32eb-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d32eb-180">d.</span><span class="sxs-lookup"><span data-stu-id="d32eb-180">d.</span></span> <span data-ttu-id="d32eb-181">Dans la zone de texte **Your Kudos URL** , tapez le nom de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="d32eb-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="d32eb-182">e.</span><span class="sxs-lookup"><span data-stu-id="d32eb-182">e.</span></span> <span data-ttu-id="d32eb-183">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d32eb-184">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d32eb-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d32eb-185">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d32eb-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d32eb-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d32eb-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d32eb-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d32eb-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="d32eb-188">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d32eb-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d32eb-190">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d32eb-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d32eb-191">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d32eb-193">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d32eb-195">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d32eb-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d32eb-197">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d32eb-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d32eb-199">a.</span><span class="sxs-lookup"><span data-stu-id="d32eb-199">a.</span></span> <span data-ttu-id="d32eb-200">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d32eb-201">b.</span><span class="sxs-lookup"><span data-stu-id="d32eb-201">b.</span></span> <span data-ttu-id="d32eb-202">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d32eb-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d32eb-203">c.</span><span class="sxs-lookup"><span data-stu-id="d32eb-203">c.</span></span> <span data-ttu-id="d32eb-204">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d32eb-205">d.</span><span class="sxs-lookup"><span data-stu-id="d32eb-205">d.</span></span> <span data-ttu-id="d32eb-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="d32eb-207">Création d’un utilisateur de test Kudos</span><span class="sxs-lookup"><span data-stu-id="d32eb-207">Creating a Kudos test user</span></span>

<span data-ttu-id="d32eb-208">Pour pouvoir se connecter à Kudos, les utilisateurs d’Azure Active Directory doivent être approvisionnés dans Kudos.</span><span class="sxs-lookup"><span data-stu-id="d32eb-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="d32eb-209">Dans le cas de Kudos, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="d32eb-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="d32eb-210">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d32eb-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d32eb-211">Connectez-vous à votre site d’entreprise **Kudos** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d32eb-211">Log in to your **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="d32eb-212">Dans le menu situé en haut, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="d32eb-213">![Paramètres](./media/active-directory-saas-kudos-tutorial/ic787806.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="d32eb-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="d32eb-214">Cliquez sur **User Admin**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="d32eb-215">Cliquez sur l’onglet **Utilisateurs**, puis sur **Ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="d32eb-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span><span class="sxs-lookup"><span data-stu-id="d32eb-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="d32eb-217">Dans la section **Add a User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d32eb-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d32eb-218">![Ajouter un utilisateur](./media/active-directory-saas-kudos-tutorial/ic787810.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="d32eb-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="d32eb-219">a.</span><span class="sxs-lookup"><span data-stu-id="d32eb-219">a.</span></span> <span data-ttu-id="d32eb-220">Tapez le prénom, le nom, l’adresse de messagerie et les autres détails d’un compte Azure Active Directory valide que vous souhaitez approvisionner dans les zones de texte correspondantes, à savoir **First Name**, **Last Name** et **Email**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="d32eb-221">b.</span><span class="sxs-lookup"><span data-stu-id="d32eb-221">b.</span></span> <span data-ttu-id="d32eb-222">Cliquez sur **Create User**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="d32eb-223">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Kudos pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d32eb-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d32eb-224">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d32eb-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d32eb-225">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Kudos.</span><span class="sxs-lookup"><span data-stu-id="d32eb-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d32eb-227">**Pour affecter Britta Simon à Kudos, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d32eb-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="d32eb-228">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d32eb-230">Dans la liste des applications, sélectionnez **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-230">In the applications list, select **Kudos**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="d32eb-232">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d32eb-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-234">Click **Add** button.</span></span> <span data-ttu-id="d32eb-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d32eb-237">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d32eb-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d32eb-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d32eb-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d32eb-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d32eb-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d32eb-240">Testing single sign-on</span></span>

<span data-ttu-id="d32eb-241">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d32eb-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d32eb-242">Lorsque vous cliquez sur la vignette Kudos dans le panneau d’accès, vous devez être connecté automatiquement à votre application Kudos.</span><span class="sxs-lookup"><span data-stu-id="d32eb-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="d32eb-243">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d32eb-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d32eb-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d32eb-244">Additional resources</span></span>

* [<span data-ttu-id="d32eb-245">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d32eb-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d32eb-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d32eb-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

