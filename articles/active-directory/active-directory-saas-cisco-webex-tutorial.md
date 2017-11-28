---
title: "Didacticiel : Intégration d’Azure Active Directory à Cisco Webex | Microsoft Docs"
description: "Découvrez comment toouse Cisco Webex avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="6f235-103">Didacticiel : Intégration d’Azure Active Directory à Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="6f235-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="6f235-104">objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="6f235-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="6f235-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6f235-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="6f235-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="6f235-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6f235-107">Un locataire Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="6f235-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="6f235-108">À l’issue de ce didacticiel, hello utilisateurs Azure AD que vous avez affectés tooCisco Webex sera en mesure de toosingle signe dans une application hello sur votre site d’entreprise Cisco Webex (service initiée par le fournisseur de session), ou à l’aide de hello [Introduction toohello Accéder au panneau de configuration](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f235-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="6f235-109">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="6f235-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="6f235-110">Activation de l’intégration d’application hello pour Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="6f235-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="6f235-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="6f235-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="6f235-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6f235-112">Configuring user provisioning</span></span>
* <span data-ttu-id="6f235-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6f235-113">Assigning users</span></span>

<span data-ttu-id="6f235-114">![Scénario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="6f235-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="6f235-115">Activer l’intégration d’application hello pour Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="6f235-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="6f235-116">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="6f235-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="6f235-117">**intégration d’application hello tooenable pour Cisco Webex, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6f235-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f235-118">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6f235-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="6f235-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6f235-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6f235-120">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="6f235-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="6f235-121">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="6f235-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="6f235-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="6f235-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6f235-123">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="6f235-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="6f235-124">![Ajouter une application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="6f235-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="6f235-125">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="6f235-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="6f235-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="6f235-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="6f235-127">Bonjour **zone de recherche**, type **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="6f235-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="6f235-128">![Galerie d’applications](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="6f235-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="6f235-129">Dans le volet de résultats hello, sélectionnez **Cisco Webex**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6f235-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="6f235-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="6f235-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="6f235-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6f235-131">Configure single sign-on</span></span>

<span data-ttu-id="6f235-132">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooCisco Webex avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="6f235-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="6f235-133">Dans le cadre de cette procédure, vous êtes toocreate requis un certificat codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="6f235-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="6f235-134">Si vous n’êtes pas familiarisé avec cette procédure, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="6f235-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="6f235-135">**tooconfigure sur l’authentification unique, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6f235-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f235-136">Bonjour portail Azure classic sur hello **Cisco Webex** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6f235-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="6f235-137">![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6f235-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="6f235-138">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooCisco Webex** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="6f235-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="6f235-139">![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6f235-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="6f235-140">Sur hello **Configure App URL** page, effectuer hello comme suit, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="6f235-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="6f235-141">![Configurer l’URL de l’application](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="6f235-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="6f235-142">Bonjour **URL de connexion** zone de texte, tapez l’URL de votre client Cisco Webex (par exemple : *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="6f235-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="6f235-143">Bonjour **URL de réponse Cisco Webex** zone de texte, type votre **URL AssertionConsumerService Cisco Webex** (par exemple : *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="6f235-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="6f235-144">Sur hello **configurer l’authentification unique sur Cisco Webex** page, toodownload votre certificat, cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6f235-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="6f235-145">![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6f235-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="6f235-146">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Cisco Webex en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6f235-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="6f235-147">Dans le menu hello haut de hello, cliquez sur **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="6f235-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="6f235-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span><span class="sxs-lookup"><span data-stu-id="6f235-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="6f235-149">Bonjour **gérer le Site** , cliquez sur **Configuration SSO**.</span><span class="sxs-lookup"><span data-stu-id="6f235-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="6f235-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span><span class="sxs-lookup"><span data-stu-id="6f235-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="6f235-151">Dans la section de Configuration de SSO de Web fédéré de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6f235-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="6f235-152">![Configuration de l’authentification unique web fédérée](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuration de l’authentification unique web fédérée")</span><span class="sxs-lookup"><span data-stu-id="6f235-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="6f235-153">À partir de hello **protocole Federation** liste, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="6f235-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="6f235-154">Créez un fichier **codé en base 64** à partir du certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6f235-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="6f235-155">Pour plus d’informations, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="6f235-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="6f235-156">Ouvrez votre certificat codé en base 64 dans le bloc-notes, puis hello copie contenu de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="6f235-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="6f235-157">Cliquez sur **Import SAML Metadata**, puis collez votre certificat codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="6f235-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="6f235-158">Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Cisco Webex** page de boîte de dialogue, hello de copie **URL de l’émetteur** valeur, puis collez-le dans hello **émetteur pour SAML (ID d’IdP)** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="6f235-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="6f235-159">Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Cisco Webex** page de boîte de dialogue, hello de copie **URL de connexion distante** valeur, puis collez-le dans hello **connexion de Service d’authentification unique client URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="6f235-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="6f235-160">À partir de hello **NameID Format** liste, sélectionnez **adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="6f235-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="6f235-161">Bonjour **AuthnContextClassRef** zone de texte, type **urn : oasis : noms : tc : SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="6f235-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="6f235-162">Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Cisco Webex** page de boîte de dialogue, hello de copie **URL de déconnexion distante** valeur, puis collez-le dans hello **déconnexion du Service client SSO URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="6f235-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="6f235-163">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="6f235-163">Click **Update**.</span></span>
9. <span data-ttu-id="6f235-164">Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Cisco Webex** page de boîte de dialogue, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6f235-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="6f235-165">![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6f235-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="6f235-166">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="6f235-166">Configure user provisioning</span></span>

<span data-ttu-id="6f235-167">Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Cisco Webex, ils doivent être configurés dans Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="6f235-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="6f235-168">Dans les cas de hello de Cisco Webex, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="6f235-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="6f235-169">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6f235-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f235-170">Connectez-vous à tooyour **Cisco Webex** client.</span><span class="sxs-lookup"><span data-stu-id="6f235-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="6f235-171">Accédez trop**gérer les utilisateurs \> ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="6f235-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="6f235-172">![Ajouter des utilisateurs](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Ajouter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="6f235-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="6f235-173">Sur la section Ajouter un utilisateur de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6f235-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="6f235-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="6f235-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="6f235-175">Dans la zone **Account Type**, sélectionnez **Host**.</span><span class="sxs-lookup"><span data-stu-id="6f235-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="6f235-176">Tapez les informations de hello d’un utilisateur Azure AD existant dans hello suivant des zones de texte : **prénom, le nom**, **nom d’utilisateur**, **messagerie**, **mot de passe**, **Confirmer le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6f235-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="6f235-177">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="6f235-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="6f235-178">Vous pouvez utiliser n’importe quel autre Cisco Webex utilisateur compte outil de création ou API fournie par Cisco Webex tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="6f235-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="6f235-179">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6f235-179">Assign users</span></span>
<span data-ttu-id="6f235-180">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="6f235-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="6f235-181">**tooassign utilisateurs tooCisco Webex, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6f235-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f235-182">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="6f235-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6f235-183">Sur hello **Cisco Webex** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6f235-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="6f235-184">![Affecter des utilisateurs](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="6f235-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="6f235-185">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="6f235-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="6f235-186">![Oui](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="6f235-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6f235-187">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="6f235-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="6f235-188">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f235-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

