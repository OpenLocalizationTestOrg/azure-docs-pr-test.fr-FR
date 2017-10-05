---
title: "Didacticiel : intégration d’Azure Active Directory à Salesforce Sandbox | Microsoft Docs"
description: "Découvrez comment configurer une authentification unique entre Azure Active Directory et Salesforce Sandbox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="c4b90-103">Didacticiel : Intégration d’Azure Active Directory à Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="c4b90-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="c4b90-104">Dans ce didacticiel, vous allez apprendre à intégrer Salesforce Sandbox avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4b90-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4b90-105">L’intégration de Salesforce Sandbox avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c4b90-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c4b90-106">Vous pouvez contrôler dans Azure AD qui a accès à Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="c4b90-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="c4b90-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Salesforce Sandbox (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4b90-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4b90-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b90-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c4b90-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4b90-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4b90-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="c4b90-110">Prerequisites</span></span>

<span data-ttu-id="c4b90-111">Pour configurer l’intégration d’Azure AD avec Salesforce Sandbox, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c4b90-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="c4b90-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4b90-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4b90-113">Un abonnement Salesforce Sandbox pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c4b90-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4b90-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c4b90-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4b90-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c4b90-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4b90-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c4b90-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4b90-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4b90-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4b90-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c4b90-118">Scenario description</span></span>
<span data-ttu-id="c4b90-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c4b90-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4b90-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c4b90-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4b90-121">Ajout de Salesforce Sandbox à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c4b90-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="c4b90-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4b90-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="c4b90-123">Ajout de Salesforce Sandbox à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c4b90-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="c4b90-124">Pour configurer l’intégration de Salesforce Sandbox avec Azure AD, vous devez ajouter Salesforce Sandbox à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="c4b90-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4b90-125">**Pour ajouter Salesforce Sandbox à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4b90-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b90-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4b90-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c4b90-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c4b90-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c4b90-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c4b90-133">Dans la zone de recherche, tapez **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="c4b90-135">Dans le volet de résultats, sélectionnez **Salesforce Sandbox**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c4b90-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4b90-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4b90-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4b90-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Salesforce Sandbox sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c4b90-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c4b90-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Salesforce Sandbox équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4b90-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="c4b90-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Salesforce Sandbox associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c4b90-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="c4b90-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** dans Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="c4b90-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="c4b90-142">Pour configurer et tester l’authentification unique Azure AD avec Salesforce Sandbox, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c4b90-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4b90-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c4b90-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4b90-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4b90-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4b90-145">**[Création d’un utilisateur de test Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)** pour avoir un équivalent de Britta Simon dans Salesforce Sandbox lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="c4b90-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4b90-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c4b90-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4b90-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c4b90-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4b90-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4b90-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4b90-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="c4b90-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="c4b90-150">**Pour configurer l’authentification unique Azure AD avec Salesforce Sandbox, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4b90-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b90-151">Dans le portail Azure, sur la page d’intégration de l’application **Salesforce Sandbox**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c4b90-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c4b90-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="c4b90-155">Dans la section **Domaine et URL Salesforce Sandbox**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c4b90-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="c4b90-157">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4b90-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4b90-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="c4b90-158">This value is not the real.</span></span> <span data-ttu-id="c4b90-159">Mettez à jour cette valeur avec l’URL de connexion réelle. Pour obtenir cette valeur, contactez l’[équipe de support client Salesforce Sandbox](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="c4b90-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="c4b90-160">Si vous avez déjà configuré l’authentification unique pour une autre instance de Salesforce Sandbox dans votre répertoire, vous devez également configurer **l’identificateur** en utilisant la même valeur que pour **l’URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="c4b90-161">Pour afficher le champ **Identificateur**, cochez la case **Afficher les paramètres avancés** dans la page **Configurer l’URL de l’application** de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c4b90-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="c4b90-162">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c4b90-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="c4b90-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c4b90-164">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c4b90-166">Dans la section **Configuration de Salesforce Sandbox**, cliquez sur **Configurer Salesforce Sandbox** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c4b90-167">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="c4b90-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="c4b90-168">![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="c4b90-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="c4b90-169">Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à votre compte d’administrateur Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="c4b90-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="c4b90-170">Dans le menu situé en haut, cliquez sur **Setup**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-170">In the menu on the top, click **Setup**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="c4b90-172">Dans le volet de navigation de gauche, cliquez sur **Security Controls (Contrôles de sécurité)**, puis sur **Single Sign-On Settings (Paramètres de l’authentification unique)**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="c4b90-174">Dans la section Single Sign-On Settings (Paramètres d’authentification unique), procédez comme suit :  ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="c4b90-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="c4b90-175">a.</span><span class="sxs-lookup"><span data-stu-id="c4b90-175">a.</span></span>  <span data-ttu-id="c4b90-176">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="c4b90-177">b.</span><span class="sxs-lookup"><span data-stu-id="c4b90-177">b.</span></span>  <span data-ttu-id="c4b90-178">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-178">Click **New**.</span></span>

12. <span data-ttu-id="c4b90-179">Dans la section SAML Single Sign-On Settings, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c4b90-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="c4b90-181">a. Dans la zone de texte Name (Nom), indiquez le nom de la configuration (par exemple, *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="c4b90-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="c4b90-182">b.</span><span class="sxs-lookup"><span data-stu-id="c4b90-182">b.</span></span> <span data-ttu-id="c4b90-183">Collez la valeur **ID d’entité SAML** dans la zone de texte **Issuer** (Émetteur).</span><span class="sxs-lookup"><span data-stu-id="c4b90-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="c4b90-184">c.</span><span class="sxs-lookup"><span data-stu-id="c4b90-184">c.</span></span> <span data-ttu-id="c4b90-185">Dans la zone de texte **Entity Id** (ID d’entité), entrez **https://test.salesforce.com** s’il s’agit de la première instance Salesforce Sandbox que vous ajoutez à votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c4b90-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="c4b90-186">Si vous avez déjà ajouté une instance de Salesforce Sandbox, pour **l’ID d’entité**, entrez **l’URL de connexion**, qui doit être au format : `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="c4b90-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="c4b90-187">d.</span><span class="sxs-lookup"><span data-stu-id="c4b90-187">d.</span></span> <span data-ttu-id="c4b90-188">Cliquez sur **Parcourir** pour charger le certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="c4b90-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="c4b90-189">e.</span><span class="sxs-lookup"><span data-stu-id="c4b90-189">e.</span></span> <span data-ttu-id="c4b90-190">Pour **SAML Identity Type (Type d’identité SAML)**, sélectionnez **Assertion contains the Federation ID from the User object (L’assertion contient l’ID de fédération de l’objet utilisateur)**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="c4b90-191">f.</span><span class="sxs-lookup"><span data-stu-id="c4b90-191">f.</span></span> <span data-ttu-id="c4b90-192">Pour **SAML Identity Location (Emplacement de l’identité SAML)**, sélectionnez **Identity is in the NameIdentifier element of the Subject statement (L’identité figure dans l’élément NameIdentifier de l’instruction Subject)**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="c4b90-193">g.</span><span class="sxs-lookup"><span data-stu-id="c4b90-193">g.</span></span> <span data-ttu-id="c4b90-194">Collez l’**URL du service d’authentification unique** dans la zone de texte **Identity Provider Login URL** (URL de connexion du fournisseur identité).</span><span class="sxs-lookup"><span data-stu-id="c4b90-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="c4b90-195">h.</span><span class="sxs-lookup"><span data-stu-id="c4b90-195">h.</span></span> <span data-ttu-id="c4b90-196">SFDC ne prend pas en charge la déconnexion SAML.</span><span class="sxs-lookup"><span data-stu-id="c4b90-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="c4b90-197">Pour contourner ce problème, collez « https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0 » dans la zone de texte **Identity Provider Logout URL** (URL de déconnexion du fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="c4b90-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="c4b90-198">i.</span><span class="sxs-lookup"><span data-stu-id="c4b90-198">i.</span></span> <span data-ttu-id="c4b90-199">Pour **Service Provider Initiated Request Binding (Liaison de demande initiée par le fournisseur de services)**, sélectionnez **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="c4b90-200">j.</span><span class="sxs-lookup"><span data-stu-id="c4b90-200">j.</span></span> <span data-ttu-id="c4b90-201">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="c4b90-202">Activer votre domaine</span><span class="sxs-lookup"><span data-stu-id="c4b90-202">Enable your domain</span></span>
<span data-ttu-id="c4b90-203">Cette section suppose que vous avez déjà créé un domaine.</span><span class="sxs-lookup"><span data-stu-id="c4b90-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="c4b90-204">Pour plus d’informations, voir [Définition de votre nom de domaine](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="c4b90-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="c4b90-205">**Pour activer votre domaine, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4b90-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b90-206">Dans le volet de navigation gauche, cliquez sur **Domain Management (Gestion des domaines)**, puis sur **My Domain (Mon domaine)**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="c4b90-208">Vérifiez que votre domaine a été correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="c4b90-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="c4b90-209">Dans la section **Login Page Settings (Paramètres de la page de connexion)**, cliquez sur **Edit (Modifier)**, puis, pour **Authentication Service (Service d’authentification)**, sélectionnez le nom du paramètre d’authentification unique SAML de la section précédente, avant de cliquer sur **Save (Enregistrer)**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="c4b90-211">Dès qu’un domaine est configuré, vos utilisateurs doivent utiliser l’URL du domaine pour se connecter au sandbox Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c4b90-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="c4b90-212">Pour obtenir la valeur de l’URL, cliquez sur le profil d’authentification unique créé à la section précédente.</span><span class="sxs-lookup"><span data-stu-id="c4b90-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="c4b90-213">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c4b90-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c4b90-214">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c4b90-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c4b90-215">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4b90-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4b90-216">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4b90-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4b90-217">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b90-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c4b90-219">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4b90-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b90-220">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4b90-222">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4b90-224">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4b90-226">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c4b90-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4b90-228">a.</span><span class="sxs-lookup"><span data-stu-id="c4b90-228">a.</span></span> <span data-ttu-id="c4b90-229">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4b90-230">b.</span><span class="sxs-lookup"><span data-stu-id="c4b90-230">b.</span></span> <span data-ttu-id="c4b90-231">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4b90-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4b90-232">c.</span><span class="sxs-lookup"><span data-stu-id="c4b90-232">c.</span></span> <span data-ttu-id="c4b90-233">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c4b90-234">d.</span><span class="sxs-lookup"><span data-stu-id="c4b90-234">d.</span></span> <span data-ttu-id="c4b90-235">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="c4b90-236">Création d’un utilisateur de test Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="c4b90-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="c4b90-237">Dans cette section, un utilisateur nommé Britta Simon est créé dans Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="c4b90-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="c4b90-238">Salesforce Sandbox prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="c4b90-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="c4b90-239">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="c4b90-239">There is no action item for you in this section.</span></span> <span data-ttu-id="c4b90-240">Si un utilisateur n’existe pas dans Salesforce Sandbox, un nouveau est créé lorsque vous tentez d’accéder à Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="c4b90-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c4b90-241">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4b90-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c4b90-242">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="c4b90-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c4b90-244">**Pour affecter Britta Simon à Salesforce Sandbox, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c4b90-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b90-245">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c4b90-247">Dans la liste des applications, sélectionnez **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="c4b90-249">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c4b90-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-251">Click **Add** button.</span></span> <span data-ttu-id="c4b90-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c4b90-254">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c4b90-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c4b90-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4b90-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c4b90-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4b90-257">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c4b90-257">Testing single sign-on</span></span>

<span data-ttu-id="c4b90-258">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c4b90-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="c4b90-259">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c4b90-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4b90-260">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c4b90-260">Additional resources</span></span>

* [<span data-ttu-id="c4b90-261">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4b90-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4b90-262">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c4b90-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c4b90-263">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c4b90-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

