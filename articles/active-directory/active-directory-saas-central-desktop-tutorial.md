---
title: "Didacticiel : Intégration d’Azure Active Directory à Central Desktop | Microsoft Docs"
description: "Apprenez à utiliser Central Desktop avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="3c027-103">Didacticiel : Intégration d’Azure Active Directory à Central Desktop</span><span class="sxs-lookup"><span data-stu-id="3c027-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="3c027-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="3c027-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="3c027-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3c027-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="3c027-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="3c027-106">A valid Azure subscription</span></span>
* <span data-ttu-id="3c027-107">Un abonnement Central Desktop pour lequel l’authentification unique est activée / locataire Central Desktop</span><span class="sxs-lookup"><span data-stu-id="3c027-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="3c027-108">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="3c027-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="3c027-109">Activation de l’intégration d’applications pour Central Desktop</span><span class="sxs-lookup"><span data-stu-id="3c027-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="3c027-110">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="3c027-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="3c027-111">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="3c027-111">Configuring user provisioning</span></span>
* <span data-ttu-id="3c027-112">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="3c027-112">Assigning users</span></span>

<span data-ttu-id="3c027-113">![Scénario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="3c027-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="3c027-114">Activer l’intégration d’applications pour Central Desktop</span><span class="sxs-lookup"><span data-stu-id="3c027-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="3c027-115">Cette section décrit l’activation de l’intégration d’applications pour Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="3c027-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="3c027-116">**Pour activer l’intégration d’applications pour Central Desktop, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="3c027-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="3c027-117">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c027-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="3c027-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="3c027-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="3c027-119">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="3c027-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3c027-120">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="3c027-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="3c027-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="3c027-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="3c027-122">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="3c027-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="3c027-123">![Ajouter une application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="3c027-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="3c027-124">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="3c027-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="3c027-125">![Ajouter une application à partir de la galerie](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="3c027-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="3c027-126">Dans la **zone de recherche**, tapez **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="3c027-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="3c027-127">![Galerie d’applications](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="3c027-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="3c027-128">Dans le volet de résultats, sélectionnez **Central Desktop**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="3c027-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="3c027-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="3c027-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="3c027-130">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3c027-130">Configure single sign-on</span></span>

<span data-ttu-id="3c027-131">Cette section explique comment permettre aux utilisateurs de s’authentifier sur Central Desktop avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="3c027-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="3c027-132">Dans le cadre de cette procédure, vous devez télécharger un certificat codé en base 64 sur votre locataire Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="3c027-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="3c027-133">Si cette procédure ne vous est pas familière, consultez [Comment convertir un certificat binaire en fichier texte](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="3c027-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="3c027-134">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3c027-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="3c027-135">Dans le portail Azure classic, sur le **Central Desktop** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** pour ouvrir la ** configurer Single Sign On ** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3c027-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="3c027-136">![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="3c027-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="3c027-137">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Central Desktop**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="3c027-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="3c027-138">![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="3c027-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="3c027-139">Dans la page **Configurer l’URL de l’application**, procédez comme suit, puis cliquez sur **Suivant** :</span><span class="sxs-lookup"><span data-stu-id="3c027-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="3c027-140">Dans la zone de texte **URL de connexion à Central Desktop**, tapez l’URL de votre locataire Central Desktop (par exemple, *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="3c027-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="3c027-141">Dans la zone de texte URL de réponse Central Desktop, tapez votre URL AssertionConsumerService Central Desktop (par exemple, https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="3c027-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="3c027-142">Vous pouvez obtenir la valeur à partir des métadonnées de Central Desktop (par exemple, *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="3c027-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="3c027-143">![Configurer l’URL de l’application](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="3c027-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="3c027-144">Dans la page **Configurer l’authentification unique sur Central Desktop**, pour télécharger votre certificat, cliquez sur **Télécharger le certificat**, puis enregistrez le fichier de certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3c027-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="3c027-145">![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="3c027-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="3c027-146">Connectez-vous à votre locataire **Central Desktop** .</span><span class="sxs-lookup"><span data-stu-id="3c027-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="3c027-147">Accédez à **Settings**, cliquez sur **Advanced**, puis sur **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="3c027-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="3c027-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span><span class="sxs-lookup"><span data-stu-id="3c027-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="3c027-149">Dans la page **Single Sign On Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3c027-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="3c027-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="3c027-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="3c027-151">Sélectionnez **Activer l’authentification unique SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="3c027-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="3c027-152">Dans le portail Azure Classic, dans la page **Configurer l’authentification unique sur Central Desktop**, copiez la valeur **URL de l’émetteur**, puis collez-la dans la zone de texte **SSO URL**.</span><span class="sxs-lookup"><span data-stu-id="3c027-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="3c027-153">Dans le portail Azure Classic, dans la page **Configurer l’authentification unique sur Central Desktop**, copiez la valeur **URL de connexion distante**, puis collez-la dans la zone de texte **SSO Login URL**.</span><span class="sxs-lookup"><span data-stu-id="3c027-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="3c027-154">Dans le portail Azure Classic, dans la page **Configurer l’authentification unique sur Central Desktop**, copiez la valeur **URL du service de déconnexion unique**, puis collez-la dans la zone de texte **SSO Logout URL**.</span><span class="sxs-lookup"><span data-stu-id="3c027-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="3c027-155">Dans la section **Message Signature Verification Method** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3c027-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="3c027-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span><span class="sxs-lookup"><span data-stu-id="3c027-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="3c027-157">Sélectionnez **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="3c027-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="3c027-158">Dans la liste **SSO Certificate**, sélectionnez **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="3c027-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="3c027-159">Créez un fichier texte à partir du certificat téléchargé, copiez le contenu du fichier texte et collez-le dans le champ **SSO Certificate** .</span><span class="sxs-lookup"><span data-stu-id="3c027-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="3c027-160">Pour plus d’informations, consultez [Comment convertir un certificat binaire en fichier texte](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="3c027-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="3c027-161">Sélectionnez **Display a link to your SAMLv2 login page**.</span><span class="sxs-lookup"><span data-stu-id="3c027-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="3c027-162">Cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="3c027-162">Click **Update**.</span></span>
10. <span data-ttu-id="3c027-163">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3c027-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="3c027-164">![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="3c027-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="3c027-165">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="3c027-165">Configure user provisioning</span></span>

<span data-ttu-id="3c027-166">Pour que les utilisateurs AAD puissent se connecter, ils doivent être approvisionnés dans l’application Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="3c027-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="3c027-167">Cette section explique comment créer des comptes d’utilisateur AAD dans Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="3c027-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="3c027-168">**Pour approvisionner des comptes d’utilisateur dans Central Desktop :**</span><span class="sxs-lookup"><span data-stu-id="3c027-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="3c027-169">Connectez-vous à votre locataire Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="3c027-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="3c027-170">Accédez à **People \> Internal Member**.</span><span class="sxs-lookup"><span data-stu-id="3c027-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="3c027-171">Cliquez sur **Ajouter des membres internes**.</span><span class="sxs-lookup"><span data-stu-id="3c027-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="3c027-172">![Personnes](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="3c027-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="3c027-173">Dans la zone de texte **Email Address of New Members**, tapez un compte AAD à approvisionner, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="3c027-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="3c027-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span><span class="sxs-lookup"><span data-stu-id="3c027-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="3c027-175">Cliquez sur **Add Internal member(s)**.</span><span class="sxs-lookup"><span data-stu-id="3c027-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="3c027-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span><span class="sxs-lookup"><span data-stu-id="3c027-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="3c027-177">Les utilisateurs que vous avez ajoutés recevront un message électronique contenant un lien de confirmation sur lequel ils doivent cliquer pour activer le compte.</span><span class="sxs-lookup"><span data-stu-id="3c027-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="3c027-178">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Central Desktop pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c027-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="3c027-179">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="3c027-179">Assign users</span></span>
<span data-ttu-id="3c027-180">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="3c027-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="3c027-181">**Pour affecter des utilisateurs à Central Desktop, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="3c027-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="3c027-182">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="3c027-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="3c027-183">Dans la page d’intégration d’application **Central Desktop**, cliquez sur **Affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3c027-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="3c027-184">![Affecter des utilisateurs](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="3c027-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="3c027-185">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="3c027-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="3c027-186">![Oui](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="3c027-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="3c027-187">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="3c027-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="3c027-188">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3c027-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

