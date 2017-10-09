---
title: aaaAzure AD v2 ASP.NET Web Server mise en route - utilisez | Documents Microsoft
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
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Ajouter un contrôleur toohandle les demandes de connexion et déconnexion

Cet montre étape comment toocreate un nouveau tooexpose de contrôleur connectez-vous et les méthodes de déconnexion.

1.  Cliquez avec le bouton droit sur hello `Controllers` et sélectionnez`Add` > `Controller`
2.  Sélectionnez `MVC (.NET version) Controller – Empty`.
3.  Cliquez sur *Ajouter*.
4.  Nommez-le `HomeController`, puis cliquez sur *Ajouter*.
5.  Ajouter *OWIN* fait référence à la classe de toohello :

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Ajouter deux méthodes de hello ci-dessous toohandle connexion et déconnexion tooyour contrôleur en lançant une stimulation d’authentification via le code :
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Créer des toosign page d’accueil de l’application hello dans utilisateurs via un bouton de connexion

Dans Visual Studio, créez un nouvelle vue tooadd hello bouton de connexion et afficher des informations de l’utilisateur après l’authentification :

1.  Cliquez avec le bouton droit sur hello `Views\Home` et sélectionnez`Add View`
2.  Nommez-le `Index`.
3.  Ajoutez hello suivant le format HTML, ce qui inclut hello bouton de connexion, toohello fichier :

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Informations complémentaires
> Cette page ajoute un bouton de connexion au format SVG avec un arrière-plan noir :<br/>![Se connecter avec Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Pour les boutons de connexion plus, consultez le site toohello [cette page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "instructions de personnalisation").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Ajouter des revendications d’un utilisateur toodisplay contrôleur
Ce contrôleur montre hello utilise Hello `[Authorize]` tooprotect un contrôleur d’attribut. Cet attribut limite le contrôleur d’accès toohello en autorisant uniquement les utilisateurs authentifiés. Hello de code ci-dessous utilise les revendications d’utilisateur hello attribut toodisplay qui ont été récupérées dans le cadre de la connexion au hello.

1.  Cliquez avec le bouton droit sur hello `Controllers` dossier :`Add` > `Controller`
2.  Sélectionnez `MVC {version} Controller – Empty`.
3.  Cliquez sur *Ajouter*.
4.  Nommez-le `ClaimsController`.
5.  Remplacez le code de hello de votre classe de contrôleur avec le code hello ci-dessous - ajoute hello `[Authorize]` toohello classe d’attributs :

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Informations complémentaires
> En raison de l’utilisation de hello Hello `[Authorize]` attribut, toutes les méthodes de ce contrôleur peut être exécutée uniquement si hello utilisateur est authentifié. Si l’utilisateur de hello n’est pas authentifié et tente de contrôleur de hello tooaccess, OWIN sera initier une demande d’authentification et forcer hello utilisateur tooauthenticate. collection de hello des revendications de code Hello ci-dessus examine hello `ClaimsPrincipal.Current` instance pour les attributs d’utilisateur spécifiques inclus dans le jeton de l’utilisateur hello. Ces attributs incluent hello son nom complet et nom d’utilisateur, ainsi que d’objet d’identificateur hello utilisateur global. Il contient également hello *ID client*, qui représente l’ID de hello pour l’organisation de l’utilisateur hello. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Créer une vue de l’utilisateur toodisplay hello

Dans Visual Studio, créez une nouvelle vue de revendications d’utilisateur toodisplay hello dans une page web :

1.  Cliquez avec le bouton droit sur hello `Views\Claims` dossier et :`Add View`
2.  Nommez-le `Index`.
3.  Ajoutez hello HTML toohello fichier suivant :

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
