---
title: "Tutorial: Intégration d'Azure Active Directory à Moxtra | Microsoft Docs"
description: "Découvrez comment configurer l'authentification unique entre Azure Active Directory et Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: db2f041a44b6771b0a4f734e58d899298ef0847b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="20474-103">Didacticiel : Intégration d'Azure Active Directory avec Moxtra</span><span class="sxs-lookup"><span data-stu-id="20474-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="20474-104">Dans ce didacticiel, vous allez apprendre à intégrer Moxtra à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="20474-104">In this tutorial, you learn how to integrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20474-105">L’intégration de Moxtra dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="20474-105">Integrating Moxtra with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="20474-106">Dans Azure AD, vous pouvez contrôler qui a accès à Moxtra</span><span class="sxs-lookup"><span data-stu-id="20474-106">You can control in Azure AD who has access to Moxtra</span></span>
- <span data-ttu-id="20474-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Moxtra (via l'authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="20474-107">You can enable your users to automatically get signed-on to Moxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="20474-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="20474-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="20474-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="20474-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20474-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="20474-110">Prerequisites</span></span>

<span data-ttu-id="20474-111">Pour configurer l'intégration d'Azure AD avec Moxtra, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="20474-111">To configure Azure AD integration with Moxtra, you need the following items:</span></span>

- <span data-ttu-id="20474-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="20474-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20474-113">Un abonnement Moxtra pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="20474-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20474-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="20474-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="20474-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="20474-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20474-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="20474-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20474-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20474-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20474-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="20474-118">Scenario description</span></span>
<span data-ttu-id="20474-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="20474-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20474-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="20474-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20474-121">Ajout de Moxtra à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="20474-121">Adding Moxtra from the gallery</span></span>
2. <span data-ttu-id="20474-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="20474-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-the-gallery"></a><span data-ttu-id="20474-123">Ajout de Moxtra à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="20474-123">Adding Moxtra from the gallery</span></span>
<span data-ttu-id="20474-124">Pour configurer l'intégration de Moxtra à Azure AD, vous devez ajouter Moxtra à votre liste d'applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="20474-124">To configure the integration of Moxtra into Azure AD, you need to add Moxtra from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="20474-125">**Pour ajouter Moxtra à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20474-125">**To add Moxtra from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="20474-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="20474-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="20474-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="20474-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="20474-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="20474-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="20474-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="20474-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="20474-133">Dans la zone de recherche, tapez **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="20474-133">In the search box, type **Moxtra**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="20474-135">Dans le panneau des résultats, sélectionnez **Moxtra**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="20474-135">In the results panel, select **Moxtra**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="20474-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="20474-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="20474-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Moxtra, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="20474-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="20474-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Moxtra correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20474-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxtra is to a user in Azure AD.</span></span> <span data-ttu-id="20474-140">En d'autres termes, il faut établir une relation entre l'utilisateur Azure AD et l'utilisateur Moxtra associé.</span><span class="sxs-lookup"><span data-stu-id="20474-140">In other words, a link relationship between an Azure AD user and the related user in Moxtra needs to be established.</span></span>

<span data-ttu-id="20474-141">Dans Moxtra, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="20474-141">In Moxtra, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="20474-142">Pour configurer et tester l'authentification unique Azure AD avec Moxtra, vous devez suivre les blocs élémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="20474-142">To configure and test Azure AD single sign-on with Moxtra, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="20474-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="20474-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="20474-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="20474-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20474-145">**[Création d’un utilisateur de test Moxtra](#creating-a-moxtra-test-user)** pour obtenir un équivalent de Britta Simon dans Moxtra lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="20474-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - to have a counterpart of Britta Simon in Moxtra that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="20474-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20474-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20474-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="20474-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="20474-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="20474-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="20474-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application Moxtra.</span><span class="sxs-lookup"><span data-stu-id="20474-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="20474-150">**Pour configurer l'authentification unique Azure AD avec Moxtra, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20474-150">**To configure Azure AD single sign-on with Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="20474-151">Dans le portail Azure, sur la page d’intégration de l’application **Moxtra**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="20474-151">In the Azure portal, on the **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="20474-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="20474-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="20474-155">Dans la section **Domaine et URL Moxtra**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="20474-155">On the **Moxtra Domain and URLs** section, perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="20474-157">Dans la zone de texte **URL d’authentification**, tapez l’URL : `https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="20474-157">In the **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="20474-158">L’application Moxtra attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="20474-158">Moxtra application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="20474-159">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="20474-159">Configure the following claims for this application.</span></span> <span data-ttu-id="20474-160">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="20474-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="20474-161">La capture d’écran suivante montre un exemple de cette configuration.</span><span class="sxs-lookup"><span data-stu-id="20474-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="20474-163">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, configurez l’attribut de jeton SAML comme sur l’image et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="20474-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="20474-164">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="20474-164">Attribute Name</span></span> | <span data-ttu-id="20474-165">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="20474-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="20474-166">firstname</span><span class="sxs-lookup"><span data-stu-id="20474-166">firstname</span></span> | <span data-ttu-id="20474-167">user.givenname</span><span class="sxs-lookup"><span data-stu-id="20474-167">user.givenname</span></span> |
    | <span data-ttu-id="20474-168">lastname</span><span class="sxs-lookup"><span data-stu-id="20474-168">lastname</span></span> | <span data-ttu-id="20474-169">user.surname</span><span class="sxs-lookup"><span data-stu-id="20474-169">user.surname</span></span> |
    | <span data-ttu-id="20474-170">idpid</span><span class="sxs-lookup"><span data-stu-id="20474-170">idpid</span></span>    | <span data-ttu-id="20474-171">< ID d’entité SAML ></span><span class="sxs-lookup"><span data-stu-id="20474-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="20474-172">La valeur de l’attribut **idpid** n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="20474-172">The value of **idpid** attribute is not real.</span></span> <span data-ttu-id="20474-173">Pour obtenir la valeur réelle, reportez-vous à la section **Référence rapide**, dans la rubrique **Configuration de Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="20474-173">You can get the actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="20474-174">a.</span><span class="sxs-lookup"><span data-stu-id="20474-174">a.</span></span> <span data-ttu-id="20474-175">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="20474-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="20474-177">b.</span><span class="sxs-lookup"><span data-stu-id="20474-177">b.</span></span> <span data-ttu-id="20474-178">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="20474-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="20474-180">c.</span><span class="sxs-lookup"><span data-stu-id="20474-180">c.</span></span> <span data-ttu-id="20474-181">Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="20474-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="20474-182">d.</span><span class="sxs-lookup"><span data-stu-id="20474-182">d.</span></span> <span data-ttu-id="20474-183">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="20474-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="20474-184">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="20474-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="20474-186">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="20474-186">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="20474-188">Dans la section **Configuration de Moxtra**, cliquez sur **Configurer Moxtra** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="20474-188">On the **Moxtra Configuration** section, click **Configure Moxtra** to open **Configure sign-on** window.</span></span> <span data-ttu-id="20474-189">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="20474-189">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="20474-191">Dans une autre fenêtre de navigateur, connectez-vous à votre site d'entreprise Moxtra en tant qu'administrateur.</span><span class="sxs-lookup"><span data-stu-id="20474-191">In another browser window, sign on to your Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="20474-192">Dans la barre d’outils située à gauche, cliquez sur **Console Administrateur > Authentification unique SAML**, puis sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="20474-192">In the toolbar on the left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="20474-194">Sur la page **SAML** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="20474-194">On the **SAML** page, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="20474-196">a.</span><span class="sxs-lookup"><span data-stu-id="20474-196">a.</span></span> <span data-ttu-id="20474-197">Dans la zone de texte **Nom**, saisissez le nom de votre configuration (par ex., *SAML*).</span><span class="sxs-lookup"><span data-stu-id="20474-197">In the **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="20474-198">b.</span><span class="sxs-lookup"><span data-stu-id="20474-198">b.</span></span> <span data-ttu-id="20474-199">Dans la zone de texte **ID d’entité IdP**, collez la valeur **ID d’entité SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="20474-199">In the **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="20474-200">c.</span><span class="sxs-lookup"><span data-stu-id="20474-200">c.</span></span> <span data-ttu-id="20474-201">Dans la zone de texte **URL de connexion**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="20474-201">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="20474-202">d.</span><span class="sxs-lookup"><span data-stu-id="20474-202">d.</span></span> <span data-ttu-id="20474-203">Dans la zone de texte **AuthnContextClassRef**, tapez **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="20474-203">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="20474-204">e.</span><span class="sxs-lookup"><span data-stu-id="20474-204">e.</span></span> <span data-ttu-id="20474-205">Dans la zone de texte **Format NameID**, entrez **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="20474-205">In the **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="20474-206">f.</span><span class="sxs-lookup"><span data-stu-id="20474-206">f.</span></span> <span data-ttu-id="20474-207">Dans le bloc-notes, ouvrez le certificat que vous avez téléchargé depuis le portail Azure, copiez son contenu, puis collez-le dans la zone de texte **Certificat**.</span><span class="sxs-lookup"><span data-stu-id="20474-207">Open certificate which you have downloaded from Azure portal in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="20474-208">g.</span><span class="sxs-lookup"><span data-stu-id="20474-208">g.</span></span> <span data-ttu-id="20474-209">Dans la zone de texte du domaine de messagerie SAML, tapez votre domaine de messagerie SAML.</span><span class="sxs-lookup"><span data-stu-id="20474-209">In the SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="20474-210">Pour connaître les étapes de vérification du domaine, cliquez sur le «**i**» ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="20474-210">To see the steps to verify the domain, click the "**i**" below.</span></span>

    <span data-ttu-id="20474-211">h.</span><span class="sxs-lookup"><span data-stu-id="20474-211">h.</span></span> <span data-ttu-id="20474-212">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="20474-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="20474-213">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="20474-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="20474-214">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="20474-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="20474-215">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="20474-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="20474-216">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="20474-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="20474-217">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="20474-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="20474-219">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20474-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="20474-220">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="20474-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20474-222">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="20474-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20474-224">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="20474-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20474-226">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="20474-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20474-228">a.</span><span class="sxs-lookup"><span data-stu-id="20474-228">a.</span></span> <span data-ttu-id="20474-229">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="20474-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20474-230">b.</span><span class="sxs-lookup"><span data-stu-id="20474-230">b.</span></span> <span data-ttu-id="20474-231">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="20474-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="20474-232">c.</span><span class="sxs-lookup"><span data-stu-id="20474-232">c.</span></span> <span data-ttu-id="20474-233">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="20474-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="20474-234">d.</span><span class="sxs-lookup"><span data-stu-id="20474-234">d.</span></span> <span data-ttu-id="20474-235">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="20474-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="20474-236">Création d'un utilisateur de test Moxtra</span><span class="sxs-lookup"><span data-stu-id="20474-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="20474-237">L'objectif de cette section est de créer un utilisateur appelé Britta Simon dans Moxtra.</span><span class="sxs-lookup"><span data-stu-id="20474-237">The objective of this section is to create a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="20474-238">**Pour créer un utilisateur appelé Britta Simon dans Moxtra, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20474-238">**To create a user called Britta Simon in Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="20474-239">Connectez-vous à votre site d’entreprise Moxtra en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="20474-239">Sign on to your Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="20474-240">Dans la barre d’outils située à gauche, cliquez sur **Console Administrateur > Gestion des utilisateurs**, puis sur **Ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="20474-240">In the toolbar on the left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="20474-242">Dans la boîte de dialogue **Ajouter un utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="20474-242">On the **Add User** dialog, perform the following steps:</span></span>
  
    <span data-ttu-id="20474-243">a.</span><span class="sxs-lookup"><span data-stu-id="20474-243">a.</span></span> <span data-ttu-id="20474-244">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="20474-244">In the **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="20474-245">b.</span><span class="sxs-lookup"><span data-stu-id="20474-245">b.</span></span> <span data-ttu-id="20474-246">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="20474-246">In the **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="20474-247">c.</span><span class="sxs-lookup"><span data-stu-id="20474-247">c.</span></span> <span data-ttu-id="20474-248">Dans la zone de texte **E-mail**, entrez l’adresse e-mail de Britta, telle qu’elle est indiquée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="20474-248">In the **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="20474-249">d.</span><span class="sxs-lookup"><span data-stu-id="20474-249">d.</span></span> <span data-ttu-id="20474-250">Dans la zone de texte **Division**, saisissez **Développement**.</span><span class="sxs-lookup"><span data-stu-id="20474-250">In the **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="20474-251">e.</span><span class="sxs-lookup"><span data-stu-id="20474-251">e.</span></span> <span data-ttu-id="20474-252">Dans la zone de texte **Service**, saisissez **Informatique**.</span><span class="sxs-lookup"><span data-stu-id="20474-252">In the **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="20474-253">f.</span><span class="sxs-lookup"><span data-stu-id="20474-253">f.</span></span> <span data-ttu-id="20474-254">Sélectionnez **Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="20474-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="20474-255">g.</span><span class="sxs-lookup"><span data-stu-id="20474-255">g.</span></span> <span data-ttu-id="20474-256">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="20474-256">Click **Add**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="20474-257">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="20474-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="20474-258">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Moxtra.</span><span class="sxs-lookup"><span data-stu-id="20474-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxtra.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="20474-260">**Pour affecter Britta Simon à Moxtra, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="20474-260">**To assign Britta Simon to Moxtra, perform the following steps:**</span></span>

1. <span data-ttu-id="20474-261">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="20474-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="20474-263">Dans la liste des applications, sélectionnez **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="20474-263">In the applications list, select **Moxtra**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="20474-265">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="20474-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="20474-267">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="20474-267">Click **Add** button.</span></span> <span data-ttu-id="20474-268">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="20474-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="20474-270">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="20474-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="20474-271">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="20474-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20474-272">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="20474-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="20474-273">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="20474-273">Testing single sign-on</span></span>

<span data-ttu-id="20474-274">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="20474-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="20474-275">Lorsque vous cliquez sur la mosaïque Moxtra dans le volet d'accès, vous êtes connecté automatiquement à votre application Moxtra.</span><span class="sxs-lookup"><span data-stu-id="20474-275">When you click the Moxtra tile in the Access Panel, you should get automatically signed-on to your Moxtra application.</span></span>
<span data-ttu-id="20474-276">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="20474-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="20474-277">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="20474-277">Additional resources</span></span>

* [<span data-ttu-id="20474-278">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="20474-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20474-279">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="20474-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

