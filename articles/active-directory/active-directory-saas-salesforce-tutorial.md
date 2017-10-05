---
title: "Didacticiel : Intégration d’Azure Active Directory à Salesforce | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="7ebb5-103">Didacticiel : Intégration d’Azure Active Directory à Salesforce</span><span class="sxs-lookup"><span data-stu-id="7ebb5-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="7ebb5-104">Dans ce didacticiel, vous allez apprendre à intégrer Salesforce à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ebb5-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ebb5-105">L’intégration de Salesforce dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ebb5-106">Dans Azure AD, vous pouvez contrôler qui a accès à Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="7ebb5-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Salesforce (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ebb5-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ebb5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7ebb5-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ebb5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ebb5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7ebb5-110">Prerequisites</span></span>

<span data-ttu-id="7ebb5-111">Pour configurer l’intégration d’Azure AD à Salesforce, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="7ebb5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebb5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ebb5-113">Un abonnement Salesforce pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7ebb5-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ebb5-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ebb5-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ebb5-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ebb5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ebb5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ebb5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7ebb5-118">Scenario description</span></span>
<span data-ttu-id="7ebb5-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ebb5-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ebb5-121">Ajout de Salesforce à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7ebb5-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="7ebb5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebb5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="7ebb5-123">Ajout de Salesforce à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7ebb5-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="7ebb5-124">Pour configurer l’intégration de Salesforce avec Azure AD, vous devez ajouter Salesforce à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ebb5-125">**Pour ajouter Salesforce à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ebb5-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ebb5-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ebb5-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ebb5-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7ebb5-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7ebb5-133">Dans la zone de recherche, tapez **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-133">In the search box, type **Salesforce**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="7ebb5-135">Dans le volet de résultats, sélectionnez **Salesforce**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ebb5-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebb5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ebb5-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Salesforce, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7ebb5-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7ebb5-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Salesforce correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="7ebb5-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Salesforce associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="7ebb5-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="7ebb5-142">Pour configurer et tester l’authentification unique Azure AD avec Salesforce, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ebb5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ebb5-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ebb5-145">**[Création d’un utilisateur de test Salesforce](#creating-a-salesforce-test-user)** pour avoir un équivalent de Britta Simon dans Salesforce lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ebb5-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ebb5-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ebb5-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebb5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ebb5-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="7ebb5-150">**Pour configurer l’authentification unique Azure AD avec Salesforce, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ebb5-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="7ebb5-151">Dans le portail Azure, sur la page d’intégration de l’application **Salesforce**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7ebb5-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="7ebb5-155">Dans la section **Domaine et URL Salesforce**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="7ebb5-157">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="7ebb5-158">Compte d’entreprise : `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7ebb5-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="7ebb5-159">Compte de développeur : `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7ebb5-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ebb5-160">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-160">These values are not the real.</span></span> <span data-ttu-id="7ebb5-161">Mettez à jour ces valeurs avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="7ebb5-162">Pour obtenir ces valeurs, contactez l’[équipe de support technique Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="7ebb5-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="7ebb5-163">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="7ebb5-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7ebb5-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7ebb5-167">Dans la section **Configuration de Salesforce** , cliquez sur **Configurer Salesforce** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ebb5-168">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="7ebb5-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="7ebb5-169">![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="7ebb5-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="7ebb5-170">Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à votre compte d’administrateur Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="7ebb5-171">Sous le volet de navigation **Administrateur**, cliquez sur **Contrôles de sécurité** pour développer la section associée.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="7ebb5-172">Puis cliquez sur **Paramètres de l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-172">Then click **Single Sign-On Settings**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="7ebb5-174">Sur la page **Paramètres de l’authentification unique**, cliquez sur le bouton **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="7ebb5-175">![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="7ebb5-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="7ebb5-176">Si vous ne pouvez pas activer les paramètres de l’authentification unique pour votre compte Salesforce, il vous faudra peut-être contacter [l’équipe du support technique de Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="7ebb5-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="7ebb5-177">Sélectionnez **SAML activé**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="7ebb5-179">Pour configurer vos paramètres d’authentification unique SAML, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="7ebb5-181">Sur la page **Modifier les paramètres d’authentification unique SAML** , procédez à la configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="7ebb5-183">a.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-183">a.</span></span> <span data-ttu-id="7ebb5-184">Dans le champ **Nom** , entrez un nom convivial pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="7ebb5-185">Le fait d’entrer une valeur pour **Nom** entraîne le remplissage automatique de la zone de texte **Nom API**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="7ebb5-186">b.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-186">b.</span></span> <span data-ttu-id="7ebb5-187">Collez la valeur **ID d’entité SAML** dans le champ **Émetteur** de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="7ebb5-188">c.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-188">c.</span></span> <span data-ttu-id="7ebb5-189">Dans la zone de texte **ID d’entité**, tapez votre nom de domaine Salesforce en suivant ce modèle :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="7ebb5-190">Compte d’entreprise : `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7ebb5-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="7ebb5-191">Compte de développeur : `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7ebb5-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="7ebb5-192">d.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-192">d.</span></span> <span data-ttu-id="7ebb5-193">Cliquez sur **Parcourir** ou **Choisir un fichier** pour ouvrir la boîte de dialogue **Choisir un fichier à télécharger**, sélectionnez votre certificat Salesforce, puis cliquez sur **Ouvrir** pour télécharger le certificat.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="7ebb5-194">e.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-194">e.</span></span> <span data-ttu-id="7ebb5-195">Pour **Type d’identité SAML**, sélectionnez **L’assertion contient le nom d’utilisateur de l’utilisateur salesforce.com**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="7ebb5-196">f.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-196">f.</span></span> <span data-ttu-id="7ebb5-197">Pour **Emplacement de l’identité SAML**, sélectionnez **L’identité est dans l’élément NameIdentifier de l’instruction Subject**</span><span class="sxs-lookup"><span data-stu-id="7ebb5-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="7ebb5-198">g.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-198">g.</span></span> <span data-ttu-id="7ebb5-199">Collez **l’URL du service d’authentification unique** dans le champ **URL de connexion au fournisseur d’identité** de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="7ebb5-200">h.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-200">h.</span></span> <span data-ttu-id="7ebb5-201">Pour **Liaison de demande initiée par le fournisseur de service**, sélectionnez **Redirection HTTP**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="7ebb5-202">i.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-202">i.</span></span> <span data-ttu-id="7ebb5-203">Enfin, cliquez sur **Enregistrer** pour appliquer vos paramètres d’authentification unique SAML.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="7ebb5-204">Dans le volet de navigation de gauche de Salesforce, cliquez sur **Gestion de domaine** pour développer la section associée, puis cliquez sur **Mon domaine**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="7ebb5-206">Faites défiler le contenu de la fenêtre jusqu’à la section **Configuration de l’authentification**, puis cliquez sur le bouton **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="7ebb5-208">Dans la section **Service d’authentification**, sélectionnez le nom convivial de votre configuration d’authentification unique SAML, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="7ebb5-210">Si plusieurs services d’authentification sont sélectionnés, les utilisateurs sont invités à choisir le service d’authentification qu’ils préfèrent utiliser pour se connecter lors de l’initialisation d’une authentification unique sur votre environnement Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="7ebb5-211">Si vous ne voulez pas que cela se produise, vous devez **décocher toutes les cases en regard des autres services d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="7ebb5-212">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ebb5-213">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée via la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ebb5-214">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ebb5-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ebb5-215">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebb5-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ebb5-216">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7ebb5-218">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ebb5-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ebb5-219">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ebb5-221">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ebb5-223">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ebb5-225">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ebb5-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ebb5-227">a.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-227">a.</span></span> <span data-ttu-id="7ebb5-228">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ebb5-229">b.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-229">b.</span></span> <span data-ttu-id="7ebb5-230">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ebb5-231">c.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-231">c.</span></span> <span data-ttu-id="7ebb5-232">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7ebb5-233">d.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-233">d.</span></span> <span data-ttu-id="7ebb5-234">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="7ebb5-235">Création d’un utilisateur de test Salesforce</span><span class="sxs-lookup"><span data-stu-id="7ebb5-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="7ebb5-236">Dans cette section, un utilisateur appelé Britta Simon est créé dans Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="7ebb5-237">Salesforce prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="7ebb5-238">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-238">There is no action item for you in this section.</span></span> <span data-ttu-id="7ebb5-239">Si un utilisateur n’existe pas dans Salesforce, un nouveau est créé lorsque vous tentez d’accéder à Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7ebb5-240">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ebb5-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7ebb5-241">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7ebb5-243">**Pour affecter Britta Simon à Salesforce, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ebb5-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="7ebb5-244">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7ebb5-246">Dans la liste des applications, sélectionnez **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-246">In the applications list, select **Salesforce**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="7ebb5-248">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7ebb5-250">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-250">Click **Add** button.</span></span> <span data-ttu-id="7ebb5-251">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7ebb5-253">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7ebb5-254">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ebb5-255">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ebb5-256">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7ebb5-256">Testing single sign-on</span></span>

<span data-ttu-id="7ebb5-257">Pour tester vos paramètres d’authentification unique, ouvrez le volet d’accès à l’adresse [https://myapps.microsoft.com](https://myapps.microsoft.com/), puis connectez-vous au compte de test et cliquez sur **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="7ebb5-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ebb5-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7ebb5-258">Additional resources</span></span>

* [<span data-ttu-id="7ebb5-259">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ebb5-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ebb5-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7ebb5-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7ebb5-261">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="7ebb5-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

