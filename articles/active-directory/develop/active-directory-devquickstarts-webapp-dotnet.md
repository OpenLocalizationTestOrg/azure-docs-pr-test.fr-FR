---
title: "Bien démarrer avec l’application web .NET Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="f093b-103">Connexion et déconnexion à une application web ASP.NET avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="f093b-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="f093b-104">En assurant une connexion et une déconnexion uniques avec seulement quelques lignes de code, Azure Active Directory (Azure AD) simplifie l’externalisation de la gestion des identités des applications web.</span><span class="sxs-lookup"><span data-stu-id="f093b-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="f093b-105">Vous pouvez connecter et déconnecter les utilisateurs des applications web ASP.NET à l’aide de l’implémentation Microsoft de l’intergiciel OWIN (Open Web Interface for .NET).</span><span class="sxs-lookup"><span data-stu-id="f093b-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="f093b-106">L’intergiciel OWIN communautaire est inclus dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f093b-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="f093b-107">Cet article explique comment utiliser OWIN pour :</span><span class="sxs-lookup"><span data-stu-id="f093b-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="f093b-108">connecter des utilisateurs à des applications web en utilisant Azure AD comme fournisseur d’identité ;</span><span class="sxs-lookup"><span data-stu-id="f093b-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="f093b-109">afficher certaines informations utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="f093b-109">Display some user information.</span></span>
* <span data-ttu-id="f093b-110">déconnecter des utilisateurs des applications.</span><span class="sxs-lookup"><span data-stu-id="f093b-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="f093b-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f093b-111">Before you get started</span></span>
* <span data-ttu-id="f093b-112">Téléchargez [la structure de l’application](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou [l’exemple terminé](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f093b-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="f093b-113">Vous avez également besoin d’un client Azure AD dans lequel inscrire l’application.</span><span class="sxs-lookup"><span data-stu-id="f093b-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="f093b-114">Si vous ne disposez pas encore d’un client Azure AD, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f093b-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="f093b-115">Lorsque vous êtes prêt, suivez les procédures des quatre sections qui suivent.</span><span class="sxs-lookup"><span data-stu-id="f093b-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="f093b-116">Étape 1 : Inscrire la nouvelle application auprès d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="f093b-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="f093b-117">Pour configurer l’application pour l’authentification des utilisateurs, commencez par l’inscrire dans votre client en procédant de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="f093b-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="f093b-118">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f093b-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f093b-119">Dans la barre supérieure, cliquez sur le nom de votre compte.</span><span class="sxs-lookup"><span data-stu-id="f093b-119">On the top bar, click your account name.</span></span> <span data-ttu-id="f093b-120">Dans la liste **Annuaire**, sélectionnez le client Active Directory dans lequel vous voulez inscrire l’application.</span><span class="sxs-lookup"><span data-stu-id="f093b-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="f093b-121">Dans le volet gauche, cliquez sur **Plus de services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f093b-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f093b-122">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f093b-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="f093b-123">Suivez les invites et créez **une nouvelle application web et/ou une nouvelle API web**.</span><span class="sxs-lookup"><span data-stu-id="f093b-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="f093b-124">Le champ **Nom** décrit l’application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f093b-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="f093b-125">Le champ **URL de connexion** indique l’URL de base de l’application.</span><span class="sxs-lookup"><span data-stu-id="f093b-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="f093b-126">L’URL par défaut de la structure est https://localhost:44320/.</span><span class="sxs-lookup"><span data-stu-id="f093b-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="f093b-127">Une fois que vous avez terminé l’inscription, Azure AD affecte un ID d’application unique à l’application.</span><span class="sxs-lookup"><span data-stu-id="f093b-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="f093b-128">Copiez la valeur de la page d’application pour l’utiliser dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="f093b-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="f093b-129">À partir de la page **Paramètres** -> **Propriétés** de votre application, mettez à jour l’URI ID d’application.</span><span class="sxs-lookup"><span data-stu-id="f093b-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="f093b-130">Le champ **URI ID d’application** est un identificateur unique de l’application.</span><span class="sxs-lookup"><span data-stu-id="f093b-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="f093b-131">La convention d’affectation de noms est `https://<tenant-domain>/<app-name>` (par exemple, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="f093b-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="f093b-132">Étape 2 : Configurer l’application pour utiliser le pipeline d’authentification OWIN</span><span class="sxs-lookup"><span data-stu-id="f093b-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="f093b-133">Au cours de cette étape, vous allez configurer l’intergiciel OWIN pour utiliser le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f093b-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="f093b-134">Vous utilisez OWIN pour émettre des demandes de connexion et de déconnexion, gérer les sessions utilisateur, obtenir des informations utilisateur, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="f093b-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="f093b-135">Pour commencer, ajoutez au projet les packages NuGet de l’intergiciel OWIN à l’aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="f093b-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="f093b-136">Pour ajouter une classe de démarrage OWIN au projet nommé `Startup.cs`, cliquez avec le bouton droit sur le projet, sélectionnez **Ajouter** puis **Nouvel élément** et recherchez **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="f093b-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="f093b-137">L’intergiciel OWIN appelle la méthode **Configuration(...)** au lancement de l’application.</span><span class="sxs-lookup"><span data-stu-id="f093b-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="f093b-138">Remplacez la déclaration de classe par `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="f093b-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="f093b-139">Nous avons déjà mis en œuvre une partie de cette classe pour vous dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="f093b-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="f093b-140">Dans la méthode **Configuration(...)**, appelez **ConfigureAuth(...)** pour configurer l’authentification de l’application.</span><span class="sxs-lookup"><span data-stu-id="f093b-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="f093b-141">Ouvrez le fichier App_Start\Startup.Auth.cs, puis implémentez la méthode **ConfigureAuth(...)**.</span><span class="sxs-lookup"><span data-stu-id="f093b-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="f093b-142">Les paramètres que vous fournissez dans *OpenIDConnectAuthenticationOptions* serviront de coordonnées pour que l’application puisse communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f093b-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="f093b-143">Vous devez également configurer l’authentification des cookies, car l’intergiciel OpenID Connect utilise des cookies en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="f093b-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

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

5. <span data-ttu-id="f093b-144">Ouvrez le fichier web.config à la racine du projet, puis entrez les valeurs de configuration dans la section `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="f093b-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="f093b-145">`ida:ClientId` : le GUID que vous avez copié à partir du Portail Azure dans « Étape 1 : Inscrire la nouvelle application auprès d’Azure AD ».</span><span class="sxs-lookup"><span data-stu-id="f093b-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="f093b-146">`ida:Tenant` : le nom de votre client Azure AD (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="f093b-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="f093b-147">`ida:PostLogoutRedirectUri` : indique à Azure AD l’endroit vers lequel un utilisateur doit être redirigé après l’exécution d’une demande de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="f093b-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="f093b-148">Étape 3 : Utiliser OWIN pour émettre des demandes de connexion et de déconnexion dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="f093b-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="f093b-149">L’application est maintenant correctement configurée pour communiquer avec Azure AD en utilisant le protocole d’authentification OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f093b-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="f093b-150">OWIN a géré tous les détails de la création de messages d’authentification, de la validation des jetons d’Azure AD et de la gestion des sessions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f093b-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="f093b-151">Il ne reste qu’à offrir aux utilisateurs un moyen de se connecter et de se déconnecter.</span><span class="sxs-lookup"><span data-stu-id="f093b-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="f093b-152">Vous pouvez utiliser des balises autorisées dans vos contrôleurs afin d’exiger que les utilisateurs se connectent pour pouvoir accéder à une page donnée.</span><span class="sxs-lookup"><span data-stu-id="f093b-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="f093b-153">Pour cela, ouvrez Controllers\HomeController.cs et ajoutez la balise `[Authorize]` au contrôleur About.</span><span class="sxs-lookup"><span data-stu-id="f093b-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="f093b-154">Vous pouvez également utiliser OWIN pour émettre des demandes d’authentification provenant directement de votre code.</span><span class="sxs-lookup"><span data-stu-id="f093b-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="f093b-155">Pour cela, ouvrez Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="f093b-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="f093b-156">Ensuite, dans les actions SignIn() et SignOut(), émettez les demandes de test OpenID Connect et de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="f093b-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="f093b-157">Ouvrez Views\Shared\_LoginPartial.cshtml pour montrer les liens de connexion et de déconnexion de l’application à l’utilisateur et pour imprimer le nom de l’utilisateur dans un affichage.</span><span class="sxs-lookup"><span data-stu-id="f093b-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="f093b-158">Étape 4 : Afficher les informations utilisateur</span><span class="sxs-lookup"><span data-stu-id="f093b-158">Step 4: Display user information</span></span>
<span data-ttu-id="f093b-159">Lorsqu’il authentifie les utilisateurs avec OpenID Connect, Azure AD renvoie un id_token à l’application qui contient des « revendications » ou des assertions concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f093b-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="f093b-160">Vous pouvez utiliser ces revendications pour personnaliser l’application de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="f093b-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="f093b-161">Ouvrez le fichier Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="f093b-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="f093b-162">Vous pouvez accéder aux revendications de l’utilisateur dans vos contrôleurs via l’objet principal de sécurité `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="f093b-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="f093b-163">Générez et exécutez l'application.</span><span class="sxs-lookup"><span data-stu-id="f093b-163">Build and run the app.</span></span> <span data-ttu-id="f093b-164">Si vous n’avez pas encore créé un nouvel utilisateur dans votre client avec un domaine onmicrosoft.com, il est temps de le faire.</span><span class="sxs-lookup"><span data-stu-id="f093b-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="f093b-165">Voici comment procéder :</span><span class="sxs-lookup"><span data-stu-id="f093b-165">Here's how:</span></span>

  <span data-ttu-id="f093b-166">a.</span><span class="sxs-lookup"><span data-stu-id="f093b-166">a.</span></span> <span data-ttu-id="f093b-167">Connectez-vous avec les informations d’identification de cet utilisateur et observez la façon dont l’identité de l’utilisateur se reflète dans la barre supérieure.</span><span class="sxs-lookup"><span data-stu-id="f093b-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="f093b-168">b.</span><span class="sxs-lookup"><span data-stu-id="f093b-168">b.</span></span> <span data-ttu-id="f093b-169">Déconnectez-vous, puis reconnectez-vous sous le nom d’un autre utilisateur de votre client.</span><span class="sxs-lookup"><span data-stu-id="f093b-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="f093b-170">c.</span><span class="sxs-lookup"><span data-stu-id="f093b-170">c.</span></span> <span data-ttu-id="f093b-171">Si vous vous sentez particulièrement ambitieux, enregistrez et exécutez une autre instance de cette application (avec son propre ID de client) et observez le fonctionnement de la connexion unique.</span><span class="sxs-lookup"><span data-stu-id="f093b-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f093b-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f093b-172">Next steps</span></span>
<span data-ttu-id="f093b-173">Pour référence, consultez [l’exemple terminé](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sans vos valeurs de configuration).</span><span class="sxs-lookup"><span data-stu-id="f093b-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="f093b-174">Vous pouvez maintenant aborder des rubriques plus avancées.</span><span class="sxs-lookup"><span data-stu-id="f093b-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="f093b-175">Par exemple, essayez de [Sécuriser une API web avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f093b-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
