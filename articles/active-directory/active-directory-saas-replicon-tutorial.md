---
title: "Didacticiel : Intégration d’Azure Active Directory à Replicon | Microsoft Docs"
description: "Découvrez comment toouse Replicon avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
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
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="42341-103">Didacticiel : Intégration d’Azure Active Directory à Replicon</span><span class="sxs-lookup"><span data-stu-id="42341-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="42341-104">objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Replicon.</span><span class="sxs-lookup"><span data-stu-id="42341-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="42341-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="42341-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="42341-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="42341-106">A valid Azure subscription</span></span>
* <span data-ttu-id="42341-107">Un locataire Replicon</span><span class="sxs-lookup"><span data-stu-id="42341-107">A Replicon tenant</span></span>

<span data-ttu-id="42341-108">À l’issue de ce didacticiel, hello Azure AD utilisateurs tooReplicon sera toosingle en mesure de l’authentification sur application hello à votre site d’entreprise Replicon (service initiée par le fournisseur de session) ou à l’aide de hello [Introduction toohello accès Panneau de configuration](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42341-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="42341-109">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="42341-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="42341-110">Activation de l’intégration d’application hello pour Replicon</span><span class="sxs-lookup"><span data-stu-id="42341-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="42341-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="42341-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="42341-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="42341-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="42341-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="42341-113">Assigning users</span></span>

<span data-ttu-id="42341-114">![Scénario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="42341-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="42341-115">Activer l’intégration d’application hello pour Replicon</span><span class="sxs-lookup"><span data-stu-id="42341-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="42341-116">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Replicon.</span><span class="sxs-lookup"><span data-stu-id="42341-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="42341-117">**intégration d’application hello tooenable pour Replicon, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42341-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="42341-118">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42341-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="42341-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="42341-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="42341-120">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="42341-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="42341-121">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="42341-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="42341-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="42341-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="42341-123">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="42341-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="42341-124">![Ajouter une application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="42341-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="42341-125">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="42341-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="42341-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-replicon-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="42341-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="42341-127">Bonjour **zone de recherche**, type **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="42341-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="42341-128">![Galerie d’applications](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="42341-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="42341-129">Dans le volet de résultats hello, sélectionnez **Replicon**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="42341-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="42341-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="42341-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="42341-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="42341-131">Configure single sign-on</span></span>

<span data-ttu-id="42341-132">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooReplicon avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="42341-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="42341-133">**tooconfigure sur l’authentification unique, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42341-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="42341-134">Bonjour portail Azure classic sur hello **Replicon** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42341-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="42341-135">![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="42341-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="42341-136">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooReplicon** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="42341-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="42341-137">![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="42341-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="42341-138">Sur hello **Configure App URL** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42341-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="42341-139">![Configurer l’URL de l’application](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="42341-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="42341-140">Bonjour **URL de connexion Replicon** zone de texte, tapez l’URL de votre client Replicon (par exemple : *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="42341-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="42341-141">Bonjour **URL de réponse Replicon** zone de texte, tapez votre URL Replicon **AssertionConsumerService** URL (par exemple : *https://global.replicon.com/ ! / saml2/entreprise/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="42341-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="42341-142">Vous pouvez obtenir hello URL à partir des métadonnées Replicon hello : **https://global.replicon.com/ ! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="42341-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="42341-143">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="42341-143">Click **Next**.</span></span>

4. <span data-ttu-id="42341-144">Sur hello **configurer l’authentification unique sur Replicon** page, toodownload vos métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez les métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="42341-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="42341-145">![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="42341-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="42341-146">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Replicon en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="42341-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="42341-147">tooconfigure SAML 2.0, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42341-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="42341-148">![Activer l’authentification SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Activer l’authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="42341-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="42341-149">toodisplay hello **EnableSAML Authentication2** boîte de dialogue, ajouter hello suivant tooyour URL, après votre clé d’entreprise : **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="42341-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="42341-150">Hello Voici schéma hello de hello des URL complète :</span><span class="sxs-lookup"><span data-stu-id="42341-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="42341-151">**https://na2.replicon.com/\<CléDeVotreEntreprise\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="42341-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="42341-152">Cliquez sur hello  **+**  tooexpand hello **v20Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="42341-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="42341-153">Cliquez sur hello  **+**  tooexpand hello **metaDataConfiguration** section.</span><span class="sxs-lookup"><span data-stu-id="42341-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="42341-154">Cliquez sur **choisir un fichier**, tooselect votre fichier XML de métadonnées de fournisseur identité, puis cliquez sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="42341-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="42341-155">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42341-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="42341-156">![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="42341-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="42341-157">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="42341-157">Configure user provisioning</span></span>

<span data-ttu-id="42341-158">Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Replicon, ils doivent être configurés dans Replicon.</span><span class="sxs-lookup"><span data-stu-id="42341-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="42341-159">Dans les cas de hello de Replicon, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="42341-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="42341-160">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42341-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="42341-161">Dans une fenêtre de navigateur web, connectez-vous à votre site d’entreprise Replicon en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="42341-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="42341-162">Accédez trop**Administration \> utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="42341-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="42341-163">![Utilisateurs](./media/active-directory-saas-replicon-tutorial/IC777806.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="42341-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="42341-164">Cliquez sur **+Add User**.</span><span class="sxs-lookup"><span data-stu-id="42341-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="42341-165">![Ajouter un utilisateur](./media/active-directory-saas-replicon-tutorial/IC777807.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="42341-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="42341-166">Bonjour **profil utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="42341-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="42341-167">![Profil utilisateur](./media/active-directory-saas-replicon-tutorial/IC777808.png "Profil utilisateur")</span><span class="sxs-lookup"><span data-stu-id="42341-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="42341-168">Bonjour **nom de connexion** zone de texte, hello de type Azure AD adresse de messagerie de l’utilisateur hello Azure AD que vous tooprovision.</span><span class="sxs-lookup"><span data-stu-id="42341-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="42341-169">Pour **Authentication Type**, sélectionnez **SSO**.</span><span class="sxs-lookup"><span data-stu-id="42341-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="42341-170">Bonjour **service** zone de texte, tapez le département de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="42341-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="42341-171">Pour **Employee Type**, sélectionnez **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="42341-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="42341-172">Cliquez sur **Save User Profile**.</span><span class="sxs-lookup"><span data-stu-id="42341-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="42341-173">Vous pouvez utiliser n’importe quel autre Replicon utilisateur compte outil de création ou API fournie par Replicon tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="42341-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="42341-174">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="42341-174">Assign users</span></span>
<span data-ttu-id="42341-175">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="42341-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="42341-176">**tooassign utilisateurs tooReplicon, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42341-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="42341-177">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="42341-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="42341-178">Sur hello **Replicon** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="42341-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="42341-179">![Affecter des utilisateurs](./media/active-directory-saas-replicon-tutorial/IC777809.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="42341-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="42341-180">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="42341-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="42341-181">![Oui](./media/active-directory-saas-replicon-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="42341-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="42341-182">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="42341-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="42341-183">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42341-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

