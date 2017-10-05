---
title: "Didacticiel : Intégration d’Azure Active Directory à Tableau Online | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 443fab1198a91a4d5749e6421f7b8603fc75a81e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="1410e-103">Didacticiel : Intégration d’Azure Active Directory à Tableau Online</span><span class="sxs-lookup"><span data-stu-id="1410e-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="1410e-104">Dans ce didacticiel, vous allez apprendre à intégrer Tableau Online à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1410e-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1410e-105">L’intégration de Tableau Online à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1410e-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1410e-106">Dans Azure AD, vous pouvez contrôler qui a accès à Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1410e-106">You can control in Azure AD who has access to Tableau Online</span></span>
- <span data-ttu-id="1410e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Tableau Online (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1410e-107">You can enable your users to automatically get signed-on to Tableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1410e-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1410e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1410e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1410e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1410e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1410e-110">Prerequisites</span></span>

<span data-ttu-id="1410e-111">Pour configurer l’intégration d’Azure AD à Tableau Online, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1410e-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

- <span data-ttu-id="1410e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1410e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1410e-113">Un abonnement Tableau Online pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1410e-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1410e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1410e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1410e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1410e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1410e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1410e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1410e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1410e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1410e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1410e-118">Scenario description</span></span>
<span data-ttu-id="1410e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1410e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1410e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1410e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1410e-121">Ajout de Tableau Online à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1410e-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="1410e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1410e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="1410e-123">Ajout de Tableau Online à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1410e-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="1410e-124">Pour configurer l’intégration de Tableau Online à Azure AD, vous devez ajouter Tableau Online à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1410e-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1410e-125">**Pour ajouter Tableau Online à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1410e-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1410e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1410e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1410e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1410e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1410e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1410e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1410e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1410e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1410e-133">Dans la zone de recherche, tapez **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="1410e-133">In the search box, type **Tableau Online**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="1410e-135">Dans le panneau de résultats, sélectionnez **Tableau Online**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1410e-135">In the results panel, select **Tableau Online**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1410e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1410e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1410e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tableau Online à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1410e-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1410e-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Tableau Online équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1410e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="1410e-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Tableau Online associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1410e-140">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="1410e-141">Dans Tableau Online, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1410e-141">In Tableau Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1410e-142">Pour configurer et tester l’authentification unique Azure AD avec Tableau Online, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1410e-142">To configure and test Azure AD single sign-on with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1410e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1410e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1410e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1410e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1410e-145">**[Création d’un utilisateur de test Tableau Online](#creating-a-tableau-online-test-user)** pour avoir un équivalent de Britta Simon dans Tableau Online lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1410e-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1410e-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1410e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1410e-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1410e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1410e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1410e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1410e-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1410e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="1410e-150">**Pour configurer l’authentification unique Azure AD avec Tableau Online, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1410e-150">**To configure Azure AD single sign-on with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="1410e-151">Dans le portail Azure, sur la page d’intégration de l’application **Tableau Online**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1410e-151">In the Azure portal, on the **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1410e-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1410e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="1410e-155">Dans la section **Tableau Online Domain and URLs** (Domaine et URL Tableau Online), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1410e-155">On the **Tableau Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="1410e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1410e-157">a.</span></span> <span data-ttu-id="1410e-158">Dans la zone de texte **URL de connexion**, tapez l’URL : `https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="1410e-158">In the **Sign-on URL** textbox, type the URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="1410e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1410e-159">b.</span></span> <span data-ttu-id="1410e-160">Dans la zone de texte **Identificateur**, tapez l’URL : `https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="1410e-160">In the **Identifier** textbox, type the URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="1410e-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1410e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="1410e-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1410e-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1410e-165">Dans une autre fenêtre du navigateur, connectez-vous à votre application Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1410e-165">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="1410e-166">Cliquez sur **Settings** (Paramètres), puis sur **Authentication** (Authentification).</span><span class="sxs-lookup"><span data-stu-id="1410e-166">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="1410e-168">Pour activer SAML, dans la section **Types d’authentification**,</span><span class="sxs-lookup"><span data-stu-id="1410e-168">To enable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="1410e-169">cochez la case **Single sign-on with SAML** (Authentification unique avec SAML).</span><span class="sxs-lookup"><span data-stu-id="1410e-169">Check the **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="1410e-171">Faites défiler la page jusqu’à la section **Import metadata file into Tableau Online (Importer le fichier de métadonnées dans Tableau Online)** .</span><span class="sxs-lookup"><span data-stu-id="1410e-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="1410e-172">Cliquez sur Browse (Parcourir) et importez le fichier de métadonnées que vous avez téléchargé à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1410e-172">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="1410e-173">Cliquez alors sur **Apply (Appliquer)**.</span><span class="sxs-lookup"><span data-stu-id="1410e-173">Then, click **Apply**.</span></span>
   
   ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="1410e-175">Dans la section **Match assertions** (Faire correspondre les assertions), insérez les noms d’assertion du fournisseur d’identité correspondants pour **l’adresse e-mail**, le **prénom** et le **nom**.</span><span class="sxs-lookup"><span data-stu-id="1410e-175">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="1410e-176">Pour obtenir ces informations à partir d’Azure AD :</span><span class="sxs-lookup"><span data-stu-id="1410e-176">To get this information from Azure AD:</span></span> 
  
    <span data-ttu-id="1410e-177">a.</span><span class="sxs-lookup"><span data-stu-id="1410e-177">a.</span></span> <span data-ttu-id="1410e-178">Dans le portail Azure, accédez à la page d’intégration de l’application **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="1410e-178">In the Azure portal, go on the **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="1410e-179">b.</span><span class="sxs-lookup"><span data-stu-id="1410e-179">b.</span></span> <span data-ttu-id="1410e-180">Dans la section des attributs, cochez la case **« Afficher et modifier tous les autres attributs utilisateur »**.</span><span class="sxs-lookup"><span data-stu-id="1410e-180">In the attributes section, Select the **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="1410e-182">c.</span><span class="sxs-lookup"><span data-stu-id="1410e-182">c.</span></span> <span data-ttu-id="1410e-183">Copiez la valeur de l’espace de noms de ces attributs : prénom, adresse e-mail et nom de famille en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="1410e-183">Copy the namespace value for these attributes: givenname, email and surname by using the following steps:</span></span>

   ![Authentification unique Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="1410e-185">d.</span><span class="sxs-lookup"><span data-stu-id="1410e-185">d.</span></span> <span data-ttu-id="1410e-186">Cliquez sur la valeur **user.givenname**.</span><span class="sxs-lookup"><span data-stu-id="1410e-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="1410e-187">e.</span><span class="sxs-lookup"><span data-stu-id="1410e-187">e.</span></span> <span data-ttu-id="1410e-188">Copiez la valeur à partir de la zone de texte **espace de noms**.</span><span class="sxs-lookup"><span data-stu-id="1410e-188">Copy the value from the **namespace** textbox.</span></span>

   ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="1410e-190">f.</span><span class="sxs-lookup"><span data-stu-id="1410e-190">f.</span></span> <span data-ttu-id="1410e-191">Pour copier les valeurs d’espace de noms pour l’adresse e-mail et le nom de famille, suivez les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="1410e-191">To copy the namesapce values for the email and surname follow the preceding steps.</span></span>

    <span data-ttu-id="1410e-192">g.</span><span class="sxs-lookup"><span data-stu-id="1410e-192">g.</span></span> <span data-ttu-id="1410e-193">Basculez dans l’application Tableau Online, puis définissez la section **Tableau Online Attributes** (Attributs Tableau Online) comme suit :</span><span class="sxs-lookup"><span data-stu-id="1410e-193">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="1410e-194">Email (Adresse de messagerie) : **mail** ou **userPrincipalName**</span><span class="sxs-lookup"><span data-stu-id="1410e-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="1410e-195">First name (Prénom) : **givenName**</span><span class="sxs-lookup"><span data-stu-id="1410e-195">First name: **givenname**</span></span>
     * <span data-ttu-id="1410e-196">Last name (Nom) : **surname**</span><span class="sxs-lookup"><span data-stu-id="1410e-196">Last name: **surname**</span></span>
   
   ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="1410e-198">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1410e-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1410e-199">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1410e-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1410e-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1410e-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1410e-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1410e-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="1410e-202">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1410e-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1410e-204">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1410e-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1410e-205">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1410e-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1410e-207">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1410e-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1410e-209">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1410e-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1410e-211">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1410e-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1410e-213">a.</span><span class="sxs-lookup"><span data-stu-id="1410e-213">a.</span></span> <span data-ttu-id="1410e-214">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1410e-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1410e-215">b.</span><span class="sxs-lookup"><span data-stu-id="1410e-215">b.</span></span> <span data-ttu-id="1410e-216">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1410e-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1410e-217">c.</span><span class="sxs-lookup"><span data-stu-id="1410e-217">c.</span></span> <span data-ttu-id="1410e-218">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1410e-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1410e-219">d.</span><span class="sxs-lookup"><span data-stu-id="1410e-219">d.</span></span> <span data-ttu-id="1410e-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1410e-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="1410e-221">Création d’un utilisateur de test Tableau Online</span><span class="sxs-lookup"><span data-stu-id="1410e-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="1410e-222">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1410e-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="1410e-223">Dans **Tableau Online**, cliquez sur **Paramètres**, puis sur la section **Authentification**.</span><span class="sxs-lookup"><span data-stu-id="1410e-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="1410e-224">Faites défiler la page jusqu’à la section **Select Users (Sélectionner des utilisateurs)** .</span><span class="sxs-lookup"><span data-stu-id="1410e-224">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="1410e-225">Cliquez sur **Ajouter des utilisateurs**, puis sur **Entrer les adresses de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="1410e-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="1410e-227">Sélectionnez **Add users for single sign-on (SSO) authentication (Ajouter des utilisateurs pour l’authentification unique (SSO))**.</span><span class="sxs-lookup"><span data-stu-id="1410e-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="1410e-228">Dans la zone de texte **Enter Email Addresses** (Entrez les adresses de messagerie), ajoutez britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="1410e-228">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="1410e-230">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1410e-230">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1410e-231">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1410e-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1410e-232">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1410e-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tableau Online.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1410e-234">**Pour affecter Britta Simon à Tableau Online, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1410e-234">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="1410e-235">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1410e-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1410e-237">Dans la liste des applications, sélectionnez **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="1410e-237">In the applications list, select **Tableau Online**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="1410e-239">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1410e-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1410e-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1410e-241">Click **Add** button.</span></span> <span data-ttu-id="1410e-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1410e-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1410e-244">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1410e-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1410e-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1410e-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1410e-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1410e-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1410e-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1410e-247">Testing single sign-on</span></span>

<span data-ttu-id="1410e-248">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1410e-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1410e-249">Si vous cliquez sur la mosaïque Tableau Online dans le volet d’accès, vous devez vous connecter automatiquement à votre application Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1410e-249">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1410e-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1410e-250">Additional resources</span></span>

* [<span data-ttu-id="1410e-251">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1410e-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1410e-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1410e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

