---
title: "Didacticiel : Intégration d’Azure Active Directory avec Jobscience | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="00fe1-103">Didacticiel : Intégration d’Azure Active Directory à Jobscience</span><span class="sxs-lookup"><span data-stu-id="00fe1-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="00fe1-104">Dans ce didacticiel, vous allez apprendre à intégrer Jobscience à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="00fe1-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00fe1-105">L’intégration de Jobscience dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="00fe1-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="00fe1-106">Dans Azure AD, vous pouvez contrôler qui a accès à Jobscience.</span><span class="sxs-lookup"><span data-stu-id="00fe1-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="00fe1-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Jobscience (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fe1-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="00fe1-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="00fe1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="00fe1-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00fe1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00fe1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="00fe1-110">Prerequisites</span></span>

<span data-ttu-id="00fe1-111">Pour configurer l’intégration d’Azure AD avec Jobscience, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="00fe1-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="00fe1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fe1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00fe1-113">Un abonnement Jobscience pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="00fe1-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00fe1-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="00fe1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00fe1-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="00fe1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00fe1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="00fe1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00fe1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00fe1-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00fe1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="00fe1-118">Scenario description</span></span>
<span data-ttu-id="00fe1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="00fe1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00fe1-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="00fe1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00fe1-121">Ajout de Jobscience à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="00fe1-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="00fe1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fe1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="00fe1-123">Ajout de Jobscience à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="00fe1-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="00fe1-124">Pour configurer l’intégration de Jobscience à Azure AD, vous devez ajouter Jobscience à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="00fe1-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="00fe1-125">**Pour ajouter Jobscience à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="00fe1-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="00fe1-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="00fe1-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="00fe1-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="00fe1-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="00fe1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="00fe1-133">Dans la zone de recherche, entrez **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-133">In the search box, type **Jobscience**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="00fe1-135">Dans le volet de résultats, sélectionnez **Jobscience**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="00fe1-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="00fe1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fe1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="00fe1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Jobscience avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="00fe1-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="00fe1-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Jobscience équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fe1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="00fe1-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Jobscience associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="00fe1-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="00fe1-141">Dans Jobscience, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="00fe1-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="00fe1-142">Pour configurer et tester l’authentification unique Azure AD avec Jobscience, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="00fe1-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="00fe1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="00fe1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="00fe1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00fe1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00fe1-145">**[Création d’un utilisateur de test Jobscience](#creating-a-jobscience-test-user)** pour avoir un équivalent de Britta Simon dans Jobscience lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="00fe1-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="00fe1-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fe1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00fe1-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="00fe1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="00fe1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fe1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="00fe1-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Jobscience.</span><span class="sxs-lookup"><span data-stu-id="00fe1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="00fe1-150">**Pour configurer l’authentification unique Azure AD avec Jobscience, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="00fe1-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="00fe1-151">Dans le portail Azure, sur la page d’intégration de l’application **Jobscience**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="00fe1-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="00fe1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="00fe1-155">Dans la section **Domaine et URL Jobscience**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="00fe1-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="00fe1-157">Dans la zone de texte **URL d’authentification**, tapez une URL en utilisant le modèle suivant : `http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="00fe1-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="00fe1-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="00fe1-158">This value is not real.</span></span> <span data-ttu-id="00fe1-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="00fe1-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="00fe1-160">Obtenez cette valeur auprès de l’[équipe de support Client Jobscience](https://www.jobscience.com/support) ou à partir du profil d’authentification unique que vous allez créer, qui est expliqué plus loin dans le tutoriel.</span><span class="sxs-lookup"><span data-stu-id="00fe1-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="00fe1-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="00fe1-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="00fe1-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="00fe1-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="00fe1-165">Dans la section **Configuration de Jobscience**, cliquez sur **Configurer Jobscience** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="00fe1-166">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="00fe1-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="00fe1-168">Connectez-vous au site d’entreprise Jobscience en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="00fe1-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="00fe1-169">Accédez à **Setup**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="00fe1-170">![Configuration](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="00fe1-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="00fe1-171">Dans le volet de navigation gauche, dans la section **Administer**, cliquez sur **Domain Management** pour développer la section associée, puis cliquez sur **My Domain** pour ouvrir la page **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="00fe1-172">![Mon domaine](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="00fe1-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="00fe1-173">Pour vérifier que votre domaine a été configuré correctement, assurez-vous qu’il figure dans **Step 4 Deployed to Users**, puis passez en revue **My Domain Settings**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="00fe1-174">![Domaine déployé sur l’utilisateur](./media/active-directory-saas-jobscience-tutorial/ic784377.png "domaine déployé sur l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="00fe1-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="00fe1-175">Sur le site d’entreprise Jobscience, cliquez sur **Security Controls**, puis sur **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="00fe1-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="00fe1-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="00fe1-177">Dans la section **Single Sign-On Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="00fe1-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="00fe1-178">![Paramètres d’authentification unique](./media/active-directory-saas-jobscience-tutorial/ic781026.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="00fe1-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="00fe1-179">a.</span><span class="sxs-lookup"><span data-stu-id="00fe1-179">a.</span></span> <span data-ttu-id="00fe1-180">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="00fe1-181">b.</span><span class="sxs-lookup"><span data-stu-id="00fe1-181">b.</span></span> <span data-ttu-id="00fe1-182">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-182">Click **New**.</span></span>

13. <span data-ttu-id="00fe1-183">Dans la boîte de dialogue **SAML Single Sign-On Setting Edit** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="00fe1-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="00fe1-184">![Configuration de l’authentification unique SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Configuration de l’authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="00fe1-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="00fe1-185">a.</span><span class="sxs-lookup"><span data-stu-id="00fe1-185">a.</span></span> <span data-ttu-id="00fe1-186">Dans la zone de texte **Name** , tapez le nom de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="00fe1-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="00fe1-187">b.</span><span class="sxs-lookup"><span data-stu-id="00fe1-187">b.</span></span> <span data-ttu-id="00fe1-188">Dans la zone de texte **Issuer (Émetteur)**, collez la valeur de **l’ID d’entité SAML** que vous avez copiée depuis le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="00fe1-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="00fe1-189">c.</span><span class="sxs-lookup"><span data-stu-id="00fe1-189">c.</span></span> <span data-ttu-id="00fe1-190">Dans la zone de texte **Entity ID** (ID identité), tapez `https://salesforce-jobscience.com`.</span><span class="sxs-lookup"><span data-stu-id="00fe1-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="00fe1-191">d.</span><span class="sxs-lookup"><span data-stu-id="00fe1-191">d.</span></span> <span data-ttu-id="00fe1-192">Cliquez sur **Parcourir** pour charger votre certificat Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fe1-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="00fe1-193">e.</span><span class="sxs-lookup"><span data-stu-id="00fe1-193">e.</span></span> <span data-ttu-id="00fe1-194">Pour **SAML Identity Type (Type d’identité SAML)**, sélectionnez **Assertion contains the Federation ID from the User object (L’assertion contient l’ID de fédération de l’objet utilisateur)**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="00fe1-195">f.</span><span class="sxs-lookup"><span data-stu-id="00fe1-195">f.</span></span> <span data-ttu-id="00fe1-196">Pour **SAML Identity Location**, sélectionnez **Identity is in the NameIdentfier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="00fe1-197">g.</span><span class="sxs-lookup"><span data-stu-id="00fe1-197">g.</span></span> <span data-ttu-id="00fe1-198">Dans la zone de texte **Identity Provider Login URL (URL de connexion du fournisseur d’identité)**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="00fe1-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="00fe1-199">h.</span><span class="sxs-lookup"><span data-stu-id="00fe1-199">h.</span></span> <span data-ttu-id="00fe1-200">Dans la zone de texte **Identity Provider Logout URL (URL de déconnexion du fournisseur d’identité)**, collez la valeur **URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="00fe1-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="00fe1-201">i.</span><span class="sxs-lookup"><span data-stu-id="00fe1-201">i.</span></span> <span data-ttu-id="00fe1-202">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-202">Click **Save**.</span></span>

14. <span data-ttu-id="00fe1-203">Dans le volet de navigation gauche, dans la section **Administer**, cliquez sur **Domain Management** pour développer la section associée, puis cliquez sur **My Domain** pour ouvrir la page **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="00fe1-204">![Mon domaine](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="00fe1-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="00fe1-205">Dans la section **Login Page Branding** de la page **My Domain**, cliquez sur **Edit**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="00fe1-206">![Personnalisation de la page de connexion](./media/active-directory-saas-jobscience-tutorial/ic767826.png "personnalisation de la page de connexion")</span><span class="sxs-lookup"><span data-stu-id="00fe1-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="00fe1-207">Le nom des **SAML SSO Settings** s’affiche dans la section **Authentication Service** de la page **Login Page Branding**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="00fe1-208">Sélectionnez-le, puis cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="00fe1-209">![Personnalisation de la page de connexion](./media/active-directory-saas-jobscience-tutorial/ic784366.png "personnalisation de la page de connexion")</span><span class="sxs-lookup"><span data-stu-id="00fe1-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="00fe1-210">Pour obtenir l’URL d’authentification unique initiée par le fournisseur de services , cliquez sur **Single Sign On settings** dans la section **Security Controls**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="00fe1-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="00fe1-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="00fe1-212">Cliquez sur le profil d’authentification unique créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="00fe1-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="00fe1-213">Cette page affiche l’URL d’authentification unique de votre société (par exemple, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid)).</span><span class="sxs-lookup"><span data-stu-id="00fe1-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="00fe1-214">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="00fe1-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="00fe1-215">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="00fe1-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="00fe1-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="00fe1-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="00fe1-217">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fe1-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="00fe1-218">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="00fe1-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="00fe1-220">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="00fe1-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="00fe1-221">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00fe1-223">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00fe1-225">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="00fe1-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00fe1-227">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="00fe1-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="00fe1-229">a.</span><span class="sxs-lookup"><span data-stu-id="00fe1-229">a.</span></span> <span data-ttu-id="00fe1-230">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00fe1-231">b.</span><span class="sxs-lookup"><span data-stu-id="00fe1-231">b.</span></span> <span data-ttu-id="00fe1-232">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00fe1-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="00fe1-233">c.</span><span class="sxs-lookup"><span data-stu-id="00fe1-233">c.</span></span> <span data-ttu-id="00fe1-234">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="00fe1-235">d.</span><span class="sxs-lookup"><span data-stu-id="00fe1-235">d.</span></span> <span data-ttu-id="00fe1-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="00fe1-237">Création d’un utilisateur de test Jobscience</span><span class="sxs-lookup"><span data-stu-id="00fe1-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="00fe1-238">Pour permettre aux utilisateurs Azure AD de se connecter à Jobscience, vous devez les approvisionner dans Jobscience.</span><span class="sxs-lookup"><span data-stu-id="00fe1-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="00fe1-239">Dans le cas de Jobscience, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="00fe1-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="00fe1-240">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte utilisateur fournis par Jobscience pour approvisionner des comptes utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="00fe1-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="00fe1-241">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="00fe1-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="00fe1-242">Connectez-vous au site d’entreprise **Jobscience** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="00fe1-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="00fe1-243">Accédez à Setup.</span><span class="sxs-lookup"><span data-stu-id="00fe1-243">Go to Setup.</span></span>
   
   <span data-ttu-id="00fe1-244">![Configuration](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="00fe1-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="00fe1-245">Accédez à **Manage Users \> Users**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="00fe1-246">![Utilisateurs](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="00fe1-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="00fe1-247">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-247">Click **New User**.</span></span>
   
   <span data-ttu-id="00fe1-248">![Tous les utilisateurs](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Tous les utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="00fe1-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="00fe1-249">Dans la boîte de dialogue **Edit User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="00fe1-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="00fe1-250">![Modification de l’utilisateur](./media/active-directory-saas-jobscience-tutorial/ic784371.png "modification de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="00fe1-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="00fe1-251">a.</span><span class="sxs-lookup"><span data-stu-id="00fe1-251">a.</span></span> <span data-ttu-id="00fe1-252">Dans la zone de texte **Prénom**, entrez le prénom de l’utilisateur, par exemple Britta.</span><span class="sxs-lookup"><span data-stu-id="00fe1-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="00fe1-253">b.</span><span class="sxs-lookup"><span data-stu-id="00fe1-253">b.</span></span> <span data-ttu-id="00fe1-254">Dans la zone de texte **Nom**, entrez le nom de l’utilisateur, par exemple Simon.</span><span class="sxs-lookup"><span data-stu-id="00fe1-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="00fe1-255">c.</span><span class="sxs-lookup"><span data-stu-id="00fe1-255">c.</span></span> <span data-ttu-id="00fe1-256">Dans la zone de texte **Alias**, entrez le nom d’alias de l’utilisateur, par exemple Britta.</span><span class="sxs-lookup"><span data-stu-id="00fe1-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="00fe1-257">d.</span><span class="sxs-lookup"><span data-stu-id="00fe1-257">d.</span></span> <span data-ttu-id="00fe1-258">Dans la zone de texte **Email** (E-mail), tapez l’adresse e-mail d’un utilisateur, par exemple, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="00fe1-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="00fe1-259">e.</span><span class="sxs-lookup"><span data-stu-id="00fe1-259">e.</span></span> <span data-ttu-id="00fe1-260">Dans la zone de texte **Nom d’utilisateur**, entrez le nom de l’utilisateur, par exemple Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="00fe1-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="00fe1-261">f.</span><span class="sxs-lookup"><span data-stu-id="00fe1-261">f.</span></span> <span data-ttu-id="00fe1-262">Dans la zone de texte **Surnom**, entrez le surnom, par exemple Simon.</span><span class="sxs-lookup"><span data-stu-id="00fe1-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="00fe1-263">g.</span><span class="sxs-lookup"><span data-stu-id="00fe1-263">g.</span></span> <span data-ttu-id="00fe1-264">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="00fe1-265">Le titulaire du compte Azure Active Directory reçoit un e-mail contenant un lien à suivre pour confirmer son compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="00fe1-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="00fe1-266">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fe1-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="00fe1-267">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Jobscience.</span><span class="sxs-lookup"><span data-stu-id="00fe1-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="00fe1-269">**Pour affecter Britta Simon à Jobscience, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="00fe1-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="00fe1-270">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="00fe1-272">Dans la liste des applications, sélectionnez **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-272">In the applications list, select **Jobscience**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="00fe1-274">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="00fe1-276">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-276">Click **Add** button.</span></span> <span data-ttu-id="00fe1-277">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="00fe1-279">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="00fe1-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="00fe1-280">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00fe1-281">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="00fe1-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="00fe1-282">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="00fe1-282">Testing single sign-on</span></span>

<span data-ttu-id="00fe1-283">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="00fe1-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="00fe1-284">Si vous cliquez sur la mosaïque Jobscience dans le volet d’accès, vous devez vous connecter automatiquement à votre application Jobscience.</span><span class="sxs-lookup"><span data-stu-id="00fe1-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="00fe1-285">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00fe1-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="00fe1-286">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="00fe1-286">Additional resources</span></span>

* [<span data-ttu-id="00fe1-287">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00fe1-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00fe1-288">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="00fe1-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

