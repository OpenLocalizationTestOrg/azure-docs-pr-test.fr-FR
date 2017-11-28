---
title: Prise en main de la connexion aux applications web Azure AD v2.0 .NET | Microsoft Docs
description: "Génération d’une application web .NET MVC qui connecte les utilisateurs à l’aide de leur compte Microsoft personnel et de leur compte professionnel ou scolaire."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="6bb31-103">Ajouter une connexion à une application Web MVC .NET</span><span class="sxs-lookup"><span data-stu-id="6bb31-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="6bb31-104">Avec le point de terminaison v2.0, vous pouvez rapidement ajouter une authentification à vos applications web, avec prise en charge des comptes Microsoft personnels et des comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="6bb31-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="6bb31-105">Dans les applications web ASP.NET, vous pouvez y parvenir en utilisant l’intergiciel OWIN de Microsoft inclus dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="6bb31-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="6bb31-106">Les scénarios et les fonctionnalités Azure Active Directory ne sont pas tous pris en charge par le point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="6bb31-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="6bb31-107">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limites de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="6bb31-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="6bb31-108">Nous allons créer une application Web qui utilise OWIN pour connecter l’utilisateur, afficher des informations sur l’utilisateur et déconnecter l’utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="6bb31-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="6bb31-109">Télécharger</span><span class="sxs-lookup"><span data-stu-id="6bb31-109">Download</span></span>
<span data-ttu-id="6bb31-110">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="6bb31-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="6bb31-111">Pour suivre la procédure, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou la cloner :</span><span class="sxs-lookup"><span data-stu-id="6bb31-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="6bb31-112">L'application terminée est également fournie à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6bb31-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="6bb31-113">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="6bb31-113">Register an app</span></span>
<span data-ttu-id="6bb31-114">Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6bb31-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="6bb31-115">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="6bb31-115">Make sure to:</span></span>

* <span data-ttu-id="6bb31-116">copier l' **ID d'application** attribué à votre application, vous en aurez bientôt besoin ;</span><span class="sxs-lookup"><span data-stu-id="6bb31-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="6bb31-117">Ajoutez la plate-forme **Web** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="6bb31-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="6bb31-118">entrer l’ **URI de redirection**approprié.</span><span class="sxs-lookup"><span data-stu-id="6bb31-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="6bb31-119">L’URI de redirection indique à Azure AD où les réponses d’authentification doivent être dirigées. La valeur par défaut pour ce didacticiel est `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="6bb31-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="6bb31-120">Installer et configurer l’authentification OWIN</span><span class="sxs-lookup"><span data-stu-id="6bb31-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="6bb31-121">Ici, nous allons configurer l’intergiciel OWIN pour utiliser le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6bb31-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="6bb31-122">OWIN sera utilisé pour émettre des demandes de connexion et de déconnexion, gérer la session utilisateur et obtenir des informations concernant l’utilisateur, entre autres.</span><span class="sxs-lookup"><span data-stu-id="6bb31-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="6bb31-123">Pour commencer, ouvrez le fichier `web.config` dans la racine du projet, puis entrez les valeurs de configuration de votre application dans la section `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="6bb31-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="6bb31-124">L’élément `ida:ClientId` est l’ **ID d’application** affecté à votre application dans le portail d’inscription.</span><span class="sxs-lookup"><span data-stu-id="6bb31-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="6bb31-125">L’élément `ida:RedirectUri` est l’ **URI de redirection** que vous avez saisi dans le portail.</span><span class="sxs-lookup"><span data-stu-id="6bb31-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="6bb31-126">Ajoutez ensuite les packages NuGet d'intergiciel (middleware) OWIN au projet à l'aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="6bb31-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="6bb31-127">Ajoutez une classe de démarrage OWIN au projet nommé `Startup.cs` Cliquez avec le bouton droit sur le projet --> **Ajouter** --> **Nouvel élément** --> Recherchez « OWIN ».</span><span class="sxs-lookup"><span data-stu-id="6bb31-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="6bb31-128">L’intergiciel OWIN appelle la méthode `Configuration(...)` lorsque votre application démarre.</span><span class="sxs-lookup"><span data-stu-id="6bb31-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="6bb31-129">Modifiez la déclaration de classe en `public partial class Startup`. Nous avons déjà mis en œuvre une partie de cette classe pour vous, dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="6bb31-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="6bb31-130">Dans la méthode `Configuration(...)`, appelez ConfigureAuth(...) pour configurer l’authentification de votre application web.</span><span class="sxs-lookup"><span data-stu-id="6bb31-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. <span data-ttu-id="6bb31-131">Ouvrez le fichier `App_Start\Startup.Auth.cs` et implémentez la méthode `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="6bb31-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="6bb31-132">Les paramètres que vous fournissez dans `OpenIdConnectAuthenticationOptions` serviront de coordonnées pour que votre application puisse communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bb31-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="6bb31-133">Vous devrez également configurer l’authentification des cookies ; l’intergiciel OpenID Connect utilise des cookies en coulisses.</span><span class="sxs-lookup"><span data-stu-id="6bb31-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

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
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a><span data-ttu-id="6bb31-134">Envoi de demandes d’authentification</span><span class="sxs-lookup"><span data-stu-id="6bb31-134">Send authentication requests</span></span>
<span data-ttu-id="6bb31-135">Votre application est maintenant correctement configurée pour communiquer avec le point de terminaison v2.0 en utilisant le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6bb31-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="6bb31-136">OWIN a pris en charge tous les détails déplaisants de la création de messages d’authentification, de la validation des jetons d’Azure AD et de la gestion des sessions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6bb31-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="6bb31-137">Il ne reste qu’à offrir aux utilisateurs un moyen de se connecter et de se déconnecter.</span><span class="sxs-lookup"><span data-stu-id="6bb31-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="6bb31-138">Vous pouvez utiliser des balises autorisées dans vos contrôleurs pour exiger que l’utilisateur se connecte avant d’accéder à une page donnée.</span><span class="sxs-lookup"><span data-stu-id="6bb31-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="6bb31-139">Ouvrez `Controllers\HomeController.cs` et ajoutez la balise `[Authorize]` au contrôleur About.</span><span class="sxs-lookup"><span data-stu-id="6bb31-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="6bb31-140">Vous pouvez également utiliser OWIN pour émettre des demandes d’authentification provenant directement de votre code.</span><span class="sxs-lookup"><span data-stu-id="6bb31-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="6bb31-141">Ouvrez `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="6bb31-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="6bb31-142">Dans les actions SignIn() et SignOut(), émettez les demandes de test OpenID Connect et de déconnexion, respectivement.</span><span class="sxs-lookup"><span data-stu-id="6bb31-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="6bb31-143">À présent, ouvrez `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="6bb31-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="6bb31-144">Voici où vous allez afficher les liens de connexion et de déconnexion de votre application pour l’utilisateur et où vous allez afficher le nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6bb31-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a><span data-ttu-id="6bb31-145">Afficher les informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="6bb31-145">Display user information</span></span>
<span data-ttu-id="6bb31-146">Lors de l’authentification des utilisateurs avec OpenID Connect, le point de terminaison v2.0 retourne un jeton d’ID à l’application qui contient des revendications ou des assertions concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6bb31-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="6bb31-147">Vous pouvez utiliser ces revendications pour personnaliser votre application :</span><span class="sxs-lookup"><span data-stu-id="6bb31-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="6bb31-148">Ouvrez le fichier `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="6bb31-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="6bb31-149">Vous pouvez accéder aux revendications de l’utilisateur dans vos contrôleurs via l’objet principal de sécurité `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="6bb31-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="6bb31-150">Exécuter</span><span class="sxs-lookup"><span data-stu-id="6bb31-150">Run</span></span>
<span data-ttu-id="6bb31-151">Enfin, générez et exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="6bb31-151">Finally, build and run your app!</span></span>   <span data-ttu-id="6bb31-152">Connectez-vous avec un compte Microsoft personnel ou un compte professionnel ou scolaire, et notez comment l’identité de l’utilisateur est indiquée dans la barre de navigation supérieure.</span><span class="sxs-lookup"><span data-stu-id="6bb31-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="6bb31-153">Vous disposez désormais d’une application web sécurisée à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.</span><span class="sxs-lookup"><span data-stu-id="6bb31-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="6bb31-154">Pour référence, l’exemple terminé (sans vos valeurs de configuration) [est fourni ici au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip). Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="6bb31-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="6bb31-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6bb31-155">Next steps</span></span>
<span data-ttu-id="6bb31-156">Vous pouvez maintenant aborder des rubriques plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="6bb31-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="6bb31-157">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6bb31-157">You may want to try:</span></span>

[<span data-ttu-id="6bb31-158">Sécuriser une API Web avec le point de terminaison v2.0 >></span><span class="sxs-lookup"><span data-stu-id="6bb31-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="6bb31-159">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="6bb31-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="6bb31-160">Guide du développeur 2.0 >></span><span class="sxs-lookup"><span data-stu-id="6bb31-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="6bb31-161">Balise StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="6bb31-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="6bb31-162">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="6bb31-162">Get security updates for our products</span></span>
<span data-ttu-id="6bb31-163">Nous vous encourageons à activer les notifications d’incidents de sécurité en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et en vous abonnant aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6bb31-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
