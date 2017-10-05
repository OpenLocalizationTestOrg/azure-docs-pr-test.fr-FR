---
title: "Didacticiel : Intégration d’Azure Active Directory avec CloudPassage | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 094740e20570665e975dec1a591989e411f90c16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a><span data-ttu-id="b67d1-103">Didacticiel : Intégration d’Azure Active Directory avec CloudPassage</span><span class="sxs-lookup"><span data-stu-id="b67d1-103">Tutorial: Azure Active Directory integration with CloudPassage</span></span>

<span data-ttu-id="b67d1-104">Dans ce didacticiel, vous allez apprendre à intégrer CloudPassage à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b67d1-104">In this tutorial, you learn how to integrate CloudPassage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b67d1-105">L’intégration de CloudPassage dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b67d1-105">Integrating CloudPassage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b67d1-106">Dans Azure AD, vous pouvez contrôler qui a accès à CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="b67d1-106">You can control in Azure AD who has access to CloudPassage</span></span>
- <span data-ttu-id="b67d1-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à CloudPassage (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b67d1-107">You can enable your users to automatically get signed-on to CloudPassage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b67d1-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b67d1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b67d1-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b67d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b67d1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b67d1-110">Prerequisites</span></span>

<span data-ttu-id="b67d1-111">Pour configurer l’intégration d’Azure AD avec CloudPassage, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b67d1-111">To configure Azure AD integration with CloudPassage, you need the following items:</span></span>

- <span data-ttu-id="b67d1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b67d1-113">Un abonnement CloudPassage pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b67d1-113">A CloudPassage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b67d1-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b67d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b67d1-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b67d1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b67d1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b67d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b67d1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b67d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b67d1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b67d1-118">Scenario description</span></span>
<span data-ttu-id="b67d1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b67d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b67d1-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b67d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b67d1-121">Ajout de CloudPassage à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b67d1-121">Adding CloudPassage from the gallery</span></span>
2. <span data-ttu-id="b67d1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloudpassage-from-the-gallery"></a><span data-ttu-id="b67d1-123">Ajout de CloudPassage à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b67d1-123">Adding CloudPassage from the gallery</span></span>
<span data-ttu-id="b67d1-124">Pour configurer l’intégration de CloudPassage avec Azure AD, vous devez ajouter CloudPassage, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b67d1-124">To configure the integration of CloudPassage into Azure AD, you need to add CloudPassage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b67d1-125">**Pour ajouter CloudPassage à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b67d1-125">**To add CloudPassage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b67d1-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b67d1-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b67d1-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b67d1-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b67d1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b67d1-133">Dans la zone de recherche, tapez **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-133">In the search box, type **CloudPassage**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. <span data-ttu-id="b67d1-135">Dans le volet de résultats, sélectionnez **CloudPassage**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b67d1-135">In the results panel, select **CloudPassage**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b67d1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b67d1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec CloudPassage avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b67d1-138">In this section, you configure and test Azure AD single sign-on with CloudPassage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b67d1-139">Pour que l’authentification unique fonctionne, Azure AD a besoin de savoir qui est l’utilisateur CloudPassage équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b67d1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CloudPassage is to a user in Azure AD.</span></span> <span data-ttu-id="b67d1-140">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur CloudPassage associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="b67d1-140">In other words, a link relationship between an Azure AD user and the related user in CloudPassage needs to be established.</span></span>

<span data-ttu-id="b67d1-141">Dans CloudPassage, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="b67d1-141">In CloudPassage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b67d1-142">Pour configurer et tester l’authentification unique Azure AD avec CloudPassage, vous avez besoin de suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="b67d1-142">To configure and test Azure AD single sign-on with CloudPassage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b67d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b67d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b67d1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b67d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b67d1-145">**[Création d’un utilisateur de test CloudPassage](#creating-a-cloudpassage-test-user)** pour avoir un équivalent de Britta Simon dans CloudPassage qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="b67d1-145">**[Creating a CloudPassage test user](#creating-a-cloudpassage-test-user)** - to have a counterpart of Britta Simon in CloudPassage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b67d1-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b67d1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b67d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b67d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b67d1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b67d1-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="b67d1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CloudPassage application.</span></span>

<span data-ttu-id="b67d1-150">**Pour configurer l’authentification unique Azure AD avec CloudPassage, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b67d1-150">**To configure Azure AD single sign-on with CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="b67d1-151">Dans le Portail Azure, sur la page d’intégration de l’application **CloudPassage**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-151">In the Azure portal, on the **CloudPassage** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b67d1-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b67d1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. <span data-ttu-id="b67d1-155">Dans la section **Domaine et URL CloudPassage**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b67d1-155">On the **CloudPassage Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    <span data-ttu-id="b67d1-157">a.</span><span class="sxs-lookup"><span data-stu-id="b67d1-157">a.</span></span> <span data-ttu-id="b67d1-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://portal.cloudpassage.com/saml/init/accountid`</span><span class="sxs-lookup"><span data-stu-id="b67d1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/init/accountid`</span></span>

    <span data-ttu-id="b67d1-159">b.</span><span class="sxs-lookup"><span data-stu-id="b67d1-159">b.</span></span> <span data-ttu-id="b67d1-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://portal.cloudpassage.com/saml/consume/accountid`.</span><span class="sxs-lookup"><span data-stu-id="b67d1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://portal.cloudpassage.com/saml/consume/accountid`.</span></span> <span data-ttu-id="b67d1-161">Vous pouvez obtenir la valeur de cet attribut en cliquant sur **SSO Setup documentation** dans la section **Single Sign-on Settings** de votre portail CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="b67d1-161">You can get your value for this attribute by clicking **SSO Setup documentation** in the **Single Sign-on Settings** section of your CloudPassage portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > <span data-ttu-id="b67d1-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="b67d1-163">These values are not real.</span></span> <span data-ttu-id="b67d1-164">Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles.</span><span class="sxs-lookup"><span data-stu-id="b67d1-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b67d1-165">Pour obtenir ces valeurs, contactez l’[équipe de support technique de CloudPassage](https://www.cloudpassage.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="b67d1-165">Contact [CloudPassage Client support team](https://www.cloudpassage.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="b67d1-166">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b67d1-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. <span data-ttu-id="b67d1-168">Votre application CloudPassage attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="b67d1-168">Your CloudPassage application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="b67d1-169">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="b67d1-169">The following screenshot shows an example for this.</span></span>
   
   ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. <span data-ttu-id="b67d1-171">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez le jeton SAML comme sur l’image ci-dessus et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b67d1-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>

    | <span data-ttu-id="b67d1-172">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="b67d1-172">Attribute Name</span></span> | <span data-ttu-id="b67d1-173">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="b67d1-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="b67d1-174">firstname</span><span class="sxs-lookup"><span data-stu-id="b67d1-174">firstname</span></span> |<span data-ttu-id="b67d1-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="b67d1-175">user.givenname</span></span> |
    | <span data-ttu-id="b67d1-176">lastname</span><span class="sxs-lookup"><span data-stu-id="b67d1-176">lastname</span></span> |<span data-ttu-id="b67d1-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="b67d1-177">user.surname</span></span> |
    | <span data-ttu-id="b67d1-178">email</span><span class="sxs-lookup"><span data-stu-id="b67d1-178">email</span></span> |<span data-ttu-id="b67d1-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="b67d1-179">user.mail</span></span> |
    
    <span data-ttu-id="b67d1-180">a.</span><span class="sxs-lookup"><span data-stu-id="b67d1-180">a.</span></span> <span data-ttu-id="b67d1-181">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b67d1-184">b.</span><span class="sxs-lookup"><span data-stu-id="b67d1-184">b.</span></span> <span data-ttu-id="b67d1-185">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="b67d1-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="b67d1-186">c.</span><span class="sxs-lookup"><span data-stu-id="b67d1-186">c.</span></span> <span data-ttu-id="b67d1-187">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="b67d1-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b67d1-188">d.</span><span class="sxs-lookup"><span data-stu-id="b67d1-188">d.</span></span> <span data-ttu-id="b67d1-189">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-189">Click **Ok**.</span></span>

7. <span data-ttu-id="b67d1-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b67d1-190">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="b67d1-192">Dans la section **Configuration de CloudPassage** , cliquez sur **Configurer CloudPassage** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-192">On the **CloudPassage Configuration** section, click **Configure CloudPassage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b67d1-193">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="b67d1-193">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. <span data-ttu-id="b67d1-195">Dans une autre fenêtre de navigateur Web, connectez-vous au site de votre entreprise CloudPassage en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b67d1-195">In a different browser window, sign-on to your CloudPassage company site as administrator.</span></span>

10. <span data-ttu-id="b67d1-196">Dans le menu situé en haut, cliquez sur **Settings** puis sur **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-196">In the menu on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
    ![Configurer l’authentification unique][12]

11. <span data-ttu-id="b67d1-198">Cliquez sur l’onglet **Authentication Settings** .</span><span class="sxs-lookup"><span data-stu-id="b67d1-198">Click the **Authentication Settings** tab.</span></span> 
   
    ![Configurer l’authentification unique][13]

12. <span data-ttu-id="b67d1-200">Dans la section **Single Sign-On Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b67d1-200">In the **Single Sign-on Settings** section, perform the following steps:</span></span> 
   
    ![Configurer l’authentification unique][14]

    <span data-ttu-id="b67d1-202">a.</span><span class="sxs-lookup"><span data-stu-id="b67d1-202">a.</span></span> <span data-ttu-id="b67d1-203">Cochez la case **Activer l’authentification unique (SSO) (Documentation de configuration de l’authentification unique)**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-203">Select **Enable Single sign-on(SSO)(SSO Setup Documentation)** checkbox.</span></span>
    
    <span data-ttu-id="b67d1-204">b.</span><span class="sxs-lookup"><span data-stu-id="b67d1-204">b.</span></span> <span data-ttu-id="b67d1-205">Collez **l’ID d’entité SAML** dans la zone de texte **URL de l’émetteur SAML**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-205">Paste **SAML Entity ID** into the **SAML issuer URL** textbox.</span></span>
  
    <span data-ttu-id="b67d1-206">c.</span><span class="sxs-lookup"><span data-stu-id="b67d1-206">c.</span></span> <span data-ttu-id="b67d1-207">Collez la valeur du champ **URL du service d’authentification unique SAML** dans la zone de texte **URL du point de terminaison SAML**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-207">Paste **SAML Single Sign-On Service URL** into the **SAML endpoint URL** textbox.</span></span>
  
    <span data-ttu-id="b67d1-208">d.</span><span class="sxs-lookup"><span data-stu-id="b67d1-208">d.</span></span> <span data-ttu-id="b67d1-209">Collez la valeur du champ **URL de déconnexion** dans la zone de texte **Page de déconnexion**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-209">Paste **Sign-Out URL** into the **Logout landing page** textbox.</span></span>
  
    <span data-ttu-id="b67d1-210">e.</span><span class="sxs-lookup"><span data-stu-id="b67d1-210">e.</span></span> <span data-ttu-id="b67d1-211">Ouvrez votre certificat téléchargé dans le Bloc-notes, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **Certificat X 509**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-211">Open your downloaded certificate in notepad, copy the content of downloaded certificate into your clipboard, and then paste it into the **x 509 certificate** textbox.</span></span>
  
    <span data-ttu-id="b67d1-212">f.</span><span class="sxs-lookup"><span data-stu-id="b67d1-212">f.</span></span> <span data-ttu-id="b67d1-213">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b67d1-214">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="b67d1-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b67d1-215">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="b67d1-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b67d1-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b67d1-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b67d1-217">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67d1-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="b67d1-218">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b67d1-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b67d1-220">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b67d1-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b67d1-221">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b67d1-223">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b67d1-225">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b67d1-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b67d1-227">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b67d1-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b67d1-229">a.</span><span class="sxs-lookup"><span data-stu-id="b67d1-229">a.</span></span> <span data-ttu-id="b67d1-230">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b67d1-231">b.</span><span class="sxs-lookup"><span data-stu-id="b67d1-231">b.</span></span> <span data-ttu-id="b67d1-232">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b67d1-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b67d1-233">c.</span><span class="sxs-lookup"><span data-stu-id="b67d1-233">c.</span></span> <span data-ttu-id="b67d1-234">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b67d1-235">d.</span><span class="sxs-lookup"><span data-stu-id="b67d1-235">d.</span></span> <span data-ttu-id="b67d1-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-236">Click **Create**.</span></span>
 
### <a name="creating-a-cloudpassage-test-user"></a><span data-ttu-id="b67d1-237">Création d’un utilisateur de test CloudPassage</span><span class="sxs-lookup"><span data-stu-id="b67d1-237">Creating a CloudPassage test user</span></span>

<span data-ttu-id="b67d1-238">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="b67d1-238">The objective of this section is to create a user called Britta Simon in CloudPassage.</span></span>

<span data-ttu-id="b67d1-239">**Pour créer un utilisateur appelé Britta Simon dans CloudPassage, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b67d1-239">**To create a user called Britta Simon in CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="b67d1-240">Connectez-vous à votre site d’entreprise **CloudPassage** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b67d1-240">Sign-on to your **CloudPassage** company site as an administrator.</span></span> 

2. <span data-ttu-id="b67d1-241">Dans la barre d’outils située en haut, cliquez sur **Paramètres**, puis sur **Administration du site**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-241">In the toolbar on the top, click **Settings**, and then click **Site Administration**.</span></span> 
   
   ![Création d’un utilisateur de test CloudPassage][22] 

3. <span data-ttu-id="b67d1-243">Cliquez sur l’onglet **Users**, puis sur **Add a user**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-243">Click the **Users** tab, and then click **Add New User**.</span></span> 
   
   ![Création d’un utilisateur de test CloudPassage][23]

4. <span data-ttu-id="b67d1-245">Dans la section **Add New User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b67d1-245">In the **Add New User** section, perform the following steps:</span></span> 
   
   ![Création d’un utilisateur de test CloudPassage][24]
    
    <span data-ttu-id="b67d1-247">a.</span><span class="sxs-lookup"><span data-stu-id="b67d1-247">a.</span></span> <span data-ttu-id="b67d1-248">Dans la zone de texte **First Name** , tapez Britta.</span><span class="sxs-lookup"><span data-stu-id="b67d1-248">In the **First Name** textbox, type Britta.</span></span> 
  
    <span data-ttu-id="b67d1-249">b.</span><span class="sxs-lookup"><span data-stu-id="b67d1-249">b.</span></span> <span data-ttu-id="b67d1-250">Dans la zone de texte **Last Name** , tapez Simon.</span><span class="sxs-lookup"><span data-stu-id="b67d1-250">In the **Last Name** textbox, type Simon.</span></span>
  
    <span data-ttu-id="b67d1-251">c.</span><span class="sxs-lookup"><span data-stu-id="b67d1-251">c.</span></span> <span data-ttu-id="b67d1-252">Dans les zones de texte **Username**, **Email** et **Retype Email**, entrez le nom d’utilisateur de Britta dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b67d1-252">In the **Username** textbox, the **Email** textbox and the **Retype Email** textbox, type Britta's user name in Azure AD.</span></span>
  
    <span data-ttu-id="b67d1-253">d.</span><span class="sxs-lookup"><span data-stu-id="b67d1-253">d.</span></span> <span data-ttu-id="b67d1-254">En tant que **Type d’accès**, sélectionnez **Activer l’accès portail Halo**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-254">As **Access Type**, select **Enable Halo Portal Access**.</span></span>
  
    <span data-ttu-id="b67d1-255">e.</span><span class="sxs-lookup"><span data-stu-id="b67d1-255">e.</span></span> <span data-ttu-id="b67d1-256">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b67d1-257">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b67d1-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b67d1-258">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="b67d1-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CloudPassage.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b67d1-260">**Pour attribuer Britta Simon à CloudPassage, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b67d1-260">**To assign Britta Simon to CloudPassage, perform the following steps:**</span></span>

1. <span data-ttu-id="b67d1-261">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b67d1-263">Dans la liste des applications, sélectionnez **CloudPassage**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-263">In the applications list, select **CloudPassage**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. <span data-ttu-id="b67d1-265">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b67d1-267">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-267">Click **Add** button.</span></span> <span data-ttu-id="b67d1-268">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b67d1-270">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b67d1-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b67d1-271">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b67d1-272">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b67d1-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b67d1-273">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b67d1-273">Testing single sign-on</span></span>

<span data-ttu-id="b67d1-274">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b67d1-274">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b67d1-275">Lorsque vous cliquez sur la vignette CloudPassage dans le volet d’accès, vous devez être connecté automatiquement à votre application CloudPassage.</span><span class="sxs-lookup"><span data-stu-id="b67d1-275">When you click the CloudPassage tile in the Access Panel, you should get automatically signed-on to your CloudPassage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b67d1-276">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b67d1-276">Additional resources</span></span>

* [<span data-ttu-id="b67d1-277">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b67d1-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b67d1-278">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b67d1-278">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

