---
title: "Didacticiel : Intégration d’Azure Active Directory à Benefitsolver | Microsoft Docs"
description: "Apprenez à utiliser Benefitsolver avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="eb1ff-103">Didacticiel : Intégration d’Azure Active Directory à Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="eb1ff-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="eb1ff-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="eb1ff-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb1ff-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="eb1ff-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="eb1ff-106">A valid Azure subscription</span></span>
* <span data-ttu-id="eb1ff-107">Un abonnement Benefitsolver pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="eb1ff-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="eb1ff-108">À l’issue de ce didacticiel, les utilisateurs Azure AD que vous avez affectés à Benefitsolver pourront s’authentifier de manière unique dans l’application à l’aide de la [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="eb1ff-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="eb1ff-109">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="eb1ff-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="eb1ff-110">Activation de l’intégration d’applications pour Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="eb1ff-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="eb1ff-111">Configuration de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="eb1ff-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="eb1ff-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="eb1ff-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="eb1ff-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="eb1ff-113">Assigning users</span></span>

<span data-ttu-id="eb1ff-114">![Scénario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="eb1ff-115">Activation de l’intégration d’applications pour Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="eb1ff-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="eb1ff-116">Cette section décrit l’activation de l’intégration d’applications pour Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="eb1ff-117">Pour activer l’intégration d’applications pour Benefitsolver, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb1ff-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="eb1ff-118">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="eb1ff-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="eb1ff-120">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="eb1ff-121">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="eb1ff-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="eb1ff-123">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="eb1ff-124">![Ajouter une application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="eb1ff-125">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="eb1ff-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="eb1ff-127">Dans la **zone de recherche**, entrez **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="eb1ff-128">![Galerie d’applications](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="eb1ff-129">Dans le volet de résultats, sélectionnez **Benefitsolver**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="eb1ff-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="eb1ff-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="eb1ff-131">Configure single sign-on</span></span>

<span data-ttu-id="eb1ff-132">Cette section explique comment permettre aux utilisateurs de s’authentifier sur Benefitsolver avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="eb1ff-133">Votre application Benefitsolver s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration des **attributs du jeton SAML** .</span><span class="sxs-lookup"><span data-stu-id="eb1ff-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="eb1ff-134">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="eb1ff-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="eb1ff-135">![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="eb1ff-136">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb1ff-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="eb1ff-137">Dans le portail Azure Classic, sur la page d’intégration d’application **Benefitsolver**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="eb1ff-138">![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="eb1ff-139">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Benefitsolver**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="eb1ff-140">![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="eb1ff-141">Dans la page **Configurer les paramètres de l’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb1ff-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="eb1ff-142">![Configurer les paramètres d’application](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurer les paramètres d’application")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="eb1ff-143">Dans la zone de texte **URL de connexion**, saisissez **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="eb1ff-144">Dans la zone de texte **URL de réponse**, saisissez **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="eb1ff-145">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-145">Click **Next**.</span></span>
4. <span data-ttu-id="eb1ff-146">Dans la page **Configurer l’authentification unique sur Benefitsolver**, pour télécharger vos métadonnées, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier de métadonnées en local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="eb1ff-147">![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="eb1ff-148">Envoyez le fichier de métadonnées téléchargé à l’équipe de support technique Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="eb1ff-149">L’équipe de support technique Benefitsolver doit se charger de la configuration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="eb1ff-150">Vous recevrez une notification dès que l’authentification unique aura été activée pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="eb1ff-151">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="eb1ff-152">![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="eb1ff-153">Dans le menu situé en haut, cliquez sur **Attributs** to open the **SAML Token Attributs** .</span><span class="sxs-lookup"><span data-stu-id="eb1ff-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="eb1ff-154">![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="eb1ff-155">Pour ajouter les mappages d’attribut requis, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb1ff-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="eb1ff-156">![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="eb1ff-157">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="eb1ff-157">Attribute Name</span></span> | <span data-ttu-id="eb1ff-158">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="eb1ff-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="eb1ff-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="eb1ff-159">ClientID</span></span> |<span data-ttu-id="eb1ff-160">L’équipe de support technique Benefitsolver doit vous fournir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="eb1ff-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="eb1ff-161">ClientKey</span></span> |<span data-ttu-id="eb1ff-162">L’équipe de support technique Benefitsolver doit vous fournir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="eb1ff-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="eb1ff-163">LogoutURL</span></span> |<span data-ttu-id="eb1ff-164">L’équipe de support technique Benefitsolver doit vous fournir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="eb1ff-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="eb1ff-165">EmployeeID</span></span> |<span data-ttu-id="eb1ff-166">L’équipe de support technique Benefitsolver doit vous fournir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="eb1ff-167">Pour chaque ligne de données dans le tableau ci-dessus, cliquez sur **Ajouter un attribut utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="eb1ff-168">Dans la zone de texte **Nom de l’attribut** , tapez le nom d’attribut indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="eb1ff-169">Dans la zone de texte **Valeur de l’attribut** , sélectionnez la valeur d’attribut indiquée pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="eb1ff-170">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-170">Click **Complete**.</span></span>
9. <span data-ttu-id="eb1ff-171">Cliquez sur **Appliquer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="eb1ff-172">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="eb1ff-172">Configure user provisioning</span></span>
<span data-ttu-id="eb1ff-173">Pour permettre aux utilisateurs Azure AD de se connecter à Benefitsolver, vous devez les approvisionner dans Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="eb1ff-174">Dans le cas de Benefitsolver, les données des employés se trouvent dans votre application, remplies grâce à un fichier de recensement issu de votre système de ressources humaines (généralement de nuit).</span><span class="sxs-lookup"><span data-stu-id="eb1ff-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="eb1ff-175">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Benefitsolver pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="eb1ff-176">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="eb1ff-176">Assigning users</span></span>
<span data-ttu-id="eb1ff-177">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="eb1ff-178">Pour affecter des utilisateurs à Benefitsolver, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb1ff-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="eb1ff-179">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="eb1ff-180">Sur la ** Benefitsolver ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="eb1ff-181">![Affecter des utilisateurs](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="eb1ff-182">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="eb1ff-183">![Oui](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="eb1ff-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="eb1ff-184">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="eb1ff-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="eb1ff-185">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb1ff-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

