---
title: "Problèmes de connexion à une application non issue de la galerie configurée pour l’authentification unique fédérée | Microsoft Docs"
description: "Instructions pour résoudre les problèmes rencontrés lors de la connexion à une application configurée pour l’authentification unique SAML fédérée avec Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 3afc7bca878caef424d3fa3c64aa17df0fda7de5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="5258c-103">Problèmes de connexion à une application non issue de la galerie configurée pour l’authentification unique fédérée</span><span class="sxs-lookup"><span data-stu-id="5258c-103">Problems signing in to a non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="5258c-104">Pour résoudre votre problème, vous devez vérifier la configuration de l’application dans Azure AD de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="5258c-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="5258c-105">Vérifiez que vous avez suivi toutes les étapes de configuration pour l’application de la galerie Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5258c-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="5258c-106">Vérifiez que l’identificateur et l’URL de réponse configurés dans AAD correspondent aux valeurs attendues dans l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="5258c-107">Vérifiez que vous avez affecté des utilisateurs à l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="5258c-108">Application introuvable dans le répertoire</span><span class="sxs-lookup"><span data-stu-id="5258c-108">Application not found in directory</span></span>

<span data-ttu-id="5258c-109">*Erreur AADSTS70001 : L’application avec l’identificateur « https://contoso.com » est introuvable dans l’annuaire*.</span><span class="sxs-lookup"><span data-stu-id="5258c-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="5258c-110">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="5258c-110">**Possible cause**</span></span>

<span data-ttu-id="5258c-111">L’attribut d’émetteur envoyé de l’application vers Azure AD dans la demande SAML ne correspond pas à la valeur de l’identificateur configurée dans l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5258c-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="5258c-112">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="5258c-112">**Resolution**</span></span>

<span data-ttu-id="5258c-113">Vérifiez que l’attribut d’émetteur de la demande SAML correspond à la valeur de l’identificateur configurée dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="5258c-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="5258c-114">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="5258c-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5258c-115">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="5258c-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5258c-116">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5258c-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5258c-117">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5258c-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5258c-118">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="5258c-118">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="5258c-119">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="5258c-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5258c-120">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5258c-120">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="5258c-121">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5258c-122"><span id="_Hlk477190042" class="anchor"></span>Accédez à la section **Domaine et URL**.</span><span class="sxs-lookup"><span data-stu-id="5258c-122"><span id="_Hlk477190042" class="anchor"></span>Go to **Domain and URLs** section.</span></span> <span data-ttu-id="5258c-123">Vérifiez que la valeur située dans la zone de texte de l’identificateur correspond à celle de l’identificateur mentionnée dans l’erreur.</span><span class="sxs-lookup"><span data-stu-id="5258c-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="5258c-124">Une fois que vous avez mis à jour la valeur d’identificateur pour qu’elle corresponde à celle envoyée par l’application dans la demande SAML, vous pouvez vous connecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="5258c-125">L’adresse de réponse ne correspond pas aux adresses de réponse configurées pour l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-125">The reply address does not match the reply addresses configured for the application.</span></span> 

<span data-ttu-id="5258c-126">*Erreur AADSTS50011 : L’adresse de réponse « https://contoso.com » ne correspond pas à l’adresse de réponse configurée pour l’application*</span><span class="sxs-lookup"><span data-stu-id="5258c-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span> 

<span data-ttu-id="5258c-127">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="5258c-127">**Possible cause**</span></span> 

<span data-ttu-id="5258c-128">La valeur AssertionConsumerServiceURL dans la demande SAML ne correspond pas à la valeur de l’URL de réponse ou au modèle configuré dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5258c-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="5258c-129">La valeur AssertionConsumerServiceURL dans la demande SAML est l’URL que vous voyez dans l’erreur.</span><span class="sxs-lookup"><span data-stu-id="5258c-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span> 

<span data-ttu-id="5258c-130">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="5258c-130">**Resolution**</span></span> 

<span data-ttu-id="5258c-131">Assurez-vous que la valeur AssertionConsumerServiceURL dans la demande SAML correspond à la valeur de l’URL de réponse configurée dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5258c-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="5258c-132">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur.**</span><span class="sxs-lookup"><span data-stu-id="5258c-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="5258c-133">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="5258c-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="5258c-134">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5258c-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="5258c-135">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5258c-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="5258c-136">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="5258c-136">click **All Applications** to view a list of all your applications.</span></span> 

  * <span data-ttu-id="5258c-137">Si l’application que vous recherchez n’apparaît pas ici, utilisez le contrôle **Filtrer** en haut de la liste **Toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5258c-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and       set the **Show** option to **All Applications.**</span></span>
  
6.  <span data-ttu-id="5258c-138">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5258c-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="5258c-139">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5258c-140">Accédez à la section **Domaine et URL**.</span><span class="sxs-lookup"><span data-stu-id="5258c-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="5258c-141">Vérifiez ou mettez à jour la valeur figurant dans la zone de texte URL de réponse pour qu’elle corresponde à la valeur AssertionConsumerServiceURL dans la demande SAML.</span><span class="sxs-lookup"><span data-stu-id="5258c-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>

  * <span data-ttu-id="5258c-142">Si vous ne voyez pas la zone de texte URL de réponse, cochez la case **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="5258c-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="5258c-143">Une fois que vous avez mis à jour la valeur de l’URL de réponse dans Azure AD et qu’elle correspond à celle envoyée par l’application dans la demande SAML, vous devez être en mesure de vous connecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="5258c-144">Utilisateur non affecté à un rôle</span><span class="sxs-lookup"><span data-stu-id="5258c-144">User not assigned a role</span></span>

<span data-ttu-id="5258c-145">*Erreur AADSTS50105 : L’utilisateur connecté « brian@contoso.com » n’est pas affecté à un rôle pour l’application*</span><span class="sxs-lookup"><span data-stu-id="5258c-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*</span></span>

<span data-ttu-id="5258c-146">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="5258c-146">**Possible cause**</span></span>

<span data-ttu-id="5258c-147">L’utilisateur ne dispose pas des autorisations nécessaires pour accéder à l’application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5258c-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="5258c-148">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="5258c-148">**Resolution**</span></span>

<span data-ttu-id="5258c-149">Pour affecter un ou plusieurs utilisateurs directement à une application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5258c-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="5258c-150">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="5258c-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5258c-151">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="5258c-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5258c-152">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5258c-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5258c-153">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5258c-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5258c-154">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="5258c-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5258c-155">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="5258c-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5258c-156">Dans la liste qui s’affiche, sélectionnez l’application à laquelle vous souhaitez affecter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5258c-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="5258c-157">Une fois l’application chargée, cliquez sur **Utilisateurs et groupes** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5258c-158">Cliquez sur le bouton **Ajouter** en haut de la liste **Utilisateurs et groupes** pour ouvrir le panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="5258c-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5258c-159">Cliquez sur le sélecteur **Utilisateurs et groupes** à partir du panneau **Ajouter une attribution**.</span><span class="sxs-lookup"><span data-stu-id="5258c-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5258c-160">Tapez **le nom complet** ou **l’adresse de messagerie** de l’utilisateur souhaité pour l’attribution dans la zone de recherche **Rechercher par nom ou adresse de messagerie**.</span><span class="sxs-lookup"><span data-stu-id="5258c-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5258c-161">Pointez sur **l’utilisateur** dans la liste pour afficher une **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="5258c-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="5258c-162">Cliquez sur la case à cocher en regard de la photo de profil ou du logo de l’utilisateur pour ajouter ce dernier à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="5258c-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="5258c-163">**Facultatif :** si vous souhaitez **ajouter plusieurs utilisateurs**, entrez un autre **nom complet** ou une autre **adresse de messagerie** dans la zone de recherche **Rechercher par nom ou adresse de messagerie**, puis cliquez sur la case à cocher pour ajouter cet utilisateur à la liste **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="5258c-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="5258c-164">Après avoir sélectionné les utilisateurs, cliquez sur le bouton **Sélectionner** pour les ajouter à la liste des utilisateurs et des groupes à affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="5258c-165">**Facultatif :** cliquez sur le sélecteur **Sélectionner un rôle** dans le panneau **Ajouter une attribution** pour sélectionner un rôle à affecter aux utilisateurs que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="5258c-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="5258c-166">Cliquez sur le bouton **Attribuer** pour affecter l’application aux utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="5258c-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="5258c-167">Après une courte période, les utilisateurs que vous avez sélectionnés seront en mesure de démarrer ces applications à l’aide des méthodes décrites dans la section de description des solutions.</span><span class="sxs-lookup"><span data-stu-id="5258c-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="5258c-168">Demande SAML non valide</span><span class="sxs-lookup"><span data-stu-id="5258c-168">Not a valid SAML Request</span></span>

<span data-ttu-id="5258c-169">*Erreur AADSTS75005 : La demande n’est pas un message de protocole Saml2 valide.*</span><span class="sxs-lookup"><span data-stu-id="5258c-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="5258c-170">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="5258c-170">**Possible cause**</span></span>

<span data-ttu-id="5258c-171">Azure AD ne prend pas en charge les demandes SAML envoyées par l’application pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5258c-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="5258c-172">Voici certains problèmes courants :</span><span class="sxs-lookup"><span data-stu-id="5258c-172">Some common issues are:</span></span>

-   <span data-ttu-id="5258c-173">Des champs obligatoires sont manquants dans la demande SAML</span><span class="sxs-lookup"><span data-stu-id="5258c-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="5258c-174">La méthode de demande SAML encodée</span><span class="sxs-lookup"><span data-stu-id="5258c-174">SAML request encoded method</span></span>

<span data-ttu-id="5258c-175">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="5258c-175">**Resolution**</span></span>

1.  <span data-ttu-id="5258c-176">Capturez la demande SAML.</span><span class="sxs-lookup"><span data-stu-id="5258c-176">Capture SAML request.</span></span> <span data-ttu-id="5258c-177">Pour savoir comment capturer la demande SAML, suivez le didacticiel [Comment déboguer une authentification unique SAML pour des applications dans Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="5258c-177">follow the tutorial on [how to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="5258c-178">Contactez le fournisseur de l’application et communiquez-lui les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5258c-178">Contact the application vendor and share:</span></span>

    -   <span data-ttu-id="5258c-179">Demande SAML</span><span class="sxs-lookup"><span data-stu-id="5258c-179">SAML request</span></span>

    -   [<span data-ttu-id="5258c-180">Spécifications du protocole SAML d’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5258c-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="5258c-181">Il doit confirmer sa prise en charge de l’implémentation SAML Azure AD pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5258c-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="5258c-182">Aucune ressource dans la liste requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="5258c-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="5258c-183">*Erreur AADSTS65005 : L’application cliente a demandé l’accès à la ressource « 00000002-0000-0000-c000-000000000000 ». La demande a échoué, car le client n’a pas spécifié cette ressource dans sa liste requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="5258c-183">*Error AADSTS65005: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="5258c-184">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="5258c-184">**Possible cause**</span></span>

<span data-ttu-id="5258c-185">L’objet d’application est endommagé.</span><span class="sxs-lookup"><span data-stu-id="5258c-185">The application object is corrupted.</span></span>

<span data-ttu-id="5258c-186">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="5258c-186">**Resolution**</span></span>

<span data-ttu-id="5258c-187">Pour résoudre ce problème, supprimez l’application du répertoire.</span><span class="sxs-lookup"><span data-stu-id="5258c-187">To solve the problem, remove the application from the directory.</span></span> <span data-ttu-id="5258c-188">Ensuite, pour ajouter et reconfigurer l’application, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5258c-188">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="5258c-189">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="5258c-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5258c-190">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="5258c-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5258c-191">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5258c-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5258c-192">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5258c-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5258c-193">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="5258c-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5258c-194">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="5258c-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5258c-195">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5258c-195">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="5258c-196">Cliquez sur **Supprimer** dans le coin supérieur gauche du panneau **Présentation** de l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-196">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="5258c-197">Actualisez Azure AD et ajoutez l’application à partir de la galerie Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5258c-197">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="5258c-198">Ensuite, reconfigurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-198">Then, Configure the application again.</span></span>

<span data-ttu-id="5258c-199">Une fois l’application reconfigurée, vous devez être en mesure de vous connecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-199">After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="5258c-200">Certificat ou clé non configuré(e)</span><span class="sxs-lookup"><span data-stu-id="5258c-200">Certificate or key not configured</span></span>

<span data-ttu-id="5258c-201">Erreur AADSTS50003 : Aucune clé de signature configurée.</span><span class="sxs-lookup"><span data-stu-id="5258c-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="5258c-202">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="5258c-202">**Possible cause**</span></span>

<span data-ttu-id="5258c-203">L’objet d’application est endommagé et Azure AD ne reconnaît pas le certificat configuré pour l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-203">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="5258c-204">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="5258c-204">**Resolution**</span></span>

<span data-ttu-id="5258c-205">Pour supprimer et créer un nouveau certificat, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5258c-205">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="5258c-206">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur**.</span><span class="sxs-lookup"><span data-stu-id="5258c-206">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5258c-207">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="5258c-207">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5258c-208">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5258c-208">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5258c-209">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5258c-209">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5258c-210">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="5258c-210">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5258c-211">Si l’application que vous recherchez ne figure pas dans la liste, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="5258c-211">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5258c-212">Sélectionnez l’application pour laquelle vous souhaitez configurer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5258c-212">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="5258c-213">Une fois l’application chargée, cliquez sur **Authentification unique** dans le menu de navigation de gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="5258c-213">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5258c-214">Dans la section **Certificat de signature SAML**, cliquez sur **Créer un certificat**.</span><span class="sxs-lookup"><span data-stu-id="5258c-214">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="5258c-215">Sélectionnez une date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="5258c-215">Select Expiration date.</span></span> <span data-ttu-id="5258c-216">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5258c-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="5258c-217">Cochez la case **Activer le nouveau certificat** pour substituer le certificat actif.</span><span class="sxs-lookup"><span data-stu-id="5258c-217">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="5258c-218">Ensuite, cliquez sur **Enregistrer** en haut du panneau, puis acceptez d’activer le certificat de substitution.</span><span class="sxs-lookup"><span data-stu-id="5258c-218">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="5258c-219">Dans la section **Certificat de signature SAML**, cliquez sur **Supprimer** pour supprimer le certificat **Inutilisé**.</span><span class="sxs-lookup"><span data-stu-id="5258c-219">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="5258c-220">Problème lors de la personnalisation des revendications SAML envoyées à une application</span><span class="sxs-lookup"><span data-stu-id="5258c-220">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="5258c-221">Pour savoir comment personnaliser les revendications d’attribut SAML envoyées à votre application, consultez l’article [Mappage des revendications dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5258c-221">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5258c-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5258c-222">Next steps</span></span>
[<span data-ttu-id="5258c-223">Spécifications du protocole SAML d’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5258c-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
