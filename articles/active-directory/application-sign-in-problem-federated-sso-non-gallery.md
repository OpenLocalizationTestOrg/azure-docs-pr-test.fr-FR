---
title: "aaaProblems application de la galerie de tooa configurée pour fédéré de signature sur l’authentification unique | Documents Microsoft"
description: "Conseils pour les problèmes spécifiques hello que vous pouvez rencontrer lors de la signature dans l’application tooan configurée pour SAML-fédéré-authentification auprès d’Azure AD"
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
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="10987-103">Problèmes de connexion d’application de non-galerie tooa configurée pour fédérée l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="10987-103">Problems signing in tooa non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="10987-104">tootroubleshoot votre problème, vous avez besoin de configuration de l’application hello tooverify dans Azure AD comme suit :</span><span class="sxs-lookup"><span data-stu-id="10987-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="10987-105">Vous avez suivi toutes les étapes de configuration hello pour hello application de la galerie Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10987-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="10987-106">Hello identificateur et l’URL de réponse configurée dans AAD correspond à elles, les valeurs attendues dans l’application hello</span><span class="sxs-lookup"><span data-stu-id="10987-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="10987-107">Vous avez affecté des utilisateurs toohello application</span><span class="sxs-lookup"><span data-stu-id="10987-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="10987-108">Application introuvable dans le répertoire</span><span class="sxs-lookup"><span data-stu-id="10987-108">Application not found in directory</span></span>

<span data-ttu-id="10987-109">*Erreur AADSTS70001 : Application avec l’identificateur « https://contoso.com » est introuvable dans le répertoire de hello*.</span><span class="sxs-lookup"><span data-stu-id="10987-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="10987-110">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="10987-110">**Possible cause**</span></span>

<span data-ttu-id="10987-111">attribut de l’émetteur Hello envoie hello application tooAzure AD dans la demande SAML hello ne correspond pas à valeur de l’identificateur hello configuré dans l’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10987-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="10987-112">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="10987-112">**Resolution**</span></span>

<span data-ttu-id="10987-113">Vérifiez que cet attribut de l’émetteur hello dans la demande SAML hello qu'est mise en correspondance le hello valeur d’identificateur configuré dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="10987-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="10987-114">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="10987-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="10987-115">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="10987-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="10987-116">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="10987-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="10987-117">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10987-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="10987-118">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="10987-118">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="10987-119">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="10987-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="10987-120">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="10987-120">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="10987-121">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="10987-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="10987-122"><span id="_Hlk477190042" class="anchor"></span>Accédez trop**domaine et les URL** section.</span><span class="sxs-lookup"><span data-stu-id="10987-122"><span id="_Hlk477190042" class="anchor"></span>Go too**Domain and URLs** section.</span></span> <span data-ttu-id="10987-123">Vérifiez cette valeur hello Bonjour identificateur valeur hello pour la valeur de l’identificateur hello affiché par erreur de hello est correspondant à la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="10987-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="10987-124">Une fois que vous avez mis à jour de valeur d’identificateur hello dans Azure AD et sa correspondance hello valeur envoie par application hello dans la demande SAML hello, vous devez être en mesure de toosign dans toohello application.</span><span class="sxs-lookup"><span data-stu-id="10987-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="10987-125">adresse de réponse Hello ne correspondent pas aux adresses de réponse de hello configurés pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="10987-125">hello reply address does not match hello reply addresses configured for hello application.</span></span> 

<span data-ttu-id="10987-126">*Erreur AADSTS50011 : adresse de réponse hello 'https://contoso.com' ne correspond pas à des adresses de réponse hello configurés pour l’application hello*</span><span class="sxs-lookup"><span data-stu-id="10987-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span> 

<span data-ttu-id="10987-127">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="10987-127">**Possible cause**</span></span> 

<span data-ttu-id="10987-128">valeur de l’URL de réponse hello ou un modèle configuré dans Azure AD ne correspond pas Hello valeur AssertionConsumerServiceURL dans la demande SAML hello.</span><span class="sxs-lookup"><span data-stu-id="10987-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="10987-129">Hello valeur AssertionConsumerServiceURL dans la demande SAML hello est URL hello vous voyez dans l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="10987-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span> 

<span data-ttu-id="10987-130">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="10987-130">**Resolution**</span></span> 

<span data-ttu-id="10987-131">Vérifiez que cette valeur de AssertionConsumerServiceURL hello dans la demande SAML hello sa correspondance hello valeur de l’URL de réponse est configuré dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10987-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="10987-132">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="10987-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="10987-133">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="10987-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="10987-134">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="10987-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="10987-135">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10987-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="10987-136">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="10987-136">click **All Applications** tooview a list of all your applications.</span></span> 

  * <span data-ttu-id="10987-137">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="10987-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and       set hello **Show** option too**All Applications.**</span></span>
  
6.  <span data-ttu-id="10987-138">Sélectionnez application hello tooconfigure l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="10987-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="10987-139">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="10987-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="10987-140">Accédez trop**domaine et les URL** section.</span><span class="sxs-lookup"><span data-stu-id="10987-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="10987-141">Vérifier ou mettre à jour la valeur de hello dans la zone de texte toomatch hello valeur AssertionConsumerServiceURL dans la demande SAML hello de hello URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="10987-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>

  * <span data-ttu-id="10987-142">Si vous ne voyez pas de zone de texte URL de réponse hello sélectionnez hello **afficher les paramètres d’URL avancés** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="10987-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="10987-143">Une fois que vous avez mis à jour valeur de l’URL de réponse hello dans Azure AD et qu’il a correspondant hello valeur envoie par application hello Bonjour demande SAML, vous devez être en mesure de toosign dans toohello application.</span><span class="sxs-lookup"><span data-stu-id="10987-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="10987-144">Utilisateur non affecté à un rôle</span><span class="sxs-lookup"><span data-stu-id="10987-144">User not assigned a role</span></span>

<span data-ttu-id="10987-145">*Erreur AADSTS50105 : hello utilisateur connecté 'brian@contoso.com' ne possède pas de rôle tooa pour l’application hello*</span><span class="sxs-lookup"><span data-stu-id="10987-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*</span></span>

<span data-ttu-id="10987-146">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="10987-146">**Possible cause**</span></span>

<span data-ttu-id="10987-147">Hello lui n'ont pas été accordées application toohello d’accès dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10987-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="10987-148">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="10987-148">**Resolution**</span></span>

<span data-ttu-id="10987-149">tooassign un ou plusieurs utilisateurs tooan application directement, comme suit hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="10987-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="10987-150">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global.**</span><span class="sxs-lookup"><span data-stu-id="10987-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="10987-151">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="10987-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="10987-152">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="10987-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="10987-153">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10987-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="10987-154">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="10987-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="10987-155">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="10987-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="10987-156">Sélectionnez l’application hello tooassign une liste des utilisateurs toofrom hello.</span><span class="sxs-lookup"><span data-stu-id="10987-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="10987-157">Une fois le charge de l’application hello, cliquez sur **utilisateurs et groupes** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="10987-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="10987-158">Cliquez sur hello **ajouter** bouton par-dessus hello **utilisateurs et groupes** hello tooopen de liste **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="10987-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="10987-159">Cliquez sur hello **utilisateurs et groupes** sélecteur de hello **ajouter l’affectation** panneau.</span><span class="sxs-lookup"><span data-stu-id="10987-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="10987-160">Type Bonjour **nom complet** ou **adresse de messagerie** d’utilisateur hello vous êtes intéressé par attribution dans hello **recherche par nom ou adresse de messagerie** zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="10987-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="10987-161">Placez le curseur sur hello **utilisateur** dans hello liste tooreveal un **case à cocher**.</span><span class="sxs-lookup"><span data-stu-id="10987-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="10987-162">Cliquez sur tooadd de photo ou le logo de profil hello case à cocher suivante toohello l’utilisateur à votre toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="10987-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="10987-163">**Facultatif :** si vous souhaitez que trop**ajouter plusieurs utilisateurs**, type dans un autre **nom complet** ou **adresse de messagerie** dans hello **Rechercher par nom ou l’adresse de messagerie** zone de recherche, cliquez sur tooadd de case à cocher hello cette toohello utilisateur **sélectionnés** liste.</span><span class="sxs-lookup"><span data-stu-id="10987-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="10987-164">Lorsque vous avez fini de sélectionner les utilisateurs, cliquez sur hello **sélectionnez** bouton tooadd les toohello la liste des toobe utilisateurs et groupes affectés toohello application.</span><span class="sxs-lookup"><span data-stu-id="10987-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="10987-165">**Facultatif :** cliquez sur hello **sélectionner un rôle** sélecteur Bonjour **ajouter l’affectation** panneau tooselect un rôle aux utilisateurs de toohello tooassign que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="10987-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="10987-166">Cliquez sur hello **affecter** bouton tooassign hello application toohello les utilisateurs sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="10987-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="10987-167">Après une courte période de temps, les utilisateurs de hello que vous avez sélectionné en toolaunch en mesure de ces applications à l’aide de hello des méthodes décrites dans la section de description de solution hello.</span><span class="sxs-lookup"><span data-stu-id="10987-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="10987-168">Demande SAML non valide</span><span class="sxs-lookup"><span data-stu-id="10987-168">Not a valid SAML Request</span></span>

<span data-ttu-id="10987-169">*Erreur AADSTS75005 : demande de hello n’est pas un message de protocole Saml2 valid.*</span><span class="sxs-lookup"><span data-stu-id="10987-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="10987-170">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="10987-170">**Possible cause**</span></span>

<span data-ttu-id="10987-171">Azure AD ne prend pas en charge hello SAML de demande envoyé par l’application hello pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="10987-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="10987-172">Voici certains problèmes courants :</span><span class="sxs-lookup"><span data-stu-id="10987-172">Some common issues are:</span></span>

-   <span data-ttu-id="10987-173">Les champs requis dans la demande SAML hello manquants</span><span class="sxs-lookup"><span data-stu-id="10987-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="10987-174">La méthode de demande SAML encodée</span><span class="sxs-lookup"><span data-stu-id="10987-174">SAML request encoded method</span></span>

<span data-ttu-id="10987-175">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="10987-175">**Resolution**</span></span>

1.  <span data-ttu-id="10987-176">Capturez la demande SAML.</span><span class="sxs-lookup"><span data-stu-id="10987-176">Capture SAML request.</span></span> <span data-ttu-id="10987-177">Suivez le didacticiel de hello [comment toodebug basé sur SAML uniques authentification tooapplications dans Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn toocapture hello SAML demander.</span><span class="sxs-lookup"><span data-stu-id="10987-177">follow hello tutorial on [how toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="10987-178">Contactez le fournisseur de l’application hello et partage :</span><span class="sxs-lookup"><span data-stu-id="10987-178">Contact hello application vendor and share:</span></span>

    -   <span data-ttu-id="10987-179">Demande SAML</span><span class="sxs-lookup"><span data-stu-id="10987-179">SAML request</span></span>

    -   [<span data-ttu-id="10987-180">Spécifications du protocole SAML d’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="10987-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="10987-181">Ils doivent valider ils prennent en charge l’implémentation d’Azure AD SAML hello pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="10987-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="10987-182">Aucune ressource dans la liste requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="10987-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="10987-183">*Erreur AADSTS65005 : hello client application demande l’accès tooresource ' 00000002-0000-0000-c000-type "000000000000"'. Cette demande a échoué, car le client de hello, cette ressource n’a pas spécifié dans sa liste requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="10987-183">*Error AADSTS65005: hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="10987-184">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="10987-184">**Possible cause**</span></span>

<span data-ttu-id="10987-185">objet de l’application Hello est endommagé.</span><span class="sxs-lookup"><span data-stu-id="10987-185">hello application object is corrupted.</span></span>

<span data-ttu-id="10987-186">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="10987-186">**Resolution**</span></span>

<span data-ttu-id="10987-187">problème de hello toosolve, supprimer une application hello à partir du répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="10987-187">toosolve hello problem, remove hello application from hello directory.</span></span> <span data-ttu-id="10987-188">Ensuite, ajoutez et reconfigurer l’application hello, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="10987-188">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="10987-189">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="10987-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="10987-190">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="10987-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="10987-191">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="10987-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="10987-192">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10987-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="10987-193">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="10987-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="10987-194">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="10987-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="10987-195">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="10987-195">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="10987-196">Cliquez sur **supprimer** en hello en haut à gauche de l’application hello **vue d’ensemble** panneau.</span><span class="sxs-lookup"><span data-stu-id="10987-196">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="10987-197">Actualiser Azure AD et ajouter l’application hello à partir de la galerie d’Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="10987-197">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="10987-198">Configurez ensuite l’application hello.</span><span class="sxs-lookup"><span data-stu-id="10987-198">Then, Configure hello application again.</span></span>

<span data-ttu-id="10987-199">Après la reconfiguration d’application hello, vous devez être en mesure de toosign dans toohello application.</span><span class="sxs-lookup"><span data-stu-id="10987-199">After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="10987-200">Certificat ou clé non configuré(e)</span><span class="sxs-lookup"><span data-stu-id="10987-200">Certificate or key not configured</span></span>

<span data-ttu-id="10987-201">Erreur AADSTS50003 : Aucune clé de signature configurée.</span><span class="sxs-lookup"><span data-stu-id="10987-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="10987-202">**Cause possible**</span><span class="sxs-lookup"><span data-stu-id="10987-202">**Possible cause**</span></span>

<span data-ttu-id="10987-203">objet de l’application Hello est endommagé et Azure AD ne reconnaît pas certificat hello configuré pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="10987-203">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="10987-204">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="10987-204">**Resolution**</span></span>

<span data-ttu-id="10987-205">toodelete et créer un nouveau certificat, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="10987-205">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="10987-206">Ouvrez hello [ **Azure Portal** ](https://portal.azure.com/) et connectez-vous en tant qu’un **administrateur Global** ou **Co-Admin.**</span><span class="sxs-lookup"><span data-stu-id="10987-206">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="10987-207">Ouvrez hello **Extension Azure Active Directory** en cliquant sur **davantage de services** bas hello du menu de navigation de gauche principal hello.</span><span class="sxs-lookup"><span data-stu-id="10987-207">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="10987-208">Tapez dans **« Azure Active Directory**» dans la zone de recherche filtre hello et sélectionnez hello **Azure Active Directory** élément.</span><span class="sxs-lookup"><span data-stu-id="10987-208">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="10987-209">Cliquez sur **des Applications d’entreprise** à partir du menu de navigation gauche hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10987-209">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="10987-210">Cliquez sur **toutes les Applications** tooview une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="10987-210">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="10987-211">Si vous ne voyez pas l’application hello que vous souhaitez afficher ici, utilisez hello **filtre** contrôle haut hello hello **liste de toutes les Applications** et ensemble hello **afficher** option trop **Toutes les Applications.**</span><span class="sxs-lookup"><span data-stu-id="10987-211">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="10987-212">Sélectionnez l’application hello tooconfigure l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="10987-212">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="10987-213">Une fois que la charge de l’application hello, cliquez sur hello **l’authentification unique** à partir du menu de navigation de gauche de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="10987-213">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="10987-214">Cliquez sur **créer un nouveau certificat** sous hello **SAML certificat de signature** section.</span><span class="sxs-lookup"><span data-stu-id="10987-214">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="10987-215">Sélectionnez une date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="10987-215">Select Expiration date.</span></span> <span data-ttu-id="10987-216">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="10987-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="10987-217">Vérifiez **activer le nouveau certificat** certificat de toooverride hello active.</span><span class="sxs-lookup"><span data-stu-id="10987-217">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="10987-218">Ensuite, cliquez sur **enregistrer** haut hello du Panneau de hello et accepter le certificat de substitution tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="10987-218">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="10987-219">Sous hello **le certificat de signature SAML** , cliquez sur **supprimer** tooremove hello **inutilisé** certificat.</span><span class="sxs-lookup"><span data-stu-id="10987-219">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="10987-220">Problème lors de la personnalisation des revendications de hello SAML envoyé tooan application</span><span class="sxs-lookup"><span data-stu-id="10987-220">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="10987-221">toolearn toocustomize hello SAML attribut revendications envoyées tooyour application, voir [revendications mappage dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="10987-221">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10987-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10987-222">Next steps</span></span>
[<span data-ttu-id="10987-223">Spécifications du protocole SAML d’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="10987-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
