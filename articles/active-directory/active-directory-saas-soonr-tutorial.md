---
title: "Didacticiel : Intégration d’Azure Active Directory à Soonr Workplace | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Soonr Workplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="9599e-103">Didacticiel : Intégration d’Azure Active Directory à Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="9599e-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="9599e-104">L’objectif de ce didacticiel est de vous montrer comment intégrer Soonr Workplace à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9599e-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="9599e-105">L’intégration de Soonr Workplace à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9599e-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9599e-106">Dans Azure AD, vous pouvez contrôler qui a accès à Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="9599e-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="9599e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Soonr Workplace (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9599e-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9599e-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="9599e-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="9599e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9599e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9599e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9599e-110">Prerequisites</span></span>

<span data-ttu-id="9599e-111">Pour configurer l’intégration d’Azure AD à Soonr Workplace, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9599e-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="9599e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9599e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9599e-113">Un abonnement Soonr Workplace pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9599e-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="9599e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9599e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="9599e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9599e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9599e-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9599e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9599e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9599e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="9599e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9599e-118">Scenario description</span></span>
<span data-ttu-id="9599e-119">Ce didacticiel vise à vous permettre de tester l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9599e-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="9599e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9599e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9599e-121">Ajout de Soonr Workplace à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9599e-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="9599e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9599e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="9599e-123">Ajout de Soonr Workplace à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9599e-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="9599e-124">Pour configurer l’intégration de Soonr Workplace à Azure AD, vous devez ajouter Soonr Workplace à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9599e-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9599e-125">**Pour ajouter Soonr Workplace à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9599e-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9599e-126">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9599e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9599e-128">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="9599e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="9599e-129">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="9599e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="9599e-131">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="9599e-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="9599e-133">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="9599e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Applications][4]

6. <span data-ttu-id="9599e-135">Dans la zone de recherche, tapez **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="9599e-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="9599e-137">Dans le volet de résultats, sélectionnez **Soonr Workplace**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9599e-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9599e-139">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9599e-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9599e-140">L’objectif de cette section est de vous montrer comment configurer et tester l’authentification unique Azure AD avec Soonr Workplace, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9599e-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9599e-141">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Soonr Workplace équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9599e-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="9599e-142">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Soonr Workplace associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="9599e-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="9599e-143">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="9599e-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="9599e-144">Pour configurer et tester l’authentification unique Azure AD avec Soonr Workplace, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="9599e-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9599e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9599e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9599e-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9599e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9599e-147">**[Création d’un utilisateur de test Soonr Workplace](#creating-a-soonr-workplace-test-user)** : pour avoir un équivalent de Britta Simon dans Soonr Workplace lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="9599e-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9599e-148">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d'utiliser l'authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9599e-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9599e-149">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9599e-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9599e-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9599e-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9599e-151">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure Classic et configurer l’authentification unique dans votre application Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="9599e-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="9599e-152">**Pour configurer l’authentification unique Azure AD avec Soonr Workplace, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9599e-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="9599e-153">Dans le portail Azure Classic, sur la page d’intégration d’applications **Soonr Workplace**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9599e-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Configurer l’authentification unique][6] 

2. <span data-ttu-id="9599e-155">Sur la page **Comment voulez-vous que les utilisateurs se connectent à Soonr Workplace**, sélectionnez **Authentification unique Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9599e-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="9599e-157">Sur la page de boîte de dialogue **Configurer les paramètres de l’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9599e-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="9599e-159">a.</span><span class="sxs-lookup"><span data-stu-id="9599e-159">a.</span></span> <span data-ttu-id="9599e-160">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="9599e-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="9599e-161">b.</span><span class="sxs-lookup"><span data-stu-id="9599e-161">b.</span></span> <span data-ttu-id="9599e-162">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9599e-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9599e-163">Notez qu’il ne s’agit pas de la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="9599e-163">Please note that this is not the real value.</span></span> <span data-ttu-id="9599e-164">Vous devez mettre à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="9599e-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="9599e-165">Contactez l’équipe de support technique de Soonr Workplace pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="9599e-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="9599e-166">Sur la page **Configurer l’authentification unique sur Soonr Workplace**, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="9599e-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="9599e-168">Pour obtenir la configuration de l’authentification unique pour votre application, contactez l’équipe de support Soonr Workplace et envoyez-lui les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9599e-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="9599e-169">•  Le fichier de **métadonnées téléchargé**</span><span class="sxs-lookup"><span data-stu-id="9599e-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="9599e-170">• **L’URL de l’émetteur**</span><span class="sxs-lookup"><span data-stu-id="9599e-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="9599e-171">• L’**URL d’authentification unique SAML**</span><span class="sxs-lookup"><span data-stu-id="9599e-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="9599e-172">•  **L’URL du service de déconnexion unique**</span><span class="sxs-lookup"><span data-stu-id="9599e-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="9599e-173">Cette application est remplacée par <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> et vous pouvez vous reporter à <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">ce</a> didacticiel pour la configuration de l’application avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9599e-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="9599e-174">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9599e-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Authentification unique Azure AD][10]

7. <span data-ttu-id="9599e-176">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="9599e-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Authentification unique Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9599e-178">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9599e-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="9599e-179">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="9599e-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="9599e-181">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9599e-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9599e-182">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9599e-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="9599e-184">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="9599e-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="9599e-185">Pour afficher la liste des utilisateurs, dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9599e-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9599e-187">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="9599e-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="9599e-189">Sur la page de boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9599e-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="9599e-191">a.</span><span class="sxs-lookup"><span data-stu-id="9599e-191">a.</span></span> <span data-ttu-id="9599e-192">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="9599e-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="9599e-193">b.</span><span class="sxs-lookup"><span data-stu-id="9599e-193">b.</span></span> <span data-ttu-id="9599e-194">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9599e-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9599e-195">c.</span><span class="sxs-lookup"><span data-stu-id="9599e-195">c.</span></span> <span data-ttu-id="9599e-196">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9599e-196">Click **Next**.</span></span>

6.  <span data-ttu-id="9599e-197">Sur la page de boîte de dialogue **Profil utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9599e-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="9599e-199">a.</span><span class="sxs-lookup"><span data-stu-id="9599e-199">a.</span></span> <span data-ttu-id="9599e-200">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9599e-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="9599e-201">b.</span><span class="sxs-lookup"><span data-stu-id="9599e-201">b.</span></span> <span data-ttu-id="9599e-202">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9599e-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="9599e-203">c.</span><span class="sxs-lookup"><span data-stu-id="9599e-203">c.</span></span> <span data-ttu-id="9599e-204">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9599e-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="9599e-205">d.</span><span class="sxs-lookup"><span data-stu-id="9599e-205">d.</span></span> <span data-ttu-id="9599e-206">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="9599e-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="9599e-207">e.</span><span class="sxs-lookup"><span data-stu-id="9599e-207">e.</span></span> <span data-ttu-id="9599e-208">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9599e-208">Click **Next**.</span></span>

7. <span data-ttu-id="9599e-209">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="9599e-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="9599e-211">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9599e-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="9599e-213">a.</span><span class="sxs-lookup"><span data-stu-id="9599e-213">a.</span></span> <span data-ttu-id="9599e-214">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9599e-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="9599e-215">b.</span><span class="sxs-lookup"><span data-stu-id="9599e-215">b.</span></span> <span data-ttu-id="9599e-216">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="9599e-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="9599e-217">Création d’un utilisateur de test Soonr Workplace</span><span class="sxs-lookup"><span data-stu-id="9599e-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="9599e-218">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="9599e-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="9599e-219">Collaborez avec l’équipe de support technique de Soonr Workplace pour créer un utilisateur dans la plateforme.</span><span class="sxs-lookup"><span data-stu-id="9599e-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="9599e-220">Vous pouvez soumettre un ticket de support avec Soonr <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">à partir d’ici</a>.</span><span class="sxs-lookup"><span data-stu-id="9599e-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9599e-221">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9599e-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9599e-222">L’objectif de cette section est de permettre à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="9599e-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9599e-224">**Pour affecter Britta Simon à Soonr Workplace, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9599e-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="9599e-225">Pour ouvrir l’affichage des applications dans le portail Azure Classic, cliquez dans la vue de répertoire sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="9599e-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9599e-227">Dans la liste des applications, sélectionnez **Soonr Workplace**.</span><span class="sxs-lookup"><span data-stu-id="9599e-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="9599e-229">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9599e-229">In the menu on the top, click **Users**.</span></span>

    ![Affecter des utilisateurs][203] 

1. <span data-ttu-id="9599e-231">Dans la liste Utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9599e-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="9599e-232">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="9599e-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Affecter des utilisateurs][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="9599e-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9599e-234">Testing single sign-on</span></span>

<span data-ttu-id="9599e-235">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9599e-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="9599e-236">Quand vous cliquez sur la vignette Soonr Workplace dans le volet d’accès, vous devez être connecté automatiquement à votre application Soonr Workplace.</span><span class="sxs-lookup"><span data-stu-id="9599e-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9599e-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9599e-237">Additional resources</span></span>

* [<span data-ttu-id="9599e-238">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9599e-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9599e-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9599e-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
