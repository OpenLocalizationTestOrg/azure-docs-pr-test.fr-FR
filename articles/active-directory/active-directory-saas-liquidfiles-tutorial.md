---
title: "Didacticiel : Intégration d’Azure Active Directory avec LiquidFiles | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LiquidFiles."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: b858c6d26b78be4641a46b3453f53d103b512356
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="9d473-103">Didacticiel : Intégration d’Azure Active Directory avec LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="9d473-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="9d473-104">Dans ce didacticiel, vous allez apprendre à intégrer LiquidFiles avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d473-104">In this tutorial, you learn how to integrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d473-105">L’intégration de LiquidFiles avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9d473-105">Integrating LiquidFiles with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9d473-106">Vous pouvez contrôler dans Azure AD qui a accès à LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9d473-106">You can control in Azure AD who has access to LiquidFiles</span></span>
- <span data-ttu-id="9d473-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à LiquidFiles (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d473-107">You can enable your users to automatically get signed-on to LiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d473-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9d473-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9d473-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d473-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d473-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="9d473-110">Prerequisites</span></span>

<span data-ttu-id="9d473-111">Pour configurer l’intégration d’Azure AD avec LiquidFiles, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9d473-111">To configure Azure AD integration with LiquidFiles, you need the following items:</span></span>

- <span data-ttu-id="9d473-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d473-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d473-113">Un abonnement LiquidFiles pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9d473-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d473-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9d473-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d473-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9d473-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d473-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9d473-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d473-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d473-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d473-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9d473-118">Scenario description</span></span>
<span data-ttu-id="9d473-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9d473-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d473-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9d473-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d473-121">Ajout de LiquidFiles à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9d473-121">Adding LiquidFiles from the gallery</span></span>
2. <span data-ttu-id="9d473-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d473-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-the-gallery"></a><span data-ttu-id="9d473-123">Ajout de LiquidFiles à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9d473-123">Adding LiquidFiles from the gallery</span></span>
<span data-ttu-id="9d473-124">Pour configurer l’intégration de LiquidFiles avec Azure AD, vous devez ajouter LiquidFiles à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="9d473-124">To configure the integration of LiquidFiles into Azure AD, you need to add LiquidFiles from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9d473-125">**Pour ajouter LiquidFiles à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9d473-125">**To add LiquidFiles from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9d473-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d473-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9d473-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9d473-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9d473-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9d473-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9d473-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9d473-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9d473-133">Dans la zone de recherche, tapez **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="9d473-133">In the search box, type **LiquidFiles**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="9d473-135">Dans le volet de résultats, sélectionnez **LiquidFiles**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9d473-135">In the results panel, select **LiquidFiles**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d473-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d473-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d473-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LiquidFiles sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9d473-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9d473-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LiquidFiles équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d473-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LiquidFiles is to a user in Azure AD.</span></span> <span data-ttu-id="9d473-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur LiquidFiles associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="9d473-140">In other words, a link relationship between an Azure AD user and the related user in LiquidFiles needs to be established.</span></span>

<span data-ttu-id="9d473-141">Dans LiquidFiles, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="9d473-141">In LiquidFiles, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9d473-142">Pour configurer et tester l’authentification unique Azure AD avec LiquidFiles, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="9d473-142">To configure and test Azure AD single sign-on with LiquidFiles, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9d473-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9d473-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9d473-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d473-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d473-145">**[Création d’un utilisateur de test LiquidFiles](#creating-a-liquidfiles-test-user)** pour avoir un équivalent de Britta Simon dans LiquidFiles lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d473-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - to have a counterpart of Britta Simon in LiquidFiles that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d473-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d473-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d473-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9d473-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d473-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d473-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d473-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9d473-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="9d473-150">**Pour configurer l’authentification unique Azure AD avec LiquidFiles, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9d473-150">**To configure Azure AD single sign-on with LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="9d473-151">Dans le portail Azure, sur la page d’intégration de l’application **LiquidFiles**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9d473-151">In the Azure portal, on the **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9d473-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9d473-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="9d473-155">Dans la section **Domaine et URL LiquidFiles**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d473-155">On the **LiquidFiles Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="9d473-157">a.</span><span class="sxs-lookup"><span data-stu-id="9d473-157">a.</span></span> <span data-ttu-id="9d473-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="9d473-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="9d473-159">b.</span><span class="sxs-lookup"><span data-stu-id="9d473-159">b.</span></span> <span data-ttu-id="9d473-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="9d473-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="9d473-161">c.</span><span class="sxs-lookup"><span data-stu-id="9d473-161">c.</span></span> <span data-ttu-id="9d473-162">b.</span><span class="sxs-lookup"><span data-stu-id="9d473-162">b.</span></span> <span data-ttu-id="9d473-163">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="9d473-163">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d473-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9d473-164">These values are not real.</span></span> <span data-ttu-id="9d473-165">Mettez à jour ces valeurs avec l’URL de connexion, l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="9d473-165">Update these values with the actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="9d473-166">Pour obtenir ces valeurs, contactez [l’équipe de support technique LiquidFiles](https://www.liquidfiles.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="9d473-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="9d473-167">Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.</span><span class="sxs-lookup"><span data-stu-id="9d473-167">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="9d473-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9d473-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d473-171">Dans la section **Configuration de LiquidFiles**, cliquez sur **Configurer LiquidFiles** pour ouvrir la fenêtre **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9d473-171">On the **LiquidFiles Configuration** section, click **Configure LiquidFiles** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9d473-172">Copiez l’**URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="9d473-172">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="9d473-174">Connectez-vous à votre site d’entreprise LiquidFiles en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9d473-174">Sign-on to your LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="9d473-175">Dans le menu **Administration > Configuration**, cliquez sur **Single Sign-On (Authentification unique)**.</span><span class="sxs-lookup"><span data-stu-id="9d473-175">Click **Single Sign-On** in the **Admin > Configuration** from the menu.</span></span>

9. <span data-ttu-id="9d473-176">Dans la page **Single Sign-On Configuration** (Configuration de l’authentification unique), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d473-176">On the **Single Sign-On Configuration** page, perform the following steps</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="9d473-178">a.</span><span class="sxs-lookup"><span data-stu-id="9d473-178">a.</span></span> <span data-ttu-id="9d473-179">Pour **Single Sign On Method** (Méthode d’authentification unique), sélectionnez **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="9d473-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="9d473-180">b.</span><span class="sxs-lookup"><span data-stu-id="9d473-180">b.</span></span> <span data-ttu-id="9d473-181">Dans la zone de texte **IDP Login URL** (URL de connexion de fournisseur d’identité), collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9d473-181">In the **IDP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9d473-182">c.</span><span class="sxs-lookup"><span data-stu-id="9d473-182">c.</span></span> <span data-ttu-id="9d473-183">Dans la zone de texte **IDP Logout URL** (URL de déconnexion de fournisseur d’identité), collez la valeur de **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9d473-183">In the **IDP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9d473-184">d.</span><span class="sxs-lookup"><span data-stu-id="9d473-184">d.</span></span> <span data-ttu-id="9d473-185">Dans la zone de texte **IDP Cert Fingerprint** (Empreinte du certificat IDP), collez la valeur **THUMBPRINT** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9d473-185">In the **IDP Cert Fingerprint** textbox, paste the **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="9d473-186">e.</span><span class="sxs-lookup"><span data-stu-id="9d473-186">e.</span></span> <span data-ttu-id="9d473-187">Dans la zone de texte Name Identifier Format (Format d’identificateur de nom), entrez la valeur **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="9d473-187">In the Name Identifier Format textbox, type the value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="9d473-188">f.</span><span class="sxs-lookup"><span data-stu-id="9d473-188">f.</span></span> <span data-ttu-id="9d473-189">Dans la zone de texte Authn Context (Contexte d’authentification), tapez la valeur **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="9d473-189">In the Authn Context textbox, type the value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="9d473-190">g.</span><span class="sxs-lookup"><span data-stu-id="9d473-190">g.</span></span> <span data-ttu-id="9d473-191">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="9d473-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="9d473-192">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9d473-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9d473-193">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9d473-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9d473-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d473-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d473-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d473-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d473-196">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9d473-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9d473-198">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9d473-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9d473-199">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d473-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d473-201">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9d473-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d473-203">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9d473-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d473-205">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d473-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d473-207">a.</span><span class="sxs-lookup"><span data-stu-id="9d473-207">a.</span></span> <span data-ttu-id="9d473-208">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d473-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d473-209">b.</span><span class="sxs-lookup"><span data-stu-id="9d473-209">b.</span></span> <span data-ttu-id="9d473-210">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9d473-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d473-211">c.</span><span class="sxs-lookup"><span data-stu-id="9d473-211">c.</span></span> <span data-ttu-id="9d473-212">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9d473-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9d473-213">d.</span><span class="sxs-lookup"><span data-stu-id="9d473-213">d.</span></span> <span data-ttu-id="9d473-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d473-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="9d473-215">Création d’un utilisateur de test LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="9d473-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="9d473-216">L’objectif de cette section est de créer un utilisateur nommé Britta Simon dans LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9d473-216">The objective of this section is to create a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="9d473-217">Demandez à votre administrateur de serveur LiquidFiles de vous ajouter en tant qu’utilisateur avant de vous connecter à votre application LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9d473-217">Work with your LiquidFiles server administrator to get yourself added as a user before logging in to your LiquidFiles application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9d473-218">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d473-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9d473-219">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9d473-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LiquidFiles.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9d473-221">**Pour affecter Britta Simon à LiquidFiles, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9d473-221">**To assign Britta Simon to LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="9d473-222">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9d473-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9d473-224">Dans la liste des applications, sélectionnez **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="9d473-224">In the applications list, select **LiquidFiles**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="9d473-226">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9d473-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9d473-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9d473-228">Click **Add** button.</span></span> <span data-ttu-id="9d473-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9d473-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9d473-231">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9d473-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9d473-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9d473-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d473-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9d473-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d473-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9d473-234">Testing single sign-on</span></span>

<span data-ttu-id="9d473-235">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9d473-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9d473-236">Lorsque vous cliquez sur la vignette LiquidFiles dans le volet d’accès, vous êtes connecté automatiquement à votre application LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="9d473-236">When you click the LiquidFiles tile in the Access Panel, you should get automatically signed-on to your LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d473-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9d473-237">Additional resources</span></span>

* [<span data-ttu-id="9d473-238">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d473-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d473-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9d473-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

