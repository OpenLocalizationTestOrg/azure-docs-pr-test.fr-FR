---
title: "prise en main d’application web .NET aaaAzure AD | Documents Microsoft"
description: "Créez une application web MVC .NET qui s’intègre avec Azure AD pour la connexion."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="a6f10-103">Connexion et déconnexion à une application web ASP.NET avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f10-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="a6f10-104">En fournissant une seule connexion et déconnexion avec seulement quelques lignes de code, Azure Active Directory (Azure AD) simplifie vous toooutsource-application web gestion des identités.</span><span class="sxs-lookup"><span data-stu-id="a6f10-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="a6f10-105">Vous pouvez signer les utilisateurs et les applications web ASP.NET à l’aide de la mise en œuvre de Microsoft hello de l’Interface Web ouverte pour .NET (OWIN) intergiciel (middleware).</span><span class="sxs-lookup"><span data-stu-id="a6f10-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="a6f10-106">L’intergiciel OWIN communautaire est inclus dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="a6f10-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="a6f10-107">Cet article explique comment toouse OWIN à :</span><span class="sxs-lookup"><span data-stu-id="a6f10-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="a6f10-108">Connecter les utilisateurs dans les applications à l’aide d’Azure AD en tant que fournisseur d’identité hello tooweb.</span><span class="sxs-lookup"><span data-stu-id="a6f10-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="a6f10-109">afficher certaines informations utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="a6f10-109">Display some user information.</span></span>
* <span data-ttu-id="a6f10-110">Connecter les utilisateurs en dehors des applications de hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="a6f10-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a6f10-111">Before you get started</span></span>
* <span data-ttu-id="a6f10-112">Télécharger hello [squelette d’application](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou télécharger hello [exemple terminé](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a6f10-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="a6f10-113">Vous devez également un locataire Azure AD dans l’application hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="a6f10-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="a6f10-114">Si vous n’avez pas déjà un locataire Azure AD, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a6f10-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="a6f10-115">Lorsque vous êtes prêt, suivez les procédures de hello dans hello quatre sections.</span><span class="sxs-lookup"><span data-stu-id="a6f10-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="a6f10-116">Étape 1 : Inscrire hello nouvelle application avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f10-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="a6f10-117">tooset des utilisateurs de tooauthenticate application hello, inscrire tout d’abord dans votre client en effectuant des opérations hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6f10-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="a6f10-118">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6f10-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6f10-119">Sur la barre supérieure de hello, cliquez sur le nom de votre compte.</span><span class="sxs-lookup"><span data-stu-id="a6f10-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="a6f10-120">Sous hello **répertoire** liste, le client d’Active Directory hello sélectionnez où vous souhaitez tooregister hello application.</span><span class="sxs-lookup"><span data-stu-id="a6f10-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="a6f10-121">Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a6f10-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="a6f10-122">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a6f10-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="a6f10-123">Suivez hello invite toocreate un nouveau **Application Web et/ou WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="a6f10-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="a6f10-124">**Nom** décrit hello application toousers.</span><span class="sxs-lookup"><span data-stu-id="a6f10-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="a6f10-125">**URL de connexion** est hello les URL de base de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="a6f10-126">URL de valeur par défaut du squelette Hello est https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="a6f10-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="a6f10-127">Une fois que vous avez terminé l’inscription de hello, Azure AD assigne application hello un ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="a6f10-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="a6f10-128">Copiez les valeur hello de toouse de page application hello dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="a6f10-129">À partir de hello **paramètres** -> **propriétés** page de votre application, la mise à jour de hello URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="a6f10-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="a6f10-130">Hello **URI ID d’application** est un identificateur unique pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="a6f10-131">Bonjour convention d’affectation de noms est `https://<tenant-domain>/<app-name>` (par exemple, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="a6f10-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="a6f10-132">Étape 2 : Configurer de pipeline de hello application toouse hello OWIN d’authentification</span><span class="sxs-lookup"><span data-stu-id="a6f10-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="a6f10-133">Dans cette étape, vous configurez hello OWIN intergiciel (middleware) toouse hello OpenID Connect protocole d’authentification.</span><span class="sxs-lookup"><span data-stu-id="a6f10-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="a6f10-134">Vous utilisez des demandes de connexion et de déconnexion de tooissue OWIN, gérez les sessions utilisateur, obtenez des informations utilisateur et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="a6f10-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="a6f10-135">toobegin, ajouter des projets toohello des packages de NuGet hello OWIN intergiciel (middleware) à l’aide de hello Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="a6f10-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="a6f10-136">tooadd un projet de démarrage OWIN de toohello de classes appelé `Startup.cs`, cliquez sur le projet de hello, sélectionnez **ajouter**, sélectionnez **un nouvel élément**, puis recherchez **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="a6f10-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="a6f10-137">intergiciel (middleware) OWIN de Hello appelle hello **Configuration(...)**  méthode au démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="a6f10-138">Modifier trop de déclaration de classe hello`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="a6f10-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="a6f10-139">Nous avons déjà mis en œuvre une partie de cette classe pour vous dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="a6f10-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="a6f10-140">Bonjour **Configuration(...)**  (méthode), effectuer un appel trop**ConfgureAuth(...)**  tooset authentification pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="a6f10-141">Ouvrez le fichier de App_Start\Startup.Auth.cs hello et implémentez hello **ConfigureAuth(...)**  (méthode).</span><span class="sxs-lookup"><span data-stu-id="a6f10-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="a6f10-142">Hello les paramètres que vous fournissez dans *OpenIDConnectAuthenticationOptions* servent de coordonnées pour toocommunicate d’application hello avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6f10-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="a6f10-143">Vous devez également tooset l’authentification de cookie, étant donné que l’intergiciel (middleware) hello OpenID Connect utilise des cookies en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="a6f10-144">Ouvrez le fichier web.config dans hello dans racine hello du projet de hello, puis entrez les valeurs de configuration hello Bonjour `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="a6f10-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="a6f10-145">`ida:ClientId`: hello GUID que vous avez copié à partir de hello portail Azure dans « étape 1 : inscrire l’application hello nouvelle auprès d’Azure AD. »</span><span class="sxs-lookup"><span data-stu-id="a6f10-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="a6f10-146">`ida:Tenant`: nom hello de votre client Azure AD (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="a6f10-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="a6f10-147">`ida:PostLogoutRedirectUri`: indicateur hello qui indique à Azure AD où un utilisateur doit être redirigé après une demande de déconnexion est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="a6f10-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="a6f10-148">Étape 3 : Utiliser OWIN tooissue connexion et déconnexion demande tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="a6f10-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="a6f10-149">application Hello est désormais toocommunicate correctement configuré avec Azure AD à l’aide du protocole d’authentification OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="a6f10-150">OWIN a traité tous les détails de hello de personnalisation des messages d’authentification, la validation des jetons d’Azure AD et la gestion des sessions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6f10-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="a6f10-151">Tout ce qui reste est toogive vos utilisateurs un toosign moyen dans et la déconnexion.</span><span class="sxs-lookup"><span data-stu-id="a6f10-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="a6f10-152">Vous pouvez utiliser autoriser des balises dans votre toosign d’utilisateurs toorequire contrôleurs dans avant accéder à certaines pages.</span><span class="sxs-lookup"><span data-stu-id="a6f10-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="a6f10-153">toodo, ouvrez Controllers\HomeController.cs et ajoutez hello `[Authorize]` toohello sur un contrôleur de balise.</span><span class="sxs-lookup"><span data-stu-id="a6f10-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="a6f10-154">Vous pouvez également utiliser des demandes d’authentification OWIN toodirectly problème dans votre code.</span><span class="sxs-lookup"><span data-stu-id="a6f10-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="a6f10-155">toodo, ouvrez Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="a6f10-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="a6f10-156">Dans actions de SignIn() et SignOut() hello, émettre OpenID Connect de challenge et de demandes de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="a6f10-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="a6f10-157">Ouvrez Views\Shared\_LoginPartial.cshtml tooshow hello utilisateur hello application connexion et déconnexion des liens et tooprint nom de l’utilisateur hello dans une vue.</span><span class="sxs-lookup"><span data-stu-id="a6f10-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="a6f10-158">Étape 4 : Afficher les informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="a6f10-158">Step 4: Display user information</span></span>
<span data-ttu-id="a6f10-159">Lors de l’authentification des utilisateurs avec OpenID Connect, Azure AD renvoie une application toohello id_token qui contient « revendications », ou assertions sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="a6f10-160">Vous pouvez utiliser ces applications de hello toopersonalize revendications de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="a6f10-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="a6f10-161">Ouvrez le fichier Controllers\HomeController.cs de hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="a6f10-162">Vous pouvez accéder à l’utilisateur hello dans vos contrôleurs via hello `ClaimsPrincipal.Current` objet principal de sécurité.</span><span class="sxs-lookup"><span data-stu-id="a6f10-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="a6f10-163">Générez et exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-163">Build and run hello app.</span></span> <span data-ttu-id="a6f10-164">Si vous n’avez pas déjà créé un nouvel utilisateur dans votre client à un domaine onmicrosoft.com, est désormais hello temps toodo donc.</span><span class="sxs-lookup"><span data-stu-id="a6f10-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="a6f10-165">Voici comment procéder :</span><span class="sxs-lookup"><span data-stu-id="a6f10-165">Here's how:</span></span>

  <span data-ttu-id="a6f10-166">a.</span><span class="sxs-lookup"><span data-stu-id="a6f10-166">a.</span></span> <span data-ttu-id="a6f10-167">Connectez-vous à cet utilisateur et notez comment l’identité d’utilisateur hello est répercutée sur la barre supérieure de hello.</span><span class="sxs-lookup"><span data-stu-id="a6f10-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="a6f10-168">b.</span><span class="sxs-lookup"><span data-stu-id="a6f10-168">b.</span></span> <span data-ttu-id="a6f10-169">Déconnectez-vous, puis reconnectez-vous sous le nom d’un autre utilisateur de votre client.</span><span class="sxs-lookup"><span data-stu-id="a6f10-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="a6f10-170">c.</span><span class="sxs-lookup"><span data-stu-id="a6f10-170">c.</span></span> <span data-ttu-id="a6f10-171">Si vous vous sentez particulièrement ambitieux, enregistrez et exécutez une autre instance de cette application (avec son propre ID de client) et observez le fonctionnement de la connexion unique.</span><span class="sxs-lookup"><span data-stu-id="a6f10-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6f10-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6f10-172">Next steps</span></span>
<span data-ttu-id="a6f10-173">Pour référence, consultez [exemple hello terminée](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sans les valeurs de configuration).</span><span class="sxs-lookup"><span data-stu-id="a6f10-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="a6f10-174">Vous pouvez maintenant passer toomore rubriques avancées.</span><span class="sxs-lookup"><span data-stu-id="a6f10-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="a6f10-175">Par exemple, essayez de [Sécuriser une API web avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a6f10-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
