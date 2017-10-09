---
title: "Didacticiel : Intégration d’Azure Active Directory à Coupa | Microsoft Docs"
description: "Découvrez comment toouse Coupa avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="881d0-103">Didacticiel : Intégration d’Azure Active Directory à Coupa</span><span class="sxs-lookup"><span data-stu-id="881d0-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="881d0-104">objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Coupa.</span><span class="sxs-lookup"><span data-stu-id="881d0-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="881d0-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="881d0-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="881d0-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="881d0-106">A valid Azure subscription</span></span>
* <span data-ttu-id="881d0-107">Un abonnement Coupa pour lequel l’authentification unique (SSO) est activée</span><span class="sxs-lookup"><span data-stu-id="881d0-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="881d0-108">À l’issue de ce didacticiel, hello Azure AD utilisateurs tooCoupa sera toosingle en mesure de l’authentification sur application hello utilisant hello [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="881d0-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="881d0-109">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="881d0-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="881d0-110">Activation de l’intégration d’application hello pour Coupa</span><span class="sxs-lookup"><span data-stu-id="881d0-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="881d0-111">Configuration de l'authentification unique</span><span class="sxs-lookup"><span data-stu-id="881d0-111">Configuring single sign-on</span></span>
* <span data-ttu-id="881d0-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="881d0-112">Configuring user provisioning</span></span>
* <span data-ttu-id="881d0-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="881d0-113">Assigning users</span></span>

<span data-ttu-id="881d0-114">![Scénario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="881d0-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="881d0-115">Activer l’intégration d’application hello pour Coupa</span><span class="sxs-lookup"><span data-stu-id="881d0-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="881d0-116">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Coupa.</span><span class="sxs-lookup"><span data-stu-id="881d0-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="881d0-117">**intégration d’application hello tooenable pour Coupa, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="881d0-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="881d0-118">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="881d0-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="881d0-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="881d0-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="881d0-120">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="881d0-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="881d0-121">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="881d0-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="881d0-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="881d0-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="881d0-123">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="881d0-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="881d0-124">![Ajouter une application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="881d0-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="881d0-125">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="881d0-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="881d0-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-coupa-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="881d0-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="881d0-127">Bonjour **zone de recherche**, type **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="881d0-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="881d0-128">![Galerie d’applications](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="881d0-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="881d0-129">Dans le volet de résultats hello, sélectionnez **Coupa**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="881d0-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="881d0-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="881d0-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="881d0-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="881d0-131">Configure single sign-on</span></span>

<span data-ttu-id="881d0-132">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooCoupa avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="881d0-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="881d0-133">Configuration de l’authentification unique pour Coupa nécessite que vous tooretrieve une valeur d’empreinte numérique à partir d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="881d0-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="881d0-134">Si vous n’êtes pas familiarisé avec cette procédure, consultez [comment tooretrieve valeur d’empreinte numérique d’un certificat](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="881d0-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="881d0-135">**tooconfigure sur l’authentification unique, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="881d0-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="881d0-136">Se connecter tooyour site d’entreprise Coupa en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="881d0-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="881d0-137">Accédez trop**le programme d’installation \> pour contrôler la sécurité**.</span><span class="sxs-lookup"><span data-stu-id="881d0-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="881d0-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="881d0-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="881d0-139">toodownload hello Coupa métadonnées fichier tooyour ordinateur, cliquez sur **télécharger et importer des métadonnées de Service Pack**.</span><span class="sxs-lookup"><span data-stu-id="881d0-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="881d0-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span><span class="sxs-lookup"><span data-stu-id="881d0-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="881d0-141">Dans une autre fenêtre de navigateur, connectez-vous toohello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="881d0-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="881d0-142">Sur hello **Coupa** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="881d0-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="881d0-143">![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="881d0-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="881d0-144">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooCoupa** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="881d0-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="881d0-145">![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="881d0-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="881d0-146">Sur hello **Configure App URL** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="881d0-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="881d0-147">![Configurer l’URL de l’application](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="881d0-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="881d0-148">Bonjour **URL de connexion** zone de texte, tapez l’URL utilisée par votre toosign utilisateurs sur tooyour application Coupa (par exemple : «*http://company.Coupa.com*»).</span><span class="sxs-lookup"><span data-stu-id="881d0-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="881d0-149">Ouvrez votre fichier de métadonnées Coupa téléchargé et copiez hello **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="881d0-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="881d0-150">Bonjour **URL de réponse Coupa** zone de texte, collez hello **AssertionConsumerService index/URL** valeur.</span><span class="sxs-lookup"><span data-stu-id="881d0-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="881d0-151">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="881d0-151">Click **Next**.</span></span>
8. <span data-ttu-id="881d0-152">Sur hello **configurer l’authentification unique sur Coupa** page, toodownload votre fichier de métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="881d0-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="881d0-153">![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="881d0-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="881d0-154">Sur le site d’entreprise Coupa hello, accédez trop**le programme d’installation \> pour contrôler la sécurité**.</span><span class="sxs-lookup"><span data-stu-id="881d0-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="881d0-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="881d0-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="881d0-156">Bonjour **se connecter à l’aide des informations d’identification Coupa** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="881d0-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="881d0-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span><span class="sxs-lookup"><span data-stu-id="881d0-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="881d0-158">Sélectionnez **Log in using SAML**.</span><span class="sxs-lookup"><span data-stu-id="881d0-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="881d0-159">Cliquez sur **Parcourir** tooupload votre fichier de métadonnées téléchargé Azure Active.</span><span class="sxs-lookup"><span data-stu-id="881d0-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="881d0-160">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="881d0-160">Click **Save**.</span></span>
11. <span data-ttu-id="881d0-161">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="881d0-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="881d0-162">![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="881d0-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="881d0-163">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="881d0-163">Configure user provisioning</span></span>

<span data-ttu-id="881d0-164">Dans l’ordre tooenable Azure AD les utilisateurs toolog à Coupa, vous devez les configurer dans Coupa.</span><span class="sxs-lookup"><span data-stu-id="881d0-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="881d0-165">Dans les cas de hello de Coupa, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="881d0-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="881d0-166">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="881d0-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="881d0-167">Connectez-vous à tooyour **Coupa** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="881d0-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="881d0-168">Dans le menu hello haut de hello, cliquez sur **le programme d’installation**, puis cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="881d0-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="881d0-169">![Utilisateurs](./media/active-directory-saas-coupa-tutorial/IC791908.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="881d0-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="881d0-170">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="881d0-170">Click **Create**.</span></span>
   
   <span data-ttu-id="881d0-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span><span class="sxs-lookup"><span data-stu-id="881d0-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="881d0-172">Bonjour **utilisateur créer** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="881d0-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="881d0-173">![Détails de l’utilisateur](./media/active-directory-saas-coupa-tutorial/IC791910.png "Détails de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="881d0-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="881d0-174">Hello de type **connexion**, **prénom**, **nom**, **ID de connexion unique**, **messagerie** attributs d’un compte Azure Active Directory valide, que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="881d0-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="881d0-175">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="881d0-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="881d0-176">détenteur du compte de Hello Azure Active Directory reçoit un e-mail avec un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="881d0-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="881d0-177">Vous pouvez utiliser n’importe quel autre Coupa utilisateur compte outil de création ou API fournie par Coupa tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="881d0-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="881d0-178">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="881d0-178">Assign users</span></span>
<span data-ttu-id="881d0-179">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="881d0-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="881d0-180">**tooassign utilisateurs tooCoupa, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="881d0-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="881d0-181">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="881d0-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="881d0-182">Sur hello ** Coupa ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="881d0-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="881d0-183">![Affecter des utilisateurs](./media/active-directory-saas-coupa-tutorial/IC791911.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="881d0-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="881d0-184">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="881d0-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="881d0-185">![Oui](./media/active-directory-saas-coupa-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="881d0-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="881d0-186">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="881d0-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="881d0-187">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="881d0-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

