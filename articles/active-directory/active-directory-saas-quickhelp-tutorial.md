---
title: "Didacticiel : Intégration d’Azure Active Directory à QuickHelp | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et QuickHelp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="fbb21-103">Didacticiel : intégration d’Azure Active Directory à QuickHelp</span><span class="sxs-lookup"><span data-stu-id="fbb21-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="fbb21-104">Dans ce didacticiel, vous allez apprendre à intégrer QuickHelp avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbb21-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbb21-105">L’intégration de QuickHelp dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fbb21-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fbb21-106">Dans Azure AD, vous pouvez contrôler qui a accès à QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="fbb21-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="fbb21-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à QuickHelp (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbb21-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbb21-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="fbb21-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fbb21-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbb21-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbb21-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="fbb21-110">Prerequisites</span></span>

<span data-ttu-id="fbb21-111">Pour configurer l’intégration d’Azure AD à QuickHelp, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fbb21-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="fbb21-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbb21-113">Un abonnement QuickHelp pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fbb21-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbb21-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fbb21-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbb21-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fbb21-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbb21-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fbb21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbb21-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbb21-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbb21-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fbb21-118">Scenario description</span></span>
<span data-ttu-id="fbb21-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fbb21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbb21-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="fbb21-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbb21-121">Ajout de QuickHelp à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="fbb21-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="fbb21-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="fbb21-123">Ajout de QuickHelp à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="fbb21-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="fbb21-124">Pour configurer l’intégration de QuickHelp à Azure AD, vous devez ajouter QuickHelp à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="fbb21-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fbb21-125">**Pour ajouter QuickHelp à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbb21-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fbb21-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbb21-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fbb21-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="fbb21-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fbb21-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="fbb21-133">Dans la zone de recherche, tapez **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-133">In the search box, type **QuickHelp**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="fbb21-135">Dans le volet de résultats, sélectionnez **QuickHelp**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="fbb21-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbb21-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbb21-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec QuickHelp sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fbb21-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbb21-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur QuickHelp équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbb21-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="fbb21-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur QuickHelp associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="fbb21-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="fbb21-141">Dans QuickHelp, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="fbb21-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fbb21-142">Pour configurer et tester l’authentification unique Azure AD avec QuickHelp, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="fbb21-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fbb21-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fbb21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fbb21-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbb21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbb21-145">**[Création d’un utilisateur de test QuickHelp](#creating-a-quickhelp-test-user)** pour avoir un équivalent de Britta Simon dans QuickHelp lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="fbb21-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbb21-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbb21-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbb21-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="fbb21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbb21-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbb21-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="fbb21-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="fbb21-150">**Pour configurer l’authentification unique Azure AD avec QuickHelp, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbb21-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="fbb21-151">Dans le portail Azure, sur la page d’intégration de l’application **QuickHelp**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="fbb21-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fbb21-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="fbb21-155">Dans la section **Domaine et URL QuickHelp**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbb21-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="fbb21-157">a.</span><span class="sxs-lookup"><span data-stu-id="fbb21-157">a.</span></span> <span data-ttu-id="fbb21-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="fbb21-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="fbb21-159">b.</span><span class="sxs-lookup"><span data-stu-id="fbb21-159">b.</span></span> <span data-ttu-id="fbb21-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="fbb21-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbb21-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="fbb21-161">These values are not real.</span></span> <span data-ttu-id="fbb21-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="fbb21-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fbb21-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique QuickHelp](https://support.quickhelp.com/).</span><span class="sxs-lookup"><span data-stu-id="fbb21-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="fbb21-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fbb21-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="fbb21-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fbb21-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="fbb21-168">Connectez-vous à votre site d’entreprise QuickHelp en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fbb21-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="fbb21-169">Dans le menu situé en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configurer l’authentification unique][21]

8. <span data-ttu-id="fbb21-171">Dans le menu **QuickHelp Admin** (Administration de QuickHelp), cliquez sur **Settings** (Paramètres).</span><span class="sxs-lookup"><span data-stu-id="fbb21-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configurer l’authentification unique][22]

9. <span data-ttu-id="fbb21-173">Cliquez sur **Authentication Settings**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="fbb21-174">Dans la page **Authentication Settings** (Paramètres d’authentification), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbb21-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Configurer l’authentification unique][23]
   
    <span data-ttu-id="fbb21-176">a.</span><span class="sxs-lookup"><span data-stu-id="fbb21-176">a.</span></span> <span data-ttu-id="fbb21-177">Pour **SSO Type**, sélectionnez **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="fbb21-178">b.</span><span class="sxs-lookup"><span data-stu-id="fbb21-178">b.</span></span> <span data-ttu-id="fbb21-179">Pour charger votre fichier de métadonnées Azure téléchargé, cliquez sur **Browse**, accédez au fichier, puis cliquez sur **Upload Metadata**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="fbb21-180">c.</span><span class="sxs-lookup"><span data-stu-id="fbb21-180">c.</span></span> <span data-ttu-id="fbb21-181">Dans la zone de texte **Email** (E-mail), tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="fbb21-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="fbb21-182">d.</span><span class="sxs-lookup"><span data-stu-id="fbb21-182">d.</span></span> <span data-ttu-id="fbb21-183">Dans la zone de texte **First Name** (Prénom), tapez `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="fbb21-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="fbb21-184">e.</span><span class="sxs-lookup"><span data-stu-id="fbb21-184">e.</span></span> <span data-ttu-id="fbb21-185">Dans la zone de texte **Last Name** (Nom), tapez `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="fbb21-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="fbb21-186">f.</span><span class="sxs-lookup"><span data-stu-id="fbb21-186">f.</span></span> <span data-ttu-id="fbb21-187">Dans la **barre d’actions**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fbb21-188">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="fbb21-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fbb21-189">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="fbb21-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fbb21-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbb21-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbb21-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb21-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbb21-192">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb21-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="fbb21-194">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbb21-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fbb21-195">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbb21-197">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbb21-199">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fbb21-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbb21-201">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbb21-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbb21-203">a.</span><span class="sxs-lookup"><span data-stu-id="fbb21-203">a.</span></span> <span data-ttu-id="fbb21-204">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbb21-205">b.</span><span class="sxs-lookup"><span data-stu-id="fbb21-205">b.</span></span> <span data-ttu-id="fbb21-206">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbb21-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbb21-207">c.</span><span class="sxs-lookup"><span data-stu-id="fbb21-207">c.</span></span> <span data-ttu-id="fbb21-208">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fbb21-209">d.</span><span class="sxs-lookup"><span data-stu-id="fbb21-209">d.</span></span> <span data-ttu-id="fbb21-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="fbb21-211">Création d’un utilisateur de test QuickHelp</span><span class="sxs-lookup"><span data-stu-id="fbb21-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="fbb21-212">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="fbb21-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="fbb21-213">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur QuickHelp équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbb21-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="fbb21-214">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur QuickHelp associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="fbb21-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="fbb21-215">QuickHelp prend en charge l’approvisionnement juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="fbb21-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="fbb21-216">Cela signifie que, si nécessaire, un compte d’utilisateur est automatiquement créé dans QuickHelp et qu’il est lié au compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbb21-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="fbb21-217">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="fbb21-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fbb21-218">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbb21-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fbb21-219">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="fbb21-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="fbb21-221">**Pour affecter Britta Simon à QuickHelp, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbb21-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="fbb21-222">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fbb21-224">Dans la liste des applications, sélectionnez **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-224">In the applications list, select **QuickHelp**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="fbb21-226">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="fbb21-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-228">Click **Add** button.</span></span> <span data-ttu-id="fbb21-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="fbb21-231">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fbb21-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fbb21-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbb21-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fbb21-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbb21-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fbb21-234">Testing single sign-on</span></span>

<span data-ttu-id="fbb21-235">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="fbb21-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="fbb21-236">Quand vous cliquez sur la vignette QuickHelp dans le volet d’accès, vous devez être connecté automatiquement à votre application QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="fbb21-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fbb21-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fbb21-237">Additional resources</span></span>

* [<span data-ttu-id="fbb21-238">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbb21-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbb21-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fbb21-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
