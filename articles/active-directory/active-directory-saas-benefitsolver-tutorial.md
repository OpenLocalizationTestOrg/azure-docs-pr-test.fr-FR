---
title: "Didacticiel : Intégration d’Azure Active Directory à Benefitsolver | Microsoft Docs"
description: "Découvrez comment toouse Benefitsolver avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
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
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="8ce7f-103">Didacticiel : Intégration d’Azure Active Directory à Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="8ce7f-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="8ce7f-104">objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="8ce7f-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8ce7f-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="8ce7f-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="8ce7f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8ce7f-107">Un abonnement Benefitsolver pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8ce7f-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="8ce7f-108">À l’issue de ce didacticiel, hello Azure AD utilisateurs tooBenefitsolver sera toosingle en mesure de l’authentification sur application hello utilisant hello [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ce7f-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="8ce7f-109">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8ce7f-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="8ce7f-110">Activation de l’intégration d’application hello pour Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="8ce7f-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="8ce7f-111">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="8ce7f-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="8ce7f-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8ce7f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="8ce7f-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8ce7f-113">Assigning users</span></span>

<span data-ttu-id="8ce7f-114">![Scénario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="8ce7f-115">Activation de l’intégration d’application hello pour Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="8ce7f-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="8ce7f-116">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="8ce7f-117">intégration d’application hello tooenable pour Benefitsolver, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ce7f-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="8ce7f-118">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="8ce7f-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8ce7f-120">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="8ce7f-121">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="8ce7f-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="8ce7f-123">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="8ce7f-124">![Ajouter une application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="8ce7f-125">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="8ce7f-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8ce7f-127">Bonjour **zone de recherche**, type **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="8ce7f-128">![Galerie d’applications](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="8ce7f-129">Dans le volet de résultats hello, sélectionnez **Benefitsolver**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="8ce7f-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="8ce7f-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8ce7f-131">Configure single sign-on</span></span>

<span data-ttu-id="8ce7f-132">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooBenefitsolver avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="8ce7f-133">Votre application Benefitsolver attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton saml** configuration.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="8ce7f-134">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="8ce7f-135">![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="8ce7f-136">**tooconfigure sur l’authentification unique, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8ce7f-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ce7f-137">Bonjour portail Azure classic sur hello **Benefitsolver** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="8ce7f-138">![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="8ce7f-139">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooBenefitsolver** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="8ce7f-140">![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="8ce7f-141">Sur hello **configurer les paramètres de l’application** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ce7f-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="8ce7f-142">![Configurer les paramètres d’application](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurer les paramètres d’application")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="8ce7f-143">Bonjour **URL de connexion** zone de texte, type **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="8ce7f-144">Bonjour **URL de réponse** zone de texte, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="8ce7f-145">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-145">Click **Next**.</span></span>
4. <span data-ttu-id="8ce7f-146">Sur hello **configurer l’authentification unique sur Benefitsolver** page, toodownload vos métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier de métadonnées hello localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="8ce7f-147">![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="8ce7f-148">Envoyer l’équipe de support technique du fichier tooyour Benefitsolver hello téléchargé métadonnées.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="8ce7f-149">Votre équipe de support Benefitsolver a configuration de SSO réelle toodo hello.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="8ce7f-150">Vous recevrez une notification dès que l’authentification unique aura été activée pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="8ce7f-151">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="8ce7f-152">![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="8ce7f-153">Dans le menu hello haut de hello, cliquez sur **attributs** tooopen hello **attributs du jeton SAML** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="8ce7f-154">![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="8ce7f-155">mappages d’attributs tooadd hello requis, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ce7f-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="8ce7f-156">![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributs")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="8ce7f-157">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="8ce7f-157">Attribute Name</span></span> | <span data-ttu-id="8ce7f-158">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="8ce7f-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="8ce7f-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="8ce7f-159">ClientID</span></span> |<span data-ttu-id="8ce7f-160">Vous devez tooget de cette valeur à partir de votre équipe de support Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="8ce7f-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="8ce7f-161">ClientKey</span></span> |<span data-ttu-id="8ce7f-162">Vous devez tooget de cette valeur à partir de votre équipe de support Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="8ce7f-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="8ce7f-163">LogoutURL</span></span> |<span data-ttu-id="8ce7f-164">Vous devez tooget de cette valeur à partir de votre équipe de support Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="8ce7f-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="8ce7f-165">EmployeeID</span></span> |<span data-ttu-id="8ce7f-166">Vous devez tooget de cette valeur à partir de votre équipe de support Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="8ce7f-167">Pour chaque ligne de données dans la table hello ci-dessus, cliquez sur **ajouter un attribut utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="8ce7f-168">Bonjour **nom de l’attribut** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="8ce7f-169">Bonjour **valeur d’attribut** zone de texte, valeur de l’attribut select hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="8ce7f-170">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-170">Click **Complete**.</span></span>
9. <span data-ttu-id="8ce7f-171">Cliquez sur **Appliquer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="8ce7f-172">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="8ce7f-172">Configure user provisioning</span></span>
<span data-ttu-id="8ce7f-173">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans Benefitsolver, ils doivent être configurés dans Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="8ce7f-174">Dans les cas de hello de Benefitsolver, les données sur les employés sont dans votre application remplie via un fichier de recensement, à partir de votre système de ressources humaines (généralement nuit).</span><span class="sxs-lookup"><span data-stu-id="8ce7f-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="8ce7f-175">Vous pouvez utiliser n’importe quel autre Benefitsolver utilisateur compte outil de création ou API fournie par Benefitsolver tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="8ce7f-176">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8ce7f-176">Assigning users</span></span>
<span data-ttu-id="8ce7f-177">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="8ce7f-178">tooassign utilisateurs tooBenefitsolver, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ce7f-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="8ce7f-179">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="8ce7f-180">Sur hello ** Benefitsolver ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="8ce7f-181">![Affecter des utilisateurs](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="8ce7f-182">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="8ce7f-183">![Oui](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="8ce7f-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="8ce7f-184">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8ce7f-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="8ce7f-185">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ce7f-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

