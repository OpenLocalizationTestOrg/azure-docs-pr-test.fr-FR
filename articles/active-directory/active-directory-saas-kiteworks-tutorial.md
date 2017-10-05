---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kiteworks | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2fd9b346cb6d838069ef94ee9c2a8d113f22779c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="d14f9-103">Didacticiel : Intégration d’Azure Active Directory à Kiteworks</span><span class="sxs-lookup"><span data-stu-id="d14f9-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="d14f9-104">Dans ce didacticiel, vous allez apprendre à intégrer Kiteworks à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d14f9-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d14f9-105">L’intégration de Kiteworks dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d14f9-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d14f9-106">Dans Azure AD, vous pouvez contrôler qui a accès à Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="d14f9-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="d14f9-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Kiteworks (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d14f9-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d14f9-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d14f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d14f9-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d14f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d14f9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d14f9-110">Prerequisites</span></span>

<span data-ttu-id="d14f9-111">Pour configurer l’intégration d’Azure AD avec Kiteworks, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d14f9-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="d14f9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d14f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d14f9-113">Un abonnement Kiteworks pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d14f9-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d14f9-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d14f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d14f9-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d14f9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d14f9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d14f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d14f9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d14f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d14f9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d14f9-118">Scenario description</span></span>
<span data-ttu-id="d14f9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d14f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d14f9-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d14f9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d14f9-121">Ajout de Kiteworks à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d14f9-121">Adding Kiteworks from the gallery</span></span>
2. <span data-ttu-id="d14f9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d14f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="d14f9-123">Ajout de Kiteworks à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d14f9-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="d14f9-124">Pour configurer l’intégration de Kiteworks avec Azure AD, vous devez ajouter Kiteworks à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d14f9-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d14f9-125">**Pour ajouter Kiteworks à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d14f9-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d14f9-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d14f9-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d14f9-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d14f9-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d14f9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d14f9-133">Dans la zone de recherche, entrez **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-133">In the search box, type **Kiteworks**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="d14f9-135">Dans le volet de résultats, sélectionnez **Kiteworks**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d14f9-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d14f9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d14f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d14f9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kiteworks avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d14f9-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d14f9-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Kiteworks équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d14f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="d14f9-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Kiteworks associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="d14f9-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="d14f9-141">Dans Kiteworks, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="d14f9-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d14f9-142">Pour configurer et tester l’authentification unique Azure AD avec Kiteworks, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d14f9-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d14f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d14f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d14f9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d14f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d14f9-145">**[Création d’un utilisateur de test Kiteworks](#creating-a-kiteworks-test-user)** pour avoir un équivalent de Britta Simon dans Kiteworks lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="d14f9-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d14f9-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d14f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d14f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d14f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d14f9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d14f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d14f9-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="d14f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="d14f9-150">**Pour configurer l’authentification unique Azure AD avec Kiteworks, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d14f9-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="d14f9-151">Dans le portail Azure, sur la page d’intégration de l’application **Kiteworks**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d14f9-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d14f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="d14f9-155">Dans la section **Domaine et URL Kiteworks**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d14f9-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="d14f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="d14f9-157">a.</span></span> <span data-ttu-id="d14f9-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="d14f9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="d14f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="d14f9-159">b.</span></span> <span data-ttu-id="d14f9-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="d14f9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d14f9-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="d14f9-161">These values are not real.</span></span> <span data-ttu-id="d14f9-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="d14f9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d14f9-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique de Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="d14f9-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="d14f9-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d14f9-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="d14f9-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d14f9-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d14f9-168">Dans la section **Configuration de Kiteworks**, cliquez sur **Configurer Kiteworks** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d14f9-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d14f9-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="d14f9-171">Connectez-vous à votre site d’entreprise Kiteworks en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d14f9-171">Sign on to your Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="d14f9-172">Dans la barre d’outils située en haut, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="d14f9-174">Dans la section **Authentification et autorisation**, cliquez sur **SSO Setup** (Configuration de l’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="d14f9-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="d14f9-176">Sur la page de configuration de l’authentification unique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d14f9-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="d14f9-178">a.</span><span class="sxs-lookup"><span data-stu-id="d14f9-178">a.</span></span> <span data-ttu-id="d14f9-179">Sélectionnez **Authenticate via SSO**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="d14f9-180">b.</span><span class="sxs-lookup"><span data-stu-id="d14f9-180">b.</span></span> <span data-ttu-id="d14f9-181">Sélectionnez **Initiate AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="d14f9-182">c.</span><span class="sxs-lookup"><span data-stu-id="d14f9-182">c.</span></span> <span data-ttu-id="d14f9-183">Dans la zone de texte **ID d’entité IdP**, collez la valeur **ID d’entité SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d14f9-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="d14f9-184">d.</span><span class="sxs-lookup"><span data-stu-id="d14f9-184">d.</span></span> <span data-ttu-id="d14f9-185">Dans la zone de texte **URL du service d’authentification unique SAML**, collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d14f9-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d14f9-186">e.</span><span class="sxs-lookup"><span data-stu-id="d14f9-186">e.</span></span> <span data-ttu-id="d14f9-187">Dans la zone de texte **URL du service de déconnexion unique**, collez la valeur de **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d14f9-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d14f9-188">f.</span><span class="sxs-lookup"><span data-stu-id="d14f9-188">f.</span></span> <span data-ttu-id="d14f9-189">Ouvrez le certificat que vous avez téléchargé dans le Bloc-notes, copiez son contenu, puis collez-le dans la zone de texte **RSA Public Key Certificate** .</span><span class="sxs-lookup"><span data-stu-id="d14f9-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="d14f9-190">g.</span><span class="sxs-lookup"><span data-stu-id="d14f9-190">g.</span></span> <span data-ttu-id="d14f9-191">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d14f9-192">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d14f9-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d14f9-193">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d14f9-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d14f9-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d14f9-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d14f9-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d14f9-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="d14f9-196">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d14f9-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d14f9-198">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d14f9-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d14f9-199">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d14f9-201">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d14f9-203">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d14f9-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d14f9-205">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d14f9-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d14f9-207">a.</span><span class="sxs-lookup"><span data-stu-id="d14f9-207">a.</span></span> <span data-ttu-id="d14f9-208">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d14f9-209">b.</span><span class="sxs-lookup"><span data-stu-id="d14f9-209">b.</span></span> <span data-ttu-id="d14f9-210">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d14f9-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d14f9-211">c.</span><span class="sxs-lookup"><span data-stu-id="d14f9-211">c.</span></span> <span data-ttu-id="d14f9-212">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d14f9-213">d.</span><span class="sxs-lookup"><span data-stu-id="d14f9-213">d.</span></span> <span data-ttu-id="d14f9-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="d14f9-215">Création d’un utilisateur de test Kiteworks</span><span class="sxs-lookup"><span data-stu-id="d14f9-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="d14f9-216">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="d14f9-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="d14f9-217">Kiteworks prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="d14f9-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d14f9-218">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="d14f9-218">There is no action item for you in this section.</span></span> <span data-ttu-id="d14f9-219">Un utilisateur est créé lors d’une tentative d’accès à Kiteworks s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="d14f9-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d14f9-220">Si vous devez créer un utilisateur manuellement, contactez [l’équipe de support de Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="d14f9-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d14f9-221">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d14f9-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d14f9-222">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="d14f9-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d14f9-224">**Pour affecter Britta Simon à Kiteworks, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d14f9-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="d14f9-225">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d14f9-227">Dans la liste des applications, sélectionnez **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-227">In the applications list, select **Kiteworks**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="d14f9-229">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d14f9-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-231">Click **Add** button.</span></span> <span data-ttu-id="d14f9-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d14f9-234">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d14f9-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d14f9-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d14f9-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d14f9-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d14f9-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d14f9-237">Testing single sign-on</span></span>

<span data-ttu-id="d14f9-238">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d14f9-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="d14f9-239">Lorsque vous cliquez sur la vignette Kiteworks dans le volet d’accès, vous devez être connecté automatiquement à votre application Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="d14f9-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d14f9-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d14f9-240">Additional resources</span></span>

* [<span data-ttu-id="d14f9-241">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d14f9-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d14f9-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d14f9-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

