---
title: "Didacticiel : Intégration d’Azure Active Directory à Qualtrics | Microsoft Docs"
description: "Découvrez comment toouse Qualtrics avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
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
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="4f8a6-103">Didacticiel : Intégration d’Azure Active Directory avec Qualtrics</span><span class="sxs-lookup"><span data-stu-id="4f8a6-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="4f8a6-104">objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure à Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="4f8a6-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4f8a6-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="4f8a6-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="4f8a6-106">A valid Azure subscription</span></span>
* <span data-ttu-id="4f8a6-107">Un abonnement Qualtrics pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4f8a6-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="4f8a6-108">À l’issue de ce didacticiel, hello Azure AD utilisateurs tooQualtrics sera toosingle en mesure de l’authentification sur application hello à votre site d’entreprise Qualtrics (service initiée par le fournisseur de session) ou à l’aide de hello [Introduction toohello Accéder au panneau de configuration](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f8a6-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="4f8a6-109">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4f8a6-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="4f8a6-110">Activation de l’intégration d’application hello pour Qualtrics</span><span class="sxs-lookup"><span data-stu-id="4f8a6-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="4f8a6-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="4f8a6-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="4f8a6-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="4f8a6-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="4f8a6-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="4f8a6-113">Assigning users</span></span>

<span data-ttu-id="4f8a6-114">![Scénario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="4f8a6-115">Activation de l’intégration d’application hello pour Qualtrics</span><span class="sxs-lookup"><span data-stu-id="4f8a6-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="4f8a6-116">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="4f8a6-117">**intégration d’application hello tooenable pour Qualtrics, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f8a6-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f8a6-118">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="4f8a6-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="4f8a6-120">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="4f8a6-121">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="4f8a6-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="4f8a6-123">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="4f8a6-124">![Ajouter une application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="4f8a6-125">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="4f8a6-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="4f8a6-127">Bonjour **zone de recherche**, type **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="4f8a6-128">![Galerie d’applications](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="4f8a6-129">Dans le volet de résultats hello, sélectionnez **Qualtrics**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="4f8a6-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="4f8a6-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4f8a6-131">Configure single sign-on</span></span>

<span data-ttu-id="4f8a6-132">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooQualtrics avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="4f8a6-133">**tooconfigure sur l’authentification unique, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f8a6-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f8a6-134">Bonjour portail Azure classic sur hello **Qualtrics** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4f8a6-135">![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="4f8a6-136">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooQualtrics** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="4f8a6-137">![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="4f8a6-138">Sur hello **Configure App URL** page hello **Qualtrics URL de connexion** zone de texte, tapez votre URL (par exemple : «*https://ssotest2ut1.qualtrics.com*»), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="4f8a6-139">![Configurer l’URL de l’application](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="4f8a6-140">Sur hello **configurer l’authentification unique sur Qualtrics** , cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="4f8a6-141">![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="4f8a6-142">Envoyer toohello de fichier de métadonnées hello équipe de support Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="4f8a6-143">configuration de SSO Hello a toobe effectuée par l’équipe de support Qualtrics de hello.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="4f8a6-144">Vous recevez une notification dès que hello configuration a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="4f8a6-145">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="4f8a6-146">![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="4f8a6-147">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="4f8a6-147">Configure user provisioning</span></span>

<span data-ttu-id="4f8a6-148">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooQualtrics.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="4f8a6-149">Quand un utilisateur affecté tente de toolog à Qualtrics à l’aide du volet d’accès hello, Qualtrics vérifie l’existence d’un utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="4f8a6-150">Si aucun compte d'utilisateur n’est disponible, Qualtrics le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="4f8a6-151">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="4f8a6-151">Assign users</span></span>
<span data-ttu-id="4f8a6-152">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="4f8a6-153">**tooassign utilisateurs tooQualtrics, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4f8a6-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="4f8a6-154">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4f8a6-155">Sur hello **Qualtrics** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="4f8a6-156">![Affecter des utilisateurs](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="4f8a6-157">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="4f8a6-158">![Oui](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="4f8a6-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4f8a6-159">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4f8a6-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="4f8a6-160">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f8a6-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

