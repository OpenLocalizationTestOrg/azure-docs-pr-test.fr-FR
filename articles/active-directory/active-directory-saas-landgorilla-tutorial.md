---
title: "Didacticiel : Intégration d’Azure Active Directory à Land Gorilla Client | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Land Gorilla Client."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 744c420aa0298c59c44e645b95a716ad876752de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="5398e-103">Didacticiel : Intégration d’Azure Active Directory à Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="5398e-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="5398e-104">Dans ce didacticiel, vous allez apprendre à intégrer Land Gorilla Client à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5398e-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5398e-105">L’intégration d’Azure AD dans Land Gorilla Client offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5398e-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5398e-106">Dans Azure AD, vous pouvez contrôler qui a accès à Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="5398e-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="5398e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Land Gorilla Client (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="5398e-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5398e-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="5398e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="5398e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5398e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5398e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5398e-110">Prerequisites</span></span>

<span data-ttu-id="5398e-111">Pour configurer l’intégration d’Azure AD dans Land Gorilla Client, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5398e-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="5398e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5398e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5398e-113">Un abonnement Land Gorilla Client pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5398e-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="5398e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5398e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="5398e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5398e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5398e-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5398e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5398e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5398e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="5398e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5398e-118">Scenario description</span></span>
<span data-ttu-id="5398e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5398e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5398e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5398e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5398e-121">Ajout de Land Gorilla Client à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5398e-121">Adding Land Gorilla Client from the gallery</span></span>
2. <span data-ttu-id="5398e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5398e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="5398e-123">Ajout de Land Gorilla Client à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5398e-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="5398e-124">Pour configurer l’intégration d’un client Land Gorilla à Azure AD, vous devez ajouter le client Land Gorilla à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5398e-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5398e-125">**Pour ajouter Land Gorilla Clientt à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5398e-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5398e-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5398e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5398e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5398e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5398e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5398e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5398e-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5398e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5398e-133">Dans la zone Rechercher, entrez **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="5398e-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="5398e-135">Dans le volet des résultats, sélectionnez **Land Gorilla Client**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5398e-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5398e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5398e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5398e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Land Gorilla Client avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5398e-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5398e-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Land Gorilla Client équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5398e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="5398e-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Land Gorilla Client associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="5398e-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="5398e-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="5398e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="5398e-142">Pour configurer et tester l’authentification unique Azure AD avec Land Gorilla Client, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5398e-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5398e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5398e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5398e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD sur un groupe limité.</span><span class="sxs-lookup"><span data-stu-id="5398e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="5398e-145">**[Création d’un utilisateur de test Land Gorilla](#creating-a-land-gorilla-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5398e-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="5398e-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d'utiliser l'authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5398e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5398e-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5398e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5398e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5398e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5398e-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="5398e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="5398e-150">**Pour configurer l’authentification unique Azure AD avec Land Gorilla Client, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5398e-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="5398e-151">Dans le portail de gestion Azure, sur la page d’intégration de l’application **Land Gorilla Client**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5398e-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5398e-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5398e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="5398e-155">Dans la section **Domaine et URL Land Gorilla Client**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5398e-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="5398e-157">a.</span><span class="sxs-lookup"><span data-stu-id="5398e-157">a.</span></span> <span data-ttu-id="5398e-158">Dans la zone de texte **Identificateur**, tapez la valeur en utilisant un des formats suivants :</span><span class="sxs-lookup"><span data-stu-id="5398e-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="5398e-159">b.</span><span class="sxs-lookup"><span data-stu-id="5398e-159">b.</span></span> <span data-ttu-id="5398e-160">Dans la zone de texte **URL de réponse** , tapez une URL en respectant l’un des formats suivants :</span><span class="sxs-lookup"><span data-stu-id="5398e-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="5398e-161">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5398e-161">Please note that these are not the real values.</span></span> <span data-ttu-id="5398e-162">Vous devez mettre à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="5398e-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="5398e-163">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="5398e-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="5398e-164">Pour obtenir ces valeurs, contactez [l’équipe de support technique Land Gorilla Client](https://www.landgorilla.com/support/).</span><span class="sxs-lookup"><span data-stu-id="5398e-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="5398e-165">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5398e-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="5398e-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5398e-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="5398e-169">Pour obtenir la configuration SSO complète pour votre application côté Land Gorilla, contactez [l’équipe de support technique Land Gorilla](https://www.landgorilla.com/support/) et fournissez-lui le fichier **« Metadata XML »** téléchargé.</span><span class="sxs-lookup"><span data-stu-id="5398e-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5398e-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5398e-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="5398e-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="5398e-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5398e-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5398e-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5398e-174">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5398e-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5398e-176">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5398e-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5398e-178">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="5398e-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5398e-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5398e-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5398e-182">a.</span><span class="sxs-lookup"><span data-stu-id="5398e-182">a.</span></span> <span data-ttu-id="5398e-183">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5398e-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5398e-184">b.</span><span class="sxs-lookup"><span data-stu-id="5398e-184">b.</span></span> <span data-ttu-id="5398e-185">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5398e-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5398e-186">c.</span><span class="sxs-lookup"><span data-stu-id="5398e-186">c.</span></span> <span data-ttu-id="5398e-187">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5398e-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5398e-188">d.</span><span class="sxs-lookup"><span data-stu-id="5398e-188">d.</span></span> <span data-ttu-id="5398e-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5398e-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="5398e-190">Création d’un utilisateur de test Land Gorilla</span><span class="sxs-lookup"><span data-stu-id="5398e-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="5398e-191">Collaborez avec [l’équipe du support technique Land Gorilla](https://www.landgorilla.com/support/) pour ajouter des utilisateurs dans la plateforme Land Gorilla.</span><span class="sxs-lookup"><span data-stu-id="5398e-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5398e-192">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5398e-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5398e-193">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="5398e-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5398e-195">**Pour affecter Britta Simon à Land Gorilla Client, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5398e-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="5398e-196">Dans le portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5398e-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5398e-198">Dans la liste des applications, sélectionnez **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="5398e-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="5398e-200">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5398e-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5398e-202">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5398e-202">Click **Add** button.</span></span> <span data-ttu-id="5398e-203">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5398e-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5398e-205">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5398e-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5398e-206">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5398e-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5398e-207">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5398e-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="5398e-208">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5398e-208">Testing single sign-on</span></span>

<span data-ttu-id="5398e-209">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5398e-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5398e-210">Lorsque vous cliquez sur la mosaïque Land Gorilla Client dans le volet d’accès, vous devez être connecté automatiquement à votre application Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="5398e-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5398e-211">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5398e-211">Additional resources</span></span>

* [<span data-ttu-id="5398e-212">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5398e-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5398e-213">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5398e-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
