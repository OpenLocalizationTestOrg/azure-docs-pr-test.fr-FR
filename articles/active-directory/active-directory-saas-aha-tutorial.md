---
title: "Didacticiel : Intégration d’Azure Active Directory à Aha! | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="eb50c-104">Didacticiel : Intégration d’Azure Active Directory à Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="eb50c-105">Dans ce didacticiel, vous allez apprendre à intégrer Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="eb50c-106">à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb50c-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb50c-107">L’intégration d’Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-107">Integrating Aha!</span></span> <span data-ttu-id="eb50c-108">à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="eb50c-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eb50c-109">Dans Azure AD, vous pouvez contrôler qui a accès à Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="eb50c-110">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="eb50c-111">(par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb50c-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb50c-112">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="eb50c-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="eb50c-113">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb50c-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb50c-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="eb50c-114">Prerequisites</span></span>

<span data-ttu-id="eb50c-115">Pour configurer l’intégration d’Azure AD à Aha!, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb50c-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="eb50c-116">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb50c-116">An Azure AD subscription</span></span>
- <span data-ttu-id="eb50c-117">Un abonnement Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-117">An Aha!</span></span> <span data-ttu-id="eb50c-118">Un abonnement pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="eb50c-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb50c-119">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="eb50c-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb50c-120">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="eb50c-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb50c-121">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eb50c-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb50c-122">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb50c-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb50c-123">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="eb50c-123">Scenario description</span></span>
<span data-ttu-id="eb50c-124">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="eb50c-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb50c-125">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="eb50c-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb50c-126">Ajout d’Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-126">Adding Aha!</span></span> <span data-ttu-id="eb50c-127">à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="eb50c-127">from the gallery</span></span>
2. <span data-ttu-id="eb50c-128">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb50c-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="eb50c-129">Ajout d’Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-129">Adding Aha!</span></span> <span data-ttu-id="eb50c-130">à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="eb50c-130">from the gallery</span></span>
<span data-ttu-id="eb50c-131">Pour configurer l’intégration d’Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-131">To configure the integration of Aha!</span></span> <span data-ttu-id="eb50c-132">à Azure AD, vous devez ajouter Aha! depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="eb50c-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="eb50c-133">à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="eb50c-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eb50c-134">**Pour ajouter Aha! à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb50c-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eb50c-135">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb50c-137">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eb50c-138">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-138">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="eb50c-140">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="eb50c-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="eb50c-142">Dans la zone de recherche, tapez **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-142">In the search box, type **Aha!**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="eb50c-144">Dans le volet de résultats, sélectionnez **Aha!**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="eb50c-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb50c-146">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb50c-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb50c-147">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="eb50c-148">au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="eb50c-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eb50c-149">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Aha! équivalent</span><span class="sxs-lookup"><span data-stu-id="eb50c-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="eb50c-150">dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb50c-150">is to a user in Azure AD.</span></span> <span data-ttu-id="eb50c-151">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Aha! associé</span><span class="sxs-lookup"><span data-stu-id="eb50c-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="eb50c-152">doit être établie.</span><span class="sxs-lookup"><span data-stu-id="eb50c-152">needs to be established.</span></span>

<span data-ttu-id="eb50c-153">Dans Aha!, affectez la valeur du **nom d’utilisateur** indiquée dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="eb50c-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eb50c-154">Pour configurer et tester l’authentification unique Azure AD avec Aha!, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="eb50c-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eb50c-155">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="eb50c-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eb50c-156">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb50c-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb50c-157">**[Création d’un utilisateur de test Aha!](#creating-an-aha-test-user)**  pour avoir dans Aha! un équivalent de Britta Simon</span><span class="sxs-lookup"><span data-stu-id="eb50c-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="eb50c-158">lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eb50c-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb50c-159">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb50c-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb50c-160">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="eb50c-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb50c-161">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb50c-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb50c-162">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre</span><span class="sxs-lookup"><span data-stu-id="eb50c-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="eb50c-163">application Aha!.</span><span class="sxs-lookup"><span data-stu-id="eb50c-163">application.</span></span>

<span data-ttu-id="eb50c-164">**Pour configurer l’authentification unique Azure AD avec Aha!, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb50c-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="eb50c-165">Dans le portail Azure, sur la page d’intégration de l’application **Aha!**,</span><span class="sxs-lookup"><span data-stu-id="eb50c-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="eb50c-166">cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-166">application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="eb50c-168">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb50c-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="eb50c-170">Dans la section **Domaine et URL Aha!** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb50c-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="eb50c-172">a.</span><span class="sxs-lookup"><span data-stu-id="eb50c-172">a.</span></span> <span data-ttu-id="eb50c-173">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="eb50c-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="eb50c-174">b.</span><span class="sxs-lookup"><span data-stu-id="eb50c-174">b.</span></span> <span data-ttu-id="eb50c-175">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="eb50c-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eb50c-176">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="eb50c-176">These values are not real.</span></span> <span data-ttu-id="eb50c-177">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="eb50c-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eb50c-178">Pour obtenir ces valeurs, contactez [ l’équipe du support technique d’Aha!](https://www.aha.io/company/contact).</span><span class="sxs-lookup"><span data-stu-id="eb50c-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="eb50c-179">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eb50c-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="eb50c-181">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="eb50c-181">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb50c-183">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="eb50c-184">en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="eb50c-184">company site as an administrator.</span></span>

7. <span data-ttu-id="eb50c-185">Dans le menu situé en haut, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="eb50c-186">![Paramètres](./media/active-directory-saas-aha-tutorial/IC798950.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="eb50c-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="eb50c-187">Cliquez sur **Account**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-187">Click **Account**.</span></span>
   
    <span data-ttu-id="eb50c-188">![Profil](./media/active-directory-saas-aha-tutorial/IC798951.png "Profil")</span><span class="sxs-lookup"><span data-stu-id="eb50c-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="eb50c-189">Cliquez sur **Security and single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="eb50c-190">![Sécurité et authentification unique](./media/active-directory-saas-aha-tutorial/IC798952.png "Sécurité et authentification unique")</span><span class="sxs-lookup"><span data-stu-id="eb50c-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="eb50c-191">Dans la section **Single Sign-On**, pour **Identity Provider**, sélectionnez **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="eb50c-192">![Sécurité et authentification unique](./media/active-directory-saas-aha-tutorial/IC798953.png "Sécurité et authentification unique")</span><span class="sxs-lookup"><span data-stu-id="eb50c-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="eb50c-193">Dans la page de configuration **Single Sign on** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb50c-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="eb50c-194">![Authentification unique](./media/active-directory-saas-aha-tutorial/IC798954.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="eb50c-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="eb50c-195">a.</span><span class="sxs-lookup"><span data-stu-id="eb50c-195">a.</span></span> <span data-ttu-id="eb50c-196">Dans la zone de texte **Name** , tapez le nom de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="eb50c-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="eb50c-197">b.</span><span class="sxs-lookup"><span data-stu-id="eb50c-197">b.</span></span> <span data-ttu-id="eb50c-198">Pour **Configure using**, sélectionnez **Metadata File**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="eb50c-199">c.</span><span class="sxs-lookup"><span data-stu-id="eb50c-199">c.</span></span> <span data-ttu-id="eb50c-200">Pour charger le fichier de métadonnées téléchargé, cliquez sur **Browse**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="eb50c-201">d.</span><span class="sxs-lookup"><span data-stu-id="eb50c-201">d.</span></span> <span data-ttu-id="eb50c-202">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="eb50c-203">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="eb50c-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eb50c-204">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="eb50c-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eb50c-205">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb50c-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb50c-206">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb50c-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb50c-207">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="eb50c-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="eb50c-209">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb50c-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eb50c-210">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb50c-212">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb50c-214">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="eb50c-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb50c-216">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb50c-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb50c-218">a.</span><span class="sxs-lookup"><span data-stu-id="eb50c-218">a.</span></span> <span data-ttu-id="eb50c-219">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb50c-220">b.</span><span class="sxs-lookup"><span data-stu-id="eb50c-220">b.</span></span> <span data-ttu-id="eb50c-221">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb50c-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb50c-222">c.</span><span class="sxs-lookup"><span data-stu-id="eb50c-222">c.</span></span> <span data-ttu-id="eb50c-223">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="eb50c-224">d.</span><span class="sxs-lookup"><span data-stu-id="eb50c-224">d.</span></span> <span data-ttu-id="eb50c-225">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="eb50c-226">Création</span><span class="sxs-lookup"><span data-stu-id="eb50c-226">Creating an Aha!</span></span> <span data-ttu-id="eb50c-227">d’un utilisateur de test Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-227">test user</span></span>

<span data-ttu-id="eb50c-228">Pour se connecter à Aha!, les utilisateurs d’Azure AD doivent être approvisionnés dans Aha!.</span><span class="sxs-lookup"><span data-stu-id="eb50c-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="eb50c-229">Dans le cas d’Aha!, l’approvisionnement est une tâche automatisée.</span><span class="sxs-lookup"><span data-stu-id="eb50c-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="eb50c-230">Vous n’avez aucune opération à effectuer.</span><span class="sxs-lookup"><span data-stu-id="eb50c-230">There is no action item for you.</span></span>

<span data-ttu-id="eb50c-231">Au besoin, les utilisateurs sont automatiquement créés lors de la première tentative d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb50c-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="eb50c-232">Vous pouvez utiliser n’importe quel autre outil de création de</span><span class="sxs-lookup"><span data-stu-id="eb50c-232">You can use any other Aha!</span></span> <span data-ttu-id="eb50c-233">compte utilisateur Aha! ou toute API fournie par Aha!</span><span class="sxs-lookup"><span data-stu-id="eb50c-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="eb50c-234">pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="eb50c-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="eb50c-235">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb50c-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="eb50c-236">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à Aha!.</span><span class="sxs-lookup"><span data-stu-id="eb50c-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="eb50c-238">**Pour affecter Britta Simon à Aha!, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb50c-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="eb50c-239">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="eb50c-241">Dans la liste des applications, sélectionnez **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-241">In the applications list, select **Aha!**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="eb50c-243">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="eb50c-245">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-245">Click **Add** button.</span></span> <span data-ttu-id="eb50c-246">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="eb50c-248">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="eb50c-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eb50c-249">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb50c-250">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eb50c-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb50c-251">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="eb50c-251">Testing single sign-on</span></span>

<span data-ttu-id="eb50c-252">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="eb50c-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="eb50c-253">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb50c-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb50c-254">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="eb50c-254">Additional resources</span></span>

* [<span data-ttu-id="eb50c-255">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb50c-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb50c-256">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="eb50c-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

