---
title: "Didacticiel : Intégration d’Azure Active Directory à Qualtrics | Microsoft Docs"
description: "Apprenez à utiliser Qualtrics avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="de21c-103">Didacticiel : Intégration d’Azure Active Directory avec Qualtrics</span><span class="sxs-lookup"><span data-stu-id="de21c-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="de21c-104">L'objectif de ce didacticiel est de montrer comment intégrer Azure et Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="de21c-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="de21c-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="de21c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="de21c-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="de21c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="de21c-107">Un abonnement Qualtrics pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="de21c-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="de21c-108">À l’issue de ce didacticiel, les utilisateurs Azure AD que vous avez affectés à Qualtrics pourront s’authentifier de manière unique dans l’application sur votre site d’entreprise Qualtrics (connexion initiée par le fournisseur du service) ou en s’aidant de la [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="de21c-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="de21c-109">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="de21c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="de21c-110">Activation de l'intégration d'applications pour Qualtrics</span><span class="sxs-lookup"><span data-stu-id="de21c-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="de21c-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="de21c-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="de21c-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="de21c-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="de21c-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="de21c-113">Assigning users</span></span>

<span data-ttu-id="de21c-114">![Scénario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="de21c-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="de21c-115">Activation de l'intégration d'applications pour Qualtrics</span><span class="sxs-lookup"><span data-stu-id="de21c-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="de21c-116">Cette section décrit l'activation de l'intégration de l'application pour Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="de21c-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="de21c-117">**Pour activer l’intégration d’applications pour Qualtrics, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de21c-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="de21c-118">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de21c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="de21c-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="de21c-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="de21c-120">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="de21c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="de21c-121">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="de21c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="de21c-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="de21c-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="de21c-123">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="de21c-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="de21c-124">![Ajouter une application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="de21c-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="de21c-125">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="de21c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="de21c-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="de21c-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="de21c-127">Dans la **zone de recherche**, entrez **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="de21c-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="de21c-128">![Galerie d’applications](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="de21c-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="de21c-129">Dans le volet de résultats, sélectionnez **Qualtrics**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="de21c-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="de21c-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="de21c-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="de21c-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="de21c-131">Configure single sign-on</span></span>

<span data-ttu-id="de21c-132">Cette section explique comment permettre aux utilisateurs de s'authentifier sur Qualtrics avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="de21c-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="de21c-133">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de21c-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="de21c-134">Dans le portail Azure Classic, dans la page d’intégration d’applications **Qualtrics**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="de21c-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="de21c-135">![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="de21c-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="de21c-136">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Qualtrics**, sélectionnez **Authentification unique avec Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="de21c-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="de21c-137">![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="de21c-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="de21c-138">Dans la page **Configurer l’URL de l’application**, dans la zone de texte **URL de connexion de Qualtrics**, tapez votre URL (par exemple : *https://ssotest2ut1.qualtrics.com*), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="de21c-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="de21c-139">![Configurer l’URL de l’application](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="de21c-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="de21c-140">Dans la page **Configurer l’authentification unique sur Qualtrics**, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="de21c-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="de21c-141">![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="de21c-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="de21c-142">Envoyez le fichier de métadonnées à l’équipe du support technique Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="de21c-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="de21c-143">La configuration de l’authentification unique doit être effectuée par l’équipe du support technique Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="de21c-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="de21c-144">Vous recevez une notification dès qu’elle est terminée.</span><span class="sxs-lookup"><span data-stu-id="de21c-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="de21c-145">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="de21c-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="de21c-146">![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="de21c-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="de21c-147">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="de21c-147">Configure user provisioning</span></span>

<span data-ttu-id="de21c-148">Aucun élément d'action ne vous permet de configurer l’approvisionnement des utilisateurs dans Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="de21c-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="de21c-149">Lorsqu'un utilisateur tente de se connecter à Qualtrics à l'aide du panneau d'accès, Qualtrics vérifie si cet utilisateur existe.</span><span class="sxs-lookup"><span data-stu-id="de21c-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="de21c-150">Si aucun compte d'utilisateur n’est disponible, Qualtrics le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="de21c-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="de21c-151">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="de21c-151">Assign users</span></span>
<span data-ttu-id="de21c-152">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="de21c-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="de21c-153">**Pour affecter des utilisateurs à Qualtrics, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="de21c-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="de21c-154">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="de21c-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="de21c-155">Dans la page d’intégration d’applications **Qualtrics**, cliquez sur **Affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="de21c-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="de21c-156">![Affecter des utilisateurs](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="de21c-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="de21c-157">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="de21c-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="de21c-158">![Oui](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="de21c-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="de21c-159">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="de21c-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="de21c-160">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="de21c-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

