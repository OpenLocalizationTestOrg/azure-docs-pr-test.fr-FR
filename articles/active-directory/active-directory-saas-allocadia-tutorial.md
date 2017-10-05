---
title: "Didacticiel : Intégration d’Azure Active Directory à Allocadia | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 8e97c365383ecdb72cc1cd449b522b75875fc1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="c68b7-103">Didacticiel : Intégration d’Azure Active Directory à Allocadia</span><span class="sxs-lookup"><span data-stu-id="c68b7-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="c68b7-104">Dans ce didacticiel, vous allez apprendre à intégrer Allocadia à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c68b7-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c68b7-105">L’intégration d’Allocadia dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c68b7-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c68b7-106">Dans Azure AD, vous pouvez contrôler qui a accès à Allocadia</span><span class="sxs-lookup"><span data-stu-id="c68b7-106">You can control in Azure AD who has access to Allocadia</span></span>
- <span data-ttu-id="c68b7-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Allocadia (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="c68b7-107">You can enable your users to automatically get signed-on to Allocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c68b7-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c68b7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c68b7-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c68b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c68b7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c68b7-110">Prerequisites</span></span>

<span data-ttu-id="c68b7-111">Pour configurer l'intégration d'Azure AD avec Allocadia, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c68b7-111">To configure Azure AD integration with Allocadia, you need the following items:</span></span>

- <span data-ttu-id="c68b7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c68b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c68b7-113">Un abonnement Allocadia pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c68b7-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c68b7-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c68b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c68b7-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c68b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c68b7-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c68b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c68b7-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c68b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c68b7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c68b7-118">Scenario description</span></span>
<span data-ttu-id="c68b7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c68b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c68b7-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c68b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c68b7-121">Ajout d’Allocadia à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c68b7-121">Adding Allocadia from the gallery</span></span>
2. <span data-ttu-id="c68b7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c68b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-the-gallery"></a><span data-ttu-id="c68b7-123">Ajout d’Allocadia à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c68b7-123">Adding Allocadia from the gallery</span></span>
<span data-ttu-id="c68b7-124">Pour configurer l’intégration d’Allocadia à Azure AD, vous devez ajouter Allocadia à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c68b7-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c68b7-125">**Pour ajouter Allocadia à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c68b7-125">**To add Allocadia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c68b7-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c68b7-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c68b7-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c68b7-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c68b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c68b7-133">Dans la zone de recherche, tapez **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-133">In the search box, type **Allocadia**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="c68b7-135">Dans le panneau des résultats, sélectionnez **Allocadia**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c68b7-135">In the results panel, select **Allocadia**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c68b7-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c68b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c68b7-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Allocadia avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c68b7-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c68b7-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Allocadia équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c68b7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span></span> <span data-ttu-id="c68b7-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Allocadia associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c68b7-140">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span></span>

<span data-ttu-id="c68b7-141">Dans Allocadia, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="c68b7-141">In Allocadia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c68b7-142">Pour configurer et tester l’authentification unique Azure AD avec Allocadia, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c68b7-142">To configure and test Azure AD single sign-on with Allocadia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c68b7-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c68b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c68b7-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c68b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c68b7-145">**[Création d’un utilisateur test Allocadia](#creating-an-allocadia-test-user)** pour avoir un équivalent de Britta Simon dans Allocadia lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="c68b7-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c68b7-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c68b7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c68b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c68b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c68b7-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c68b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c68b7-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Allocadia.</span><span class="sxs-lookup"><span data-stu-id="c68b7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="c68b7-150">**Pour configurer l’authentification unique Azure AD avec Allocadia, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="c68b7-150">**To configure Azure AD single sign-on with Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="c68b7-151">Dans le portail Azure, dans la page d’intégration de l’application **Allocadia**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-151">In the Azure portal, on the **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c68b7-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c68b7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="c68b7-155">Dans la section **Domaine et URL Allocadia**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c68b7-155">On the **Allocadia Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="c68b7-157">a.</span><span class="sxs-lookup"><span data-stu-id="c68b7-157">a.</span></span> <span data-ttu-id="c68b7-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="c68b7-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
       
     <span data-ttu-id="c68b7-159">Pour l’environnement de test : `https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="c68b7-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="c68b7-160">Pour l’environnement de production : `https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="c68b7-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="c68b7-161">b.</span><span class="sxs-lookup"><span data-stu-id="c68b7-161">b.</span></span> <span data-ttu-id="c68b7-162">Dans la zone de texte **URL de réponse** , tapez une URL en respectant les formats suivants :</span><span class="sxs-lookup"><span data-stu-id="c68b7-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
     <span data-ttu-id="c68b7-163">Pour l’environnement de test : `https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="c68b7-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="c68b7-164">Pour l’environnement de production : `https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="c68b7-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c68b7-165">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c68b7-165">These values are not real.</span></span> <span data-ttu-id="c68b7-166">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="c68b7-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="c68b7-167">Pour obtenir ces valeurs, contactez [l’équipe du support Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="c68b7-167">Contact [Allocadia support team](mailTo:support@allocadia.com) to get these values.</span></span>

4. <span data-ttu-id="c68b7-168">L’application Allocadia attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="c68b7-168">Allocadia application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c68b7-169">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c68b7-169">Configure the following claims for this application.</span></span> <span data-ttu-id="c68b7-170">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="c68b7-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c68b7-171">La capture d’écran suivante montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="c68b7-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="c68b7-173">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c68b7-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="c68b7-174">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="c68b7-174">Attribute Name</span></span> | <span data-ttu-id="c68b7-175">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="c68b7-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="c68b7-176">firstname</span><span class="sxs-lookup"><span data-stu-id="c68b7-176">firstname</span></span> | <span data-ttu-id="c68b7-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="c68b7-177">user.givenname</span></span> |
    | <span data-ttu-id="c68b7-178">lastname</span><span class="sxs-lookup"><span data-stu-id="c68b7-178">lastname</span></span> | <span data-ttu-id="c68b7-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="c68b7-179">user.surname</span></span> |
    | <span data-ttu-id="c68b7-180">email</span><span class="sxs-lookup"><span data-stu-id="c68b7-180">email</span></span> | <span data-ttu-id="c68b7-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="c68b7-181">user.mail</span></span> |
    
    <span data-ttu-id="c68b7-182">a.</span><span class="sxs-lookup"><span data-stu-id="c68b7-182">a.</span></span> <span data-ttu-id="c68b7-183">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="c68b7-185">b.</span><span class="sxs-lookup"><span data-stu-id="c68b7-185">b.</span></span> <span data-ttu-id="c68b7-186">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c68b7-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c68b7-188">c.</span><span class="sxs-lookup"><span data-stu-id="c68b7-188">c.</span></span> <span data-ttu-id="c68b7-189">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c68b7-189">From the **Value** list, type the attribute value shown for that row.</span></span>
 
    <span data-ttu-id="c68b7-190">d.</span><span class="sxs-lookup"><span data-stu-id="c68b7-190">d.</span></span> <span data-ttu-id="c68b7-191">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-191">Click **Ok**.</span></span>



6. <span data-ttu-id="c68b7-192">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c68b7-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="c68b7-194">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c68b7-194">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="c68b7-196">Pour configurer l’authentification unique côté **Allocadia**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à [l’équipe du support Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="c68b7-196">To configure single sign-on on **Allocadia** side, you need to send the downloaded **Metadata XML** to [Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="c68b7-197">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="c68b7-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c68b7-198">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c68b7-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c68b7-199">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c68b7-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c68b7-200">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c68b7-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c68b7-201">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c68b7-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="c68b7-202">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c68b7-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c68b7-204">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c68b7-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c68b7-205">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c68b7-207">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c68b7-209">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c68b7-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c68b7-211">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c68b7-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c68b7-213">a.</span><span class="sxs-lookup"><span data-stu-id="c68b7-213">a.</span></span> <span data-ttu-id="c68b7-214">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c68b7-215">b.</span><span class="sxs-lookup"><span data-stu-id="c68b7-215">b.</span></span> <span data-ttu-id="c68b7-216">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c68b7-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c68b7-217">c.</span><span class="sxs-lookup"><span data-stu-id="c68b7-217">c.</span></span> <span data-ttu-id="c68b7-218">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c68b7-219">d.</span><span class="sxs-lookup"><span data-stu-id="c68b7-219">d.</span></span> <span data-ttu-id="c68b7-220">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="c68b7-221">Création d’un utilisateur test Allocadia</span><span class="sxs-lookup"><span data-stu-id="c68b7-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="c68b7-222">Cette application prend en charge l’approvisionnement d’utilisateurs de type « juste-à-temps ».</span><span class="sxs-lookup"><span data-stu-id="c68b7-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="c68b7-223">Une fois identifiés, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="c68b7-223">After authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c68b7-224">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c68b7-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c68b7-225">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Allocadia.</span><span class="sxs-lookup"><span data-stu-id="c68b7-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Allocadia.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c68b7-227">**Pour affecter Britta Simon à Allocadia, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c68b7-227">**To assign Britta Simon to Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="c68b7-228">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c68b7-230">Dans la liste des applications, sélectionnez **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-230">In the applications list, select **Allocadia**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="c68b7-232">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c68b7-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-234">Click **Add** button.</span></span> <span data-ttu-id="c68b7-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c68b7-237">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c68b7-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c68b7-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c68b7-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c68b7-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c68b7-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c68b7-240">Testing single sign-on</span></span>

<span data-ttu-id="c68b7-241">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c68b7-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c68b7-242">Lorsque vous cliquez sur la mosaïque Allocadia dans le volet d’accès, vous devez être connecté automatiquement à votre application Allocadia.</span><span class="sxs-lookup"><span data-stu-id="c68b7-242">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span></span>
<span data-ttu-id="c68b7-243">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c68b7-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c68b7-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c68b7-244">Additional resources</span></span>

* [<span data-ttu-id="c68b7-245">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c68b7-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c68b7-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c68b7-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

