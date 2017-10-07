---
title: "Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Secure | Microsoft Docs"
description: "Découvrez comment toouse TOPdesk - Secure avec Azure Active Directory tooenable l’authentification unique, l’approvisionnement automatisé et bien plus encore !."
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
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="04cc7-103">Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="04cc7-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="04cc7-104">objectif Hello de ce didacticiel est d’intégration de hello tooshow d’Azure et de TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="04cc7-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="04cc7-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="04cc7-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="04cc7-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="04cc7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="04cc7-107">Un abonnement TOPdesk - Secure pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="04cc7-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="04cc7-108">Quand ils auront terminé ce didacticiel, les utilisateurs de hello Azure AD vous avez affecté tooTOPdesk - sécurisé va être toosingle en mesure de l’authentification sur application hello à TOPdesk - site d’entreprise sécurisé (service initiée par le fournisseur de session), ou à l’aide de hello [Introduction Volet d’accès de toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="04cc7-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="04cc7-109">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="04cc7-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="04cc7-110">Activation de l’intégration d’application hello pour TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="04cc7-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="04cc7-111">Configuration de l'authentification unique</span><span class="sxs-lookup"><span data-stu-id="04cc7-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="04cc7-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="04cc7-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="04cc7-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="04cc7-113">Assigning users</span></span>

<span data-ttu-id="04cc7-114">![Scénario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="04cc7-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="04cc7-115">Activation de l’intégration d’application hello pour TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="04cc7-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="04cc7-116">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="04cc7-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="04cc7-117">intégration d’application hello tooenable pour TOPdesk - Secure, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="04cc7-118">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="04cc7-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="04cc7-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="04cc7-120">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="04cc7-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="04cc7-121">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="04cc7-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="04cc7-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="04cc7-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="04cc7-123">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="04cc7-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="04cc7-124">![Ajouter une application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="04cc7-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="04cc7-125">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="04cc7-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="04cc7-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="04cc7-127">Bonjour **zone de recherche**, type **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="04cc7-128">![Galerie d’applications](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="04cc7-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="04cc7-129">Dans le volet de résultats hello, sélectionnez **TOPdesk - Secure**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="04cc7-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="04cc7-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="04cc7-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="04cc7-131">Configuration de l'authentification unique</span><span class="sxs-lookup"><span data-stu-id="04cc7-131">Configuring single sign-on</span></span>
<span data-ttu-id="04cc7-132">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooTOPdesk - Secure avec leur compte dans Azure AD en utilisant la fédération basée sur hello protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="04cc7-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="04cc7-133">Configurer l’authentification unique pour TOPdesk - Secure nécessite que vous tooupload un fichier d’icône de logo.</span><span class="sxs-lookup"><span data-stu-id="04cc7-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="04cc7-134">fichier d’icône tooget hello, équipe de support technique TOPdesk hello contact.</span><span class="sxs-lookup"><span data-stu-id="04cc7-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="04cc7-135">tooconfigure sur l’authentification unique, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="04cc7-136">Ouverture de session tooyour **TOPdesk - Secure** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="04cc7-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="04cc7-137">Bonjour **TOPdesk** menu, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="04cc7-138">![Paramètres](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="04cc7-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="04cc7-139">Cliquez sur **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="04cc7-140">![Paramètres de connexion](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Paramètres de connexion")</span><span class="sxs-lookup"><span data-stu-id="04cc7-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="04cc7-141">Développez hello **les paramètres de connexion** menu, puis sur **général**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="04cc7-142">![Général](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Général")</span><span class="sxs-lookup"><span data-stu-id="04cc7-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="04cc7-143">Bonjour **Secure** section Hello **connexion SAML** configuration section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="04cc7-144">![Paramètres techniques](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Paramètres techniques")</span><span class="sxs-lookup"><span data-stu-id="04cc7-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="04cc7-145">a.</span><span class="sxs-lookup"><span data-stu-id="04cc7-145">a.</span></span> <span data-ttu-id="04cc7-146">Cliquez sur **télécharger** toodownload hello du fichier de métadonnées publiques et les enregistrer localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="04cc7-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="04cc7-147">b.</span><span class="sxs-lookup"><span data-stu-id="04cc7-147">b.</span></span> <span data-ttu-id="04cc7-148">Ouvrez le fichier de métadonnées hello et recherchez hello **AssertionConsumerService** nœud.</span><span class="sxs-lookup"><span data-stu-id="04cc7-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="04cc7-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span><span class="sxs-lookup"><span data-stu-id="04cc7-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="04cc7-150">c.</span><span class="sxs-lookup"><span data-stu-id="04cc7-150">c.</span></span> <span data-ttu-id="04cc7-151">Hello de copie **AssertionConsumerService** valeur.</span><span class="sxs-lookup"><span data-stu-id="04cc7-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="04cc7-152">Vous devez serez hello valeur Bonjour **Configure App URL** section plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="04cc7-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="04cc7-153">Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail Azure Classic** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="04cc7-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="04cc7-154">Sur hello **TOPdesk - Secure** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello ** configurer Single Sign On ** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="04cc7-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="04cc7-155">![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="04cc7-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="04cc7-156">Sur hello **Comment voulez-vous comme toosign utilisateurs sur tooTOPdesk - Secure** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="04cc7-157">![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="04cc7-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="04cc7-158">Sur hello **Configure App URL** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="04cc7-159">![Configurer l’URL de l’application](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="04cc7-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="04cc7-160">a.</span><span class="sxs-lookup"><span data-stu-id="04cc7-160">a.</span></span> <span data-ttu-id="04cc7-161">Bonjour **TOPdesk - Secure URL de connexion** zone de texte, tapez l’URL hello utilisé par votre toosign d’utilisateurs dans votre application TOPdesk - Secure (par exemple : «*https://qssolutions.topdesk.net*»).</span><span class="sxs-lookup"><span data-stu-id="04cc7-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="04cc7-162">b.</span><span class="sxs-lookup"><span data-stu-id="04cc7-162">b.</span></span> <span data-ttu-id="04cc7-163">Bonjour **TOPdesk – URL de réponse publique** zone de texte, collez hello **TOPdesk - Secure AssertionConsumerService URL** (par exemple : «*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="04cc7-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="04cc7-164">c.</span><span class="sxs-lookup"><span data-stu-id="04cc7-164">c.</span></span> <span data-ttu-id="04cc7-165">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-165">Click **Next**.</span></span>

10. <span data-ttu-id="04cc7-166">Sur hello **configurer l’authentification unique sur TOPdesk - Secure** page, toodownload votre fichier de métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="04cc7-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="04cc7-167">![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="04cc7-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="04cc7-168">toocreate un fichier de certificat, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="04cc7-169">![Certificat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificat")</span><span class="sxs-lookup"><span data-stu-id="04cc7-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="04cc7-170">a.</span><span class="sxs-lookup"><span data-stu-id="04cc7-170">a.</span></span> <span data-ttu-id="04cc7-171">Fichier de métadonnées téléchargé hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="04cc7-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="04cc7-172">b.</span><span class="sxs-lookup"><span data-stu-id="04cc7-172">b.</span></span> <span data-ttu-id="04cc7-173">Développez hello **RoleDescriptor** nœud qui a un **xsi : type** de **fed : ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="04cc7-174">c.</span><span class="sxs-lookup"><span data-stu-id="04cc7-174">c.</span></span> <span data-ttu-id="04cc7-175">Copier la valeur hello Hello **X509Certificate** nœud.</span><span class="sxs-lookup"><span data-stu-id="04cc7-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="04cc7-176">d.</span><span class="sxs-lookup"><span data-stu-id="04cc7-176">d.</span></span> <span data-ttu-id="04cc7-177">Hello enregistrer copié **X509Certificate** valeur localement sur votre ordinateur dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="04cc7-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="04cc7-178">Sur votre TOPdesk - Secure site d’entreprise, Bonjour **TOPdesk** menu, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="04cc7-179">![Paramètres](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="04cc7-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="04cc7-180">Cliquez sur **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="04cc7-181">![Paramètres de connexion](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Paramètres de connexion")</span><span class="sxs-lookup"><span data-stu-id="04cc7-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="04cc7-182">Développez hello **les paramètres de connexion** menu, puis sur **général**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="04cc7-183">![Général](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Général")</span><span class="sxs-lookup"><span data-stu-id="04cc7-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="04cc7-184">Bonjour **Public** , cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="04cc7-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span><span class="sxs-lookup"><span data-stu-id="04cc7-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="04cc7-186">Sur hello **l’assistant configuration de SAML** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="04cc7-187">![Assistant de configuration SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Assistant de configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="04cc7-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="04cc7-188">a.</span><span class="sxs-lookup"><span data-stu-id="04cc7-188">a.</span></span> <span data-ttu-id="04cc7-189">tooupload vos métadonnées téléchargée un fichier, sous **les métadonnées de fédération**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="04cc7-190">b.</span><span class="sxs-lookup"><span data-stu-id="04cc7-190">b.</span></span> <span data-ttu-id="04cc7-191">tooupload fichier de votre certificat, sous **Certificate (RSA)**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="04cc7-192">c.</span><span class="sxs-lookup"><span data-stu-id="04cc7-192">c.</span></span> <span data-ttu-id="04cc7-193">fichier de logo hello tooupload que vous avez obtenu à partir de l’équipe de support technique TOPdesk hello sous **icône du Logo**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="04cc7-194">d.</span><span class="sxs-lookup"><span data-stu-id="04cc7-194">d.</span></span> <span data-ttu-id="04cc7-195">Bonjour **attribut nom d’utilisateur** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="04cc7-196">e.</span><span class="sxs-lookup"><span data-stu-id="04cc7-196">e.</span></span> <span data-ttu-id="04cc7-197">Bonjour **nom d’affichage** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="04cc7-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="04cc7-198">f.</span><span class="sxs-lookup"><span data-stu-id="04cc7-198">f.</span></span> <span data-ttu-id="04cc7-199">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-199">Click **Save**.</span></span>

17. <span data-ttu-id="04cc7-200">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="04cc7-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="04cc7-201">![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="04cc7-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="04cc7-202">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="04cc7-202">Configuring user provisioning</span></span>
<span data-ttu-id="04cc7-203">Dans l’ordre tooenable Azure AD les utilisateurs toolog à TOPdesk - sécurisé, vous devez les configurer dans TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="04cc7-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="04cc7-204">Dans le cas de hello de TOPdesk -, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="04cc7-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="04cc7-205">configuration, de l’utilisateur tooconfigure effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="04cc7-206">Ouverture de session tooyour **TOPdesk - Secure** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="04cc7-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="04cc7-207">Dans le menu hello haut de hello, cliquez sur **TOPdesk \> nouveau \> les fichiers de prise en charge \> opérateur**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="04cc7-208">![Operator (Opérateur)](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator (Opérateur)")</span><span class="sxs-lookup"><span data-stu-id="04cc7-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="04cc7-209">Sur hello **nouvel opérateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="04cc7-210">![New Operator (Nouvel opérateur)](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator (Nouvel opérateur)")</span><span class="sxs-lookup"><span data-stu-id="04cc7-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="04cc7-211">a.</span><span class="sxs-lookup"><span data-stu-id="04cc7-211">a.</span></span> <span data-ttu-id="04cc7-212">Cliquez sur Général hello.</span><span class="sxs-lookup"><span data-stu-id="04cc7-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="04cc7-213">b.</span><span class="sxs-lookup"><span data-stu-id="04cc7-213">b.</span></span> <span data-ttu-id="04cc7-214">Bonjour **Surname** zone de texte Hello **général** section, le type hello nom d’un compte Azure Active Directory valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="04cc7-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="04cc7-215">c.</span><span class="sxs-lookup"><span data-stu-id="04cc7-215">c.</span></span> <span data-ttu-id="04cc7-216">Sélectionnez un **Site** compte hello Bonjour **emplacement** section.</span><span class="sxs-lookup"><span data-stu-id="04cc7-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="04cc7-217">d.</span><span class="sxs-lookup"><span data-stu-id="04cc7-217">d.</span></span> <span data-ttu-id="04cc7-218">Bonjour **nom de connexion** zone de texte Hello **TOPdesk Login** , tapez un nom de connexion pour votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="04cc7-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="04cc7-219">e.</span><span class="sxs-lookup"><span data-stu-id="04cc7-219">e.</span></span> <span data-ttu-id="04cc7-220">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="04cc7-221">Vous pouvez utiliser n’importe quel autre TOPdesk - compte d’utilisateur sécurisé de création ou API fournies par TOPdesk - Secure tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="04cc7-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="04cc7-222">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="04cc7-222">Assigning users</span></span>
<span data-ttu-id="04cc7-223">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="04cc7-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="04cc7-224">tooassign utilisateurs tooTOPdesk - Secure, procédez de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="04cc7-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="04cc7-225">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="04cc7-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="04cc7-226">Sur hello ** TOPdesk - Secure ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="04cc7-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="04cc7-227">![Affecter des utilisateurs](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="04cc7-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="04cc7-228">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="04cc7-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="04cc7-229">![Oui](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="04cc7-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="04cc7-230">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="04cc7-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="04cc7-231">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="04cc7-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

