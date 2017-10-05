---
title: "Didacticiel : Intégration d’Azure Active Directory à Slack | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Slack."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 5aca630b2077d3f7d4ce9273ee668ed6a5f9843d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="7ec6b-103">Didacticiel : Intégration d’Azure AD avec Slack</span><span class="sxs-lookup"><span data-stu-id="7ec6b-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="7ec6b-104">Dans ce didacticiel, vous allez apprendre à intégrer Slack à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ec6b-104">In this tutorial, you learn how to integrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ec6b-105">L’intégration de Slack dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-105">Integrating Slack with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ec6b-106">Dans Azure AD, vous pouvez contrôler qui a accès à Slack</span><span class="sxs-lookup"><span data-stu-id="7ec6b-106">You can control in Azure AD who has access to Slack</span></span>
- <span data-ttu-id="7ec6b-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Slack (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ec6b-107">You can enable your users to automatically get signed-on to Slack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7ec6b-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7ec6b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7ec6b-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ec6b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ec6b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7ec6b-110">Prerequisites</span></span>

<span data-ttu-id="7ec6b-111">Pour configurer l’intégration d’Azure AD à Slack, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-111">To configure Azure AD integration with Slack, you need the following items:</span></span>

- <span data-ttu-id="7ec6b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ec6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ec6b-113">Un abonnement Slack pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7ec6b-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ec6b-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ec6b-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ec6b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ec6b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ec6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ec6b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7ec6b-118">Scenario description</span></span>
<span data-ttu-id="7ec6b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ec6b-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ec6b-121">Ajout de Slack à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7ec6b-121">Adding Slack from the gallery</span></span>
2. <span data-ttu-id="7ec6b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ec6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-the-gallery"></a><span data-ttu-id="7ec6b-123">Ajout de Slack à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7ec6b-123">Adding Slack from the gallery</span></span>
<span data-ttu-id="7ec6b-124">Pour configurer l’intégration de Slack avec Azure AD, vous devez ajouter Slack à partir de la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-124">To configure the integration of Slack into Azure AD, you need to add Slack from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ec6b-125">**Pour ajouter Slack à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ec6b-125">**To add Slack from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec6b-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7ec6b-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ec6b-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7ec6b-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7ec6b-133">Dans la zone de recherche, tapez **Slack**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-133">In the search box, type **Slack**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="7ec6b-135">Dans le volet de résultats, sélectionnez **Slack**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-135">In the results panel, select **Slack**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7ec6b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ec6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7ec6b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Slack avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7ec6b-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ec6b-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Slack équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Slack is to a user in Azure AD.</span></span> <span data-ttu-id="7ec6b-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Slack associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-140">In other words, a link relationship between an Azure AD user and the related user in Slack needs to be established.</span></span>

<span data-ttu-id="7ec6b-141">Dans Slack, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-141">In Slack, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7ec6b-142">Pour configurer et tester l’authentification unique Azure AD avec Slack, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-142">To configure and test Azure AD single sign-on with Slack, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ec6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ec6b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ec6b-145">**[Création d’un utilisateur de test Slack](#creating-a-slack-test-user)** pour avoir un équivalent de Britta Simon dans Slack, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - to have a counterpart of Britta Simon in Slack that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ec6b-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ec6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7ec6b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ec6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7ec6b-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Slack.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="7ec6b-150">**Pour configurer l’authentification unique Azure AD avec Slack, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ec6b-150">**To configure Azure AD single sign-on with Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec6b-151">Dans le portail Azure, sur la page d’intégration de l’application **Slack**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-151">In the Azure portal, on the **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7ec6b-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="7ec6b-155">Dans la section **Domaine et URL Slack**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-155">On the **Slack Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="7ec6b-157">a.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-157">a.</span></span> <span data-ttu-id="7ec6b-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="7ec6b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="7ec6b-159">b.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-159">b.</span></span> <span data-ttu-id="7ec6b-160">Dans la zone de texte **Identificateur**, saisissez l’URL : `https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="7ec6b-160">In the **Identifier** textbox, type the URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ec6b-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-161">The value is not real.</span></span> <span data-ttu-id="7ec6b-162">Vous devez mettre à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-162">You have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="7ec6b-163">Pour obtenir la valeur, contactez [l’équipe de support technique Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="7ec6b-163">Contact [Slack support team](https://slack.com/help/contact) to get the value</span></span>
     
4. <span data-ttu-id="7ec6b-164">L’application Slack attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-164">Slack application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7ec6b-165">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-165">Configure the following claims for this application.</span></span> <span data-ttu-id="7ec6b-166">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="7ec6b-167">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-167">The following screenshot shows an example for this.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="7ec6b-169">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique**, sélectionnez **user.mail** en tant **qu’identificateur d’utilisateur**, et pour chaque ligne indiquée dans le tableau ci-dessous, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-169">In the **User Attributes** section on the **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in the table below, perform the following steps:</span></span>
    
    | <span data-ttu-id="7ec6b-170">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="7ec6b-170">Attribute Name</span></span> | <span data-ttu-id="7ec6b-171">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="7ec6b-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="7ec6b-172">first_name</span><span class="sxs-lookup"><span data-stu-id="7ec6b-172">first_name</span></span> | <span data-ttu-id="7ec6b-173">user.givenname</span><span class="sxs-lookup"><span data-stu-id="7ec6b-173">user.givenname</span></span> |
    | <span data-ttu-id="7ec6b-174">last_name</span><span class="sxs-lookup"><span data-stu-id="7ec6b-174">last_name</span></span> | <span data-ttu-id="7ec6b-175">user.surname</span><span class="sxs-lookup"><span data-stu-id="7ec6b-175">user.surname</span></span> |
    | <span data-ttu-id="7ec6b-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="7ec6b-176">User.Email</span></span> | <span data-ttu-id="7ec6b-177">user.mail</span><span class="sxs-lookup"><span data-stu-id="7ec6b-177">user.mail</span></span> |  
    | <span data-ttu-id="7ec6b-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="7ec6b-178">User.Username</span></span> | <span data-ttu-id="7ec6b-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="7ec6b-179">user.userprincipalname</span></span> |

    <span data-ttu-id="7ec6b-180">a.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-180">a.</span></span> <span data-ttu-id="7ec6b-181">Cliquez sur **Attribut** pour ouvrir la boîte de dialogue **Modifier l’attribut** et effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-181">Click on **Attribute** to open **Edit Attribute** dialog box and perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="7ec6b-183">a.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-183">a.</span></span> <span data-ttu-id="7ec6b-184">Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="7ec6b-185">b.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-185">b.</span></span> <span data-ttu-id="7ec6b-186">Dans la liste **Valeur** , sélectionnez la valeur de l’attribut pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-186">From the **Value** list, select the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7ec6b-187">c.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-187">c.</span></span> <span data-ttu-id="7ec6b-188">Cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="7ec6b-188">Click **OK**</span></span>

6. <span data-ttu-id="7ec6b-189">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-189">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="7ec6b-191">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7ec6b-191">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7ec6b-193">Dans la section **Configuration de Slack** , cliquez sur **Configurer Slack** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-193">On the **Slack Configuration** section, click **Configure Slack** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ec6b-194">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-194">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="7ec6b-196">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Slack en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-196">In a different web browser window, log in to your Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="7ec6b-197">Accédez à **Microsoft Azure AD**, puis à **Team Settings**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-197">Navigate to **Microsoft Azure AD** then go to **Team Settings**.</span></span>

     ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="7ec6b-199">Dans la section **Team Settings**, cliquez sur l’onglet **Authentication** puis sur **Change Settings**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-199">In the **Team Settings** section, click the **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="7ec6b-201">Dans la boîte de dialogue **SAML Authentication Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-201">On the **SAML Authentication Settings** dialog, perform the following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="7ec6b-203">a.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-203">a.</span></span>  <span data-ttu-id="7ec6b-204">Dans la zone de texte **Point de terminaison SAML 2.0 (HTTP)**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-204">In the **SAML 2.0 Endpoint (HTTP)** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7ec6b-205">b.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-205">b.</span></span>  <span data-ttu-id="7ec6b-206">Dans la zone de texte **Émetteur du fournisseur d’identité**, collez la valeur de l’**ID d’entité SAML** copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-206">In the **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7ec6b-207">c.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-207">c.</span></span>  <span data-ttu-id="7ec6b-208">Ouvrez votre fichier de certificat téléchargé dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat public**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-208">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>

    <span data-ttu-id="7ec6b-209">d.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-209">d.</span></span> <span data-ttu-id="7ec6b-210">Configurez les trois paramètres ci-dessus comme nécessaire pour votre équipe Slack.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-210">Configure the above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="7ec6b-211">Pour plus d’informations sur les paramètres, vous trouverez le **guide de configuration de l’authentification unique sur Slack**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-211">For more information about the settings, please find the **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="7ec6b-212">e.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-212">e.</span></span>  <span data-ttu-id="7ec6b-213">Cliquez sur **Enregistrer la configuration**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users to change their email address**.

    e.  Select **Allow users to choose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="7ec6b-214">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ec6b-215">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ec6b-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ec6b-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7ec6b-217">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ec6b-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="7ec6b-218">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7ec6b-220">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ec6b-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec6b-221">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7ec6b-223">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7ec6b-225">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7ec6b-227">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ec6b-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7ec6b-229">a.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-229">a.</span></span> <span data-ttu-id="7ec6b-230">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ec6b-231">b.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-231">b.</span></span> <span data-ttu-id="7ec6b-232">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7ec6b-233">c.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-233">c.</span></span> <span data-ttu-id="7ec6b-234">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7ec6b-235">d.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-235">d.</span></span> <span data-ttu-id="7ec6b-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="7ec6b-237">Création d’un utilisateur de test Slack</span><span class="sxs-lookup"><span data-stu-id="7ec6b-237">Creating a Slack test user</span></span>

<span data-ttu-id="7ec6b-238">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Slack.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-238">The objective of this section is to create a user called Britta Simon in Slack.</span></span> <span data-ttu-id="7ec6b-239">Slack prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="7ec6b-240">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-240">There is no action item for you in this section.</span></span> <span data-ttu-id="7ec6b-241">Un utilisateur est créé lors d’une tentative d’accès à Slack s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-241">A new user is created during an attempt to access Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec6b-242">Si vous devez créer un utilisateur manuellement, contactez l’[équipe de support technique Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="7ec6b-242">If you need to create a user manually, you need to Contact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7ec6b-243">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ec6b-243">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7ec6b-244">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Slack.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Slack.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7ec6b-246">**Pour affecter Britta Simon à Slack, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ec6b-246">**To assign Britta Simon to Slack, perform the following steps:**</span></span>

1. <span data-ttu-id="7ec6b-247">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7ec6b-249">Dans la liste des applications, sélectionnez **Slack**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-249">In the applications list, select **Slack**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="7ec6b-251">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7ec6b-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-253">Click **Add** button.</span></span> <span data-ttu-id="7ec6b-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7ec6b-256">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7ec6b-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ec6b-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7ec6b-259">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7ec6b-259">Testing single sign-on</span></span>

<span data-ttu-id="7ec6b-260">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7ec6b-261">Lorsque vous cliquez sur la mosaïque Slack dans le volet d’accès, vous devez être connecté automatiquement à votre application Slack.</span><span class="sxs-lookup"><span data-stu-id="7ec6b-261">When you click the Slack tile in the Access Panel, you should get automatically signed-on to your Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ec6b-262">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7ec6b-262">Additional resources</span></span>

* [<span data-ttu-id="7ec6b-263">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ec6b-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ec6b-264">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7ec6b-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

