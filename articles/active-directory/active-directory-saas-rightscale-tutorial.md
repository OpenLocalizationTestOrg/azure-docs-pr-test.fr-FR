---
title: "Didacticiel : Intégration d’Azure Active Directory avec RightScale | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et RightScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 222c4414a9f736a3589b4cdd0ed934696f6c31ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="c5fcc-103">Didacticiel : Intégration d’Azure Active Directory avec RightScale</span><span class="sxs-lookup"><span data-stu-id="c5fcc-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="c5fcc-104">Dans ce didacticiel, vous allez apprendre à intégrer RightScale avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5fcc-104">In this tutorial, you learn how to integrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5fcc-105">L’intégration de RightScale avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c5fcc-105">Integrating Rightscale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c5fcc-106">Dans Azure AD, vous pouvez contrôler qui a accès à RightScale.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-106">You can control in Azure AD who has access to Rightscale</span></span>
- <span data-ttu-id="c5fcc-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à RightScale (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-107">You can enable your users to automatically get signed-on to Rightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c5fcc-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c5fcc-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5fcc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5fcc-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="c5fcc-110">Prerequisites</span></span>

<span data-ttu-id="c5fcc-111">Pour configurer l’intégration d’Azure AD avec RightScale, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c5fcc-111">To configure Azure AD integration with Rightscale, you need the following items:</span></span>

- <span data-ttu-id="c5fcc-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5fcc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5fcc-113">Un abonnement RightScale pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c5fcc-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5fcc-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5fcc-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c5fcc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5fcc-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5fcc-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5fcc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5fcc-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c5fcc-118">Scenario description</span></span>
<span data-ttu-id="c5fcc-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5fcc-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c5fcc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5fcc-121">Ajout de RightScale à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c5fcc-121">Adding Rightscale from the gallery</span></span>
2. <span data-ttu-id="c5fcc-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5fcc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-the-gallery"></a><span data-ttu-id="c5fcc-123">Ajout de RightScale à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c5fcc-123">Adding Rightscale from the gallery</span></span>
<span data-ttu-id="c5fcc-124">Pour configurer l’intégration de RightScale à Azure AD, vous devez ajouter RightScale à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-124">To configure the integration of Rightscale into Azure AD, you need to add Rightscale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c5fcc-125">**Pour ajouter RightScale à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c5fcc-125">**To add Rightscale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c5fcc-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c5fcc-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c5fcc-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c5fcc-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c5fcc-133">Dans la zone de recherche, tapez **RightScale**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-133">In the search box, type **Rightscale**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="c5fcc-135">Dans le volet de résultats, sélectionnez **RightScale**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-135">In the results panel, select **Rightscale**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5fcc-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5fcc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5fcc-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RightScale sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c5fcc-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5fcc-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur RightScale équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Rightscale is to a user in Azure AD.</span></span> <span data-ttu-id="c5fcc-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur RightScale associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-140">In other words, a link relationship between an Azure AD user and the related user in Rightscale needs to be established.</span></span>

<span data-ttu-id="c5fcc-141">Dans RightScale, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-141">In Rightscale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c5fcc-142">Pour configurer et tester l’authentification unique Azure AD avec RightScale, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c5fcc-142">To configure and test Azure AD single sign-on with Rightscale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c5fcc-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c5fcc-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5fcc-145">**[Création d’un utilisateur de test RightScale](#creating-a-rightscale-test-user)** pour avoir un équivalent de Britta Simon dans RightScale lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in Rightscale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5fcc-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5fcc-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5fcc-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5fcc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c5fcc-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application RightScale.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="c5fcc-150">**Pour configurer l’authentification unique Azure AD avec RightScale, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c5fcc-150">**To configure Azure AD single sign-on with Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="c5fcc-151">Dans le portail Azure, dans la page d’intégration de l’application **RightScale**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-151">In the Azure portal, on the **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c5fcc-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="c5fcc-155">Dans la section **Domaine et URL RightScale**, si vous souhaitez configurer l’application en **mode initialisé IDP** vous n’avez rien à faire, car l’application est déjà pré-intégrée avec Azure.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-155">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **IDP initiated mode** you do not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="c5fcc-157">Dans la section **Domaine et URL RightScale**, si vous souhaitez configurer l’application en **mode initié SP**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5fcc-157">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="c5fcc-159">a.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-159">a.</span></span> <span data-ttu-id="c5fcc-160">Cliquez sur l’option **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-160">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="c5fcc-161">b.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-161">b.</span></span> <span data-ttu-id="c5fcc-162">Dans la zone de texte **URL d’authentification**, saisissez l’URL : `https://login.rightscale.com/`.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-162">In the **Sign On URL** textbox, type the URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="c5fcc-163">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="c5fcc-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c5fcc-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c5fcc-167">Dans la section **Configuration de RightScale**, cliquez sur **Configurer RightScale** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-167">On the **Rightscale Configuration** section, click **Configure Rightscale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c5fcc-168">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-168">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="c5fcc-169">![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="c5fcc-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="c5fcc-170">Pour que l’authentification unique soit configurée pour votre application, vous devez vous connecter à votre locataire RightScale en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-170">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="c5fcc-171">a.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-171">a.</span></span> <span data-ttu-id="c5fcc-172">Dans le menu situé en haut, cliquez sur l’onglet **Paramètres** et sélectionnez **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="c5fcc-174">b.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-174">b.</span></span> <span data-ttu-id="c5fcc-175">Cliquez sur le bouton « **nouveau** » pour ajouter **vos fournisseurs d’identité SAML**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-175">Click the "**new**" button to add **Your SAML Identity Providers**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="c5fcc-177">c.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-177">c.</span></span> <span data-ttu-id="c5fcc-178">Dans la zone de texte **Nom d'affichage**, entrez le nom de votre société.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-178">In the textbox of **Display Name**, input your company name.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="c5fcc-180">d.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-180">d.</span></span> <span data-ttu-id="c5fcc-181">Sélectionnez **Allow RightScale-initiated SSO using a discovery hint** et entrez votre **nom de domaine** dans la zone de texte située dessous.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="c5fcc-183">e.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-183">e.</span></span> <span data-ttu-id="c5fcc-184">Collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée sur le portail Azure vers **SAML SSO Endpoint** dans RightScale.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-184">Paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="c5fcc-186">f.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-186">f.</span></span> <span data-ttu-id="c5fcc-187">Collez la valeur de l’**ID d’entité SAML** que vous avez copiée sur le portail Azure vers **SAML EntityID** dans RightScale.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-187">Paste the value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="c5fcc-189">g.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-189">g.</span></span> <span data-ttu-id="c5fcc-190">Cliquez sur le bouton **Explorateur** pour charger le certificat que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-190">Click **Browser** button to upload the certificate which you downloaded from Azure portal.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="c5fcc-192">h.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-192">h.</span></span> <span data-ttu-id="c5fcc-193">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="c5fcc-194">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c5fcc-195">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c5fcc-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5fcc-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5fcc-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5fcc-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5fcc-198">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c5fcc-200">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c5fcc-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c5fcc-201">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c5fcc-203">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c5fcc-205">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c5fcc-207">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5fcc-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c5fcc-209">a.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-209">a.</span></span> <span data-ttu-id="c5fcc-210">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5fcc-211">b.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-211">b.</span></span> <span data-ttu-id="c5fcc-212">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c5fcc-213">c.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-213">c.</span></span> <span data-ttu-id="c5fcc-214">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c5fcc-215">d.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-215">d.</span></span> <span data-ttu-id="c5fcc-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="c5fcc-217">Création d’un utilisateur de test RightScale</span><span class="sxs-lookup"><span data-stu-id="c5fcc-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="c5fcc-218">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans RightScale.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="c5fcc-219">Collaborez avec l’[équipe de support technique RightScale](mailto:support@rightscale.com) pour ajouter les utilisateurs dans la plateforme RightScale.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) to add the users in the RightScale platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c5fcc-220">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5fcc-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c5fcc-221">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à RightScale.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rightscale.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c5fcc-223">**Pour affecter Britta Simon à RightScale, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c5fcc-223">**To assign Britta Simon to Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="c5fcc-224">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c5fcc-226">Dans la liste des applications, sélectionnez **RightScale**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-226">In the applications list, select **Rightscale**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="c5fcc-228">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c5fcc-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-230">Click **Add** button.</span></span> <span data-ttu-id="c5fcc-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c5fcc-233">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c5fcc-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5fcc-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c5fcc-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c5fcc-236">Testing single sign-on</span></span>

<span data-ttu-id="c5fcc-237">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="c5fcc-238">Quand vous cliquez sur la mosaïque RightScale dans le volet d’accès, vous devez être connecté automatiquement à votre application RightScale.</span><span class="sxs-lookup"><span data-stu-id="c5fcc-238">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5fcc-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c5fcc-239">Additional resources</span></span>

* [<span data-ttu-id="c5fcc-240">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5fcc-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5fcc-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c5fcc-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

