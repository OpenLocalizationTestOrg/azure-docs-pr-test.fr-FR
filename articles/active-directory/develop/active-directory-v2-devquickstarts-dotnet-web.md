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
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>Ajouter une connexion tooan .NET MVC web app
Avec le point de terminaison v2.0 hello, vous pouvez ajouter rapidement des applications web de tooyour d’authentification avec prise en charge pour les deux comptes personnels de Microsoft et comptes professionnels ou scolaires.  Dans les applications web ASP.NET, vous pouvez y parvenir en utilisant l’intergiciel OWIN de Microsoft inclus dans .NET Framework 4.5.

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
>
>

 Ici nous allons construire une application web qui utilise l’utilisateur OWIN toosign hello dans Affichage des informations sur l’utilisateur de hello et signe hello utilisateur hors de l’application de hello.

## <a name="download"></a>Télécharger
code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).  toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou un clone hello squelette :

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

application Hello terminée est fournie à des fin de hello de ce didacticiel également.

## <a name="register-an-app"></a>Inscription d’une application
Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).  Veillez à respecter les points suivants :

* Copie vers le bas hello **Id d’Application** affecté tooyour application, vous en aurez besoin plus rapidement.
* Ajouter hello **Web** plate-forme pour votre application.
* Entrez hello correct **URI de redirection**. uri de redirection Hello indique tooAzure AD dans lequel les réponses d’authentification doivent être dirigées - valeur par défaut de hello pour ce didacticiel est `https://localhost:44326/`.

## <a name="install--configure-owin-authentication"></a>Installer et configurer l’authentification OWIN
Ici, nous allons configurer hello OWIN intergiciel (middleware) toouse hello OpenID Connect protocole d’authentification.  OWIN est utilisé tooissue les demandes de connexion et déconnexion, gérer la session de l’utilisateur hello et obtenir des informations sur l’utilisateur hello, entre autres.

1. toobegin, ouvrez hello `web.config` fichier racine hello du projet de hello et entrez les valeurs de configuration de votre application Bonjour `<appSettings>` section.

  * Hello `ida:ClientId` est hello **Id d’Application** affecté application tooyour dans le portail de l’enregistrement hello.
  * Hello `ida:RedirectUri` est hello **Uri de redirection** vous avez entré dans le portail de hello.

2. Ensuite, ajoutez hello OWIN intergiciel (middleware) NuGet packages toohello projet à l’aide de la Console du Gestionnaire de Package de hello.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. Ajouter un projet de toohello « Classe de démarrage OWIN » appelé `Startup.cs` droit, cliquez sur le projet de hello--> **ajouter** --> **un nouvel élément** --> Recherchez « OWIN ».  intergiciel (middleware) OWIN de Hello appellera hello `Configuration(...)` méthode au démarrage de votre application.
4. Modifier trop de déclaration de classe hello`public partial class Startup` -nous avons déjà implémenté le cadre de cette classe pour vous dans un autre fichier.  Bonjour `Configuration(...)` (méthode), effectuer un tooset de tooConfigureAuth(...) d’appel de l’authentification pour votre application web  

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

5. Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et implémenter hello `ConfigureAuth(...)` (méthode).  Hello les paramètres que vous fournissez dans `OpenIdConnectAuthenticationOptions` servira de coordonnées pour toocommunicate de votre application auprès d’Azure AD.  Vous devez également tooset l’authentification de Cookie : hello OpenID Connect intergiciel (middleware) utilise des cookies sous hello couvre.

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

## <a name="send-authentication-requests"></a>Envoi de demandes d’authentification
Votre application est maintenant toocommunicate correctement configurée avec un point de terminaison v2.0 hello à l’aide du protocole d’authentification OpenID Connect hello.  OWIN a prise en charge tous les détails de laid hello d’élaborer des messages d’authentification, la validation des jetons d’Azure AD et la gestion de session utilisateur.  Tout ce qui reste est toogive vos utilisateurs un toosign moyen dans et la déconnexion.

- Vous pouvez utiliser autoriser des balises dans votre toorequire contrôleurs connexion de l’utilisateur avant d’accéder à une page donnée.  Ouvrez `Controllers\HomeController.cs`et ajoutez hello `[Authorize]` toohello sur un contrôleur de balise.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- Vous pouvez également utiliser des demandes d’authentification OWIN toodirectly problème dans votre code.  Ouvrez `Controllers\AccountController.cs`.  Hello SignIn() et les actions de SignOut(), émettre OpenID Connect de challenge et de demandes de déconnexion, respectivement.

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

- À présent, ouvrez `Views\Shared\_LoginPartial.cshtml`.  Il s’agit où vous allez afficher les liens de connexion et la déconnexion de votre application utilisateur de hello et imprimer le nom de l’utilisateur hello dans une vue.

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

## <a name="display-user-information"></a>Afficher les informations utilisateur
Lors de l’authentification des utilisateurs avec OpenID Connect, point de terminaison hello v2.0 retourne une application toohello id_token qui contient les revendications, ou assertions sur l’utilisateur de hello.  Vous pouvez utiliser ces toopersonalize de revendications à votre application :

- Ouvrez hello `Controllers\HomeController.cs` fichier.  Vous pouvez accéder à l’utilisateur hello dans vos contrôleurs via hello `ClaimsPrincipal.Current` objet principal de sécurité.

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

## <a name="run"></a>Exécuter
Enfin, générez et exécutez votre application.   Connectez-vous avec un Account Microsoft personnel ou d’un compte professionnel ou scolaire et notez comment l’identité d’utilisateur hello est reflétée dans la barre de navigation supérieure hello.  Vous disposez désormais d’une application web sécurisée à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.

Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie en tant qu’un fichier zip ici](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), ou vous pouvez le cloner à partir de GitHub :

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant aborder des rubriques plus sophistiquées.  Vous souhaiterez peut-être tootry :

[Sécuriser une API Web avec le point de terminaison hello hello v2.0 >>](active-directory-devquickstarts-webapi-dotnet.md)

Pour obtenir des ressources supplémentaires, consultez :

* [guide du développeur v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Balise StackOverflow "azure-active-directory" &gt;&gt;](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obtenir les mises à jour de sécurité de nos produits
Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.
