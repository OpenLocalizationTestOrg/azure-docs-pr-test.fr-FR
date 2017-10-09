---
title: "aaaSession de gestion - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "mesures d’atténuation des menaces exposé Bonjour outil de modélisation des menaces"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="b91c6-103">Infrastructure de sécurité : gestion des sessions | Articles</span><span class="sxs-lookup"><span data-stu-id="b91c6-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="b91c6-104">Produit/service</span><span class="sxs-lookup"><span data-stu-id="b91c6-104">Product/Service</span></span> | <span data-ttu-id="b91c6-105">Article</span><span class="sxs-lookup"><span data-stu-id="b91c6-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="b91c6-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="b91c6-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="b91c6-107">Implémenter une déconnexion appropriée à l’aide de méthodes ADAL lors de l’utilisation d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91c6-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="b91c6-108">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="b91c6-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="b91c6-109">Utiliser des durées de vie limitées pour les jetons SaS générés</span><span class="sxs-lookup"><span data-stu-id="b91c6-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="b91c6-110">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="b91c6-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="b91c6-111">Utiliser des durées de vie de jeton minimales pour les jetons de ressource générés</span><span class="sxs-lookup"><span data-stu-id="b91c6-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="b91c6-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="b91c6-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="b91c6-113">Implémenter une déconnexion appropriée à l’aide de méthodes WsFederation lors de l’utilisation d’ADFS</span><span class="sxs-lookup"><span data-stu-id="b91c6-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="b91c6-114">**IdentityServer**</span><span class="sxs-lookup"><span data-stu-id="b91c6-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="b91c6-115">Implémenter une déconnexion appropriée lors de l’utilisation d’IdentityServer</span><span class="sxs-lookup"><span data-stu-id="b91c6-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="b91c6-116">**Application web**</span><span class="sxs-lookup"><span data-stu-id="b91c6-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="b91c6-117">Utilisation requise de cookies sécurisés par les applications disponibles par le biais de HTTPS</span><span class="sxs-lookup"><span data-stu-id="b91c6-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="b91c6-118">Élément httpOnly requis dans la définition des cookies pour toutes les applications basées sur HTTP</span><span class="sxs-lookup"><span data-stu-id="b91c6-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="b91c6-119">Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les pages web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b91c6-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="b91c6-120">Configurer la durée de vie d’inactivité d’une session</span><span class="sxs-lookup"><span data-stu-id="b91c6-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="b91c6-121">Implémenter la déconnexion appropriée à partir de l’application hello</span><span class="sxs-lookup"><span data-stu-id="b91c6-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="b91c6-122">**API Web**</span><span class="sxs-lookup"><span data-stu-id="b91c6-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="b91c6-123">Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b91c6-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="b91c6-124"><a id="logout-adal"></a>Implémenter une déconnexion appropriée à l’aide de méthodes ADAL lors de l’utilisation d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91c6-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="b91c6-125">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-125">Title</span></span>                   | <span data-ttu-id="b91c6-126">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-127">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-127">**Component**</span></span>               | <span data-ttu-id="b91c6-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91c6-128">Azure AD</span></span> | 
| <span data-ttu-id="b91c6-129">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-129">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-130">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-130">Build</span></span> |  
| <span data-ttu-id="b91c6-131">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-131">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-132">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-132">Generic</span></span> |
| <span data-ttu-id="b91c6-133">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-133">**Attributes**</span></span>              | <span data-ttu-id="b91c6-134">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-134">N/A</span></span>  |
| <span data-ttu-id="b91c6-135">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-135">**References**</span></span>              | <span data-ttu-id="b91c6-136">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-136">N/A</span></span>  |
| <span data-ttu-id="b91c6-137">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-137">**Steps**</span></span> | <span data-ttu-id="b91c6-138">Si l’application hello s’appuie sur le jeton d’accès émis par Azure AD, le Gestionnaire d’événements déconnexion hello doit appeler</span><span class="sxs-lookup"><span data-stu-id="b91c6-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="b91c6-139">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="b91c6-140">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-140">Example</span></span>
<span data-ttu-id="b91c6-141">Il est également nécessaire de détruire la session de l’utilisateur en appelant la méthode Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="b91c6-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="b91c6-142">La méthode ci-après présente une implémentation sécurisée de la déconnexion d’un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="b91c6-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="b91c6-143"><a id="finite-tokens"></a>Utiliser des durées de vie limitées pour les jetons SaS générés</span><span class="sxs-lookup"><span data-stu-id="b91c6-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="b91c6-144">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-144">Title</span></span>                   | <span data-ttu-id="b91c6-145">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-146">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-146">**Component**</span></span>               | <span data-ttu-id="b91c6-147">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="b91c6-147">IoT Device</span></span> | 
| <span data-ttu-id="b91c6-148">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-148">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-149">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-149">Build</span></span> |  
| <span data-ttu-id="b91c6-150">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-150">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-151">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-151">Generic</span></span> |
| <span data-ttu-id="b91c6-152">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-152">**Attributes**</span></span>              | <span data-ttu-id="b91c6-153">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-153">N/A</span></span>  |
| <span data-ttu-id="b91c6-154">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-154">**References**</span></span>              | <span data-ttu-id="b91c6-155">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-155">N/A</span></span>  |
| <span data-ttu-id="b91c6-156">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-156">**Steps**</span></span> | <span data-ttu-id="b91c6-157">Jetons SAP générés pour l’authentification tooAzure IoT Hub doivent avoir une période d’expiration finie.</span><span class="sxs-lookup"><span data-stu-id="b91c6-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="b91c6-158">Conserver hello SaS durées de vie de jeton tooa toolimit minimale hello durée qu’ils peuvent être relues dans le cas où les jetons hello sont compromis.</span><span class="sxs-lookup"><span data-stu-id="b91c6-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="b91c6-159"><a id="resource-tokens"></a>Utiliser des durées de vie de jeton minimales pour les jetons de ressource générés</span><span class="sxs-lookup"><span data-stu-id="b91c6-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="b91c6-160">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-160">Title</span></span>                   | <span data-ttu-id="b91c6-161">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-162">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-162">**Component**</span></span>               | <span data-ttu-id="b91c6-163">Azure Document DB</span><span class="sxs-lookup"><span data-stu-id="b91c6-163">Azure Document DB</span></span> | 
| <span data-ttu-id="b91c6-164">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-164">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-165">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-165">Build</span></span> |  
| <span data-ttu-id="b91c6-166">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-166">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-167">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-167">Generic</span></span> |
| <span data-ttu-id="b91c6-168">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-168">**Attributes**</span></span>              | <span data-ttu-id="b91c6-169">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-169">N/A</span></span>  |
| <span data-ttu-id="b91c6-170">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-170">**References**</span></span>              | <span data-ttu-id="b91c6-171">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-171">N/A</span></span>  |
| <span data-ttu-id="b91c6-172">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-172">**Steps**</span></span> | <span data-ttu-id="b91c6-173">Réduire timespan hello de valeur minimale du jeton tooa ressource requise.</span><span class="sxs-lookup"><span data-stu-id="b91c6-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="b91c6-174">Les jetons de ressource ont une durée de validité par défaut d'une heure.</span><span class="sxs-lookup"><span data-stu-id="b91c6-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="b91c6-175"><a id="wsfederation-logout"></a>Implémenter une déconnexion appropriée à l’aide de méthodes WsFederation lors de l’utilisation d’ADFS</span><span class="sxs-lookup"><span data-stu-id="b91c6-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="b91c6-176">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-176">Title</span></span>                   | <span data-ttu-id="b91c6-177">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-178">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-178">**Component**</span></span>               | <span data-ttu-id="b91c6-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="b91c6-179">ADFS</span></span> | 
| <span data-ttu-id="b91c6-180">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-180">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-181">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-181">Build</span></span> |  
| <span data-ttu-id="b91c6-182">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-182">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-183">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-183">Generic</span></span> |
| <span data-ttu-id="b91c6-184">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-184">**Attributes**</span></span>              | <span data-ttu-id="b91c6-185">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-185">N/A</span></span>  |
| <span data-ttu-id="b91c6-186">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-186">**References**</span></span>              | <span data-ttu-id="b91c6-187">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-187">N/A</span></span>  |
| <span data-ttu-id="b91c6-188">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-188">**Steps**</span></span> | <span data-ttu-id="b91c6-189">Si l’application hello s’appuie sur le jeton STS émis par ADFS, le Gestionnaire d’événements déconnexion hello doit appeler toolog de méthode WSFederationAuthenticationModule.FederatedSignOut() utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="b91c6-190">Également hello session en cours doit être détruit, et la valeur du jeton de session hello doit être réinitialisé et annulé.</span><span class="sxs-lookup"><span data-stu-id="b91c6-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="b91c6-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="b91c6-192"><a id="proper-logout"></a>Implémenter une déconnexion appropriée lors de l’utilisation d’IdentityServer</span><span class="sxs-lookup"><span data-stu-id="b91c6-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="b91c6-193">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-193">Title</span></span>                   | <span data-ttu-id="b91c6-194">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-195">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-195">**Component**</span></span>               | <span data-ttu-id="b91c6-196">IdentityServer</span><span class="sxs-lookup"><span data-stu-id="b91c6-196">Identity Server</span></span> | 
| <span data-ttu-id="b91c6-197">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-197">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-198">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-198">Build</span></span> |  
| <span data-ttu-id="b91c6-199">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-199">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-200">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-200">Generic</span></span> |
| <span data-ttu-id="b91c6-201">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-201">**Attributes**</span></span>              | <span data-ttu-id="b91c6-202">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-202">N/A</span></span>  |
| <span data-ttu-id="b91c6-203">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-203">**References**</span></span>              | [<span data-ttu-id="b91c6-204">IdentityServer3-Federated sign out</span><span class="sxs-lookup"><span data-stu-id="b91c6-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="b91c6-205">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-205">**Steps**</span></span> | <span data-ttu-id="b91c6-206">IdentityServer prend en charge toofederate de capacité hello aux fournisseurs d’identité externe.</span><span class="sxs-lookup"><span data-stu-id="b91c6-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="b91c6-207">Quand un utilisateur se déconnecte un fournisseur d’identité en amont, en fonction de protocole hello utilisé, il peut être possible tooreceive une notification lorsque hello utilisateur se déconnecte. Il permet de toonotify IdentityServer ses clients afin qu’ils peuvent également se connecter hello utilisateur out. Consultez la documentation de hello dans la section des références hello pour les détails d’implémentation hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="b91c6-208"><a id="https-secure-cookies"></a>Utilisation requise de cookies sécurisés par les applications disponibles par le biais de HTTPS</span><span class="sxs-lookup"><span data-stu-id="b91c6-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="b91c6-209">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-209">Title</span></span>                   | <span data-ttu-id="b91c6-210">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-211">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-211">**Component**</span></span>               | <span data-ttu-id="b91c6-212">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-212">Web Application</span></span> | 
| <span data-ttu-id="b91c6-213">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-213">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-214">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-214">Build</span></span> |  
| <span data-ttu-id="b91c6-215">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-215">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-216">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-216">Generic</span></span> |
| <span data-ttu-id="b91c6-217">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-217">**Attributes**</span></span>              | <span data-ttu-id="b91c6-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="b91c6-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="b91c6-219">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-219">**References**</span></span>              | <span data-ttu-id="b91c6-220">[httpCookies, élément (Schéma des paramètres ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property (Propriété HttpCookie.Secure)](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="b91c6-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="b91c6-221">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-221">**Steps**</span></span> | <span data-ttu-id="b91c6-222">Les cookies sont normalement uniquement accessible toohello domaine pour lequel ils ont été limités.</span><span class="sxs-lookup"><span data-stu-id="b91c6-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="b91c6-223">Malheureusement, définition hello de « domaine » n’inclut pas de protocole de hello les cookies qui sont créés via le protocole HTTPS sont accessibles via HTTP.</span><span class="sxs-lookup"><span data-stu-id="b91c6-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="b91c6-224">attribut de « sécurisées » Hello indique navigateur toohello hello cookie doit uniquement être rendue disponible via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b91c6-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="b91c6-225">Assurez-vous que tous les cookies définis sur HTTPS utilisent hello **sécurisé** attribut.</span><span class="sxs-lookup"><span data-stu-id="b91c6-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="b91c6-226">spécification de Hello peut être appliquée dans le fichier web.config de hello en définissant hello requireSSL attribut tootrue.</span><span class="sxs-lookup"><span data-stu-id="b91c6-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="b91c6-227">Il s’agit de hello préféré approche, car il appliquera hello **sécurisé** d’attribut pour tous les cookies actuels et futurs sans hello besoin toomake toutes les modifications de code supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="b91c6-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="b91c6-228">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="b91c6-229">paramètre de Hello est appliquée même si HTTP est utilisé tooaccess hello application.</span><span class="sxs-lookup"><span data-stu-id="b91c6-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="b91c6-230">Si le protocole HTTP est utilisé tooaccess hello application, de hello sauts paramètre application hello parce que les cookies de hello sont définies avec le navigateur hello attribut et hello sécurisé n’envoie pas les toohello application.</span><span class="sxs-lookup"><span data-stu-id="b91c6-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="b91c6-231">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-231">Title</span></span>                   | <span data-ttu-id="b91c6-232">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-233">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-233">**Component**</span></span>               | <span data-ttu-id="b91c6-234">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-234">Web Application</span></span> | 
| <span data-ttu-id="b91c6-235">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-235">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-236">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-236">Build</span></span> |  
| <span data-ttu-id="b91c6-237">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-237">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-238">Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="b91c6-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="b91c6-239">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-239">**Attributes**</span></span>              | <span data-ttu-id="b91c6-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="b91c6-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="b91c6-241">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-241">**References**</span></span>              | <span data-ttu-id="b91c6-242">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-242">N/A</span></span>  |
| <span data-ttu-id="b91c6-243">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-243">**Steps**</span></span> | <span data-ttu-id="b91c6-244">Lorsque hello web application hello partie de confiance, et hello IdP est le serveur AD FS, attribut de sécurité du jeton hello FedAuth peut être configuré en définissant le tooTrue requireSSL dans `system.identityModel.services` section du fichier web.config :</span><span class="sxs-lookup"><span data-stu-id="b91c6-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="b91c6-245">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="b91c6-246"><a id="cookie-definition"></a>Élément httpOnly requis dans la définition des cookies pour toutes les applications basées sur HTTP</span><span class="sxs-lookup"><span data-stu-id="b91c6-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="b91c6-247">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-247">Title</span></span>                   | <span data-ttu-id="b91c6-248">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-249">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-249">**Component**</span></span>               | <span data-ttu-id="b91c6-250">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-250">Web Application</span></span> | 
| <span data-ttu-id="b91c6-251">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-251">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-252">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-252">Build</span></span> |  
| <span data-ttu-id="b91c6-253">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-253">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-254">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-254">Generic</span></span> |
| <span data-ttu-id="b91c6-255">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-255">**Attributes**</span></span>              | <span data-ttu-id="b91c6-256">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-256">N/A</span></span>  |
| <span data-ttu-id="b91c6-257">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-257">**References**</span></span>              | [<span data-ttu-id="b91c6-258">Secure Cookie Attribute (Attribut de cookie sécurisé)</span><span class="sxs-lookup"><span data-stu-id="b91c6-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="b91c6-259">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-259">**Steps**</span></span> | <span data-ttu-id="b91c6-260">toomitigate hello risque de divulgation avec une attaque de l’écriture de scripts entre sites (XSS), un nouvel attribut - httpOnly - a été introduite toocookies et est pris en charge par tous les principaux navigateurs.</span><span class="sxs-lookup"><span data-stu-id="b91c6-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="b91c6-261">attribut de Hello Spécifie qu’un cookie n’est pas accessible via un script.</span><span class="sxs-lookup"><span data-stu-id="b91c6-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="b91c6-262">À l’aide de cookies HttpOnly, une application web réduit les risques de hello volées via un script et d’envoyés du site Web de l’attaquant tooan les informations sensibles contenues dans le cookie de hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="b91c6-263">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-263">Example</span></span>
<span data-ttu-id="b91c6-264">Toutes les applications HTTP qui utilisent des cookies doivent spécifier HttpOnly dans la définition de cookie hello en implémentant après la configuration dans le fichier web.config :</span><span class="sxs-lookup"><span data-stu-id="b91c6-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="b91c6-265">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-265">Title</span></span>                   | <span data-ttu-id="b91c6-266">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-267">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-267">**Component**</span></span>               | <span data-ttu-id="b91c6-268">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-268">Web Application</span></span> | 
| <span data-ttu-id="b91c6-269">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-269">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-270">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-270">Build</span></span> |  
| <span data-ttu-id="b91c6-271">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-271">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-272">Web Forms</span><span class="sxs-lookup"><span data-stu-id="b91c6-272">Web Forms</span></span> |
| <span data-ttu-id="b91c6-273">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-273">**Attributes**</span></span>              | <span data-ttu-id="b91c6-274">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-274">N/A</span></span>  |
| <span data-ttu-id="b91c6-275">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-275">**References**</span></span>              | [<span data-ttu-id="b91c6-276">FormsAuthentication.RequireSSL Property (Propriété FormsAuthentication.RequireSSL)</span><span class="sxs-lookup"><span data-stu-id="b91c6-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="b91c6-277">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-277">**Steps**</span></span> | <span data-ttu-id="b91c6-278">Hello RequireSSL valeur de la propriété est définie dans le fichier de configuration hello pour une application ASP.NET à l’aide de l’attribut requireSSL de hello d’élément de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="b91c6-279">Vous pouvez spécifier dans le fichier Web.config de hello pour votre application ASP.NET si SSL (Secure Sockets Layer) est le serveur toohello de cookies d’authentification par formulaire hello tooreturn requis par attribut de paramètre hello requireSSL.</span><span class="sxs-lookup"><span data-stu-id="b91c6-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="b91c6-280">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-280">Example</span></span> 
<span data-ttu-id="b91c6-281">Hello exemple de code suivant définit hello requireSSL attribut dans le fichier Web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="b91c6-282">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-282">Title</span></span>                   | <span data-ttu-id="b91c6-283">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-284">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-284">**Component**</span></span>               | <span data-ttu-id="b91c6-285">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-285">Web Application</span></span> | 
| <span data-ttu-id="b91c6-286">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-286">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-287">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-287">Build</span></span> |  
| <span data-ttu-id="b91c6-288">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-288">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="b91c6-289">MVC5</span></span> |
| <span data-ttu-id="b91c6-290">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-290">**Attributes**</span></span>              | <span data-ttu-id="b91c6-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="b91c6-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="b91c6-292">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-292">**References**</span></span>              | [<span data-ttu-id="b91c6-293">Windows Identity Foundation (WIF) Configuration – Part II (Configuration de Windows Identity Foundation (WIF) - Partie II)</span><span class="sxs-lookup"><span data-stu-id="b91c6-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="b91c6-294">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-294">**Steps**</span></span> | <span data-ttu-id="b91c6-295">attribut httpOnly tooset pour les cookies FedAuth hideFromCsript attribut doit être la valeur tooTrue.</span><span class="sxs-lookup"><span data-stu-id="b91c6-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="b91c6-296">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-296">Example</span></span>
<span data-ttu-id="b91c6-297">Configuration suivante montre la configuration correcte de hello :</span><span class="sxs-lookup"><span data-stu-id="b91c6-297">Following configuration shows hello correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="b91c6-298"><a id="csrf-asp"></a>Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les pages web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b91c6-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="b91c6-299">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-299">Title</span></span>                   | <span data-ttu-id="b91c6-300">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-301">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-301">**Component**</span></span>               | <span data-ttu-id="b91c6-302">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-302">Web Application</span></span> | 
| <span data-ttu-id="b91c6-303">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-303">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-304">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-304">Build</span></span> |  
| <span data-ttu-id="b91c6-305">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-305">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-306">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-306">Generic</span></span> |
| <span data-ttu-id="b91c6-307">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-307">**Attributes**</span></span>              | <span data-ttu-id="b91c6-308">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-308">N/A</span></span>  |
| <span data-ttu-id="b91c6-309">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-309">**References**</span></span>              | <span data-ttu-id="b91c6-310">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-310">N/A</span></span>  |
| <span data-ttu-id="b91c6-311">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-311">**Steps**</span></span> | <span data-ttu-id="b91c6-312">Falsification de requête (CSRF ou XSRF) est un type d’attaque dans lequel une personne malveillante peut exécuter des actions dans le contexte de sécurité hello de session établie d’un autre utilisateur sur un site web.</span><span class="sxs-lookup"><span data-stu-id="b91c6-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="b91c6-313">objectif de Hello est toomodify ou supprimer le contenu, si le site web ciblé de hello s’appuie exclusivement sur session cookies tooauthenticate réception d’une requête.</span><span class="sxs-lookup"><span data-stu-id="b91c6-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="b91c6-314">Un pirate peut exploiter cette vulnérabilité en obtenant tooload du navigateur d’un autre utilisateur d’une URL avec une commande d’un site vulnérable sur lequel hello utilisateur est déjà connecté.</span><span class="sxs-lookup"><span data-stu-id="b91c6-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="b91c6-315">Il existe de nombreuses façons pour un toodo attaquant, telles que par un autre site web d’hébergement qui charge une ressource de serveur vulnérable de hello ou tooclick d’utilisateur lors de l’obtention hello un lien.</span><span class="sxs-lookup"><span data-stu-id="b91c6-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="b91c6-316">attaque de Hello peut être évitée si le serveur de hello envoie un client toohello de jeton supplémentaires, requiert hello client tooinclude ce jeton dans toutes les demandes futures et vérifie que toutes les demandes futures incluent un jeton qui se rapporte toohello la session active, comme par à l’aide de hello ASP.NET AntiForgeryToken ou ViewState.</span><span class="sxs-lookup"><span data-stu-id="b91c6-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="b91c6-317">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-317">Title</span></span>                   | <span data-ttu-id="b91c6-318">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-319">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-319">**Component**</span></span>               | <span data-ttu-id="b91c6-320">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-320">Web Application</span></span> | 
| <span data-ttu-id="b91c6-321">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-321">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-322">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-322">Build</span></span> |  
| <span data-ttu-id="b91c6-323">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-323">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="b91c6-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="b91c6-325">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-325">**Attributes**</span></span>              | <span data-ttu-id="b91c6-326">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-326">N/A</span></span>  |
| <span data-ttu-id="b91c6-327">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-327">**References**</span></span>              | [<span data-ttu-id="b91c6-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages (Prévention des attaques XSRF/CSRF dans les pages MVC et Web ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b91c6-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="b91c6-329">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-329">**Steps**</span></span> | <span data-ttu-id="b91c6-330">Formulaires anti-CSRF et ASP.NET MVC - hello d’utilisation `AntiForgeryToken` méthode d’assistance sur les vues ; mettez un `Html.AntiForgeryToken()` dans l’écran hello, par exemple,</span><span class="sxs-lookup"><span data-stu-id="b91c6-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="b91c6-331">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="b91c6-332">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="b91c6-333">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-333">Example</span></span>
<span data-ttu-id="b91c6-334">À hello même moment, visiteur de hello Html.AntiForgeryToken() donne un cookie appelé __RequestVerificationToken, avec hello même valeur que la valeur aléatoire masqué hello indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b91c6-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="b91c6-335">Toovalidate une publication de formulaire entrantes, ajoutez ensuite la méthode d’action hello [ValidateAntiForgeryToken] filtre toohello cible.</span><span class="sxs-lookup"><span data-stu-id="b91c6-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="b91c6-336">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b91c6-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="b91c6-337">Un filtre d’autorisation qui vérifie les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b91c6-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="b91c6-338">demande entrante de Hello dispose d’un cookie appelé __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="b91c6-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="b91c6-339">Hello demande entrante a un `Request.Form` entrée appelée __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="b91c6-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="b91c6-340">Ces cookies et `Request.Form` correspondance des valeurs en supposant que toutes les est bien, hello demande passe par normalement.</span><span class="sxs-lookup"><span data-stu-id="b91c6-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="b91c6-341">Dans le cas contraire, un échec d’autorisation survient avec le message « Un jeton anti-contrefaçon requis n’a pas été fourni ou n’est pas valide ».</span><span class="sxs-lookup"><span data-stu-id="b91c6-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="b91c6-342">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-342">Example</span></span>
<span data-ttu-id="b91c6-343">AJAX et anti-CSRF : jeton de formulaire hello peut poser un problème pour les requêtes AJAX, car une requête AJAX peut envoyer des données JSON, pas les données de formulaire HTML.</span><span class="sxs-lookup"><span data-stu-id="b91c6-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="b91c6-344">Une solution consiste aux jetons hello toosend dans un en-tête HTTP personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b91c6-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="b91c6-345">Hello de code suivant utilise des jetons de Razor syntaxe toogenerate hello, puis ajoute hello jetons tooan AJAX demande.</span><span class="sxs-lookup"><span data-stu-id="b91c6-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="b91c6-346">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-346">Example</span></span>
<span data-ttu-id="b91c6-347">Lorsque vous traitez la demande de hello, extrayez les jetons hello à partir de l’en-tête de demande hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="b91c6-348">Puis l’appel hello AntiForgery.Validate méthode toovalidate des jetons hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="b91c6-349">Hello méthode Validate lève une exception si les jetons hello ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="b91c6-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="b91c6-350">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-350">Title</span></span>                   | <span data-ttu-id="b91c6-351">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-352">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-352">**Component**</span></span>               | <span data-ttu-id="b91c6-353">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-353">Web Application</span></span> | 
| <span data-ttu-id="b91c6-354">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-354">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-355">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-355">Build</span></span> |  
| <span data-ttu-id="b91c6-356">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-356">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-357">Web Forms</span><span class="sxs-lookup"><span data-stu-id="b91c6-357">Web Forms</span></span> |
| <span data-ttu-id="b91c6-358">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-358">**Attributes**</span></span>              | <span data-ttu-id="b91c6-359">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-359">N/A</span></span>  |
| <span data-ttu-id="b91c6-360">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-360">**References**</span></span>              | [<span data-ttu-id="b91c6-361">Tirer parti des fonctionnalités intégrées ASP.NET tooFend Off Web des attaques</span><span class="sxs-lookup"><span data-stu-id="b91c6-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="b91c6-362">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-362">**Steps**</span></span> | <span data-ttu-id="b91c6-363">Attaques CSRF dans WebForm en fonction des applications peuvent être atténuées en définissant la chaîne aléatoire ViewStateUserKey tooa qui varie pour chaque utilisateur - ID utilisateur ou, mieux encore, ID de session.</span><span class="sxs-lookup"><span data-stu-id="b91c6-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="b91c6-364">Pour un certain nombre de raisons techniques et sociales, l’identifiant de session constitue un bien meilleur choix, car ce type d’identifiant est imprévisible, arrive à expiration et varie selon chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b91c6-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="b91c6-365">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-365">Example</span></span>
<span data-ttu-id="b91c6-366">Voici le code hello vous devez toohave dans toutes les pages :</span><span class="sxs-lookup"><span data-stu-id="b91c6-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="b91c6-367"><a id="inactivity-lifetime"></a>Configurer la durée de vie d’inactivité d’une session</span><span class="sxs-lookup"><span data-stu-id="b91c6-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="b91c6-368">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-368">Title</span></span>                   | <span data-ttu-id="b91c6-369">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-370">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-370">**Component**</span></span>               | <span data-ttu-id="b91c6-371">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-371">Web Application</span></span> | 
| <span data-ttu-id="b91c6-372">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-372">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-373">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-373">Build</span></span> |  
| <span data-ttu-id="b91c6-374">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-374">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-375">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-375">Generic</span></span> |
| <span data-ttu-id="b91c6-376">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-376">**Attributes**</span></span>              | <span data-ttu-id="b91c6-377">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-377">N/A</span></span>  |
| <span data-ttu-id="b91c6-378">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-378">**References**</span></span>              | <span data-ttu-id="b91c6-379">[HttpSessionState.Timeout Property (Propriété HttpSessionState.Timeout)](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="b91c6-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="b91c6-380">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-380">**Steps**</span></span> | <span data-ttu-id="b91c6-381">Délai d’expiration de session représente hello événement qui se produit quand un utilisateur ne n’exécute aucune action sur un site web pendant un intervalle (défini par le serveur web).</span><span class="sxs-lookup"><span data-stu-id="b91c6-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="b91c6-382">Hello d’événement, côté serveur, de modifier le statut de hello de too'invalid de session utilisateur hello » (par exemple « non utilisé plus ») et lui demander de hello web server toodestroy (la suppression de toutes les données contenues dans celui-ci).</span><span class="sxs-lookup"><span data-stu-id="b91c6-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="b91c6-383">Hello exemple de code suivant définit hello délai d’expiration session attribut too15 minutes dans le fichier Web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="b91c6-384">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-384">Example</span></span>
<span data-ttu-id="b91c6-385">``\`Code XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="b91c6-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="b91c6-386">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-386">Title</span></span>                   | <span data-ttu-id="b91c6-387">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-388">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-388">**Component**</span></span>               | <span data-ttu-id="b91c6-389">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-389">Web Application</span></span> | 
| <span data-ttu-id="b91c6-390">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-390">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-391">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-391">Build</span></span> |  
| <span data-ttu-id="b91c6-392">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-392">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-393">Web Forms</span><span class="sxs-lookup"><span data-stu-id="b91c6-393">Web Forms</span></span> |
| <span data-ttu-id="b91c6-394">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-394">**Attributes**</span></span>              | <span data-ttu-id="b91c6-395">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-395">N/A</span></span>  |
| <span data-ttu-id="b91c6-396">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-396">**References**</span></span>              | <span data-ttu-id="b91c6-397">[forms, élément de authentication (Schéma des paramètres ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="b91c6-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="b91c6-398">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-398">**Steps**</span></span> | <span data-ttu-id="b91c6-399">Définir les minutes hello too15 de délai d’attente de cookie de Ticket d’authentification de formulaires</span><span class="sxs-lookup"><span data-stu-id="b91c6-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="b91c6-400">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-400">Example</span></span>
<span data-ttu-id="b91c6-401">``\`Code XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="b91c6-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="b91c6-402">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-402">Example</span></span>
<span data-ttu-id="b91c6-403">Également hello ADFS émis la durée de vie du jeton SAML revendication doit être défini à too15 minutes, en exécutant hello commande powershell sur un serveur AD FS hello suivante :</span><span class="sxs-lookup"><span data-stu-id="b91c6-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="b91c6-404"><a id="proper-app-logout"></a>Implémenter la déconnexion appropriée à partir de l’application hello</span><span class="sxs-lookup"><span data-stu-id="b91c6-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="b91c6-405">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-405">Title</span></span>                   | <span data-ttu-id="b91c6-406">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-407">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-407">**Component**</span></span>               | <span data-ttu-id="b91c6-408">Application web</span><span class="sxs-lookup"><span data-stu-id="b91c6-408">Web Application</span></span> | 
| <span data-ttu-id="b91c6-409">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-409">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-410">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-410">Build</span></span> |  
| <span data-ttu-id="b91c6-411">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-411">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-412">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-412">Generic</span></span> |
| <span data-ttu-id="b91c6-413">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-413">**Attributes**</span></span>              | <span data-ttu-id="b91c6-414">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-414">N/A</span></span>  |
| <span data-ttu-id="b91c6-415">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-415">**References**</span></span>              | <span data-ttu-id="b91c6-416">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-416">N/A</span></span>  |
| <span data-ttu-id="b91c6-417">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-417">**Steps**</span></span> | <span data-ttu-id="b91c6-418">Effectuer déconnexion approprié à partir de l’application hello, lorsque l’utilisateur appuie sur déconnecter de bouton.</span><span class="sxs-lookup"><span data-stu-id="b91c6-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="b91c6-419">Lors de la déconnexion, l’application doit détruire la session de l’utilisateur et également réinitialiser et annuler la valeur du cookie de session, ainsi que la valeur du cookie d’authentification.</span><span class="sxs-lookup"><span data-stu-id="b91c6-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="b91c6-420">En outre, lorsque plusieurs sessions identité d’utilisateur unique tooa liés, ils doivent être collectivement terminées côté hello serveur au délai d’attente ou de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="b91c6-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="b91c6-421">Enfin, assurez-vous que la fonctionnalité de déconnexion est accessible sur chaque page.</span><span class="sxs-lookup"><span data-stu-id="b91c6-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="b91c6-422"><a id="csrf-api"></a>Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b91c6-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="b91c6-423">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-423">Title</span></span>                   | <span data-ttu-id="b91c6-424">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-425">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-425">**Component**</span></span>               | <span data-ttu-id="b91c6-426">API Web</span><span class="sxs-lookup"><span data-stu-id="b91c6-426">Web API</span></span> | 
| <span data-ttu-id="b91c6-427">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-427">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-428">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-428">Build</span></span> |  
| <span data-ttu-id="b91c6-429">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-429">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-430">Générique</span><span class="sxs-lookup"><span data-stu-id="b91c6-430">Generic</span></span> |
| <span data-ttu-id="b91c6-431">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-431">**Attributes**</span></span>              | <span data-ttu-id="b91c6-432">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-432">N/A</span></span>  |
| <span data-ttu-id="b91c6-433">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-433">**References**</span></span>              | <span data-ttu-id="b91c6-434">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-434">N/A</span></span>  |
| <span data-ttu-id="b91c6-435">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-435">**Steps**</span></span> | <span data-ttu-id="b91c6-436">Falsification de requête (CSRF ou XSRF) est un type d’attaque dans lequel une personne malveillante peut exécuter des actions dans le contexte de sécurité hello de session établie d’un autre utilisateur sur un site web.</span><span class="sxs-lookup"><span data-stu-id="b91c6-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="b91c6-437">objectif de Hello est toomodify ou supprimer le contenu, si le site web ciblé de hello s’appuie exclusivement sur session cookies tooauthenticate réception d’une requête.</span><span class="sxs-lookup"><span data-stu-id="b91c6-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="b91c6-438">Un pirate peut exploiter cette vulnérabilité en obtenant tooload du navigateur d’un autre utilisateur d’une URL avec une commande d’un site vulnérable sur lequel hello utilisateur est déjà connecté.</span><span class="sxs-lookup"><span data-stu-id="b91c6-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="b91c6-439">Il existe de nombreuses façons pour un toodo attaquant, telles que par un autre site web d’hébergement qui charge une ressource de serveur vulnérable de hello ou tooclick d’utilisateur lors de l’obtention hello un lien.</span><span class="sxs-lookup"><span data-stu-id="b91c6-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="b91c6-440">attaque de Hello peut être évitée si le serveur de hello envoie un client toohello de jeton supplémentaires, requiert hello client tooinclude ce jeton dans toutes les demandes futures et vérifie que toutes les demandes futures incluent un jeton qui se rapporte toohello la session active, comme par à l’aide de hello ASP.NET AntiForgeryToken ou ViewState.</span><span class="sxs-lookup"><span data-stu-id="b91c6-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="b91c6-441">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-441">Title</span></span>                   | <span data-ttu-id="b91c6-442">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-443">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-443">**Component**</span></span>               | <span data-ttu-id="b91c6-444">API Web</span><span class="sxs-lookup"><span data-stu-id="b91c6-444">Web API</span></span> | 
| <span data-ttu-id="b91c6-445">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-445">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-446">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-446">Build</span></span> |  
| <span data-ttu-id="b91c6-447">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-447">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="b91c6-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="b91c6-449">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-449">**Attributes**</span></span>              | <span data-ttu-id="b91c6-450">N/A</span><span class="sxs-lookup"><span data-stu-id="b91c6-450">N/A</span></span>  |
| <span data-ttu-id="b91c6-451">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-451">**References**</span></span>              | [<span data-ttu-id="b91c6-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API (Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) dans les API Web ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b91c6-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="b91c6-453">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-453">**Steps**</span></span> | <span data-ttu-id="b91c6-454">AJAX et anti-CSRF : jeton de formulaire hello peut poser un problème pour les requêtes AJAX, car une requête AJAX peut envoyer des données JSON, pas les données de formulaire HTML.</span><span class="sxs-lookup"><span data-stu-id="b91c6-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="b91c6-455">Une solution consiste aux jetons hello toosend dans un en-tête HTTP personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b91c6-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="b91c6-456">Hello de code suivant utilise des jetons de Razor syntaxe toogenerate hello, puis ajoute hello jetons tooan AJAX demande.</span><span class="sxs-lookup"><span data-stu-id="b91c6-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="b91c6-457">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="b91c6-458">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-458">Example</span></span>
<span data-ttu-id="b91c6-459">Lorsque vous traitez la demande de hello, extrayez les jetons hello à partir de l’en-tête de demande hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="b91c6-460">Puis l’appel hello AntiForgery.Validate méthode toovalidate des jetons hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="b91c6-461">Hello méthode Validate lève une exception si les jetons hello ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="b91c6-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="b91c6-462">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-462">Example</span></span>
<span data-ttu-id="b91c6-463">Anti-CSRF et formulaires ASP.NET MVC - hello d’utilisation méthode d’assistance de AntiForgeryToken sur les vues ; Placez un Html.AntiForgeryToken() sous forme de hello, par exemple,</span><span class="sxs-lookup"><span data-stu-id="b91c6-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="b91c6-464">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-464">Example</span></span>
<span data-ttu-id="b91c6-465">exemple Hello ci-dessus produira hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b91c6-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="b91c6-466">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-466">Example</span></span>
<span data-ttu-id="b91c6-467">À hello même moment, visiteur de hello Html.AntiForgeryToken() donne un cookie appelé __RequestVerificationToken, avec hello même valeur que la valeur aléatoire masqué hello indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b91c6-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="b91c6-468">Toovalidate une publication de formulaire entrantes, ajoutez ensuite la méthode d’action hello [ValidateAntiForgeryToken] filtre toohello cible.</span><span class="sxs-lookup"><span data-stu-id="b91c6-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="b91c6-469">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b91c6-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="b91c6-470">Un filtre d’autorisation qui vérifie les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b91c6-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="b91c6-471">demande entrante de Hello dispose d’un cookie appelé __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="b91c6-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="b91c6-472">Hello demande entrante a un `Request.Form` entrée appelée __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="b91c6-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="b91c6-473">Ces cookies et `Request.Form` correspondance des valeurs en supposant que toutes les est bien, hello demande passe par normalement.</span><span class="sxs-lookup"><span data-stu-id="b91c6-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="b91c6-474">Dans le cas contraire, un échec d’autorisation survient avec le message « Un jeton anti-contrefaçon requis n’a pas été fourni ou n’est pas valide ».</span><span class="sxs-lookup"><span data-stu-id="b91c6-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="b91c6-475">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b91c6-475">Title</span></span>                   | <span data-ttu-id="b91c6-476">Détails</span><span class="sxs-lookup"><span data-stu-id="b91c6-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b91c6-477">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b91c6-477">**Component**</span></span>               | <span data-ttu-id="b91c6-478">API Web</span><span class="sxs-lookup"><span data-stu-id="b91c6-478">Web API</span></span> | 
| <span data-ttu-id="b91c6-479">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b91c6-479">**SDL Phase**</span></span>               | <span data-ttu-id="b91c6-480">Créer</span><span class="sxs-lookup"><span data-stu-id="b91c6-480">Build</span></span> |  
| <span data-ttu-id="b91c6-481">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b91c6-481">**Applicable Technologies**</span></span> | <span data-ttu-id="b91c6-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="b91c6-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="b91c6-483">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b91c6-483">**Attributes**</span></span>              | <span data-ttu-id="b91c6-484">Fournisseur d’identité - ADFS, Fournisseur d’identité - Azure AD</span><span class="sxs-lookup"><span data-stu-id="b91c6-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="b91c6-485">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b91c6-485">**References**</span></span>              | [<span data-ttu-id="b91c6-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2 (Sécuriser une API Web avec des comptes individuels et une connexion locale dans API Web ASP.NET 2.2)</span><span class="sxs-lookup"><span data-stu-id="b91c6-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="b91c6-487">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b91c6-487">**Steps**</span></span> | <span data-ttu-id="b91c6-488">Si hello API Web est sécurisé à l’aide d’OAuth 2.0, puis il attend un jeton de support dans l’autorisation demande en-tête et accorde l’accès toohello la demande uniquement si le jeton de hello est valide.</span><span class="sxs-lookup"><span data-stu-id="b91c6-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="b91c6-489">Contrairement à l’authentification basé sur les cookies, les navigateurs n’attachement pas toorequests de jetons de porteur hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="b91c6-490">Hello demande client doit tooexplicitly d’attacher le jeton de support hello dans l’en-tête de demande hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="b91c6-491">Par conséquent, dans le cas des API Web ASP.NET protégées à l’aide d’OAuth 2.0, les jetons du porteur sont considérés comme un moyen de défense contre les attaques CSRF.</span><span class="sxs-lookup"><span data-stu-id="b91c6-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="b91c6-492">Notez que si la partie MVC hello de l’application hello utilise l’authentification par formulaire (par exemple, utilise les cookies), les jetons anti-contrefaçon ont toobe utilisé par l’application web MVC est hello.</span><span class="sxs-lookup"><span data-stu-id="b91c6-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="b91c6-493">Exemple</span><span class="sxs-lookup"><span data-stu-id="b91c6-493">Example</span></span>
<span data-ttu-id="b91c6-494">Hello API Web a toobe informé toorely uniquement sur les jetons de support et non sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="b91c6-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="b91c6-495">Il est possible en hello suivant la configuration dans `WebApiConfig.Register` méthode : ''' config du code C-Sharp. SuppressDefaultHostAuthentication() ; configuration. Filters.Add (nouvelle HostAuthenticationFilter(OAuthDefaults.AuthenticationType)) ;</span><span class="sxs-lookup"><span data-stu-id="b91c6-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
