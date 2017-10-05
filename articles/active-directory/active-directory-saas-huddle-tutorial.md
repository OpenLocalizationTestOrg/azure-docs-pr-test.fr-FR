---
title: "Didacticiel : Intégration d’Azure Active Directory avec Huddle | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="e3d32-103">Didacticiel : Intégration d’Azure Active Directory avec Huddle</span><span class="sxs-lookup"><span data-stu-id="e3d32-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="e3d32-104">Dans ce didacticiel, vous allez apprendre à intégrer Huddle à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3d32-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3d32-105">L’intégration de Huddle dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e3d32-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e3d32-106">Dans Azure AD, vous pouvez contrôler qui a accès à Huddle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="e3d32-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Huddle (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3d32-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e3d32-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="e3d32-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e3d32-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3d32-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3d32-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e3d32-110">Prerequisites</span></span>

<span data-ttu-id="e3d32-111">Pour configurer l’intégration d’Azure AD avec Huddle, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e3d32-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="e3d32-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3d32-113">Un abonnement Huddle pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e3d32-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3d32-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e3d32-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3d32-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e3d32-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3d32-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e3d32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3d32-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3d32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3d32-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e3d32-118">Scenario description</span></span>

<span data-ttu-id="e3d32-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e3d32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3d32-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3d32-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3d32-121">Ajout de Huddle depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="e3d32-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="e3d32-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="e3d32-123">Ajout de Huddle depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="e3d32-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="e3d32-124">Pour configurer l’intégration de Huddle avec Azure AD, vous devez ajouter Huddle à votre liste d’applications SaaS gérées, à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="e3d32-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e3d32-125">**Pour ajouter Huddle à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d32-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e3d32-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e3d32-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e3d32-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e3d32-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e3d32-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e3d32-133">Dans la zone de recherche, entrez **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-133">In the search box, type **Huddle**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="e3d32-135">Dans le panneau des résultats, sélectionnez **Huddle**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="e3d32-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e3d32-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d32-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="e3d32-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Huddle avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e3d32-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e3d32-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Huddle équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3d32-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="e3d32-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Huddle associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="e3d32-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="e3d32-141">Dans Huddle, attribuez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="e3d32-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e3d32-142">Pour configurer et tester l’authentification unique Azure AD avec Huddle, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3d32-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e3d32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e3d32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="e3d32-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3d32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="e3d32-145">**[Création d’un utilisateur de test Huddle](#creating-a-huddle-test-user)** pour obtenir un équivalent de Britta Simon dans Huddle lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3d32-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="e3d32-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3d32-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="e3d32-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="e3d32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e3d32-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e3d32-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Huddle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="e3d32-150">**Pour configurer l’authentification unique Azure AD avec Huddle, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d32-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="e3d32-151">Dans le portail Azure, sur la page d’intégration de l’application **Huddle**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e3d32-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3d32-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="e3d32-155">Dans la section **Domaine et URL Huddle**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3d32-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="e3d32-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="e3d32-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3d32-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-158">This value is not real.</span></span> <span data-ttu-id="e3d32-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e3d32-160">Contactez [l’équipe de support technique Huddle](https://huddle.zendesk.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="e3d32-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="e3d32-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e3d32-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="e3d32-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e3d32-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e3d32-165">Dans la section **Configuration de Huddle**, cliquez sur **Configurer Huddle** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e3d32-166">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="e3d32-168">Pour configurer l’authentification unique côté Huddle, vous devez envoyer le **Certificat** téléchargé, **l’ID d’entité SAML** et **l’URL du service d’authentification unique SAML** à [l’équipe de support technique Huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="e3d32-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="e3d32-169">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="e3d32-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="e3d32-170">L’authentification unique doit être activée par l’équipe du support technique Huddle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="e3d32-171">Vous recevrez une notification une fois la configuration terminée.</span><span class="sxs-lookup"><span data-stu-id="e3d32-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="e3d32-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="e3d32-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e3d32-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="e3d32-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e3d32-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3d32-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e3d32-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d32-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="e3d32-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d32-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e3d32-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d32-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e3d32-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e3d32-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e3d32-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e3d32-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e3d32-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3d32-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e3d32-187">a.</span><span class="sxs-lookup"><span data-stu-id="e3d32-187">a.</span></span> <span data-ttu-id="e3d32-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3d32-189">b.</span><span class="sxs-lookup"><span data-stu-id="e3d32-189">b.</span></span> <span data-ttu-id="e3d32-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3d32-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e3d32-191">c.</span><span class="sxs-lookup"><span data-stu-id="e3d32-191">c.</span></span> <span data-ttu-id="e3d32-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e3d32-193">d.</span><span class="sxs-lookup"><span data-stu-id="e3d32-193">d.</span></span> <span data-ttu-id="e3d32-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="e3d32-195">Création d’un utilisateur de test Huddle</span><span class="sxs-lookup"><span data-stu-id="e3d32-195">Creating a Huddle test user</span></span>

<span data-ttu-id="e3d32-196">Pour se connecter à Huddle, les utilisateurs d’Azure AD doivent être configurés dans Huddle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="e3d32-197">Dans le cas de Huddle, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="e3d32-198">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d32-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e3d32-199">Connectez-vous à votre site d’entreprise **Huddle** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e3d32-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="e3d32-200">Cliquez sur **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="e3d32-201">Cliquez sur **People \> Invite People**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="e3d32-202">![Personnes](./media/active-directory-saas-huddle-tutorial/IC787838.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="e3d32-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="e3d32-203">Dans la section **Create a new invitation** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3d32-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="e3d32-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span><span class="sxs-lookup"><span data-stu-id="e3d32-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="e3d32-205">a.</span><span class="sxs-lookup"><span data-stu-id="e3d32-205">a.</span></span> <span data-ttu-id="e3d32-206">Dans la liste **Choose a team to invite people to join**, sélectionnez **team**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="e3d32-207">b.</span><span class="sxs-lookup"><span data-stu-id="e3d32-207">b.</span></span> <span data-ttu-id="e3d32-208">Entrez l’**adresse e-mail** associée au compte Azure AD valide que vous souhaitez configurer dans la zone de texte **Entrer l’adresse e-mail des personnes que vous souhaitez inviter**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="e3d32-209">c.</span><span class="sxs-lookup"><span data-stu-id="e3d32-209">c.</span></span> <span data-ttu-id="e3d32-210">Cliquez sur **Inviter**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="e3d32-211">Le titulaire du compte Azure AD reçoit alors un message électronique contenant un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="e3d32-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="e3d32-212">Vous pouvez utiliser n’importe quels autres outils ou API de création de compte d’utilisateur Huddle fourni par ce site pour configurer des comptes d’utilisateurs Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3d32-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e3d32-213">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d32-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e3d32-214">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Huddle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e3d32-216">**Pour affecter Britta Simon à Huddle, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d32-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="e3d32-217">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e3d32-219">Dans la liste des applications, sélectionnez **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-219">In the applications list, select **Huddle**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="e3d32-221">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e3d32-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-223">Click **Add** button.</span></span> <span data-ttu-id="e3d32-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e3d32-226">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e3d32-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e3d32-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3d32-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3d32-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e3d32-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e3d32-229">Testing single sign-on</span></span>

<span data-ttu-id="e3d32-230">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="e3d32-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e3d32-231">Lorsque vous cliquez sur la vignette Huddle dans le panneau d’accès, vous accédez automatiquement à la page de connexion Huddle.</span><span class="sxs-lookup"><span data-stu-id="e3d32-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="e3d32-232">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3d32-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3d32-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e3d32-233">Additional resources</span></span>

* [<span data-ttu-id="e3d32-234">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3d32-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3d32-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e3d32-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
