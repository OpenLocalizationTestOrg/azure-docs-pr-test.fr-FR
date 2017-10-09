---
title: "Azure B2C Active Directory : Présentation des stratégies personnalisées de pack de démarrage hello | Documents Microsoft"
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
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="540ef-103">Fonctionnement des stratégies personnalisées hello de pack de démarrage de stratégie personnalisée hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="540ef-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="540ef-104">Cette section répertorie tous les éléments de base hello de stratégie hello B2C_1A_base fourni avec hello **Starter Pack** et qui est utilisé pour la création de vos propres stratégies via l’héritage hello Hello *B2C_1A_base_ stratégie d’extensions*.</span><span class="sxs-lookup"><span data-stu-id="540ef-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="540ef-105">Par conséquent, il plus particulièrement axé sur hello déjà défini les types, les transformations de revendications, définitions de contenu, les fournisseurs de revendications avec leurs profils techniques de revendication et hello trajets d’utilisateur de base.</span><span class="sxs-lookup"><span data-stu-id="540ef-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="540ef-106">Microsoft n’apporte aucune garantie, expresse ou implicite, avec les informations de toohello égard fournies ci-après.</span><span class="sxs-lookup"><span data-stu-id="540ef-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="540ef-107">Des modifications peuvent être apportées à tout moment, avant, pendant ou après la mise à la disposition générale.</span><span class="sxs-lookup"><span data-stu-id="540ef-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="540ef-108">Vos propres stratégies et les hello B2C_1A_base_extensions stratégie peuvent remplacer ces définitions et étendre cette stratégie parent en fournissant de nouvelles en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="540ef-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="540ef-109">Hello principaux éléments de hello *B2C_1A_base stratégie* sont des types de revendications, les transformations de revendications et des définitions de contenu.</span><span class="sxs-lookup"><span data-stu-id="540ef-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="540ef-110">Ces éléments peuvent toobe susceptibles d’être référencé dans vos propres stratégies ainsi que dans hello *B2C_1A_base_extensions stratégie*.</span><span class="sxs-lookup"><span data-stu-id="540ef-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="540ef-111">Schéma de revendications</span><span class="sxs-lookup"><span data-stu-id="540ef-111">Claims schemas</span></span>

<span data-ttu-id="540ef-112">Ce schéma de revendications comprend trois sections :</span><span class="sxs-lookup"><span data-stu-id="540ef-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="540ef-113">Première section qui répertorie les revendications minimale hello qui sont requises pour hello utilisateur trajets toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="540ef-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="540ef-114">Une deuxième section que listes hello revendications requises pour les paramètres de chaîne de requête et autres toobe paramètres spéciaux passé tooother les fournisseurs de revendications, notamment login.microsoftonline.com pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="540ef-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="540ef-115">**Ne modifiez pas ces revendications**.</span><span class="sxs-lookup"><span data-stu-id="540ef-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="540ef-116">Et finit par une troisième section qui répertorie toutes les revendications supplémentaires, facultatifs qui peuvent être collectées à partir de l’utilisateur de hello, stocké dans le répertoire de hello et envoyés dans les jetons lors de l’authentification dans.</span><span class="sxs-lookup"><span data-stu-id="540ef-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="540ef-117">Nouvelles revendications type toobe collectées à partir de l’utilisateur de hello et/ou envoyées dans le jeton de hello peuvent être ajoutées dans cette section.</span><span class="sxs-lookup"><span data-stu-id="540ef-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="540ef-118">schéma de revendications Hello contient des restrictions sur certaines revendications telles que les noms d’utilisateur et mots de passe.</span><span class="sxs-lookup"><span data-stu-id="540ef-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="540ef-119">Hello stratégie d’approbation d’infrastructure (TF) traite Azure AD comme tout autre fournisseur de revendications et tous ses restrictions sont modélisées dans la stratégie de premium hello.</span><span class="sxs-lookup"><span data-stu-id="540ef-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="540ef-120">Une stratégie peut être modifiée tooadd plus de restrictions, ou utiliser un autre fournisseur de revendications pour le stockage d’informations d’identification qui disposera de ses propres restrictions.</span><span class="sxs-lookup"><span data-stu-id="540ef-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="540ef-121">types de revendications disponibles Hello sont répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="540ef-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="540ef-122">Revendications qui sont requises pour les déplacements des utilisateurs hello</span><span class="sxs-lookup"><span data-stu-id="540ef-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="540ef-123">Hello suivant les revendications est requise pour utilisateur trajets toowork correctement :</span><span class="sxs-lookup"><span data-stu-id="540ef-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="540ef-124">Type de revendication</span><span class="sxs-lookup"><span data-stu-id="540ef-124">Claims type</span></span> | <span data-ttu-id="540ef-125">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="540ef-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="540ef-126">*UserId*</span></span> | <span data-ttu-id="540ef-127">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="540ef-127">Username</span></span> |
| <span data-ttu-id="540ef-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="540ef-128">*signInName*</span></span> | <span data-ttu-id="540ef-129">Nom de connexion</span><span class="sxs-lookup"><span data-stu-id="540ef-129">Sign in name</span></span> |
| <span data-ttu-id="540ef-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="540ef-130">*tenantId*</span></span> | <span data-ttu-id="540ef-131">Identificateur de client (ID) d’objet utilisateur hello Premium d’Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="540ef-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="540ef-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="540ef-132">*objectId*</span></span> | <span data-ttu-id="540ef-133">Identificateur d’objet (ID) de l’objet utilisateur hello Premium d’Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="540ef-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="540ef-134">*mot de passe*</span><span class="sxs-lookup"><span data-stu-id="540ef-134">*password*</span></span> | <span data-ttu-id="540ef-135">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="540ef-135">Password</span></span> |
| <span data-ttu-id="540ef-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="540ef-136">*newPassword*</span></span> | |
| <span data-ttu-id="540ef-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="540ef-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="540ef-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="540ef-138">*passwordPolicies*</span></span> | <span data-ttu-id="540ef-139">Stratégies de mot de passe utilisés par la longueur de mot de passe toodetermine Premium d’Azure AD B2C, expiration, etc..</span><span class="sxs-lookup"><span data-stu-id="540ef-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="540ef-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="540ef-140">*sub*</span></span> | |
| <span data-ttu-id="540ef-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="540ef-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="540ef-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="540ef-142">*identityProvider*</span></span> | |
| <span data-ttu-id="540ef-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="540ef-143">*displayName*</span></span> | |
| <span data-ttu-id="540ef-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="540ef-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="540ef-145">Numéro de téléphone de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="540ef-145">User's telephone number</span></span> |
| <span data-ttu-id="540ef-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="540ef-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="540ef-147">*email*</span><span class="sxs-lookup"><span data-stu-id="540ef-147">*email*</span></span> | <span data-ttu-id="540ef-148">Adresse de messagerie qui peut être utilisé toocontact hello utilisateur</span><span class="sxs-lookup"><span data-stu-id="540ef-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="540ef-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="540ef-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="540ef-150">Adresse de messagerie hello utilisateur peut utiliser toosign dans</span><span class="sxs-lookup"><span data-stu-id="540ef-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="540ef-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="540ef-151">*otherMails*</span></span> | <span data-ttu-id="540ef-152">Adresses de messagerie qui peuvent être utilisé toocontact hello utilisateur</span><span class="sxs-lookup"><span data-stu-id="540ef-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="540ef-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="540ef-153">*userPrincipalName*</span></span> | <span data-ttu-id="540ef-154">Nom d’utilisateur, tel que stocké dans hello Premium d’Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="540ef-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="540ef-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="540ef-155">*upnUserName*</span></span> | <span data-ttu-id="540ef-156">Nom d’utilisateur utilisé pour créer le nom d’utilisateur principal</span><span class="sxs-lookup"><span data-stu-id="540ef-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="540ef-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="540ef-157">*mailNickName*</span></span> | <span data-ttu-id="540ef-158">Nom d’utilisateur messagerie nick stocké dans hello Premium d’Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="540ef-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="540ef-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="540ef-159">*newUser*</span></span> | |
| <span data-ttu-id="540ef-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="540ef-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="540ef-161">Revendication qui spécifie si les attributs ont été collectées à partir de l’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="540ef-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="540ef-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="540ef-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="540ef-163">Revendication qui spécifie si un nouveau numéro de téléphone a été collecté à partir de l’utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="540ef-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="540ef-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="540ef-164">*authenticationSource*</span></span> | <span data-ttu-id="540ef-165">Spécifie si l’utilisateur de hello a été authentifié au fournisseur d’identité sociaux, login.microsoftonline.com ou compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="540ef-166">Revendications requises pour les paramètres de chaîne de requête et d’autres paramètres spéciaux</span><span class="sxs-lookup"><span data-stu-id="540ef-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="540ef-167">Hello revendications suivantes sont requises toopass sur les fournisseurs de revendications tooother paramètres spéciaux (y compris certains paramètres de chaîne de requête) :</span><span class="sxs-lookup"><span data-stu-id="540ef-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="540ef-168">Type de revendication</span><span class="sxs-lookup"><span data-stu-id="540ef-168">Claims type</span></span> | <span data-ttu-id="540ef-169">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="540ef-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="540ef-170">*nux*</span></span> | <span data-ttu-id="540ef-171">Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="540ef-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="540ef-172">*nca*</span></span> | <span data-ttu-id="540ef-173">Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="540ef-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="540ef-174">*prompt*</span></span> | <span data-ttu-id="540ef-175">Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="540ef-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="540ef-176">*mkt*</span></span> | <span data-ttu-id="540ef-177">Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="540ef-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="540ef-178">*lc*</span></span> | <span data-ttu-id="540ef-179">Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="540ef-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="540ef-180">*grant_type*</span></span> | <span data-ttu-id="540ef-181">Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="540ef-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="540ef-182">*scope*</span></span> | <span data-ttu-id="540ef-183">Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="540ef-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="540ef-184">*client_id*</span></span> | <span data-ttu-id="540ef-185">Spéciaux passés pour toologin.microsoftonline.com de l’authentification de compte local</span><span class="sxs-lookup"><span data-stu-id="540ef-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="540ef-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="540ef-186">*objectIdFromSession*</span></span> | <span data-ttu-id="540ef-187">Paramètre fourni par hello par défaut session gestion fournisseur tooindicate qui hello id d’objet a été récupéré à partir d’une session de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="540ef-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="540ef-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="540ef-188">*isActiveMFASession*</span></span> | <span data-ttu-id="540ef-189">Paramètre fourni par tooindicate de gestion de session de l’authentification Multifacteur hello que cet utilisateur hello a une session active de l’authentification Multifacteur</span><span class="sxs-lookup"><span data-stu-id="540ef-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="540ef-190">Revendications supplémentaires (facultatives) qui peuvent être collectées</span><span class="sxs-lookup"><span data-stu-id="540ef-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="540ef-191">suivant de Hello revendications sont des revendications supplémentaires qui peuvent être collectées auprès des utilisateurs de hello, stocké dans le répertoire de hello et envoyé dans le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="540ef-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="540ef-192">Comme avant, des revendications supplémentaires peuvent être ajoutées toothis liste.</span><span class="sxs-lookup"><span data-stu-id="540ef-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="540ef-193">Type de revendication</span><span class="sxs-lookup"><span data-stu-id="540ef-193">Claims type</span></span> | <span data-ttu-id="540ef-194">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="540ef-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="540ef-195">*givenName*</span></span> | <span data-ttu-id="540ef-196">Prénom de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="540ef-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="540ef-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="540ef-197">*surname*</span></span> | <span data-ttu-id="540ef-198">Nom de famille de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="540ef-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="540ef-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="540ef-199">*Extension_picture*</span></span> | <span data-ttu-id="540ef-200">Image de l’utilisateur obtenue via les réseaux sociaux</span><span class="sxs-lookup"><span data-stu-id="540ef-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="540ef-201">Transformations de revendication</span><span class="sxs-lookup"><span data-stu-id="540ef-201">Claim transformations</span></span>

<span data-ttu-id="540ef-202">transformations de revendications disponibles Hello sont répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="540ef-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="540ef-203">Transformation de revendication</span><span class="sxs-lookup"><span data-stu-id="540ef-203">Claim transformation</span></span> | <span data-ttu-id="540ef-204">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="540ef-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="540ef-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="540ef-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="540ef-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="540ef-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="540ef-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="540ef-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="540ef-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="540ef-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="540ef-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="540ef-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="540ef-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="540ef-211">Définitions de contenu</span><span class="sxs-lookup"><span data-stu-id="540ef-211">Content definitions</span></span>

<span data-ttu-id="540ef-212">Cette section décrit les définitions de contenu hello déjà déclarées dans hello *B2C_1A_base* stratégie.</span><span class="sxs-lookup"><span data-stu-id="540ef-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="540ef-213">Ces définitions de contenu sont susceptibles d’être toobe référencé, substitution et/ou étendue autant que nécessaire dans vos propres stratégies ainsi que dans hello *B2C_1A_base_extensions* stratégie.</span><span class="sxs-lookup"><span data-stu-id="540ef-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="540ef-214">Fournisseur de revendications</span><span class="sxs-lookup"><span data-stu-id="540ef-214">Claims provider</span></span> | <span data-ttu-id="540ef-215">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="540ef-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="540ef-216">*Facebook*</span></span> | |
| <span data-ttu-id="540ef-217">*Local Account SignIn*</span><span class="sxs-lookup"><span data-stu-id="540ef-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="540ef-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="540ef-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="540ef-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="540ef-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="540ef-220">*Self Asserted*</span><span class="sxs-lookup"><span data-stu-id="540ef-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="540ef-221">*Local Account*</span><span class="sxs-lookup"><span data-stu-id="540ef-221">*Local Account*</span></span> | |
| <span data-ttu-id="540ef-222">*Gestion des sessions*</span><span class="sxs-lookup"><span data-stu-id="540ef-222">*Session Management*</span></span> | |
| <span data-ttu-id="540ef-223">*Trustframework Policy Engine*</span><span class="sxs-lookup"><span data-stu-id="540ef-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="540ef-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="540ef-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="540ef-225">*Token Issuer*</span><span class="sxs-lookup"><span data-stu-id="540ef-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="540ef-226">Profils techniques</span><span class="sxs-lookup"><span data-stu-id="540ef-226">Technical profiles</span></span>

<span data-ttu-id="540ef-227">Cette section décrit les profils techniques hello déjà déclarés par le fournisseur de revendications Bonjour *B2C_1A_base* stratégie.</span><span class="sxs-lookup"><span data-stu-id="540ef-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="540ef-228">Ces profils techniques sont susceptibles d’être toobe plus référencée, substitution et/ou étendue autant que nécessaire dans vos propres stratégies ainsi que dans hello *B2C_1A_base_extensions* stratégie.</span><span class="sxs-lookup"><span data-stu-id="540ef-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="540ef-229">Profils techniques pour Facebook</span><span class="sxs-lookup"><span data-stu-id="540ef-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="540ef-230">Profil technique</span><span class="sxs-lookup"><span data-stu-id="540ef-230">Technical profile</span></span> | <span data-ttu-id="540ef-231">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="540ef-232">*Facebook-OAUTH*</span><span class="sxs-lookup"><span data-stu-id="540ef-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="540ef-233">Profils techniques pour Local Account Signin</span><span class="sxs-lookup"><span data-stu-id="540ef-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="540ef-234">Profil technique</span><span class="sxs-lookup"><span data-stu-id="540ef-234">Technical profile</span></span> | <span data-ttu-id="540ef-235">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="540ef-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="540ef-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="540ef-237">Profils techniques pour PhoneFactor</span><span class="sxs-lookup"><span data-stu-id="540ef-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="540ef-238">Profil technique</span><span class="sxs-lookup"><span data-stu-id="540ef-238">Technical profile</span></span> | <span data-ttu-id="540ef-239">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="540ef-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="540ef-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="540ef-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="540ef-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="540ef-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="540ef-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="540ef-243">Profils techniques pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="540ef-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="540ef-244">Profil technique</span><span class="sxs-lookup"><span data-stu-id="540ef-244">Technical profile</span></span> | <span data-ttu-id="540ef-245">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="540ef-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="540ef-246">*AAD-Common*</span></span> | <span data-ttu-id="540ef-247">Profil technique inclus par hello autres profils techniques AAD-xxx</span><span class="sxs-lookup"><span data-stu-id="540ef-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="540ef-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="540ef-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="540ef-249">Profil technique pour les connexions via les réseaux sociaux</span><span class="sxs-lookup"><span data-stu-id="540ef-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="540ef-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="540ef-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="540ef-251">Profil technique pour les connexions via les réseaux sociaux</span><span class="sxs-lookup"><span data-stu-id="540ef-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="540ef-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="540ef-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="540ef-253">Profil technique pour les connexions via les réseaux sociaux</span><span class="sxs-lookup"><span data-stu-id="540ef-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="540ef-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="540ef-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="540ef-255">Profils techniques pour les comptes locaux</span><span class="sxs-lookup"><span data-stu-id="540ef-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="540ef-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="540ef-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="540ef-257">Profils techniques pour les comptes locaux</span><span class="sxs-lookup"><span data-stu-id="540ef-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="540ef-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="540ef-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="540ef-259">Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet</span><span class="sxs-lookup"><span data-stu-id="540ef-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="540ef-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="540ef-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="540ef-261">Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet</span><span class="sxs-lookup"><span data-stu-id="540ef-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="540ef-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="540ef-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="540ef-263">Profil technique pour la mise à jour de l’enregistrement utilisateur à l’aide de l’ID d’objet</span><span class="sxs-lookup"><span data-stu-id="540ef-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="540ef-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="540ef-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="540ef-265">Profil technique donnée tooread utilisée une fois que l’utilisateur s’authentifie</span><span class="sxs-lookup"><span data-stu-id="540ef-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="540ef-266">Profils techniques pour Self Asserted</span><span class="sxs-lookup"><span data-stu-id="540ef-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="540ef-267">Profil technique</span><span class="sxs-lookup"><span data-stu-id="540ef-267">Technical profile</span></span> | <span data-ttu-id="540ef-268">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="540ef-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="540ef-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="540ef-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="540ef-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="540ef-271">Profils techniques pour Local Account</span><span class="sxs-lookup"><span data-stu-id="540ef-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="540ef-272">Profil technique</span><span class="sxs-lookup"><span data-stu-id="540ef-272">Technical profile</span></span> | <span data-ttu-id="540ef-273">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="540ef-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="540ef-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="540ef-275">Profils techniques pour Session Management</span><span class="sxs-lookup"><span data-stu-id="540ef-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="540ef-276">Profil technique</span><span class="sxs-lookup"><span data-stu-id="540ef-276">Technical profile</span></span> | <span data-ttu-id="540ef-277">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="540ef-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="540ef-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="540ef-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="540ef-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="540ef-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="540ef-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="540ef-281">Nom du profil est en cours de la session d’AAD toodisambiguate utilisé entre le signe des et se connecter</span><span class="sxs-lookup"><span data-stu-id="540ef-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="540ef-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="540ef-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="540ef-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="540ef-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="540ef-284">Profils techniques pour Trustframework Policy Engine TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="540ef-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="540ef-285">Actuellement, aucun profil technique n’est définis pour hello **Trustframework stratégie moteur TechnicalProfiles** fournisseur de revendications.</span><span class="sxs-lookup"><span data-stu-id="540ef-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="540ef-286">Profils techniques pour Token Issuer</span><span class="sxs-lookup"><span data-stu-id="540ef-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="540ef-287">Profil technique</span><span class="sxs-lookup"><span data-stu-id="540ef-287">Technical profile</span></span> | <span data-ttu-id="540ef-288">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="540ef-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="540ef-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="540ef-290">Parcours utilisateur</span><span class="sxs-lookup"><span data-stu-id="540ef-290">User journeys</span></span>

<span data-ttu-id="540ef-291">Cette section décrit le parcours d’utilisateur hello déjà déclarés dans hello *B2C_1A_base* stratégie.</span><span class="sxs-lookup"><span data-stu-id="540ef-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="540ef-292">Ces parcours de l’utilisateur sont susceptibles d’être toobe plus référencée, substitution et/ou étendue autant que nécessaire dans vos propres stratégies ainsi que dans hello *B2C_1A_base_extensions* stratégie.</span><span class="sxs-lookup"><span data-stu-id="540ef-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="540ef-293">Parcours utilisateur</span><span class="sxs-lookup"><span data-stu-id="540ef-293">User journey</span></span> | <span data-ttu-id="540ef-294">Description</span><span class="sxs-lookup"><span data-stu-id="540ef-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="540ef-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="540ef-295">*SignUp*</span></span> | |
| <span data-ttu-id="540ef-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="540ef-296">*SignIn*</span></span> | |
| <span data-ttu-id="540ef-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="540ef-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="540ef-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="540ef-298">*EditProfile*</span></span> | |
| <span data-ttu-id="540ef-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="540ef-299">*PasswordReset*</span></span> | |
