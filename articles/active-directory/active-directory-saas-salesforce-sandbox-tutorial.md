---
title: "Didacticiel : intégration d’Azure Active Directory à Salesforce Sandbox | Microsoft Docs"
description: "Apprenez à utiliser Salesforce Sandbox avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 32835e79188806bb2ff319eea23b1b52ab585ab1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="75bfe-103">Didacticiel : Intégration d’Azure Active Directory à Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="75bfe-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="75bfe-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="75bfe-104">The objective of this tutorial is to show the integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="75bfe-105">Pour les commentaires, consultez la [Page de support Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="75bfe-105">For feedback, see the [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="75bfe-106">Les bacs à sable (sandbox) vous permettent de créer plusieurs copies de votre organisation dans des environnements distincts à des fins diverses, notamment le développement, le test et la formation, sans compromettre les données ou les applications de votre organisation de production Salesforce.</span><span class="sxs-lookup"><span data-stu-id="75bfe-106">Sandboxes give you the ability to create multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising the data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="75bfe-107">Pour plus d’informations, consultez la page [Présentation de Sandbox](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="75bfe-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="75bfe-108">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="75bfe-108">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="75bfe-109">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="75bfe-109">A valid Azure subscription</span></span>
* <span data-ttu-id="75bfe-110">Un bac à sable (sandbox) dans Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="75bfe-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="75bfe-111">Si vous ne disposez pas encore d’un bac à sable (sandbox) valide dans Salesforce.com, vous devez contacter Salesforce.</span><span class="sxs-lookup"><span data-stu-id="75bfe-111">If you don’t have a valid sandbox in Salesforce.com yet, you need to contact Salesforce.</span></span>

<span data-ttu-id="75bfe-112">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="75bfe-112">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="75bfe-113">Activation de l’intégration d’application pour Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="75bfe-113">Enabling the application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="75bfe-114">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="75bfe-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="75bfe-115">Activation de votre domaine</span><span class="sxs-lookup"><span data-stu-id="75bfe-115">Enabling your domain</span></span>
4. <span data-ttu-id="75bfe-116">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="75bfe-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="75bfe-117">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="75bfe-117">Assigning users</span></span>

<span data-ttu-id="75bfe-118">![Scénario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="75bfe-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="75bfe-119">Activer l’intégration d’application pour Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="75bfe-119">Enable the application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="75bfe-120">Cette section décrit l’activation de l’intégration d’application pour Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="75bfe-120">The objective of this section is to outline how to enable the application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="75bfe-121">**Pour activer l’intégration d’application pour Salesforce Sandbox, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bfe-121">**To enable the application integration for Salesforce sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="75bfe-122">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-122">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="75bfe-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="75bfe-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="75bfe-124">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="75bfe-124">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="75bfe-125">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="75bfe-125">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="75bfe-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="75bfe-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="75bfe-127">Pour ouvrir la **Galerie d’applications**, cliquez sur **Ajouter une application**, puis sur **Ajouter une application utilisable par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-127">To open the **Application Gallery**, click **Add An App**, and then click **Add an application for my organization to use**.</span></span>
   
   <span data-ttu-id="75bfe-128">![Que souhaitez-vous faire ?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Que souhaitez-vous faire ?")</span><span class="sxs-lookup"><span data-stu-id="75bfe-128">![What do you want to do?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want to do?")</span></span>
5. <span data-ttu-id="75bfe-129">Dans la **zone de recherche**, tapez **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-129">In the **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="75bfe-130">![Galerie d’applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="75bfe-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="75bfe-131">Dans le volet de résultats, sélectionnez **Salesforce Sandbox**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="75bfe-131">In the results pane, select **Salesforce Sandbox**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="75bfe-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="75bfe-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="75bfe-133">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="75bfe-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="75bfe-134">Cette section explique comment permettre aux utilisateurs de s’authentifier sur Salesforce Sandbox avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="75bfe-134">The objective of this section is to outline how to enable users to authenticate to Salesforce with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="75bfe-135">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bfe-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="75bfe-136">Dans le portail Azure Classic, dans la page d’intégration d’application **Salesforce Sandbox**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-136">In the Azure classic portal, on the **Salesforce Sandbox** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="75bfe-137">![Configurer l’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="75bfe-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="75bfe-138">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Salesforce Sandbox**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-138">On the **How would you like users to sign on to Salesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="75bfe-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="75bfe-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="75bfe-140">Dans la page **Configurer l’URL de l’application**, dans la zone de texte **URL de connexion**, tapez votre URL selon le modèle suivant `http://company.my.salesforce.com`, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-140">On the **Configure App URL** page, in the **Sign On URL** textbox, type your URL using the following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="75bfe-141">![Configurer l’URL de l’application](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="75bfe-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="75bfe-142">Si vous avez déjà configuré l’authentification unique pour une autre instance de Salesforce Sandbox dans votre répertoire, vous devez également configurer **l’identificateur** en utilisant la même valeur que pour **l’URL de connexion**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
 * <span data-ttu-id="75bfe-143">Pour afficher le champ **Identificateur**, cochez la case **Afficher les paramètres avancés** dans la page **Configurer l’URL de l’application** de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="75bfe-143">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog.</span></span>
5. <span data-ttu-id="75bfe-144">Dans la page **Configurer l’authentification unique sur Salesforce Sandbox**, cliquez sur **Télécharger le certificat**, puis enregistrez le fichier de certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="75bfe-144">On the **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="75bfe-145">![Configurer l’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="75bfe-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="75bfe-146">Dans une autre fenêtre de navigateur web, connectez-vous à votre sandbox Salesforce en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="75bfe-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="75bfe-147">Dans le menu situé en haut, cliquez sur **Setup**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-147">In the menu on the top, click **Setup**.</span></span>
   
   <span data-ttu-id="75bfe-148">![Configuration](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="75bfe-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="75bfe-149">Dans le volet de navigation de gauche, cliquez sur **Security Controls (Contrôles de sécurité)**, puis sur **Single Sign-On Settings (Paramètres de l’authentification unique)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-149">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="75bfe-150">![Paramètres d’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="75bfe-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="75bfe-151">Dans la section Single Sign-On Settings, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="75bfe-151">On the Single Sign-On Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="75bfe-152">![Paramètres d’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="75bfe-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="75bfe-153">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="75bfe-154">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-154">Click **New**.</span></span>
10. <span data-ttu-id="75bfe-155">Dans la section SAML Single Sign-On Settings, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="75bfe-155">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>
    
    <span data-ttu-id="75bfe-156">![SAML Single Sign On Settings (Paramètres d’authentification unique SAML)](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign On Settings (Paramètres d’authentification unique SAML)")</span><span class="sxs-lookup"><span data-stu-id="75bfe-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="75bfe-157">Dans la zone de texte Name (Nom), indiquez le nom de la configuration (par exemple, *SPSSOWAAD\_Test*).</span><span class="sxs-lookup"><span data-stu-id="75bfe-157">In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="75bfe-158">Dans la page **Configurer l’authentification unique sur Salesforce Sandbox** du portail Azure Classic, copiez la valeur **URL de l’émetteur** et collez-la dans la zone de texte **Issuer (Émetteur)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-158">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Issuer URL** value, and then paste it into the **Issuer** textbox.</span></span>
 3. <span data-ttu-id="75bfe-159">Dans la zone de texte **ID d’entité**, entrez **https://test.salesforce.com** s’il s’agit de la première instance de Salesforce Sandbox que vous ajoutez à votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="75bfe-159">In the **Entity Id** textbox, type **https://test.salesforce.com** if this is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="75bfe-160">Si vous avez déjà ajouté une instance de Salesforce Sandbox, pour **l’ID d’entité**, entrez **l’URL de connexion**, qui doit être au format : `http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="75bfe-160">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="75bfe-161">Cliquez sur **Parcourir** pour charger le certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="75bfe-161">Click **Browse** to upload the downloaded certificate.</span></span>  
 5. <span data-ttu-id="75bfe-162">Pour **SAML Identity Type (Type d’identité SAML)**, sélectionnez **Assertion contains the Federation ID from the User object (L’assertion contient l’ID de fédération de l’objet utilisateur)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-162">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span> 
 6. <span data-ttu-id="75bfe-163">Pour **SAML Identity Location (Emplacement de l’identité SAML)**, sélectionnez **Identity is in the NameIdentifier element of the Subject statement (L’identité figure dans l’élément NameIdentifier de l’instruction Subject)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-163">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
 7. <span data-ttu-id="75bfe-164">Dans la page **Configurer l’authentification unique sur Salesforce Sandbox** du portail Azure Classic, copiez la valeur **URL de connexion distante** et collez-la dans la zone de texte **Identity Provider Login URL (URL de connexion du fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-164">In the Azure classic portal, on the **Configure single sign-on at Salesforce Sandbox** dialogue page, copy the **Remote Login URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="75bfe-165">SFDC ne prend pas en charge la déconnexion SAML.</span><span class="sxs-lookup"><span data-stu-id="75bfe-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="75bfe-166">Pour contourner ce problème, collez « https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0 » dans la zone de texte **Identity Provider Logout URL** (URL de déconnexion du fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="75bfe-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="75bfe-167">Pour **Service Provider Initiated Request Binding (Liaison de demande initiée par le fournisseur de services)**, sélectionnez **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="75bfe-168">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-168">Click **Save**.</span></span>
11. <span data-ttu-id="75bfe-169">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-169">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="75bfe-170">![Configurer l’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="75bfe-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="75bfe-171">Activer votre domaine</span><span class="sxs-lookup"><span data-stu-id="75bfe-171">Enable your domain</span></span>
<span data-ttu-id="75bfe-172">Cette section suppose que vous avez déjà créé un domaine.</span><span class="sxs-lookup"><span data-stu-id="75bfe-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="75bfe-173">Pour plus d’informations, consultez [Définition de votre nom de domaine](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="75bfe-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="75bfe-174">**Pour activer votre domaine, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bfe-174">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="75bfe-175">Dans le volet de navigation gauche, cliquez sur **Domain Management (Gestion des domaines)**, puis sur **My Domain (Mon domaine)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-175">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="75bfe-176">![Mon domaine](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="75bfe-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="75bfe-177">Vérifiez que votre domaine a été correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="75bfe-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="75bfe-178">Dans la section **Login Page Settings (Paramètres de la page de connexion)**, cliquez sur **Edit (Modifier)**, puis, pour **Authentication Service (Service d’authentification)**, sélectionnez le nom du paramètre d’authentification unique SAML de la section précédente, avant de cliquer sur **Save (Enregistrer)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-178">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="75bfe-179">![Mon domaine](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="75bfe-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="75bfe-180">Dès qu’un domaine est configuré, vos utilisateurs doivent utiliser l’URL du domaine pour se connecter au sandbox Salesforce.</span><span class="sxs-lookup"><span data-stu-id="75bfe-180">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="75bfe-181">Pour obtenir la valeur de l’URL, cliquez sur le profil d’authentification unique créé à la section précédente.</span><span class="sxs-lookup"><span data-stu-id="75bfe-181">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="75bfe-182">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="75bfe-182">Configure user provisioning</span></span>
<span data-ttu-id="75bfe-183">Cette section décrit comment activer l’approvisionnement des utilisateurs des comptes d’utilisateurs Active Directory sur Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="75bfe-183">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce Sandbox.</span></span>

<span data-ttu-id="75bfe-184">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bfe-184">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="75bfe-185">Dans le portail Salesforce, dans la barre de navigation supérieure, sélectionnez votre nom pour développer votre menu utilisateur :</span><span class="sxs-lookup"><span data-stu-id="75bfe-185">In the Salesforce portal, in the top navigation bar, select your name to expand your user menu:</span></span>
   
   <span data-ttu-id="75bfe-186">![My Settings (Mes paramètres)](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings (Mes paramètres)")</span><span class="sxs-lookup"><span data-stu-id="75bfe-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="75bfe-187">Dans votre menu utilisateur, sélectionnez **My Settings (Mes paramètres)** pour ouvrir votre page **My Settings (Mes paramètres)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-187">From your user menu, select **My Settings** to open your **My Settings** page.</span></span>
3. <span data-ttu-id="75bfe-188">Dans le volet gauche, cliquez sur **Personal (Personnel)** pour développer la section du même nom, puis sur **Reset My Security Token (Réinitialiser mon jeton de sécurité)**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-188">In the left pane, click **Personal** to expand the Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="75bfe-189">![My Settings (Mes paramètres)](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings (Mes paramètres)")</span><span class="sxs-lookup"><span data-stu-id="75bfe-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="75bfe-190">Dans la page **Reset My Security Token (Réinitialiser mon jeton de sécurité)**, cliquez sur **Reset Security Token (Réinitialiser le jeton de sécurité)** pour demander un courrier électronique contenant votre jeton de sécurité Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="75bfe-190">On the **Reset My Security Token** page, click **Reset Security Token** to request an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="75bfe-191">![New Token (Nouveau jeton)](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token (Nouveau jeton)")</span><span class="sxs-lookup"><span data-stu-id="75bfe-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="75bfe-192">Recherchez dans votre boîte de réception un courrier électronique provenant de Salesforce.com ayant pour objet «**salesforce.com.com security confirmation**» (confirmation de sécurité salesforce.com.com).</span><span class="sxs-lookup"><span data-stu-id="75bfe-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="75bfe-193">Lisez ce courrier électronique et copiez la valeur du jeton de sécurité.</span><span class="sxs-lookup"><span data-stu-id="75bfe-193">Review this email and copy the security token value.</span></span>
7. <span data-ttu-id="75bfe-194">Dans le portail Azure Classic, dans la page d’intégration d’application **Salesforce Sandbox**, cliquez sur **Configurer l’approvisionnement d’utilisateurs** pour ouvrir la boîte de dialogue **Configurer l’approvisionnement d’utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-194">In the Azure classic portal, on the **salesforce Sandbox** application integration page, click **Configure user provisioning** to open the **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="75bfe-195">![Configurer l’approvisionnement de l’utilisateur](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configurer l’approvisionnement de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="75bfe-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="75bfe-196">Dans la page **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** , indiquez les paramètres de configuration suivants :</span><span class="sxs-lookup"><span data-stu-id="75bfe-196">On the **Enter your Salesforce Sandbox credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
   <span data-ttu-id="75bfe-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="75bfe-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="75bfe-198">Dans la zone de texte **Salesforce Sandbox Admin User Name (Nom d’utilisateur admin Salesforce Sandbox)**, tapez le nom d’un compte Salesforce Sandbox auquel le profil **System Administrator (Administrateur système)** est affecté dans Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="75bfe-198">In the **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="75bfe-199">Dans la zone de texte **Salesforce Sandbox Admin Password** , tapez le mot de passe de ce compte.</span><span class="sxs-lookup"><span data-stu-id="75bfe-199">In the **Salesforce Sandbox Admin Password** textbox, type the password for this account.</span></span>
 3. <span data-ttu-id="75bfe-200">Dans la zone de texte **User Security Token** , collez la valeur du jeton de sécurité.</span><span class="sxs-lookup"><span data-stu-id="75bfe-200">In the **User Security Token** textbox, paste the security token value.</span></span>
 4. <span data-ttu-id="75bfe-201">Cliquez sur **Valider** pour vérifier votre configuration.</span><span class="sxs-lookup"><span data-stu-id="75bfe-201">Click **Validate** to verify your configuration.</span></span>
 5. <span data-ttu-id="75bfe-202">Cliquez sur le bouton **Suivant** pour ouvrir la page **Confirmation**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-202">Click the **Next** button to open the **Confirmation** page.</span></span>
9. <span data-ttu-id="75bfe-203">Dans la page **Confirmation**, cliquez sur **Terminer** pour enregistrer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="75bfe-203">On the **Confirmation** page, click **Complete** to save your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="75bfe-204">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="75bfe-204">Assigning users</span></span>

<span data-ttu-id="75bfe-205">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="75bfe-205">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="75bfe-206">**Pour affecter des utilisateurs à Salesforce Sandbox, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="75bfe-206">**To assign users to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="75bfe-207">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="75bfe-207">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="75bfe-208">Dans la page d’intégration d’application **Salesforce Sandbox**, cliquez sur **Affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="75bfe-208">On the **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="75bfe-209">![Affecter des utilisateurs](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="75bfe-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="75bfe-210">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="75bfe-210">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="75bfe-211">![Oui](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="75bfe-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="75bfe-212">À présent, patientez 10 minutes et vérifiez que le compte est bien synchronisé avec Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="75bfe-212">You should now wait for 10 minutes and verify that the account has been synchronized to Salesforce Sandbox.</span></span>

<span data-ttu-id="75bfe-213">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="75bfe-213">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="75bfe-214">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="75bfe-214">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

