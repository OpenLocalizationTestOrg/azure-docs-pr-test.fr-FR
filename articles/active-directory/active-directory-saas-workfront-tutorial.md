---
title: "Didacticiel : Intégration d’Azure Active Directory avec Workfront | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Workfront."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: f7ba8d4895474de0da0e04da5f31959963ae65ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="ef2fe-103">Didacticiel : Intégration d’Azure Active Directory avec Workfront</span><span class="sxs-lookup"><span data-stu-id="ef2fe-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="ef2fe-104">Dans ce didacticiel, vous allez apprendre à intégrer Workfront à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef2fe-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef2fe-105">L’intégration de Workfront dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ef2fe-106">Dans Azure AD, vous pouvez contrôler qui a accès à Workfront</span><span class="sxs-lookup"><span data-stu-id="ef2fe-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="ef2fe-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Workfront (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2fe-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ef2fe-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ef2fe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ef2fe-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ef2fe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef2fe-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ef2fe-110">Prerequisites</span></span>

<span data-ttu-id="ef2fe-111">Pour configurer l’intégration d’Azure AD à Workfront, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="ef2fe-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef2fe-113">Un abonnement Workfront pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ef2fe-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef2fe-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ef2fe-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef2fe-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ef2fe-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef2fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef2fe-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ef2fe-118">Scenario description</span></span>
<span data-ttu-id="ef2fe-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef2fe-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef2fe-121">Ajout de Workfront à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ef2fe-121">Adding Workfront from the gallery</span></span>
2. <span data-ttu-id="ef2fe-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="ef2fe-123">Ajout de Workfront à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ef2fe-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="ef2fe-124">Pour configurer l’intégration de Workfront à Azure AD, vous devez ajouter Workfront à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef2fe-125">**Pour ajouter Workfront à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef2fe-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2fe-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ef2fe-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ef2fe-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ef2fe-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ef2fe-133">Dans la zone de recherche, tapez **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-133">In the search box, type **Workfront**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_search.png)

5. <span data-ttu-id="ef2fe-135">Dans le volet des résultats, sélectionnez **Workfront**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef2fe-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef2fe-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workfront, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ef2fe-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ef2fe-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Workfront équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="ef2fe-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Workfront associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="ef2fe-141">Dans Workfront, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ef2fe-142">Pour configurer et tester l’authentification unique Azure AD avec Workfront, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef2fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef2fe-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef2fe-145">**[Création d’un utilisateur de test Workfront](#creating-a-workfront-test-user)** pour avoir un équivalent de Britta Simon dans Workfront lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef2fe-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef2fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef2fe-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ef2fe-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Workfront.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="ef2fe-150">**Pour configurer l’authentification unique Azure AD avec Workfront, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef2fe-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2fe-151">Dans le portail Azure, sur la page d’intégration de l’application **Workfront**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ef2fe-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_samlbase.png)

3. <span data-ttu-id="ef2fe-155">Dans la section **Domaine et URL Workfront**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="ef2fe-157">a.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-157">a.</span></span> <span data-ttu-id="ef2fe-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="ef2fe-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="ef2fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-159">b.</span></span> <span data-ttu-id="ef2fe-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="ef2fe-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef2fe-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-161">These values are not real.</span></span> <span data-ttu-id="ef2fe-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ef2fe-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Workfront](https://www.workfront.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="ef2fe-163">Contact [Workfront Client support team](https://www.workfront.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="ef2fe-164">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (Base64)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_certificate.png) 

5. <span data-ttu-id="ef2fe-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ef2fe-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ef2fe-168">Dans la section **Configuration de Workfront**, cliquez sur **Configurer Workfront** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ef2fe-169">Copiez l’**URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_configure.png) 

7. <span data-ttu-id="ef2fe-171">Connectez-vous à votre site d’entreprise Workfront en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-171">Sign-on to your Workfront company site as administrator.</span></span>

8. <span data-ttu-id="ef2fe-172">Accédez à **Single Sign On Configuration**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-172">Go to **Single Sign On Configuration**.</span></span>

9. <span data-ttu-id="ef2fe-173">Dans la boîte de dialogue **Authentification unique** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Configurer l’authentification unique][23]
   
    <span data-ttu-id="ef2fe-175">a.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-175">a.</span></span> <span data-ttu-id="ef2fe-176">Comme **Type**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="ef2fe-177">b.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-177">b.</span></span> <span data-ttu-id="ef2fe-178">Sélectionnez **///ID fournisseur de services**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="ef2fe-179">c.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-179">c.</span></span> <span data-ttu-id="ef2fe-180">Coller l’**URL du service d’authentification unique SAML** dans la zone de texte **URL du portail de connexion**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="ef2fe-181">d.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-181">d.</span></span> <span data-ttu-id="ef2fe-182">Collez l’**URL du service de déconnexion unique** dans la zone de texte **URL de déconnexion**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="ef2fe-183">e.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-183">e.</span></span> <span data-ttu-id="ef2fe-184">Collez l’**URL de modification du mot de passe** dans la zone de texte **URL de modification du mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="ef2fe-185">f.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-185">f.</span></span> <span data-ttu-id="ef2fe-186">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ef2fe-187">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ef2fe-188">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ef2fe-189">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ef2fe-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef2fe-190">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2fe-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef2fe-191">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ef2fe-193">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef2fe-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2fe-194">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef2fe-196">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef2fe-198">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef2fe-200">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef2fe-202">a.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-202">a.</span></span> <span data-ttu-id="ef2fe-203">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef2fe-204">b.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-204">b.</span></span> <span data-ttu-id="ef2fe-205">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef2fe-206">c.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-206">c.</span></span> <span data-ttu-id="ef2fe-207">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ef2fe-208">d.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-208">d.</span></span> <span data-ttu-id="ef2fe-209">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="ef2fe-210">Création d’un utilisateur de test Workfront</span><span class="sxs-lookup"><span data-stu-id="ef2fe-210">Creating a Workfront test user</span></span>

<span data-ttu-id="ef2fe-211">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Workfront.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="ef2fe-212">**Pour créer un utilisateur appelé Britta Simon dans Workfront, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef2fe-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2fe-213">Connectez-vous à votre site d’entreprise Workfront en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-213">Sign on to your Workfront company site as administrator.</span></span>
2. <span data-ttu-id="ef2fe-214">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-214">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="ef2fe-215">Cliquez sur **New Person**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-215">Click **New Person**.</span></span> 
4. <span data-ttu-id="ef2fe-216">Dans la boîte de dialogue New User, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ef2fe-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Créer un utilisateur de test Workfront][21] 
   
    <span data-ttu-id="ef2fe-218">a.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-218">a.</span></span> <span data-ttu-id="ef2fe-219">Dans la zone de texte **Prénom**, tapez « Britta ».</span><span class="sxs-lookup"><span data-stu-id="ef2fe-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="ef2fe-220">b.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-220">b.</span></span> <span data-ttu-id="ef2fe-221">Dans la zone de texte **Nom**, tapez « Simon ».</span><span class="sxs-lookup"><span data-stu-id="ef2fe-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="ef2fe-222">c.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-222">c.</span></span> <span data-ttu-id="ef2fe-223">Dans la zone de texte **Adresse de messagerie** , tapez l'adresse de messagerie de Simon Britta dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="ef2fe-224">d.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-224">d.</span></span> <span data-ttu-id="ef2fe-225">Cliquez sur **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ef2fe-226">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef2fe-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ef2fe-227">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Workfront.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ef2fe-229">**Pour affecter Britta Simon à Workfront, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef2fe-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="ef2fe-230">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ef2fe-232">Dans la liste des applications, sélectionnez **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-232">In the applications list, select **Workfront**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-workfront-tutorial/tutorial_workfront_app.png) 

3. <span data-ttu-id="ef2fe-234">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ef2fe-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-236">Click **Add** button.</span></span> <span data-ttu-id="ef2fe-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ef2fe-239">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ef2fe-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef2fe-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ef2fe-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ef2fe-242">Testing single sign-on</span></span>

<span data-ttu-id="ef2fe-243">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ef2fe-244">Lorsque vous cliquez sur la mosaïque Workfront dans le volet d’accès, la page de connexion de l’application Workfront devrait apparaître.</span><span class="sxs-lookup"><span data-stu-id="ef2fe-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="ef2fe-245">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef2fe-245">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ef2fe-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ef2fe-246">Additional resources</span></span>

* [<span data-ttu-id="ef2fe-247">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef2fe-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef2fe-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ef2fe-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_04.png
[21]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_08.png
[23]:./media/active-directory-saas-workfront-tutorial/tutorial_attask_06.png
[100]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workfront-tutorial/tutorial_general_203.png

