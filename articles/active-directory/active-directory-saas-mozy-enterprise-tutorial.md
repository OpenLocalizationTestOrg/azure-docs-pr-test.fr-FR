---
title: "Didacticiel : Intégration d’Azure Active Directory avec Mozy Enterprise | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: ac73aadcb8205f24f9d2dbce5af76f53bbcb9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="d4255-103">Didacticiel : Intégration d’Azure Active Directory avec Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="d4255-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="d4255-104">Dans ce didacticiel, vous allez apprendre à intégrer Mozy Enterprise avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d4255-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d4255-105">L’intégration du logiciel Mozy Enterprise avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d4255-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d4255-106">Dans Azure AD, vous pouvez contrôler qui a accès à Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d4255-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="d4255-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Mozy Enterprise (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4255-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d4255-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d4255-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d4255-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d4255-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4255-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d4255-110">Prerequisites</span></span>

<span data-ttu-id="d4255-111">Pour configurer l’intégration d’Azure AD avec Mozy Enterprise, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d4255-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="d4255-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4255-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d4255-113">Un abonnement Mozy Enterprise pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d4255-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d4255-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d4255-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d4255-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d4255-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d4255-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d4255-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d4255-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4255-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d4255-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d4255-118">Scenario description</span></span>
<span data-ttu-id="d4255-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d4255-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d4255-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4255-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d4255-121">Ajout de Mozy Enterprise à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d4255-121">Adding Mozy Enterprise from the gallery</span></span>
2. <span data-ttu-id="d4255-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4255-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="d4255-123">Ajout de Mozy Enterprise à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d4255-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="d4255-124">Pour configurer l’intégration de Mozy Enterprise à Azure AD, vous devez ajouter Mozy Enterprise à votre liste d’applications SaaS gérées, depuis la galerie.</span><span class="sxs-lookup"><span data-stu-id="d4255-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d4255-125">**Pour ajouter Mozy Enterprise à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d4255-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d4255-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d4255-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d4255-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d4255-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d4255-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d4255-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d4255-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d4255-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d4255-133">Dans la zone de recherche, entrez **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="d4255-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="d4255-135">Dans le panneau des résultats, sélectionnez **Mozy Enterprise**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d4255-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d4255-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4255-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d4255-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mozy Enterprise avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d4255-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d4255-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Mozy Enterprise équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4255-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="d4255-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Mozy Enterprise associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="d4255-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="d4255-141">Dans Mozy Enterprise, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="d4255-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d4255-142">Pour configurer et tester l’authentification unique Azure AD avec Mozy Enterprise, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4255-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d4255-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d4255-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d4255-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d4255-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d4255-145">**[Création d’un utilisateur de test Mozy Enterprise](#creating-a-mozy-enterprise-test-user)** pour obtenir un équivalent de Britta Simon dans Mozy Enterprise, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="d4255-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d4255-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4255-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d4255-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d4255-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d4255-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4255-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d4255-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d4255-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="d4255-150">**Pour configurer l’authentification unique Azure AD avec Mozy Enterprise, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d4255-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="d4255-151">Dans le portail Azure, sur la page d’intégration de l’application **Mozy Enterprise**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d4255-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d4255-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d4255-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="d4255-155">Dans la section **Domaine et URL Mozy Enterprise**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d4255-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="d4255-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="d4255-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d4255-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="d4255-158">This value is not real.</span></span> <span data-ttu-id="d4255-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="d4255-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d4255-160">Contactez l’[équipe de support Mozy Enterprise](http://support.mozy.com/) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="d4255-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

4. <span data-ttu-id="d4255-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d4255-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="d4255-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d4255-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d4255-165">Dans la section **Configuration de Mozy Enterprise**, cliquez sur **Configurer Mozy Enterprise** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d4255-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d4255-166">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d4255-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="d4255-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Mozy Enterprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d4255-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="d4255-169">Dans la section **Configuration**, cliquez sur **Authentication Policy**.</span><span class="sxs-lookup"><span data-stu-id="d4255-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="d4255-170">![Stratégie d’authentification](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Stratégie d’authentification")</span><span class="sxs-lookup"><span data-stu-id="d4255-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="d4255-171">Dans la section **Authentication Policy** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d4255-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="d4255-172">![Stratégie d’authentification](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Stratégie d’authentification")</span><span class="sxs-lookup"><span data-stu-id="d4255-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="d4255-173">a.</span><span class="sxs-lookup"><span data-stu-id="d4255-173">a.</span></span> <span data-ttu-id="d4255-174">Sélectionnez **Directory Service** comme **Provider**.</span><span class="sxs-lookup"><span data-stu-id="d4255-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="d4255-175">b.</span><span class="sxs-lookup"><span data-stu-id="d4255-175">b.</span></span> <span data-ttu-id="d4255-176">Sélectionnez **Use LDAP Push**.</span><span class="sxs-lookup"><span data-stu-id="d4255-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="d4255-177">c.</span><span class="sxs-lookup"><span data-stu-id="d4255-177">c.</span></span> <span data-ttu-id="d4255-178">Cliquez sur l’onglet **SAML Authentication** .</span><span class="sxs-lookup"><span data-stu-id="d4255-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="d4255-179">d.</span><span class="sxs-lookup"><span data-stu-id="d4255-179">d.</span></span> <span data-ttu-id="d4255-180">Collez l’**URL du service d’authentification unique SAML** que vous avez copiée sur le portail Azure dans la zone de texte de l’**URL d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d4255-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="d4255-181">e.</span><span class="sxs-lookup"><span data-stu-id="d4255-181">e.</span></span> <span data-ttu-id="d4255-182">Collez l’**ID d’entité SAML** que vous avez copié sur le portail Azure dans la zone de texte du **Point de terminaison SAML**.</span><span class="sxs-lookup"><span data-stu-id="d4255-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="d4255-183">f.</span><span class="sxs-lookup"><span data-stu-id="d4255-183">f.</span></span> <span data-ttu-id="d4255-184">Ouvrez votre certificat téléchargé, codé en base 64, dans le bloc-notes, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **Certificat SAML**.</span><span class="sxs-lookup"><span data-stu-id="d4255-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="d4255-185">g.</span><span class="sxs-lookup"><span data-stu-id="d4255-185">g.</span></span> <span data-ttu-id="d4255-186">Sélectionnez **Enable SSO for Admins to log in with their network credentials**.</span><span class="sxs-lookup"><span data-stu-id="d4255-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="d4255-187">h.</span><span class="sxs-lookup"><span data-stu-id="d4255-187">h.</span></span> <span data-ttu-id="d4255-188">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="d4255-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="d4255-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d4255-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d4255-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d4255-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d4255-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d4255-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d4255-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4255-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d4255-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d4255-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d4255-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d4255-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d4255-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d4255-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d4255-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d4255-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d4255-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d4255-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d4255-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d4255-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d4255-204">a.</span><span class="sxs-lookup"><span data-stu-id="d4255-204">a.</span></span> <span data-ttu-id="d4255-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d4255-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d4255-206">b.</span><span class="sxs-lookup"><span data-stu-id="d4255-206">b.</span></span> <span data-ttu-id="d4255-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d4255-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d4255-208">c.</span><span class="sxs-lookup"><span data-stu-id="d4255-208">c.</span></span> <span data-ttu-id="d4255-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d4255-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d4255-210">d.</span><span class="sxs-lookup"><span data-stu-id="d4255-210">d.</span></span> <span data-ttu-id="d4255-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d4255-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="d4255-212">Création d’un utilisateur de test Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="d4255-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="d4255-213">Pour permettre aux utilisateurs Azure AD de se connecter à Mozy Enterprise, vous devez les approvisionner dans Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d4255-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="d4255-214">Dans le cas de Mozy Enterprise, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="d4255-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="d4255-215">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Mozy Enterprise pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d4255-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="d4255-216">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d4255-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="d4255-217">Connectez-vous à votre locataire **Mozy Enterprise** .</span><span class="sxs-lookup"><span data-stu-id="d4255-217">Log in to your **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="d4255-218">Cliquez sur **Users**, puis sur **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="d4255-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="d4255-219">![Utilisateurs](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="d4255-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d4255-220">L’option **Add New User** ne s’affiche que si **Mozy** est sélectionné comme fournisseur sous **Authentication policy**.</span><span class="sxs-lookup"><span data-stu-id="d4255-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="d4255-221">Si l’authentification SAML est configurée, les utilisateurs sont ajoutés automatiquement lors de la première connexion à l’aide de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d4255-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="d4255-222">Dans la boîte de dialogue New User, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d4255-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="d4255-223">![Ajouter des utilisateurs](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "ajouter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="d4255-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="d4255-224">a.</span><span class="sxs-lookup"><span data-stu-id="d4255-224">a.</span></span> <span data-ttu-id="d4255-225">Dans la liste **Choose a Group** , sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="d4255-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="d4255-226">b.</span><span class="sxs-lookup"><span data-stu-id="d4255-226">b.</span></span> <span data-ttu-id="d4255-227">Dans la liste **What type of user** , sélectionnez un type.</span><span class="sxs-lookup"><span data-stu-id="d4255-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="d4255-228">c.</span><span class="sxs-lookup"><span data-stu-id="d4255-228">c.</span></span> <span data-ttu-id="d4255-229">Dans la zone de texte **Username** , tapez le nom de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4255-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="d4255-230">d.</span><span class="sxs-lookup"><span data-stu-id="d4255-230">d.</span></span> <span data-ttu-id="d4255-231">Dans la zone de texte **Email** , tapez l’adresse de messagerie de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4255-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="d4255-232">e.</span><span class="sxs-lookup"><span data-stu-id="d4255-232">e.</span></span> <span data-ttu-id="d4255-233">Sélectionnez **Send user instruction email**.</span><span class="sxs-lookup"><span data-stu-id="d4255-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="d4255-234">f.</span><span class="sxs-lookup"><span data-stu-id="d4255-234">f.</span></span> <span data-ttu-id="d4255-235">Cliquez sur **Add User(s)**.</span><span class="sxs-lookup"><span data-stu-id="d4255-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="d4255-236">Après la création de l’utilisateur, un message électronique sera envoyé à l’utilisateur Azure AD avec un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="d4255-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d4255-237">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4255-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d4255-238">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Mozy Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d4255-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d4255-240">**Pour affecter Britta Simon à Mozy Enterprise, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d4255-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="d4255-241">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d4255-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d4255-243">Dans la liste des applications, sélectionnez **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="d4255-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="d4255-245">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d4255-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d4255-247">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d4255-247">Click **Add** button.</span></span> <span data-ttu-id="d4255-248">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d4255-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d4255-250">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d4255-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d4255-251">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d4255-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d4255-252">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d4255-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d4255-253">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d4255-253">Testing single sign-on</span></span>

<span data-ttu-id="d4255-254">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d4255-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d4255-255">Lorsque vous cliquez sur la vignette Mozy Enterprise dans le panneau d’accès, la page de connexion de l’application Mozy Enterprise doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="d4255-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="d4255-256">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d4255-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d4255-257">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d4255-257">Additional resources</span></span>

* [<span data-ttu-id="d4255-258">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4255-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d4255-259">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d4255-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

