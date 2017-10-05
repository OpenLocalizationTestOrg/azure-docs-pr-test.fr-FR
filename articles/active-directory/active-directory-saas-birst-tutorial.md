---
title: "Didacticiel : Intégration d’Azure Active Directory à Birst Agile Business Analytics | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Birst Agile Business Analytics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 779f9e0a57ffb2274ea22a90ed9759734ab6916d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="447ec-103">Didacticiel : Intégration d’Azure Active Directory à Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="447ec-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="447ec-104">Dans ce didacticiel, vous allez découvrir comment intégrer Birst Agile Business Analytics avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="447ec-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="447ec-105">L’intégration de Birst Agile Business Analytics dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="447ec-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="447ec-106">Dans Azure AD, vous pouvez contrôler qui a accès à Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="447ec-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
- <span data-ttu-id="447ec-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Birst Agile Business Analytics (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="447ec-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="447ec-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="447ec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="447ec-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="447ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="447ec-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="447ec-110">Prerequisites</span></span>

<span data-ttu-id="447ec-111">Pour configurer l’intégration d’Azure AD à Birst Agile Business Analytics, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="447ec-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

- <span data-ttu-id="447ec-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="447ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="447ec-113">Un abonnement Birst Agile Business Analytics pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="447ec-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="447ec-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="447ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="447ec-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="447ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="447ec-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="447ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="447ec-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="447ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="447ec-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="447ec-118">Scenario description</span></span>
<span data-ttu-id="447ec-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="447ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="447ec-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="447ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="447ec-121">Ajout de Birst Agile Business Analytics à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="447ec-121">Adding Birst Agile Business Analytics from the gallery</span></span>
2. <span data-ttu-id="447ec-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="447ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="447ec-123">Ajout de Birst Agile Business Analytics à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="447ec-123">Adding Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="447ec-124">Pour configurer l’intégration de Birst Agile Business Analytics à Azure AD, vous devez ajouter Birst Agile Business Analytics à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="447ec-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="447ec-125">**Pour ajouter Birst Agile Business Analytics à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="447ec-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="447ec-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="447ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="447ec-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="447ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="447ec-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="447ec-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="447ec-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="447ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="447ec-133">Dans la zone de recherche, tapez **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="447ec-133">In the search box, type **Birst Agile Business Analytics**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="447ec-135">Dans le volet de résultats, sélectionnez **Birst Agile Business Analytics**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="447ec-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="447ec-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="447ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="447ec-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Birst Agile Business Analytics, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="447ec-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="447ec-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Birst Agile Business Analytics équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="447ec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="447ec-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Birst Agile Business Analytics associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="447ec-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="447ec-141">Dans Birst Agile Business Analytics, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="447ec-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="447ec-142">Pour configurer et tester l’authentification unique Azure AD avec Birst Agile Business Analytics, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="447ec-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="447ec-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="447ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="447ec-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="447ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="447ec-145">**[Création d’un utilisateur de test Birst Agile Business Analytics](#creating-a-birst-agile-business-analytics-test-user)** pour avoir un équivalent de Britta Simon dans Birst Agile Business Analytics, lié à sa représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="447ec-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="447ec-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="447ec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="447ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="447ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="447ec-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="447ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="447ec-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="447ec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="447ec-150">**Pour configurer l’authentification unique Azure AD avec Birst Agile Business Analytics, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="447ec-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="447ec-151">Dans le portail Azure, dans la page d’intégration de l’application **Birst Agile Business Analytics**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="447ec-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="447ec-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="447ec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="447ec-155">Dans la section **Domaine et URL Birst Agile Business Analytics**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="447ec-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="447ec-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="447ec-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="447ec-158">L’URL dépend du centre de données dans lequel se trouve votre compte Birst :</span><span class="sxs-lookup"><span data-stu-id="447ec-158">The URL depends on the datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="447ec-159">Pour le centre de données États-Unis, utilisez le modèle suivant : `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="447ec-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="447ec-160">Pour le centre de données Europe, utilisez le modèle suivant : `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="447ec-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="447ec-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="447ec-161">This value is not real.</span></span> <span data-ttu-id="447ec-162">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="447ec-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="447ec-163">Contact l’[équipe de support technique Birst Agile Business Analytics](mailto:info@birst.com) pour obtenir la valeur.</span><span class="sxs-lookup"><span data-stu-id="447ec-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span></span> 
 
4. <span data-ttu-id="447ec-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="447ec-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="447ec-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="447ec-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="447ec-168">Dans la section **Configuration de Birst Agile Business Analytics**, cliquez sur **Configurer Birst Agile Business Analytics** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="447ec-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="447ec-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="447ec-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="447ec-171">Pour configurer l’authentification unique côté **Birst Agile Business Analytics**, vous devez envoyer le **Certificat (Base64)** téléchargé, l’**URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à l’[équipe de support Birst Agile Business Analytics](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="447ec-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="447ec-172">Indiquez à l’équipe Birst que cette intégration nécessite l’algorithme SHA256 (SHA1 n’est pas pris en charge) pour que l’authentification unique puisse être définie sur le serveur approprié, comme **app2101**, etc.</span><span class="sxs-lookup"><span data-stu-id="447ec-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="447ec-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="447ec-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="447ec-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="447ec-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="447ec-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="447ec-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="447ec-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="447ec-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="447ec-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="447ec-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="447ec-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="447ec-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="447ec-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="447ec-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="447ec-182">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="447ec-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="447ec-184">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="447ec-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="447ec-186">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="447ec-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="447ec-188">a.</span><span class="sxs-lookup"><span data-stu-id="447ec-188">a.</span></span> <span data-ttu-id="447ec-189">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="447ec-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="447ec-190">b.</span><span class="sxs-lookup"><span data-stu-id="447ec-190">b.</span></span> <span data-ttu-id="447ec-191">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="447ec-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="447ec-192">c.</span><span class="sxs-lookup"><span data-stu-id="447ec-192">c.</span></span> <span data-ttu-id="447ec-193">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="447ec-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="447ec-194">d.</span><span class="sxs-lookup"><span data-stu-id="447ec-194">d.</span></span> <span data-ttu-id="447ec-195">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="447ec-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="447ec-196">Création d’un utilisateur de test Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="447ec-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="447ec-197">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="447ec-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="447ec-198">Collaborez avec l’[équipe du support technique Birst Agile Business Analytics](mailto:info@birst.com) pour ajouter des utilisateurs au compte Birst.</span><span class="sxs-lookup"><span data-stu-id="447ec-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="447ec-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="447ec-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="447ec-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="447ec-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="447ec-202">**Pour affecter Britta Simon à Birst Agile Business Analytics, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="447ec-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="447ec-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="447ec-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="447ec-205">Dans la liste des applications, sélectionnez **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="447ec-205">In the applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="447ec-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="447ec-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="447ec-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="447ec-209">Click **Add** button.</span></span> <span data-ttu-id="447ec-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="447ec-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="447ec-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="447ec-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="447ec-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="447ec-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="447ec-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="447ec-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="447ec-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="447ec-215">Testing single sign-on</span></span>

<span data-ttu-id="447ec-216">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="447ec-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="447ec-217">Lorsque vous cliquez sur la vignette Birst Agile Business Analytics dans le volet d’accès, vous devez être connecté automatiquement à votre application Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="447ec-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="447ec-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="447ec-218">Additional resources</span></span>

* [<span data-ttu-id="447ec-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="447ec-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="447ec-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="447ec-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

