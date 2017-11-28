---
title: "Gestion des sessions - Outil Microsoft de modélisation des menaces - Azure | Microsoft Docs"
description: "mesures de prévention des menaces exposées dans l’outil de modélisation des menaces"
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
ms.openlocfilehash: 56471d8ef68eacacb3ecebad5056d7e7a9f3ca40
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="b40ff-103">Infrastructure de sécurité : gestion des sessions | Articles</span><span class="sxs-lookup"><span data-stu-id="b40ff-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="b40ff-104">Produit/service</span><span class="sxs-lookup"><span data-stu-id="b40ff-104">Product/Service</span></span> | <span data-ttu-id="b40ff-105">Article</span><span class="sxs-lookup"><span data-stu-id="b40ff-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="b40ff-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="b40ff-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="b40ff-107">Implémenter une déconnexion appropriée à l’aide de méthodes ADAL lors de l’utilisation d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="b40ff-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="b40ff-108">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="b40ff-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="b40ff-109">Utiliser des durées de vie limitées pour les jetons SaS générés</span><span class="sxs-lookup"><span data-stu-id="b40ff-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="b40ff-110">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="b40ff-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="b40ff-111">Utiliser des durées de vie de jeton minimales pour les jetons de ressource générés</span><span class="sxs-lookup"><span data-stu-id="b40ff-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="b40ff-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="b40ff-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="b40ff-113">Implémenter une déconnexion appropriée à l’aide de méthodes WsFederation lors de l’utilisation d’ADFS</span><span class="sxs-lookup"><span data-stu-id="b40ff-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="b40ff-114">**Serveur d’identité**</span><span class="sxs-lookup"><span data-stu-id="b40ff-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="b40ff-115">Implémenter une déconnexion appropriée lors de l’utilisation d’IdentityServer</span><span class="sxs-lookup"><span data-stu-id="b40ff-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="b40ff-116">**Application web**</span><span class="sxs-lookup"><span data-stu-id="b40ff-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="b40ff-117">Utilisation requise de cookies sécurisés par les applications disponibles par le biais de HTTPS</span><span class="sxs-lookup"><span data-stu-id="b40ff-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="b40ff-118">Élément httpOnly requis dans la définition des cookies pour toutes les applications basées sur HTTP</span><span class="sxs-lookup"><span data-stu-id="b40ff-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="b40ff-119">Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les pages web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b40ff-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="b40ff-120">Configurer la durée de vie d’inactivité d’une session</span><span class="sxs-lookup"><span data-stu-id="b40ff-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="b40ff-121">Implémenter une déconnexion appropriée de l’application</span><span class="sxs-lookup"><span data-stu-id="b40ff-121">Implement proper logout from the application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="b40ff-122">**API Web**</span><span class="sxs-lookup"><span data-stu-id="b40ff-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="b40ff-123">Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b40ff-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="b40ff-124"><a id="logout-adal"></a>Implémenter une déconnexion appropriée à l’aide de méthodes ADAL lors de l’utilisation d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="b40ff-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="b40ff-125">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-125">Title</span></span>                   | <span data-ttu-id="b40ff-126">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-127">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-127">**Component**</span></span>               | <span data-ttu-id="b40ff-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="b40ff-128">Azure AD</span></span> | 
| <span data-ttu-id="b40ff-129">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-129">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-130">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-130">Build</span></span> |  
| <span data-ttu-id="b40ff-131">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-131">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-132">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-132">Generic</span></span> |
| <span data-ttu-id="b40ff-133">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-133">**Attributes**</span></span>              | <span data-ttu-id="b40ff-134">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-134">N/A</span></span>  |
| <span data-ttu-id="b40ff-135">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-135">**References**</span></span>              | <span data-ttu-id="b40ff-136">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-136">N/A</span></span>  |
| <span data-ttu-id="b40ff-137">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-137">**Steps**</span></span> | <span data-ttu-id="b40ff-138">Si l’application s’appuie sur le jeton d’accès émis par Azure AD, le gestionnaire d’événements de déconnexion doit appeler</span><span class="sxs-lookup"><span data-stu-id="b40ff-138">If the application relies on access token issued by Azure AD, the logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="b40ff-139">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="b40ff-140">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-140">Example</span></span>
<span data-ttu-id="b40ff-141">Il est également nécessaire de détruire la session de l’utilisateur en appelant la méthode Session.Abandon().</span><span class="sxs-lookup"><span data-stu-id="b40ff-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="b40ff-142">La méthode ci-après présente une implémentation sécurisée de la déconnexion d’un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="b40ff-142">Following method shows secure implementation of user logout:</span></span>
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

## <span data-ttu-id="b40ff-143"><a id="finite-tokens"></a>Utiliser des durées de vie limitées pour les jetons SaS générés</span><span class="sxs-lookup"><span data-stu-id="b40ff-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="b40ff-144">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-144">Title</span></span>                   | <span data-ttu-id="b40ff-145">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-146">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-146">**Component**</span></span>               | <span data-ttu-id="b40ff-147">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="b40ff-147">IoT Device</span></span> | 
| <span data-ttu-id="b40ff-148">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-148">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-149">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-149">Build</span></span> |  
| <span data-ttu-id="b40ff-150">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-150">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-151">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-151">Generic</span></span> |
| <span data-ttu-id="b40ff-152">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-152">**Attributes**</span></span>              | <span data-ttu-id="b40ff-153">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-153">N/A</span></span>  |
| <span data-ttu-id="b40ff-154">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-154">**References**</span></span>              | <span data-ttu-id="b40ff-155">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-155">N/A</span></span>  |
| <span data-ttu-id="b40ff-156">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-156">**Steps**</span></span> | <span data-ttu-id="b40ff-157">Les jetons SaS générés pour l’authentification auprès d’Azure IoT Hub doivent présenter une période d’expiration limitée dans le temps.</span><span class="sxs-lookup"><span data-stu-id="b40ff-157">SaS tokens generated for authenticating to Azure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="b40ff-158">Conservez les durées de vie des jetons SaS sur une valeur minimale pour limiter la durée pendant laquelle ces jetons peuvent être relus dans le cas où leur intégrité a été compromise.</span><span class="sxs-lookup"><span data-stu-id="b40ff-158">Keep the SaS token lifetimes to a minimum to limit the amount of time they can be replayed in case the tokens are compromised.</span></span>|

## <span data-ttu-id="b40ff-159"><a id="resource-tokens"></a>Utiliser des durées de vie de jeton minimales pour les jetons de ressource générés</span><span class="sxs-lookup"><span data-stu-id="b40ff-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="b40ff-160">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-160">Title</span></span>                   | <span data-ttu-id="b40ff-161">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-162">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-162">**Component**</span></span>               | <span data-ttu-id="b40ff-163">Azure Document DB</span><span class="sxs-lookup"><span data-stu-id="b40ff-163">Azure Document DB</span></span> | 
| <span data-ttu-id="b40ff-164">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-164">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-165">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-165">Build</span></span> |  
| <span data-ttu-id="b40ff-166">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-166">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-167">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-167">Generic</span></span> |
| <span data-ttu-id="b40ff-168">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-168">**Attributes**</span></span>              | <span data-ttu-id="b40ff-169">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-169">N/A</span></span>  |
| <span data-ttu-id="b40ff-170">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-170">**References**</span></span>              | <span data-ttu-id="b40ff-171">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-171">N/A</span></span>  |
| <span data-ttu-id="b40ff-172">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-172">**Steps**</span></span> | <span data-ttu-id="b40ff-173">Définissez la période de validité d’un jeton de ressource sur une valeur minimale.</span><span class="sxs-lookup"><span data-stu-id="b40ff-173">Reduce the timespan of resource token to a minimum value required.</span></span> <span data-ttu-id="b40ff-174">Les jetons de ressource ont une durée de validité par défaut d'une heure.</span><span class="sxs-lookup"><span data-stu-id="b40ff-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="b40ff-175"><a id="wsfederation-logout"></a>Implémenter une déconnexion appropriée à l’aide de méthodes WsFederation lors de l’utilisation d’ADFS</span><span class="sxs-lookup"><span data-stu-id="b40ff-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="b40ff-176">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-176">Title</span></span>                   | <span data-ttu-id="b40ff-177">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-178">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-178">**Component**</span></span>               | <span data-ttu-id="b40ff-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="b40ff-179">ADFS</span></span> | 
| <span data-ttu-id="b40ff-180">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-180">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-181">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-181">Build</span></span> |  
| <span data-ttu-id="b40ff-182">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-182">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-183">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-183">Generic</span></span> |
| <span data-ttu-id="b40ff-184">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-184">**Attributes**</span></span>              | <span data-ttu-id="b40ff-185">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-185">N/A</span></span>  |
| <span data-ttu-id="b40ff-186">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-186">**References**</span></span>              | <span data-ttu-id="b40ff-187">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-187">N/A</span></span>  |
| <span data-ttu-id="b40ff-188">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-188">**Steps**</span></span> | <span data-ttu-id="b40ff-189">Si l’application s’appuie sur un jeton STS (service d’émission de jeton de sécurité) émis par les services ADFS (Active Directory Federation Services), le gestionnaire d’événements de déconnexion doit appeler la méthode WSFederationAuthenticationModule.FederatedSignOut() pour déconnecter l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b40ff-189">If the application relies on STS token issued by ADFS, the logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method to log out the user.</span></span> <span data-ttu-id="b40ff-190">En outre, la session actuelle doit être détruite, et la valeur de jeton de session doit être réinitialisée et annulée.</span><span class="sxs-lookup"><span data-stu-id="b40ff-190">Also the current session should be destroyed, and the session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="b40ff-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes the user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at the specified security token service (STS) by using the WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of the current session and raises the appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at the specified security token service (STS) by using the WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="b40ff-192"><a id="proper-logout"></a>Implémenter une déconnexion appropriée lors de l’utilisation d’IdentityServer</span><span class="sxs-lookup"><span data-stu-id="b40ff-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="b40ff-193">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-193">Title</span></span>                   | <span data-ttu-id="b40ff-194">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-195">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-195">**Component**</span></span>               | <span data-ttu-id="b40ff-196">IdentityServer</span><span class="sxs-lookup"><span data-stu-id="b40ff-196">Identity Server</span></span> | 
| <span data-ttu-id="b40ff-197">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-197">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-198">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-198">Build</span></span> |  
| <span data-ttu-id="b40ff-199">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-199">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-200">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-200">Generic</span></span> |
| <span data-ttu-id="b40ff-201">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-201">**Attributes**</span></span>              | <span data-ttu-id="b40ff-202">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-202">N/A</span></span>  |
| <span data-ttu-id="b40ff-203">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-203">**References**</span></span>              | [<span data-ttu-id="b40ff-204">IdentityServer3-Federated sign out</span><span class="sxs-lookup"><span data-stu-id="b40ff-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="b40ff-205">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-205">**Steps**</span></span> | <span data-ttu-id="b40ff-206">IdentityServer prend en charge une possibilité de fédération avec des fournisseurs d’identité externes.</span><span class="sxs-lookup"><span data-stu-id="b40ff-206">IdentityServer supports the ability to federate with external identity providers.</span></span> <span data-ttu-id="b40ff-207">Lorsqu’un utilisateur se déconnecte d’un fournisseur d’identité en amont, selon le protocole utilisé, la déconnexion de l’utilisateur peut parfois être signalée par une notification. Cela permet à IdentityServer d’informer ses clients pour que ceux-ci puissent également déconnecter l’utilisateur. Pour plus d’informations sur les détails d’implémentation, consultez la section relative aux références dans la documentation.</span><span class="sxs-lookup"><span data-stu-id="b40ff-207">When a user signs out of an upstream identity provider, depending upon the protocol used, it might be possible to receive a notification when the user signs out. It allows IdentityServer to notify its clients so they can also sign the user out. Check the documentation in the references section for the implementation details.</span></span>|

## <span data-ttu-id="b40ff-208"><a id="https-secure-cookies"></a>Utilisation requise de cookies sécurisés par les applications disponibles par le biais de HTTPS</span><span class="sxs-lookup"><span data-stu-id="b40ff-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="b40ff-209">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-209">Title</span></span>                   | <span data-ttu-id="b40ff-210">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-211">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-211">**Component**</span></span>               | <span data-ttu-id="b40ff-212">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-212">Web Application</span></span> | 
| <span data-ttu-id="b40ff-213">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-213">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-214">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-214">Build</span></span> |  
| <span data-ttu-id="b40ff-215">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-215">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-216">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-216">Generic</span></span> |
| <span data-ttu-id="b40ff-217">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-217">**Attributes**</span></span>              | <span data-ttu-id="b40ff-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="b40ff-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="b40ff-219">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-219">**References**</span></span>              | <span data-ttu-id="b40ff-220">[httpCookies, élément (Schéma des paramètres ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property (Propriété HttpCookie.Secure)](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="b40ff-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="b40ff-221">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-221">**Steps**</span></span> | <span data-ttu-id="b40ff-222">Normalement, les cookies sont uniquement accessibles au domaine auquel ils ont été étendus.</span><span class="sxs-lookup"><span data-stu-id="b40ff-222">Cookies are normally only accessible to the domain for which they were scoped.</span></span> <span data-ttu-id="b40ff-223">Malheureusement, la définition du terme « domaine » n’inclut pas le protocole, de sorte que les cookies créés par le biais du protocole HTTPS sont accessibles par l’intermédiaire de HTTP.</span><span class="sxs-lookup"><span data-stu-id="b40ff-223">Unfortunately, the definition of "domain" does not include the protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="b40ff-224">L’attribut « secure » indique donc au navigateur que le cookie doit uniquement être accessible via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b40ff-224">The "secure" attribute indicates to the browser that the cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="b40ff-225">Assurez-vous que tous les cookies définis sur HTTPS utilisent l’attribut **secure**.</span><span class="sxs-lookup"><span data-stu-id="b40ff-225">Ensure that all cookies set over HTTPS use the **secure** attribute.</span></span> <span data-ttu-id="b40ff-226">Il est possible d’appliquer cette exigence dans le fichier web.config en définissant l’attribut requireSSL sur la valeur true.</span><span class="sxs-lookup"><span data-stu-id="b40ff-226">The requirement can be enforced in the web.config file by setting the requireSSL attribute to true.</span></span> <span data-ttu-id="b40ff-227">Cette approche est recommandée, car elle appliquera l’attribut **secure** à tous les cookies actuels et futurs sans nécessiter aucune modification de code supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="b40ff-227">It is the preferred approach because it will enforce the **secure** attribute for all current and future cookies without the need to make any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="b40ff-228">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="b40ff-229">Le paramètre est appliqué même en cas d’utilisation du protocole HTTP pour accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="b40ff-229">The setting is enforced even if HTTP is used to access the application.</span></span> <span data-ttu-id="b40ff-230">Si le protocole HTTP est utilisé, ce paramètre arrête l’application, car les cookies étant définis avec l’attribut secure, le navigateur ne les renvoie pas à l’application.</span><span class="sxs-lookup"><span data-stu-id="b40ff-230">If HTTP is used to access the application, the setting breaks the application because the cookies are set with the secure attribute and the browser will not send them back to the application.</span></span>

| <span data-ttu-id="b40ff-231">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-231">Title</span></span>                   | <span data-ttu-id="b40ff-232">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-233">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-233">**Component**</span></span>               | <span data-ttu-id="b40ff-234">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-234">Web Application</span></span> | 
| <span data-ttu-id="b40ff-235">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-235">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-236">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-236">Build</span></span> |  
| <span data-ttu-id="b40ff-237">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-237">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-238">Web Forms, MVC5</span><span class="sxs-lookup"><span data-stu-id="b40ff-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="b40ff-239">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-239">**Attributes**</span></span>              | <span data-ttu-id="b40ff-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="b40ff-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="b40ff-241">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-241">**References**</span></span>              | <span data-ttu-id="b40ff-242">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-242">N/A</span></span>  |
| <span data-ttu-id="b40ff-243">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-243">**Steps**</span></span> | <span data-ttu-id="b40ff-244">Lorsque l’application web constitue la partie de confiance et que le fournisseur d’identité est le serveur ADFS, il est possible de configurer l’attribut secure du jeton FedAuth en définissant l’élément requireSSL sur la valeur True dans la section `system.identityModel.services` du fichier web.config :</span><span class="sxs-lookup"><span data-stu-id="b40ff-244">When the web application is the Relying Party, and the IdP is ADFS server, the FedAuth token's secure attribute can be configured by setting requireSSL to True in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="b40ff-245">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="b40ff-246"><a id="cookie-definition"></a>Élément httpOnly requis dans la définition des cookies pour toutes les applications basées sur HTTP</span><span class="sxs-lookup"><span data-stu-id="b40ff-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="b40ff-247">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-247">Title</span></span>                   | <span data-ttu-id="b40ff-248">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-249">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-249">**Component**</span></span>               | <span data-ttu-id="b40ff-250">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-250">Web Application</span></span> | 
| <span data-ttu-id="b40ff-251">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-251">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-252">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-252">Build</span></span> |  
| <span data-ttu-id="b40ff-253">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-253">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-254">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-254">Generic</span></span> |
| <span data-ttu-id="b40ff-255">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-255">**Attributes**</span></span>              | <span data-ttu-id="b40ff-256">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-256">N/A</span></span>  |
| <span data-ttu-id="b40ff-257">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-257">**References**</span></span>              | [<span data-ttu-id="b40ff-258">Secure Cookie Attribute (Attribut de cookie sécurisé)</span><span class="sxs-lookup"><span data-stu-id="b40ff-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="b40ff-259">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-259">**Steps**</span></span> | <span data-ttu-id="b40ff-260">Pour atténuer les risques de divulgation d’informations découlant d’une attaque par exécution de scripts intersites (XSS), le nouvel attribut httpOnly a été introduit pour les cookies et est pris en charge par tous les principaux navigateurs.</span><span class="sxs-lookup"><span data-stu-id="b40ff-260">To mitigate the risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced to cookies and is supported by all major browsers.</span></span> <span data-ttu-id="b40ff-261">L’attribut indique qu’un cookie n’est pas accessible par le biais d’un script.</span><span class="sxs-lookup"><span data-stu-id="b40ff-261">The attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="b40ff-262">En utilisant des cookies HttpOnly, une application web réduit les risques que des informations sensibles contenues dans le cookie soient volées par l’intermédiaire d’un script et envoyées au site web d’un attaquant.</span><span class="sxs-lookup"><span data-stu-id="b40ff-262">By using HttpOnly cookies, a web application reduces the possibility that sensitive information contained in the cookie can be stolen via script and sent to an attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="b40ff-263">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-263">Example</span></span>
<span data-ttu-id="b40ff-264">Toutes les applications basées sur HTTP qui utilisent des cookies doivent spécifier l’attribut HttpOnly dans la définition des cookies en implémentant la configuration suivante dans le fichier web.config :</span><span class="sxs-lookup"><span data-stu-id="b40ff-264">All HTTP-based applications that use cookies should specify HttpOnly in the cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="b40ff-265">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-265">Title</span></span>                   | <span data-ttu-id="b40ff-266">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-267">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-267">**Component**</span></span>               | <span data-ttu-id="b40ff-268">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-268">Web Application</span></span> | 
| <span data-ttu-id="b40ff-269">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-269">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-270">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-270">Build</span></span> |  
| <span data-ttu-id="b40ff-271">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-271">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-272">Web Forms</span><span class="sxs-lookup"><span data-stu-id="b40ff-272">Web Forms</span></span> |
| <span data-ttu-id="b40ff-273">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-273">**Attributes**</span></span>              | <span data-ttu-id="b40ff-274">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-274">N/A</span></span>  |
| <span data-ttu-id="b40ff-275">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-275">**References**</span></span>              | [<span data-ttu-id="b40ff-276">FormsAuthentication.RequireSSL Property (Propriété FormsAuthentication.RequireSSL)</span><span class="sxs-lookup"><span data-stu-id="b40ff-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="b40ff-277">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-277">**Steps**</span></span> | <span data-ttu-id="b40ff-278">La valeur de propriété RequireSSL est définie dans le fichier de configuration d’une application ASP.NET à l’aide de l’attribut requireSSL de l’élément de configuration.</span><span class="sxs-lookup"><span data-stu-id="b40ff-278">The RequireSSL property value is set in the configuration file for an ASP.NET application by using the requireSSL attribute of the configuration element.</span></span> <span data-ttu-id="b40ff-279">Dans le fichier web.config de votre application ASP.NET, vous pouvez définir l’attribut requireSSL afin de spécifier si le protocole SSL (Secure Sockets Layer) est requis pour renvoyer le cookie d’authentification par formulaire au serveur.</span><span class="sxs-lookup"><span data-stu-id="b40ff-279">You can specify in the Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required to return the forms-authentication cookie to the server by setting the requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="b40ff-280">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-280">Example</span></span> 
<span data-ttu-id="b40ff-281">L’exemple de code ci-après définit l’attribut requireSSL dans le fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="b40ff-281">The following code example sets the requireSSL attribute in the Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="b40ff-282">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-282">Title</span></span>                   | <span data-ttu-id="b40ff-283">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-284">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-284">**Component**</span></span>               | <span data-ttu-id="b40ff-285">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-285">Web Application</span></span> | 
| <span data-ttu-id="b40ff-286">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-286">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-287">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-287">Build</span></span> |  
| <span data-ttu-id="b40ff-288">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-288">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="b40ff-289">MVC5</span></span> |
| <span data-ttu-id="b40ff-290">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-290">**Attributes**</span></span>              | <span data-ttu-id="b40ff-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="b40ff-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="b40ff-292">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-292">**References**</span></span>              | [<span data-ttu-id="b40ff-293">Windows Identity Foundation (WIF) Configuration – Part II (Configuration de Windows Identity Foundation (WIF) - Partie II)</span><span class="sxs-lookup"><span data-stu-id="b40ff-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="b40ff-294">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-294">**Steps**</span></span> | <span data-ttu-id="b40ff-295">Pour définir l’attribut httpOnly pour les cookies FedAuth, définissez l’attribut hideFromCsript sur la valeur True.</span><span class="sxs-lookup"><span data-stu-id="b40ff-295">To set httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set to True.</span></span> |

### <a name="example"></a><span data-ttu-id="b40ff-296">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-296">Example</span></span>
<span data-ttu-id="b40ff-297">Le code ci-après présente la configuration appropriée :</span><span class="sxs-lookup"><span data-stu-id="b40ff-297">Following configuration shows the correct configuration:</span></span>
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

## <span data-ttu-id="b40ff-298"><a id="csrf-asp"></a>Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les pages web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b40ff-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="b40ff-299">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-299">Title</span></span>                   | <span data-ttu-id="b40ff-300">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-301">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-301">**Component**</span></span>               | <span data-ttu-id="b40ff-302">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-302">Web Application</span></span> | 
| <span data-ttu-id="b40ff-303">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-303">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-304">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-304">Build</span></span> |  
| <span data-ttu-id="b40ff-305">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-305">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-306">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-306">Generic</span></span> |
| <span data-ttu-id="b40ff-307">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-307">**Attributes**</span></span>              | <span data-ttu-id="b40ff-308">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-308">N/A</span></span>  |
| <span data-ttu-id="b40ff-309">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-309">**References**</span></span>              | <span data-ttu-id="b40ff-310">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-310">N/A</span></span>  |
| <span data-ttu-id="b40ff-311">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-311">**Steps**</span></span> | <span data-ttu-id="b40ff-312">La falsification de requête intersites (CSRF ou XSRF) est un type d’attaque dans lequel une personne malveillante peut exécuter des actions dans le contexte de sécurité de la session établie d’un autre utilisateur sur un site web.</span><span class="sxs-lookup"><span data-stu-id="b40ff-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="b40ff-313">L’objectif est de modifier ou de supprimer du contenu, si le site web ciblé s’appuie exclusivement sur les cookies de session pour authentifier la demande reçue.</span><span class="sxs-lookup"><span data-stu-id="b40ff-313">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="b40ff-314">Un attaquant pourrait exploiter cette faille de sécurité en faisant en sorte que le navigateur d’un autre utilisateur charge une URL avec une commande à partir d’un site vulnérable auquel l’utilisateur est déjà connecté.</span><span class="sxs-lookup"><span data-stu-id="b40ff-314">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="b40ff-315">Un attaquant dispose de nombreuses méthodes pour parvenir à ce résultat, notamment en hébergeant un autre site web qui charge une ressource à partir du serveur vulnérable, ou en incitant l’utilisateur à cliquer sur un lien.</span><span class="sxs-lookup"><span data-stu-id="b40ff-315">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="b40ff-316">Il est possible d’éviter cette attaque en faisant en sorte que le serveur envoie un jeton supplémentaire au client, qu’il demande au client d’inclure ce jeton dans toutes les demandes ultérieures et qu’il vérifie que toutes ces demandes comprennent un jeton s’appliquant à la session actuelle, par exemple en utilisant AntiForgeryToken ou ViewState ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b40ff-316">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="b40ff-317">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-317">Title</span></span>                   | <span data-ttu-id="b40ff-318">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-319">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-319">**Component**</span></span>               | <span data-ttu-id="b40ff-320">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-320">Web Application</span></span> | 
| <span data-ttu-id="b40ff-321">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-321">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-322">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-322">Build</span></span> |  
| <span data-ttu-id="b40ff-323">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-323">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="b40ff-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="b40ff-325">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-325">**Attributes**</span></span>              | <span data-ttu-id="b40ff-326">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-326">N/A</span></span>  |
| <span data-ttu-id="b40ff-327">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-327">**References**</span></span>              | [<span data-ttu-id="b40ff-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages (Prévention des attaques XSRF/CSRF dans les pages MVC et Web ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b40ff-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="b40ff-329">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-329">**Steps**</span></span> | <span data-ttu-id="b40ff-330">Formulaires anti-CSRF et MVC ASP.NET - Utilisez la méthode d’assistance `AntiForgeryToken` sur les vues ; placez un élément `Html.AntiForgeryToken()` dans le formulaire, par exemple,</span><span class="sxs-lookup"><span data-stu-id="b40ff-330">Anti-CSRF and ASP.NET MVC forms - Use the `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into the form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="b40ff-331">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="b40ff-332">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="b40ff-333">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-333">Example</span></span>
<span data-ttu-id="b40ff-334">Au même moment, Html.AntiForgeryToken() fournit au visiteur un cookie appelé __RequestVerificationToken, présentant la même valeur que la valeur masquée aléatoire indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b40ff-334">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="b40ff-335">Ensuite, pour valider une publication de formulaire entrante, ajoutez le filtre [ValidateAntiForgeryToken] à la méthode d’action cible.</span><span class="sxs-lookup"><span data-stu-id="b40ff-335">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="b40ff-336">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b40ff-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="b40ff-337">Un filtre d’autorisation qui vérifie les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b40ff-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="b40ff-338">La demande entrante comporte un cookie appelé __RequestVerificationToken.</span><span class="sxs-lookup"><span data-stu-id="b40ff-338">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="b40ff-339">La demande entrante comporte une entrée `Request.Form` appelée __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="b40ff-339">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="b40ff-340">Ce cookie et ces valeurs `Request.Form` correspondent. Si tout va bien, la demande s’exécute normalement.</span><span class="sxs-lookup"><span data-stu-id="b40ff-340">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="b40ff-341">Dans le cas contraire, un échec d’autorisation survient avec le message « Un jeton anti-contrefaçon requis n’a pas été fourni ou n’est pas valide ».</span><span class="sxs-lookup"><span data-stu-id="b40ff-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="b40ff-342">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-342">Example</span></span>
<span data-ttu-id="b40ff-343">Anti-CSRF et AJAX : le jeton de formulaire peut se révéler problématique pour les demandes AJAX, car une demande AJAX risque d’envoyer des données JSON, et non des données de formulaire HTML.</span><span class="sxs-lookup"><span data-stu-id="b40ff-343">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="b40ff-344">L’une des solutions consiste à envoyer les jetons dans un en-tête HTTP personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b40ff-344">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="b40ff-345">Le code ci-après utilise la syntaxe Razor pour générer les jetons, puis ajoute les jetons à une demande AJAX.</span><span class="sxs-lookup"><span data-stu-id="b40ff-345">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> 
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

### <a name="example"></a><span data-ttu-id="b40ff-346">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-346">Example</span></span>
<span data-ttu-id="b40ff-347">Lorsque vous traitez la demande, extrayez les jetons de l’en-tête de la demande.</span><span class="sxs-lookup"><span data-stu-id="b40ff-347">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="b40ff-348">Ensuite, appelez la méthode AntiForgery.Validate pour valider les jetons.</span><span class="sxs-lookup"><span data-stu-id="b40ff-348">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="b40ff-349">Si les jetons ne sont pas valides, la méthode Validate lève une exception.</span><span class="sxs-lookup"><span data-stu-id="b40ff-349">The Validate method throws an exception if the tokens are not valid.</span></span>
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

| <span data-ttu-id="b40ff-350">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-350">Title</span></span>                   | <span data-ttu-id="b40ff-351">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-352">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-352">**Component**</span></span>               | <span data-ttu-id="b40ff-353">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-353">Web Application</span></span> | 
| <span data-ttu-id="b40ff-354">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-354">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-355">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-355">Build</span></span> |  
| <span data-ttu-id="b40ff-356">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-356">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-357">Web Forms</span><span class="sxs-lookup"><span data-stu-id="b40ff-357">Web Forms</span></span> |
| <span data-ttu-id="b40ff-358">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-358">**Attributes**</span></span>              | <span data-ttu-id="b40ff-359">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-359">N/A</span></span>  |
| <span data-ttu-id="b40ff-360">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-360">**References**</span></span>              | [<span data-ttu-id="b40ff-361">Utilisation des fonctionnalités intégrées ASP.NET pour repousser les attaques Web</span><span class="sxs-lookup"><span data-stu-id="b40ff-361">Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="b40ff-362">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-362">**Steps**</span></span> | <span data-ttu-id="b40ff-363">Il est possible de prévenir les attaques CSRF dans les applications reposant sur WebForm en définissant l’élément ViewStateUserKey sur une chaîne aléatoire qui varie selon chaque utilisateur (identifiant utilisateur ou, mieux encore, identifiant de session).</span><span class="sxs-lookup"><span data-stu-id="b40ff-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey to a random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="b40ff-364">Pour un certain nombre de raisons techniques et sociales, l’identifiant de session constitue un bien meilleur choix, car ce type d’identifiant est imprévisible, arrive à expiration et varie selon chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b40ff-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="b40ff-365">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-365">Example</span></span>
<span data-ttu-id="b40ff-366">Voici le code qui doit apparaître dans toutes vos pages :</span><span class="sxs-lookup"><span data-stu-id="b40ff-366">Here's the code you need to have in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="b40ff-367"><a id="inactivity-lifetime"></a>Configurer la durée de vie d’inactivité d’une session</span><span class="sxs-lookup"><span data-stu-id="b40ff-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="b40ff-368">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-368">Title</span></span>                   | <span data-ttu-id="b40ff-369">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-370">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-370">**Component**</span></span>               | <span data-ttu-id="b40ff-371">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-371">Web Application</span></span> | 
| <span data-ttu-id="b40ff-372">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-372">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-373">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-373">Build</span></span> |  
| <span data-ttu-id="b40ff-374">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-374">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-375">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-375">Generic</span></span> |
| <span data-ttu-id="b40ff-376">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-376">**Attributes**</span></span>              | <span data-ttu-id="b40ff-377">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-377">N/A</span></span>  |
| <span data-ttu-id="b40ff-378">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-378">**References**</span></span>              | <span data-ttu-id="b40ff-379">[HttpSessionState.Timeout Property (Propriété HttpSessionState.Timeout)](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="b40ff-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="b40ff-380">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-380">**Steps**</span></span> | <span data-ttu-id="b40ff-381">Un événement d’expiration de session survient lorsqu’un utilisateur n’exécute aucune action sur un site web au cours d’un intervalle de temps donné (défini par le serveur web).</span><span class="sxs-lookup"><span data-stu-id="b40ff-381">Session timeout represents the event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="b40ff-382">Côté serveur, cet événement redéfinit l’état de la session utilisateur comme non valide (par exemple, « plus utilisé ») et demande au serveur web de détruire la session (en supprimant toutes les données qu’elle contient).</span><span class="sxs-lookup"><span data-stu-id="b40ff-382">The event, on server side, change the status of the user session to 'invalid' (for example  "not used anymore") and instruct the web server to destroy it (deleting all data contained into it).</span></span> <span data-ttu-id="b40ff-383">L’exemple de code ci-après définit l’attribut d’expiration de session sur 15 minutes dans le fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="b40ff-383">The following code example sets the timeout session attribute to 15 minutes in the Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="b40ff-384">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-384">Example</span></span>
<span data-ttu-id="b40ff-385">``\`Code XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="b40ff-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="b40ff-386">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-386">Title</span></span>                   | <span data-ttu-id="b40ff-387">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-388">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-388">**Component**</span></span>               | <span data-ttu-id="b40ff-389">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-389">Web Application</span></span> | 
| <span data-ttu-id="b40ff-390">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-390">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-391">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-391">Build</span></span> |  
| <span data-ttu-id="b40ff-392">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-392">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-393">Web Forms</span><span class="sxs-lookup"><span data-stu-id="b40ff-393">Web Forms</span></span> |
| <span data-ttu-id="b40ff-394">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-394">**Attributes**</span></span>              | <span data-ttu-id="b40ff-395">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-395">N/A</span></span>  |
| <span data-ttu-id="b40ff-396">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-396">**References**</span></span>              | <span data-ttu-id="b40ff-397">[forms, élément de authentication (Schéma des paramètres ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="b40ff-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="b40ff-398">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-398">**Steps**</span></span> | <span data-ttu-id="b40ff-399">Définissez le délai d’expiration du cookie du ticket d’authentification par formulaire sur 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="b40ff-399">Set the Forms Authentication Ticket cookie timeout to 15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="b40ff-400">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-400">Example</span></span>
<span data-ttu-id="b40ff-401">``\`Code XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="b40ff-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When the web application is Relying Party and ADFS is the STS, the lifetime of the authentication cookies - FedAuth tokens - can be set by the following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use the code below to enable encryption-decryption of claims received from ADFS. Thumbprint value varies based on the certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="b40ff-402">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-402">Example</span></span>
<span data-ttu-id="b40ff-403">Définissez également la durée de vie du jeton de revendication SAML émis par ADFS sur 15 minutes en exécutant la commande PowerShell ci-après sur le serveur ADFS :</span><span class="sxs-lookup"><span data-stu-id="b40ff-403">Also the ADFS issued SAML claim token's lifetime should be set to 15 minutes, by executing the following powershell command on the ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="b40ff-404"><a id="proper-app-logout"></a>Implémenter une déconnexion appropriée de l’application</span><span class="sxs-lookup"><span data-stu-id="b40ff-404"><a id="proper-app-logout"></a>Implement proper logout from the application</span></span>

| <span data-ttu-id="b40ff-405">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-405">Title</span></span>                   | <span data-ttu-id="b40ff-406">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-407">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-407">**Component**</span></span>               | <span data-ttu-id="b40ff-408">Application web</span><span class="sxs-lookup"><span data-stu-id="b40ff-408">Web Application</span></span> | 
| <span data-ttu-id="b40ff-409">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-409">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-410">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-410">Build</span></span> |  
| <span data-ttu-id="b40ff-411">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-411">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-412">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-412">Generic</span></span> |
| <span data-ttu-id="b40ff-413">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-413">**Attributes**</span></span>              | <span data-ttu-id="b40ff-414">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-414">N/A</span></span>  |
| <span data-ttu-id="b40ff-415">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-415">**References**</span></span>              | <span data-ttu-id="b40ff-416">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-416">N/A</span></span>  |
| <span data-ttu-id="b40ff-417">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-417">**Steps**</span></span> | <span data-ttu-id="b40ff-418">Effectuez une déconnexion appropriée de l’application lorsque l’utilisateur appuie sur le bouton de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="b40ff-418">Perform proper Sign Out from the application, when user presses log out button.</span></span> <span data-ttu-id="b40ff-419">Lors de la déconnexion, l’application doit détruire la session de l’utilisateur et également réinitialiser et annuler la valeur du cookie de session, ainsi que la valeur du cookie d’authentification.</span><span class="sxs-lookup"><span data-stu-id="b40ff-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="b40ff-420">En outre, lorsque plusieurs sessions sont associées à une seule identité d’utilisateur, elles doivent être terminées de manière collective côté serveur au moment de l’arrivée à expiration ou de la déconnexion.</span><span class="sxs-lookup"><span data-stu-id="b40ff-420">Also, when multiple sessions are tied to a single user identity, they must be collectively terminated on the server side at timeout or logout.</span></span> <span data-ttu-id="b40ff-421">Enfin, assurez-vous que la fonctionnalité de déconnexion est accessible sur chaque page.</span><span class="sxs-lookup"><span data-stu-id="b40ff-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="b40ff-422"><a id="csrf-api"></a>Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) sur les API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b40ff-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="b40ff-423">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-423">Title</span></span>                   | <span data-ttu-id="b40ff-424">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-425">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-425">**Component**</span></span>               | <span data-ttu-id="b40ff-426">API Web</span><span class="sxs-lookup"><span data-stu-id="b40ff-426">Web API</span></span> | 
| <span data-ttu-id="b40ff-427">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-427">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-428">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-428">Build</span></span> |  
| <span data-ttu-id="b40ff-429">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-429">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-430">Générique</span><span class="sxs-lookup"><span data-stu-id="b40ff-430">Generic</span></span> |
| <span data-ttu-id="b40ff-431">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-431">**Attributes**</span></span>              | <span data-ttu-id="b40ff-432">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-432">N/A</span></span>  |
| <span data-ttu-id="b40ff-433">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-433">**References**</span></span>              | <span data-ttu-id="b40ff-434">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-434">N/A</span></span>  |
| <span data-ttu-id="b40ff-435">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-435">**Steps**</span></span> | <span data-ttu-id="b40ff-436">La falsification de requête intersites (CSRF ou XSRF) est un type d’attaque dans lequel une personne malveillante peut exécuter des actions dans le contexte de sécurité de la session établie d’un autre utilisateur sur un site web.</span><span class="sxs-lookup"><span data-stu-id="b40ff-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="b40ff-437">L’objectif est de modifier ou de supprimer du contenu, si le site web ciblé s’appuie exclusivement sur les cookies de session pour authentifier la demande reçue.</span><span class="sxs-lookup"><span data-stu-id="b40ff-437">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="b40ff-438">Un attaquant pourrait exploiter cette faille de sécurité en faisant en sorte que le navigateur d’un autre utilisateur charge une URL avec une commande à partir d’un site vulnérable auquel l’utilisateur est déjà connecté.</span><span class="sxs-lookup"><span data-stu-id="b40ff-438">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="b40ff-439">Un attaquant dispose de nombreuses méthodes pour parvenir à ce résultat, notamment en hébergeant un autre site web qui charge une ressource à partir du serveur vulnérable, ou en incitant l’utilisateur à cliquer sur un lien.</span><span class="sxs-lookup"><span data-stu-id="b40ff-439">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="b40ff-440">Il est possible d’éviter cette attaque en faisant en sorte que le serveur envoie un jeton supplémentaire au client, qu’il demande au client d’inclure ce jeton dans toutes les demandes ultérieures et qu’il vérifie que toutes ces demandes comprennent un jeton s’appliquant à la session actuelle, par exemple en utilisant AntiForgeryToken ou ViewState ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b40ff-440">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="b40ff-441">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-441">Title</span></span>                   | <span data-ttu-id="b40ff-442">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-443">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-443">**Component**</span></span>               | <span data-ttu-id="b40ff-444">API Web</span><span class="sxs-lookup"><span data-stu-id="b40ff-444">Web API</span></span> | 
| <span data-ttu-id="b40ff-445">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-445">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-446">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-446">Build</span></span> |  
| <span data-ttu-id="b40ff-447">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-447">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="b40ff-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="b40ff-449">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-449">**Attributes**</span></span>              | <span data-ttu-id="b40ff-450">N/A</span><span class="sxs-lookup"><span data-stu-id="b40ff-450">N/A</span></span>  |
| <span data-ttu-id="b40ff-451">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-451">**References**</span></span>              | [<span data-ttu-id="b40ff-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API (Prévenir les attaques de falsification de requête intersites (CSRF, Cross Site Request Forgery) dans les API Web ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="b40ff-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="b40ff-453">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-453">**Steps**</span></span> | <span data-ttu-id="b40ff-454">Anti-CSRF et AJAX : le jeton de formulaire peut se révéler problématique pour les demandes AJAX, car une demande AJAX risque d’envoyer des données JSON, et non des données de formulaire HTML.</span><span class="sxs-lookup"><span data-stu-id="b40ff-454">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="b40ff-455">L’une des solutions consiste à envoyer les jetons dans un en-tête HTTP personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b40ff-455">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="b40ff-456">Le code ci-après utilise la syntaxe Razor pour générer les jetons, puis ajoute les jetons à une demande AJAX.</span><span class="sxs-lookup"><span data-stu-id="b40ff-456">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="b40ff-457">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-457">Example</span></span>
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

### <a name="example"></a><span data-ttu-id="b40ff-458">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-458">Example</span></span>
<span data-ttu-id="b40ff-459">Lorsque vous traitez la demande, extrayez les jetons de l’en-tête de la demande.</span><span class="sxs-lookup"><span data-stu-id="b40ff-459">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="b40ff-460">Ensuite, appelez la méthode AntiForgery.Validate pour valider les jetons.</span><span class="sxs-lookup"><span data-stu-id="b40ff-460">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="b40ff-461">Si les jetons ne sont pas valides, la méthode Validate lève une exception.</span><span class="sxs-lookup"><span data-stu-id="b40ff-461">The Validate method throws an exception if the tokens are not valid.</span></span>
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

### <a name="example"></a><span data-ttu-id="b40ff-462">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-462">Example</span></span>
<span data-ttu-id="b40ff-463">Formulaires anti-CSRF et MVC ASP.NET - Utilisez la méthode d’assistance AntiForgeryToken sur les vues ; placez un élément Html.AntiForgeryToken() dans le formulaire, par exemple,</span><span class="sxs-lookup"><span data-stu-id="b40ff-463">Anti-CSRF and ASP.NET MVC forms - Use the AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into the form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="b40ff-464">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-464">Example</span></span>
<span data-ttu-id="b40ff-465">Le résultat de l’exemple ci-dessus devrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b40ff-465">The example above will output something like the following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="b40ff-466">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-466">Example</span></span>
<span data-ttu-id="b40ff-467">Au même moment, Html.AntiForgeryToken() fournit au visiteur un cookie appelé __RequestVerificationToken, présentant la même valeur que la valeur masquée aléatoire indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b40ff-467">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="b40ff-468">Ensuite, pour valider une publication de formulaire entrante, ajoutez le filtre [ValidateAntiForgeryToken] à la méthode d’action cible.</span><span class="sxs-lookup"><span data-stu-id="b40ff-468">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="b40ff-469">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b40ff-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="b40ff-470">Un filtre d’autorisation qui vérifie les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b40ff-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="b40ff-471">La demande entrante comporte un cookie appelé __RequestVerificationToken.</span><span class="sxs-lookup"><span data-stu-id="b40ff-471">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="b40ff-472">La demande entrante comporte une entrée `Request.Form` appelée __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="b40ff-472">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="b40ff-473">Ce cookie et ces valeurs `Request.Form` correspondent. Si tout va bien, la demande s’exécute normalement.</span><span class="sxs-lookup"><span data-stu-id="b40ff-473">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="b40ff-474">Dans le cas contraire, un échec d’autorisation survient avec le message « Un jeton anti-contrefaçon requis n’a pas été fourni ou n’est pas valide ».</span><span class="sxs-lookup"><span data-stu-id="b40ff-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="b40ff-475">Intitulé</span><span class="sxs-lookup"><span data-stu-id="b40ff-475">Title</span></span>                   | <span data-ttu-id="b40ff-476">Détails</span><span class="sxs-lookup"><span data-stu-id="b40ff-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="b40ff-477">**Composant**</span><span class="sxs-lookup"><span data-stu-id="b40ff-477">**Component**</span></span>               | <span data-ttu-id="b40ff-478">API Web</span><span class="sxs-lookup"><span data-stu-id="b40ff-478">Web API</span></span> | 
| <span data-ttu-id="b40ff-479">**Phase SDL**</span><span class="sxs-lookup"><span data-stu-id="b40ff-479">**SDL Phase**</span></span>               | <span data-ttu-id="b40ff-480">Créer</span><span class="sxs-lookup"><span data-stu-id="b40ff-480">Build</span></span> |  
| <span data-ttu-id="b40ff-481">**Technologies applicables**</span><span class="sxs-lookup"><span data-stu-id="b40ff-481">**Applicable Technologies**</span></span> | <span data-ttu-id="b40ff-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="b40ff-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="b40ff-483">**Attributs**</span><span class="sxs-lookup"><span data-stu-id="b40ff-483">**Attributes**</span></span>              | <span data-ttu-id="b40ff-484">Fournisseur d’identité - ADFS, Fournisseur d’identité - Azure AD</span><span class="sxs-lookup"><span data-stu-id="b40ff-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="b40ff-485">**Informations de référence**</span><span class="sxs-lookup"><span data-stu-id="b40ff-485">**References**</span></span>              | [<span data-ttu-id="b40ff-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2 (Sécuriser une API Web avec des comptes individuels et une connexion locale dans API Web ASP.NET 2.2)</span><span class="sxs-lookup"><span data-stu-id="b40ff-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="b40ff-487">**Étapes**</span><span class="sxs-lookup"><span data-stu-id="b40ff-487">**Steps**</span></span> | <span data-ttu-id="b40ff-488">Si l’API Web est sécurisée à l’aide d’OAuth 2.0, elle attend un jeton du porteur dans l’en-tête de la demande d’autorisation et n’accorde l’accès à la demande que si le jeton est valide.</span><span class="sxs-lookup"><span data-stu-id="b40ff-488">If the Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access to the request only if the token is valid.</span></span> <span data-ttu-id="b40ff-489">Contrairement à l’authentification basée sur les cookies, les navigateurs n’attachent pas les jetons du porteur aux demandes.</span><span class="sxs-lookup"><span data-stu-id="b40ff-489">Unlike cookie based authentication, browsers do not attach the bearer tokens to requests.</span></span> <span data-ttu-id="b40ff-490">Le client effectuant la demande doit attacher explicitement le jeton du porteur dans l’en-tête de la demande.</span><span class="sxs-lookup"><span data-stu-id="b40ff-490">The requesting client needs to explicitly attach the bearer token in the request header.</span></span> <span data-ttu-id="b40ff-491">Par conséquent, dans le cas des API Web ASP.NET protégées à l’aide d’OAuth 2.0, les jetons du porteur sont considérés comme un moyen de défense contre les attaques CSRF.</span><span class="sxs-lookup"><span data-stu-id="b40ff-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="b40ff-492">Notez que si la partie MVC de l’application utilise l’authentification par formulaire (autrement dit, des cookies), l’application web MVC doit recourir à des jetons anti-contrefaçon.</span><span class="sxs-lookup"><span data-stu-id="b40ff-492">Please note that if the MVC portion of the application uses forms authentication (i.e., uses cookies), anti-forgery tokens have to be used by the MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="b40ff-493">Exemple</span><span class="sxs-lookup"><span data-stu-id="b40ff-493">Example</span></span>
<span data-ttu-id="b40ff-494">L’API Web doit être informée qu’elle doit UNIQUEMENT se fier aux jetons du porteur, et non aux cookies.</span><span class="sxs-lookup"><span data-stu-id="b40ff-494">The Web API has to be informed to rely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="b40ff-495">Vous pouvez obtenir ce résultat à l’aide de la configuration ci-après dans la méthode `WebApiConfig.Register` : ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="b40ff-495">It can be done by the following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
The SuppressDefaultHostAuthentication method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API to authenticate only using bearer tokens.