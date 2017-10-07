---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform | Microsoft Docs"
description: "Découvrez comment toouse SAP HANA Cloud Platform avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
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
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="39f5f-103">Didacticiel : Intégration d’Azure Active Directory avec SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="39f5f-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="39f5f-104">objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et la plateforme Cloud SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="39f5f-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="39f5f-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="39f5f-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="39f5f-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="39f5f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="39f5f-107">Un compte SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="39f5f-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="39f5f-108">À l’issue de ce didacticiel, hello utilisateurs Azure AD que vous avez affectés tooSAP HANA Cloud Platform sera toosingle en mesure de connexion dans l’application hello utilisant hello [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39f5f-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="39f5f-109">Vous devez toodeploy votre propre application ou s’abonner tooan application sur votre serveur SAP HANA Cloud Platform connectent tootest compte unique.</span><span class="sxs-lookup"><span data-stu-id="39f5f-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="39f5f-110">Dans ce didacticiel, une application est déployée dans le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="39f5f-111">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="39f5f-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="39f5f-112">Activation de l’intégration d’application hello pour SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="39f5f-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="39f5f-113">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="39f5f-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="39f5f-114">Affectation d’un utilisateur tooa de rôle</span><span class="sxs-lookup"><span data-stu-id="39f5f-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="39f5f-115">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="39f5f-115">Assigning users</span></span>

<span data-ttu-id="39f5f-116">![Scénario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="39f5f-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="39f5f-117">Activation de l’intégration d’application hello pour SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="39f5f-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="39f5f-118">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="39f5f-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="39f5f-119">**intégration d’application hello tooenable pour SAP HANA Cloud Platform, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="39f5f-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="39f5f-120">Bonjour portail de gestion Azure, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="39f5f-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="39f5f-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="39f5f-122">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="39f5f-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="39f5f-123">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="39f5f-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="39f5f-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="39f5f-125">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="39f5f-126">![Ajouter une application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="39f5f-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="39f5f-127">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="39f5f-128">![Ajouter une application à partir de la galerie](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="39f5f-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="39f5f-129">Bonjour **zone de recherche**, type **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="39f5f-130">![Galerie d’applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="39f5f-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="39f5f-131">Dans le volet de résultats hello, sélectionnez **SAP HANA Cloud Platform**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="39f5f-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="39f5f-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="39f5f-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="39f5f-133">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="39f5f-133">Configure single sign-on</span></span>

<span data-ttu-id="39f5f-134">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooSAP HANA Cloud Platform avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="39f5f-135">Dans le cadre de cette procédure, vous êtes tooupload requis un locataire de SAP HANA Cloud Platform tooyour certificat codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="39f5f-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="39f5f-136">Si vous n’êtes pas familiarisé avec cette procédure, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="39f5f-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="39f5f-137">**tooconfigure sur l’authentification unique, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="39f5f-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="39f5f-138">Bonjour portail Azure classic sur hello **SAP HANA Cloud Platform** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique**boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="39f5f-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="39f5f-139">![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="39f5f-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="39f5f-140">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooSAP HANA Cloud Platform** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="39f5f-141">![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="39f5f-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="39f5f-142">Dans une fenêtre de navigateur web, connectez-vous toohello Cockpit de plateforme Cloud SAP HANA à https://account. \<hôte du paysage\>.ondemand.com/cockpit (par exemple : *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="39f5f-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="39f5f-143">Cliquez sur hello **confiance** onglet.</span><span class="sxs-lookup"><span data-stu-id="39f5f-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="39f5f-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span><span class="sxs-lookup"><span data-stu-id="39f5f-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="39f5f-145">Dans la section Gestion de confiance, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="39f5f-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="39f5f-146">![Obtenir les métadonnées](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obtenir les métadonnées")</span><span class="sxs-lookup"><span data-stu-id="39f5f-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="39f5f-147">Cliquez sur hello **Local Service Provider** onglet.</span><span class="sxs-lookup"><span data-stu-id="39f5f-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="39f5f-148">hello de toodownload fichier de métadonnées de plateforme Cloud SAP HANA, cliquez sur **obtenir les métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="39f5f-149">Portail de classique hello Active Azure, sur hello **Configure App URL** page, effectuer hello comme suit, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="39f5f-150">![Configurer l’URL de l’application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="39f5f-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="39f5f-151">Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par votre toosign d’utilisateurs dans votre **SAP HANA Cloud Platform** application.</span><span class="sxs-lookup"><span data-stu-id="39f5f-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="39f5f-152">Il s’agit de hello URL spécifique au compte d’une ressource protégée dans votre application SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="39f5f-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="39f5f-153">URL Hello est basée sur hello modèle : *https://\<applicationName\>\<accountName\>.\< hôte de paysage\>.ondemand.com/\<chemin d’accès\_à\_protégé\_ressource\>*  (par exemple : *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="39f5f-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="39f5f-154">Il s’agit d’URL de hello dans votre application de plateforme Cloud SAP HANA nécessitant hello utilisateur tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="39f5f-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="39f5f-155">Ouvrez le fichier de métadonnées de plateforme Cloud SAP HANA hello téléchargé et recherchez hello **NS3 : assertionconsumerservice** balise.</span><span class="sxs-lookup"><span data-stu-id="39f5f-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="39f5f-156">Copier la valeur hello Hello **emplacement** d’attribut, puis collez-le dans hello **URL de réponse SAP HANA Cloud Platform** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="39f5f-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="39f5f-157">Sur hello **configurer l’authentification unique sur SAP HANA Cloud Platform** page, toodownload vos métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="39f5f-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="39f5f-158">![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="39f5f-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="39f5f-159">Sur hello Cockpit de plateforme Cloud SAP HANA, Bonjour **Local Service Provider** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="39f5f-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="39f5f-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="39f5f-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="39f5f-161">Cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="39f5f-162">Comme **Configuration Type**, sélectionnez **Custom**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="39f5f-163">En tant que **Local Provider Name**, laissez la valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="39f5f-164">toogenerate un **clé de signature** et un **certificat de signature de** paire de clés, cliquez sur **générer la paire de clés**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="39f5f-165">Pour **Principal Propagation**, sélectionnez **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="39f5f-166">Pour **Force Authentication**, sélectionnez **Disabled**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="39f5f-167">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-167">Click **Save**.</span></span>

9. <span data-ttu-id="39f5f-168">Cliquez sur hello **fournisseur d’identité approuvé** onglet, puis cliquez sur **ajouter un fournisseur d’identité approuvé**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="39f5f-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="39f5f-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="39f5f-170">liste de hello toomanage de fournisseurs d’identité approuvés, vous devez toohave choisi hello type de configuration personnalisée dans hello section Local Service Provider.</span><span class="sxs-lookup"><span data-stu-id="39f5f-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="39f5f-171">Pour le type de configuration par défaut, vous avez un Service d’ID SAP de toohello approbation non modifiable et implicite.</span><span class="sxs-lookup"><span data-stu-id="39f5f-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="39f5f-172">Pour None, vous n’avez aucun paramètre d’approbation.</span><span class="sxs-lookup"><span data-stu-id="39f5f-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="39f5f-173">Cliquez sur hello **général** onglet, puis cliquez sur **Parcourir** hello de tooupload téléchargé le fichier de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="39f5f-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="39f5f-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span><span class="sxs-lookup"><span data-stu-id="39f5f-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="39f5f-175">Après avoir téléchargé le fichier de métadonnées hello, des valeurs hello **URL de connexion unique**, **URL de déconnexion unique** et **certificat de signature** sont remplis automatiquement.</span><span class="sxs-lookup"><span data-stu-id="39f5f-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="39f5f-176">Cliquez sur hello **attributs** onglet.</span><span class="sxs-lookup"><span data-stu-id="39f5f-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="39f5f-177">Sur hello **attributs** onglet, effectuez hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="39f5f-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="39f5f-178">![Attributs](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="39f5f-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="39f5f-179">Cliquez sur **based Attribute**, puis ajoutez hello suivant des attributs basés sur une assertion :</span><span class="sxs-lookup"><span data-stu-id="39f5f-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="39f5f-180">Assertion Attribute</span><span class="sxs-lookup"><span data-stu-id="39f5f-180">Assertion Attribute</span></span> | <span data-ttu-id="39f5f-181">Principal Attribute</span><span class="sxs-lookup"><span data-stu-id="39f5f-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="39f5f-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="39f5f-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="39f5f-183">firstname</span><span class="sxs-lookup"><span data-stu-id="39f5f-183">firstname</span></span> |
    | <span data-ttu-id="39f5f-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="39f5f-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="39f5f-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="39f5f-185">lastname</span></span> |
    | <span data-ttu-id="39f5f-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="39f5f-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="39f5f-187">email</span><span class="sxs-lookup"><span data-stu-id="39f5f-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="39f5f-188">configuration Hello d’attributs de hello dépend de l’ou les applications hello sur HCP sont développées, autrement dit, attributs attendus dans hello réponse SAML et sous le nom (attribut Principal) qu’ils accèdent à cet attribut dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="39f5f-189">Hello **attribut par défaut** Bonjour capture d’écran est uniquement à des fins d’illustration.</span><span class="sxs-lookup"><span data-stu-id="39f5f-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="39f5f-190">Il n’est pas nécessaire de travail de scénario toomake hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="39f5f-191">Hello les noms et valeurs des **attribut Principal** illustré hello capture d’écran dépendent de la façon dont l’application hello est développée.</span><span class="sxs-lookup"><span data-stu-id="39f5f-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="39f5f-192">Il est possible que votre application exige des mappages différents.</span><span class="sxs-lookup"><span data-stu-id="39f5f-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="39f5f-193">Bonjour portail Azure classic sur hello **configurer l’authentification unique sur SAP HANA Cloud Platform** page de boîte de dialogue, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="39f5f-194">![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="39f5f-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="39f5f-195">Groupes basés sur une assertion</span><span class="sxs-lookup"><span data-stu-id="39f5f-195">Assertion-based groups</span></span>
<span data-ttu-id="39f5f-196">Une étape facultative est de configurer des groupes basés sur une assertion pour votre fournisseur d’identité Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="39f5f-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="39f5f-197">À l’aide de groupes sur SAP HANA Cloud Platform vous permet d’affecter toodynamically un ou plus tooone d’utilisateurs ou de plusieurs rôles dans vos applications SAP HANA Cloud Platform, déterminés par les valeurs des attributs de hello SAML 2.0 assertion.</span><span class="sxs-lookup"><span data-stu-id="39f5f-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="39f5f-198">Par exemple, si hello assertion contenant l’attribut de hello »*contrat = temporaire*«, vous pouvez tous les utilisateurs affectés toobe toohello ajouté groupe »*temporaire*».</span><span class="sxs-lookup"><span data-stu-id="39f5f-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="39f5f-199">groupe de Hello »*temporaire*» peut contenir un ou plusieurs rôles à partir d’une ou plusieurs applications déployées dans votre compte SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="39f5f-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="39f5f-200">Utilisez des groupes basés sur une assertion toosimultaneously affecter plusieurs utilisateurs tooone ou plusieurs rôles d’applications dans votre compte SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="39f5f-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="39f5f-201">Si vous ne souhaitez qu’un seul ou un petit nombre de rôles d’utilisateurs toospecific de tooassign, nous vous recommandons de les affecter directement dans hello »**autorisations**« onglet du cockpit de plateforme Cloud SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="39f5f-202">Affecter un utilisateur tooa de rôle</span><span class="sxs-lookup"><span data-stu-id="39f5f-202">Assign a role tooa user</span></span>
<span data-ttu-id="39f5f-203">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans SAP HANA Cloud Platform, vous devez attribuer des rôles dans hello SAP HANA Cloud Platform toothem.</span><span class="sxs-lookup"><span data-stu-id="39f5f-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="39f5f-204">**tooassign un utilisateur tooa de rôle, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="39f5f-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="39f5f-205">Connectez-vous à tooyour **SAP HANA Cloud Platform** cockpit.</span><span class="sxs-lookup"><span data-stu-id="39f5f-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="39f5f-206">Effectuez les opérations suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="39f5f-206">Perform hello following:</span></span>
   
   <span data-ttu-id="39f5f-207">![Autorisations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorisations")</span><span class="sxs-lookup"><span data-stu-id="39f5f-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="39f5f-208">Cliquez sur **Authorization**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="39f5f-209">Cliquez sur hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="39f5f-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="39f5f-210">Bonjour **utilisateur** zone de texte, adresse de messagerie de l’utilisateur de type hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="39f5f-211">Cliquez sur **affecter** rôle tooa tooassign hello.</span><span class="sxs-lookup"><span data-stu-id="39f5f-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="39f5f-212">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="39f5f-213">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="39f5f-213">Assign users</span></span>
<span data-ttu-id="39f5f-214">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="39f5f-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="39f5f-215">**tooassign utilisateurs tooSAP HANA Cloud Platform, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="39f5f-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="39f5f-216">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="39f5f-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="39f5f-217">Sur hello **SAP HANA Cloud Platform** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="39f5f-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="39f5f-218">![Affecter des utilisateurs](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="39f5f-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="39f5f-219">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="39f5f-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="39f5f-220">![Oui](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="39f5f-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="39f5f-221">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="39f5f-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="39f5f-222">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39f5f-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

