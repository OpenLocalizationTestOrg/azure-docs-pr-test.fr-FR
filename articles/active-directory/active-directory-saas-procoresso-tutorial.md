---
title: "Didacticiel : Intégration d’Azure Active Directory à Procore SSO | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Procore SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: 042a41eaa6bb21670b4c12068f1b017222f64b99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="8cee7-103">Didacticiel : Intégration d’Azure Active Directory à Procore SSO</span><span class="sxs-lookup"><span data-stu-id="8cee7-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="8cee7-104">Dans ce didacticiel, vous allez apprendre à intégrer Procore SSO à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8cee7-104">In this tutorial, you learn how to integrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8cee7-105">L’intégration de Procore SSO dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8cee7-105">Integrating Procore SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8cee7-106">Dans Azure AD, vous pouvez contrôler qui a accès à Procore SSO</span><span class="sxs-lookup"><span data-stu-id="8cee7-106">You can control in Azure AD who has access to Procore SSO</span></span>
- <span data-ttu-id="8cee7-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Procore SSO par le biais de l’authentification unique (SSO) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cee7-107">You can enable your users to automatically get signed-on to Procore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8cee7-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="8cee7-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="8cee7-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8cee7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Procore SSO, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="8cee7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8cee7-110">Prerequisites</span></span>

<span data-ttu-id="8cee7-111">Pour configurer l’intégration d’Azure AD à Procore SSO, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8cee7-111">To configure Azure AD integration with Procore SSO, you need the following items:</span></span>

- <span data-ttu-id="8cee7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cee7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8cee7-113">Un abonnement Procore SSO pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8cee7-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8cee7-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8cee7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8cee7-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8cee7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8cee7-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8cee7-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="8cee7-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8cee7-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8cee7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8cee7-118">Scenario description</span></span>
<span data-ttu-id="8cee7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8cee7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8cee7-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8cee7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8cee7-121">Ajout de Procore SSO à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8cee7-121">Adding Procore SSO from the gallery</span></span>
2. <span data-ttu-id="8cee7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cee7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-the-gallery"></a><span data-ttu-id="8cee7-123">Ajout de Procore SSO à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8cee7-123">Adding Procore SSO from the gallery</span></span>
<span data-ttu-id="8cee7-124">Pour configurer l’intégration de Procore SSO à Azure AD, vous devez ajouter Procore SSO à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8cee7-124">To configure the integration of Procore SSO into Azure AD, you need to add Procore SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8cee7-125">**Pour ajouter Procore SSO à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8cee7-125">**To add Procore SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8cee7-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8cee7-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8cee7-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8cee7-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8cee7-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8cee7-133">Dans le champ de recherche, tapez **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-133">In the search box, type **Procore SSO**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="8cee7-135">Dans le volet de résultats, sélectionnez **Procore SSO**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8cee7-135">In the results panel, select **Procore SSO**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8cee7-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cee7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8cee7-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Procore SSO avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8cee7-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8cee7-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Procore SSO équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cee7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Procore SSO is to a user in Azure AD.</span></span> <span data-ttu-id="8cee7-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Procore SSO associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="8cee7-140">In other words, a link relationship between an Azure AD user and the related user in Procore SSO needs to be established.</span></span>

<span data-ttu-id="8cee7-141">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** dans Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="8cee7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Procore SSO.</span></span>

<span data-ttu-id="8cee7-142">Pour configurer et tester l’authentification unique Azure AD avec Procore SSO, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="8cee7-142">To configure and test Azure AD single sign-on with Procore SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8cee7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8cee7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8cee7-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8cee7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8cee7-145">**[Création d’un utilisateur de test Procore SSO](#creating-a-procore-sso-test-user)** pour avoir un équivalent de Britta Simon dans Procore SSO lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="8cee7-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - to have a counterpart of Britta Simon in Procore SSO that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8cee7-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d'utiliser l'authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cee7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8cee7-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8cee7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8cee7-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cee7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8cee7-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="8cee7-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="8cee7-150">**Pour configurer l’authentification unique Azure AD avec Procore SSO, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8cee7-150">**To configure Azure AD single sign-on with Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="8cee7-151">Dans le portail de gestion Azure, sur la page d’intégration de l’application **Procore SSO**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-151">In the Azure Management portal, on the **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8cee7-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8cee7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="8cee7-155">Dans la section **Domaine SSO et URL de Procore**, l’utilisateur n’aura pas à effectuer les étapes que l’application a déjà intégrées préalablement avec Azure.</span><span class="sxs-lookup"><span data-stu-id="8cee7-155">On the **Procore SSO Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="8cee7-157">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8cee7-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="8cee7-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8cee7-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8cee7-161">Dans la section **Configuration de Procore SSO** , cliquez sur **Configurer PProcore SSO** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-161">On the **Procore SSO Configuration** section, click **Configure Procore SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8cee7-162">Copiez **l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8cee7-162">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="8cee7-164">Pour configurer l’authentification unique sur **Procore SSO**, connectez-vous à votre site d’entreprise Procore en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8cee7-164">To configure single sign-on on **Procore SSO** side, login to your procore company site as an administrator.</span></span>

8. <span data-ttu-id="8cee7-165">Dans la liste déroulante de boîte à outils, cliquez sur **Admin** pour ouvrir la page de paramètres de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8cee7-165">From the toolbox drop down, click on **Admin** to open the SSO settings page.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="8cee7-167">Collez les valeurs dans les zones comme décrit ci-dessous-</span><span class="sxs-lookup"><span data-stu-id="8cee7-167">Paste the values in the boxes as described below-</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="8cee7-169">a.</span><span class="sxs-lookup"><span data-stu-id="8cee7-169">a.</span></span> <span data-ttu-id="8cee7-170">Dans la zone **Émetteur d’URL d’authentification unique**, collez l’ID d’entité SAML copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8cee7-170">In the **Single Sign On Issuer URL** box, paste the SAML Entity ID copied from the Azure portal.</span></span>

    <span data-ttu-id="8cee7-171">b.</span><span class="sxs-lookup"><span data-stu-id="8cee7-171">b.</span></span> <span data-ttu-id="8cee7-172">Dans la zone **URL cible de connexion SAML**, collez l’URL d’authentification unique SAML copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8cee7-172">In the **SAML Sign On Target URL** box, paste the SAML Single Sign-On Service URL copied from the Azure portal.</span></span>

    <span data-ttu-id="8cee7-173">c.</span><span class="sxs-lookup"><span data-stu-id="8cee7-173">c.</span></span> <span data-ttu-id="8cee7-174">Ouvrez maintenant le fichier **XML de métadonnées** téléchargé à partir du portail Azure et copiez le certificat dans la balise nommée **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-174">Now open the **Metadata XML** downloaded above from the Azure portal and copy the certficate in the tag named **X509Certificate**.</span></span> <span data-ttu-id="8cee7-175">Collez la valeur copiée dans la zone **Certificat x509 d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-175">Paste the copied value into the **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="8cee7-176">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="8cee7-177">Après ces paramètres, vous devez envoyer le **nom de domaine** (par ex. **contoso.com**) via lequel vous connectez à Procore à [l’équipe de support technique de Procore](https://support.procore.com/), qui activera l’authentification unique fédérée pour ce domaine.</span><span class="sxs-lookup"><span data-stu-id="8cee7-177">After these settings, you needs to send the **domain name** (e.g **contoso.com**) through which you are logging into Procore to the [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

To ensure users can sign-in to Procore SSO after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Procore SSO in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8cee7-178">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cee7-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="8cee7-179">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="8cee7-179">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8cee7-181">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8cee7-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8cee7-182">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-182">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8cee7-184">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8cee7-184">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8cee7-186">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-186">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8cee7-188">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8cee7-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8cee7-190">a.</span><span class="sxs-lookup"><span data-stu-id="8cee7-190">a.</span></span> <span data-ttu-id="8cee7-191">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8cee7-192">b.</span><span class="sxs-lookup"><span data-stu-id="8cee7-192">b.</span></span> <span data-ttu-id="8cee7-193">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8cee7-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8cee7-194">c.</span><span class="sxs-lookup"><span data-stu-id="8cee7-194">c.</span></span> <span data-ttu-id="8cee7-195">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8cee7-196">d.</span><span class="sxs-lookup"><span data-stu-id="8cee7-196">d.</span></span> <span data-ttu-id="8cee7-197">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="8cee7-198">Création d’un utilisateur de test Procore SSO</span><span class="sxs-lookup"><span data-stu-id="8cee7-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="8cee7-199">Suivez les étapes ci-dessous pour créer un utilisateur de test Procore de leur côté.</span><span class="sxs-lookup"><span data-stu-id="8cee7-199">Please follow the below steps to create a Procore test user on their side.</span></span>

1. <span data-ttu-id="8cee7-200">Connectez-vous à votre site d’entreprise Procore en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8cee7-200">Login to your procore company site as an administrator.</span></span>  

2. <span data-ttu-id="8cee7-201">Dans la liste déroulante de boîte à outils, cliquez sur **Annuaire** pour ouvrir la page d’annuaire de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="8cee7-201">From the toolbox drop down, click on **Directory** to open the company directory page.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="8cee7-203">Cliquez sur l’option **Ajouter une personne** pour ouvrir le formulaire et réglez les options suivantes -</span><span class="sxs-lookup"><span data-stu-id="8cee7-203">Click on **Add a Person** option to open the form and enter perform following options -</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="8cee7-205">a.</span><span class="sxs-lookup"><span data-stu-id="8cee7-205">a.</span></span> <span data-ttu-id="8cee7-206">Dans la zone de texte **First Name**, tapez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-206">In the **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="8cee7-207">b.</span><span class="sxs-lookup"><span data-stu-id="8cee7-207">b.</span></span> <span data-ttu-id="8cee7-208">Dans la zone de texte **Last Name**, tapez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-208">In the **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="8cee7-209">c.</span><span class="sxs-lookup"><span data-stu-id="8cee7-209">c.</span></span> <span data-ttu-id="8cee7-210">Dans la zone de texte **Adresse e-mail** , tapez l’adresse de messagerie de l’utilisateur, par exemple **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-210">In the **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="8cee7-211">d.</span><span class="sxs-lookup"><span data-stu-id="8cee7-211">d.</span></span> <span data-ttu-id="8cee7-212">Sélectionnez **Modèle d’autorisation** pour **Appliquer le modèle d’autorisation plus tard**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="8cee7-213">e.</span><span class="sxs-lookup"><span data-stu-id="8cee7-213">e.</span></span> <span data-ttu-id="8cee7-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-214">Click **Create**.</span></span>

4. <span data-ttu-id="8cee7-215">Vérifiez et mettez à jour les détails du contact nouvellement ajouté.</span><span class="sxs-lookup"><span data-stu-id="8cee7-215">Check and update the details for the newly added contact.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="8cee7-217">Cliquez sur **Enregistrer et envoyer l’invitation** (si une invitation par e-mail est requise) ou **Enregistrer** (enregistrer directement) pour terminer l’inscription de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8cee7-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) to complete the user registration.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8cee7-219">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cee7-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8cee7-220">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="8cee7-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Procore SSO.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8cee7-222">**Pour affecter Britta Simon à Procore SSO, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8cee7-222">**To assign Britta Simon to Procore SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="8cee7-223">Dans le portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8cee7-225">Dans la liste des applications, sélectionnez **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-225">In the applications list, select **Procore SSO**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="8cee7-227">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8cee7-229">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-229">Click **Add** button.</span></span> <span data-ttu-id="8cee7-230">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8cee7-232">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8cee7-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8cee7-233">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8cee7-234">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8cee7-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8cee7-235">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8cee7-235">Testing single sign-on</span></span>

<span data-ttu-id="8cee7-236">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8cee7-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8cee7-237">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8cee7-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="8cee7-238">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8cee7-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="8cee7-239">Lorsque vous cliquez sur la mosaïque Procore SSO dans le volet d’accès, vous devez être connecté automatiquement à votre application Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="8cee7-239">When you click the Procore SSO tile in the Access Panel, you should get automatically signed-on to your Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8cee7-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8cee7-240">Additional resources</span></span>

* [<span data-ttu-id="8cee7-241">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8cee7-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8cee7-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8cee7-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

