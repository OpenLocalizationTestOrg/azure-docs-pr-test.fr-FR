---
title: "Prise en main de l’appel d’API dans les applications web Azure AD v2.0 .NET | Microsoft Docs"
description: "Comment créer une application Web .NET MVC qui appelle des services Web à l’aide de comptes personnels Microsoft et de comptes professionnels ou scolaires pour la connexion."
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
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="255f9-103">Appeler une API web à partir d’une application web .NET</span><span class="sxs-lookup"><span data-stu-id="255f9-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="255f9-104">Avec le point de terminaison v2.0, vous pouvez rapidement ajouter une authentification à vos applications Web et à vos API Web, avec prise en charge pour les comptes Microsoft personnels, ainsi que pour les comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="255f9-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="255f9-105">Ici, nous allons créer une application web MVC qui connecte les utilisateurs à l’aide d’OpenID Connect, avec l’aide de l’intergiciel OWIN de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="255f9-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="255f9-106">L’application web obtiendra des jetons d’accès OAuth 2.0 pour une API web sécurisée par OAuth 2.0 qui permet d’exécuter des opérations de création, lecture et suppression dans la « To Do List » (Liste des tâches) d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="255f9-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="255f9-107">Ce didacticiel s’intéresse principalement à l’utilisation de la bibliothèque MSAL pour récupérer et utiliser des jetons d’accès dans une application Web, dont la description complète est disponible [ici](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="255f9-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="255f9-108">Afin de vous renseigner sur la configuration requise, apprenez dans un premier temps comment [ajouter une connexion de base à une application Web](active-directory-v2-devquickstarts-dotnet-web.md) ou comment [sécuriser une application Web de manière appropriée](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="255f9-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="255f9-109">Les scénarios et les fonctionnalités Azure Active Directory ne sont pas tous pris en charge par le point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="255f9-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="255f9-110">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limites de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="255f9-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="255f9-111">Télécharger l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="255f9-111">Download sample code</span></span>
<span data-ttu-id="255f9-112">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="255f9-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="255f9-113">Pour suivre la procédure, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) ou la cloner :</span><span class="sxs-lookup"><span data-stu-id="255f9-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="255f9-114">Vous pouvez également [télécharger l'application terminée dans un fichier zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ou cloner l'application terminée :</span><span class="sxs-lookup"><span data-stu-id="255f9-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="255f9-115">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="255f9-115">Register an app</span></span>
<span data-ttu-id="255f9-116">Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="255f9-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="255f9-117">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="255f9-117">Make sure to:</span></span>

* <span data-ttu-id="255f9-118">copier l' **ID d'application** attribué à votre application, vous en aurez bientôt besoin ;</span><span class="sxs-lookup"><span data-stu-id="255f9-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="255f9-119">créer un **secret d’application** du type **Mot de passe**, puis copiez sa valeur pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="255f9-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="255f9-120">Ajoutez la plate-forme **Web** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="255f9-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="255f9-121">entrer l’ **URI de redirection**approprié.</span><span class="sxs-lookup"><span data-stu-id="255f9-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="255f9-122">L’URI de redirection indique à Azure AD où les réponses d’authentification doivent être dirigées. La valeur par défaut pour ce didacticiel est `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="255f9-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="255f9-123">Installer OWIN</span><span class="sxs-lookup"><span data-stu-id="255f9-123">Install OWIN</span></span>
<span data-ttu-id="255f9-124">Ajoutez au projet `TodoList-WebApp` les packages NuGet de l’intergiciel OWIN à l’aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="255f9-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="255f9-125">L’intergiciel OWIN sera utilisé pour émettre des demandes de connexion et de déconnexion, gérer la session utilisateur et obtenir des informations concernant l’utilisateur, entre autres.</span><span class="sxs-lookup"><span data-stu-id="255f9-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="255f9-126">Connexion de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="255f9-126">Sign the user in</span></span>
<span data-ttu-id="255f9-127">À présent, configurez l’intergiciel OWIN pour utiliser le [protocole d’authentification OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="255f9-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="255f9-128">Ouvrez le fichier `web.config` à la racine du projet `TodoList-WebApp`, puis entrez les valeurs de configuration de votre application dans la section `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="255f9-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="255f9-129">L’élément `ida:ClientId` est l’ **ID d’application** affecté à votre application dans le portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="255f9-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="255f9-130">L’élément `ida:ClientSecret` est le **secret d’application** que vous avez créé dans le portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="255f9-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="255f9-131">L’élément `ida:RedirectUri` est l’ **URI de redirection** que vous avez saisi dans le portail.</span><span class="sxs-lookup"><span data-stu-id="255f9-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="255f9-132">Ouvrez le fichier `web.config` dans la racine du projet `TodoList-Service`, puis remplacez l’élément `ida:Audience` par **l’ID d’application** ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="255f9-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="255f9-133">Ouvrez le fichier `App_Start\Startup.Auth.cs`, puis ajoutez les instructions `using` pour les bibliothèques ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="255f9-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="255f9-134">Dans le même fichier, implémentez la méthode `ConfigureAuth(...)` .</span><span class="sxs-lookup"><span data-stu-id="255f9-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="255f9-135">Les paramètres que vous fournissez dans `OpenIDConnectAuthenticationOptions` serviront de coordonnées pour que votre application puisse communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="255f9-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="255f9-136">Utilisation de la bibliothèque MSAL pour obtenir des jetons d’accès</span><span class="sxs-lookup"><span data-stu-id="255f9-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="255f9-137">Dans la notification `AuthorizationCodeReceived`, nous souhaitons utiliser [OAuth 2.0 en tandem avec OpenID Connect](active-directory-v2-protocols.md) afin d’échanger le code d’autorisation contre un jeton d’accès au service de la liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="255f9-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="255f9-138">La bibliothèque MSAL peut vous faciliter ce processus :</span><span class="sxs-lookup"><span data-stu-id="255f9-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="255f9-139">Tout d’abord, installez la version d’évaluation de MSAL :</span><span class="sxs-lookup"><span data-stu-id="255f9-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="255f9-140">Puis, ajoutez une autre instruction `using` au fichier `App_Start\Startup.Auth.cs` pour MSAL.</span><span class="sxs-lookup"><span data-stu-id="255f9-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="255f9-141">Vous pouvez alors ajouter une nouvelle méthode, le gestionnaire d’événements `OnAuthorizationCodeReceived`.</span><span class="sxs-lookup"><span data-stu-id="255f9-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="255f9-142">Ce gestionnaire utilisera MSAL pour acquérir un jeton d’accès à l’API To-Do List et le stockera dans le cache de jetons MSAL pour une utilisation ultérieure :</span><span class="sxs-lookup"><span data-stu-id="255f9-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="255f9-143">Dans les applications Web, MSAL dispose d’un cache de jeton extensible pouvant être utilisé pour stocker les jetons.</span><span class="sxs-lookup"><span data-stu-id="255f9-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="255f9-144">Cet exemple implémente l’élément `NaiveSessionCache` qui utilise le stockage de session HTTP pour mettre en cache les jetons.</span><span class="sxs-lookup"><span data-stu-id="255f9-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="255f9-145">Appel de l’API web</span><span class="sxs-lookup"><span data-stu-id="255f9-145">Call the Web API</span></span>
<span data-ttu-id="255f9-146">Il est à présent temps d’utiliser le jeton d’accès acquis lors de l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="255f9-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="255f9-147">Ouvrez le fichier `Controllers\TodoListController.cs` de l’application web, qui exécute l’ensemble des requêtes CRUD sur l’API To-Do List.</span><span class="sxs-lookup"><span data-stu-id="255f9-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="255f9-148">Vous pouvez réutiliser MSAL afin de récupérer les jetons d’accès du cache MSAL.</span><span class="sxs-lookup"><span data-stu-id="255f9-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="255f9-149">Tout d’abord, ajoutez une instruction `using` pour MSAL dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="255f9-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="255f9-150">Dans l’action `Index`, utilisez la méthode `AcquireTokenSilentAsync` de MSAL pour obtenir un jeton d’accès pouvant être utilisé pour lire les données du service de la liste des tâches :</span><span class="sxs-lookup"><span data-stu-id="255f9-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="255f9-151">L’exemple ajoute ensuite le jeton obtenu à la requête GET HTTP en tant qu’en-tête `Authorization`, que le service de la liste des tâches utilise pour authentifier la requête.</span><span class="sxs-lookup"><span data-stu-id="255f9-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="255f9-152">Si le service To-Do List renvoie une réponse `401 Unauthorized`, les jetons d’accès de MSAL deviennent non valides, pour une raison indéterminée.</span><span class="sxs-lookup"><span data-stu-id="255f9-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="255f9-153">Dans ce cas, vous devez abandonner les jetons d’accès du cache MSAL et transmettre à l’utilisateur un message lui demandant de se reconnecter. Le cas échéant, le flux d’acquisition des jetons est redémarré.</span><span class="sxs-lookup"><span data-stu-id="255f9-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="255f9-154">De la même manière, si MSAL est dans l’impossibilité de renvoyer un jeton d’accès, pour quelque raison que ce soit, vous devez demander à l’utilisateur de se reconnecter.</span><span class="sxs-lookup"><span data-stu-id="255f9-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="255f9-155">Cette opération n’est pas plus compliquée que la récupération d’un élément `MSALException` :</span><span class="sxs-lookup"><span data-stu-id="255f9-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="255f9-156">Le même appel `AcquireTokenSilentAsync` est implémenté dans les actions `Create` et `Delete`.</span><span class="sxs-lookup"><span data-stu-id="255f9-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="255f9-157">Dans les applications Web, vous pouvez utiliser cette méthode MSAL pour obtenir les jetons d’accès lorsque vous en avez besoin dans votre application.</span><span class="sxs-lookup"><span data-stu-id="255f9-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="255f9-158">MSAL se charge de l’acquisition, de la mise en cache et de l’actualisation des jetons.</span><span class="sxs-lookup"><span data-stu-id="255f9-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="255f9-159">Enfin, générez et exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="255f9-159">Finally, build and run your app!</span></span>  <span data-ttu-id="255f9-160">Connectez-vous avec un compte Microsoft ou un compte Azure AD, et prenez note du mode d’indication de l’identité de l’utilisateur dans la barre de navigation supérieure.</span><span class="sxs-lookup"><span data-stu-id="255f9-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="255f9-161">Ajoutez et supprimez certains éléments de la liste de tâches de l’utilisateur afin d’observer les appels d’API sécurisés OAuth 2.0 en action.</span><span class="sxs-lookup"><span data-stu-id="255f9-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="255f9-162">Vous disposez désormais d’une application Web et d’une API Web, toutes deux sécurisées à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.</span><span class="sxs-lookup"><span data-stu-id="255f9-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="255f9-163">Pour référence, l’exemple terminé (sans vos valeurs de configuration) [est fourni ici](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="255f9-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="255f9-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="255f9-164">Next Steps</span></span>
<span data-ttu-id="255f9-165">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="255f9-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="255f9-166">Guide du développeur 2.0 >></span><span class="sxs-lookup"><span data-stu-id="255f9-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="255f9-167">Balise StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="255f9-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="255f9-168">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="255f9-168">Get security updates for our products</span></span>
<span data-ttu-id="255f9-169">Nous vous encourageons à activer les notifications d’incidents de sécurité en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et en vous abonnant aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="255f9-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

