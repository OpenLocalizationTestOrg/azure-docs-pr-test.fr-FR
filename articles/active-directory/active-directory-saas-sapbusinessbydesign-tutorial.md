---
title: "Didacticiel : intégration d’Azure Active Directory à SAP Business ByDesign | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="5c444-103">Didacticiel : Intégration d’Azure Active Directory à SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="5c444-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="5c444-104">Dans ce didacticiel, vous allez apprendre à intégrer SAP Business ByDesign à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c444-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c444-105">L’intégration de SAP Business ByDesign à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5c444-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c444-106">Dans Azure AD, vous pouvez déterminer qui a accès à SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="5c444-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="5c444-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à SAP Business ByDesign (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c444-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5c444-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c444-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5c444-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c444-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c444-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5c444-110">Prerequisites</span></span>

<span data-ttu-id="5c444-111">Pour configurer l’intégration d’Azure AD avec SAP Business ByDesign, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5c444-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="5c444-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c444-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c444-113">Un abonnement SAP Business ByDesign pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5c444-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c444-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5c444-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c444-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5c444-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c444-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5c444-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c444-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c444-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c444-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5c444-118">Scenario description</span></span>
<span data-ttu-id="5c444-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5c444-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c444-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c444-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c444-121">Ajouter SAP Business ByDesign à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5c444-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="5c444-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c444-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="5c444-123">Ajouter SAP Business ByDesign à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5c444-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="5c444-124">Pour configurer l’intégration de SAP Business ByDesign à Azure AD, vous devez ajouter SAP Business ByDesign depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5c444-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c444-125">**Pour ajouter SAP Business ByDesign à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c444-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c444-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c444-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="5c444-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5c444-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c444-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5c444-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="5c444-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5c444-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="5c444-133">Dans la zone de recherche, saisissez **SAP Business ByDesign.**, sélectionnez **SAP Business ByDesign.** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5c444-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign dans la liste des résultats](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5c444-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c444-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5c444-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Business ByDesign, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5c444-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c444-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SAP Business ByDesign équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c444-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="5c444-138">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur SAP Business ByDesign associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="5c444-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="5c444-139">Dans SAP Business ByDesign, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="5c444-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c444-140">Pour configurer et tester l’authentification unique Azure AD avec SAP Business ByDesign, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c444-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c444-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5c444-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c444-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c444-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c444-143">**[Créer un utilisateur de test SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)** pour avoir un équivalent de Britta Simon dans SAP Business ByDesign, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="5c444-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c444-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c444-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c444-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5c444-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5c444-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c444-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5c444-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="5c444-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="5c444-148">**Pour configurer l’authentification unique Azure AD avec SAP Business ByDesign, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c444-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="5c444-149">Dans le portail Azure, dans la page d’intégration de l’application **SAP Business ByDesign**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5c444-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="5c444-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5c444-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="5c444-153">Dans la section **Domaine et URL SAP Business ByDesign**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c444-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans la section Domaine et URL SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="5c444-155">a.</span><span class="sxs-lookup"><span data-stu-id="5c444-155">a.</span></span> <span data-ttu-id="5c444-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="5c444-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="5c444-157">b.</span><span class="sxs-lookup"><span data-stu-id="5c444-157">b.</span></span> <span data-ttu-id="5c444-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="5c444-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c444-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5c444-159">These values are not real.</span></span> <span data-ttu-id="5c444-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="5c444-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5c444-161">Pour obtenir ces valeurs, contactez [l’équipe de support technique SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="5c444-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="5c444-162">Dans la section **Attributs d’utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c444-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![Section d’attribut de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="5c444-164">a.</span><span class="sxs-lookup"><span data-stu-id="5c444-164">a.</span></span> <span data-ttu-id="5c444-165">Dans la liste **Identificateur de l’utilisateur**, sélectionnez la fonction **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="5c444-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="5c444-166">b.</span><span class="sxs-lookup"><span data-stu-id="5c444-166">b.</span></span> <span data-ttu-id="5c444-167">Dans la liste **Courrier** , sélectionnez l’attribut utilisateur que vous souhaitez utiliser pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="5c444-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="5c444-168">Par exemple, si vous souhaitez utiliser EmployeeID comme identificateur d’utilisateur unique et que vous avez stocké la valeur d’attribut dans ExtensionAttribute2, sélectionnez user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="5c444-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="5c444-169">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5c444-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="5c444-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5c444-171">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5c444-173">Dans la section **Configuration de SAP Business ByDesign**, cliquez sur **Configurer SAP Business ByDesign** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="5c444-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5c444-174">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="5c444-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="5c444-176">Pour configurer l’authentification unique pour votre application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c444-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="5c444-177">a.</span><span class="sxs-lookup"><span data-stu-id="5c444-177">a.</span></span> <span data-ttu-id="5c444-178">Connectez-vous à votre portail SAP Business ByDesign avec des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5c444-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="5c444-179">b.</span><span class="sxs-lookup"><span data-stu-id="5c444-179">b.</span></span> <span data-ttu-id="5c444-180">Accédez à **Application and User Management Common Task (Tâche courante d’application et de gestion des utilisateurs)** et cliquez sur l’onglet **Identity Provider (Fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="5c444-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="5c444-181">c.</span><span class="sxs-lookup"><span data-stu-id="5c444-181">c.</span></span> <span data-ttu-id="5c444-182">Cliquez sur **New Identity Provider** (Nouveau fournisseur d’identité) et sélectionnez le fichier XML de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c444-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="5c444-183">En important les métadonnées, le système charge automatiquement le certificat de signature ainsi que le certificat de chiffrement requis.</span><span class="sxs-lookup"><span data-stu-id="5c444-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="5c444-185">d.</span><span class="sxs-lookup"><span data-stu-id="5c444-185">d.</span></span> <span data-ttu-id="5c444-186">Pour inclure **l’URL Assertion Consumer Service** dans la requête SAML, sélectionnez **Include Assertion Consumer Service URL (Inclure l’URL Assertion Consumer Service)**.</span><span class="sxs-lookup"><span data-stu-id="5c444-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="5c444-187">e.</span><span class="sxs-lookup"><span data-stu-id="5c444-187">e.</span></span> <span data-ttu-id="5c444-188">Cliquez sur **Activate Single Sign-On**(Activer l’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="5c444-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="5c444-189">f.</span><span class="sxs-lookup"><span data-stu-id="5c444-189">f.</span></span> <span data-ttu-id="5c444-190">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="5c444-190">Save your changes.</span></span>
   
    <span data-ttu-id="5c444-191">g.</span><span class="sxs-lookup"><span data-stu-id="5c444-191">g.</span></span> <span data-ttu-id="5c444-192">Cliquez sur l’onglet **My System** (Mon système).</span><span class="sxs-lookup"><span data-stu-id="5c444-192">Click the **My System** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="5c444-194">h.</span><span class="sxs-lookup"><span data-stu-id="5c444-194">h.</span></span> <span data-ttu-id="5c444-195">Dans la zone de texte de **l’URL du service d’authentification unique Azure AD**, collez **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c444-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="5c444-197">i.</span><span class="sxs-lookup"><span data-stu-id="5c444-197">i.</span></span> <span data-ttu-id="5c444-198">Précisez si l’employé peut choisir manuellement entre l’authentification à l’aide d’un ID d’utilisateur/mot de passe ou l’authentification unique en cliquant sur **Manual Identity Provider Selection**(Sélection manuelle du fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="5c444-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="5c444-199">j.</span><span class="sxs-lookup"><span data-stu-id="5c444-199">j.</span></span> <span data-ttu-id="5c444-200">Dans la section **URL SSO** , spécifiez l’URL devant être utilisée par l’employé pour se connecter au système.</span><span class="sxs-lookup"><span data-stu-id="5c444-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="5c444-201">Dans la liste déroulante URL Sent to Employee (URL envoyée à l’employé), vous pouvez choisir entre les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="5c444-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="5c444-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="5c444-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="5c444-203">Le système envoie uniquement l’URL du système normale à l’employé.</span><span class="sxs-lookup"><span data-stu-id="5c444-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="5c444-204">L’employé ne peut pas se connecter à l’aide de l’authentification unique ; il doit donc utiliser un mot de passe ou un certificat.</span><span class="sxs-lookup"><span data-stu-id="5c444-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="5c444-205">**URL SSO**</span><span class="sxs-lookup"><span data-stu-id="5c444-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="5c444-206">Le système envoie uniquement l’URL SSO à l’employé.</span><span class="sxs-lookup"><span data-stu-id="5c444-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="5c444-207">L’employé peut se connecter à l’aide de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5c444-207">The employee can log on using SSO.</span></span> <span data-ttu-id="5c444-208">La demande d’authentification est redirigée via l’IdP.</span><span class="sxs-lookup"><span data-stu-id="5c444-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="5c444-209">**Sélection automatique**</span><span class="sxs-lookup"><span data-stu-id="5c444-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="5c444-210">Si l’authentification unique n’est pas activée, le système envoie l’URL du système normale à l’employé.</span><span class="sxs-lookup"><span data-stu-id="5c444-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="5c444-211">Si l’authentification unique est activée, le système vérifie si l’employé possède un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5c444-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="5c444-212">Le cas échéant, les URL SSO et les URL non SSO sont envoyées à l’employé.</span><span class="sxs-lookup"><span data-stu-id="5c444-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="5c444-213">Toutefois, si l’employé ne possède aucun mot de passe, seule l’URL SSO est envoyée à l’employé.</span><span class="sxs-lookup"><span data-stu-id="5c444-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="5c444-214">k.</span><span class="sxs-lookup"><span data-stu-id="5c444-214">k.</span></span> <span data-ttu-id="5c444-215">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="5c444-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="5c444-216">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5c444-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c444-217">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5c444-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c444-218">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c444-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5c444-219">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c444-219">Create an Azure AD test user</span></span>

<span data-ttu-id="5c444-220">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c444-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="5c444-222">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c444-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c444-223">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c444-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5c444-225">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5c444-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5c444-227">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5c444-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5c444-229">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5c444-229">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5c444-231">a.</span><span class="sxs-lookup"><span data-stu-id="5c444-231">a.</span></span> <span data-ttu-id="5c444-232">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c444-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c444-233">b.</span><span class="sxs-lookup"><span data-stu-id="5c444-233">b.</span></span> <span data-ttu-id="5c444-234">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c444-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="5c444-235">c.</span><span class="sxs-lookup"><span data-stu-id="5c444-235">c.</span></span> <span data-ttu-id="5c444-236">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5c444-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="5c444-237">d.</span><span class="sxs-lookup"><span data-stu-id="5c444-237">d.</span></span> <span data-ttu-id="5c444-238">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5c444-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="5c444-239">Créer un utilisateur de test pour SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="5c444-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="5c444-240">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="5c444-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="5c444-241">Veuillez contacter [l’équipe de prise en charge des clients de SAP Business ByDesign](https://www.sap.com/products/cloud-analytics.support.html) pour ajouter des utilisateurs sur la plateforme SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="5c444-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="5c444-242">Assurez-vous que la valeur NameID correspond au champ de nom d’utilisateur dans la plateforme SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="5c444-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5c444-243">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c444-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="5c444-244">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="5c444-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Assigner le rôle d’utilisateur][200] 

<span data-ttu-id="5c444-246">**Pour affecter Britta Simon à SAP Business ByDesign, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5c444-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="5c444-247">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5c444-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5c444-249">Dans la liste des applications, sélectionnez **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="5c444-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![Lien correspondant à SAP Business ByDesign dans la liste des applications](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="5c444-251">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5c444-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="5c444-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c444-253">Click **Add** button.</span></span> <span data-ttu-id="5c444-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5c444-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="5c444-256">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5c444-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c444-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5c444-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c444-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5c444-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5c444-259">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5c444-259">Test single sign-on</span></span>

<span data-ttu-id="5c444-260">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5c444-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c444-261">Lorsque vous cliquez sur la vignette SAP Business ByDesign dans le volet d’accès, vous devez être connecté automatiquement à votre application SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="5c444-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c444-262">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5c444-262">Additional resources</span></span>

* [<span data-ttu-id="5c444-263">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c444-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c444-264">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5c444-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

