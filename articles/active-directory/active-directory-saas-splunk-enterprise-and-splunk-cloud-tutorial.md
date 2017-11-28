---
title: "Didacticiel : intégration d’Azure Active Directory à Splunk Enterprise et Splunk Cloud | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Splunk Enterprise et Splunk Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="f5ba3-103">Didacticiel : Intégration d’Azure Active Directory avec Splunk Enterprise et Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="f5ba3-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="f5ba3-104">Dans ce didacticiel, vous allez apprendre à intégrer Splunk Enterprise et Splunk Cloud à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5ba3-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5ba3-105">L’intégration de Splunk Enterprise et Splunk Cloud à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5ba3-106">Dans Azure AD, vous pouvez contrôler qui a accès à Splunk Enterprise et Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="f5ba3-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="f5ba3-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Splunk Enterprise et Splunk Cloud (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5ba3-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5ba3-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f5ba3-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5ba3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5ba3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f5ba3-110">Prerequisites</span></span>

<span data-ttu-id="f5ba3-111">Pour configurer l’intégration d’Azure AD à Splunk Enterprise et Splunk Cloud, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="f5ba3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5ba3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5ba3-113">Un abonnement Splunk Enterprise ou Splunk Cloud avec l’authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="f5ba3-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="f5ba3-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="f5ba3-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5ba3-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f5ba3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5ba3-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f5ba3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f5ba3-118">Scenario description</span></span>
<span data-ttu-id="f5ba3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="f5ba3-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5ba3-121">Ajout de Splunk Enterprise et Splunk Cloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f5ba3-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="f5ba3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5ba3-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="f5ba3-123">Ajouter Splunk Enterprise et Splunk Cloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f5ba3-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="f5ba3-124">Pour configurer son intégration à Azure AD, vous devez ajouter Splunk Enterprise et Splunk Cloud à votre liste d’applications SaaS gérées, à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5ba3-125">**Pour ajouter Splunk Enterprise et Splunk Cloud à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f5ba3-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5ba3-126">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="f5ba3-128">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f5ba3-129">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="f5ba3-131">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="f5ba3-133">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="f5ba3-135">Dans la zone de recherche, tapez **Splunk Enterprise ou Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="f5ba3-137">Dans le volet des résultats, sélectionnez **Splunk Enterprise et Splunk Cloud**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f5ba3-139">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5ba3-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="f5ba3-140">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Splunk Enterprise et Splunk Cloud, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f5ba3-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5ba3-141">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Splunk Enterprise et Splunk Cloud équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="f5ba3-142">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et un utilisateur Splunk Enterprise et Splunk Cloud associé.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="f5ba3-143">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="f5ba3-144">Pour configurer et tester l’authentification unique Azure AD avec Splunk Enterprise et Splunk Cloud, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5ba3-145">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5ba3-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5ba3-147">**[Création d’un utilisateur de test Splunk Enterprise et Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** pour avoir un équivalent de Britta Simon dans Splunk Enterprise et Splunk Cloud, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f5ba3-148">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5ba3-149">**[Test de l’authentification unique](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f5ba3-150">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5ba3-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f5ba3-151">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure Classic et configurer l’authentification unique dans votre application Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="f5ba3-152">**Pour configurer l’authentification unique Azure AD avec Splunk Enterprise et Splunk Cloud, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f5ba3-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="f5ba3-153">Dans le portail Classic, sur la page d’intégration d’applications **Splunk Enterprise and Splunk Cloud**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurer l’authentification unique][6] 

2. <span data-ttu-id="f5ba3-155">Sur la page **Comment voulez-vous que les utilisateurs se connectent à Splunk Enterprise et Splunk Cloud ?**, sélectionnez **Authentification unique avec Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="f5ba3-157">Sur la page **Configurer les paramètres d’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="f5ba3-159">Dans la zone de texte **URL de connexion**, tapez l’URL utilisée par les utilisateurs pour se connecter à votre application Splunk Enterprise et Splunk Cloud au format suivant : `https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="f5ba3-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="f5ba3-160">Dans la zone de texte **Identificateur**, entrez de votre serveur Splunk.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="f5ba3-161">Dans la zone de texte **URL de réponse**, tapez l’URL au format suivant : `https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="f5ba3-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="f5ba3-162">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="f5ba3-163">Dans la page **Configurer l’authentification unique sur Splunk Enterprise et Splunk Cloud**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="f5ba3-165">Cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="f5ba3-166">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-166">Click **Next**.</span></span>

5. <span data-ttu-id="f5ba3-167">Pour obtenir la configuration de l’authentification unique pour votre application, contactez l’équipe de support Splunk Enterprise et Splunk Cloud et fournissez-lui les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="f5ba3-168">Les **métadonnées de fédération** téléchargées</span><span class="sxs-lookup"><span data-stu-id="f5ba3-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="f5ba3-169">Dans le portail classique, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Authentification unique Azure AD][10]

7. <span data-ttu-id="f5ba3-171">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f5ba3-173">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5ba3-173">Create an Azure AD test user</span></span>
<span data-ttu-id="f5ba3-174">Dans cette section, vous allez créer un utilisateur de test appelé Britta Simon dans le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="f5ba3-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f5ba3-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5ba3-177">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="f5ba3-179">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f5ba3-180">Pour afficher la liste des utilisateurs, dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5ba3-182">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="f5ba3-184">Sur la page de boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="f5ba3-186">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="f5ba3-187">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="f5ba3-188">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-188">Click **Next**.</span></span>

6.  <span data-ttu-id="f5ba3-189">Sur la page de boîte de dialogue **Profil utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="f5ba3-191">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="f5ba3-192">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="f5ba3-193">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="f5ba3-194">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="f5ba3-195">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-195">Click **Next**.</span></span>

7. <span data-ttu-id="f5ba3-196">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="f5ba3-198">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5ba3-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="f5ba3-200">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="f5ba3-201">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="f5ba3-202">Créer un utilisateur de test Splunk Enterprise et Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="f5ba3-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="f5ba3-203">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="f5ba3-204">Veuillez travailler avec l’équipe de support technique de Splunk Enterprise et Splunk Cloud pour ajouter des utilisateurs dans la plateforme Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f5ba3-205">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5ba3-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="f5ba3-206">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f5ba3-208">**Pour affecter Britta Simon à Splunk Enterprise et Splunk Cloud, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f5ba3-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="f5ba3-209">Pour ouvrir la vue des applications dans le portail Azure Classic, dans la vue d’annuaire, cliquez sur l’option **Applications** figurant dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f5ba3-211">Dans la liste des applications, sélectionnez **Splunk Enterprise et Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="f5ba3-213">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-213">In the menu on the top, click **Users**.</span></span>

    ![Affecter des utilisateurs][203]

4. <span data-ttu-id="f5ba3-215">Dans la liste Utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="f5ba3-216">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="f5ba3-218">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f5ba3-218">Test single sign-on</span></span>

<span data-ttu-id="f5ba3-219">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="f5ba3-220">Lorsque vous cliquez sur la vignette Splunk Enterprise et Splunk Cloud dans le volet d’accès, vous devez être connecté automatiquement à votre application Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="f5ba3-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f5ba3-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f5ba3-221">Additional resources</span></span>

* [<span data-ttu-id="f5ba3-222">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5ba3-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5ba3-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f5ba3-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
