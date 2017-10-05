---
title: "Didacticiel : Intégration d’Azure Active Directory avec le logiciel Cezanne HR | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et le logiciel Cezanne HR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 623c438edfce5f98c2d32d8bb25a97d86aa77909
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="80b5b-103">Didacticiel : Intégration d’Azure Active Directory avec le logiciel Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="80b5b-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="80b5b-104">Dans ce didacticiel, vous allez apprendre à intégrer le logiciel Cezanne HR avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80b5b-104">In this tutorial, you learn how to integrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80b5b-105">L’intégration du logiciel Cezanne HR dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="80b5b-105">Integrating Cezanne HR software with Azure AD provides you with the following benefits.</span></span> <span data-ttu-id="80b5b-106">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="80b5b-106">You can:</span></span>

- <span data-ttu-id="80b5b-107">contrôler, dans Azure AD, qui a accès au logiciel Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="80b5b-107">Control in Azure AD who has access to Cezanne HR software.</span></span>
- <span data-ttu-id="80b5b-108">autoriser les utilisateurs à se connecter automatiquement au logiciel Cezanne HR (par le biais d’une authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80b5b-108">Enable your users to automatically sign in to Cezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="80b5b-109">gérer vos comptes à un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="80b5b-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="80b5b-110">Pour en savoir plus sur l’intégration d’applications SaaS (software as a service) dans Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80b5b-110">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80b5b-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="80b5b-111">Prerequisites</span></span>

<span data-ttu-id="80b5b-112">Pour configurer l’intégration d’Azure AD avec le logiciel Cezanne HR, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="80b5b-112">To configure Azure AD integration with Cezanne HR software, you need the following items:</span></span>

- <span data-ttu-id="80b5b-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="80b5b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="80b5b-114">Un abonnement au logiciel Cezanne HR pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="80b5b-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80b5b-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="80b5b-115">To test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="80b5b-116">Pour tester la procédure de ce didacticiel, suivez les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="80b5b-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="80b5b-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="80b5b-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80b5b-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80b5b-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80b5b-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="80b5b-119">Scenario description</span></span>
<span data-ttu-id="80b5b-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="80b5b-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="80b5b-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="80b5b-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="80b5b-122">Ajout du logiciel Cezanne HR à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="80b5b-122">Adding Cezanne HR software from the gallery</span></span>
* <span data-ttu-id="80b5b-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="80b5b-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-the-gallery"></a><span data-ttu-id="80b5b-124">Ajouter le logiciel Cezanne HR à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="80b5b-124">Add Cezanne HR software from the gallery</span></span>
<span data-ttu-id="80b5b-125">Pour configurer l’intégration du logiciel Cezanne HR avec Azure AD, ajoutez le logiciel Cezanne HR, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="80b5b-125">To configure the integration of Cezanne HR software into Azure AD, add Cezanne HR software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="80b5b-126">Pour ajouter le logiciel Cezanne HR à partir de la galerie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80b5b-126">To add Cezanne HR software from the gallery, do the following:</span></span>

1. <span data-ttu-id="80b5b-127">Dans le volet gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-127">In the **[Azure portal](https://portal.azure.com)**, in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Le bouton « Azure Active Directory »][1]

2. <span data-ttu-id="80b5b-129">Sélectionnez **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Lien Toutes les applications][2]
    
3. <span data-ttu-id="80b5b-131">Pour ajouter une application, en haut de la boîte de dialogue **Toutes les applications**, sélectionnez **Nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-131">To add a new application, at the top of the **All applications** dialog box, select **New application**.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="80b5b-133">Dans la zone de recherche, entrez **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-133">In the search box, type **Cezanne HR Software**.</span></span>

    ![La zone de recherche](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="80b5b-135">Dans la liste des résultats, sélectionnez **Cezanne HR Software**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="80b5b-135">In the results list, select **Cezanne HR Software** and then select the **Add** button to add the application.</span></span>

    ![Liste des résultats](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="80b5b-137">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="80b5b-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="80b5b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec le logiciel Cezanne HR, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="80b5b-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="80b5b-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’équivalent du logiciel Cezanne HR pour l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80b5b-139">For SSO to work, Azure AD needs to know the Cezanne HR software counterpart to the Azure AD user.</span></span> <span data-ttu-id="80b5b-140">En d’autres termes, vous devez établir un lien entre un utilisateur Azure AD et l’utilisateur du logiciel Cezanne HR associé.</span><span class="sxs-lookup"><span data-stu-id="80b5b-140">In other words, you must establish a link relationship between an Azure AD user and the related user in the Cezanne HR software.</span></span>

<span data-ttu-id="80b5b-141">Pour établir cette relation, assignez la valeur du **nom d’utilisateur** du logiciel Cezanne HR en tant que valeur de **nom d’utilisateur** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80b5b-141">To establish the link relationship, assign the Cezanne HR software **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="80b5b-142">Pour configurer et tester l’authentification unique Azure AD avec le logiciel Cezanne HR, conformez-vous aux indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="80b5b-142">To configure and test Azure AD SSO by using Cezanne HR software, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="80b5b-143">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="80b5b-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="80b5b-144">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et la configurer dans votre application logicielle Cezanne HR en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="80b5b-144">In this section, you can enable Azure AD SSO in the Azure portal and configure SSO in your Cezanne HR software application by doing the following:</span></span>

1. <span data-ttu-id="80b5b-145">Sur le portail Azure, dans la page d’intégration de l’application **Cezanne HR Software**, sélectionnez **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-145">In the Azure portal, on the **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Commande Authentification unique][4]

2. <span data-ttu-id="80b5b-147">Pour activer l’authentification unique, dans la boîte de dialogue **Authentification unique**, sous la zone **Mode**, sélectionnez **Authentification basée sur SAML**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-147">To enable SSO, in the **Single sign-on** dialog box, select the **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Zone Mode](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="80b5b-149">Sous **Domaine et URL Cezanne HR Software**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80b5b-149">Under **Cezanne HR Software Domain and URLs**, do the following:</span></span>

    ![Section Domaine et URL Cezanne HR Software](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="80b5b-151">a.</span><span class="sxs-lookup"><span data-stu-id="80b5b-151">a.</span></span> <span data-ttu-id="80b5b-152">Dans la zone de texte **URL de connexion**, tapez une URL dont la syntaxe est la suivante : `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="80b5b-152">In the **Sign-on URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="80b5b-153">b.</span><span class="sxs-lookup"><span data-stu-id="80b5b-153">b.</span></span> <span data-ttu-id="80b5b-154">Dans la zone de texte **URL de réponse**, tapez une URL dont la syntaxe est la suivante : `https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="80b5b-154">In the **Reply URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="80b5b-155">Les valeurs ci-dessus ne sont pas réelles.</span><span class="sxs-lookup"><span data-stu-id="80b5b-155">The preceding values are not real.</span></span> <span data-ttu-id="80b5b-156">Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles.</span><span class="sxs-lookup"><span data-stu-id="80b5b-156">Update them with the actual reply URL and the sign-on URL.</span></span> <span data-ttu-id="80b5b-157">Pour obtenir ces valeurs, contactez [l’équipe du support technique du logiciel Cezanne HR](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="80b5b-157">To obtain the values, contact the [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="80b5b-158">Sous **Certificat de signature SAML**, sélectionnez **Certificat (en base64)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="80b5b-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="80b5b-160">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-160">Select **Save**.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="80b5b-162">Sous **Configuration de Cezanne HR Software**, sélectionnez **Configurer Cezanne HR Software** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="80b5b-163">Copiez l’**ID d’entité SAML** et l’URL du **service d’authentification unique SAML** à partir de la section **Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-163">Copy the **SAML Entity ID** and **SAML Single Sign-On Service** URL from the **Quick Reference** section.</span></span>

    ![Section Configuration de Cezanne HR Software](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="80b5b-165">Dans une autre fenêtre de navigateur web, connectez-vous à votre locataire du logiciel Cezanne HR en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="80b5b-165">In a different web browser window, sign on to your Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="80b5b-166">Dans le volet gauche, sélectionnez **Paramétrage du système**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-166">In the left pane, select **System Setup**.</span></span> <span data-ttu-id="80b5b-167">Sélectionnez **Paramètres de sécurité** > **Configuration d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![Lien Configuration d’authentification unique](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="80b5b-169">Dans le volet **Autoriser les utilisateurs à se connecter à l’aide de l’authentification unique**, cochez la case **SAML 2.0** et sélectionnez l’option **Configuration avancée**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-169">In the **Allow users to log in using the following Single Sign-On (SSO) services** pane, select the **SAML 2.0** check box and select the **Advanced Configuration** option.</span></span>

    ![Options des services d’authentification unique](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="80b5b-171">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-171">Select **Add New**.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="80b5b-173">Sous **SAML 2.0 Identity Providers**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80b5b-173">Under **SAML 2.0 Identity Providers**, do the following:</span></span>

    ![Section SAML 2.0 Identity Providers](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="80b5b-175">a.</span><span class="sxs-lookup"><span data-stu-id="80b5b-175">a.</span></span> <span data-ttu-id="80b5b-176">Dans la zone **Nom affiché**, entrez le nom de votre fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="80b5b-176">In the **Display Name** box, enter the name of your identity provider.</span></span>

    <span data-ttu-id="80b5b-177">b.</span><span class="sxs-lookup"><span data-stu-id="80b5b-177">b.</span></span> <span data-ttu-id="80b5b-178">Dans la zone de texte **Identificateur d’identité**, collez l’**ID d’entité SAML** copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="80b5b-178">In the **Entity Identifier** box, paste the **SAML Entity ID** that you copied from the Azure portal.</span></span> 

    <span data-ttu-id="80b5b-179">c.</span><span class="sxs-lookup"><span data-stu-id="80b5b-179">c.</span></span> <span data-ttu-id="80b5b-180">Dans la zone de liste **SAML Binding** (Liaison SAML), sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-180">In the **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="80b5b-181">d.</span><span class="sxs-lookup"><span data-stu-id="80b5b-181">d.</span></span> <span data-ttu-id="80b5b-182">Dans la zone de texte **Point de terminaison de service du jeton de sécurité**, collez l’URL du **service d’authentification unique SAML** que vous avez copiée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="80b5b-182">In the **Security Token Service Endpoint** box, paste the **SAML Single Sign-On Service** URL that you copied from the Azure portal.</span></span> 
    
    <span data-ttu-id="80b5b-183">e.</span><span class="sxs-lookup"><span data-stu-id="80b5b-183">e.</span></span> <span data-ttu-id="80b5b-184">Dans la zone de texte **Nom d’attribut de l’ID d’utilisateur**, entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="80b5b-184">In the **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="80b5b-185">f.</span><span class="sxs-lookup"><span data-stu-id="80b5b-185">f.</span></span> <span data-ttu-id="80b5b-186">Pour charger le certificat obtenu auprès d’Azure AD, cliquez sur le bouton **Charger**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-186">To upload the downloaded certificate from Azure AD, select the **Upload** button.</span></span>
    
    <span data-ttu-id="80b5b-187">g.</span><span class="sxs-lookup"><span data-stu-id="80b5b-187">g.</span></span> <span data-ttu-id="80b5b-188">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-188">Select **OK**.</span></span> 

12. <span data-ttu-id="80b5b-189">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-189">Select **Save**.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="80b5b-191">Lors de la configuration de l’application, vous pouvez lire une version abrégée des instructions précédentes sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="80b5b-191">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="80b5b-192">Après avoir ajouté cette application à partir de la section **Active Directory** > **Applications d’entreprise**, sélectionnez l’onglet **Authentification unique**. Ensuite, accédez à la documentation incorporée par le biais de la section **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-192">After you add the app from the **Active Directory** > **Enterprise applications** section, select the **Single sign-on** tab. Then access the embedded documentation from the **Configuration** section.</span></span> 

<span data-ttu-id="80b5b-193">Pour en savoir plus sur la fonctionnalité de documentation incorporée, consultez la [documentation incorporée d’Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="80b5b-193">To learn more about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="80b5b-194">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="80b5b-194">Create an Azure AD test user</span></span>
<span data-ttu-id="80b5b-195">Dans cette section, vous allez créer un utilisateur de test nommé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="80b5b-195">In this section, you create test user Britta Simon in the Azure portal.</span></span>

![Utilisateur de test Britta Simon][100]

<span data-ttu-id="80b5b-197">Pour créer un utilisateur de test dans Azure AD, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="80b5b-197">To create a test user in Azure AD, do the following:</span></span>

1. <span data-ttu-id="80b5b-198">Dans le volet gauche du **portail Azure**, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-198">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Le bouton « Azure Active Directory »](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80b5b-200">Pour afficher la liste des utilisateurs, sélectionnez **Utilisateurs et groupes** > **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-200">To display the list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Lien Tous les utilisateurs](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="80b5b-202">La boîte de dialogue **Tous les utilisateurs** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="80b5b-202">The **All users** dialog box opens.</span></span>

3. <span data-ttu-id="80b5b-203">Pour ouvrir la boîte de dialogue **Utilisateur**, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-203">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Bouton « Ajouter »](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80b5b-205">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80b5b-205">In the **User** dialog box, do the following:</span></span>
 
    ![La boîte de dialogue « Utilisateur »](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80b5b-207">a.</span><span class="sxs-lookup"><span data-stu-id="80b5b-207">a.</span></span> <span data-ttu-id="80b5b-208">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80b5b-209">b.</span><span class="sxs-lookup"><span data-stu-id="80b5b-209">b.</span></span> <span data-ttu-id="80b5b-210">Dans la zone **Nom d’utilisateur**, tapez l’**adresse e-mail** de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80b5b-210">In the **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="80b5b-211">c.</span><span class="sxs-lookup"><span data-stu-id="80b5b-211">c.</span></span> <span data-ttu-id="80b5b-212">Cochez la case **Afficher le mot de passe**, puis notez la valeur générée dans la zone **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-212">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="80b5b-213">d.</span><span class="sxs-lookup"><span data-stu-id="80b5b-213">d.</span></span> <span data-ttu-id="80b5b-214">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="80b5b-215">Créer un utilisateur de test pour le logiciel Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="80b5b-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="80b5b-216">Pour permettre aux utilisateurs Azure AD de se connecter au logiciel Cezanne HR, vous devez les approvisionner dans le logiciel Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="80b5b-216">To enable Azure AD users to sign in to Cezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="80b5b-217">Dans le cas du logiciel Cezanne HR, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="80b5b-217">In the case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="80b5b-218">Pour approvisionner un compte d’utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80b5b-218">Provision a user account by doing the following:</span></span>

1.  <span data-ttu-id="80b5b-219">Connectez-vous au site d’entreprise du logiciel Cezanne HR en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="80b5b-219">Sign in to your Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="80b5b-220">Dans le volet gauche, sélectionnez **Paramétrage du système** > **Gérer les utilisateurs** > **Ajouter un nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-220">In the left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="80b5b-221">![Lien Ajouter un nouvel utilisateur](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="80b5b-221">![The "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="80b5b-222">Sous **Détails du candidat**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80b5b-222">Under **Person Details**, do the following:</span></span>

    <span data-ttu-id="80b5b-223">![Section Détails du candidat](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="80b5b-223">![The "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="80b5b-224">a.</span><span class="sxs-lookup"><span data-stu-id="80b5b-224">a.</span></span> <span data-ttu-id="80b5b-225">Paramétrez **Utilisateur interne** sur **Désactivé**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="80b5b-226">b.</span><span class="sxs-lookup"><span data-stu-id="80b5b-226">b.</span></span> <span data-ttu-id="80b5b-227">Dans la zone **Prénom** , tapez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-227">In the **First Name** box, type the user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="80b5b-228">c.</span><span class="sxs-lookup"><span data-stu-id="80b5b-228">c.</span></span> <span data-ttu-id="80b5b-229">Dans la zone **Nom** , tapez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-229">In the **Last Name** box, type the user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="80b5b-230">d.</span><span class="sxs-lookup"><span data-stu-id="80b5b-230">d.</span></span> <span data-ttu-id="80b5b-231">Dans la zone **E-mail**, tapez l’adresse e-mail de l’utilisateur, par exemple Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="80b5b-231">In the **E-mail** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="80b5b-232">Sous **Informations sur le compte**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80b5b-232">Under **Account Information**, do the following:</span></span>

    <span data-ttu-id="80b5b-233">![Section Informations sur le compte](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="80b5b-233">![The "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="80b5b-234">a.</span><span class="sxs-lookup"><span data-stu-id="80b5b-234">a.</span></span> <span data-ttu-id="80b5b-235">Dans la zone **Nom d’utilisateur**, tapez l’adresse e-mail de l’utilisateur, par exemple Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="80b5b-235">In the **Username** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="80b5b-236">b.</span><span class="sxs-lookup"><span data-stu-id="80b5b-236">b.</span></span> <span data-ttu-id="80b5b-237">Dans la zone **Mot de passe**, entrez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="80b5b-237">In the **Password** box, type the user's password.</span></span>
    
    <span data-ttu-id="80b5b-238">c.</span><span class="sxs-lookup"><span data-stu-id="80b5b-238">c.</span></span> <span data-ttu-id="80b5b-239">Dans la zone **Rôle de sécurité**, sélectionnez **Professionnel des RH**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-239">In the **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="80b5b-240">d.</span><span class="sxs-lookup"><span data-stu-id="80b5b-240">d.</span></span> <span data-ttu-id="80b5b-241">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-241">Select **OK**.</span></span>

5. <span data-ttu-id="80b5b-242">Dans l’onglet **Authentification unique**, sous la section **Identificateurs SAML 2.0**, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-242">On the **Single sign-on** tab, in the **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="80b5b-243">![Bouton Ajouter](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "Utilisateur")</span><span class="sxs-lookup"><span data-stu-id="80b5b-243">![The "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="80b5b-244">Dans la zone de liste **Fournisseur d’identité**, sélectionnez votre fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="80b5b-244">In the **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="80b5b-245">Dans la zone **Identificateur d’utilisateur**, entrez l’adresse e-mail du compte de test de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="80b5b-245">In the **User Identifier** box, enter the email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="80b5b-246">![Zones Fournisseur d’identité et Identificateur d’utilisateur](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "Utilisateur")</span><span class="sxs-lookup"><span data-stu-id="80b5b-246">![The "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="80b5b-247">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-247">Select **Save**.</span></span>

    <span data-ttu-id="80b5b-248">![Bouton Enregistrer](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "Utilisateur")</span><span class="sxs-lookup"><span data-stu-id="80b5b-248">![The "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="80b5b-249">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="80b5b-249">Assign the Azure AD test user</span></span>

<span data-ttu-id="80b5b-250">Dans cette section, vous allez autoriser l’utilisateur de test Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès au logiciel Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="80b5b-250">In this section, you enable test user Britta Simon to use Azure SSO by granting access to Cezanne HR software.</span></span>

![Accès de l’utilisateur de test][200] 

1. <span data-ttu-id="80b5b-252">Dans le portail Azure, ouvrez la vue des applications, puis accédez à la vue des répertoires.</span><span class="sxs-lookup"><span data-stu-id="80b5b-252">In the Azure portal, open the applications view and then go to the directory view.</span></span> <span data-ttu-id="80b5b-253">Sélectionnez **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Lien Toutes les applications][201] 

2. <span data-ttu-id="80b5b-255">Dans la liste des applications, sélectionnez **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-255">In the applications list, select **Cezanne HR Software**.</span></span>

    ![Liste Applications](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="80b5b-257">Dans le menu de gauche, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-257">In the menu on the left, select **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="80b5b-259">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-259">Select **Add**.</span></span> <span data-ttu-id="80b5b-260">Ensuite, dans la boîte de dialogue **Ajouter une attribution**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-260">Then in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Lien Utilisateurs et groupes][203]

5. <span data-ttu-id="80b5b-262">Dans la boîte de dialogue **Utilisateurs et groupes**, dans la liste **Utilisateurs**, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-262">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="80b5b-263">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-263">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="80b5b-264">Dans la boîte de dialogue **Ajouter une attribution**, sélectionnez **Affecter**.</span><span class="sxs-lookup"><span data-stu-id="80b5b-264">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="80b5b-265">Tester l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="80b5b-265">Test SSO</span></span>

<span data-ttu-id="80b5b-266">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="80b5b-266">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="80b5b-267">Lorsque vous cliquez sur la vignette du logiciel Cezanne HR dans le panneau d’accès, vous vous connectez automatiquement à votre application logicielle Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="80b5b-267">When you select the Cezanne HR software tile in the Access Panel, you sign on automatically to your Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80b5b-268">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80b5b-268">Next steps</span></span>

* [<span data-ttu-id="80b5b-269">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80b5b-269">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80b5b-270">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="80b5b-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

