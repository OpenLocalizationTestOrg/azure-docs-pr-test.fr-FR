---
title: "Didacticiel : Intégration d’Azure Active Directory à Jive | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6d2d4b777d7afd74598d2eba4a7e3571a8a18d6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="8b4af-103">Didacticiel : Intégration d’Azure Active Directory avec Jive</span><span class="sxs-lookup"><span data-stu-id="8b4af-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="8b4af-104">Dans ce didacticiel, vous allez apprendre à intégrer Jive à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b4af-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b4af-105">L’intégration de Jive dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8b4af-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8b4af-106">Dans Azure AD, vous pouvez contrôler qui a accès à Jive</span><span class="sxs-lookup"><span data-stu-id="8b4af-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="8b4af-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Jive (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4af-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b4af-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8b4af-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8b4af-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b4af-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b4af-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8b4af-110">Prerequisites</span></span>

<span data-ttu-id="8b4af-111">Pour configurer l’intégration d’Azure AD avec Jive, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8b4af-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="8b4af-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b4af-113">Un abonnement Jive pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8b4af-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b4af-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8b4af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b4af-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8b4af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b4af-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8b4af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b4af-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b4af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b4af-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8b4af-118">Scenario description</span></span>
<span data-ttu-id="8b4af-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8b4af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b4af-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b4af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b4af-121">Ajout de Jive depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="8b4af-121">Adding Jive from the gallery</span></span>
2. <span data-ttu-id="8b4af-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="8b4af-123">Ajout de Jive depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="8b4af-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="8b4af-124">Pour configurer l’intégration de Jive avec Azure AD, vous devez ajouter Jive disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8b4af-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8b4af-125">**Pour ajouter Jive à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8b4af-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8b4af-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8b4af-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8b4af-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8b4af-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8b4af-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8b4af-133">Dans la zone de recherche, entrez **Jive**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-133">In the search box, type **Jive**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_search.png)

5. <span data-ttu-id="8b4af-135">Dans le volet de résultats, sélectionnez **Jive**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8b4af-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b4af-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b4af-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Jive avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8b4af-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8b4af-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Jive équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b4af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="8b4af-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Jive associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="8b4af-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="8b4af-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Jive.</span><span class="sxs-lookup"><span data-stu-id="8b4af-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="8b4af-142">Pour configurer et tester l’authentification unique Azure AD avec Jive, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="8b4af-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8b4af-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8b4af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8b4af-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b4af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b4af-145">**[Création d’un utilisateur de test Jive](#creating-a-jive-test-user)** pour avoir un équivalent de Britta Simon dans Jive lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8b4af-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b4af-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b4af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b4af-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8b4af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b4af-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b4af-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Jive.</span><span class="sxs-lookup"><span data-stu-id="8b4af-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="8b4af-150">**Pour configurer l’authentification unique Azure AD avec Jive, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8b4af-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="8b4af-151">Dans le portail Azure, sur la page d’intégration de l’application **Jive**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8b4af-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8b4af-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_jive_samlbase.png)

3. <span data-ttu-id="8b4af-155">Dans la section **Domaine et URL Jive**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8b4af-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="8b4af-157">a.</span><span class="sxs-lookup"><span data-stu-id="8b4af-157">a.</span></span> <span data-ttu-id="8b4af-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="8b4af-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="8b4af-159">b.</span><span class="sxs-lookup"><span data-stu-id="8b4af-159">b.</span></span> <span data-ttu-id="8b4af-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="8b4af-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b4af-161">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="8b4af-161">These values are not the real.</span></span> <span data-ttu-id="8b4af-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="8b4af-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="8b4af-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Jive](https://www.jivesoftware.com/services-support/).</span><span class="sxs-lookup"><span data-stu-id="8b4af-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span> 
 
4. <span data-ttu-id="8b4af-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8b4af-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_jive_certificate.png) 

5. <span data-ttu-id="8b4af-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8b4af-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b4af-168">Pour configurer l’authentification unique côté **Jive**, connectez-vous au locataire Jive en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8b4af-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

7. <span data-ttu-id="8b4af-169">Dans le menu du haut, cliquez sur **Saml**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-169">In the menu on the top, Click "**Saml**."</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="8b4af-171">a.</span><span class="sxs-lookup"><span data-stu-id="8b4af-171">a.</span></span> <span data-ttu-id="8b4af-172">Sélectionnez **Activé** sous l’onglet **Général**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-172">Select **Enabled** under the **General** tab.</span></span>   
    <span data-ttu-id="8b4af-173">b.</span><span class="sxs-lookup"><span data-stu-id="8b4af-173">b.</span></span> <span data-ttu-id="8b4af-174">Cliquez sur le bouton «**Enregistrer tous les paramètres saml**».</span><span class="sxs-lookup"><span data-stu-id="8b4af-174">Click the "**Save all saml settings**" button.</span></span>

8. <span data-ttu-id="8b4af-175">Accédez à l’onglet «**Idp Metadata**(Métadonnées du fournisseur d’identité) ».</span><span class="sxs-lookup"><span data-stu-id="8b4af-175">Navigate to the "**Idp Metadata**" tab.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-jive-tutorial/tutorial_jive_003.png)
   
    <span data-ttu-id="8b4af-177">a.</span><span class="sxs-lookup"><span data-stu-id="8b4af-177">a.</span></span> <span data-ttu-id="8b4af-178">Copiez le contenu du fichier XML de métadonnées téléchargé et collez-le dans la zone de texte **Métadonnées du fournisseur d'identité (IDP)** .</span><span class="sxs-lookup"><span data-stu-id="8b4af-178">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>
    
    <span data-ttu-id="8b4af-179">b.</span><span class="sxs-lookup"><span data-stu-id="8b4af-179">b.</span></span> <span data-ttu-id="8b4af-180">Cliquez sur le bouton «**Enregistrer tous les paramètres saml**».</span><span class="sxs-lookup"><span data-stu-id="8b4af-180">Click the "**Save all saml settings**" button.</span></span> 

9. <span data-ttu-id="8b4af-181">Accédez à l’onglet «**Mappage d’attributs utilisateur**».</span><span class="sxs-lookup"><span data-stu-id="8b4af-181">Go to the "**User Attribute Mapping**" tab.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-jive-tutorial/tutorial_jive_004.png)
   
    <span data-ttu-id="8b4af-183">a.</span><span class="sxs-lookup"><span data-stu-id="8b4af-183">a.</span></span> <span data-ttu-id="8b4af-184">Dans la zone de texte **E-mail**, copiez et collez le nom de la valeur **mail**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-184">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>
   
    <span data-ttu-id="8b4af-185">b.</span><span class="sxs-lookup"><span data-stu-id="8b4af-185">b.</span></span> <span data-ttu-id="8b4af-186">Dans la zone de texte **Prénom**, copiez et collez le nom de la valeur **givenname**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-186">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>
   
    <span data-ttu-id="8b4af-187">c.</span><span class="sxs-lookup"><span data-stu-id="8b4af-187">c.</span></span> <span data-ttu-id="8b4af-188">Dans la zone de texte **Nom**, copiez et collez le nom de la valeur **surname**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-188">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

> [!TIP]
> <span data-ttu-id="8b4af-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="8b4af-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8b4af-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="8b4af-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8b4af-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b4af-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b4af-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4af-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b4af-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8b4af-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8b4af-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8b4af-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8b4af-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b4af-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b4af-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8b4af-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b4af-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8b4af-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jive-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b4af-204">a.</span><span class="sxs-lookup"><span data-stu-id="8b4af-204">a.</span></span> <span data-ttu-id="8b4af-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b4af-206">b.</span><span class="sxs-lookup"><span data-stu-id="8b4af-206">b.</span></span> <span data-ttu-id="8b4af-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b4af-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b4af-208">c.</span><span class="sxs-lookup"><span data-stu-id="8b4af-208">c.</span></span> <span data-ttu-id="8b4af-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8b4af-210">d.</span><span class="sxs-lookup"><span data-stu-id="8b4af-210">d.</span></span> <span data-ttu-id="8b4af-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-211">Click **Create**.</span></span>
 
### <a name="creating-a-jive-test-user"></a><span data-ttu-id="8b4af-212">Création d’un utilisateur de test Jive</span><span class="sxs-lookup"><span data-stu-id="8b4af-212">Creating a Jive test user</span></span>

<span data-ttu-id="8b4af-213">Collaborez avec l’[équipe du support du client Jive](https://www.jivesoftware.com/services-support/) pour ajouter des utilisateurs dans la plateforme Jive.</span><span class="sxs-lookup"><span data-stu-id="8b4af-213">Work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8b4af-214">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b4af-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8b4af-215">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Jive.</span><span class="sxs-lookup"><span data-stu-id="8b4af-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8b4af-217">**Pour affecter Britta Simon à Jive, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8b4af-217">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="8b4af-218">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8b4af-220">Dans la liste des applications, sélectionnez **Jive**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-220">In the applications list, select **Jive**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jive-tutorial/tutorial_jive_app.png) 

3. <span data-ttu-id="8b4af-222">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8b4af-224">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-224">Click **Add** button.</span></span> <span data-ttu-id="8b4af-225">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8b4af-227">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8b4af-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8b4af-228">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b4af-229">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8b4af-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b4af-230">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8b4af-230">Testing single sign-on</span></span>

<span data-ttu-id="8b4af-231">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8b4af-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8b4af-232">Lorsque vous cliquez sur la vignette Jive dans le volet d’accès, vous devez être connecté automatiquement à votre application Jive.</span><span class="sxs-lookup"><span data-stu-id="8b4af-232">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8b4af-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8b4af-233">Additional resources</span></span>

* [<span data-ttu-id="8b4af-234">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b4af-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b4af-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8b4af-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8b4af-236">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8b4af-236">Configure User Provisioning</span></span>](active-directory-saas-jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jive-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jive-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jive-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jive-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jive-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jive-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jive-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jive-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jive-tutorial/tutorial_general_203.png

