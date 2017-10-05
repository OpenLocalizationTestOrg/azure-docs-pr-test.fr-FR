---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform | Microsoft Docs"
description: "Apprenez à utiliser SAP HANA Cloud Platform avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="ec2e4-103">Didacticiel : Intégration d’Azure Active Directory avec SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="ec2e4-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="ec2e4-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="ec2e4-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ec2e4-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ec2e4-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="ec2e4-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ec2e4-107">Un compte SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="ec2e4-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="ec2e4-108">À l’issue de ce didacticiel, les utilisateurs d’Azure AD que vous avez affectés à SAP HANA Cloud Platform pourront s’authentifier de manière unique dans l’application (connexion initiée par le fournisseur du service) à l’aide de la [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ec2e4-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="ec2e4-109">Vous devez déployer votre propre application ou vous abonner à une application sur votre compte SAP HANA Cloud Platform pour tester l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="ec2e4-110">Dans ce didacticiel, une application est déployée dans le compte.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="ec2e4-111">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="ec2e4-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="ec2e4-112">Activation de l’intégration d’application pour SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="ec2e4-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="ec2e4-113">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="ec2e4-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="ec2e4-114">Affectation d’un rôle à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="ec2e4-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="ec2e4-115">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ec2e4-115">Assigning users</span></span>

<span data-ttu-id="ec2e4-116">![Scénario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="ec2e4-117">Activation de l’intégration d’application pour SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="ec2e4-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="ec2e4-118">Cette section décrit l’activation de l’intégration d’application pour SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="ec2e4-119">**Pour activer l’intégration d’applications pour SAP HANA Cloud Platform, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ec2e4-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="ec2e4-120">Dans le volet de navigation gauche du portail de gestion Azure, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="ec2e4-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ec2e4-122">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ec2e4-123">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="ec2e4-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ec2e4-125">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="ec2e4-126">![Ajouter une application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ec2e4-127">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="ec2e4-128">![Ajouter une application à partir de la galerie](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ec2e4-129">Dans la **zone de recherche**, tapez **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="ec2e4-130">![Galerie d’applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="ec2e4-131">Dans le volet des résultats, sélectionnez **SAP HANA Cloud Platform**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="ec2e4-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ec2e4-133">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ec2e4-133">Configure single sign-on</span></span>

<span data-ttu-id="ec2e4-134">Cette section explique comment permettre aux utilisateurs de s’authentifier sur SAP HANA Cloud Platform avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="ec2e4-135">Dans le cadre de cette procédure, vous devez créer un fichier de certificat codé en base 64 sur votre locataire SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="ec2e4-136">Si cette procédure ne vous est pas familière, consultez [Conversion d’un certificat binaire en fichier texte](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="ec2e4-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="ec2e4-137">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ec2e4-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="ec2e4-138">Dans le portail Azure Classic, sur la page d’intégration d’application **SAP HANA Cloud Platform**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="ec2e4-139">![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="ec2e4-140">Dans la page **Comment voulez-vous que les utilisateurs se connectent à SAP HANA Cloud Platform**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="ec2e4-141">![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="ec2e4-142">Dans une autre fenêtre de navigateur web, connectez-vous à SAP HANA Cloud Platform Cockpit à l’adresse \<https://account.\>landscape host.ondemand.com/cockpit (par ex. *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="ec2e4-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="ec2e4-143">Cliquez sur l’onglet **Trust** .</span><span class="sxs-lookup"><span data-stu-id="ec2e4-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="ec2e4-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="ec2e4-145">Dans la section de gestion d’approbation, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec2e4-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="ec2e4-146">![Obtenir les métadonnées](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obtenir les métadonnées")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="ec2e4-147">Cliquez sur l’onglet **Local Service Provider** .</span><span class="sxs-lookup"><span data-stu-id="ec2e4-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="ec2e4-148">Pour télécharger le fichier de métadonnées SAP HANA Cloud Platform, cliquez sur **Get Metadata**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="ec2e4-149">Dans le portail Azure Classic, dans la page **Configurer l’URL de l’application**, procédez comme suit, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="ec2e4-150">![Configurer l’URL de l’application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="ec2e4-151">Dans la zone de texte **URL d’authentification**, entrez l’URL utilisée par vos utilisateurs pour se connecter à votre application **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="ec2e4-152">Il s’agit de l’URL spécifique au compte d’une ressource protégée de votre application SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="ec2e4-153">L’URL est au format suivant : *https://\<nomApplication\>\<nomCompte\>.\<hôte\>.ondemand.com/\<chemin\_vers\_ressource\_protégée\>* (par ex. : *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="ec2e4-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="ec2e4-154">Il s’agit de l’URL de votre application SAP HANA Cloud Platform sur laquelle l’utilisateur doit s’authentifier.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="ec2e4-155">Ouvrez le fichier de métadonnées SAP HANA Cloud Platform téléchargé et recherchez la balise **ns3:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="ec2e4-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="ec2e4-156">Copiez la valeur de l’attribut **Location** et collez-la dans la zone de texte **SAP HANA Cloud Platform Reply URL**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="ec2e4-157">Dans la page **Configurer l’authentification unique à SAP HANA Cloud Platform**, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="ec2e4-158">![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="ec2e4-159">Sur SAP HANA Cloud Platform Cockpit, dans la section **Local Service Provider** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec2e4-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="ec2e4-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="ec2e4-161">Cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="ec2e4-162">Comme **Configuration Type**, sélectionnez **Custom**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="ec2e4-163">Pour **Local Provider Name**, laissez la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="ec2e4-164">Pour générer une paire de clés **Signature Key** et **Signing Certificate**, cliquez sur **Generate Key Pair**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="ec2e4-165">Pour **Principal Propagation**, sélectionnez **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="ec2e4-166">Pour **Force Authentication**, sélectionnez **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="ec2e4-167">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-167">Click **Save**.</span></span>

9. <span data-ttu-id="ec2e4-168">Cliquez sur l’onglet **Trusted Identity Provider**, puis sur **Add Trusted Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="ec2e4-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="ec2e4-170">Pour gérer la liste de fournisseurs d’identité approuvés, vous devrez avoir choisi le type de configuration Custom dans la section Local Service Provider.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="ec2e4-171">Pour le type de configuration Default, vous disposez d’une approbation non modifiable et implicite au SAP ID Service.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="ec2e4-172">Pour None, vous n’avez aucun paramètre d’approbation.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="ec2e4-173">Cliquez sur l’onglet **General**, puis sur **Browse** pour charger le fichier de métadonnées que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="ec2e4-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="ec2e4-175">Après avoir téléchargé le fichier de métadonnées, les valeurs de **Single Sign-on URL**, **Single Logout URL** et de **Signing Certificate** sont remplies automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="ec2e4-176">Cliquez sur onglet **Attributes** .</span><span class="sxs-lookup"><span data-stu-id="ec2e4-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="ec2e4-177">Sous l’onglet **Attributes**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec2e4-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="ec2e4-178">![Attributs](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="ec2e4-179">Cliquez sur **Add Assertion-Based Attribute**, puis ajoutez les attributs basés sur une assertion suivants :</span><span class="sxs-lookup"><span data-stu-id="ec2e4-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="ec2e4-180">Assertion Attribute</span><span class="sxs-lookup"><span data-stu-id="ec2e4-180">Assertion Attribute</span></span> | <span data-ttu-id="ec2e4-181">Principal Attribute</span><span class="sxs-lookup"><span data-stu-id="ec2e4-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="ec2e4-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="ec2e4-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="ec2e4-183">firstname</span><span class="sxs-lookup"><span data-stu-id="ec2e4-183">firstname</span></span> |
    | <span data-ttu-id="ec2e4-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="ec2e4-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="ec2e4-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="ec2e4-185">lastname</span></span> |
    | <span data-ttu-id="ec2e4-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="ec2e4-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="ec2e4-187">email</span><span class="sxs-lookup"><span data-stu-id="ec2e4-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="ec2e4-188">La configuration des attributs dépend de la façon dont sont développées les applications sur HCP, en l’occurrence des attributs qu’elles attendent dans la réponse SAML et avec quel nom (Principal Attribute) elles accèdent à cet attribut dans le code.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-188">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="ec2e4-189">L’attribut **Default Attribute** de la capture d’écran ne sert qu’à des fins d’illustration.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-189">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="ec2e4-190">Il n’est pas nécessaire de faire fonctionner le scénario.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-190">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="ec2e4-191">Les noms et valeurs de **Principal Attribute** dans la capture d’écran dépendent de la façon dont l’application est développée.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-191">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="ec2e4-192">Il est possible que votre application exige des mappages différents.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="ec2e4-193">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configure single sign-on at SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-193">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="ec2e4-194">![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="ec2e4-195">Groupes basés sur une assertion</span><span class="sxs-lookup"><span data-stu-id="ec2e4-195">Assertion-based groups</span></span>
<span data-ttu-id="ec2e4-196">Une étape facultative est de configurer des groupes basés sur une assertion pour votre fournisseur d’identité Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="ec2e4-197">L’utilisation de SAP HANA Cloud Platform vous permet d’attribuer de manière dynamique un ou plusieurs utilisateurs à un ou plusieurs rôles dans vos applications SAP HANA Cloud Platform, en fonction des valeurs des attributs de l’assertion SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-197">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="ec2e4-198">Par exemple, si l’assertion contient l’attribut « *contract=temporaire* », vous souhaiterez peut-être que tous les utilisateurs affectés soient ajoutés au groupe « *TEMPORAIRE* ».</span><span class="sxs-lookup"><span data-stu-id="ec2e4-198">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="ec2e4-199">Le groupe «*TEMPORAIRE*» peut contenir un ou plusieurs rôles d’une ou plusieurs applications déployées dans votre compte SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-199">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="ec2e4-200">Utilisez des groupes basés sur une assertion quand vous voulez affecter simultanément plusieurs utilisateurs à un ou plusieurs rôles d’applications dans votre compte SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-200">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="ec2e4-201">Si vous ne voulez affecter qu’un seul utilisateur ou un petit nombre d’utilisateurs à des rôles spécifiques, nous vous recommandons de les affecter directement dans l’onglet « **Autorisations** » de SAP HANA Cloud Platform Cockpit.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-201">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="ec2e4-202">Affecter un rôle à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="ec2e4-202">Assign a role to a user</span></span>
<span data-ttu-id="ec2e4-203">Pour permettre aux utilisateurs d’Azure AD de se connecter à SAP HANA Cloud Platform, vous devez leur attribuer des rôles dans SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-203">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="ec2e4-204">**Pour affecter un rôle à un utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ec2e4-204">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="ec2e4-205">Connectez-vous à votre cockpit **SAP HANA Cloud Platform** .</span><span class="sxs-lookup"><span data-stu-id="ec2e4-205">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="ec2e4-206">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec2e4-206">Perform the following:</span></span>
   
   <span data-ttu-id="ec2e4-207">![Autorisations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorisations")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="ec2e4-208">Cliquez sur **Authorization**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="ec2e4-209">Cliquez sur l’onglet **Users** .</span><span class="sxs-lookup"><span data-stu-id="ec2e4-209">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="ec2e4-210">Dans la zone de texte **User** , tapez l’adresse de messagerie de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-210">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="ec2e4-211">Cliquez sur **Assign** pour attribuer l’utilisateur à un rôle.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-211">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="ec2e4-212">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="ec2e4-213">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ec2e4-213">Assign users</span></span>
<span data-ttu-id="ec2e4-214">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-214">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="ec2e4-215">**Pour affecter des utilisateurs à SAP HANA Cloud Platform, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ec2e4-215">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="ec2e4-216">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-216">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ec2e4-217">Dans la page d’intégration d’application **SAP HANA Cloud Platform**, cliquez sur **Affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-217">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="ec2e4-218">![Affecter des utilisateurs](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="ec2e4-219">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-219">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="ec2e4-220">![Oui](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="ec2e4-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ec2e4-221">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ec2e4-221">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="ec2e4-222">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ec2e4-222">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

