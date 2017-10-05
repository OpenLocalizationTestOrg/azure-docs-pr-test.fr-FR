---
title: "Didacticiel : intégration d’Azure Active Directory à Teamphoria | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 2a35efb04d7fe22abc6894c149caf090666ce016
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="1c193-103">Didacticiel : Intégration d’Azure Active Directory à Teamphoria</span><span class="sxs-lookup"><span data-stu-id="1c193-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="1c193-104">Dans ce didacticiel, vous allez apprendre à intégrer Teamphoria à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c193-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c193-105">L’intégration de Teamphoria dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1c193-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1c193-106">Dans Azure AD, vous pouvez contrôler qui a accès à Teamphoria</span><span class="sxs-lookup"><span data-stu-id="1c193-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="1c193-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Teamphoria (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c193-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c193-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="1c193-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="1c193-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c193-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Teamphoria, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="1c193-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1c193-110">Prerequisites</span></span>

<span data-ttu-id="1c193-111">Pour configurer l’intégration d’Azure AD avec Teamphoria, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1c193-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="1c193-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c193-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c193-113">Un abonnement Teamphoria pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1c193-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c193-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1c193-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c193-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1c193-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c193-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1c193-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1c193-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c193-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c193-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1c193-118">Scenario description</span></span>
<span data-ttu-id="1c193-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1c193-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c193-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c193-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c193-121">Ajout de Teamphoria à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1c193-121">Adding Teamphoria from the gallery</span></span>
2. <span data-ttu-id="1c193-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c193-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="1c193-123">Ajout de Teamphoria à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1c193-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="1c193-124">Pour configurer l’intégration de Teamphoria à Azure AD, vous devez ajouter Teamphoria à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1c193-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1c193-125">**Pour ajouter Teamphoria à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c193-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1c193-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c193-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c193-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1c193-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1c193-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1c193-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1c193-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1c193-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1c193-133">Dans la zone de recherche, entrez **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="1c193-133">In the search box, type **Teamphoria**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="1c193-135">Dans le panneau de résultats, sélectionnez **Teamphoria**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1c193-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c193-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c193-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c193-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Teamphoria avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1c193-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c193-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Teamphoria équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c193-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="1c193-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Teamphoria associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1c193-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="1c193-141">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** dans Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="1c193-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Teamphoria.</span></span>

<span data-ttu-id="1c193-142">Pour configurer et tester l’authentification unique Azure AD avec Teamphoria, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c193-142">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1c193-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1c193-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1c193-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c193-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c193-145">**[Création d’un utilisateur de test Teamphoria](#creating-a-teamphoria-test-user)** pour avoir un équivalent de Britta Simon dans Teamphoria qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1c193-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1c193-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c193-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c193-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1c193-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c193-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c193-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c193-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le Portail de gestion Azure et configurer l’authentification unique dans votre application Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="1c193-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="1c193-150">**Pour configurer l'authentification unique Azure AD avec Teamphoria, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c193-150">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="1c193-151">Dans le Portail de gestion Azure, sur la page d’intégration de l’application **Teamphoria**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1c193-151">In the Azure Management portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1c193-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1c193-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="1c193-155">Dans la section **Domaine et URL Teamphoria**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c193-155">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="1c193-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c193-157">a.</span></span> <span data-ttu-id="1c193-158">Dans la zone de texte **URL de connexion**, tapez l’URL au format suivant : `https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="1c193-158">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>    

    > [!NOTE] 
    > <span data-ttu-id="1c193-159">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1c193-159">Please note that these are not the real values.</span></span> <span data-ttu-id="1c193-160">Vous devez mettre à jour ces valeurs avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="1c193-160">You have to update these values with the actual Sign-On URL.</span></span> <span data-ttu-id="1c193-161">Contactez l[’équipe de support technique Teamphoria](https://www.teamphoria.com/) pour obtenir l’URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="1c193-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span> 

4. <span data-ttu-id="1c193-162">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1c193-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="1c193-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1c193-164">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c193-166">Dans la section **Configuration de Teamphoria**, cliquez sur **Configurer Teamphoria** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="1c193-166">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1c193-167">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="1c193-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="1c193-169">Pour configurer l’authentification unique côté **Teamphoria**, connectez-vous à votre application Teamphoria en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1c193-169">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="1c193-170">Accédez à l’option **ADMIN SETTINGS** (Paramètres d’administration) dans la barre d’outils gauche puis, sous l’onglet Configure (Configurer), cliquez sur **SINGLE SIGN-ON** (Authentification unique) pour ouvrir la fenêtre de configuration de l’authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="1c193-170">Go to **ADMIN SETTINGS** option in the left toolbar and under the the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="1c193-172">Cliquez sur l’option **ADD NEW IDENTITY PROVIDER** (Ajouter un nouveau fournisseur d’identité) dans le coin supérieur droit pour ouvrir le formulaire permettant d’ajouter les paramètres pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1c193-172">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="1c193-174">Entrez les informations dans les champs comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1c193-174">Enter the details in the fields as described below-</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="1c193-176">a.</span><span class="sxs-lookup"><span data-stu-id="1c193-176">a.</span></span> <span data-ttu-id="1c193-177">**DISPLAY NAME** (Nom d’affichage) : entrez le nom d’affichage du plug-in sur la page d’administration.</span><span class="sxs-lookup"><span data-stu-id="1c193-177">**DISPLAY NAME** : Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="1c193-178">b.</span><span class="sxs-lookup"><span data-stu-id="1c193-178">b.</span></span> <span data-ttu-id="1c193-179">**BUTTON NAME** (Nom du bouton) : nom de l’onglet qui s’affiche sur la page de connexion via l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1c193-179">**BUTTON NAME** : The name of the tab which will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="1c193-180">c.</span><span class="sxs-lookup"><span data-stu-id="1c193-180">c.</span></span> <span data-ttu-id="1c193-181">**CERTIFICATE** (Certificat) : ouvrez le certificat téléchargé précédemment à partir du portail Azure dans le Bloc-notes, copiez le contenu puis collez-le dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="1c193-181">**CERTIFICATE** : Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="1c193-182">d.</span><span class="sxs-lookup"><span data-stu-id="1c193-182">d.</span></span> <span data-ttu-id="1c193-183">**ENTRY POINT** (Point d’entrée) : collez l**’URL du service d’authentification unique SAML** copiée précédemment à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1c193-183">**ENTRY POINT** : Paste the **SAML Single Sign-On Service URL** copied earlier form the Azure portal.</span></span>

    <span data-ttu-id="1c193-184">e.</span><span class="sxs-lookup"><span data-stu-id="1c193-184">e.</span></span> <span data-ttu-id="1c193-185">Définissez l’option sur **ON** , puis cliquez sur **SAVE** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="1c193-185">Switch the option to **ON** and click on **SAVE**.</span></span>   

<!--### Next steps

To ensure users can sign-in to Teamphoria after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Teamphoria in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c193-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c193-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c193-187">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="1c193-187">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1c193-189">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c193-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1c193-190">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c193-190">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c193-192">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1c193-192">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c193-194">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1c193-194">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c193-196">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c193-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c193-198">a.</span><span class="sxs-lookup"><span data-stu-id="1c193-198">a.</span></span> <span data-ttu-id="1c193-199">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c193-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c193-200">b.</span><span class="sxs-lookup"><span data-stu-id="1c193-200">b.</span></span> <span data-ttu-id="1c193-201">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c193-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c193-202">c.</span><span class="sxs-lookup"><span data-stu-id="1c193-202">c.</span></span> <span data-ttu-id="1c193-203">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1c193-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1c193-204">d.</span><span class="sxs-lookup"><span data-stu-id="1c193-204">d.</span></span> <span data-ttu-id="1c193-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c193-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="1c193-206">Création d’un utilisateur de test Teamphoria</span><span class="sxs-lookup"><span data-stu-id="1c193-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="1c193-207">Pour se connecter à Teamphoria, les utilisateurs d’Azure AD doivent être approvisionnés dans Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="1c193-207">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="1c193-208">Dans le cas de Teamphoria, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="1c193-208">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="1c193-209">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c193-209">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="1c193-210">Connectez-vous au site d’entreprise Teamphoria en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1c193-210">Log in to your Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="1c193-211">Cliquez sur les paramètres **ADMIN** dans la barre d’outils gauche puis, sous l’onglet **MANAGE** (Gérer), cliquez sur **USERS** (Utilisateurs) afin d’ouvrir la page d’administration pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1c193-211">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="1c193-213">Cliquez sur l’option **MANUAL INVITE** (Inviter manuellement).</span><span class="sxs-lookup"><span data-stu-id="1c193-213">Click on the **MANUAL INVITE** option.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="1c193-215">Dans cette page, effectuez l’action suivante.</span><span class="sxs-lookup"><span data-stu-id="1c193-215">On this page, perform following action.</span></span> 
    
    ![Inviter des personnes](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="1c193-217">a.</span><span class="sxs-lookup"><span data-stu-id="1c193-217">a.</span></span> <span data-ttu-id="1c193-218">Dans la zone de texte **EMAIL ADDRESS** (Adresse e-mail), tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c193-218">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c193-219">b.</span><span class="sxs-lookup"><span data-stu-id="1c193-219">b.</span></span> <span data-ttu-id="1c193-220">Dans la zone de texte **FIRST NAME** (Prénom), tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1c193-220">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="1c193-221">c.</span><span class="sxs-lookup"><span data-stu-id="1c193-221">c.</span></span> <span data-ttu-id="1c193-222">Dans la zone de texte **LAST NAME** (Nom), tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1c193-222">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="1c193-223">d.</span><span class="sxs-lookup"><span data-stu-id="1c193-223">d.</span></span> <span data-ttu-id="1c193-224">Cliquez sur **INVITE 1 USER** (Inviter l’utilisateur 1).</span><span class="sxs-lookup"><span data-stu-id="1c193-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="1c193-225">L’utilisateur doit accepter l’invitation pour être créé dans le système.</span><span class="sxs-lookup"><span data-stu-id="1c193-225">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1c193-226">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c193-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1c193-227">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="1c193-227">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Teamphoria.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1c193-229">**Pour affecter Britta Simon à Teamphoria, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1c193-229">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="1c193-230">Dans le portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1c193-230">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1c193-232">Dans la liste des applications, sélectionnez **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="1c193-232">In the applications list, select **Teamphoria**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="1c193-234">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1c193-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1c193-236">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1c193-236">Click **Add** button.</span></span> <span data-ttu-id="1c193-237">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1c193-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1c193-239">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1c193-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1c193-240">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1c193-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c193-241">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1c193-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c193-242">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1c193-242">Testing single sign-on</span></span>

<span data-ttu-id="1c193-243">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1c193-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1c193-244">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1c193-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="1c193-245">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1c193-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1c193-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1c193-246">Additional resources</span></span>

* [<span data-ttu-id="1c193-247">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c193-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c193-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1c193-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

