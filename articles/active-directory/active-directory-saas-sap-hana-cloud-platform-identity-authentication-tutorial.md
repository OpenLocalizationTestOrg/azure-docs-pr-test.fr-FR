---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform Identity Authentication | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SAP HANA Cloud Platform Identity Authentication."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 7799bf03cc6705f805a48f329a265a3d84bed55f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="bbc3b-103">Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="bbc3b-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="bbc3b-104">Dans ce didacticiel, vous allez apprendre à intégrer SAP HANA Cloud Platform Identity Authentication à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbc3b-104">In this tutorial, you learn how to integrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bbc3b-105">SAP HANA Cloud Platform Identity Authentication est utilisé comme IdP proxy pour accéder aux applications SAP avec Azure AD comme IdP principal.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP to access SAP applications using Azure AD as the main IdP.</span></span>

<span data-ttu-id="bbc3b-106">L’intégration de SAP HANA Cloud Platform Identity Authentication avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bbc3b-107">Vous pouvez contrôler dans Azure AD qui a accès à l’application SAP.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-107">You can control in Azure AD who has access to SAP application</span></span>
- <span data-ttu-id="bbc3b-108">Vous pouvez autoriser les utilisateurs à se connecter automatiquement aux applications SAP via l’authentification unique (SSO) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-108">You can enable your users to automatically get signed-on to SAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbc3b-109">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-109">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="bbc3b-110">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbc3b-110">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bbc3b-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bbc3b-111">Prerequisites</span></span>

<span data-ttu-id="bbc3b-112">Pour configurer l’intégration d’Azure AD avec SAP HANA Cloud Platform Identity Authentication, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-112">To configure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need the following items:</span></span>

- <span data-ttu-id="bbc3b-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc3b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="bbc3b-114">Un abonnement **SAP HANA Cloud Platform Identity Authentication** compatible avec l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bbc3b-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="bbc3b-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="bbc3b-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbc3b-117">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="bbc3b-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbc3b-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbc3b-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bbc3b-119">Scenario description</span></span>
<span data-ttu-id="bbc3b-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="bbc3b-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbc3b-122">Ajouter SAP HANA Cloud Platform Identity Authentication à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="bbc3b-122">Adding SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
2. <span data-ttu-id="bbc3b-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc3b-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="bbc3b-124">Avant de rentrer dans les détails techniques, il est essentiel de comprendre les concepts que vous allez voir.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-124">Before diving into the technical details, it is vital to understand the concepts you're going to look at.</span></span> <span data-ttu-id="bbc3b-125">La fédération SAP HANA Cloud Platform Identity Authentication et Azure Active Directory vous permet d’implémenter l’authentification unique entre les applications ou les services protégés par AAD (comme IdP) et les applications et services SAP protégés par SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-125">The SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you to implement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="bbc3b-126">Actuellement, SAP HANA Cloud Platform Identity Authentication remplit la fonction de fournisseur d’identité proxy pour les applications SAP.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider to SAP-applications.</span></span> <span data-ttu-id="bbc3b-127">Azure Active Directory joue en retour le rôle de fournisseur d’identité principal dans cette configuration.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-127">Azure Active Directory in turn acts as the leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="bbc3b-128">En voici une illustration :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-128">The following diagram illustrates this:</span></span>    

![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="bbc3b-130">Avec cette configuration, votre client SAP HANA Cloud Platform Identity Authentication sera configuré en tant qu’application approuvée dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="bbc3b-131">Toutes les applications et tous les services SAP que vous souhaitez protéger de cette façon sont ensuite configurés dans la console de gestion SAP HANA Cloud Platform Identity Authentication !</span><span class="sxs-lookup"><span data-stu-id="bbc3b-131">All SAP applications and services you want to protect through this way are subsequently configured in the SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="bbc3b-132">Cela signifie que l’autorisation d’accorder l’accès aux services et applications SAP doit avoir lieu dans SAP HANA Cloud Platform Identity Authentication pour ce type de configuration (contrairement à la configuration des autorisations dans Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="bbc3b-132">This means that authorization for granting access to SAP applications and services needs to take place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed to configuring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="bbc3b-133">Si vous configurez l’authentification SAP HANA Cloud Platform Identity Authentication en tant qu’application sur la Place de marché Azure Active Directory, vous n’avez pas besoin de gérer la configuration nécessaire aux revendications individuelles / les assertions et transformations SAML nécessaires pour produire un jeton d’authentification valide pour les applications SAP.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through the Azure Active Directory Marketplace, you don't need to take care of configuring needed individual claims / SAML assertions and transformations needed to produce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="bbc3b-134">Actuellement, l’authentification unique web n’a été testée que par les deux parties.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="bbc3b-135">Les flux nécessaires à la communication application-API ou API-API devraient fonctionner mais n’ont pas encore été testés.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="bbc3b-136">Ils seront testés dans le cadre des activités à venir.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a><span data-ttu-id="bbc3b-137">Ajouter SAP HANA Cloud Platform Identity Authentication à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="bbc3b-137">Add SAP HANA Cloud Platform Identity Authentication from the gallery</span></span>
<span data-ttu-id="bbc3b-138">Pour configurer l’intégration de SAP HANA Cloud Platform Identity Authentication dans Azure AD, vous devez ajouter SAP HANA Cloud Platform Identity Authentication à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-138">To configure the integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need to add SAP HANA Cloud Platform Identity Authentication from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bbc3b-139">**Pour ajouter SAP HANA Cloud Platform Identity Authentication à partir de la galerie, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="bbc3b-139">**To add SAP HANA Cloud Platform Identity Authentication from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc3b-140">Dans le [**Portail de gestion Azure**](https://portal.azure.com), dans le panneau de navigation de gauche, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-140">In the [**Azure Management portal**](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bbc3b-142">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-142">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bbc3b-143">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-143">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bbc3b-145">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-145">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bbc3b-147">Dans la zone de recherche, tapez **SAP HANA Cloud Platform Identity Authentication**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-147">In the search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="bbc3b-149">Dans le volet de résultats, sélectionnez **SAP HANA Cloud Platform Identity Authentication**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-149">In the results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bbc3b-151">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc3b-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="bbc3b-152">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP HANA Cloud Platform Identity Authentication, à partir d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bbc3b-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bbc3b-153">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SAP HANA Cloud Platform Identity Authentication équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-153">For SSO to work, Azure AD needs to know what the counterpart user in SAP HANA Cloud Platform Identity Authentication is to a user in Azure AD.</span></span> <span data-ttu-id="bbc3b-154">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur SAP HANA Cloud Platform Identity Authentication associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-154">In other words, a link relationship between an Azure AD user and the related user in SAP HANA Cloud Platform Identity Authentication needs to be established.</span></span>

<span data-ttu-id="bbc3b-155">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-155">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="bbc3b-156">Pour configurer et tester l’authentification unique Azure AD avec SAP HANA Cloud Platform Identity Authentication, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-156">To configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bbc3b-157">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bbc3b-158">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbc3b-159">**[Création d’un utilisateur de test SAP HANA Cloud Platform Identity Authentication](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** pour avoir un équivalent de Britta Simon dans SAP HANA Cloud Platform Identity Authentication qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - to have a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="bbc3b-160">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-160">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbc3b-161">**[Test de l’authentification unique](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-161">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="bbc3b-162">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc3b-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="bbc3b-163">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-163">In this section, you enable Azure AD SSO in the Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="bbc3b-164">L’application SAP HANA Cloud Platform Identity Authentication attend les assertions SAML dans un format précis.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-164">SAP HANA Cloud Platform Identity Authentication application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="bbc3b-165">Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-165">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="bbc3b-166">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-166">The following screenshot shows an example for this.</span></span>

![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="bbc3b-168">**Pour configurer l’authentification unique d’Azure AD avec SAP HANA Cloud Platform Identity Authentication, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="bbc3b-168">**To configure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc3b-169">Dans le Portail de gestion Azure, sur la page d’intégration des applications **SAP HANA Cloud Platform Identity Authentication**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-169">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bbc3b-171">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-171">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique][5]

3. <span data-ttu-id="bbc3b-173">Dans la section **Attributs utilisateur**, sur la boîte de dialogue **Authentification unique**, si votre application SAP attend un attribut, par exemple « firstName ».</span><span class="sxs-lookup"><span data-stu-id="bbc3b-173">In the **User Attributes** section on the **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="bbc3b-174">Dans la boîte de dialogue des attributs du jeton SAML, ajoutez l’attribut « firstName ».</span><span class="sxs-lookup"><span data-stu-id="bbc3b-174">On the SAML token attributes dialog, add the "firstName" attribute.</span></span>
 1. <span data-ttu-id="bbc3b-175">Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
 
    ![Configurer l’authentification unique][6]

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="bbc3b-178">Dans la zone de texte **Nom de l’attribut**, tapez le nom de l’attribut « firstName ».</span><span class="sxs-lookup"><span data-stu-id="bbc3b-178">In the **Attribute Name** textbox, type the attribute name "firstName".</span></span>
 3. <span data-ttu-id="bbc3b-179">Dans la liste **Valeur de l’attribut**, sélectionnez la valeur d’attribut « user.givenname ».</span><span class="sxs-lookup"><span data-stu-id="bbc3b-179">From the **Attribute Value** list, select the attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="bbc3b-180">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-180">Click **Ok**.</span></span>

4. <span data-ttu-id="bbc3b-181">Dans la section **Domaine et URL SAP HANA Cloud Platform Identity Authentication**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-181">On the **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="bbc3b-183">Dans la zone de texte **URL de connexion**, tapez l’URL de connexion de l’application SAP.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-183">In the **Sign On URL** textbox, type the sign on URL for the SAP application.</span></span>
 2. <span data-ttu-id="bbc3b-184">Dans la zone de texte **Identificateur**, tapez la valeur au format suivant : `<entity-id>.accounts.ondemand.com`.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-184">In the **Identifier** textbox, type the value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="bbc3b-185">Si vous ne connaissez pas cette valeur, suivez la documentation SAP HANA Cloud Platform Identity Authentication sur [Configuration du client SAML 2.0](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="bbc3b-185">If you don't know this value, please follow the SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="bbc3b-186">Dans la section **Configuration SAP HANA Cloud Platform Identity Authentication**, cliquez sur **Configurer SAP HANA Cloud Platform Identity Authentication** pour ouvrir la boîte de dialogue **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-186">On the **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** to open **Configure sign-on** dialog.</span></span> <span data-ttu-id="bbc3b-187">Ensuite, cliquez sur **Métadonnées XML SAML** et enregistrez le fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-187">Then, click on **SAML XML Metadata** and save the file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="bbc3b-190">Pour configurer l’authentification unique sur votre application, accédez à la console d’administration de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-190">To get SSO configured for your application, go to SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="bbc3b-191">L’URL suit le modèle suivant : `https://<tenant-id>.accounts.ondemand.com/admin`.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-191">The URL has the following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="bbc3b-192">Ensuite, suivez la documentation sur SAP HANA Cloud Platform Identity Authentication pour [configurer Microsoft Azure AD en tant que fournisseur d’identité d’entreprise sur SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="bbc3b-192">Then, follow the documentation on SAP HANA Cloud Platform Identity Authentication to [Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="bbc3b-193">Dans le Portail de gestion Azure, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-193">In the Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="bbc3b-194">Effectuez les étapes suivantes uniquement si vous souhaitez ajouter et activer l’authentification unique (SSO) pour une autre application SAP.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-194">Continue the following steps only if you want to add and enable SSO for another SAP application.</span></span> <span data-ttu-id="bbc3b-195">Répétez les étapes décrites dans la section « Ajouter SAP HANA Cloud Platform Identity Authentication à partir de la galerie » pour ajouter une autre instance de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-195">Repeat steps under the section “Adding SAP HANA Cloud Platform Identity Authentication from the gallery” to add another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="bbc3b-196">Dans le Portail de gestion Azure, sur la page d’intégration des applications **SAP HANA Cloud Platform Identity Authentication**, cliquez sur **Authentification liée**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-196">In the Azure Management portal, on the **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Configurer l’authentification liée](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="bbc3b-198">Enregistrez ensuite la configuration.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-198">Then, save the configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="bbc3b-199">La nouvelle application utilisera la configuration de l’authentification unique (SSO) de l’application SAP précédente.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-199">The new application will leverage the SSO configuration for the previous SAP application.</span></span> <span data-ttu-id="bbc3b-200">Veillez à utiliser les mêmes fournisseurs d’identité d’entreprise dans la console d’administration de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-200">Please make sure you use the same Corporate Identity Providers in the SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bbc3b-201">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc3b-201">Create an Azure AD test user</span></span>
<span data-ttu-id="bbc3b-202">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le nouveau portail.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-202">The objective of this section is to create a test user in the new portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bbc3b-204">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbc3b-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc3b-205">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-205">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbc3b-207">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-207">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbc3b-209">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-209">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbc3b-211">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bbc3b-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="bbc3b-213">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-213">In the **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="bbc3b-214">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="bbc3b-215">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-215">Select **Show Password** and write down the value of the **Password**.</span></span>
  4. <span data-ttu-id="bbc3b-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="bbc3b-217">Créer un utilisateur de test SAP HANA Cloud Platform Identity Authentication</span><span class="sxs-lookup"><span data-stu-id="bbc3b-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="bbc3b-218">Vous n’avez pas besoin de créer un utilisateur sur SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-218">You don't need to create an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="bbc3b-219">Les utilisateurs qui se trouvent dans le magasin d’utilisateurs Azure AD peuvent utiliser la fonctionnalité d’authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="bbc3b-219">Users who are in the Azure AD user store can use the SSO functionality.</span></span>

<span data-ttu-id="bbc3b-220">SAP HANA Cloud Platform Identity Authentication prend en charge l’option de fédération des identités.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-220">SAP HANA Cloud Platform Identity Authentication supports the Identity Federation option.</span></span> <span data-ttu-id="bbc3b-221">Cette option permet à l’application de vérifier si les utilisateurs authentifiés par le fournisseur d’identité d’entreprise sont présents dans le magasin d’utilisateurs de SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-221">This option allows the application to check if the users authenticated by the corporate identity provider exist in the user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="bbc3b-222">Dans le paramètre par défaut, l’option de fédération des identités est désactivée.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-222">In the default setting, the Identity Federation option is disabled.</span></span> <span data-ttu-id="bbc3b-223">Si la fédération des identités est activée, seuls les utilisateurs importés dans SAP HANA Cloud Platform Identity Authentication peuvent accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-223">If Identity Federation is enabled, only the users that are imported in SAP HANA Cloud Platform Identity Authentication are able to access the application.</span></span> 

<span data-ttu-id="bbc3b-224">Pour savoir comment activer ou désactiver la fédération des identités avec SAP HANA Cloud Platform Identity Authentication, consultez la page Activer la fédération des identités avec SAP HANA Cloud Platform Identity Authentication dans la section [Configurer la fédération des identités avec le magasin d’utilisateurs de SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="bbc3b-224">For more information about how to enable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with the User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bbc3b-225">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc3b-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="bbc3b-226">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-226">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SAP HANA Cloud Platform Identity Authentication.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bbc3b-228">**Pour affecter Britta Simon à SAP HANA Cloud Platform Identity Authentication, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="bbc3b-228">**To assign Britta Simon to SAP HANA Cloud Platform Identity Authentication, perform the following steps:**</span></span>

1. <span data-ttu-id="bbc3b-229">Dans le Portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, allez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-229">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bbc3b-231">Dans la liste des applications, sélectionnez **SAP HANA Cloud Platform Identity Authentication**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-231">In the applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="bbc3b-233">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bbc3b-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-235">Click **Add** button.</span></span> <span data-ttu-id="bbc3b-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bbc3b-238">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bbc3b-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbc3b-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="bbc3b-241">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bbc3b-241">Test single sign-on</span></span>

<span data-ttu-id="bbc3b-242">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-242">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="bbc3b-243">Lorsque vous cliquez sur la mosaïque SAP HANA Cloud Platform Identity Authentication dans le volet d’accès, vous êtes automatiquement connecté à votre application SAP HANA Cloud Platform Identity Authentication.</span><span class="sxs-lookup"><span data-stu-id="bbc3b-243">When you click the SAP HANA Cloud Platform Identity Authentication tile in the Access Panel, you should get automatically signed-on to your SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bbc3b-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bbc3b-244">Additional resources</span></span>

* [<span data-ttu-id="bbc3b-245">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbc3b-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbc3b-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bbc3b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png