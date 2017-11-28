---
title: "Prise en main d’Azure AD v2 avec les applications de serveur web ASP.NET - Utilisation | Documents Microsoft"
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
ms.openlocfilehash: 3b7d29e48c91f40e8782a5e32a52998b815fe331
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="add-a-controller-to-handle-sign-in-and-sign-out-requests"></a><span data-ttu-id="267ca-103">Ajouter un contrôleur pour gérer les demandes de connexion et de déconnexion</span><span class="sxs-lookup"><span data-stu-id="267ca-103">Add a controller to handle sign-in and sign-out requests</span></span>

<span data-ttu-id="267ca-104">Cette étape explique comment créer un contrôleur pour exposer les méthodes de connexion et de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="267ca-104">This step shows how to create a new controller to expose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="267ca-105">Cliquez avec le bouton droit sur le dossier `Controllers` et sélectionnez `Add` > `Controller`.</span><span class="sxs-lookup"><span data-stu-id="267ca-105">Right click the `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="267ca-106">Sélectionnez `MVC (.NET version) Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="267ca-106">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="267ca-107">Cliquez sur *Ajouter*.</span><span class="sxs-lookup"><span data-stu-id="267ca-107">Click *Add*</span></span>
4.  <span data-ttu-id="267ca-108">Nommez-le `HomeController`, puis cliquez sur *Ajouter*.</span><span class="sxs-lookup"><span data-stu-id="267ca-108">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="267ca-109">Ajoutez les références *OWIN* à la classe :</span><span class="sxs-lookup"><span data-stu-id="267ca-109">Add *OWIN* references to the class:</span></span>

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="267ca-110">Ajoutez les deux méthodes ci-dessous pour gérer la connexion à votre contrôleur et la déconnexion de celui-ci en lançant une demande d’authentification via du code :</span><span class="sxs-lookup"><span data-stu-id="267ca-110">Add the two methods below to handle sign-in and sign-out to your controller by initiating an authentication challenge via code:</span></span>
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate the SignIn method with the [Authorize] attribute
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

## <a name="create-the-apps-home-page-to-sign-in-users-via-a-sign-in-button"></a><span data-ttu-id="267ca-111">Créer la page d’accueil de l’application pour connecter des utilisateurs via un bouton de connexion</span><span class="sxs-lookup"><span data-stu-id="267ca-111">Create the app's home page to sign in users via a sign-in button</span></span>

<span data-ttu-id="267ca-112">Dans Visual Studio, créez une vue pour ajouter le bouton de connexion et afficher les informations de l’utilisateur après l’authentification :</span><span class="sxs-lookup"><span data-stu-id="267ca-112">In Visual Studio, create a new view to add the sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="267ca-113">Cliquez avec le bouton droit sur le dossier `Views\Home` et sélectionnez `Add View`.</span><span class="sxs-lookup"><span data-stu-id="267ca-113">Right click the `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="267ca-114">Nommez-le `Index`.</span><span class="sxs-lookup"><span data-stu-id="267ca-114">Name it `Index`.</span></span>
3.  <span data-ttu-id="267ca-115">Ajoutez le code HTML suivant, qui inclut le bouton de connexion, au fichier :</span><span class="sxs-lookup"><span data-stu-id="267ca-115">Add the following HTML, which includes the sign-in button, to the file:</span></span>

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If the user is not authenticated, display the sign-in button -->
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
### <a name="more-information"></a><span data-ttu-id="267ca-116">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="267ca-116">More Information</span></span>
> <span data-ttu-id="267ca-117">Cette page ajoute un bouton de connexion au format SVG avec un arrière-plan noir :</span><span class="sxs-lookup"><span data-stu-id="267ca-117">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="267ca-118">![Se connecter avec Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="267ca-118">![Sign-in with Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="267ca-119">Pour accéder à d’autres boutons de connexion, rendez-vous sur [cette page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span><span class="sxs-lookup"><span data-stu-id="267ca-119">For more sign-in buttons, please go to the [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="add-a-controller-to-display-users-claims"></a><span data-ttu-id="267ca-120">Ajouter un contrôleur pour afficher les revendications de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="267ca-120">Add a controller to display user's claims</span></span>
<span data-ttu-id="267ca-121">Ce contrôleur démontre les utilisations de l’attribut `[Authorize]` pour protéger un contrôleur.</span><span class="sxs-lookup"><span data-stu-id="267ca-121">This controller demonstrates the uses of the `[Authorize]` attribute to protect a controller.</span></span> <span data-ttu-id="267ca-122">Cet attribut limite l’accès au contrôleur en autorisant uniquement les utilisateurs authentifiés.</span><span class="sxs-lookup"><span data-stu-id="267ca-122">This attribute restricts access to the controller by only allowing authenticated users.</span></span> <span data-ttu-id="267ca-123">Le code ci-dessous tire parti de l’attribut pour afficher les revendications de l’utilisateur qui ont été récupérées dans le cadre de la connexion.</span><span class="sxs-lookup"><span data-stu-id="267ca-123">The code below makes use of the attribute to display user claims that were retrieved as part of the sign-in.</span></span>

1.  <span data-ttu-id="267ca-124">Cliquez avec le bouton droit sur le dossier `Controllers` et sélectionnez `Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="267ca-124">Right click the `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="267ca-125">Sélectionnez `MVC {version} Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="267ca-125">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="267ca-126">Cliquez sur *Ajouter*.</span><span class="sxs-lookup"><span data-stu-id="267ca-126">Click *Add*</span></span>
4.  <span data-ttu-id="267ca-127">Nommez-le `ClaimsController`.</span><span class="sxs-lookup"><span data-stu-id="267ca-127">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="267ca-128">Remplacez le code de votre classe de contrôleur par le code ci-dessous afin d’ajouter l’attribut `[Authorize]` à la classe :</span><span class="sxs-lookup"><span data-stu-id="267ca-128">Replace the code of your controller class with the code below - this adds the `[Authorize]` attribute to the class:</span></span>

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims to viewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get the user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // The 'preferred_username' claim can be used for showing the username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // The subject claim can be used to uniquely identify the user across the web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is the unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="267ca-129">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="267ca-129">More Information</span></span>
> <span data-ttu-id="267ca-130">En raison de l’utilisation de l’attribut `[Authorize]`, toutes les méthodes de ce contrôleur peuvent uniquement être exécutées si l’utilisateur est authentifié.</span><span class="sxs-lookup"><span data-stu-id="267ca-130">Because of the use of the `[Authorize]` attribute, all methods of this controller can only be executed if the user is authenticated.</span></span> <span data-ttu-id="267ca-131">Si l’utilisateur n’est pas authentifié et tente d’accéder au contrôleur, OWIN initialise une demande d’authentification et oblige l’utilisateur à s’authentifier.</span><span class="sxs-lookup"><span data-stu-id="267ca-131">If the user is not authenticated and tries to access the controller, OWIN will initiate an authentication challenge and force the user to authenticate.</span></span> <span data-ttu-id="267ca-132">Le code ci-dessus examine la collection de revendications de l’instance `ClaimsPrincipal.Current` pour les attributs utilisateur spécifiques inclus dans le jeton de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="267ca-132">The code above looks at the claims collection of the `ClaimsPrincipal.Current` instance for specific user attributes included in the user’s token.</span></span> <span data-ttu-id="267ca-133">Ces attributs incluent le nom complet et le nom d’utilisateur de l’utilisateur, ainsi que le sujet d’identificateur d’utilisateur global.</span><span class="sxs-lookup"><span data-stu-id="267ca-133">These attributes include the user’s full name and username, as well as the global user identifier subject.</span></span> <span data-ttu-id="267ca-134">Il contient également le *ID client*, qui représente l’identifiant de l’organisation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="267ca-134">It also contains the *Tenant ID*, which represents the ID for the user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-to-display-the-users-claims"></a><span data-ttu-id="267ca-135">Créer une vue pour afficher les revendications de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="267ca-135">Create a view to display the user's claims</span></span>

<span data-ttu-id="267ca-136">Dans Visual Studio, créez une vue pour afficher les revendications de l’utilisateur dans une page web :</span><span class="sxs-lookup"><span data-stu-id="267ca-136">In Visual Studio, create a new view to display the user's claims in a web page:</span></span>

1.  <span data-ttu-id="267ca-137">Cliquez avec le bouton droit sur le dossier `Views\Claims` et sélectionnez `Add View`.</span><span class="sxs-lookup"><span data-stu-id="267ca-137">Right click the `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="267ca-138">Nommez-le `Index`.</span><span class="sxs-lookup"><span data-stu-id="267ca-138">Name it `Index`.</span></span>
3.  <span data-ttu-id="267ca-139">Ajoutez le code HTML suivant au fichier :</span><span class="sxs-lookup"><span data-stu-id="267ca-139">Add the following HTML to the file:</span></span>

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
