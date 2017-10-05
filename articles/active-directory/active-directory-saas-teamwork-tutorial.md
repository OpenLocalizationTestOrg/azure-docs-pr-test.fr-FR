---
title: "Didacticiel : Intégration d’Azure Active Directory à Teamwork | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Teamwork."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: edd2f9446515531f1147a8abf99295b618b89b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="5bdc1-103">Didacticiel : Intégration d’Azure Active Directory à Teamwork</span><span class="sxs-lookup"><span data-stu-id="5bdc1-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="5bdc1-104">Dans ce didacticiel, vous allez apprendre à intégrer Teamwork à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bdc1-104">In this tutorial, you learn how to integrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bdc1-105">L’intégration de Teamwork à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5bdc1-105">Integrating Teamwork with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5bdc1-106">Dans Azure AD, vous pouvez contrôler qui a accès à Teamwork.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-106">You can control in Azure AD who has access to Teamwork</span></span>
- <span data-ttu-id="5bdc1-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Teamwork (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-107">You can enable your users to automatically get signed-on to Teamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bdc1-108">Vous pouvez gérer vos comptes de manière centralisée dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="5bdc1-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bdc1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bdc1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5bdc1-110">Prerequisites</span></span>

<span data-ttu-id="5bdc1-111">Pour configurer l’intégration d’Azure AD à Teamwork, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5bdc1-111">To configure Azure AD integration with Teamwork, you need the following items:</span></span>

- <span data-ttu-id="5bdc1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bdc1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bdc1-113">Un abonnement Teamwork pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5bdc1-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="5bdc1-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="5bdc1-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5bdc1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bdc1-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5bdc1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bdc1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="5bdc1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5bdc1-118">Scenario description</span></span>
<span data-ttu-id="5bdc1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bdc1-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5bdc1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bdc1-121">Ajout de Teamwork à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5bdc1-121">Adding Teamwork from the gallery</span></span>
2. <span data-ttu-id="5bdc1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bdc1-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-the-gallery"></a><span data-ttu-id="5bdc1-123">Ajout de Teamwork à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5bdc1-123">Adding Teamwork from the gallery</span></span>
<span data-ttu-id="5bdc1-124">Pour configurer l’intégration de Teamwork à Azure AD, vous devez ajouter Teamwork à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-124">To configure the integration of Teamwork into Azure AD, you need to add Teamwork from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5bdc1-125">**Pour ajouter Teamwork à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5bdc1-125">**To add Teamwork from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5bdc1-126">Dans le **[Portail de gestion Azure](https://portal.azure.com)**, dans le panneau de navigation gauche, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5bdc1-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5bdc1-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5bdc1-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5bdc1-133">Dans la zone de recherche, tapez **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-133">In the search box, type **Teamwork**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="5bdc1-135">Dans le panneau de résultats, sélectionnez **Teamwork**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-135">In the results panel, select **Teamwork**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bdc1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bdc1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bdc1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Teamwork au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5bdc1-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5bdc1-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Teamwork équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork is to a user in Azure AD.</span></span> <span data-ttu-id="5bdc1-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Teamwork associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-140">In other words, a link relationship between an Azure AD user and the related user in Teamwork needs to be established.</span></span>

<span data-ttu-id="5bdc1-141">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** (Nom d’utilisateur) dans Teamwork.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamwork.</span></span>

<span data-ttu-id="5bdc1-142">Pour configurer et tester l’authentification unique Azure AD avec Teamwork, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5bdc1-142">To configure and test Azure AD single sign-on with Teamwork, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5bdc1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5bdc1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bdc1-145">**[Création d’un utilisateur de test Teamwork](#creating-a-teamwork-test-user)** pour avoir un équivalent de Britta Simon dans Teamwork lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - to have a counterpart of Britta Simon in Teamwork that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5bdc1-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bdc1-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bdc1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bdc1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bdc1-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le Portail de gestion Azure et configurer l’authentification unique dans votre application Teamwork.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="5bdc1-150">**Pour configurer l’authentification unique Azure AD avec Teamwork, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5bdc1-150">**To configure Azure AD single sign-on with Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="5bdc1-151">Dans le Portail de gestion Azure, sur la page d’intégration de l’application **Teamwork**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-151">In the Azure Management portal, on the **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5bdc1-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="5bdc1-155">Dans la section **Domaine et URL Teamwork**, renseignez la zone de texte **URL de connexion** avec une URL présentant le format suivant : `https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="5bdc1-155">On the **Teamwork Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="5bdc1-157">Notez qu’il ne s’agit pas de la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-157">Please note that this is not the real value.</span></span> <span data-ttu-id="5bdc1-158">Vous devez mettre à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="5bdc1-159">Pour obtenir cette valeur, contactez [l’équipe de support technique de Teamwork](mailto:support@teamwork.com).</span><span class="sxs-lookup"><span data-stu-id="5bdc1-159">Contact [Teamwork support team](mailto:support@teamwork.com) to get this value.</span></span> 

4. <span data-ttu-id="5bdc1-160">Dans la section **Certificat de signature SAML**, cliquez sur **Créer un certificat**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="5bdc1-162">Dans la boîte de dialogue **Créer un certificat**, cliquez sur l’icône de calendrier et sélectionnez une **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="5bdc1-163">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-163">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="5bdc1-165">Dans la section **Certificat de signature SAML**, sélectionnez **Activer le nouveau certificat** et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="5bdc1-167">Dans la fenêtre contextuelle **Certificat de substitution**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5bdc1-169">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="5bdc1-171">Pour obtenir la configuration de l’authentification unique pour votre application, contactez [l’équipe de support technique de Teamwork](mailto:support@teamwork.com) en lui fournissant les **métadonnées** téléchargées.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-171">To get SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with the downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bdc1-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bdc1-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bdc1-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-173">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5bdc1-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5bdc1-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5bdc1-176">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-176">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bdc1-178">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-178">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bdc1-180">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-180">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bdc1-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5bdc1-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bdc1-184">a.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-184">a.</span></span> <span data-ttu-id="5bdc1-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bdc1-186">b.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-186">b.</span></span> <span data-ttu-id="5bdc1-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bdc1-188">c.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-188">c.</span></span> <span data-ttu-id="5bdc1-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5bdc1-190">d.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-190">d.</span></span> <span data-ttu-id="5bdc1-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="5bdc1-192">Création d’un utilisateur de test Teamwork</span><span class="sxs-lookup"><span data-stu-id="5bdc1-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="5bdc1-193">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Teamwork.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="5bdc1-194">Collaborez avec [l’équipe de support technique de Teamwork](mailto:support@teamwork.com) pour ajouter les utilisateurs dans la plateforme Teamwork.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-194">Please work with [Teamwork support team](mailto:support@teamwork.com) to add the users in the Teamwork platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5bdc1-195">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bdc1-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5bdc1-196">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Teamwork.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-196">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamwork.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5bdc1-198">**Pour affecter Britta Simon à Teamwork, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5bdc1-198">**To assign Britta Simon to Teamwork, perform the following steps:**</span></span>

1. <span data-ttu-id="5bdc1-199">Dans le Portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, allez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-199">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5bdc1-201">Dans la liste des applications, sélectionnez **Teamwork**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-201">In the applications list, select **Teamwork**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="5bdc1-203">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5bdc1-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-205">Click **Add** button.</span></span> <span data-ttu-id="5bdc1-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5bdc1-208">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5bdc1-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bdc1-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="5bdc1-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5bdc1-211">Testing single sign-on</span></span>

<span data-ttu-id="5bdc1-212">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5bdc1-213">Lorsque vous cliquez sur la vignette Teamwork dans le volet d’accès, vous devez être connecté automatiquement à votre application Teamwork.</span><span class="sxs-lookup"><span data-stu-id="5bdc1-213">When you click the Teamwork tile in the Access Panel, you should get automatically signed-on to your Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5bdc1-214">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5bdc1-214">Additional resources</span></span>

* [<span data-ttu-id="5bdc1-215">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bdc1-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bdc1-216">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5bdc1-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png