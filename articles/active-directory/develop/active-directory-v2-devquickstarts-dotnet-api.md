---
title: "à l’aide des API web .NET MVC connectez-vous tooa aaaAdd hello de point de terminaison Azure AD v2.0 | Documents Microsoft"
description: Comment toobuild une Api Web de MVC .NET qui accepte les jetons de deux Account personnel de Microsoft et comptes professionnels ou scolaires.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="1ce25-103">Sécurisation d’une API Web MVC</span><span class="sxs-lookup"><span data-stu-id="1ce25-103">Secure an MVC web API</span></span>
<span data-ttu-id="1ce25-104">Avec le point de terminaison Azure Active Directory hello v2.0, vous pouvez protéger un à l’aide de l’API Web [OAuth 2.0](active-directory-v2-protocols.md) jetons d’accès, l’activation des utilisateurs avec les deux compte Microsoft personnel et les comptes professionnels ou scolaires toosecurely accéder à votre API Web.</span><span class="sxs-lookup"><span data-stu-id="1ce25-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="1ce25-105">Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="1ce25-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="1ce25-106">toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="1ce25-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="1ce25-107">Dans les API web ASP.NET, vous pouvez y parvenir en utilisant l’intergiciel OWIN de Microsoft inclus dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="1ce25-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="1ce25-108">Ici, nous allons utiliser OWIN toobuild une API Web MVC « tooDo liste » qui permet aux clients des tâches toocreate et en lecture à partir de la liste des actions d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1ce25-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="1ce25-109">API web de Hello validera que les demandes entrantes contiennent un jeton d’accès valide et rejettent les demandes qui ne passent pas de validation sur un itinéraire protégé.</span><span class="sxs-lookup"><span data-stu-id="1ce25-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="1ce25-110">Cet exemple a été créé à l’aide de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="1ce25-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="1ce25-111">Télécharger</span><span class="sxs-lookup"><span data-stu-id="1ce25-111">Download</span></span>
<span data-ttu-id="1ce25-112">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="1ce25-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="1ce25-113">toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="1ce25-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="1ce25-114">application squelette Hello inclut tout le code réutilisable hello pour une API simple, mais il manque l’intégralité des hello liées à l’identité.</span><span class="sxs-lookup"><span data-stu-id="1ce25-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="1ce25-115">Si vous ne souhaitez pas toofollow le long, vous pouvez à la place cloner ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="1ce25-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="1ce25-116">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="1ce25-116">Register an app</span></span>
<span data-ttu-id="1ce25-117">Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="1ce25-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="1ce25-118">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="1ce25-118">Make sure to:</span></span>

* <span data-ttu-id="1ce25-119">Copie vers le bas hello **Id d’Application** affecté tooyour application, vous en aurez besoin plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="1ce25-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="1ce25-120">Cette solution Visual Studio contient également une valeur « TodoListClient », qui est une application simple WPF.</span><span class="sxs-lookup"><span data-stu-id="1ce25-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="1ce25-121">Hello TodoListClient est utilisé toodemonstrate comment un utilisateur se connecte en et comment un client peut émettre des demandes tooyour API Web.</span><span class="sxs-lookup"><span data-stu-id="1ce25-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="1ce25-122">Dans ce cas, hello TodoListClient et hello TodoListService sont représentées par hello même application.</span><span class="sxs-lookup"><span data-stu-id="1ce25-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="1ce25-123">tooconfigure hello TodoListClient, vous devez également :</span><span class="sxs-lookup"><span data-stu-id="1ce25-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="1ce25-124">Ajouter hello **Mobile** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="1ce25-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="1ce25-125">Installer OWIN</span><span class="sxs-lookup"><span data-stu-id="1ce25-125">Install OWIN</span></span>
<span data-ttu-id="1ce25-126">Maintenant que vous avez inscrit une application, vous avez besoin tooset toocommunicate de votre application avec le point de terminaison hello v2.0 dans un ordre toovalidate les demandes entrantes et les jetons.</span><span class="sxs-lookup"><span data-stu-id="1ce25-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="1ce25-127">toobegin, ouvrez la solution de hello et ajoutez hello OWIN intergiciel (middleware) NuGet packages toohello TodoListService projet à l’aide de la Console du Gestionnaire de Package de hello.</span><span class="sxs-lookup"><span data-stu-id="1ce25-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="1ce25-128">Configurer l’authentification OAuth</span><span class="sxs-lookup"><span data-stu-id="1ce25-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="1ce25-129">Ajouter un projet de démarrage OWIN la TodoListService de toohello de la classe appelé `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="1ce25-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="1ce25-130">Un clic droit sur le projet de hello--> **ajouter** --> **un nouvel élément** --> Recherchez « OWIN ».</span><span class="sxs-lookup"><span data-stu-id="1ce25-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="1ce25-131">intergiciel (middleware) OWIN de Hello appellera hello `Configuration(…)` méthode au démarrage de votre application.</span><span class="sxs-lookup"><span data-stu-id="1ce25-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="1ce25-132">Modifier trop de déclaration de classe hello`public partial class Startup` -nous avons déjà implémenté le cadre de cette classe pour vous dans un autre fichier.</span><span class="sxs-lookup"><span data-stu-id="1ce25-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="1ce25-133">Bonjour `Configuration(…)` (méthode), effectuer un tooset de tooConfgureAuth(...) d’appel de l’authentification pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="1ce25-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="1ce25-134">Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et implémenter hello `ConfigureAuth(…)` (méthode), qui définit les jetons de tooaccept hello API Web à partir du point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="1ce25-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="1ce25-135">Vous pouvez désormais utiliser `[Authorize]` attributs tooprotect vos contrôleurs et vos actions avec l’authentification du support OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1ce25-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="1ce25-136">Décorer hello `Controllers\TodoListController.cs` classe avec une balise authorize.</span><span class="sxs-lookup"><span data-stu-id="1ce25-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="1ce25-137">Cela obligera toosign d’utilisateur hello dans avant d’accéder à cette page.</span><span class="sxs-lookup"><span data-stu-id="1ce25-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="1ce25-138">Quand un appelant autorisé correctement appelle l’une des hello `TodoListController` API, action de hello peut-être besoin d’accès tooinformation sur l’appelant de hello.</span><span class="sxs-lookup"><span data-stu-id="1ce25-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="1ce25-139">OWIN fournit des revendications toohello d’accès à l’intérieur du jeton de support hello via hello `ClaimsPrincpal` objet.</span><span class="sxs-lookup"><span data-stu-id="1ce25-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="1ce25-140">Enfin, ouvrez hello `web.config` fichier racine hello du projet TodoListService de hello et entrez les valeurs de configuration Bonjour `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="1ce25-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="1ce25-141">Votre `ida:Audience` est hello **Id d’Application** de l’application hello que vous avez entré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="1ce25-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="1ce25-142">Configurer l’application cliente de hello</span><span class="sxs-lookup"><span data-stu-id="1ce25-142">Configure hello client app</span></span>
<span data-ttu-id="1ce25-143">Avant de pouvoir afficher hello Service de liste de tâches en action, vous devez tooconfigure hello Client de liste de tâches afin de pouvoir obtenir des jetons à partir du point de terminaison v2.0 hello et effectuer des appels toohello service.</span><span class="sxs-lookup"><span data-stu-id="1ce25-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="1ce25-144">Dans le projet de TodoListClient hello, ouvrez `App.config` et entrez les valeurs de configuration Bonjour `<appSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="1ce25-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="1ce25-145">Votre `ida:ClientId` vous avez copié à partir du portail de hello Id d’Application.</span><span class="sxs-lookup"><span data-stu-id="1ce25-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="1ce25-146">Enfin, nettoyez, générez et exécutez chaque projet.</span><span class="sxs-lookup"><span data-stu-id="1ce25-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="1ce25-147">Vous disposez maintenant d’une API web MVC .NET qui accepte les jetons des comptes Microsoft personnels et des comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="1ce25-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="1ce25-148">Connectez-vous à hello TodoListClient et appelez la liste de tâches web api tooadd tâches toohello de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1ce25-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="1ce25-149">Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie en tant qu’un fichier zip ici](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), ou vous pouvez le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="1ce25-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="1ce25-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ce25-150">Next steps</span></span>
<span data-ttu-id="1ce25-151">Vous pouvez à présent passer à d’autres rubriques.</span><span class="sxs-lookup"><span data-stu-id="1ce25-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="1ce25-152">Vous souhaiterez peut-être tootry :</span><span class="sxs-lookup"><span data-stu-id="1ce25-152">You may want tootry:</span></span>

[<span data-ttu-id="1ce25-153">Appeler une API web à partir d’une application web &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="1ce25-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="1ce25-154">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="1ce25-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="1ce25-155">guide du développeur v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="1ce25-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="1ce25-156">Balise StackOverflow "azure-active-directory" &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="1ce25-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="1ce25-157">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="1ce25-157">Get security updates for our products</span></span>
<span data-ttu-id="1ce25-158">Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="1ce25-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
