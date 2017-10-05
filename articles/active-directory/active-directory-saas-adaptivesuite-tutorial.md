---
title: "Didacticiel : Intégration d’Azure Active Directory à Adaptative Suite | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Adaptive Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="854a8-103">Didacticiel : Intégration d’Azure Active Directory à Adaptative Suite</span><span class="sxs-lookup"><span data-stu-id="854a8-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="854a8-104">Dans ce didacticiel, vous allez apprendre à intégrer Adaptive Suite dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="854a8-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="854a8-105">L’intégration d’Adaptive Suite dans Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="854a8-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="854a8-106">Dans Azure AD, vous pouvez contrôler qui a accès à Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="854a8-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="854a8-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Adaptive Suite (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="854a8-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="854a8-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="854a8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="854a8-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="854a8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="854a8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="854a8-110">Prerequisites</span></span>

<span data-ttu-id="854a8-111">Pour configurer l’intégration d’Azure AD dans Adaptive Suite, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="854a8-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="854a8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="854a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="854a8-113">Un abonnement Adaptive Suite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="854a8-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="854a8-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="854a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="854a8-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="854a8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="854a8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="854a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="854a8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="854a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="854a8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="854a8-118">Scenario description</span></span>
<span data-ttu-id="854a8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="854a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="854a8-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="854a8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="854a8-121">Ajout d’Adaptive Suite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="854a8-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="854a8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="854a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="854a8-123">Ajout d’Adaptive Suite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="854a8-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="854a8-124">Pour configurer l’intégration d’Adaptive Suite dans Azure AD, vous devez ajouter Adaptive Suite, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="854a8-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="854a8-125">**Pour ajouter Adaptive Suite à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="854a8-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="854a8-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="854a8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="854a8-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="854a8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="854a8-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="854a8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="854a8-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="854a8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="854a8-133">Dans la zone de recherche, tapez **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="854a8-133">In the search box, type **Adaptive Suite**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="854a8-135">Dans le volet de résultats, sélectionnez **Adaptive Suite**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="854a8-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="854a8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="854a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="854a8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Adaptive Suite, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="854a8-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="854a8-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Adaptive Suite correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="854a8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="854a8-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Adaptive Suite associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="854a8-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="854a8-141">Dans Adaptive Suite, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="854a8-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="854a8-142">Pour configurer et tester l’authentification unique Azure AD avec Adaptive Suite, vous devez suivre les indications des sections ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="854a8-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="854a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="854a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="854a8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="854a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="854a8-145">**[Création d’un utilisateur de test Adaptive Suite](#creating-an-adaptive-suite-test-user)** pour avoir un équivalent de Britta Simon dans Adaptive Suite lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="854a8-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="854a8-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="854a8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="854a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="854a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="854a8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="854a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="854a8-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="854a8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="854a8-150">**Pour configurer l’authentification unique Azure AD avec Adaptive Suite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="854a8-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="854a8-151">Dans le portail Azure, sur la page d’intégration de l’application **Adaptive Suite**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="854a8-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="854a8-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="854a8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="854a8-155">Dans la section **Domaine et URL Adaptive Suite**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="854a8-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="854a8-157">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="854a8-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="854a8-158">Vous pouvez obtenir cette valeur dans la page **SAML SSO Settings** d’Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="854a8-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="854a8-159">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="854a8-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="854a8-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="854a8-161">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="854a8-163">Dans la section **Configuration d’Adaptive Suite**, cliquez sur **Configurer Adaptive Suite** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="854a8-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="854a8-164">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**</span><span class="sxs-lookup"><span data-stu-id="854a8-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="854a8-166">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Adaptive Suite en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="854a8-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="854a8-167">Accédez à **Admin**.</span><span class="sxs-lookup"><span data-stu-id="854a8-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="854a8-168">![Administrateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="854a8-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="854a8-169">Dans la section **Users and Roles**, cliquez sur **Manage SAML SSO Settings**.</span><span class="sxs-lookup"><span data-stu-id="854a8-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="854a8-170">![Gérer les paramètres d’authentification unique de SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Gérer les paramètres d’authentification unique de SAML")</span><span class="sxs-lookup"><span data-stu-id="854a8-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="854a8-171">Dans la page **SAML SSO Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="854a8-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="854a8-172">![Paramètres d’authentification unique de SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Paramètres d’authentification unique de SAML")</span><span class="sxs-lookup"><span data-stu-id="854a8-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="854a8-173">a.</span><span class="sxs-lookup"><span data-stu-id="854a8-173">a.</span></span> <span data-ttu-id="854a8-174">Dans la zone de texte **Identity provider name** , attribuez un nom à votre configuration.</span><span class="sxs-lookup"><span data-stu-id="854a8-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="854a8-175">b.</span><span class="sxs-lookup"><span data-stu-id="854a8-175">b.</span></span> <span data-ttu-id="854a8-176">Collez la valeur **ID d’entité SAML** copiée à partir du portail Azure dans la zone de texte **ID d’entité du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="854a8-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="854a8-177">c.</span><span class="sxs-lookup"><span data-stu-id="854a8-177">c.</span></span> <span data-ttu-id="854a8-178">Collez la valeur **URL du service d’authentification unique SAML** copiée à partir du portail Azure dans la zone de texte **URL SSO du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="854a8-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="854a8-179">d.</span><span class="sxs-lookup"><span data-stu-id="854a8-179">d.</span></span> <span data-ttu-id="854a8-180">Collez la valeur **URL du service d’authentification unique SAML** copiée à partir du portail Azure dans la zone de texte **Custom logout URL** (URL de connexion personnalisée).</span><span class="sxs-lookup"><span data-stu-id="854a8-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="854a8-181">e.</span><span class="sxs-lookup"><span data-stu-id="854a8-181">e.</span></span> <span data-ttu-id="854a8-182">Pour charger votre certificat téléchargé, cliquez sur **Choisir un fichier**.</span><span class="sxs-lookup"><span data-stu-id="854a8-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="854a8-183">f.</span><span class="sxs-lookup"><span data-stu-id="854a8-183">f.</span></span> <span data-ttu-id="854a8-184">Sélectionnez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="854a8-184">Select the following, for:</span></span>
    * <span data-ttu-id="854a8-185">Pour **SAML user id**, sélectionnez **User’s Adaptive Insights user name**.</span><span class="sxs-lookup"><span data-stu-id="854a8-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="854a8-186">Pour **SAML user id location**, sélectionnez **User id in NameID of Subject**.</span><span class="sxs-lookup"><span data-stu-id="854a8-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="854a8-187">Pour **SAML NameID format**, sélectionnez **Email address**.</span><span class="sxs-lookup"><span data-stu-id="854a8-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="854a8-188">Pour **Enable SAML**, sélectionnez **Allow SAML SSO and direct Adaptive Insights login**.</span><span class="sxs-lookup"><span data-stu-id="854a8-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="854a8-189">g.</span><span class="sxs-lookup"><span data-stu-id="854a8-189">g.</span></span> <span data-ttu-id="854a8-190">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="854a8-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="854a8-191">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="854a8-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="854a8-192">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="854a8-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="854a8-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="854a8-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="854a8-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="854a8-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="854a8-195">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="854a8-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="854a8-197">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="854a8-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="854a8-198">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="854a8-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="854a8-200">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="854a8-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="854a8-202">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="854a8-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="854a8-204">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="854a8-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="854a8-206">a.</span><span class="sxs-lookup"><span data-stu-id="854a8-206">a.</span></span> <span data-ttu-id="854a8-207">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="854a8-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="854a8-208">b.</span><span class="sxs-lookup"><span data-stu-id="854a8-208">b.</span></span> <span data-ttu-id="854a8-209">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="854a8-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="854a8-210">c.</span><span class="sxs-lookup"><span data-stu-id="854a8-210">c.</span></span> <span data-ttu-id="854a8-211">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="854a8-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="854a8-212">d.</span><span class="sxs-lookup"><span data-stu-id="854a8-212">d.</span></span> <span data-ttu-id="854a8-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="854a8-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="854a8-214">Création d’un utilisateur de test Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="854a8-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="854a8-215">Pour permettre aux utilisateurs Azure AD de se connecter à Adaptive Suite, vous devez les approvisionner dans Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="854a8-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="854a8-216">Dans le cas d’Adaptive Suite, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="854a8-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="854a8-217">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="854a8-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="854a8-218">Connectez-vous à votre site d’entreprise **Adaptive Suite** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="854a8-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="854a8-219">Accédez à **Admin**.</span><span class="sxs-lookup"><span data-stu-id="854a8-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="854a8-220">![Administrateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="854a8-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="854a8-221">Dans la section **Users and Roles**, cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="854a8-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="854a8-222">![Ajouter un utilisateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="854a8-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="854a8-223">Dans la section **New User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="854a8-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="854a8-224">![Envoyer](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Envoyer")</span><span class="sxs-lookup"><span data-stu-id="854a8-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="854a8-225">a.</span><span class="sxs-lookup"><span data-stu-id="854a8-225">a.</span></span> <span data-ttu-id="854a8-226">Tapez le nom, l’identifiant de connexion, l’adresse de messagerie et le mot de passe de l’utilisateur Azure Active Directory valide que vous souhaitez renseigner dans les zones de texte correspondantes, à savoir, **Name**, **Login**, **Email** et **Password**.</span><span class="sxs-lookup"><span data-stu-id="854a8-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="854a8-227">b.</span><span class="sxs-lookup"><span data-stu-id="854a8-227">b.</span></span> <span data-ttu-id="854a8-228">Sélectionnez un **rôle**.</span><span class="sxs-lookup"><span data-stu-id="854a8-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="854a8-229">c.</span><span class="sxs-lookup"><span data-stu-id="854a8-229">c.</span></span> <span data-ttu-id="854a8-230">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="854a8-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="854a8-231">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur Adaptive Suite fourni par ce service pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="854a8-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="854a8-232">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="854a8-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="854a8-233">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="854a8-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="854a8-235">**Pour assigner Britta Simon à Adaptive Suite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="854a8-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="854a8-236">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="854a8-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="854a8-238">Dans la liste des applications, sélectionnez **Adaptive Suite**.</span><span class="sxs-lookup"><span data-stu-id="854a8-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="854a8-240">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="854a8-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="854a8-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="854a8-242">Click **Add** button.</span></span> <span data-ttu-id="854a8-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="854a8-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="854a8-245">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="854a8-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="854a8-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="854a8-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="854a8-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="854a8-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="854a8-248">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="854a8-248">Testing single sign-on</span></span>

<span data-ttu-id="854a8-249">L’objectif de cette section est de tester la configuration de l’authentification unique Microsoft Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="854a8-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="854a8-250">Lorsque vous cliquez sur la vignette Adaptive Suite dans le panneau d’accès, vous devez être connecté automatiquement à votre application Adaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="854a8-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="854a8-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="854a8-251">Additional resources</span></span>

* [<span data-ttu-id="854a8-252">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="854a8-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="854a8-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="854a8-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

