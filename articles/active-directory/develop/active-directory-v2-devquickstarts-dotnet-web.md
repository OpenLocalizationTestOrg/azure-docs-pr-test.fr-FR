---
title: "aaaAzure AD v2.0 .NET web d’inscription de l’application prise en main | Documents Microsoft"
description: Comment toobuild application Web MVC .NET qui connecte aux utilisateurs avec les deux Account personnel de Microsoft et comptes professionnels ou scolaires.
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
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="b0b4a-103">Ajouter une connexion tooan .NET MVC web app</span><span class="sxs-lookup"><span data-stu-id="b0b4a-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="b0b4a-104">Avec le point de terminaison v2.0 hello, vous pouvez ajouter rapidement des applications web de tooyour d’authentification avec prise en charge pour les deux comptes personnels de Microsoft et comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="b0b4a-105">Dans les applications web ASP.NET, vous pouvez y parvenir en utilisant l’intergiciel OWIN de Microsoft inclus dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="b0b4a-106">Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="b0b4a-107">toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="b0b4a-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="b0b4a-108">Ici nous allons construire une application web qui utilise l’utilisateur OWIN toosign hello dans Affichage des informations sur l’utilisateur de hello et signe hello utilisateur hors de l’application de hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="b0b4a-109">Télécharger</span><span class="sxs-lookup"><span data-stu-id="b0b4a-109">Download</span></span>
<span data-ttu-id="b0b4a-110">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="b0b4a-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="b0b4a-111">toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="b0b4a-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="b0b4a-112">application Hello terminée est fournie à des fin de hello de ce didacticiel également.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="b0b4a-113">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="b0b4a-113">Register an app</span></span>
<span data-ttu-id="b0b4a-114">Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="b0b4a-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="b0b4a-115">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="b0b4a-115">Make sure to:</span></span>

* <span data-ttu-id="b0b4a-116">Copie vers le bas hello **Id d’Application** affecté tooyour application, vous en aurez besoin plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="b0b4a-117">Ajouter hello **Web** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="b0b4a-118">Entrez hello correct **URI de redirection**.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="b0b4a-119">uri de redirection Hello indique tooAzure AD dans lequel les réponses d’authentification doivent être dirigées - valeur par défaut de hello pour ce didacticiel est `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="b0b4a-120">Installer et configurer l’authentification OWIN</span><span class="sxs-lookup"><span data-stu-id="b0b4a-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="b0b4a-121">Ici, nous allons configurer hello OWIN intergiciel (middleware) toouse hello OpenID Connect protocole d’authentification.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="b0b4a-122">OWIN est utilisé tooissue les demandes de connexion et déconnexion, gérer la session de l’utilisateur hello et obtenir des informations sur l’utilisateur hello, entre autres.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="b0b4a-123">toobegin, ouvrez hello `web.config` fichier racine hello du projet de hello et entrez les valeurs de configuration de votre application Bonjour `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="b0b4a-124">Hello `ida:ClientId` est hello **Id d’Application** affecté application tooyour dans le portail de l’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="b0b4a-125">Hello `ida:RedirectUri` est hello **Uri de redirection** vous avez entré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="b0b4a-126">Ensuite, ajoutez hello OWIN intergiciel (middleware) NuGet packages toohello projet à l’aide de la Console du Gestionnaire de Package de hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="b0b4a-127">Ajouter un projet de toohello « Classe de démarrage OWIN » appelé `Startup.cs` droit, cliquez sur le projet de hello--> **ajouter** --> **un nouvel élément** --> Recherchez « OWIN ».</span><span class="sxs-lookup"><span data-stu-id="b0b4a-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="b0b4a-128">intergiciel (middleware) OWIN de Hello appellera hello `Configuration(...)` méthode au démarrage de votre application.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="b0b4a-129">Modifier trop de déclaration de classe hello`public partial class Startup` -nous avons déjà implémenté le cadre de cette classe pour vous dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="b0b4a-130">Bonjour `Configuration(...)` (méthode), effectuer un tooset de tooConfigureAuth(...) d’appel de l’authentification pour votre application web</span><span class="sxs-lookup"><span data-stu-id="b0b4a-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

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

5. <span data-ttu-id="b0b4a-131">Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et implémenter hello `ConfigureAuth(...)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="b0b4a-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="b0b4a-132">Hello les paramètres que vous fournissez dans `OpenIdConnectAuthenticationOptions` servira de coordonnées pour toocommunicate de votre application auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="b0b4a-133">Vous devez également tooset l’authentification de Cookie : hello OpenID Connect intergiciel (middleware) utilise des cookies sous hello couvre.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="b0b4a-134">Envoi de demandes d’authentification</span><span class="sxs-lookup"><span data-stu-id="b0b4a-134">Send authentication requests</span></span>
<span data-ttu-id="b0b4a-135">Votre application est maintenant toocommunicate correctement configurée avec un point de terminaison v2.0 hello à l’aide du protocole d’authentification OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="b0b4a-136">OWIN a prise en charge tous les détails de laid hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD et la gestion de session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="b0b4a-137">Tout ce qui reste est toogive vos utilisateurs un toosign moyen dans et la déconnexion.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="b0b4a-138">Vous pouvez utiliser autoriser des balises dans votre toorequire contrôleurs connexion de l’utilisateur avant d’accéder à une page donnée.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="b0b4a-139">Ouvrez `Controllers\HomeController.cs`et ajoutez hello `[Authorize]` toohello sur un contrôleur de balise.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="b0b4a-140">Vous pouvez également utiliser des demandes d’authentification OWIN toodirectly problème dans votre code.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="b0b4a-141">Ouvrez `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="b0b4a-142">Hello SignIn() et les actions de SignOut(), émettre OpenID Connect de challenge et de demandes de déconnexion, respectivement.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="b0b4a-143">À présent, ouvrez `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="b0b4a-144">Il s’agit où vous allez afficher les liens de connexion et la déconnexion de votre application utilisateur de hello et imprimer le nom de l’utilisateur hello dans une vue.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="b0b4a-145">Afficher les informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="b0b4a-145">Display user information</span></span>
<span data-ttu-id="b0b4a-146">Lors de l’authentification des utilisateurs avec OpenID Connect, point de terminaison hello v2.0 retourne une application toohello id_token qui contient les revendications, ou assertions sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="b0b4a-147">Vous pouvez utiliser ces toopersonalize de revendications à votre application :</span><span class="sxs-lookup"><span data-stu-id="b0b4a-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="b0b4a-148">Ouvrez hello `Controllers\HomeController.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="b0b4a-149">Vous pouvez accéder à l’utilisateur hello dans vos contrôleurs via hello `ClaimsPrincipal.Current` objet principal de sécurité.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="b0b4a-150">Exécuter</span><span class="sxs-lookup"><span data-stu-id="b0b4a-150">Run</span></span>
<span data-ttu-id="b0b4a-151">Enfin, générez et exécutez votre application.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-151">Finally, build and run your app!</span></span>   <span data-ttu-id="b0b4a-152">Connectez-vous avec un Account Microsoft personnel ou d’un compte professionnel ou scolaire et notez comment l’identité d’utilisateur hello est reflétée dans la barre de navigation supérieure hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="b0b4a-153">Vous disposez désormais d’une application web sécurisée à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="b0b4a-154">Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie en tant qu’un fichier zip ici](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), ou vous pouvez le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="b0b4a-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="b0b4a-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0b4a-155">Next steps</span></span>
<span data-ttu-id="b0b4a-156">Vous pouvez maintenant aborder des rubriques plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="b0b4a-157">Vous souhaiterez peut-être tootry :</span><span class="sxs-lookup"><span data-stu-id="b0b4a-157">You may want tootry:</span></span>

[<span data-ttu-id="b0b4a-158">Sécuriser une API Web avec le point de terminaison hello hello v2.0 >></span><span class="sxs-lookup"><span data-stu-id="b0b4a-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="b0b4a-159">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="b0b4a-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="b0b4a-160">guide du développeur v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="b0b4a-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="b0b4a-161">Balise StackOverflow "azure-active-directory" &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="b0b4a-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="b0b4a-162">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="b0b4a-162">Get security updates for our products</span></span>
<span data-ttu-id="b0b4a-163">Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="b0b4a-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
