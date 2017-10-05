---
title: "Didacticiel : Intégration d’Azure Active Directory à Cisco Webex | Microsoft Docs"
description: "Apprenez à utiliser Cisco Webex avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore !"
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
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="7c976-103">Didacticiel : Intégration d’Azure Active Directory à Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="7c976-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="7c976-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="7c976-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="7c976-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7c976-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="7c976-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="7c976-106">A valid Azure subscription</span></span>
* <span data-ttu-id="7c976-107">Un locataire Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="7c976-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="7c976-108">À l’issue de ce didacticiel, les utilisateurs Azure AD que vous avez affectés à Cisco Webex pourront s’authentifier de manière unique dans l’application sur votre site d’entreprise Cisco Webex (connexion initiée par le fournisseur du service) ou à l’aide de la [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7c976-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="7c976-109">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="7c976-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="7c976-110">Activation de l’intégration d’applications pour Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="7c976-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="7c976-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="7c976-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="7c976-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="7c976-112">Configuring user provisioning</span></span>
* <span data-ttu-id="7c976-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="7c976-113">Assigning users</span></span>

<span data-ttu-id="7c976-114">![Scénario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="7c976-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="7c976-115">Activer l’intégration d’applications pour Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="7c976-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="7c976-116">Cette section décrit l’activation de l’intégration d’applications pour Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="7c976-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="7c976-117">**Pour activer l’intégration d’applications pour Cisco Webex, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="7c976-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="7c976-118">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c976-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="7c976-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="7c976-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="7c976-120">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="7c976-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7c976-121">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="7c976-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="7c976-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="7c976-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="7c976-123">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="7c976-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="7c976-124">![Ajouter une application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="7c976-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="7c976-125">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="7c976-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="7c976-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="7c976-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="7c976-127">Dans la **zone de recherche**, tapez **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="7c976-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="7c976-128">![Galerie d’applications](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="7c976-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="7c976-129">Dans le volet de résultats, sélectionnez **Cisco Webex**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7c976-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="7c976-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="7c976-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="7c976-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7c976-131">Configure single sign-on</span></span>

<span data-ttu-id="7c976-132">Cette section explique comment permettre aux utilisateurs de s’authentifier sur Cisco Webex avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="7c976-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="7c976-133">Dans le cadre de cette procédure, vous devez créer un certificat codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="7c976-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="7c976-134">Si cette procédure ne vous est pas familière, consultez [Conversion d’un certificat binaire en fichier texte](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="7c976-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="7c976-135">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7c976-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="7c976-136">Sur la page d’intégration d’applications **Cisco Webex** du Portail Azure Classic, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7c976-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="7c976-137">![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="7c976-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="7c976-138">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Cisco Webex**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7c976-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="7c976-139">![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="7c976-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="7c976-140">Dans la page **Configurer l’URL de l’application**, procédez comme suit, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7c976-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="7c976-141">![Configurer l’URL de l’application](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="7c976-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="7c976-142">Dans la zone de texte **URL de connexion**, tapez l’URL de votre locataire Cisco Webex (par exemple, *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="7c976-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="7c976-143">Dans la zone de texte **URL de réponse Cisco Webex**, saisissez votre **URL AssertionConsumerService Cisco Webex** (par exemple : *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span><span class="sxs-lookup"><span data-stu-id="7c976-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="7c976-144">Dans la page **Configurer l’authentification unique sur Cisco Webex**, pour télécharger votre certificat, cliquez sur **Télécharger le certificat**, puis enregistrez le fichier de certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7c976-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="7c976-145">![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="7c976-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="7c976-146">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Cisco Webex en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7c976-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="7c976-147">Dans le menu situé en haut, cliquez sur **Site Administration**.</span><span class="sxs-lookup"><span data-stu-id="7c976-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="7c976-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span><span class="sxs-lookup"><span data-stu-id="7c976-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="7c976-149">Dans la section **Manage Site**, cliquez sur **SSO Configuration**.</span><span class="sxs-lookup"><span data-stu-id="7c976-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="7c976-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span><span class="sxs-lookup"><span data-stu-id="7c976-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="7c976-151">Dans la section Configuration de l’authentification unique web fédérée, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7c976-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="7c976-152">![Configuration de l’authentification unique web fédérée](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuration de l’authentification unique web fédérée")</span><span class="sxs-lookup"><span data-stu-id="7c976-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="7c976-153">Dans la liste **Protocole de fédération**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7c976-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="7c976-154">Créez un fichier **codé en base 64** à partir du certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7c976-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="7c976-155">Pour plus d’informations, consultez [Conversion d’un certificat binaire en fichier texte](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="7c976-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="7c976-156">Ouvrez le certificat codé en base 64 dans le Bloc-notes, puis copiez son contenu.</span><span class="sxs-lookup"><span data-stu-id="7c976-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="7c976-157">Cliquez sur **Import SAML Metadata**, puis collez votre certificat codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="7c976-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="7c976-158">Dans le portail Azure Classic, dans la page **Configurer l’authentification unique sur Cisco Webex** de la boîte de dialogue, copiez la valeur **URL de l’émetteur**, puis collez-la dans la zone de texte **Issuer for SAML (IdP ID)**.</span><span class="sxs-lookup"><span data-stu-id="7c976-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="7c976-159">Dans le portail Azure Classic, dans la page **Configurer l’authentification unique sur Cisco Webex**, copiez la valeur **URL de connexion distante**, puis collez-la dans la zone de texte **Customer SSO Service Login URL**.</span><span class="sxs-lookup"><span data-stu-id="7c976-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="7c976-160">Dans la liste **NameID Format**, sélectionnez **Email address**.</span><span class="sxs-lookup"><span data-stu-id="7c976-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="7c976-161">Dans la zone de texte **AuthnContextClassRef**, tapez **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="7c976-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="7c976-162">Dans le portail Azure Classic, dans la page **Configurer l’authentification unique sur Cisco Webex**, copiez la valeur **URL de déconnexion distante**, puis collez-la dans la zone de texte **Customer SSO Service Logout URL**.</span><span class="sxs-lookup"><span data-stu-id="7c976-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="7c976-163">Cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="7c976-163">Click **Update**.</span></span>
9. <span data-ttu-id="7c976-164">Dans le portail Azure Classic, dans la page **Configurer l’authentification unique sur Cisco Webex**, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7c976-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="7c976-165">![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="7c976-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="7c976-166">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="7c976-166">Configure user provisioning</span></span>

<span data-ttu-id="7c976-167">Pour permettre aux utilisateurs Azure AD de se connecter à Cisco Webex, vous devez les approvisionner dans Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="7c976-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="7c976-168">En l’occurrence, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="7c976-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="7c976-169">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7c976-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="7c976-170">Connectez-vous à votre locataire **Cisco Webex** .</span><span class="sxs-lookup"><span data-stu-id="7c976-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="7c976-171">Accédez à **Manage Users \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="7c976-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="7c976-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span><span class="sxs-lookup"><span data-stu-id="7c976-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="7c976-173">Dans la section Ajouter un utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7c976-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="7c976-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="7c976-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="7c976-175">Dans la zone **Account Type**, sélectionnez **Host**.</span><span class="sxs-lookup"><span data-stu-id="7c976-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="7c976-176">Tapez les informations d’un utilisateur Azure AD existant dans les zones de texte suivantes : **Prénom, Nom**, **Nom d’utilisateur**, **Adresse de messagerie**, **Mot de passe**, **Confirmer le mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7c976-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="7c976-177">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7c976-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="7c976-178">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Cisco Webex pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c976-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="7c976-179">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="7c976-179">Assign users</span></span>
<span data-ttu-id="7c976-180">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="7c976-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="7c976-181">**Pour affecter des utilisateurs à Cisco Webex, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="7c976-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="7c976-182">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="7c976-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="7c976-183">Sur la page d’intégration d’applications **Cisco Webex**, cliquez sur **Affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7c976-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="7c976-184">![Affecter des utilisateurs](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="7c976-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="7c976-185">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="7c976-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="7c976-186">![Oui](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="7c976-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="7c976-187">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="7c976-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="7c976-188">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7c976-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

