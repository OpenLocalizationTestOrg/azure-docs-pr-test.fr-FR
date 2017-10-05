---
title: "Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Secure | Microsoft Docs"
description: "Découvrez comment utiliser TOPdesk - Secure avec Azure AD pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="580ea-103">Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="580ea-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="580ea-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="580ea-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="580ea-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="580ea-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="580ea-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="580ea-106">A valid Azure subscription</span></span>
* <span data-ttu-id="580ea-107">Un abonnement TOPdesk - Secure pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="580ea-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="580ea-108">À l’issue de ce didacticiel, les utilisateurs d’Azure AD que vous avez affectés à TOPdesk - Secure pourront s’authentifier de manière unique dans l’application sur votre site d’entreprise TOPdesk - Secure (connexion initiée par le fournisseur du service) ou à l’aide de la [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="580ea-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="580ea-109">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="580ea-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="580ea-110">Activation de l’intégration d’applications pour TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="580ea-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="580ea-111">Configuration de l'authentification unique</span><span class="sxs-lookup"><span data-stu-id="580ea-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="580ea-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="580ea-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="580ea-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="580ea-113">Assigning users</span></span>

<span data-ttu-id="580ea-114">![Scénario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="580ea-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="580ea-115">Activation de l’intégration d’applications pour TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="580ea-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="580ea-116">Cette section décrit l’activation de l’intégration d’applications pour TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="580ea-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="580ea-117">Pour activer l’intégration d’applications pour TOPdesk - Secure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="580ea-118">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="580ea-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="580ea-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="580ea-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="580ea-120">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="580ea-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="580ea-121">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="580ea-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="580ea-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="580ea-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="580ea-123">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="580ea-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="580ea-124">![Ajouter une application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="580ea-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="580ea-125">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="580ea-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="580ea-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="580ea-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="580ea-127">Dans la **zone de recherche**, entrez **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="580ea-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="580ea-128">![Galerie d’applications](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="580ea-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="580ea-129">Dans le volet des résultats, sélectionnez **TOPdesk - Secure**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="580ea-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="580ea-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="580ea-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="580ea-131">Configuration de l'authentification unique</span><span class="sxs-lookup"><span data-stu-id="580ea-131">Configuring single sign-on</span></span>
<span data-ttu-id="580ea-132">Cette section explique comment permettre aux utilisateurs de s’authentifier sur TOPdesk - Secure avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="580ea-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="580ea-133">La configuration de l’authentification unique pour TOPdesk - Secure vous oblige à télécharger le fichier d’une icône.</span><span class="sxs-lookup"><span data-stu-id="580ea-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="580ea-134">Pour obtenir ce fichier d’icône, contactez l’équipe de support TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="580ea-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="580ea-135">Pour configurer l’authentification unique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="580ea-136">Connectez-vous à votre site d’entreprise **TOPdesk - Secure** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="580ea-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="580ea-137">Dans le menu **TOPdesk**, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="580ea-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="580ea-138">![Paramètres](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="580ea-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="580ea-139">Cliquez sur **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="580ea-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="580ea-140">![Paramètres de connexion](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Paramètres de connexion")</span><span class="sxs-lookup"><span data-stu-id="580ea-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="580ea-141">Développez le menu **Login Settings**, puis cliquez sur **General**.</span><span class="sxs-lookup"><span data-stu-id="580ea-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="580ea-142">![Général](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Général")</span><span class="sxs-lookup"><span data-stu-id="580ea-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="580ea-143">Dans la section **Secure** de la section de configuration **SAML login**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="580ea-144">![Paramètres techniques](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Paramètres techniques")</span><span class="sxs-lookup"><span data-stu-id="580ea-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="580ea-145">a.</span><span class="sxs-lookup"><span data-stu-id="580ea-145">a.</span></span> <span data-ttu-id="580ea-146">Cliquez sur **Download** pour télécharger le fichier de métadonnées public et enregistrez-le en local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="580ea-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="580ea-147">b.</span><span class="sxs-lookup"><span data-stu-id="580ea-147">b.</span></span> <span data-ttu-id="580ea-148">Ouvrez le fichier de métadonnées et recherchez le nœud **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="580ea-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="580ea-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span><span class="sxs-lookup"><span data-stu-id="580ea-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="580ea-150">c.</span><span class="sxs-lookup"><span data-stu-id="580ea-150">c.</span></span> <span data-ttu-id="580ea-151">Copiez la valeur de **AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="580ea-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="580ea-152">Vous en aurez besoin dans la section **Configurer l’URL de l’application** plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="580ea-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="580ea-153">Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail Azure Classic** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="580ea-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="580ea-154">Sur le **TOPdesk - Secure** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** pour ouvrir la ** configurer Single Sign On ** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="580ea-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="580ea-155">![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="580ea-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="580ea-156">Dans la page **Comment voulez-vous que les utilisateurs se connectent à TOPdesk - Secure**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="580ea-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="580ea-157">![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="580ea-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="580ea-158">Dans la page **Configurer l’URL de l’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="580ea-159">![Configurer l’URL de l’application](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="580ea-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="580ea-160">a.</span><span class="sxs-lookup"><span data-stu-id="580ea-160">a.</span></span> <span data-ttu-id="580ea-161">Dans la zone de texte **URL d’authentification de TOPdesk - Secure**, entrez l’URL utilisée par vos utilisateurs pour se connecter à votre application TOPdesk - Secure (par exemple : *https://qssolutions.topdesk.net*).</span><span class="sxs-lookup"><span data-stu-id="580ea-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="580ea-162">b.</span><span class="sxs-lookup"><span data-stu-id="580ea-162">b.</span></span> <span data-ttu-id="580ea-163">Dans la zone de texte **URL de réponse TOPdesk - Secure**, collez l’**URL d’AssertionConsumerService TOPdesk - Secure** (par exemple : *https://qssolutions.topdesk.net/tas/public/login/saml*).</span><span class="sxs-lookup"><span data-stu-id="580ea-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="580ea-164">c.</span><span class="sxs-lookup"><span data-stu-id="580ea-164">c.</span></span> <span data-ttu-id="580ea-165">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="580ea-165">Click **Next**.</span></span>

10. <span data-ttu-id="580ea-166">Dans la page **Configurer l’authentification unique sur TOPdesk - Secure**, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="580ea-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="580ea-167">![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="580ea-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="580ea-168">Pour créer un fichier de certificat, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="580ea-169">![Certificat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificat")</span><span class="sxs-lookup"><span data-stu-id="580ea-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="580ea-170">a.</span><span class="sxs-lookup"><span data-stu-id="580ea-170">a.</span></span> <span data-ttu-id="580ea-171">Ouvrez le fichier de métadonnées téléchargé.</span><span class="sxs-lookup"><span data-stu-id="580ea-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="580ea-172">b.</span><span class="sxs-lookup"><span data-stu-id="580ea-172">b.</span></span> <span data-ttu-id="580ea-173">Développez le nœud **RoleDescriptor** dont le **xsi:type** est **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="580ea-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="580ea-174">c.</span><span class="sxs-lookup"><span data-stu-id="580ea-174">c.</span></span> <span data-ttu-id="580ea-175">Copiez la valeur du nœud **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="580ea-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="580ea-176">d.</span><span class="sxs-lookup"><span data-stu-id="580ea-176">d.</span></span> <span data-ttu-id="580ea-177">Enregistrez la valeur de **X509Certificate** copiée, dans un fichier local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="580ea-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="580ea-178">Dans le menu **TOPdesk** de votre site d’entreprise TOPdesk - Secure, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="580ea-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="580ea-179">![Paramètres](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="580ea-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="580ea-180">Cliquez sur **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="580ea-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="580ea-181">![Paramètres de connexion](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Paramètres de connexion")</span><span class="sxs-lookup"><span data-stu-id="580ea-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="580ea-182">Développez le menu **Login Settings**, puis cliquez sur **General**.</span><span class="sxs-lookup"><span data-stu-id="580ea-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="580ea-183">![Général](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Général")</span><span class="sxs-lookup"><span data-stu-id="580ea-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="580ea-184">Dans la section **Public**, cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="580ea-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="580ea-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span><span class="sxs-lookup"><span data-stu-id="580ea-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="580ea-186">Dans la boîte de dialogue **SAML configuration assistant** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="580ea-187">![Assistant de configuration SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Assistant de configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="580ea-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="580ea-188">a.</span><span class="sxs-lookup"><span data-stu-id="580ea-188">a.</span></span> <span data-ttu-id="580ea-189">Pour charger votre fichier de métadonnées téléchargé, dans **Federation Metadata**, cliquez sur **Browse**.</span><span class="sxs-lookup"><span data-stu-id="580ea-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="580ea-190">b.</span><span class="sxs-lookup"><span data-stu-id="580ea-190">b.</span></span> <span data-ttu-id="580ea-191">Pour charger votre fichier de certificat, sous **Certificate (RSA)**, cliquez sur **Browse**.</span><span class="sxs-lookup"><span data-stu-id="580ea-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="580ea-192">c.</span><span class="sxs-lookup"><span data-stu-id="580ea-192">c.</span></span> <span data-ttu-id="580ea-193">Pour charger le fichier de logo que vous avez obtenu de l’équipe de support TOPdesk, sous **Logo icon**, cliquez sur **Browse**.</span><span class="sxs-lookup"><span data-stu-id="580ea-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="580ea-194">d.</span><span class="sxs-lookup"><span data-stu-id="580ea-194">d.</span></span> <span data-ttu-id="580ea-195">Dans la zone de texte **User name attribute**, tapez **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="580ea-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="580ea-196">e.</span><span class="sxs-lookup"><span data-stu-id="580ea-196">e.</span></span> <span data-ttu-id="580ea-197">Dans la zone de texte **Display name** , indiquez le nom de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="580ea-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="580ea-198">f.</span><span class="sxs-lookup"><span data-stu-id="580ea-198">f.</span></span> <span data-ttu-id="580ea-199">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="580ea-199">Click **Save**.</span></span>

17. <span data-ttu-id="580ea-200">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="580ea-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="580ea-201">![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="580ea-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="580ea-202">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="580ea-202">Configuring user provisioning</span></span>
<span data-ttu-id="580ea-203">Pour se connecter à TOPdesk - Secure, les utilisateurs d’Azure AD doivent être approvisionnés dans TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="580ea-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="580ea-204">Dans le cas de TOPdesk - Secure, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="580ea-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="580ea-205">Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="580ea-206">Connectez-vous à votre site d’entreprise **TOPdesk - Secure** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="580ea-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="580ea-207">Dans le menu en haut, cliquez sur **TOPdesk \> New \> Support Files \> Operator**.</span><span class="sxs-lookup"><span data-stu-id="580ea-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="580ea-208">![Operator (Opérateur)](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator (Opérateur)")</span><span class="sxs-lookup"><span data-stu-id="580ea-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="580ea-209">Dans la boîte de dialogue **New Operator** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="580ea-210">![New Operator (Nouvel opérateur)](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator (Nouvel opérateur)")</span><span class="sxs-lookup"><span data-stu-id="580ea-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="580ea-211">a.</span><span class="sxs-lookup"><span data-stu-id="580ea-211">a.</span></span> <span data-ttu-id="580ea-212">Cliquez sur l’onglet General.</span><span class="sxs-lookup"><span data-stu-id="580ea-212">Click the General tab.</span></span>
   
    <span data-ttu-id="580ea-213">b.</span><span class="sxs-lookup"><span data-stu-id="580ea-213">b.</span></span> <span data-ttu-id="580ea-214">Dans la zone de texte **Surname** de la section **General**, indiquez le nom du compte Azure Active Directory valide que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="580ea-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="580ea-215">c.</span><span class="sxs-lookup"><span data-stu-id="580ea-215">c.</span></span> <span data-ttu-id="580ea-216">Sélectionnez un **Site** pour le compte dans la section **Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="580ea-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="580ea-217">d.</span><span class="sxs-lookup"><span data-stu-id="580ea-217">d.</span></span> <span data-ttu-id="580ea-218">Dans la zone de texte **Login Name** de la section **TOPdesk Login**, indiquez le nom de connexion de votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="580ea-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="580ea-219">e.</span><span class="sxs-lookup"><span data-stu-id="580ea-219">e.</span></span> <span data-ttu-id="580ea-220">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="580ea-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="580ea-221">Vous pouvez utiliser n’importe quel outil ou API de création de compte d’utilisateur, fourni par TOPdesk - Secure, pour approvisionner des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="580ea-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="580ea-222">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="580ea-222">Assigning users</span></span>
<span data-ttu-id="580ea-223">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="580ea-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="580ea-224">Pour affecter des utilisateurs à TOPdesk - Secure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="580ea-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="580ea-225">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="580ea-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="580ea-226">Sur la ** TOPdesk - Secure ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="580ea-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="580ea-227">![Affecter des utilisateurs](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="580ea-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="580ea-228">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="580ea-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="580ea-229">![Oui](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="580ea-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="580ea-230">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="580ea-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="580ea-231">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="580ea-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

