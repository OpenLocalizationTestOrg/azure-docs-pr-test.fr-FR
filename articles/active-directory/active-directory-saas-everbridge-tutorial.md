---
title: "Didacticiel : Intégration d’Azure Active Directory à EverBridge | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: f5a97fc8df978dd55a73ae53516a82f884c14bec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="dd52e-103">Didacticiel : Intégration d’Azure Active Directory à Everbridge</span><span class="sxs-lookup"><span data-stu-id="dd52e-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="dd52e-104">Dans ce didacticiel, vous allez apprendre à intégrer EverBridge à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd52e-104">In this tutorial, you learn how to integrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd52e-105">L’intégration d’EverBridge à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dd52e-105">Integrating EverBridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dd52e-106">Dans Azure AD, vous pouvez contrôler qui a accès à EverBridge</span><span class="sxs-lookup"><span data-stu-id="dd52e-106">You can control in Azure AD who has access to EverBridge</span></span>
- <span data-ttu-id="dd52e-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à EverBridge (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd52e-107">You can enable your users to automatically get signed-on to EverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd52e-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd52e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dd52e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd52e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd52e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dd52e-110">Prerequisites</span></span>

<span data-ttu-id="dd52e-111">Pour configurer l’intégration d’Azure AD à EverBridge, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dd52e-111">To configure Azure AD integration with EverBridge, you need the following items:</span></span>

- <span data-ttu-id="dd52e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd52e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd52e-113">Un abonnement EverBridge pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dd52e-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd52e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dd52e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd52e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="dd52e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd52e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dd52e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd52e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd52e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd52e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dd52e-118">Scenario description</span></span>
<span data-ttu-id="dd52e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dd52e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd52e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd52e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd52e-121">Ajout d’EverBridge à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="dd52e-121">Adding EverBridge from the gallery</span></span>
2. <span data-ttu-id="dd52e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd52e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-the-gallery"></a><span data-ttu-id="dd52e-123">Ajout d’EverBridge à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="dd52e-123">Adding EverBridge from the gallery</span></span>
<span data-ttu-id="dd52e-124">Pour configurer l’intégration d’EverBridge à Azure AD, vous devez ajouter EverBridge à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dd52e-124">To configure the integration of EverBridge into Azure AD, you need to add EverBridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dd52e-125">**Pour ajouter EverBridge à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd52e-125">**To add EverBridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dd52e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd52e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dd52e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dd52e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd52e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dd52e-133">Dans la zone de recherche, tapez **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-133">In the search box, type **EverBridge**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="dd52e-135">Dans le panneau de résultats, sélectionnez **EverBridge**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="dd52e-135">In the results panel, select **EverBridge**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd52e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd52e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd52e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec EverBridge à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dd52e-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd52e-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur EverBridge équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd52e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EverBridge is to a user in Azure AD.</span></span> <span data-ttu-id="dd52e-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur EverBridge associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="dd52e-140">In other words, a link relationship between an Azure AD user and the related user in EverBridge needs to be established.</span></span>

<span data-ttu-id="dd52e-141">Dans EverBridge, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="dd52e-141">In EverBridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dd52e-142">Pour configurer et tester l’authentification unique Azure AD avec EverBridge, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd52e-142">To configure and test Azure AD single sign-on with EverBridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dd52e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dd52e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dd52e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd52e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd52e-145">**[Création d’un utilisateur de test EverBridge](#creating-an-everbridge-test-user)** pour avoir un équivalent de Britta Simon dans EverBridge lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd52e-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - to have a counterpart of Britta Simon in EverBridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd52e-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd52e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd52e-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="dd52e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd52e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd52e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd52e-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application EverBridge.</span><span class="sxs-lookup"><span data-stu-id="dd52e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="dd52e-150">**Pour configurer l’authentification unique Azure AD avec EverBridge, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd52e-150">**To configure Azure AD single sign-on with EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="dd52e-151">Dans le portail Azure, sur la page d’intégration de l’application **EverBridge**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-151">In the Azure portal, on the **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dd52e-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd52e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="dd52e-155">Dans la section **EverBridge Domain and URLs** (Domaine et URL EverBridge), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd52e-155">On the **EverBridge Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="dd52e-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd52e-157">a.</span></span> <span data-ttu-id="dd52e-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="dd52e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="dd52e-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd52e-159">b.</span></span> <span data-ttu-id="dd52e-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="dd52e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dd52e-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="dd52e-161">These values are not real.</span></span> <span data-ttu-id="dd52e-162">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="dd52e-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="dd52e-163">Contactez [l’équipe de support technique EverBridge](mailto:support@everbridge.com) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="dd52e-163">Contact [EverBridge support team](mailto:support@everbridge.com) to get these values.</span></span>
 
4. <span data-ttu-id="dd52e-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dd52e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="dd52e-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dd52e-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd52e-168">Dans la section **EverBridge Configuration** (Configuration d’EverBridge), cliquez sur **Configure EverBridge** (Configurer EverBridge) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-168">On the **EverBridge Configuration** section, click **Configure EverBridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dd52e-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="dd52e-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="dd52e-171">Pour que l’authentification unique soit configurée pour votre application, vous devez vous connecter à votre locataire Everbridge en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd52e-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="dd52e-172">Dans le menu situé en haut, cliquez sur l’onglet **Paramètres** et sélectionnez **Authentification unique** sous **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="dd52e-174">a.</span><span class="sxs-lookup"><span data-stu-id="dd52e-174">a.</span></span> <span data-ttu-id="dd52e-175">Dans la zone de texte **Nom**, entrez le nom du fournisseur d’identificateurs (par exemple : le nom de votre entreprise).</span><span class="sxs-lookup"><span data-stu-id="dd52e-175">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="dd52e-176">b.</span><span class="sxs-lookup"><span data-stu-id="dd52e-176">b.</span></span> <span data-ttu-id="dd52e-177">Dans la zone de texte **nom de l’API** , saisissez le nom de l’API.</span><span class="sxs-lookup"><span data-stu-id="dd52e-177">In the **API Name** textbox, type the name of API.</span></span>
   
    <span data-ttu-id="dd52e-178">c.</span><span class="sxs-lookup"><span data-stu-id="dd52e-178">c.</span></span> <span data-ttu-id="dd52e-179">Cliquez sur le bouton **Choisir un fichier** pour charger le fichier de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd52e-179">Click **Choose File** button to upload the metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="dd52e-180">d.</span><span class="sxs-lookup"><span data-stu-id="dd52e-180">d.</span></span> <span data-ttu-id="dd52e-181">Dans SAML Identity Location (Emplacement de l’identité SAML), sélectionnez **Identity is in the NameIdentifier element of the Subject statement** (L’identité figure dans l’élément NameIdentifier de l’instruction Subject).</span><span class="sxs-lookup"><span data-stu-id="dd52e-181">In the SAML Identity Location, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
   
    <span data-ttu-id="dd52e-182">e.</span><span class="sxs-lookup"><span data-stu-id="dd52e-182">e.</span></span> <span data-ttu-id="dd52e-183">Dans la zone de texte **URL du fournisseur d’identité**, collez la valeur de l’URL SSO SAML depuis Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd52e-183">In the **Identity Provider Login URL** textbox, paste the value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="dd52e-185">f.</span><span class="sxs-lookup"><span data-stu-id="dd52e-185">f.</span></span> <span data-ttu-id="dd52e-186">Dans Liaison de demande initiée par le fournisseur de service, sélectionnez **Redirection HTTP**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-186">In the Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="dd52e-187">g.</span><span class="sxs-lookup"><span data-stu-id="dd52e-187">g.</span></span> <span data-ttu-id="dd52e-188">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="dd52e-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="dd52e-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dd52e-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="dd52e-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dd52e-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd52e-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd52e-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd52e-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd52e-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd52e-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dd52e-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd52e-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dd52e-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd52e-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd52e-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd52e-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd52e-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd52e-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd52e-204">a.</span><span class="sxs-lookup"><span data-stu-id="dd52e-204">a.</span></span> <span data-ttu-id="dd52e-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd52e-206">b.</span><span class="sxs-lookup"><span data-stu-id="dd52e-206">b.</span></span> <span data-ttu-id="dd52e-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd52e-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd52e-208">c.</span><span class="sxs-lookup"><span data-stu-id="dd52e-208">c.</span></span> <span data-ttu-id="dd52e-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dd52e-210">d.</span><span class="sxs-lookup"><span data-stu-id="dd52e-210">d.</span></span> <span data-ttu-id="dd52e-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="dd52e-212">Création d’un utilisateur de test EverBridge</span><span class="sxs-lookup"><span data-stu-id="dd52e-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="dd52e-213">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Everbridge.</span><span class="sxs-lookup"><span data-stu-id="dd52e-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="dd52e-214">Travaillez avec [l’équipe de support technique EverBridge](mailto:support@everbridge.com) pour ajouter les utilisateurs à la plateforme EverBridge.</span><span class="sxs-lookup"><span data-stu-id="dd52e-214">Work with [EverBridge support team](mailto:support@everbridge.com) to add the users in the Everbridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dd52e-215">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd52e-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dd52e-216">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à EverBridge.</span><span class="sxs-lookup"><span data-stu-id="dd52e-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EverBridge.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dd52e-218">**Pour attribuer Britta Simon à EverBridge, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd52e-218">**To assign Britta Simon to EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="dd52e-219">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dd52e-221">Dans la liste des applications, sélectionnez **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-221">In the applications list, select **EverBridge**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="dd52e-223">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dd52e-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-225">Click **Add** button.</span></span> <span data-ttu-id="dd52e-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dd52e-228">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dd52e-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dd52e-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd52e-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd52e-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd52e-231">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dd52e-231">Testing single sign-on</span></span>

<span data-ttu-id="dd52e-232">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="dd52e-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dd52e-233">Lorsque vous cliquez sur la vignette Everbridge dans le volet d’accès, vous devez être connecté automatiquement à votre application Everbridge.</span><span class="sxs-lookup"><span data-stu-id="dd52e-233">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd52e-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dd52e-234">Additional resources</span></span>

* [<span data-ttu-id="dd52e-235">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd52e-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd52e-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dd52e-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

