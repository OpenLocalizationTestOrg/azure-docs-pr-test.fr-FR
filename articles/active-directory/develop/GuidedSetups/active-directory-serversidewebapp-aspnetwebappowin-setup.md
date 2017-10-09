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
## <a name="set-up-your-project"></a><span data-ttu-id="57197-103">Configuration de votre projet</span><span class="sxs-lookup"><span data-stu-id="57197-103">Set up your project</span></span>

<span data-ttu-id="57197-104">Cette section montre hello étapes tooinstall et configurer le pipeline d’authentification hello via l’intergiciel OWIN dans un projet ASP.NET à l’aide de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="57197-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="57197-105">Vous préférez toodownload de projet Visual Studio de cet exemple à la place ?</span><span class="sxs-lookup"><span data-stu-id="57197-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="57197-106">[Télécharger un projet](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) et ignorer toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="57197-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="57197-107">Créer votre projet ASP.NET</span><span class="sxs-lookup"><span data-stu-id="57197-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="57197-108">Dans Visual Studio : `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="57197-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="57197-109">Sous *Visual C# \Web*, sélectionnez `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="57197-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="57197-110">Donnez un nom à votre application et cliquez sur *OK*.</span><span class="sxs-lookup"><span data-stu-id="57197-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="57197-111">Sélectionnez `Empty` et hello select case à cocher tooadd `MVC` références</span><span class="sxs-lookup"><span data-stu-id="57197-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="57197-112">Ajouter les composants d’authentification</span><span class="sxs-lookup"><span data-stu-id="57197-112">Add authentication components</span></span>

1. <span data-ttu-id="57197-113">Dans Visual Studio : `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="57197-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="57197-114">Ajouter *les packages NuGet intergiciel (middleware) OWIN* en tapant hello qui suit dans la fenêtre de Console du Gestionnaire de Package de hello :</span><span class="sxs-lookup"><span data-stu-id="57197-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="57197-115">À propos de ces bibliothèques</span><span class="sxs-lookup"><span data-stu-id="57197-115">About these libraries</span></span>

><span data-ttu-id="57197-116">bibliothèques Hello ci-dessus Activer session unique (SSO) à l’aide de OpenID Connect via l’authentification basée sur le cookie.</span><span class="sxs-lookup"><span data-stu-id="57197-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="57197-117">Une fois l’authentification est terminée et jeton hello représentant l’utilisateur de hello est envoyé tooyour application, intergiciel (middleware) OWIN crée un cookie de session.</span><span class="sxs-lookup"><span data-stu-id="57197-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="57197-118">navigateur de Hello utilise ensuite ce cookie sur les demandes suivantes afin de l’utilisateur de hello n’a pas besoin tooretype leur mot de passe, et aucune vérification supplémentaire n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="57197-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="57197-119">Configurer le pipeline de l’authentification de hello</span><span class="sxs-lookup"><span data-stu-id="57197-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="57197-120">les étapes de Hello ci-dessous sont utilisé toocreate une classe de démarrage tooconfigure OpenID Connect authentification l’intergiciel OWIN.</span><span class="sxs-lookup"><span data-stu-id="57197-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="57197-121">Cette classe sera exécutée automatiquement au démarrage de votre processus IIS.</span><span class="sxs-lookup"><span data-stu-id="57197-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="57197-122">Si votre projet n’a pas un `Startup.cs` fichier dans le dossier racine de hello :</span><span class="sxs-lookup"><span data-stu-id="57197-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="57197-123">Cliquez avec le bouton droit sur le dossier racine du projet hello : >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="57197-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="57197-124">Nommez-le `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="57197-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="57197-125">Assurez-vous que la classe hello sélectionnée est une classe de démarrage OWIN et pas une standard classe c#.</span><span class="sxs-lookup"><span data-stu-id="57197-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="57197-126">En assurer en vérifiant si vous voyez `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` ci-dessus hello espace de noms.</span><span class="sxs-lookup"><span data-stu-id="57197-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="57197-127">Ajouter *OWIN* et *Microsoft.IdentityModel* fait référence à trop`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="57197-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

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
<span data-ttu-id="57197-128">Remplacez la classe de démarrage avec le code hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="57197-128">Replace Startup class with hello code below:</span></span>
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
> ### <a name="more-information"></a><span data-ttu-id="57197-129">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="57197-129">More Information</span></span>

> <span data-ttu-id="57197-130">Hello les paramètres que vous fournissez dans *OpenIDConnectAuthenticationOptions* servent de coordonnées pour toocommunicate d’application hello avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57197-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="57197-131">Étant donné que l’intergiciel (middleware) hello OpenID Connect utilise des cookies en arrière-plan de hello, vous devez également tooset l’authentification de cookie en tant que code hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="57197-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="57197-132">Hello *ValidateIssuer* valeur indique OpenIdConnect toonot restreindre l’accès tooone organisation.</span><span class="sxs-lookup"><span data-stu-id="57197-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

