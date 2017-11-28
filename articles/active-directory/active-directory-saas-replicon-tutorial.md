---
title: "Didacticiel : Intégration d’Azure Active Directory à Replicon | Microsoft Docs"
description: "Apprenez à utiliser Replicon avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2aeeceb61191962b62892b8409218684f76c6fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="c56c4-103">Didacticiel : Intégration d’Azure Active Directory à Replicon</span><span class="sxs-lookup"><span data-stu-id="c56c4-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="c56c4-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et Replicon.</span><span class="sxs-lookup"><span data-stu-id="c56c4-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="c56c4-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c56c4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="c56c4-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="c56c4-106">A valid Azure subscription</span></span>
* <span data-ttu-id="c56c4-107">Un locataire Replicon</span><span class="sxs-lookup"><span data-stu-id="c56c4-107">A Replicon tenant</span></span>

<span data-ttu-id="c56c4-108">À l’issue de ce didacticiel, les utilisateurs Azure AD que vous avez affectés à Replicon pourront s’authentifier de manière unique dans l’application sur votre site d’entreprise Replicon (connexion initiée par le fournisseur du service) ou en s’aidant de la [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c56c4-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="c56c4-109">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="c56c4-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="c56c4-110">Activation de l’intégration d’application pour Replicon</span><span class="sxs-lookup"><span data-stu-id="c56c4-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="c56c4-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="c56c4-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="c56c4-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c56c4-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="c56c4-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c56c4-113">Assigning users</span></span>

<span data-ttu-id="c56c4-114">![Scénario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="c56c4-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="c56c4-115">Activer l’intégration d’applications pour Replicon</span><span class="sxs-lookup"><span data-stu-id="c56c4-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="c56c4-116">Cette section décrit l’activation de l’intégration d’application pour Replicon.</span><span class="sxs-lookup"><span data-stu-id="c56c4-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="c56c4-117">**Pour activer l’intégration d’applications pour Replicon, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="c56c4-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="c56c4-118">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="c56c4-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="c56c4-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="c56c4-120">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="c56c4-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c56c4-121">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="c56c4-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="c56c4-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="c56c4-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="c56c4-123">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="c56c4-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="c56c4-124">![Ajouter une application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="c56c4-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="c56c4-125">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="c56c4-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-replicon-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="c56c4-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="c56c4-127">Dans la **zone de recherche**, entrez **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="c56c4-128">![Galerie d’applications](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="c56c4-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="c56c4-129">Dans le volet de résultats, sélectionnez **Replicon**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c56c4-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="c56c4-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="c56c4-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="c56c4-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c56c4-131">Configure single sign-on</span></span>

<span data-ttu-id="c56c4-132">Cette section explique comment permettre aux utilisateurs de s’authentifier sur Replicon avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="c56c4-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="c56c4-133">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c56c4-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="c56c4-134">Dans le portail Azure Classic, puis, sur la page d’intégration d’application **Replicon**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="c56c4-135">![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="c56c4-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="c56c4-136">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Replicon**, sélectionnez **Authentification unique avec Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="c56c4-137">![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="c56c4-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="c56c4-138">Dans la page **Configurer l’URL de l’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c56c4-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="c56c4-139">![Configurer l’URL de l’application](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="c56c4-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="c56c4-140">Dans la zone de texte **Replicon Sign On URL**, saisissez l’URL de votre client Replicon (par exemple : *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="c56c4-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="c56c4-141">Dans la zone de texte **Replicon Reply URL**, entrez votre URL Replicon **AssertionConsumerService** (par exemple, *https://global.replicon.com/!/saml2/company/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="c56c4-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="c56c4-142">Vous pouvez obtenir l’URL à partir des métadonnées Replicon à : **https://global.replicon.com/!/saml2/\<CléDeVotreEntreprise>\>**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="c56c4-143">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-143">Click **Next**.</span></span>

4. <span data-ttu-id="c56c4-144">Dans la page **Configurer l’authentification unique sur Replicon**, cliquez sur **Télécharger les métadonnées**, puis enregistrez les métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c56c4-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="c56c4-145">![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="c56c4-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="c56c4-146">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Replicon en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c56c4-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="c56c4-147">Procédez comme suit pour configurer SAML 2.0 :</span><span class="sxs-lookup"><span data-stu-id="c56c4-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="c56c4-148">![Activer l’authentification SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Activer l’authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="c56c4-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="c56c4-149">Pour afficher la boîte de dialogue **EnableSAML Authentication2**, ajoutez ce qui suit à votre URL, après votre clé d’entreprise : **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="c56c4-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="c56c4-150">Voici une illustration du schéma de l’URL complète :</span><span class="sxs-lookup"><span data-stu-id="c56c4-150">The following shows the schema of the complete URL:</span></span>  
   <span data-ttu-id="c56c4-151">**https://na2.replicon.com/\<CléDeVotreEntreprise\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="c56c4-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="c56c4-152">Cliquez sur **+** pour développer la section **v20Configuration**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-152">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="c56c4-153">Cliquez sur **+** pour développer la section **metaDataConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-153">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="c56c4-154">Cliquez sur **Choose File** pour sélectionner votre fichier XML de métadonnées de fournisseur d’identité, puis cliquez sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-154">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="c56c4-155">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="c56c4-156">![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="c56c4-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="c56c4-157">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="c56c4-157">Configure user provisioning</span></span>

<span data-ttu-id="c56c4-158">Pour se connecter à Replicon, les utilisateurs d’Azure AD doivent être approvisionnés dans Replicon.</span><span class="sxs-lookup"><span data-stu-id="c56c4-158">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="c56c4-159">Dans le cas de Replicon, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="c56c4-159">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="c56c4-160">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c56c4-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="c56c4-161">Dans une fenêtre de navigateur web, connectez-vous à votre site d’entreprise Replicon en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c56c4-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="c56c4-162">Accédez à **Administration \> Users**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-162">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="c56c4-163">![Utilisateurs](./media/active-directory-saas-replicon-tutorial/IC777806.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="c56c4-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="c56c4-164">Cliquez sur **+Add User**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="c56c4-165">![Ajouter un utilisateur](./media/active-directory-saas-replicon-tutorial/IC777807.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="c56c4-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="c56c4-166">Dans la section **User Profile** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c56c4-166">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="c56c4-167">![Profil utilisateur](./media/active-directory-saas-replicon-tutorial/IC777808.png "Profil utilisateur")</span><span class="sxs-lookup"><span data-stu-id="c56c4-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="c56c4-168">Dans la zone de texte **Login Name** , tapez l’adresse de messagerie Azure AD de l’utilisateur Azure AD que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="c56c4-168">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="c56c4-169">Pour **Authentication Type**, sélectionnez **SSO**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="c56c4-170">Dans la zone de texte **Department** , tapez le département de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c56c4-170">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="c56c4-171">Pour **Employee Type**, sélectionnez **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="c56c4-172">Cliquez sur **Save User Profile**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="c56c4-173">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par Replicon, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="c56c4-173">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="c56c4-174">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="c56c4-174">Assign users</span></span>
<span data-ttu-id="c56c4-175">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="c56c4-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="c56c4-176">**Pour affecter des utilisateurs à Replicon, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c56c4-176">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="c56c4-177">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="c56c4-177">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="c56c4-178">Sur la page d’intégration d’application **Replicon**, cliquez sur **Affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c56c4-178">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="c56c4-179">![Affecter des utilisateurs](./media/active-directory-saas-replicon-tutorial/IC777809.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="c56c4-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="c56c4-180">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="c56c4-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="c56c4-181">![Oui](./media/active-directory-saas-replicon-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="c56c4-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="c56c4-182">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c56c4-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="c56c4-183">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c56c4-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

