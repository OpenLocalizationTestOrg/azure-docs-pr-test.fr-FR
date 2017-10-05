---
title: "Didacticiel : Intégration d’Azure Active Directory avec LockPath Keylight | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e64a966f24411818abc4cc4ab29a428b5577d012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="70df2-103">Didacticiel : Intégration d’Azure Active Directory avec LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="70df2-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="70df2-104">Dans ce didacticiel, vous allez apprendre à intégrer LockPath Keylight avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70df2-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70df2-105">L’intégration de LockPath Keylight avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="70df2-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="70df2-106">Dans Azure AD, vous pouvez contrôler qui a accès à LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="70df2-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="70df2-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à LockPath Keylight (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70df2-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70df2-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="70df2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="70df2-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70df2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70df2-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="70df2-110">Prerequisites</span></span>

<span data-ttu-id="70df2-111">Pour configurer l’intégration d’Azure AD avec LockPath Keylight, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="70df2-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="70df2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="70df2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70df2-113">Un abonnement LockPath Keylight pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="70df2-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70df2-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="70df2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70df2-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="70df2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70df2-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="70df2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70df2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70df2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70df2-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="70df2-118">Scenario description</span></span>
<span data-ttu-id="70df2-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="70df2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70df2-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="70df2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70df2-121">Ajout de LockPath Keylight à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="70df2-121">Adding LockPath Keylight from the gallery</span></span>
2. <span data-ttu-id="70df2-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70df2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="70df2-123">Ajout de LockPath Keylight à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="70df2-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="70df2-124">Pour configurer l’intégration de LockPath Keylight à Azure AD, vous devez ajouter LockPath Keylight à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="70df2-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="70df2-125">**Pour ajouter LockPath Keylight à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70df2-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="70df2-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70df2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70df2-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="70df2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="70df2-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="70df2-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="70df2-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="70df2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="70df2-133">Dans la zone de recherche, tapez **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="70df2-133">In the search box, type **LockPath Keylight**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="70df2-135">Dans le volet de résultats, sélectionnez **LockPath Keylight**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="70df2-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70df2-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70df2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70df2-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LockPath Keylight sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="70df2-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70df2-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LockPath Keylight équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70df2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="70df2-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur LockPath Keylight associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="70df2-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="70df2-141">Dans LockPath Keylight, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="70df2-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="70df2-142">Pour configurer et tester l’authentification unique Azure AD avec LockPath Keylight, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="70df2-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="70df2-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="70df2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="70df2-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70df2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70df2-145">**[Création d’un utilisateur de test LockPath Keylight](#creating-a-lockpath-keylight-test-user)** pour avoir un équivalent de Britta Simon dans LockPath Keylight lié à sa représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="70df2-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="70df2-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70df2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70df2-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="70df2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70df2-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70df2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70df2-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="70df2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="70df2-150">**Pour configurer l’authentification unique Azure AD avec LockPath Keylight, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70df2-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="70df2-151">Dans le portail Azure, sur la page d’intégration de l’application **LockPath Keylight**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="70df2-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="70df2-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="70df2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="70df2-155">Dans la section **Domaine et URL LockPath Keylight**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="70df2-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="70df2-157">a.</span><span class="sxs-lookup"><span data-stu-id="70df2-157">a.</span></span> <span data-ttu-id="70df2-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="70df2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="70df2-159">b.</span><span class="sxs-lookup"><span data-stu-id="70df2-159">b.</span></span> <span data-ttu-id="70df2-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="70df2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="70df2-161">c.</span><span class="sxs-lookup"><span data-stu-id="70df2-161">c.</span></span> <span data-ttu-id="70df2-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="70df2-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="70df2-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="70df2-163">These values are not real.</span></span> <span data-ttu-id="70df2-164">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="70df2-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="70df2-165">Pour obtenir ces valeurs, contactez l’[équipe de support technique LockPath Keylight](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="70df2-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

4. <span data-ttu-id="70df2-166">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="70df2-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="70df2-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="70df2-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="70df2-170">Dans la section **Configuration de LockPath Keylight**, cliquez sur **Configurer LockPath Keylight** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="70df2-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="70df2-171">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="70df2-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="70df2-173">Pour activer l’authentification unique dans LockPath Keylight, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="70df2-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="70df2-174">a.</span><span class="sxs-lookup"><span data-stu-id="70df2-174">a.</span></span> <span data-ttu-id="70df2-175">Connectez-vous à votre compte LockPath Keylight en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="70df2-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="70df2-176">b.</span><span class="sxs-lookup"><span data-stu-id="70df2-176">b.</span></span> <span data-ttu-id="70df2-177">Dans le menu situé en haut, cliquez sur **Person** (Personne), puis sélectionnez **Keylight Setup** (Installation de Keylight).</span><span class="sxs-lookup"><span data-stu-id="70df2-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="70df2-179">c.</span><span class="sxs-lookup"><span data-stu-id="70df2-179">c.</span></span> <span data-ttu-id="70df2-180">Dans l’arborescence sur la gauche, cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="70df2-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="70df2-182">d.</span><span class="sxs-lookup"><span data-stu-id="70df2-182">d.</span></span> <span data-ttu-id="70df2-183">Dans la boîte de dialogue **SAML Settings** (Paramètres SAML), cliquez sur **Edit** (Modifier).</span><span class="sxs-lookup"><span data-stu-id="70df2-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="70df2-185">Dans la page de boîte de dialogue **Edit SAML Settings** (Modifier les paramètres SAML), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="70df2-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="70df2-187">a.</span><span class="sxs-lookup"><span data-stu-id="70df2-187">a.</span></span> <span data-ttu-id="70df2-188">Affectez à **SAML authentication** (Authentication SAML) la valeur **Active**.</span><span class="sxs-lookup"><span data-stu-id="70df2-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="70df2-189">b.</span><span class="sxs-lookup"><span data-stu-id="70df2-189">b.</span></span> <span data-ttu-id="70df2-190">Collez la valeur **URL du service d’authentification unique SAML** copiée dans le portail Azure dans la zone de texte **Identity Provider Login URL (URL de connexion du fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="70df2-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="70df2-191">c.</span><span class="sxs-lookup"><span data-stu-id="70df2-191">c.</span></span> <span data-ttu-id="70df2-192">Collez la valeur **URL du service d’authentification unique** copiée dans le portail Azure dans la zone de texte **Identity Provider Logout URL (URL de déconnexion du fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="70df2-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="70df2-193">d.</span><span class="sxs-lookup"><span data-stu-id="70df2-193">d.</span></span> <span data-ttu-id="70df2-194">Cliquez sur **Choose File** (Choisir un fichier) pour sélectionner votre certificat LockPath Keylight téléchargé, puis sur **Ouvrir** pour charger le certificat.</span><span class="sxs-lookup"><span data-stu-id="70df2-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="70df2-195">e.</span><span class="sxs-lookup"><span data-stu-id="70df2-195">e.</span></span> <span data-ttu-id="70df2-196">Affectez à **SAML User Id location** (Emplacement de l’ID utilisateur SAML) la valeur **NameIdentifier element of the subject statement** (Élément NameIdentifier de l’instruction Subject).</span><span class="sxs-lookup"><span data-stu-id="70df2-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="70df2-197">f.</span><span class="sxs-lookup"><span data-stu-id="70df2-197">f.</span></span> <span data-ttu-id="70df2-198">Indiquez la valeur **Keylight Service Provider** (Fournisseur de service Keylight) au format suivant : **https://&lt;Nom société&gt;.keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="70df2-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="70df2-199">g.</span><span class="sxs-lookup"><span data-stu-id="70df2-199">g.</span></span> <span data-ttu-id="70df2-200">Affectez à **Auto-provision users** (Configuration automatique des utilisateurs) la valeur **Active**.</span><span class="sxs-lookup"><span data-stu-id="70df2-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="70df2-201">h.</span><span class="sxs-lookup"><span data-stu-id="70df2-201">h.</span></span> <span data-ttu-id="70df2-202">Affectez à **Auto-provision account type** (Configuration automatique du type de compte) la valeur **Full User** (Utilisateur global).</span><span class="sxs-lookup"><span data-stu-id="70df2-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="70df2-203">i.</span><span class="sxs-lookup"><span data-stu-id="70df2-203">i.</span></span> <span data-ttu-id="70df2-204">Définissez **Auto-provision security role** (Configuration automatique du rôle de sécurité), sélectionnez **Standard User with SAML** (Utilisateur standard avec SAML).</span><span class="sxs-lookup"><span data-stu-id="70df2-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="70df2-205">j.</span><span class="sxs-lookup"><span data-stu-id="70df2-205">j.</span></span> <span data-ttu-id="70df2-206">Définissez **Auto-provision security config** (Configuration automatique des paramètres de sécurité), sélectionnez **Standard User Configuration** (Configuration utilisateur standard).</span><span class="sxs-lookup"><span data-stu-id="70df2-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="70df2-207">k.</span><span class="sxs-lookup"><span data-stu-id="70df2-207">k.</span></span> <span data-ttu-id="70df2-208">Dans la zone de texte **Email Attribute** (Attribut d’e-mail), entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="70df2-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="70df2-209">l.</span><span class="sxs-lookup"><span data-stu-id="70df2-209">l.</span></span> <span data-ttu-id="70df2-210">Dans la zone de texte **First name attribute** (Attribut de prénom), entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="70df2-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="70df2-211">m.</span><span class="sxs-lookup"><span data-stu-id="70df2-211">m.</span></span> <span data-ttu-id="70df2-212">Dans la zone de texte **Last name attribute** (Attribut de nom), entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="70df2-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="70df2-213">n.</span><span class="sxs-lookup"><span data-stu-id="70df2-213">n.</span></span> <span data-ttu-id="70df2-214">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="70df2-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="70df2-215">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="70df2-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="70df2-216">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="70df2-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="70df2-217">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70df2-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70df2-218">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="70df2-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="70df2-219">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="70df2-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="70df2-221">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70df2-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="70df2-222">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70df2-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70df2-224">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="70df2-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70df2-226">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="70df2-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70df2-228">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="70df2-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70df2-230">a.</span><span class="sxs-lookup"><span data-stu-id="70df2-230">a.</span></span> <span data-ttu-id="70df2-231">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70df2-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70df2-232">b.</span><span class="sxs-lookup"><span data-stu-id="70df2-232">b.</span></span> <span data-ttu-id="70df2-233">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70df2-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70df2-234">c.</span><span class="sxs-lookup"><span data-stu-id="70df2-234">c.</span></span> <span data-ttu-id="70df2-235">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="70df2-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="70df2-236">d.</span><span class="sxs-lookup"><span data-stu-id="70df2-236">d.</span></span> <span data-ttu-id="70df2-237">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="70df2-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="70df2-238">Création d’un utilisateur de test LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="70df2-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="70df2-239">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="70df2-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="70df2-240">LockPath Keylight prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="70df2-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="70df2-241">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="70df2-241">There is no action item for you in this section.</span></span> <span data-ttu-id="70df2-242">Un utilisateur est créé lors de l’accès à LockPath Keylight si l’utilisateur n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="70df2-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="70df2-243">Si vous devez créer un utilisateur manuellement, contactez l’[équipe de support technique LockPath Keylight](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="70df2-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="70df2-244">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="70df2-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="70df2-245">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="70df2-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="70df2-247">**Pour affecter Britta Simon à LockPath Keylight, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70df2-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="70df2-248">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="70df2-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="70df2-250">Dans la liste des applications, sélectionnez **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="70df2-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="70df2-252">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="70df2-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="70df2-254">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="70df2-254">Click **Add** button.</span></span> <span data-ttu-id="70df2-255">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="70df2-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="70df2-257">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="70df2-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="70df2-258">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="70df2-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70df2-259">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="70df2-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70df2-260">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="70df2-260">Testing single sign-on</span></span>

<span data-ttu-id="70df2-261">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="70df2-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="70df2-262">Quand vous cliquez sur la vignette LockPath Keylight dans le volet d’accès, vous devez être connecté automatiquement à votre application LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="70df2-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="70df2-263">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="70df2-263">Additional resources</span></span>

* [<span data-ttu-id="70df2-264">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70df2-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70df2-265">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="70df2-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

