---
title: "Didacticiel : Intégration d’Azure Active Directory avec Wizergos Productivity Software | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Wizergos Productivity Software."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 73b3bc05aeb337c12acb7e47c0dbebe6d0196530
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="75bb2-103">Didacticiel : Intégration d’Azure Active Directory avec Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="75bb2-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="75bb2-104">L’objectif de ce didacticiel est de vous montrer comment intégrer Wizergos Productivity Software dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="75bb2-104">The objective of this tutorial is to show you how to integrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75bb2-105">L’intégration de Wizergos Productivity Software dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="75bb2-105">Integrating Wizergos Productivity Software with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="75bb2-106">Dans Azure AD, vous pouvez contrôler qui a accès à Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="75bb2-106">You can control in Azure AD who has access to Wizergos Productivity Software</span></span>
* <span data-ttu-id="75bb2-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Wizergos Productivity Software par le biais de l’authentification unique (SSO) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75bb2-107">You can enable your users to automatically get signed-on to Wizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="75bb2-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="75bb2-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="75bb2-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="75bb2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75bb2-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="75bb2-110">Prerequisites</span></span>
<span data-ttu-id="75bb2-111">Pour configurer l’intégration d’Azure AD avec Wizergos Productivity Software, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="75bb2-111">To configure Azure AD integration with Wizergos Productivity Software, you need the following items:</span></span>

* <span data-ttu-id="75bb2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="75bb2-112">An Azure AD subscription</span></span>
* <span data-ttu-id="75bb2-113">Un abonnement Wizergos Productivity Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="75bb2-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="75bb2-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="75bb2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="75bb2-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="75bb2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="75bb2-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="75bb2-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="75bb2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75bb2-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75bb2-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="75bb2-118">Scenario description</span></span>
<span data-ttu-id="75bb2-119">Ce didacticiel vise à vous permettre de tester l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="75bb2-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="75bb2-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="75bb2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75bb2-121">Ajout de Wizergos Productivity Software depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="75bb2-121">Adding Wizergos Productivity Software from the gallery</span></span>
2. <span data-ttu-id="75bb2-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="75bb2-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-the-gallery"></a><span data-ttu-id="75bb2-123">Ajout de Wizergos Productivity Software depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="75bb2-123">Adding Wizergos Productivity Software from the gallery</span></span>
<span data-ttu-id="75bb2-124">Pour configurer l’intégration de Wizergos Productivity Software avec Azure AD, vous devez ajouter Wizergos Productivity Software, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="75bb2-124">To configure the integration of Wizergos Productivity Software into Azure AD, you need to add Wizergos Productivity Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75bb2-125">**Pour ajouter Wizergos Productivity Software depuis la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bb2-125">**To add Wizergos Productivity Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="75bb2-126">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="75bb2-128">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="75bb2-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="75bb2-129">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="75bb2-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="75bb2-131">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="75bb2-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="75bb2-133">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="75bb2-135">Dans la zone de recherche, tapez **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-135">In the search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="75bb2-137">Dans le volet des résultats, sélectionnez **Wizergos Productivity Software**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="75bb2-137">In the results panel, select **Wizergos Productivity Software**, and then click **Complete** to add the application.</span></span>
   
    ![Sélection de l’application dans la galerie](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="75bb2-139">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="75bb2-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="75bb2-140">Cette section vous indique comment configurer et tester l’authentification unique Azure AD avec Wizergos Productivity Software au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="75bb2-140">The objective of this section is to show you how to configure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75bb2-141">Pour que l’authentification unique fonctionne, Azure AD a besoin de savoir qui est l’utilisateur Wizergos Productivity Software équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75bb2-141">For SSO to work, Azure AD needs to know what the counterpart user in Wizergos Productivity Software to an user in Azure AD is.</span></span> <span data-ttu-id="75bb2-142">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Wizergos Productivity Software associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="75bb2-142">In other words, a link relationship between an Azure AD user and the related user in Wizergos Productivity Software needs to be established.</span></span>

<span data-ttu-id="75bb2-143">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="75bb2-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="75bb2-144">Pour configurer et tester l’authentification unique Azure AD avec Wizergos Productivity Software, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="75bb2-144">To configure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="75bb2-145">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="75bb2-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="75bb2-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="75bb2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75bb2-147">**[Création d’un utilisateur de test Wizergos Productivity Software](#creating-a-wizergos-productivity-software-test-user)** pour avoir un équivalent de Britta Simon dans Wizergos Productivity Software qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="75bb2-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - to have a counterpart of Britta Simon in Wizergos Productivity Software that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="75bb2-148">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75bb2-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75bb2-149">**[Test de l’authentification unique](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="75bb2-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="75bb2-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="75bb2-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="75bb2-151">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure Classic et configurer l’authentification unique dans votre application Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="75bb2-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="75bb2-152">**Pour configurer l’authentification unique Azure AD avec Wizergos Productivity Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bb2-152">**To configure Azure AD single sign-on with Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="75bb2-153">Dans le portail Classic, dans la page d’intégration d’applications **Wizergos Productivity Software**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-153">In the classic portal, on the **Wizergos Productivity Software** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][6] 
2. <span data-ttu-id="75bb2-155">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Wizergos Productivity Software**, sélectionnez **Authentification unique Azure AD**, puis cliquez sur **Suivant** :</span><span class="sxs-lookup"><span data-stu-id="75bb2-155">On the **How would you like users to sign on to Wizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="75bb2-157">Dans la page **Configurer les paramètres de l’application** , cliquez sur **Suivant** :</span><span class="sxs-lookup"><span data-stu-id="75bb2-157">On the **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="75bb2-159">Dans la page **Configurer l’authentification unique sur Wizergos Productivity Software**, cliquez sur **Télécharger le certificat**, puis enregistrez le fichier sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="75bb2-159">On the **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save the file on your computer:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="75bb2-161">Dans une autre fenêtre de navigateur web, connectez-vous à votre client Wizergos Productivity Software en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="75bb2-161">In a different web browser window, sign-on to your Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="75bb2-162">Dans le menu de type hamburger, sélectionnez **Admin**(Administrateur).</span><span class="sxs-lookup"><span data-stu-id="75bb2-162">From the hamburger menu, select **Admin**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="75bb2-164">Dans le menu de gauche de la page Admin (Administrateur), sélectionnez **AUTHENTICATION** (AUTHENTIFICATION), puis cliquez sur **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="75bb2-166">Dans la section **AUTHENTICATION** (AUTHENTIFICATION), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="75bb2-166">Perform the following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="75bb2-168">Cliquez sur le bouton **CHARGER** (UPLOAD) pour charger le certificat obtenu auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75bb2-168">Click **UPLOAD** button to upload the downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="75bb2-169">Dans la zone de texte **Issuer URL** (URL de l’émetteur), copiez la valeur de **l’URL de l’émetteur** indiquée dans l’Assistant Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75bb2-169">In the **Issuer URL** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="75bb2-170">Dans la zone de texte **Single Sign-On URL** (URL d’authentification unique), copiez la valeur de **l’URL du service d’authentification unique** indiquée dans l’Assistant Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75bb2-170">In the **Single Sign-On URL** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="75bb2-171">Dans la zone de texte **Single Sign-Out URL** (URL de déconnexion unique), copiez la valeur de **l’URL du service de déconnexion unique** indiquée dans l’Assistant Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75bb2-171">In the **Single Sign-Out URL** textbox put the value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="75bb2-172">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="75bb2-172">Click **Save** button.</span></span>
9. <span data-ttu-id="75bb2-173">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][10]
10. <span data-ttu-id="75bb2-175">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="75bb2-177">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="75bb2-177">Create an Azure AD test user</span></span>
<span data-ttu-id="75bb2-178">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail classique.</span><span class="sxs-lookup"><span data-stu-id="75bb2-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="75bb2-180">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bb2-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="75bb2-181">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="75bb2-183">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="75bb2-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="75bb2-184">Pour afficher la liste des utilisateurs, dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="75bb2-186">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="75bb2-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="75bb2-188">Sur la page de boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="75bb2-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="75bb2-190">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="75bb2-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="75bb2-191">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="75bb2-192">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-192">Click **Next**.</span></span>
6. <span data-ttu-id="75bb2-193">Sur la page de boîte de dialogue **Profil utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="75bb2-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="75bb2-195">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="75bb2-196">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="75bb2-197">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="75bb2-198">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="75bb2-199">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-199">Click **Next**.</span></span>
7. <span data-ttu-id="75bb2-200">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="75bb2-202">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="75bb2-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="75bb2-204">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="75bb2-205">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="75bb2-206">Créer un utilisateur de test Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="75bb2-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="75bb2-207">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="75bb2-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="75bb2-208">Collaborez avec l’équipe du support technique Wizergos Productivity Software via l’adresse [support@wizergos.com](emailTo:support@wizergos.com) pour ajouter les utilisateurs à la plateforme Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="75bb2-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) to add the users in the Wizergos Productivity Software platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="75bb2-209">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="75bb2-209">Assign the Azure AD test user</span></span>
<span data-ttu-id="75bb2-210">L’objectif de cette section est de permettre à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="75bb2-210">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Wizergos Productivity Software.</span></span>

  ![Affecter des utilisateurs][200]

<span data-ttu-id="75bb2-212">**Pour affecter Britta Simon à Wizergos Productivity Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bb2-212">**To assign Britta Simon to Wizergos Productivity Software, perform the following steps:**</span></span>

1. <span data-ttu-id="75bb2-213">Pour ouvrir la vue des applications dans le portail Azure Classic, dans la vue de répertoire, cliquez sur l’option **Applications** figurant dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="75bb2-213">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Affecter des utilisateurs][201]
2. <span data-ttu-id="75bb2-215">Dans la liste des applications, sélectionnez **Wizergos Productivity Software**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-215">In the applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="75bb2-217">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-217">In the menu on the top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203]
4. <span data-ttu-id="75bb2-219">Dans la liste Utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-219">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="75bb2-220">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="75bb2-220">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="75bb2-222">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="75bb2-222">Test single sign-on</span></span>
<span data-ttu-id="75bb2-223">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="75bb2-223">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="75bb2-224">Lorsque vous cliquez sur la vignette Wizergos Productivity Software dans le volet d’accès, vous devez être connecté automatiquement à votre application Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="75bb2-224">When you click the Wizergos Productivity Software tile in the Access Panel, you should get automatically signed-on to your Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75bb2-225">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="75bb2-225">Additional resources</span></span>
* [<span data-ttu-id="75bb2-226">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75bb2-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75bb2-227">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="75bb2-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
