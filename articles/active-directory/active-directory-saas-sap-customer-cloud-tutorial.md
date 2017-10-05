---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP Cloud pour le client | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SAP Cloud pour le client."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: e4d945525a45704f34e1d9e742220928a516f341
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="f504f-103">Didacticiel : Intégration d’Azure Active Directory avec SAP Cloud pour le client</span><span class="sxs-lookup"><span data-stu-id="f504f-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="f504f-104">Dans ce didacticiel, vous allez apprendre à intégrer SAP Cloud pour le client à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f504f-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f504f-105">L’intégration de SAP Cloud pour le client à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f504f-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f504f-106">Dans Azure AD, vous pouvez contrôler qui a accès à SAP Cloud pour le client.</span><span class="sxs-lookup"><span data-stu-id="f504f-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="f504f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à SAP Cloud pour le client (via l’authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f504f-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f504f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f504f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f504f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f504f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f504f-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="f504f-110">Prerequisites</span></span>

<span data-ttu-id="f504f-111">Pour configurer l’intégration d’Azure AD avec SAP Cloud pour le client, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f504f-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="f504f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f504f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f504f-113">Un abonnement SAP Cloud for Customer pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f504f-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f504f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f504f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f504f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f504f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f504f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f504f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f504f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f504f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f504f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f504f-118">Scenario description</span></span>
<span data-ttu-id="f504f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f504f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f504f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="f504f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f504f-121">Ajout de SAP Cloud pour le client à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f504f-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="f504f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f504f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="f504f-123">Ajout de SAP Cloud pour le client à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f504f-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="f504f-124">Pour configurer l’intégration de SAP Cloud pour le client à Azure AD, vous devez ajouter SAP Cloud pour le client depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f504f-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f504f-125">**Pour ajouter SAP Cloud pour le client à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f504f-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f504f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f504f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f504f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f504f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f504f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f504f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f504f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f504f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f504f-133">Dans la zone de recherche, tapez **SAP Cloud pour le client**.</span><span class="sxs-lookup"><span data-stu-id="f504f-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="f504f-135">Dans le panneau de résultats, sélectionnez **SAP Cloud for Customer**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="f504f-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f504f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f504f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f504f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Cloud pour le client, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f504f-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f504f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SAP Cloud pour le client équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f504f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="f504f-140">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur SAP Cloud pour le client associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="f504f-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="f504f-141">Dans SAP Cloud pour le client, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Username** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="f504f-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f504f-142">Pour configurer et tester l’authentification unique Azure AD avec SAP Cloud pour le client, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="f504f-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f504f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f504f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f504f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f504f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f504f-145">**[Création d’un utilisateur de test SAP Cloud for Customer](#creating-a-sap-cloud-for-customer-test-user)** pour avoir un équivalent de Britta Simon dans SAP Cloud for Customer lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="f504f-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f504f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f504f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f504f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="f504f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f504f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f504f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f504f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="f504f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="f504f-150">**Pour configurer l’authentification unique Azure AD avec SAP Cloud pour le client, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f504f-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="f504f-151">Dans le portail Azure, sur la page d’intégration de l’application **SAP Cloud for Customer**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f504f-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f504f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f504f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="f504f-155">Dans la section **Domaine et URL SAP Cloud for Customer**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f504f-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="f504f-157">a.</span><span class="sxs-lookup"><span data-stu-id="f504f-157">a.</span></span> <span data-ttu-id="f504f-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="f504f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="f504f-159">b.</span><span class="sxs-lookup"><span data-stu-id="f504f-159">b.</span></span> <span data-ttu-id="f504f-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="f504f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f504f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f504f-161">These values are not real.</span></span> <span data-ttu-id="f504f-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="f504f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f504f-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique SAP Cloud for Customer](https://www.sap.com/about/agreements.sap-cloud-services-customers.html).</span><span class="sxs-lookup"><span data-stu-id="f504f-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

4. <span data-ttu-id="f504f-164">Dans la section **Attributs d’utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f504f-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="f504f-166">a.</span><span class="sxs-lookup"><span data-stu-id="f504f-166">a.</span></span> <span data-ttu-id="f504f-167">Dans la liste **Identificateur de l’utilisateur**, sélectionnez la fonction **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="f504f-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="f504f-168">b.</span><span class="sxs-lookup"><span data-stu-id="f504f-168">b.</span></span> <span data-ttu-id="f504f-169">Dans la liste **Courrier** , sélectionnez l’attribut utilisateur que vous souhaitez utiliser pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="f504f-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="f504f-170">Par exemple, si vous souhaitez utiliser EmployeeID comme identificateur d’utilisateur unique et que vous avez stocké la valeur d’attribut dans ExtensionAttribute2, sélectionnez user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="f504f-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="f504f-171">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f504f-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="f504f-173">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f504f-173">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f504f-175">Dans la section **Configuration de SAP Cloud for Customer**, cliquez sur **Configurer SAP Cloud pour le client** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="f504f-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f504f-176">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="f504f-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="f504f-178">Pour configurer l’authentification unique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f504f-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="f504f-179">a.</span><span class="sxs-lookup"><span data-stu-id="f504f-179">a.</span></span> <span data-ttu-id="f504f-180">Connectez-vous au portail SAP Cloud pour le client avec des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f504f-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="f504f-181">b.</span><span class="sxs-lookup"><span data-stu-id="f504f-181">b.</span></span> <span data-ttu-id="f504f-182">Accédez à **Application and User Management Common Task** (Tâche courante d’application et de gestion des utilisateurs) et cliquez sur l’onglet **Identity Provider** (Fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="f504f-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="f504f-183">c.</span><span class="sxs-lookup"><span data-stu-id="f504f-183">c.</span></span> <span data-ttu-id="f504f-184">Cliquez sur **New Identity Provider** (Nouveau fournisseur d’identité) et sélectionnez le fichier XML de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f504f-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="f504f-185">En important les métadonnées, le système charge automatiquement le certificat de signature ainsi que le certificat de chiffrement requis.</span><span class="sxs-lookup"><span data-stu-id="f504f-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="f504f-187">d.</span><span class="sxs-lookup"><span data-stu-id="f504f-187">d.</span></span> <span data-ttu-id="f504f-188">Azure Active Directory nécessitant l’URL Assertion Consumer Service dans la requête SAML, cochez la case **Include Assertion Consumer Service URL** (Inclure l’URL Assertion Consumer Service).</span><span class="sxs-lookup"><span data-stu-id="f504f-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="f504f-189">e.</span><span class="sxs-lookup"><span data-stu-id="f504f-189">e.</span></span> <span data-ttu-id="f504f-190">Cliquez sur **Activate Single Sign-On**(Activer l’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="f504f-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="f504f-191">f.</span><span class="sxs-lookup"><span data-stu-id="f504f-191">f.</span></span> <span data-ttu-id="f504f-192">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="f504f-192">Save your changes.</span></span>
   
    <span data-ttu-id="f504f-193">g.</span><span class="sxs-lookup"><span data-stu-id="f504f-193">g.</span></span> <span data-ttu-id="f504f-194">Cliquez sur l’onglet **My System** (Mon système).</span><span class="sxs-lookup"><span data-stu-id="f504f-194">Click the **My System** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="f504f-196">h.</span><span class="sxs-lookup"><span data-stu-id="f504f-196">h.</span></span> <span data-ttu-id="f504f-197">Dans la zone de texte **Azure AD Sign On URL** (URL de connexion Azure AD), collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f504f-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="f504f-199">i.</span><span class="sxs-lookup"><span data-stu-id="f504f-199">i.</span></span> <span data-ttu-id="f504f-200">Précisez si l’employé peut choisir manuellement entre l’authentification à l’aide d’un ID d’utilisateur/mot de passe ou l’authentification unique en cliquant sur **Manual Identity Provider Selection**(Sélection manuelle du fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="f504f-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="f504f-201">j.</span><span class="sxs-lookup"><span data-stu-id="f504f-201">j.</span></span> <span data-ttu-id="f504f-202">Dans la section **URL SSO** , spécifiez l’URL devant être utilisée par vos employés pour se connecter au système.</span><span class="sxs-lookup"><span data-stu-id="f504f-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="f504f-203">Dans la liste **URL Sent to Employee** (URL envoyée à l’employé), vous pouvez choisir entre les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="f504f-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="f504f-204">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="f504f-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="f504f-205">Le système envoie uniquement l’URL du système normale à l’employé.</span><span class="sxs-lookup"><span data-stu-id="f504f-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="f504f-206">L’employé ne peut pas se connecter à l’aide de l’authentification unique ; il doit donc utiliser un mot de passe ou un certificat.</span><span class="sxs-lookup"><span data-stu-id="f504f-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="f504f-207">**URL SSO**</span><span class="sxs-lookup"><span data-stu-id="f504f-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="f504f-208">Le système envoie uniquement l’URL SSO à l’employé.</span><span class="sxs-lookup"><span data-stu-id="f504f-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="f504f-209">L’employé peut se connecter à l’aide de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f504f-209">The employee can log on using SSO.</span></span> <span data-ttu-id="f504f-210">La demande d’authentification est redirigée via l’IdP.</span><span class="sxs-lookup"><span data-stu-id="f504f-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="f504f-211">**Sélection automatique**</span><span class="sxs-lookup"><span data-stu-id="f504f-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="f504f-212">Si l’authentification unique n’est pas activée, le système envoie l’URL du système normale à l’employé.</span><span class="sxs-lookup"><span data-stu-id="f504f-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="f504f-213">Si l’authentification unique est activée, le système vérifie si l’employé possède un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f504f-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="f504f-214">Le cas échéant, les URL SSO et les URL non SSO sont envoyées à l’employé.</span><span class="sxs-lookup"><span data-stu-id="f504f-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="f504f-215">Toutefois, si l’employé ne possède aucun mot de passe, seule l’URL SSO est envoyée à l’employé.</span><span class="sxs-lookup"><span data-stu-id="f504f-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="f504f-216">k.</span><span class="sxs-lookup"><span data-stu-id="f504f-216">k.</span></span> <span data-ttu-id="f504f-217">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="f504f-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="f504f-218">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="f504f-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f504f-219">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="f504f-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f504f-220">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f504f-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f504f-221">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f504f-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="f504f-222">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f504f-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f504f-224">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f504f-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f504f-225">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f504f-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f504f-227">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f504f-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f504f-229">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f504f-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f504f-231">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f504f-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f504f-233">a.</span><span class="sxs-lookup"><span data-stu-id="f504f-233">a.</span></span> <span data-ttu-id="f504f-234">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f504f-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f504f-235">b.</span><span class="sxs-lookup"><span data-stu-id="f504f-235">b.</span></span> <span data-ttu-id="f504f-236">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f504f-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f504f-237">c.</span><span class="sxs-lookup"><span data-stu-id="f504f-237">c.</span></span> <span data-ttu-id="f504f-238">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f504f-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f504f-239">d.</span><span class="sxs-lookup"><span data-stu-id="f504f-239">d.</span></span> <span data-ttu-id="f504f-240">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f504f-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="f504f-241">Création d’un utilisateur de test SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="f504f-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="f504f-242">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SAP Cloud pour le client.</span><span class="sxs-lookup"><span data-stu-id="f504f-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="f504f-243">Collaborez avec l’[équipe de support technique SAP Cloud for Customer](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) pour ajouter les utilisateurs dans la plateforme SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="f504f-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="f504f-244">Assurez-vous que la valeur NameID correspond au champ de nom d’utilisateur dans la plateforme SAP Cloud pour le client.</span><span class="sxs-lookup"><span data-stu-id="f504f-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f504f-245">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f504f-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f504f-246">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SAP Cloud for Customer.</span><span class="sxs-lookup"><span data-stu-id="f504f-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f504f-248">**Pour affecter Britta Simon à SAP Cloud pour le client, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f504f-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="f504f-249">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f504f-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f504f-251">Dans la liste des applications, sélectionnez **Cloud SAP pour le client**.</span><span class="sxs-lookup"><span data-stu-id="f504f-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="f504f-253">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f504f-253">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f504f-255">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f504f-255">Click **Add** button.</span></span> <span data-ttu-id="f504f-256">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f504f-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f504f-258">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f504f-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f504f-259">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f504f-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f504f-260">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f504f-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f504f-261">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f504f-261">Testing single sign-on</span></span>

<span data-ttu-id="f504f-262">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="f504f-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f504f-263">Lorsque vous cliquez sur la vignette SAP Cloud pour le client dans le volet d’accès, vous devez être connecté automatiquement à votre application SAP Cloud pour le client.</span><span class="sxs-lookup"><span data-stu-id="f504f-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="f504f-264">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f504f-264">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f504f-265">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f504f-265">Additional resources</span></span>

* [<span data-ttu-id="f504f-266">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f504f-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f504f-267">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f504f-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

