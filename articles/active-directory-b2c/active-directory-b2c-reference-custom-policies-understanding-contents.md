---
title: "Azure Active Directory B2C : Présentation des stratégies personnalisées du pack de démarrage | Microsoft Docs"
description: "Une rubrique sur les stratégies personnalisées Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="d14ba-103">Présentation des stratégies personnalisées du pack de démarrage Azure AD B2C Custom Policy</span><span class="sxs-lookup"><span data-stu-id="d14ba-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="d14ba-104">Cette section répertorie les principaux éléments de la stratégie B2C_1A_base qui est fournie avec le **Pack de démarrage** et utilisée pour créer ses propres stratégies via l’héritage de la *stratégie B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="d14ba-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="d14ba-105">Par conséquent, il se concentre plutôt sur les types de revendication, les transformations de revendication, les définitions de contenu, les fournisseurs de revendications avec leurs profils techniques, et les principaux parcours utilisateur déjà définis.</span><span class="sxs-lookup"><span data-stu-id="d14ba-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d14ba-106">Microsoft n’offre aucune garantie, expresse ou implicite, concernant les informations contenues dans ce document.</span><span class="sxs-lookup"><span data-stu-id="d14ba-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="d14ba-107">Des modifications peuvent être apportées à tout moment, avant, pendant ou après la mise à la disposition générale.</span><span class="sxs-lookup"><span data-stu-id="d14ba-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="d14ba-108">Vos propres stratégies, ainsi que la stratégie B2C_1A_base_extensions, peuvent remplacer ces définitions et étendre cette stratégie parente en fournissant de nouvelles définitions le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="d14ba-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="d14ba-109">La *stratégie B2C_1A_base* comporte des types de revendication, des transformations de revendication et des définitions de contenu.</span><span class="sxs-lookup"><span data-stu-id="d14ba-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="d14ba-110">Ces éléments peuvent être référencés dans vos propres stratégies, ainsi que dans la *stratégie B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="d14ba-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="d14ba-111">Schéma de revendications</span><span class="sxs-lookup"><span data-stu-id="d14ba-111">Claims schemas</span></span>

<span data-ttu-id="d14ba-112">Ce schéma de revendications comprend trois sections :</span><span class="sxs-lookup"><span data-stu-id="d14ba-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="d14ba-113">La première section répertorie les revendications minimales requises pour garantir le bon fonctionnement des parcours utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d14ba-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="d14ba-114">La deuxième section répertorie les revendications requises pour les paramètres de chaîne de requête et d’autres paramètres spéciaux devant être transférés à d’autres fournisseurs de revendications, notamment login.microsoftonline.com pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="d14ba-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="d14ba-115">**Ne modifiez pas ces revendications**.</span><span class="sxs-lookup"><span data-stu-id="d14ba-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="d14ba-116">Enfin, la troisième section répertorie toutes les revendications supplémentaires et facultatives qui peuvent être collectées à partir de l’utilisateur, stockées dans le répertoire et transmises aux jetons lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="d14ba-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="d14ba-117">Vous pouvez ajouter dans cette section tout nouveau type de revendications à collecter à partir de l’utilisateur et/ou à transmettre au jeton.</span><span class="sxs-lookup"><span data-stu-id="d14ba-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d14ba-118">Le schéma de revendications inclut des restrictions pour certaines revendications, telles que des noms d’utilisateur et des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="d14ba-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="d14ba-119">La stratégie Trust Framework (TF) traite Azure AD comme n’importe quel autre fournisseur de revendications et toutes ses restrictions sont modélisées dans la stratégie premium.</span><span class="sxs-lookup"><span data-stu-id="d14ba-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="d14ba-120">Vous pouvez modifier une stratégie pour y ajouter de nouvelles restrictions ou utiliser un autre fournisseur de revendications pour le stockage d’informations d’identification avec ses propres restrictions.</span><span class="sxs-lookup"><span data-stu-id="d14ba-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="d14ba-121">Les types de revendication disponibles sont répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d14ba-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="d14ba-122">Revendications requises pour les parcours utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="d14ba-123">Les revendications suivantes sont requises pour garantir le bon fonctionnement des parcours utilisateur :</span><span class="sxs-lookup"><span data-stu-id="d14ba-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="d14ba-124">Type de revendication</span><span class="sxs-lookup"><span data-stu-id="d14ba-124">Claims type</span></span> | <span data-ttu-id="d14ba-125">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="d14ba-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-126">*UserId*</span></span> | <span data-ttu-id="d14ba-127">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-127">Username</span></span> |
| <span data-ttu-id="d14ba-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="d14ba-128">*signInName*</span></span> | <span data-ttu-id="d14ba-129">Nom de connexion</span><span class="sxs-lookup"><span data-stu-id="d14ba-129">Sign in name</span></span> |
| <span data-ttu-id="d14ba-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-130">*tenantId*</span></span> | <span data-ttu-id="d14ba-131">ID de locataire de l’objet utilisateur dans Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="d14ba-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="d14ba-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-132">*objectId*</span></span> | <span data-ttu-id="d14ba-133">ID d’objet de l’objet utilisateur dans Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="d14ba-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="d14ba-134">*mot de passe*</span><span class="sxs-lookup"><span data-stu-id="d14ba-134">*password*</span></span> | <span data-ttu-id="d14ba-135">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="d14ba-135">Password</span></span> |
| <span data-ttu-id="d14ba-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="d14ba-136">*newPassword*</span></span> | |
| <span data-ttu-id="d14ba-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="d14ba-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="d14ba-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="d14ba-138">*passwordPolicies*</span></span> | <span data-ttu-id="d14ba-139">Stratégies de mot de passe utilisées par Azure AD B2C Premium pour définir la force du mot de passe, la date d’expiration, etc.</span><span class="sxs-lookup"><span data-stu-id="d14ba-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="d14ba-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="d14ba-140">*sub*</span></span> | |
| <span data-ttu-id="d14ba-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="d14ba-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="d14ba-142">*identityProvider*</span></span> | |
| <span data-ttu-id="d14ba-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="d14ba-143">*displayName*</span></span> | |
| <span data-ttu-id="d14ba-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="d14ba-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="d14ba-145">Numéro de téléphone de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-145">User's telephone number</span></span> |
| <span data-ttu-id="d14ba-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="d14ba-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="d14ba-147">*email*</span><span class="sxs-lookup"><span data-stu-id="d14ba-147">*email*</span></span> | <span data-ttu-id="d14ba-148">Adresse e-mail qui peut être utilisée pour contacter l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="d14ba-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="d14ba-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="d14ba-150">Adresse e-mail que l’utilisateur peut utiliser pour se connecter</span><span class="sxs-lookup"><span data-stu-id="d14ba-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="d14ba-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="d14ba-151">*otherMails*</span></span> | <span data-ttu-id="d14ba-152">Adresses e-mail qui peuvent être utilisées pour contacter l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="d14ba-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="d14ba-153">*userPrincipalName*</span></span> | <span data-ttu-id="d14ba-154">Nom d’utilisateur enregistré dans Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="d14ba-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="d14ba-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="d14ba-155">*upnUserName*</span></span> | <span data-ttu-id="d14ba-156">Nom d’utilisateur utilisé pour créer le nom d’utilisateur principal</span><span class="sxs-lookup"><span data-stu-id="d14ba-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="d14ba-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="d14ba-157">*mailNickName*</span></span> | <span data-ttu-id="d14ba-158">Pseudonyme de l’utilisateur enregistré dans Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="d14ba-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="d14ba-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="d14ba-159">*newUser*</span></span> | |
| <span data-ttu-id="d14ba-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="d14ba-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="d14ba-161">Revendication qui spécifie si les attributs ont été collectés à partir de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="d14ba-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="d14ba-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="d14ba-163">Revendication qui spécifie si un nouveau numéro de téléphone a été collecté à partir de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="d14ba-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="d14ba-164">*authenticationSource*</span></span> | <span data-ttu-id="d14ba-165">Spécifie si l’utilisateur a été authentifié via un fournisseur d’identité de réseaux sociaux, login.microsoftonline.com ou un compte local</span><span class="sxs-lookup"><span data-stu-id="d14ba-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="d14ba-166">Revendications requises pour les paramètres de chaîne de requête et d’autres paramètres spéciaux</span><span class="sxs-lookup"><span data-stu-id="d14ba-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="d14ba-167">Les revendications suivantes sont requises pour transmettre des paramètres spéciaux (y compris certains paramètres de chaîne de requête) à d’autres fournisseurs de revendications :</span><span class="sxs-lookup"><span data-stu-id="d14ba-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="d14ba-168">Type de revendication</span><span class="sxs-lookup"><span data-stu-id="d14ba-168">Claims type</span></span> | <span data-ttu-id="d14ba-169">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="d14ba-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="d14ba-170">*nux*</span></span> | <span data-ttu-id="d14ba-171">Paramètre spécial transmis pour l’authentification du compte local à login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d14ba-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="d14ba-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="d14ba-172">*nca*</span></span> | <span data-ttu-id="d14ba-173">Paramètre spécial transmis pour l’authentification du compte local à login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d14ba-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="d14ba-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="d14ba-174">*prompt*</span></span> | <span data-ttu-id="d14ba-175">Paramètre spécial transmis pour l’authentification du compte local à login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d14ba-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="d14ba-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="d14ba-176">*mkt*</span></span> | <span data-ttu-id="d14ba-177">Paramètre spécial transmis pour l’authentification du compte local à login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d14ba-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="d14ba-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="d14ba-178">*lc*</span></span> | <span data-ttu-id="d14ba-179">Paramètre spécial transmis pour l’authentification du compte local à login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d14ba-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="d14ba-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="d14ba-180">*grant_type*</span></span> | <span data-ttu-id="d14ba-181">Paramètre spécial transmis pour l’authentification du compte local à login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d14ba-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="d14ba-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="d14ba-182">*scope*</span></span> | <span data-ttu-id="d14ba-183">Paramètre spécial transmis pour l’authentification du compte local à login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d14ba-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="d14ba-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="d14ba-184">*client_id*</span></span> | <span data-ttu-id="d14ba-185">Paramètre spécial transmis pour l’authentification du compte local à login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="d14ba-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="d14ba-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="d14ba-186">*objectIdFromSession*</span></span> | <span data-ttu-id="d14ba-187">Paramètre fourni par le fournisseur de gestion des sessions par défaut pour indiquer que l’ID d’objet a été récupéré à partir d’une session d’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d14ba-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="d14ba-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="d14ba-188">*isActiveMFASession*</span></span> | <span data-ttu-id="d14ba-189">Paramètre fourni par le fournisseur de gestion des sessions MFA pour indiquer que l’utilisateur dispose d’une session MFA active</span><span class="sxs-lookup"><span data-stu-id="d14ba-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="d14ba-190">Revendications supplémentaires (facultatives) qui peuvent être collectées</span><span class="sxs-lookup"><span data-stu-id="d14ba-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="d14ba-191">Les revendications suivantes sont des revendications supplémentaires qui peuvent être collectées à partir des utilisateurs, stockées dans le répertoire et transmises aux jetons.</span><span class="sxs-lookup"><span data-stu-id="d14ba-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="d14ba-192">Comme indiqué ci-dessus, des revendications supplémentaires peuvent être ajoutées à cette liste.</span><span class="sxs-lookup"><span data-stu-id="d14ba-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="d14ba-193">Type de revendication</span><span class="sxs-lookup"><span data-stu-id="d14ba-193">Claims type</span></span> | <span data-ttu-id="d14ba-194">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="d14ba-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="d14ba-195">*givenName*</span></span> | <span data-ttu-id="d14ba-196">Prénom de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="d14ba-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="d14ba-197">*surname*</span></span> | <span data-ttu-id="d14ba-198">Nom de famille de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="d14ba-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="d14ba-199">*Extension_picture*</span></span> | <span data-ttu-id="d14ba-200">Image de l’utilisateur obtenue via les réseaux sociaux</span><span class="sxs-lookup"><span data-stu-id="d14ba-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="d14ba-201">Transformations de revendication</span><span class="sxs-lookup"><span data-stu-id="d14ba-201">Claim transformations</span></span>

<span data-ttu-id="d14ba-202">Les transformations de revendication disponibles sont répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d14ba-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="d14ba-203">Transformation de revendication</span><span class="sxs-lookup"><span data-stu-id="d14ba-203">Claim transformation</span></span> | <span data-ttu-id="d14ba-204">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="d14ba-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="d14ba-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="d14ba-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="d14ba-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="d14ba-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="d14ba-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="d14ba-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="d14ba-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="d14ba-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="d14ba-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="d14ba-211">Définitions de contenu</span><span class="sxs-lookup"><span data-stu-id="d14ba-211">Content definitions</span></span>

<span data-ttu-id="d14ba-212">Cette section présente les définitions de contenu déjà déclarées dans la stratégie *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="d14ba-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="d14ba-213">Ces définitions de contenu peuvent être référencées, remplacées et/ou étendues autant que nécessaire dans vos propres stratégies, ainsi que dans la stratégie *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="d14ba-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="d14ba-214">Fournisseur de revendications</span><span class="sxs-lookup"><span data-stu-id="d14ba-214">Claims provider</span></span> | <span data-ttu-id="d14ba-215">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="d14ba-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="d14ba-216">*Facebook*</span></span> | |
| <span data-ttu-id="d14ba-217">*Local Account SignIn*</span><span class="sxs-lookup"><span data-stu-id="d14ba-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="d14ba-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="d14ba-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="d14ba-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="d14ba-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="d14ba-220">*Self Asserted*</span><span class="sxs-lookup"><span data-stu-id="d14ba-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="d14ba-221">*Local Account*</span><span class="sxs-lookup"><span data-stu-id="d14ba-221">*Local Account*</span></span> | |
| <span data-ttu-id="d14ba-222">*Gestion des sessions*</span><span class="sxs-lookup"><span data-stu-id="d14ba-222">*Session Management*</span></span> | |
| <span data-ttu-id="d14ba-223">*Trustframework Policy Engine*</span><span class="sxs-lookup"><span data-stu-id="d14ba-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="d14ba-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="d14ba-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="d14ba-225">*Token Issuer*</span><span class="sxs-lookup"><span data-stu-id="d14ba-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="d14ba-226">Profils techniques</span><span class="sxs-lookup"><span data-stu-id="d14ba-226">Technical profiles</span></span>

<span data-ttu-id="d14ba-227">Cette section décrit les profils techniques déjà déclarés par le fournisseur de revendications dans la stratégie *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="d14ba-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="d14ba-228">Ces profils techniques peuvent être référencés, remplacés et/ou étendus autant que nécessaire dans vos propres stratégies, ainsi que dans la stratégie *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="d14ba-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="d14ba-229">Profils techniques pour Facebook</span><span class="sxs-lookup"><span data-stu-id="d14ba-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="d14ba-230">Profil technique</span><span class="sxs-lookup"><span data-stu-id="d14ba-230">Technical profile</span></span> | <span data-ttu-id="d14ba-231">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d14ba-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="d14ba-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="d14ba-233">Profils techniques pour Local Account Signin</span><span class="sxs-lookup"><span data-stu-id="d14ba-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="d14ba-234">Profil technique</span><span class="sxs-lookup"><span data-stu-id="d14ba-234">Technical profile</span></span> | <span data-ttu-id="d14ba-235">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d14ba-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="d14ba-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="d14ba-237">Profils techniques pour PhoneFactor</span><span class="sxs-lookup"><span data-stu-id="d14ba-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="d14ba-238">Profil technique</span><span class="sxs-lookup"><span data-stu-id="d14ba-238">Technical profile</span></span> | <span data-ttu-id="d14ba-239">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d14ba-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="d14ba-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="d14ba-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="d14ba-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="d14ba-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="d14ba-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="d14ba-243">Profils techniques pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d14ba-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="d14ba-244">Profil technique</span><span class="sxs-lookup"><span data-stu-id="d14ba-244">Technical profile</span></span> | <span data-ttu-id="d14ba-245">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d14ba-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="d14ba-246">*AAD-Common*</span></span> | <span data-ttu-id="d14ba-247">Profil technique contenu dans les autres profils techniques AAD-xxx</span><span class="sxs-lookup"><span data-stu-id="d14ba-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="d14ba-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="d14ba-249">Profil technique pour les connexions via les réseaux sociaux</span><span class="sxs-lookup"><span data-stu-id="d14ba-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="d14ba-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="d14ba-251">Profil technique pour les connexions via les réseaux sociaux</span><span class="sxs-lookup"><span data-stu-id="d14ba-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="d14ba-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="d14ba-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="d14ba-253">Profil technique pour les connexions via les réseaux sociaux</span><span class="sxs-lookup"><span data-stu-id="d14ba-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="d14ba-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="d14ba-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="d14ba-255">Profils techniques pour les comptes locaux</span><span class="sxs-lookup"><span data-stu-id="d14ba-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="d14ba-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="d14ba-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="d14ba-257">Profils techniques pour les comptes locaux</span><span class="sxs-lookup"><span data-stu-id="d14ba-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="d14ba-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="d14ba-259">Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet</span><span class="sxs-lookup"><span data-stu-id="d14ba-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="d14ba-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="d14ba-261">Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet</span><span class="sxs-lookup"><span data-stu-id="d14ba-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="d14ba-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="d14ba-263">Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet</span><span class="sxs-lookup"><span data-stu-id="d14ba-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="d14ba-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="d14ba-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="d14ba-265">Profil technique utilisé pour lire les données une fois que l’utilisateur s’est authentifié</span><span class="sxs-lookup"><span data-stu-id="d14ba-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="d14ba-266">Profils techniques pour Self Asserted</span><span class="sxs-lookup"><span data-stu-id="d14ba-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="d14ba-267">Profil technique</span><span class="sxs-lookup"><span data-stu-id="d14ba-267">Technical profile</span></span> | <span data-ttu-id="d14ba-268">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d14ba-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="d14ba-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="d14ba-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="d14ba-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="d14ba-271">Profils techniques pour Local Account</span><span class="sxs-lookup"><span data-stu-id="d14ba-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="d14ba-272">Profil technique</span><span class="sxs-lookup"><span data-stu-id="d14ba-272">Technical profile</span></span> | <span data-ttu-id="d14ba-273">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d14ba-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="d14ba-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="d14ba-275">Profils techniques pour Session Management</span><span class="sxs-lookup"><span data-stu-id="d14ba-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="d14ba-276">Profil technique</span><span class="sxs-lookup"><span data-stu-id="d14ba-276">Technical profile</span></span> | <span data-ttu-id="d14ba-277">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d14ba-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="d14ba-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="d14ba-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="d14ba-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="d14ba-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="d14ba-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="d14ba-281">Nom de profil utilisé pour enlever toute ambiguïté entre l’inscription et la connexion de la session AAD</span><span class="sxs-lookup"><span data-stu-id="d14ba-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="d14ba-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="d14ba-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="d14ba-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="d14ba-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="d14ba-284">Profils techniques pour Trustframework Policy Engine TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="d14ba-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="d14ba-285">Aucun profil technique n’est actuellement défini pour le fournisseur de revendications **Trustframework Policy Engine TechnicalProfiles**.</span><span class="sxs-lookup"><span data-stu-id="d14ba-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="d14ba-286">Profils techniques pour Token Issuer</span><span class="sxs-lookup"><span data-stu-id="d14ba-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="d14ba-287">Profil technique</span><span class="sxs-lookup"><span data-stu-id="d14ba-287">Technical profile</span></span> | <span data-ttu-id="d14ba-288">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="d14ba-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="d14ba-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="d14ba-290">Parcours utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-290">User journeys</span></span>

<span data-ttu-id="d14ba-291">Cette section décrit les parcours utilisateur déjà déclarés dans la stratégie *B2C_1A_base*.</span><span class="sxs-lookup"><span data-stu-id="d14ba-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="d14ba-292">Ces parcours utilisateur peuvent être référencés, remplacés et/ou étendus autant que nécessaire dans vos propres stratégies, ainsi que dans la stratégie *B2C_1A_base_extensions*.</span><span class="sxs-lookup"><span data-stu-id="d14ba-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="d14ba-293">Parcours utilisateur</span><span class="sxs-lookup"><span data-stu-id="d14ba-293">User journey</span></span> | <span data-ttu-id="d14ba-294">Description</span><span class="sxs-lookup"><span data-stu-id="d14ba-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="d14ba-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="d14ba-295">*SignUp*</span></span> | |
| <span data-ttu-id="d14ba-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="d14ba-296">*SignIn*</span></span> | |
| <span data-ttu-id="d14ba-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="d14ba-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="d14ba-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="d14ba-298">*EditProfile*</span></span> | |
| <span data-ttu-id="d14ba-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="d14ba-299">*PasswordReset*</span></span> | |
