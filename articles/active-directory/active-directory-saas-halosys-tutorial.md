---
title: "Didacticiel : intégration d’Azure Active Directory à Halosys | Microsoft Docs"
description: "Apprenez à utiliser Halosys avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="44664-103">Didacticiel : intégration d’Azure Active Directory à Halosys</span><span class="sxs-lookup"><span data-stu-id="44664-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="44664-104">Dans ce didacticiel, vous allez apprendre à intégrer Halosys à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44664-104">In this tutorial, you learn how to integrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44664-105">L’intégration de Halosys dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="44664-105">Integrating Halosys with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44664-106">Dans Azure AD, vous pouvez contrôler qui a accès à Halosys</span><span class="sxs-lookup"><span data-stu-id="44664-106">You can control in Azure AD who has access to Halosys</span></span>
- <span data-ttu-id="44664-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Halosys (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="44664-107">You can enable your users to automatically get signed-on to Halosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44664-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="44664-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="44664-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44664-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44664-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="44664-110">Prerequisites</span></span>

<span data-ttu-id="44664-111">Pour configurer l’intégration d’Azure AD avec Halosys, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="44664-111">To configure Azure AD integration with Halosys, you need the following items:</span></span>

- <span data-ttu-id="44664-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="44664-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44664-113">Un abonnement Halosys pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="44664-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="44664-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="44664-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="44664-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="44664-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44664-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="44664-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="44664-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44664-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="44664-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="44664-118">Scenario description</span></span>
<span data-ttu-id="44664-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="44664-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="44664-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="44664-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44664-121">Ajout de Halosys à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="44664-121">Adding Halosys from the gallery</span></span>
2. <span data-ttu-id="44664-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44664-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-the-gallery"></a><span data-ttu-id="44664-123">Ajout de Halosys à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="44664-123">Adding Halosys from the gallery</span></span>
<span data-ttu-id="44664-124">Pour configurer l’intégration de Halosys à Azure AD, vous devez ajouter Halosys à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="44664-124">To configure the integration of Halosys into Azure AD, you need to add Halosys from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44664-125">**Pour ajouter Halosys à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44664-125">**To add Halosys from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44664-126">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44664-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="44664-128">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="44664-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="44664-129">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="44664-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Applications][2]

4. <span data-ttu-id="44664-131">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="44664-131">Click **Add** at the bottom of the page.</span></span>

    ![Applications][3]

5. <span data-ttu-id="44664-133">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="44664-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Applications][4]

6. <span data-ttu-id="44664-135">Dans la zone de recherche, tapez **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="44664-135">In the search box, type **Halosys**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="44664-137">Dans le volet des résultats, sélectionnez **Halosys**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="44664-137">In the results pane, select **Halosys**, and then click **Complete** to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44664-139">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44664-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44664-140">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Halosys avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="44664-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="44664-141">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Halosys équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44664-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Halosys is to a user in Azure AD.</span></span> <span data-ttu-id="44664-142">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Halosys associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="44664-142">In other words, a link relationship between an Azure AD user and the related user in Halosys needs to be established.</span></span>

<span data-ttu-id="44664-143">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Halosys.</span><span class="sxs-lookup"><span data-stu-id="44664-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Halosys.</span></span>

<span data-ttu-id="44664-144">Pour configurer et tester l’authentification unique Azure AD avec Halosys, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="44664-144">To configure and test Azure AD single sign-on with Halosys, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44664-145">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="44664-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44664-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44664-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44664-147">**[Création d’un utilisateur de test Halosys](#creating-a-halosys-test-user)** : pour avoir un équivalent de Britta Simon dans Halosys lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="44664-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - to have a counterpart of Britta Simon in Halosys that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="44664-148">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44664-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44664-149">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="44664-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44664-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44664-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44664-151">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Classic et configurer l’authentification unique dans votre application Halosys.</span><span class="sxs-lookup"><span data-stu-id="44664-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="44664-152">**Pour configurer l’authentification unique Azure AD avec Halosys, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44664-152">**To configure Azure AD single sign-on with Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="44664-153">Dans le portail Classic, dans la page d’intégration d’application **Halosys**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="44664-153">In the classic portal, on the **Halosys** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurer l’authentification unique][6] 

2. <span data-ttu-id="44664-155">Sur la page **Comment voulez-vous que les utilisateurs se connectent à Halosys**, sélectionnez **Authentification unique Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="44664-155">On the **How would you like users to sign on to Halosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="44664-157">Sur la page **Configurer les paramètres d’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="44664-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="44664-159">a.</span><span class="sxs-lookup"><span data-stu-id="44664-159">a.</span></span> <span data-ttu-id="44664-160">Dans la zone de texte **URL de connexion**, tapez l’URL utilisée par les utilisateurs pour se connecter à votre application Halosys au format suivant : `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="44664-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Halosys application using the following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="44664-161">Dans la zone de texte **URL d’identificateur**, tapez l’URL au format suivant : `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="44664-161">b.In the **Identifier URL** textbox, type the URL in the following pattern: `https://<company-name>.Halosys.com`.</span></span>   
         
4. <span data-ttu-id="44664-162">Sur la page **Configurer l’authentification unique sur Halosys**, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="44664-162">On the **Configure single sign-on at Halosys** page, click **Download metadata**, and then save the file on your computer:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="44664-164">Pour obtenir la configuration de l’authentification unique pour votre application, contactez l’équipe de support Halosys et fournissez-lui les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="44664-164">To get SSO configured for your application, contact Halosys support team and provide them with the following:</span></span>

    <span data-ttu-id="44664-165">• le fichier de **métadonnées téléchargé**</span><span class="sxs-lookup"><span data-stu-id="44664-165">• The downloaded **metadata file**</span></span>
    
    <span data-ttu-id="44664-166">• **L’URL d’authentification unique SAML**</span><span class="sxs-lookup"><span data-stu-id="44664-166">• The **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="44664-167">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="44664-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Authentification unique Azure AD][10]

7. <span data-ttu-id="44664-169">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="44664-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Authentification unique Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44664-171">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="44664-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="44664-172">Dans cette section, vous allez créer un utilisateur de test appelé Britta Simon dans le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="44664-172">In this section, you create a test user in the classic portal called Britta Simon.</span></span>


![Créer un utilisateur Azure AD][20]

<span data-ttu-id="44664-174">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44664-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44664-175">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44664-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="44664-177">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="44664-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="44664-178">Pour afficher la liste des utilisateurs, dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="44664-178">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44664-180">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="44664-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="44664-182">Sur le **faites-nous part de cet utilisateur** boîte de dialogue de page, procédez comme suit : ![création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="44664-182">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="44664-183">a.</span><span class="sxs-lookup"><span data-stu-id="44664-183">a.</span></span> <span data-ttu-id="44664-184">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="44664-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="44664-185">b.</span><span class="sxs-lookup"><span data-stu-id="44664-185">b.</span></span> <span data-ttu-id="44664-186">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44664-186">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44664-187">c.</span><span class="sxs-lookup"><span data-stu-id="44664-187">c.</span></span> <span data-ttu-id="44664-188">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="44664-188">Click **Next**.</span></span>

6.  <span data-ttu-id="44664-189">Sur la page de boîte de dialogue **Profil utilisateur**, procédez comme suit : ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="44664-189">On the **User Profile** dialog page, perform the following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="44664-190">a.</span><span class="sxs-lookup"><span data-stu-id="44664-190">a.</span></span> <span data-ttu-id="44664-191">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="44664-191">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="44664-192">b.</span><span class="sxs-lookup"><span data-stu-id="44664-192">b.</span></span> <span data-ttu-id="44664-193">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="44664-193">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="44664-194">c.</span><span class="sxs-lookup"><span data-stu-id="44664-194">c.</span></span> <span data-ttu-id="44664-195">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="44664-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="44664-196">d.</span><span class="sxs-lookup"><span data-stu-id="44664-196">d.</span></span> <span data-ttu-id="44664-197">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="44664-197">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="44664-198">e.</span><span class="sxs-lookup"><span data-stu-id="44664-198">e.</span></span> <span data-ttu-id="44664-199">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="44664-199">Click **Next**.</span></span>

7. <span data-ttu-id="44664-200">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="44664-200">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="44664-202">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="44664-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="44664-204">a.</span><span class="sxs-lookup"><span data-stu-id="44664-204">a.</span></span> <span data-ttu-id="44664-205">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="44664-205">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="44664-206">b.</span><span class="sxs-lookup"><span data-stu-id="44664-206">b.</span></span> <span data-ttu-id="44664-207">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="44664-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="44664-208">Création d’un utilisateur de test Halosys</span><span class="sxs-lookup"><span data-stu-id="44664-208">Creating a Halosys test user</span></span>

<span data-ttu-id="44664-209">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Halosys.</span><span class="sxs-lookup"><span data-stu-id="44664-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="44664-210">Collaborez avec l’équipe du support technique Halosys pour ajouter des utilisateurs dans la plateforme Halosys.</span><span class="sxs-lookup"><span data-stu-id="44664-210">Please work with Halosys support team to add the users in the Halosys platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44664-211">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="44664-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44664-212">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Halosys.</span><span class="sxs-lookup"><span data-stu-id="44664-212">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Halosys.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="44664-214">**Pour affecter Britta Simon à Halosys, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44664-214">**To assign Britta Simon to Halosys, perform the following steps:**</span></span>

1. <span data-ttu-id="44664-215">Pour ouvrir la vue des applications dans le portail Azure Classic, dans la vue d’annuaire, cliquez sur l’option **Applications** figurant dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="44664-215">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="44664-217">Dans la liste des applications, sélectionnez **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="44664-217">In the applications list, select **Halosys**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="44664-219">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="44664-219">In the menu on the top, click **Users**.</span></span>

    ![Affecter des utilisateurs][203]

4. <span data-ttu-id="44664-221">Dans la liste Utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="44664-221">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="44664-222">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="44664-222">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Affecter des utilisateurs][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="44664-224">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="44664-224">Testing single sign-on</span></span>

<span data-ttu-id="44664-225">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="44664-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44664-226">Lorsque vous cliquez sur la vignette Halosys dans le volet d’accès, vous devez être connecté automatiquement à votre application Halosys.</span><span class="sxs-lookup"><span data-stu-id="44664-226">When you click the Halosys tile in the Access Panel, you should get automatically signed-on to your Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="44664-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="44664-227">Additional resources</span></span>

* [<span data-ttu-id="44664-228">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44664-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44664-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="44664-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
