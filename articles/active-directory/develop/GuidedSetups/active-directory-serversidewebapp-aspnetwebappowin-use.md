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
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a><span data-ttu-id="57a91-103">Ajouter un contrôleur toohandle les demandes de connexion et déconnexion</span><span class="sxs-lookup"><span data-stu-id="57a91-103">Add a controller toohandle sign-in and sign-out requests</span></span>

<span data-ttu-id="57a91-104">Cet montre étape comment toocreate un nouveau tooexpose de contrôleur connectez-vous et les méthodes de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="57a91-104">This step shows how toocreate a new controller tooexpose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="57a91-105">Cliquez avec le bouton droit sur hello `Controllers` et sélectionnez`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="57a91-105">Right click hello `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="57a91-106">Sélectionnez `MVC (.NET version) Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="57a91-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="57a91-107">Cliquez sur *Ajouter*.</span><span class="sxs-lookup"><span data-stu-id="57a91-107">Click *Add*</span></span>
4.  <span data-ttu-id="57a91-108">Nommez-le `HomeController`, puis cliquez sur *Ajouter*.</span><span class="sxs-lookup"><span data-stu-id="57a91-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="57a91-109">Ajouter *OWIN* fait référence à la classe de toohello :</span><span class="sxs-lookup"><span data-stu-id="57a91-109">Add *OWIN* references toohello class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="57a91-110">Ajouter deux méthodes de hello ci-dessous toohandle connexion et déconnexion tooyour contrôleur en lançant une stimulation d’authentification via le code :</span><span class="sxs-lookup"><span data-stu-id="57a91-110">Add hello two methods below toohandle sign-in and sign-out tooyour controller by initiating an authentication challenge via code:</span></span>
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

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a><span data-ttu-id="57a91-111">Créer des toosign page d’accueil de l’application hello dans utilisateurs via un bouton de connexion</span><span class="sxs-lookup"><span data-stu-id="57a91-111">Create hello app's home page toosign in users via a sign-in button</span></span>

<span data-ttu-id="57a91-112">Dans Visual Studio, créez un nouvelle vue tooadd hello bouton de connexion et afficher des informations de l’utilisateur après l’authentification :</span><span class="sxs-lookup"><span data-stu-id="57a91-112">In Visual Studio, create a new view tooadd hello sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="57a91-113">Cliquez avec le bouton droit sur hello `Views\Home` et sélectionnez`Add View`</span><span class="sxs-lookup"><span data-stu-id="57a91-113">Right click hello `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="57a91-114">Nommez-le `Index`.</span><span class="sxs-lookup"><span data-stu-id="57a91-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="57a91-115">Ajoutez hello suivant le format HTML, ce qui inclut hello bouton de connexion, toohello fichier :</span><span class="sxs-lookup"><span data-stu-id="57a91-115">Add hello following HTML, which includes hello sign-in button, toohello file:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="57a91-116">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="57a91-116">More Information</span></span>
> <span data-ttu-id="57a91-117">Cette page ajoute un bouton de connexion au format SVG avec un arrière-plan noir :</span><span class="sxs-lookup"><span data-stu-id="57a91-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="57a91-118">![Se connecter avec Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="57a91-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="57a91-119">Pour les boutons de connexion plus, consultez le site toohello [cette page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "instructions de personnalisation").</span><span class="sxs-lookup"><span data-stu-id="57a91-119">For more sign-in buttons, please go toohello [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a><span data-ttu-id="57a91-120">Ajouter des revendications d’un utilisateur toodisplay contrôleur</span><span class="sxs-lookup"><span data-stu-id="57a91-120">Add a controller toodisplay user's claims</span></span>
<span data-ttu-id="57a91-121">Ce contrôleur montre hello utilise Hello `[Authorize]` tooprotect un contrôleur d’attribut.</span><span class="sxs-lookup"><span data-stu-id="57a91-121">This controller demonstrates hello uses of hello `[Authorize]` attribute tooprotect a controller.</span></span> <span data-ttu-id="57a91-122">Cet attribut limite le contrôleur d’accès toohello en autorisant uniquement les utilisateurs authentifiés.</span><span class="sxs-lookup"><span data-stu-id="57a91-122">This attribute restricts access toohello controller by only allowing authenticated users.</span></span> <span data-ttu-id="57a91-123">Hello de code ci-dessous utilise les revendications d’utilisateur hello attribut toodisplay qui ont été récupérées dans le cadre de la connexion au hello.</span><span class="sxs-lookup"><span data-stu-id="57a91-123">hello code below makes use of hello attribute toodisplay user claims that were retrieved as part of hello sign-in.</span></span>

1.  <span data-ttu-id="57a91-124">Cliquez avec le bouton droit sur hello `Controllers` dossier :`Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="57a91-124">Right click hello `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="57a91-125">Sélectionnez `MVC {version} Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="57a91-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="57a91-126">Cliquez sur *Ajouter*.</span><span class="sxs-lookup"><span data-stu-id="57a91-126">Click *Add*</span></span>
4.  <span data-ttu-id="57a91-127">Nommez-le `ClaimsController`.</span><span class="sxs-lookup"><span data-stu-id="57a91-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="57a91-128">Remplacez le code de hello de votre classe de contrôleur avec le code hello ci-dessous - ajoute hello `[Authorize]` toohello classe d’attributs :</span><span class="sxs-lookup"><span data-stu-id="57a91-128">Replace hello code of your controller class with hello code below - this adds hello `[Authorize]` attribute toohello class:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="57a91-129">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="57a91-129">More Information</span></span>
> <span data-ttu-id="57a91-130">En raison de l’utilisation de hello Hello `[Authorize]` attribut, toutes les méthodes de ce contrôleur peut être exécutée uniquement si hello utilisateur est authentifié.</span><span class="sxs-lookup"><span data-stu-id="57a91-130">Because of hello use of hello `[Authorize]` attribute, all methods of this controller can only be executed if hello user is authenticated.</span></span> <span data-ttu-id="57a91-131">Si l’utilisateur de hello n’est pas authentifié et tente de contrôleur de hello tooaccess, OWIN sera initier une demande d’authentification et forcer hello utilisateur tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="57a91-131">If hello user is not authenticated and tries tooaccess hello controller, OWIN will initiate an authentication challenge and force hello user tooauthenticate.</span></span> <span data-ttu-id="57a91-132">collection de hello des revendications de code Hello ci-dessus examine hello `ClaimsPrincipal.Current` instance pour les attributs d’utilisateur spécifiques inclus dans le jeton de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="57a91-132">hello code above looks at hello claims collection of hello `ClaimsPrincipal.Current` instance for specific user attributes included in hello user’s token.</span></span> <span data-ttu-id="57a91-133">Ces attributs incluent hello son nom complet et nom d’utilisateur, ainsi que d’objet d’identificateur hello utilisateur global.</span><span class="sxs-lookup"><span data-stu-id="57a91-133">These attributes include hello user’s full name and username, as well as hello global user identifier subject.</span></span> <span data-ttu-id="57a91-134">Il contient également hello *ID client*, qui représente l’ID de hello pour l’organisation de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="57a91-134">It also contains hello *Tenant ID*, which represents hello ID for hello user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a><span data-ttu-id="57a91-135">Créer une vue de l’utilisateur toodisplay hello</span><span class="sxs-lookup"><span data-stu-id="57a91-135">Create a view toodisplay hello user's claims</span></span>

<span data-ttu-id="57a91-136">Dans Visual Studio, créez une nouvelle vue de revendications d’utilisateur toodisplay hello dans une page web :</span><span class="sxs-lookup"><span data-stu-id="57a91-136">In Visual Studio, create a new view toodisplay hello user's claims in a web page:</span></span>

1.  <span data-ttu-id="57a91-137">Cliquez avec le bouton droit sur hello `Views\Claims` dossier et :`Add View`</span><span class="sxs-lookup"><span data-stu-id="57a91-137">Right click hello `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="57a91-138">Nommez-le `Index`.</span><span class="sxs-lookup"><span data-stu-id="57a91-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="57a91-139">Ajoutez hello HTML toohello fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="57a91-139">Add hello following HTML toohello file:</span></span>

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
