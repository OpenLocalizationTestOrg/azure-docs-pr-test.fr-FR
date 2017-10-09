---
title: "aaaAzure AD v2 ASP.NET Web Server mise en route - le programme d’installation | Documents Microsoft"
description: "Implémentation de la connexion Microsoft dans une solution ASP.NET avec une application basée sur un navigateur web traditionnel utilisant le standard OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configuration de votre projet

Cette section montre hello étapes tooinstall et configurer le pipeline d’authentification hello via l’intergiciel OWIN dans un projet ASP.NET à l’aide de OpenID Connect. 

> Vous préférez toodownload de projet Visual Studio de cet exemple à la place ? [Télécharger un projet](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) et ignorer toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant l’exécution.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Créer votre projet ASP.NET

> 1. Dans Visual Studio : `File` > `New` > `Project`<br/>
> 2. Sous *Visual C# \Web*, sélectionnez `ASP.NET Web Application (.NET Framework)`.
> 3. Donnez un nom à votre application et cliquez sur *OK*.
> 4. Sélectionnez `Empty` et hello select case à cocher tooadd `MVC` références
<!--end-collapse-->

## <a name="add-authentication-components"></a>Ajouter les composants d’authentification

1. Dans Visual Studio : `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Ajouter *les packages NuGet intergiciel (middleware) OWIN* en tapant hello qui suit dans la fenêtre de Console du Gestionnaire de Package de hello :

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>À propos de ces bibliothèques

>bibliothèques Hello ci-dessus Activer session unique (SSO) à l’aide de OpenID Connect via l’authentification basée sur le cookie. Une fois l’authentification est terminée et jeton hello représentant l’utilisateur de hello est envoyé tooyour application, intergiciel (middleware) OWIN crée un cookie de session. navigateur de Hello utilise ensuite ce cookie sur les demandes suivantes afin de l’utilisateur de hello n’a pas besoin tooretype leur mot de passe, et aucune vérification supplémentaire n’est nécessaire.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Configurer le pipeline de l’authentification de hello
les étapes de Hello ci-dessous sont utilisé toocreate une classe de démarrage tooconfigure OpenID Connect authentification l’intergiciel OWIN. Cette classe sera exécutée automatiquement au démarrage de votre processus IIS.

> Si votre projet n’a pas un `Startup.cs` fichier dans le dossier racine de hello :<br/>
> 1. Cliquez avec le bouton droit sur le dossier racine du projet hello : >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Nommez-le `Startup.cs`.

> Assurez-vous que la classe hello sélectionnée est une classe de démarrage OWIN et pas une standard classe c#. En assurer en vérifiant si vous voyez `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` ci-dessus hello espace de noms.


1. Ajouter *OWIN* et *Microsoft.IdentityModel* fait référence à trop`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Remplacez la classe de démarrage avec le code hello ci-dessous :
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Informations complémentaires

> Hello les paramètres que vous fournissez dans *OpenIDConnectAuthenticationOptions* servent de coordonnées pour toocommunicate d’application hello avec Azure AD. Étant donné que l’intergiciel (middleware) hello OpenID Connect utilise des cookies en arrière-plan de hello, vous devez également tooset l’authentification de cookie en tant que code hello ci-dessus. Hello *ValidateIssuer* valeur indique OpenIdConnect toonot restreindre l’accès tooone organisation.
<!--end-collapse-->

