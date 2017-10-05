---
title: "Didacticiel : Intégration d’Azure Active Directory à Bynder | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="ea078-103">Didacticiel : Intégration d’Azure Active Directory avec Bynder</span><span class="sxs-lookup"><span data-stu-id="ea078-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="ea078-104">L’objectif de ce didacticiel est de vous montrer comment intégrer Bynder avec Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ea078-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea078-105">L’intégration de Bynder à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ea078-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="ea078-106">Dans Azure AD, vous pouvez contrôler qui a accès à Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="ea078-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Bynder via l’authentification unique avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea078-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="ea078-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="ea078-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="ea078-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea078-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea078-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ea078-110">Prerequisites</span></span>
<span data-ttu-id="ea078-111">Pour configurer l’intégration d’Azure AD avec Bynder, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ea078-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="ea078-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea078-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ea078-113">Un abonnement Bynder pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ea078-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="ea078-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ea078-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="ea078-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ea078-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ea078-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ea078-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ea078-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea078-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea078-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ea078-118">Scenario description</span></span>
<span data-ttu-id="ea078-119">Ce didacticiel vise à vous permettre de tester l’authentification unique Microsoft Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ea078-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="ea078-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea078-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea078-121">Ajout de Bynder depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="ea078-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="ea078-122">Configuration et test de l’authentification unique Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea078-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="ea078-123">Ajouter Bynder à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ea078-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="ea078-124">Pour configurer l’intégration de Bynder avec Azure AD, vous devez ajouter Bynder, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ea078-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ea078-125">**Pour ajouter Bynder à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea078-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ea078-126">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea078-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="ea078-128">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="ea078-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ea078-129">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="ea078-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="ea078-131">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="ea078-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="ea078-133">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="ea078-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="ea078-135">Dans la zone de recherche, tapez **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="ea078-135">In the search box, type **Bynder**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="ea078-137">Dans le volet des résultats, sélectionnez **Bynder**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ea078-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![Sélection de l’application dans la galerie](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="ea078-139">Configurer et tester l’authentification unique Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea078-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="ea078-140">L’objectif de cette section est de vous montrer comment configurer et tester l’authentification unique Microsoft Azure AD avec Bynder au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ea078-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ea078-141">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Bynder équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea078-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="ea078-142">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Bynder associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ea078-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="ea078-143">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="ea078-144">Pour configurer et tester l’authentification unique Microsoft Azure AD avec Bynder, vous devez suivre les indications des sections ci-après :</span><span class="sxs-lookup"><span data-stu-id="ea078-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ea078-145">**[Configuration de l’authentification unique Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ea078-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ea078-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Microsoft Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ea078-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="ea078-147">**[Création d’un utilisateur de test Bynder](#creating-a-bynder-test-user)** pour avoir un équivalent de Britta Simon dans Bynder, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="ea078-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ea078-148">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Microsoft Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea078-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="ea078-149">**[Test de l’authentification unique](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ea078-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="ea078-150">Configuration de l’authentification unique Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea078-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="ea078-151">Dans cette section, vous allez activer l’authentification unique Microsoft Azure AD dans le portail Azure Classic et la configurer dans votre application Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="ea078-152">**Pour configurer l’authentification unique Microsoft Azure AD avec Bynder, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea078-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="ea078-153">Dans le portail Azure Classic, dans la page d’intégration d’applications **Bynder**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ea078-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][6] 
2. <span data-ttu-id="ea078-155">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Bynder**, sélectionnez **Authentification unique avec Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ea078-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="ea078-157">Dans la page de boîte de dialogue **Configurer les paramètres d’application**, si vous souhaitez configurer l’application en **mode lancé par le fournisseur d’identité**, procédez comme suit et cliquez sur **Suivant** :</span><span class="sxs-lookup"><span data-stu-id="ea078-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="ea078-159">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="ea078-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="ea078-160">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ea078-160">Click **Next**.</span></span>
4. <span data-ttu-id="ea078-161">Si vous souhaitez configurer l’application en **mode lancé par le fournisseur de service** dans la page de boîte de dialogue **Configurer les paramètres d’application**, cliquez sur **Affichez les paramètres avancés (facultatif)**, saisissez **l’URL de connexion** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ea078-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="ea078-163">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="ea078-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="ea078-164">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ea078-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="ea078-165">Dans ce didacticiel, la valeur de l’URL de connexion est un espace réservé.</span><span class="sxs-lookup"><span data-stu-id="ea078-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="ea078-166">Pour obtenir la valeur réelle pour votre environnement, contactez Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="ea078-167">Dans la page **Configurer l’authentification unique sur Bynder**, procédez comme suit et cliquez sur **Suivant** :</span><span class="sxs-lookup"><span data-stu-id="ea078-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="ea078-169">Cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ea078-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="ea078-170">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ea078-170">Click **Next**.</span></span>
6. <span data-ttu-id="ea078-171">Pour que l’authentification unique soit configurée pour votre application, contactez votre équipe du support technique Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="ea078-172">Joignez le fichier de métadonnées téléchargé et partagez-le avec l’équipe Bynder pour qu’elle configure l’authentification unique de son côté.</span><span class="sxs-lookup"><span data-stu-id="ea078-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="ea078-173">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ea078-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][10]
8. <span data-ttu-id="ea078-175">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="ea078-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ea078-177">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea078-177">Create an Azure AD test user</span></span>
<span data-ttu-id="ea078-178">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail classique.</span><span class="sxs-lookup"><span data-stu-id="ea078-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="ea078-180">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea078-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ea078-181">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea078-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="ea078-183">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="ea078-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ea078-184">Pour afficher la liste des utilisateurs, dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ea078-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="ea078-186">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="ea078-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="ea078-188">Sur la page de boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea078-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="ea078-190">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ea078-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="ea078-191">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea078-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="ea078-192">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ea078-192">Click **Next**.</span></span>
6. <span data-ttu-id="ea078-193">Sur la page de boîte de dialogue **Profil utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea078-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="ea078-195">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ea078-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="ea078-196">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ea078-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="ea078-197">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ea078-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="ea078-198">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="ea078-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="ea078-199">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ea078-199">Click **Next**.</span></span>
7. <span data-ttu-id="ea078-200">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="ea078-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="ea078-202">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea078-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="ea078-204">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ea078-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="ea078-205">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="ea078-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="ea078-206">Créer un utilisateur de test Bynder</span><span class="sxs-lookup"><span data-stu-id="ea078-206">Create a Bynder test user</span></span>
<span data-ttu-id="ea078-207">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="ea078-208">Bynder prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="ea078-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ea078-209">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="ea078-209">There is no action item for you in this section.</span></span> <span data-ttu-id="ea078-210">Un utilisateur est créé lors d’une tentative d’accès à Bynder s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="ea078-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="ea078-211">Si vous devez créer un utilisateur manuellement, contactez l’équipe du support technique Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ea078-212">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea078-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="ea078-213">L’objectif de cette section est de permettre à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Affecter des utilisateurs][200]

<span data-ttu-id="ea078-215">**Pour affecter Britta Simon à Bynder, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ea078-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="ea078-216">Pour ouvrir la vue des applications dans le portail Azure Classic, dans la vue d’annuaire, cliquez sur l’option **Applications** figurant dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="ea078-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Affecter des utilisateurs][201]
2. <span data-ttu-id="ea078-218">Dans la liste des applications, sélectionnez **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="ea078-218">In the applications list, select **Bynder**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="ea078-220">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ea078-220">In the menu on the top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203]
4. <span data-ttu-id="ea078-222">Dans la liste Utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ea078-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="ea078-223">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="ea078-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="ea078-225">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ea078-225">Test single sign-on</span></span>
<span data-ttu-id="ea078-226">L’objectif de cette section est de tester la configuration de l’authentification unique Microsoft Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ea078-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="ea078-227">Lorsque vous cliquez sur la vignette Bynder dans le volet d’accès, vous devez être connecté automatiquement à votre application Bynder.</span><span class="sxs-lookup"><span data-stu-id="ea078-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea078-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ea078-228">Additional resources</span></span>
* [<span data-ttu-id="ea078-229">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea078-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea078-230">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ea078-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
