---
title: "Didacticiel : Intégration d’Azure Active Directory à Coupa | Microsoft Docs"
description: "Apprenez à utiliser Coupa avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore."
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
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="6746b-103">Didacticiel : Intégration d’Azure Active Directory à Coupa</span><span class="sxs-lookup"><span data-stu-id="6746b-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="6746b-104">L’objectif de ce didacticiel est de montrer comment intégrer Azure et Coupa.</span><span class="sxs-lookup"><span data-stu-id="6746b-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="6746b-105">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6746b-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="6746b-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="6746b-106">A valid Azure subscription</span></span>
* <span data-ttu-id="6746b-107">Un abonnement Coupa pour lequel l’authentification unique (SSO) est activée</span><span class="sxs-lookup"><span data-stu-id="6746b-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="6746b-108">À l’issue de ce didacticiel, les utilisateurs d’Azure AD que vous avez affectés à Coupa pourront s’authentifier de manière unique dans l’application à l’aide de la [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6746b-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="6746b-109">Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="6746b-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="6746b-110">Activation de l’intégration d’applications pour Coupa</span><span class="sxs-lookup"><span data-stu-id="6746b-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="6746b-111">Configuration de l'authentification unique</span><span class="sxs-lookup"><span data-stu-id="6746b-111">Configuring single sign-on</span></span>
* <span data-ttu-id="6746b-112">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6746b-112">Configuring user provisioning</span></span>
* <span data-ttu-id="6746b-113">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6746b-113">Assigning users</span></span>

<span data-ttu-id="6746b-114">![Scénario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="6746b-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="6746b-115">Activer l’intégration d’applications pour Coupa</span><span class="sxs-lookup"><span data-stu-id="6746b-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="6746b-116">Cette section décrit l’activation de l’intégration d’applications pour Coupa.</span><span class="sxs-lookup"><span data-stu-id="6746b-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="6746b-117">**Pour activer l’intégration d’applications pour Coupa, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="6746b-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="6746b-118">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6746b-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="6746b-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="6746b-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="6746b-120">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="6746b-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6746b-121">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="6746b-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="6746b-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="6746b-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="6746b-123">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="6746b-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="6746b-124">![Ajouter une application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="6746b-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="6746b-125">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="6746b-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="6746b-126">![Ajouter une application à partir de la galerie](./media/active-directory-saas-coupa-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="6746b-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="6746b-127">Dans la **zone de recherche**, tapez **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="6746b-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="6746b-128">![Galerie d’applications](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="6746b-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="6746b-129">Dans le volet des résultats, sélectionnez **Coupa**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="6746b-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="6746b-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="6746b-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="6746b-131">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6746b-131">Configure single sign-on</span></span>

<span data-ttu-id="6746b-132">Cette section explique comment permettre aux utilisateurs de s’authentifier sur Coupa avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="6746b-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="6746b-133">La configuration de l’authentification unique pour Coupa vous oblige à récupérer une valeur d’empreinte numérique dans un certificat.</span><span class="sxs-lookup"><span data-stu-id="6746b-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="6746b-134">Si cette procédure ne vous est pas familière, consultez [Comment récupérer la valeur d’empreinte numérique d’un certificat](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="6746b-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="6746b-135">**Pour configurer l’authentification unique, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6746b-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="6746b-136">Connectez-vous à votre site d’entreprise Coupa en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6746b-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="6746b-137">Accédez à **Setup \> Security controls**.</span><span class="sxs-lookup"><span data-stu-id="6746b-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="6746b-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="6746b-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="6746b-139">Pour télécharger le fichier de métadonnées Coupa sur votre ordinateur, cliquez sur **Download and import SP metadata**.</span><span class="sxs-lookup"><span data-stu-id="6746b-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="6746b-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span><span class="sxs-lookup"><span data-stu-id="6746b-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="6746b-141">Dans une autre fenêtre du navigateur, connectez-vous au portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="6746b-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="6746b-142">Sur la page d’intégration d’applications **Coupa**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6746b-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="6746b-143">![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6746b-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="6746b-144">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Coupa**, sélectionnez **Authentification unique avec Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6746b-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="6746b-145">![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6746b-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="6746b-146">Dans la page **Configurer l’URL de l’application** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6746b-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="6746b-147">![Configurer l’URL de l’application](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="6746b-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="6746b-148">Dans la zone de texte **URL de connexion**, tapez l’URL utilisée par vos utilisateurs pour se connecter à votre application Coupa (par exemple, « *http://company.Coupa.com* »).</span><span class="sxs-lookup"><span data-stu-id="6746b-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="6746b-149">Ouvrez votre fichier de métadonnées Coupa téléchargé, puis copiez la valeur **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="6746b-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="6746b-150">Dans la zone de texte **URL de réponse Coupa**, collez la valeur **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="6746b-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="6746b-151">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6746b-151">Click **Next**.</span></span>
8. <span data-ttu-id="6746b-152">Dans la page **Configurer l’authentification unique sur Coupa**, pour télécharger votre fichier de métadonnées, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier en local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6746b-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="6746b-153">![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6746b-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="6746b-154">Sur le site d’entreprise Coupa, accédez à **Setup \> Security controls**.</span><span class="sxs-lookup"><span data-stu-id="6746b-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="6746b-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span><span class="sxs-lookup"><span data-stu-id="6746b-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="6746b-156">Dans la section **Log in using Coupa credentials** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6746b-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="6746b-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span><span class="sxs-lookup"><span data-stu-id="6746b-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="6746b-158">Sélectionnez **Log in using SAML**.</span><span class="sxs-lookup"><span data-stu-id="6746b-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="6746b-159">Cliquez sur **Browse** pour charger le fichier de métadonnées Azure Active Directory téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6746b-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="6746b-160">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="6746b-160">Click **Save**.</span></span>
11. <span data-ttu-id="6746b-161">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6746b-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="6746b-162">![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6746b-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="6746b-163">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="6746b-163">Configure user provisioning</span></span>

<span data-ttu-id="6746b-164">Pour se connecter à Coupa, les utilisateurs d’Azure AD doivent être approvisionnés dans Coupa.</span><span class="sxs-lookup"><span data-stu-id="6746b-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="6746b-165">Dans le cas de Coupa, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="6746b-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="6746b-166">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6746b-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6746b-167">Connectez-vous à votre site d’entreprise **Coupa** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6746b-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="6746b-168">Dans le menu situé en haut, cliquez sur **Setup**, puis sur **Users**.</span><span class="sxs-lookup"><span data-stu-id="6746b-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="6746b-169">![Utilisateurs](./media/active-directory-saas-coupa-tutorial/IC791908.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="6746b-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="6746b-170">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6746b-170">Click **Create**.</span></span>
   
   <span data-ttu-id="6746b-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span><span class="sxs-lookup"><span data-stu-id="6746b-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="6746b-172">Dans la section **User Create** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6746b-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="6746b-173">![Détails de l’utilisateur](./media/active-directory-saas-coupa-tutorial/IC791910.png "Détails de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="6746b-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="6746b-174">Tapez l’ID de connexion, le prénom, le nom, l’ID d’authentification unique et l’adresse électronique d’un compte Azure Active Directory valide que vous souhaitez approvisionner dans les zones de texte **Login**, **First name**, **Last Name**, **Single Sign-On ID** et **Email**.</span><span class="sxs-lookup"><span data-stu-id="6746b-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="6746b-175">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6746b-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="6746b-176">Le titulaire du compte Azure Active Directory reçoit un message électronique contenant un lien pour confirmer le compte et l’activer.</span><span class="sxs-lookup"><span data-stu-id="6746b-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="6746b-177">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur fourni par Coupa pour approvisionner des comptes d’utilisateurs AAD.</span><span class="sxs-lookup"><span data-stu-id="6746b-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="6746b-178">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6746b-178">Assign users</span></span>
<span data-ttu-id="6746b-179">Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="6746b-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="6746b-180">**Pour affecter des utilisateurs à Coupa, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="6746b-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="6746b-181">Dans le portail Azure Classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="6746b-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="6746b-182">Sur la ** Coupa ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6746b-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="6746b-183">![Affecter des utilisateurs](./media/active-directory-saas-coupa-tutorial/IC791911.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="6746b-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="6746b-184">Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.</span><span class="sxs-lookup"><span data-stu-id="6746b-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="6746b-185">![Oui](./media/active-directory-saas-coupa-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="6746b-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="6746b-186">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="6746b-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="6746b-187">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6746b-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

