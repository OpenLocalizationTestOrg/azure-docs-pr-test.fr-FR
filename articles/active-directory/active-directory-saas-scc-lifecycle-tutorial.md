---
title: "Didacticiel : Intégration d’Azure Active Directory à SCC LifeCycle | Microsoft Docs"
description: "Découvrez comment utiliser SCC LifeCycle avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="95b8c-103">Didacticiel : Intégration d’Azure AD à SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="95b8c-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="95b8c-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="95b8c-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="95b8c-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="95b8c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="95b8c-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="95b8c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="95b8c-107">Un abonnement SCC LifeCycle pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="95b8c-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="95b8c-108">À l’issue de ce didacticiel, les utilisateurs d’Azure AD que vous avez affectés à SCC LifeCycle pourront s’authentifier de manière unique dans l’application sur votre site d’entreprise SCC LifeCycle (connexion initiée par le fournisseur du service) ou en s’aidant de la [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="95b8c-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="95b8c-109">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="95b8c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="95b8c-110">Activation de l’intégration d’applications pour SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="95b8c-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="95b8c-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="95b8c-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="95b8c-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="95b8c-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="95b8c-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="95b8c-113">Assigning users</span></span>

<span data-ttu-id="95b8c-114">![Scénario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="95b8c-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="95b8c-115">Activer l’intégration d’applications pour SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="95b8c-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="95b8c-116">Cette section décrit comment activer l’intégration d’applications pour SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="95b8c-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="95b8c-117">**Pour activer l’intégration d’applications pour SCC LifeCycle, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="95b8c-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="95b8c-118">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95b8c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="95b8c-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="95b8c-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="95b8c-120">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="95b8c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="95b8c-121">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="95b8c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="95b8c-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="95b8c-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="95b8c-123">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="95b8c-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="95b8c-124">![Ajouter une application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="95b8c-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="95b8c-125">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="95b8c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="95b8c-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="95b8c-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="95b8c-127">Dans la **zone de recherche**, entrez **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="95b8c-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="95b8c-128">![Galerie d’applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="95b8c-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="95b8c-129">Dans le volet des résultats, sélectionnez **SCC LifeCycle**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="95b8c-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="95b8c-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="95b8c-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="95b8c-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="95b8c-131">Configure single sign-on</span></span>

<span data-ttu-id="95b8c-132">Cette section explique comment permettre aux utilisateurs de s’authentifier sur SCC LifeCycle avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="95b8c-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="95b8c-133">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="95b8c-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="95b8c-134">Dans la page d’intégration d’application **SCC LifeCycle** du portail Azure Classic, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="95b8c-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="95b8c-135">![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="95b8c-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="95b8c-136">Dans la page **Comment voulez-vous que les utilisateurs se connectent à SCC LifeCycle**, sélectionnez **Authentification unique avec Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95b8c-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="95b8c-137">![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="95b8c-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="95b8c-138">Dans la zone de texte **URL de connexion** de la page **Configurer l’URL de l’application**, tapez l’URL utilisée par vos utilisateurs pour se connecter à votre application SCC LifeCycle à l’aide du modèle suivant « *https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx* », puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="95b8c-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="95b8c-139">![Configurer l’URL de l’application](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="95b8c-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="95b8c-140">Dans la page **Configurer l’authentification unique sur SCC LifeCycle**, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier de métadonnées en local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="95b8c-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="95b8c-141">![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="95b8c-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="95b8c-142">Transférez ce fichier de métadonnées à l’équipe de support de SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="95b8c-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="95b8c-143">L’authentification unique doit être activée par l’équipe de support de SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="95b8c-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="95b8c-144">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="95b8c-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="95b8c-145">![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="95b8c-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="95b8c-146">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="95b8c-146">Configure user provisioning</span></span>

<span data-ttu-id="95b8c-147">Pour se connecter à SCC LifeCycle, les utilisateurs d’Azure AD doivent être approvisionnés dans SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="95b8c-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="95b8c-148">Vous n’avez rien à faire pour configurer l’approvisionnement des utilisateurs dans SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="95b8c-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="95b8c-149">Lorsqu’un utilisateur tente de se connecter à SCC LifeCycle, un compte SCC LifeCycle est, au besoin, automatiquement créé.</span><span class="sxs-lookup"><span data-stu-id="95b8c-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="95b8c-150">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur, fourni par SCC LifeCycle, pour approvisionner des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="95b8c-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="95b8c-151">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="95b8c-151">Assign users</span></span>
<span data-ttu-id="95b8c-152">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="95b8c-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="95b8c-153">**Pour affecter des utilisateurs à SCC LifeCycle, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="95b8c-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="95b8c-154">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="95b8c-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="95b8c-155">Dans la page d’intégration d’applications **SCC LifeCycle**, cliquez sur **Affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="95b8c-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="95b8c-156">![Affecter des utilisateurs](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="95b8c-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="95b8c-157">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="95b8c-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="95b8c-158">![Oui](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="95b8c-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="95b8c-159">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="95b8c-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="95b8c-160">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="95b8c-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

