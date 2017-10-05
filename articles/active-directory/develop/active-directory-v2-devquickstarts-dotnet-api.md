---
title: "Ajoutez la connexion à une API web MVC .NET à l’aide du point de terminaison Azure AD v2.0 | Microsoft Docs"
description: "Génération d’une API web MVC .NET qui accepte les jetons des comptes Microsoft personnels et des comptes professionnels ou scolaires."
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
ms.openlocfilehash: b2d7bbfcd9218698f71e9dfdb1ad5d9ff8740f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="d0941-103">Sécurisation d’une API Web MVC</span><span class="sxs-lookup"><span data-stu-id="d0941-103">Secure an MVC web API</span></span>
<span data-ttu-id="d0941-104">Le point de terminaison v2.0 Azure Active Directory vous permet de protéger une API Web à l’aide des jetons d’accès [OAuth 2.0](active-directory-v2-protocols.md) , ce qui permet aux utilisateurs disposant d’un compte Microsoft personnel et de comptes professionnels ou scolaires d’accéder en toute sécurité à votre API Web.</span><span class="sxs-lookup"><span data-stu-id="d0941-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="d0941-105">Les scénarios et les fonctionnalités Azure Active Directory ne sont pas tous pris en charge par le point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="d0941-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="d0941-106">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limites de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d0941-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="d0941-107">Dans les API web ASP.NET, vous pouvez y parvenir en utilisant l’intergiciel OWIN de Microsoft inclus dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d0941-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="d0941-108">Ici, nous allons utiliser OWIN pour générer une API Web MVC « To Do List » (Liste de tâches) qui permet aux clients de créer et lire des tâches à partir de la liste de tâches d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d0941-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="d0941-109">L’API Web valide que les demandes entrantes contiennent un jeton d’accès valide et rejettent les demandes qui échouent à la validation sur un itinéraire protégé.</span><span class="sxs-lookup"><span data-stu-id="d0941-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="d0941-110">Cet exemple a été créé à l’aide de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d0941-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="d0941-111">Télécharger</span><span class="sxs-lookup"><span data-stu-id="d0941-111">Download</span></span>
<span data-ttu-id="d0941-112">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="d0941-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="d0941-113">Pour suivre la procédure, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou la cloner :</span><span class="sxs-lookup"><span data-stu-id="d0941-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="d0941-114">L’application squelette comprend l’ensemble du code réutilisable associé à une API simple, mais n’intègre pas l’ensemble des éléments liés à l’identité.</span><span class="sxs-lookup"><span data-stu-id="d0941-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="d0941-115">Si vous ne souhaitez pas suivre la procédure, vous pouvez cloner ou [télécharger l’exemple terminé](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d0941-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="d0941-116">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="d0941-116">Register an app</span></span>
<span data-ttu-id="d0941-117">Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d0941-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="d0941-118">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="d0941-118">Make sure to:</span></span>

* <span data-ttu-id="d0941-119">copier l' **ID d'application** attribué à votre application, vous en aurez bientôt besoin ;</span><span class="sxs-lookup"><span data-stu-id="d0941-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="d0941-120">Cette solution Visual Studio contient également une valeur « TodoListClient », qui est une application simple WPF.</span><span class="sxs-lookup"><span data-stu-id="d0941-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="d0941-121">La valeur « TodoListClient » permet d'indiquer comment un utilisateur se connecte et comment un client peut émettre des requêtes à votre API Web.</span><span class="sxs-lookup"><span data-stu-id="d0941-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="d0941-122">Les valeurs TodoListClient et TodoListService sont, dans ce cas, représentées par la même application.</span><span class="sxs-lookup"><span data-stu-id="d0941-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="d0941-123">Pour configurer la valeur TodoListClient, vous devez également :</span><span class="sxs-lookup"><span data-stu-id="d0941-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="d0941-124">ajouter la plateforme **Mobile** pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="d0941-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="d0941-125">Installer OWIN</span><span class="sxs-lookup"><span data-stu-id="d0941-125">Install OWIN</span></span>
<span data-ttu-id="d0941-126">Une fois l'application enregistrée, vous devez la configurer pour qu'elle puisse communiquer avec le point de terminaison v2.0 afin de valider les requêtes entrantes et les jetons.</span><span class="sxs-lookup"><span data-stu-id="d0941-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="d0941-127">Pour commencer, ouvrez la solution et ajoutez les packages NuGet de l’intergiciel OWIN au projet TodoListService à l’aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="d0941-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="d0941-128">Configurer l’authentification OAuth</span><span class="sxs-lookup"><span data-stu-id="d0941-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="d0941-129">Ajoutez une classe de démarrage OWIN au projet TodoListService appelé `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="d0941-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="d0941-130">Cliquez avec le bouton droit sur le projet --> **Ajouter** --> **Nouvel élément** --> Recherchez « OWIN ».</span><span class="sxs-lookup"><span data-stu-id="d0941-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="d0941-131">L’intergiciel OWIN appelle la méthode `Configuration(…)` lorsque votre application démarre.</span><span class="sxs-lookup"><span data-stu-id="d0941-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="d0941-132">Modifiez la déclaration de classe en `public partial class Startup` .</span><span class="sxs-lookup"><span data-stu-id="d0941-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="d0941-133">Dans la méthode `Configuration(…)`, appelez ConfgureAuth(...) pour configurer l’authentification pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="d0941-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="d0941-134">Ouvrez le fichier `App_Start\Startup.Auth.cs` et implémentez la méthode `ConfigureAuth(…)`, qui configure l’API web pour accepter les jetons du point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="d0941-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="d0941-135">Vous pouvez désormais utiliser les attributs `[Authorize]` pour protéger vos contrôleurs et vos actions avec l’authentification de porteur OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d0941-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="d0941-136">Décorez la classe `Controllers\TodoListController.cs` avec une balise authorize.</span><span class="sxs-lookup"><span data-stu-id="d0941-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="d0941-137">Cela force l’utilisateur à se connecter avant d’accéder à cette page.</span><span class="sxs-lookup"><span data-stu-id="d0941-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="d0941-138">Lorsqu’un appelant autorisé appelle correctement l’une des API `TodoListController` , l’action peut avoir besoin d’accéder aux informations sur l’appelant.</span><span class="sxs-lookup"><span data-stu-id="d0941-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="d0941-139">OWIN fournit l’accès aux revendications dans le jeton porteur via l’objet `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="d0941-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="d0941-140">Enfin, ouvrez le fichier `web.config` dans la racine du projet ToDoListService, puis entrez les valeurs de configuration dans la section `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="d0941-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="d0941-141">`ida:Audience` est l’ **ID de l’application** que vous avez entré dans le portail.</span><span class="sxs-lookup"><span data-stu-id="d0941-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="d0941-142">Configurer l’application cliente</span><span class="sxs-lookup"><span data-stu-id="d0941-142">Configure the client app</span></span>
<span data-ttu-id="d0941-143">Avant de pouvoir voir le service Todo List en action, vous devez configurer le client Todo List afin qu’il puisse obtenir des jetons du point de terminaison v2.0 et effectuer des appels au service.</span><span class="sxs-lookup"><span data-stu-id="d0941-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="d0941-144">Dans le projet TodoListClient, ouvrez `App.config` et entrez les valeurs de votre configuration dans la section `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="d0941-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="d0941-145">`ida:ClientId` est l’ID d’application que vous avez copié à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="d0941-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="d0941-146">Enfin, nettoyez, générez et exécutez chaque projet.</span><span class="sxs-lookup"><span data-stu-id="d0941-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="d0941-147">Vous disposez maintenant d’une API web MVC .NET qui accepte les jetons des comptes Microsoft personnels et des comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="d0941-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="d0941-148">Connectez-vous au projet TodoListClient, puis appelez votre API web pour ajouter des tâches à la liste des tâches de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d0941-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="d0941-149">Pour référence, l’exemple terminé (sans vos valeurs de configuration) [est fourni ici au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip). Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="d0941-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="d0941-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0941-150">Next steps</span></span>
<span data-ttu-id="d0941-151">Vous pouvez à présent passer à d’autres rubriques.</span><span class="sxs-lookup"><span data-stu-id="d0941-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="d0941-152">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d0941-152">You may want to try:</span></span>

[<span data-ttu-id="d0941-153">Appeler une API web à partir d’une application web >></span><span class="sxs-lookup"><span data-stu-id="d0941-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="d0941-154">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="d0941-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="d0941-155">Guide du développeur 2.0 >></span><span class="sxs-lookup"><span data-stu-id="d0941-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="d0941-156">Balise StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="d0941-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d0941-157">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="d0941-157">Get security updates for our products</span></span>
<span data-ttu-id="d0941-158">Nous vous encourageons à activer les notifications d’incidents de sécurité en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et en vous abonnant aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d0941-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
