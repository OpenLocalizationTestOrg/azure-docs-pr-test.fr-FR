---
title: "Prise en main d’Azure AD v2 avec les applications de serveur web ASP.NET - Paramétrage | Microsoft Docs"
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
ms.openlocfilehash: ebf54f5a203adb7f0e5b0c47dcc07595e269e218
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="9a889-103">Configuration de votre projet</span><span class="sxs-lookup"><span data-stu-id="9a889-103">Set up your project</span></span>

<span data-ttu-id="9a889-104">Cette section explique comment installer et configurer le pipeline d’authentification via l’intergiciel OWIN sur un projet ASP.NET à l’aide d’OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9a889-104">This section shows the steps to install and configure the authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="9a889-105">Vous préférez télécharger le projet Visual Studio de cet exemple ?</span><span class="sxs-lookup"><span data-stu-id="9a889-105">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="9a889-106">[Téléchargez un projet](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) et passez à l’étape [Configuration](#create-an-application-express) pour configurer l’exemple de code avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="9a889-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="9a889-107">Créer votre projet ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9a889-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="9a889-108">Dans Visual Studio : `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="9a889-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="9a889-109">Sous *Visual C# \Web*, sélectionnez `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="9a889-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="9a889-110">Donnez un nom à votre application et cliquez sur *OK*.</span><span class="sxs-lookup"><span data-stu-id="9a889-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="9a889-111">Sélectionnez `Empty` et cochez la case pour ajouter des références `MVC`.</span><span class="sxs-lookup"><span data-stu-id="9a889-111">Select `Empty` and select the checkbox to add `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="9a889-112">Ajouter les composants d’authentification</span><span class="sxs-lookup"><span data-stu-id="9a889-112">Add authentication components</span></span>

1. <span data-ttu-id="9a889-113">Dans Visual Studio : `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="9a889-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="9a889-114">Ajoutez *les packages NuGet de l’intergiciel OWIN* en saisissant la commande suivante dans la fenêtre Console du gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="9a889-114">Add *OWIN middleware NuGet packages* by typing the following in the Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="9a889-115">À propos de ces bibliothèques</span><span class="sxs-lookup"><span data-stu-id="9a889-115">About these libraries</span></span>

><span data-ttu-id="9a889-116">Les bibliothèques ci-dessus activent l’authentification unique à l’aide d’OpenID Connect via l’authentification basée sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="9a889-116">The libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="9a889-117">Une fois que l’authentification est terminée et que le jeton qui représente l’utilisateur est envoyé à votre application, l’intergiciel OWIN crée un cookie de session.</span><span class="sxs-lookup"><span data-stu-id="9a889-117">After authentication is completed and the token representing the user is sent to your application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="9a889-118">Le navigateur utilise ensuite ce cookie pour les requêtes ultérieures afin que l’utilisateur n’ait pas besoin de saisir à nouveau son mot de passe, et aucune vérification complémentaire n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9a889-118">The browser then uses this cookie on subsequent requests so the user doesn't need to retype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-the-authentication-pipeline"></a><span data-ttu-id="9a889-119">Configurer le pipeline d’authentification</span><span class="sxs-lookup"><span data-stu-id="9a889-119">Configure the authentication pipeline</span></span>
<span data-ttu-id="9a889-120">Les étapes suivantes permettent de créer une classe de démarrage d’intergiciel OWIN pour configurer l’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9a889-120">The steps below are used to create an OWIN middleware Startup Class to configure OpenID Connect authentication.</span></span> <span data-ttu-id="9a889-121">Cette classe sera exécutée automatiquement au démarrage de votre processus IIS.</span><span class="sxs-lookup"><span data-stu-id="9a889-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="9a889-122">Si votre projet n’a pas de fichier `Startup.cs` dans le dossier racine :</span><span class="sxs-lookup"><span data-stu-id="9a889-122">If your project doesn't have a `Startup.cs` file in the root folder:</span></span><br/>
> 1. <span data-ttu-id="9a889-123">Cliquez avec le bouton droit sur le dossier racine du projet : >    `Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="9a889-123">Right click on the project's root folder: >    `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="9a889-124">Nommez-le `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="9a889-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="9a889-125">Assurez-vous que la classe sélectionnée est une classe de démarrage OWIN et non une classe C# standard.</span><span class="sxs-lookup"><span data-stu-id="9a889-125">Make sure the class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="9a889-126">Pour le savoir, vérifiez que `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` s’affiche au-dessus de l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="9a889-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above the namespace.</span></span>


1. <span data-ttu-id="9a889-127">Ajoutez les références *OWIN* et *Microsoft.IdentityModel* à `Startup.cs` :</span><span class="sxs-lookup"><span data-stu-id="9a889-127">Add *OWIN* and *Microsoft.IdentityModel* references to `Startup.cs`:</span></span>

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
<span data-ttu-id="9a889-128">Remplacez la classe de démarrage par le code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9a889-128">Replace Startup class with the code below:</span></span>
</li>
</ol>

```csharp
public class Startup
{        
    // The Client ID is used by the application to uniquely identify itself to Azure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is the URL where the user will be redirected to after they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is the tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is the URL for authority, composed by Azure Active Directory v2 endpoint and the tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN to use OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets the ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is the page that users will be redirected to after sign-out. In this case, it is using the home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set to request the id_token - which contains basic information about the signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set to false to allow personal and work accounts from any organization to sign in to your application
                // To only allow users from a single organizations, set ValidateIssuer to true and 'tenant' setting in web.config to the tenant name
                // To allow users from only a list of specific organizations, set ValidateIssuer to true and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN to send notification of failed authentications to OnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting the user to the home page with an error in the query string
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
> ### <a name="more-information"></a><span data-ttu-id="9a889-129">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="9a889-129">More Information</span></span>

> <span data-ttu-id="9a889-130">Les paramètres que vous fournissez dans *OpenIDConnectAuthenticationOptions* serviront de coordonnées pour que l’application puisse communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a889-130">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the application to communicate with Azure AD.</span></span> <span data-ttu-id="9a889-131">Vous devez également configurer l’authentification des cookies comme indiqué dans le code ci-dessus, car l’intergiciel OpenID Connect utilise des cookies en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="9a889-131">Because the OpenID Connect middleware uses cookies in the background, you also need to set up cookie authentication as the code above shows.</span></span> <span data-ttu-id="9a889-132">La valeur *ValidateIssuer* indique à OpenID Connect de ne pas restreindre l’accès à une organisation spécifique.</span><span class="sxs-lookup"><span data-stu-id="9a889-132">The *ValidateIssuer* value tells OpenIdConnect to not restrict access to one specific organization.</span></span>
<!--end-collapse-->

