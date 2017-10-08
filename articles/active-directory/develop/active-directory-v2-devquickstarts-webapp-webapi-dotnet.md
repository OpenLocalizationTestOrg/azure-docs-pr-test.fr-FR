---
title: aaaAzure AD v2.0 .NET web application appelant API est prise en main | Documents Microsoft
description: "Comment toobuild application Web MVC .NET qui appelle web services à l’aide de Microsoft personnel des comptes et de travail ou d’établissement scolaire pour la connexion."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="bcfee-103">Appeler une API web à partir d’une application web .NET</span><span class="sxs-lookup"><span data-stu-id="bcfee-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="bcfee-104">Avec le point de terminaison hello v2.0, vous pouvez rapidement ajouter des applications web d’authentification tooyour et API web avec prise en charge pour les deux comptes personnels de Microsoft et comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="bcfee-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="bcfee-105">Ici, nous allons créer une application web MVC qui connecte les utilisateurs à l’aide d’OpenID Connect, avec l’aide de l’intergiciel OWIN de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bcfee-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="bcfee-106">Hello web application sera obtenir des jetons d’accès OAuth 2.0 pour un site web api sécurisée par OAuth 2.0 qui permet de créer, lire et supprimer un utilisateur donné « liste des tâches ».</span><span class="sxs-lookup"><span data-stu-id="bcfee-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="bcfee-107">Ce didacticiel est concentrer principalement sur l’utilisation de MSAL tooacquire et utilise des jetons d’accès dans une application web, une description complète [ici](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="bcfee-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="bcfee-108">En tant que composants requis, vous souhaiterez peut-être toofirst apprendre comment trop[ajouter une application web de base connectez-vous tooa](active-directory-v2-devquickstarts-dotnet-web.md) ou comment trop[sécuriser correctement une API web](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="bcfee-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bcfee-109">Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="bcfee-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="bcfee-110">toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="bcfee-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="bcfee-111">Télécharger l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="bcfee-111">Download sample code</span></span>
<span data-ttu-id="bcfee-112">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="bcfee-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="bcfee-113">toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="bcfee-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="bcfee-114">Vous pouvez également [télécharger une application hello terminée comme un fichier zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ou le clonage d’application hello terminée :</span><span class="sxs-lookup"><span data-stu-id="bcfee-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="bcfee-115">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="bcfee-115">Register an app</span></span>
<span data-ttu-id="bcfee-116">Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="bcfee-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="bcfee-117">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="bcfee-117">Make sure to:</span></span>

* <span data-ttu-id="bcfee-118">Copie vers le bas hello **Id d’Application** affecté tooyour application, vous en aurez besoin plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="bcfee-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="bcfee-119">Créer un **Secret d’application** Hello **mot de passe** type et copie vers le bas de sa valeur pour une date ultérieure</span><span class="sxs-lookup"><span data-stu-id="bcfee-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="bcfee-120">Ajouter hello **Web** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="bcfee-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="bcfee-121">Entrez hello correct **URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="bcfee-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="bcfee-122">uri de redirection Hello indique tooAzure AD dans lequel les réponses d’authentification doivent être dirigées - valeur par défaut de hello pour ce didacticiel est `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="bcfee-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="bcfee-123">Installer OWIN</span><span class="sxs-lookup"><span data-stu-id="bcfee-123">Install OWIN</span></span>
<span data-ttu-id="bcfee-124">Ajouter hello OWIN intergiciel (middleware) NuGet packages toohello `TodoList-WebApp` projet à l’aide de hello Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="bcfee-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="bcfee-125">intergiciel (middleware) OWIN de Hello est tooissue utilisé les demandes de connexion et déconnexion, gérer la session de l’utilisateur hello et obtenir des informations sur l’utilisateur hello, entre autres.</span><span class="sxs-lookup"><span data-stu-id="bcfee-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="bcfee-126">Utilisateur de hello signe dans</span><span class="sxs-lookup"><span data-stu-id="bcfee-126">Sign hello user in</span></span>
<span data-ttu-id="bcfee-127">À présent configurer Bonjour OWIN intergiciel (middleware) toouse Bonjour [protocole d’authentification OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="bcfee-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="bcfee-128">Ouvrez hello `web.config` fichier racine hello hello `TodoList-WebApp` le projet, puis entrez les valeurs de configuration de votre application Bonjour `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="bcfee-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="bcfee-129">Hello `ida:ClientId` est hello **Id d’Application** affecté application tooyour dans le portail de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="bcfee-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="bcfee-130">Hello `ida:ClientSecret` est hello **Secret d’application** vous avez créé dans le portail de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="bcfee-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="bcfee-131">Hello `ida:RedirectUri` est hello **Uri de redirection** vous avez entré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfee-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="bcfee-132">Ouvrez hello `web.config` fichier racine hello hello `TodoList-Service` le projet, puis remplacez hello `ida:Audience` avec hello même **Id d’Application** comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="bcfee-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="bcfee-133">Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et ajoutez `using` instructions pour les bibliothèques hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="bcfee-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="bcfee-134">Dans l’hello du même fichier, implémenter hello `ConfigureAuth(...)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="bcfee-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="bcfee-135">Hello les paramètres que vous fournissez dans `OpenIDConnectAuthenticationOptions` servira de coordonnées pour toocommunicate de votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bcfee-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="bcfee-136">Utiliser des jetons d’accès MSAL tooget</span><span class="sxs-lookup"><span data-stu-id="bcfee-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="bcfee-137">Bonjour `AuthorizationCodeReceived` notification, nous souhaitons toouse [OAuth 2.0 en tandem avec OpenID Connect](active-directory-v2-protocols.md) authorization_code de hello tooredeem pour un toohello de jeton d’accès Service de liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="bcfee-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="bcfee-138">La bibliothèque MSAL peut vous faciliter ce processus :</span><span class="sxs-lookup"><span data-stu-id="bcfee-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="bcfee-139">Pour commencer, installez hello préversion de MSAL :</span><span class="sxs-lookup"><span data-stu-id="bcfee-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="bcfee-140">Et ajouter un autre `using` instruction toohello `App_Start\Startup.Auth.cs` fichier MSAL.</span><span class="sxs-lookup"><span data-stu-id="bcfee-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="bcfee-141">Maintenant ajouter une nouvelle méthode hello `OnAuthorizationCodeReceived` Gestionnaire d’événements.</span><span class="sxs-lookup"><span data-stu-id="bcfee-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="bcfee-142">Ce gestionnaire utilisera MSAL tooacquire un toohello de jeton d’accès API de liste de tâches et stocke le jeton de hello dans le cache de jeton de MSAL pour une date ultérieure :</span><span class="sxs-lookup"><span data-stu-id="bcfee-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="bcfee-143">Dans les applications web, MSAL a un cache de jeton extensible qui peut être des jetons de toostore utilisé.</span><span class="sxs-lookup"><span data-stu-id="bcfee-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="bcfee-144">Cet exemple implémente hello `NaiveSessionCache` qui utilise des jetons de toocache de stockage de session http.</span><span class="sxs-lookup"><span data-stu-id="bcfee-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="bcfee-145">Appel hello API Web</span><span class="sxs-lookup"><span data-stu-id="bcfee-145">Call hello Web API</span></span>
<span data-ttu-id="bcfee-146">Il est maintenant temps tooactually utiliser access_token hello vous avez acquis à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="bcfee-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="bcfee-147">L’application hello ouvrir web `Controllers\TodoListController.cs` de fichiers, ce qui rend tous les hello CRUD demande toohello API de liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="bcfee-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="bcfee-148">Vous pouvez utiliser MSAL à nouveau ici access_tokens toofetch de hello du cache MSAL.</span><span class="sxs-lookup"><span data-stu-id="bcfee-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="bcfee-149">Tout d’abord, ajoutez un `using` instruction pour MSAL toothis fichier.</span><span class="sxs-lookup"><span data-stu-id="bcfee-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="bcfee-150">Bonjour `Index` , MSAL d’utiliser l’action `AcquireTokenSilentAsync` méthode tooget un access_token qui peuvent être utilisés tooread des données à partir de hello service de liste de tâches :</span><span class="sxs-lookup"><span data-stu-id="bcfee-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="bcfee-151">Hello exemple puis ajoute demande hello obtenue toohello jeton HTTP GET comme hello `Authorization` en-tête, le service de liste de tâches hello utilise la demande de hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="bcfee-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="bcfee-152">Si hello service de liste de tâches renvoie un `401 Unauthorized` réponse, access_tokens hello dans MSAL sont devenues non valides pour une raison quelconque.</span><span class="sxs-lookup"><span data-stu-id="bcfee-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="bcfee-153">Dans ce cas, vous devez supprimer n’importe quel access_tokens de hello du cache MSAL et afficher les utilisateur hello un message qu’ils peuvent avoir besoin toosign dans là encore, ce qui va redémarrer le flux d’acquisition de jeton hello.</span><span class="sxs-lookup"><span data-stu-id="bcfee-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* <span data-ttu-id="bcfee-154">De même, si MSAL est impossible de tooreturn un access_token pour une raison quelconque, vous devez demander à nouveau toosign d’utilisateur hello dans.</span><span class="sxs-lookup"><span data-stu-id="bcfee-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="bcfee-155">Cette opération n’est pas plus compliquée que la récupération d’un élément `MSALException` :</span><span class="sxs-lookup"><span data-stu-id="bcfee-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="bcfee-156">Hello exacte même `AcquireTokenSilentAsync` appel est implementd Bonjour `Create` et `Delete` actions.</span><span class="sxs-lookup"><span data-stu-id="bcfee-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="bcfee-157">Dans les applications web, vous pouvez utiliser cette access_tokens de tooget MSAL méthode chaque fois que vous avez besoin dans votre application.</span><span class="sxs-lookup"><span data-stu-id="bcfee-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="bcfee-158">MSAL se charge de l’acquisition, de la mise en cache et de l’actualisation des jetons.</span><span class="sxs-lookup"><span data-stu-id="bcfee-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="bcfee-159">Enfin, générez et exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="bcfee-159">Finally, build and run your app!</span></span>  <span data-ttu-id="bcfee-160">Connectez-vous avec un Account Microsoft ou un compte Azure et notez comment l’identité d’utilisateur hello est reflétée dans la barre de navigation supérieure hello.</span><span class="sxs-lookup"><span data-stu-id="bcfee-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="bcfee-161">Ajouter et supprimer des éléments à partir de la liste des tâches de l’utilisateur hello hello toosee Qu'oauth 2.0 sécurisés API appelle en action.</span><span class="sxs-lookup"><span data-stu-id="bcfee-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="bcfee-162">Vous disposez désormais d’une application Web et d’une API Web, toutes deux sécurisées à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.</span><span class="sxs-lookup"><span data-stu-id="bcfee-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="bcfee-163">Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fourni ici](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="bcfee-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="bcfee-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcfee-164">Next Steps</span></span>
<span data-ttu-id="bcfee-165">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="bcfee-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="bcfee-166">guide du développeur v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="bcfee-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="bcfee-167">Balise StackOverflow "azure-active-directory" &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="bcfee-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="bcfee-168">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="bcfee-168">Get security updates for our products</span></span>
<span data-ttu-id="bcfee-169">Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="bcfee-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

