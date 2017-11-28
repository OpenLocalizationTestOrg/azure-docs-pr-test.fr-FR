---
title: "Didacticiel : Intégration d’Azure Active Directory à Syncplicity | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="4f775-103">Didacticiel : Intégration d’Azure Active Directory à Syncplicity</span><span class="sxs-lookup"><span data-stu-id="4f775-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="4f775-104">Dans ce didacticiel, vous allez apprendre à intégrer Syncplicity à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4f775-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4f775-105">L’intégration de Syncplicity dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4f775-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4f775-106">Dans Azure AD, vous pouvez contrôler qui a accès à Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="4f775-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="4f775-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Syncplicity (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f775-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4f775-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="4f775-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4f775-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4f775-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f775-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4f775-110">Prerequisites</span></span>

<span data-ttu-id="4f775-111">Pour configurer l’intégration d’Azure AD à Syncplicity, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4f775-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="4f775-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f775-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4f775-113">Un abonnement Syncplicity pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4f775-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4f775-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4f775-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4f775-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4f775-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4f775-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4f775-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4f775-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4f775-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4f775-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4f775-118">Scenario description</span></span>
<span data-ttu-id="4f775-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4f775-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4f775-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f775-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4f775-121">Ajout de Syncplicity à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4f775-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="4f775-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f775-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="4f775-123">Ajout de Syncplicity à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4f775-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="4f775-124">Pour configurer l’intégration de Syncplicity à Azure AD, vous devez ajouter Syncplicity à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4f775-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4f775-125">**Pour ajouter Syncplicity à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f775-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f775-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4f775-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4f775-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4f775-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4f775-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4f775-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4f775-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4f775-133">Dans la zone de recherche, tapez **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="4f775-133">In the search box, type **Syncplicity**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="4f775-135">Dans le panneau de résultats, sélectionnez **Syncplicity**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="4f775-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4f775-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f775-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4f775-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Syncplicity à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4f775-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4f775-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Syncplicity équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f775-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="4f775-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Syncplicity associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="4f775-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="4f775-141">Dans Syncplicity, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="4f775-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4f775-142">Pour configurer et tester l’authentification unique Azure AD avec Syncplicity, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f775-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4f775-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4f775-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4f775-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f775-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4f775-145">**[Création d’un utilisateur de test Syncplicity](#creating-a-syncplicity-test-user)** pour avoir un équivalent de Britta Simon dans Syncplicity lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f775-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4f775-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f775-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4f775-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4f775-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4f775-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f775-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4f775-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="4f775-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="4f775-150">**Pour configurer l’authentification unique Azure AD avec Syncplicity, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f775-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-151">Dans le portail Azure, sur la page d’intégration de l’application **Syncplicity**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4f775-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4f775-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4f775-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="4f775-155">Dans la section **Syncplicity Domain and URLs** (Domaine et URL Syncplicity), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f775-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="4f775-157">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-157">a.</span></span> <span data-ttu-id="4f775-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="4f775-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="4f775-159">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-159">b.</span></span> <span data-ttu-id="4f775-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="4f775-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4f775-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4f775-161">These values are not real.</span></span> <span data-ttu-id="4f775-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="4f775-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4f775-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Syncplicity](https://www.syncplicity.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="4f775-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="4f775-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4f775-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="4f775-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4f775-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4f775-168">Dans la section **Syncplicity Configuration** (Configuration de Syncplicity), cliquez sur **Configure Syncplicity** (Configurer Syncplicity) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="4f775-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4f775-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4f775-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="4f775-171">Connectez-vous à votre locataire **Syncplicity** .</span><span class="sxs-lookup"><span data-stu-id="4f775-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="4f775-172">Dans le menu en haut, cliquez sur **admin**, sélectionnez **settings**, puis cliquez sur **Custom domain and single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4f775-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="4f775-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="4f775-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="4f775-174">Dans la boîte de dialogue **Single Sign on (SSO)** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f775-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="4f775-175">![Authentification unique \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="4f775-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="4f775-176">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-176">a.</span></span> <span data-ttu-id="4f775-177">Dans la zone de texte **Custom Domain** , entrez le nom de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="4f775-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="4f775-178">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-178">b.</span></span> <span data-ttu-id="4f775-179">Sélectionnez **Enabled** dans **Single Sign-On Status**.</span><span class="sxs-lookup"><span data-stu-id="4f775-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="4f775-180">c.</span><span class="sxs-lookup"><span data-stu-id="4f775-180">c.</span></span> <span data-ttu-id="4f775-181">Dans la zone de texte **ID d’entité**, collez la valeur de **l’ID d’entité SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4f775-182">d.</span><span class="sxs-lookup"><span data-stu-id="4f775-182">d.</span></span> <span data-ttu-id="4f775-183">Dans la zone de texte **URL de la page de connexion**, collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4f775-184">e.</span><span class="sxs-lookup"><span data-stu-id="4f775-184">e.</span></span> <span data-ttu-id="4f775-185">Dans la zone de texte **Logout page URL** (URL de la page de déconnexion), collez la valeur de **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4f775-186">f.</span><span class="sxs-lookup"><span data-stu-id="4f775-186">f.</span></span> <span data-ttu-id="4f775-187">Dans **Certificat du fournisseur d’identité**, cliquez sur **Choisir un fichier**, puis chargez le certificat que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="4f775-188">g.</span><span class="sxs-lookup"><span data-stu-id="4f775-188">g.</span></span> <span data-ttu-id="4f775-189">Cliquez sur **ENREGISTRER LES MODIFICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="4f775-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="4f775-190">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="4f775-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4f775-191">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="4f775-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4f775-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4f775-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4f775-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f775-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="4f775-194">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4f775-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4f775-196">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f775-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-197">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f775-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4f775-199">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4f775-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4f775-201">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4f775-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4f775-203">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f775-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4f775-205">a.</span><span class="sxs-lookup"><span data-stu-id="4f775-205">a.</span></span> <span data-ttu-id="4f775-206">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4f775-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4f775-207">b.</span><span class="sxs-lookup"><span data-stu-id="4f775-207">b.</span></span> <span data-ttu-id="4f775-208">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4f775-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4f775-209">c.</span><span class="sxs-lookup"><span data-stu-id="4f775-209">c.</span></span> <span data-ttu-id="4f775-210">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4f775-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4f775-211">d.</span><span class="sxs-lookup"><span data-stu-id="4f775-211">d.</span></span> <span data-ttu-id="4f775-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4f775-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="4f775-213">Création d’un utilisateur de test Syncplicity</span><span class="sxs-lookup"><span data-stu-id="4f775-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="4f775-214">Pour que les utilisateurs AAD puissent se connecter, ils doivent être approvisionnés dans l’application Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="4f775-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="4f775-215">Cette section décrit comment créer des comptes d’utilisateur AAD dans Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="4f775-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="4f775-216">**Pour approvisionner un compte d’utilisateur dans Syncplicity, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f775-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-217">Connectez-vous à votre locataire **Syncplicity** (par exemple : `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="4f775-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="4f775-218">Cliquez sur **admin** et sélectionnez **	Comptes d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="4f775-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="4f775-219">Cliquez sur **AJOUTER UN UTILISATEUR**.</span><span class="sxs-lookup"><span data-stu-id="4f775-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="4f775-220">![Gestion des utilisateurs](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="4f775-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="4f775-221">Entrez **l’adresse e-mail** d’un compte AAD que vous souhaitez approvisionner, sélectionnez **Utilisateur** pour **Rôle**, puis cliquez sur **SUIVANT**.</span><span class="sxs-lookup"><span data-stu-id="4f775-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="4f775-222">![Informations du compte](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Informations du compte")</span><span class="sxs-lookup"><span data-stu-id="4f775-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="4f775-223">Le détenteur du compte AAD reçoit un message électronique contenant un lien pour confirmer et activer le compte.</span><span class="sxs-lookup"><span data-stu-id="4f775-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="4f775-224">Sélectionnez un groupe dans votre société dont votre nouvel utilisateur doit devenir membre, puis cliquez sur **SUIVANT**.</span><span class="sxs-lookup"><span data-stu-id="4f775-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="4f775-225">![Appartenance de groupe](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Appartenance de groupe")</span><span class="sxs-lookup"><span data-stu-id="4f775-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="4f775-226">Si aucun groupe n’est répertorié, cliquez sur **SUIVANT**.</span><span class="sxs-lookup"><span data-stu-id="4f775-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="4f775-227">Sélectionnez les dossiers que vous souhaitez placer sous le contrôle de Syncplicity sur l’ordinateur de l’utilisateur, puis cliquez sur **SUIVANT**.</span><span class="sxs-lookup"><span data-stu-id="4f775-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="4f775-228">![Dossiers Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Dossiers Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="4f775-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="4f775-229">Vous pouvez utiliser n’importe quel outil ou API de création de compte d’utilisateur, fourni par Syncplicity, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="4f775-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4f775-230">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f775-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4f775-231">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="4f775-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4f775-233">**Pour affecter Britta Simon à Syncplicity, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f775-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="4f775-234">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4f775-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4f775-236">Dans la liste des applications, sélectionnez **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="4f775-236">In the applications list, select **Syncplicity**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="4f775-238">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4f775-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4f775-240">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4f775-240">Click **Add** button.</span></span> <span data-ttu-id="4f775-241">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4f775-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4f775-243">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4f775-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4f775-244">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4f775-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4f775-245">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4f775-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4f775-246">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4f775-246">Testing single sign-on</span></span>

<span data-ttu-id="4f775-247">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="4f775-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4f775-248">Lorsque vous cliquez sur la vignette Syncplicity dans le panneau d’accès, vous devez être connecté automatiquement à votre application Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="4f775-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="4f775-249">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4f775-249">Additional resources</span></span>

* [<span data-ttu-id="4f775-250">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f775-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4f775-251">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4f775-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

