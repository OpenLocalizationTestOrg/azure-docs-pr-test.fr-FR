---
title: "Didacticiel : Intégration d’Azure Active Directory à Netsuite | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="9bc09-103">Didacticiel : Intégration d’Azure Active Directory à Netsuite</span><span class="sxs-lookup"><span data-stu-id="9bc09-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="9bc09-104">Dans ce didacticiel, vous allez apprendre à intégrer Azure Active Directory (Azure AD) avec Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9bc09-105">L’intégration de Netsuite avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9bc09-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9bc09-106">Dans Azure AD, vous pouvez contrôler qui a accès à Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="9bc09-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Netsuite (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bc09-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9bc09-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc09-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9bc09-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9bc09-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bc09-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="9bc09-110">Prerequisites</span></span>

<span data-ttu-id="9bc09-111">Pour configurer l’intégration d’Azure AD avec Netsuite, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9bc09-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="9bc09-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bc09-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9bc09-113">Un abonnement Netsuite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9bc09-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9bc09-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9bc09-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9bc09-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9bc09-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9bc09-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9bc09-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9bc09-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bc09-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9bc09-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9bc09-118">Scenario description</span></span>
<span data-ttu-id="9bc09-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9bc09-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9bc09-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9bc09-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9bc09-121">Ajout de Netsuite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9bc09-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="9bc09-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bc09-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="9bc09-123">Ajout de Netsuite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9bc09-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="9bc09-124">Pour configurer l’intégration de Netsuite à Azure AD, vous devez ajouter Netsuite à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="9bc09-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9bc09-125">**Pour ajouter Netsuite à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9bc09-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9bc09-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9bc09-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9bc09-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9bc09-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9bc09-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9bc09-133">Dans la zone de recherche, tapez **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-133">In the search box, type **Netsuite**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="9bc09-135">Dans le panneau des résultats, sélectionnez **Netsuite**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9bc09-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9bc09-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bc09-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9bc09-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Netsuite sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9bc09-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9bc09-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Netsuite équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bc09-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="9bc09-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Netsuite associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="9bc09-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="9bc09-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** dans Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="9bc09-142">Pour configurer et tester l’authentification unique Azure AD avec Netsuite, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="9bc09-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9bc09-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9bc09-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9bc09-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9bc09-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9bc09-145">**[Création d’un utilisateur de test Netsuite](#creating-a-netsuite-test-user)** pour avoir un équivalent de Britta Simon dans Netsuite lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="9bc09-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9bc09-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bc09-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9bc09-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9bc09-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9bc09-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bc09-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9bc09-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="9bc09-150">**Pour configurer l’authentification unique Azure AD avec Netsuite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9bc09-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="9bc09-151">Dans le portail Azure, sur la page d’intégration de l’application **Netsuite**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9bc09-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9bc09-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="9bc09-155">Dans la section **Domaine et URL Netsuite**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9bc09-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="9bc09-157">Dans la zone de texte **URL de réponse**, tapez une URL au format suivant :   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="9bc09-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9bc09-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="9bc09-158">This value is not real value.</span></span> <span data-ttu-id="9bc09-159">Mettez à jour la valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="9bc09-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="9bc09-160">Pour obtenir cette valeur, contactez [l’équipe de support technique Netsuite](http://www.netsuite.com/portal/services/support.shtml).</span><span class="sxs-lookup"><span data-stu-id="9bc09-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="9bc09-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9bc09-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="9bc09-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9bc09-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9bc09-165">Dans la section **Configuration de Netsuite**, cliquez sur **Configurer Netsuite** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9bc09-166">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="9bc09-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="9bc09-168">Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à votre site d’entreprise Netsuite en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9bc09-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="9bc09-169">Dans la barre d’outils située en haut de la page, cliquez sur **Configuration**, puis sur **Gestionnaire de configuration**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="9bc09-171">Dans la liste **Tâches de configuration**, sélectionnez **Intégration**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="9bc09-173">Dans la section **Gérer l’authentification**, cliquez sur **Authentification unique SAML**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="9bc09-175">Sur la page **Configuration SAML** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9bc09-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="9bc09-176">a.</span><span class="sxs-lookup"><span data-stu-id="9bc09-176">a.</span></span> <span data-ttu-id="9bc09-177">Copiez la valeur **URL du service d’authentification unique SAML** à partir de la section **Référence rapide** de **Configurer l’authentification**, puis collez-la dans le champ **Identity Provider Login Page** (Page de connexion du fournisseur d’identité) de Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="9bc09-179">b.</span><span class="sxs-lookup"><span data-stu-id="9bc09-179">b.</span></span> <span data-ttu-id="9bc09-180">Dans Netsuite, sélectionnez **Méthode d’authentification principale**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="9bc09-181">c.</span><span class="sxs-lookup"><span data-stu-id="9bc09-181">c.</span></span> <span data-ttu-id="9bc09-182">Pour le champ intitulé **Métadonnées du fournisseur d’identité SAMLV2**, sélectionnez **Charger un fichier de métadonnées IDP**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="9bc09-183">Cliquez ensuite sur **Parcourir** pour charger le fichier de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc09-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="9bc09-185">d.</span><span class="sxs-lookup"><span data-stu-id="9bc09-185">d.</span></span> <span data-ttu-id="9bc09-186">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-186">Click **Submit**.</span></span>

12. <span data-ttu-id="9bc09-187">Dans Azure AD, activez la case à cocher **Afficher et modifier tous les autres attributs utilisateur**, puis ajoutez un attribut.</span><span class="sxs-lookup"><span data-stu-id="9bc09-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="9bc09-189">Dans le champ **Nom de l’attribut**, entrez `account`.</span><span class="sxs-lookup"><span data-stu-id="9bc09-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="9bc09-190">Dans le champ **Valeur de l’attribut**, entrez votre ID de compte Netsuite. Cette valeur est constante et change en fonction du compte.</span><span class="sxs-lookup"><span data-stu-id="9bc09-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="9bc09-191">Vous trouverez ci-dessous des instructions sur la recherche de votre ID de compte :</span><span class="sxs-lookup"><span data-stu-id="9bc09-191">Instructions on how to find your account ID are included below:</span></span>

      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="9bc09-193">a.</span><span class="sxs-lookup"><span data-stu-id="9bc09-193">a.</span></span> <span data-ttu-id="9bc09-194">Dans Netsuite, dans le menu de navigation supérieur, cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="9bc09-195">b.</span><span class="sxs-lookup"><span data-stu-id="9bc09-195">b.</span></span> <span data-ttu-id="9bc09-196">Cliquez ensuite sous la section **Tâches de configuration** du menu de navigation situé à gauche, sélectionnez la section **Intégration**, puis cliquez sur **Préférences de services web**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="9bc09-197">c.</span><span class="sxs-lookup"><span data-stu-id="9bc09-197">c.</span></span> <span data-ttu-id="9bc09-198">Copiez votre ID de compte Netsuite et collez-le dans le champ **Valeur de l’attribut** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bc09-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="9bc09-200">Avant que les utilisateurs puissent utiliser l’authentification unique dans Netsuite, vous devez d’abord leur affecter les autorisations appropriées dans Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="9bc09-201">Procédez comme suit pour attribuer ces instructions.</span><span class="sxs-lookup"><span data-stu-id="9bc09-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="9bc09-202">a.</span><span class="sxs-lookup"><span data-stu-id="9bc09-202">a.</span></span> <span data-ttu-id="9bc09-203">Dans le menu de navigation principal, cliquez sur **Configuration**, puis sur **Gestionnaire de configuration**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="9bc09-205">b.</span><span class="sxs-lookup"><span data-stu-id="9bc09-205">b.</span></span> <span data-ttu-id="9bc09-206">Dans le menu de navigation situé à gauche, sélectionnez **Utilisateurs/Rôles**, puis cliquez sur **Gérer les rôles**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="9bc09-208">c.</span><span class="sxs-lookup"><span data-stu-id="9bc09-208">c.</span></span> <span data-ttu-id="9bc09-209">Cliquez sur **Nouveau rôle**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-209">Click **New Role**.</span></span>

    <span data-ttu-id="9bc09-210">d.</span><span class="sxs-lookup"><span data-stu-id="9bc09-210">d.</span></span> <span data-ttu-id="9bc09-211">Entrez un **Nom** pour le nouveau rôle, puis cochez la case **Authentification unique seulement**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="9bc09-213">e.</span><span class="sxs-lookup"><span data-stu-id="9bc09-213">e.</span></span> <span data-ttu-id="9bc09-214">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-214">Click **Save**.</span></span>

    <span data-ttu-id="9bc09-215">f.</span><span class="sxs-lookup"><span data-stu-id="9bc09-215">f.</span></span> <span data-ttu-id="9bc09-216">Dans le menu situé en haut, cliquez sur **Autorisations**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="9bc09-217">Cliquez sur **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-217">Then click **Setup**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="9bc09-219">g.</span><span class="sxs-lookup"><span data-stu-id="9bc09-219">g.</span></span> <span data-ttu-id="9bc09-220">Sélectionnez **Configurer l’authentification unique SAM**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="9bc09-221">h.</span><span class="sxs-lookup"><span data-stu-id="9bc09-221">h.</span></span> <span data-ttu-id="9bc09-222">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-222">Click **Save**.</span></span>

    <span data-ttu-id="9bc09-223">i.</span><span class="sxs-lookup"><span data-stu-id="9bc09-223">i.</span></span> <span data-ttu-id="9bc09-224">Dans le menu de navigation principal, cliquez sur **Configuration**, puis sur **Gestionnaire de configuration**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="9bc09-226">j.</span><span class="sxs-lookup"><span data-stu-id="9bc09-226">j.</span></span> <span data-ttu-id="9bc09-227">Dans le menu de navigation situé à gauche, sélectionnez **Utilisateurs/Rôles**, puis cliquez sur **Gérer les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="9bc09-229">k.</span><span class="sxs-lookup"><span data-stu-id="9bc09-229">k.</span></span> <span data-ttu-id="9bc09-230">Sélectionnez un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="9bc09-230">Select a test user.</span></span> <span data-ttu-id="9bc09-231">Puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-231">Then click **Edit**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="9bc09-233">l.</span><span class="sxs-lookup"><span data-stu-id="9bc09-233">l.</span></span> <span data-ttu-id="9bc09-234">Dans la boîte de dialogue Rôles, sélectionnez le rôle que vous avez créé et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Configurer l’authentification unique](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="9bc09-236">m.</span><span class="sxs-lookup"><span data-stu-id="9bc09-236">m.</span></span> <span data-ttu-id="9bc09-237">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="9bc09-238">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9bc09-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9bc09-239">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9bc09-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9bc09-240">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9bc09-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9bc09-241">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bc09-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="9bc09-242">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc09-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9bc09-244">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9bc09-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9bc09-245">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="9bc09-247">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9bc09-249">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9bc09-251">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9bc09-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9bc09-253">a.</span><span class="sxs-lookup"><span data-stu-id="9bc09-253">a.</span></span> <span data-ttu-id="9bc09-254">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9bc09-255">b.</span><span class="sxs-lookup"><span data-stu-id="9bc09-255">b.</span></span> <span data-ttu-id="9bc09-256">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9bc09-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9bc09-257">c.</span><span class="sxs-lookup"><span data-stu-id="9bc09-257">c.</span></span> <span data-ttu-id="9bc09-258">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9bc09-259">d.</span><span class="sxs-lookup"><span data-stu-id="9bc09-259">d.</span></span> <span data-ttu-id="9bc09-260">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="9bc09-261">Création d’un utilisateur de test Netsuite</span><span class="sxs-lookup"><span data-stu-id="9bc09-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="9bc09-262">Dans cette section, un utilisateur nommé Britta Simon est créé dans Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="9bc09-263">Netsuite prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="9bc09-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="9bc09-264">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="9bc09-264">There is no action item for you in this section.</span></span> <span data-ttu-id="9bc09-265">Si un utilisateur n’existe pas dans Netsuite, un nouveau est créé lorsque vous tentez d’accéder à Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9bc09-266">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bc09-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9bc09-267">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Netsuite.</span><span class="sxs-lookup"><span data-stu-id="9bc09-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9bc09-269">**Pour affecter Britta Simon à Netsuite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9bc09-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="9bc09-270">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9bc09-272">Dans la liste des applications, sélectionnez **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-272">In the applications list, select **Netsuite**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="9bc09-274">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9bc09-276">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-276">Click **Add** button.</span></span> <span data-ttu-id="9bc09-277">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9bc09-279">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9bc09-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9bc09-280">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9bc09-281">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9bc09-282">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9bc09-282">Testing single sign-on</span></span>

<span data-ttu-id="9bc09-283">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9bc09-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9bc09-284">Pour tester vos paramètres d’authentification unique, ouvrez le volet d’accès à l’adresse [https://myapps.microsoft.com](https://myapps.microsoft.com/), puis connectez-vous au compte de test et cliquez sur **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="9bc09-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9bc09-285">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9bc09-285">Additional resources</span></span>

* [<span data-ttu-id="9bc09-286">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9bc09-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9bc09-287">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9bc09-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9bc09-288">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="9bc09-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

