---
title: "Didacticiel : Intégration d’Azure Active Directory avec SCC LifeCycle | Microsoft Docs"
description: "Découvrez comment toouse SCC LifeCycle avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
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
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="676a1-103">Didacticiel : Intégration d’Azure AD avec SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="676a1-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="676a1-104">objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="676a1-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="676a1-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="676a1-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="676a1-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="676a1-106">A valid Azure subscription</span></span>
* <span data-ttu-id="676a1-107">Un abonnement SCC LifeCycle pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="676a1-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="676a1-108">À l’issue de ce didacticiel, hello Azure AD utilisateurs tooSCC cycle de vie sera toosingle en mesure de connexion dans l’application hello sur votre site d’entreprise SCC LifeCycle (service initiée par le fournisseur de session), ou à l’aide de hello [Introduction Volet d’accès de toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="676a1-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="676a1-109">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="676a1-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="676a1-110">Activation de l’intégration d’application hello pour SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="676a1-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="676a1-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="676a1-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="676a1-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="676a1-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="676a1-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="676a1-113">Assigning users</span></span>

<span data-ttu-id="676a1-114">![Scénario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="676a1-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="676a1-115">Activer l’intégration d’application hello pour SCC LifeCycle</span><span class="sxs-lookup"><span data-stu-id="676a1-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="676a1-116">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="676a1-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="676a1-117">**intégration d’application hello tooenable pour SCC LifeCycle, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="676a1-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="676a1-118">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="676a1-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="676a1-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="676a1-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="676a1-120">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="676a1-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="676a1-121">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="676a1-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="676a1-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="676a1-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="676a1-123">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="676a1-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="676a1-124">![Ajouter une application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="676a1-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="676a1-125">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="676a1-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="676a1-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="676a1-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="676a1-127">Bonjour **zone de recherche**, type **SCC LifeCycle**.</span><span class="sxs-lookup"><span data-stu-id="676a1-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="676a1-128">![Galerie d’applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="676a1-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="676a1-129">Dans le volet de résultats hello, sélectionnez **SCC LifeCycle**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="676a1-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="676a1-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="676a1-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="676a1-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="676a1-131">Configure single sign-on</span></span>

<span data-ttu-id="676a1-132">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooSCC du cycle de vie avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="676a1-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="676a1-133">**tooconfigure sur l’authentification unique, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="676a1-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="676a1-134">Bonjour portail Azure classic sur hello **SCC LifeCycle** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello ** configurer Single Sign On ** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="676a1-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="676a1-135">![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="676a1-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="676a1-136">Sur hello **Comment souhaitez-vous toosign les utilisateurs sur le cycle de vie de tooSCC** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="676a1-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="676a1-137">![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="676a1-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="676a1-138">Sur hello **Configure App URL** page hello **URL de connexion** zone de texte, tapez l’URL hello utilisé par votre toosign utilisateurs sur tooyour application SCC LifeCycle à l’aide de hello suivant le modèle «*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*», puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="676a1-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="676a1-139">![Configurer l’URL de l’application](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="676a1-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="676a1-140">Sur hello **configurer l’authentification unique sur SCC LifeCycle** , cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier de métadonnées localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="676a1-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="676a1-141">![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="676a1-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="676a1-142">Transférer ce tooSCC de fichier de métadonnées équipe de Support du cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="676a1-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="676a1-143">L’authentification unique a toobe activé par l’équipe de support technique SCC LifeCycle de hello.</span><span class="sxs-lookup"><span data-stu-id="676a1-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="676a1-144">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="676a1-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="676a1-145">![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="676a1-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="676a1-146">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="676a1-146">Configure user provisioning</span></span>

<span data-ttu-id="676a1-147">Dans l’ordre tooenable Azure AD les utilisateurs toolog à SCC LifeCycle, ils doivent être configurés à SCC LifeCycle.</span><span class="sxs-lookup"><span data-stu-id="676a1-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="676a1-148">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooSCC du cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="676a1-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="676a1-149">Lorsqu’un toolog tentatives utilisateur affecté à SCC LifeCycle, un compte SCC LifeCycle est créé automatiquement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="676a1-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="676a1-150">Vous pouvez utiliser n’importe quel autre SCC LifeCycle utilisateur compte outil de création ou API fournie par SCC LifeCycle tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="676a1-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="676a1-151">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="676a1-151">Assign users</span></span>
<span data-ttu-id="676a1-152">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="676a1-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="676a1-153">**les utilisateurs de tooassign tooSCC du cycle de vie, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="676a1-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="676a1-154">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="676a1-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="676a1-155">Sur hello ** SCC LifeCycle ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="676a1-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="676a1-156">![Affecter des utilisateurs](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="676a1-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="676a1-157">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="676a1-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="676a1-158">![Oui](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="676a1-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="676a1-159">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="676a1-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="676a1-160">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="676a1-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

