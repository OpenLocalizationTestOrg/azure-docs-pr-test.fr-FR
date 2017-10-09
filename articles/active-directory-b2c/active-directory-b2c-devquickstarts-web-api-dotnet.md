---
title: aaaAzure Active Directory B2C | Documents Microsoft
description: "Comment toobuild une application Web .NET et appeler une web api à l’aide des jetons d’accès Azure Active Directory B2C et OAuth 2.0."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="1279a-103">Azure AD B2C : appel d’une API web .NET à partir d’une application web .NET</span><span class="sxs-lookup"><span data-stu-id="1279a-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="1279a-104">À l’aide de Azure AD B2C, vous pouvez ajouter des fonctionnalités puissantes identité gestion tooyour des applications web et des API web.</span><span class="sxs-lookup"><span data-stu-id="1279a-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="1279a-105">Cet article explique comment toorequest jetons d’accès et effectuer des appels à partir d’une « liste de tâches » .NET tooa d’application web .NET web api.</span><span class="sxs-lookup"><span data-stu-id="1279a-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="1279a-106">Cet article ne couvre pas comment tooimplement connectez-vous, d’abonnement et de profil de gestion avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="1279a-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="1279a-107">Il se concentre sur des API web appelant après que hello utilisateur est déjà authentifié.</span><span class="sxs-lookup"><span data-stu-id="1279a-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="1279a-108">Si vous ne l’avez pas déjà fait, consultez :</span><span class="sxs-lookup"><span data-stu-id="1279a-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="1279a-109">Bien démarrer avec une [application web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="1279a-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="1279a-110">Bien démarrer avec une [API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="1279a-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="1279a-111">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="1279a-111">Prerequisite</span></span>

<span data-ttu-id="1279a-112">toobuild une application web qui appelle une web api, vous devez :</span><span class="sxs-lookup"><span data-stu-id="1279a-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="1279a-113">[Créez un locataire Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1279a-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="1279a-114">[Inscrivez une API web](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="1279a-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="1279a-115">[Inscrivez une application web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="1279a-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="1279a-116">[Configurez des stratégies](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1279a-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="1279a-117">[Grant Bonjour web application autorisations toouse Bonjour web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="1279a-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1279a-118">application cliente de Hello et API web doivent utiliser Active de B2C hello même instance Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1279a-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="1279a-119">Télécharger le code de hello</span><span class="sxs-lookup"><span data-stu-id="1279a-119">Download hello code</span></span>

<span data-ttu-id="1279a-120">code Hello pour ce didacticiel est conservée sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="1279a-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="1279a-121">Vous pouvez cloner l’exemple hello en exécutant :</span><span class="sxs-lookup"><span data-stu-id="1279a-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="1279a-122">Après avoir téléchargé l’exemple de code hello, ouvrez hello tooget du fichier .sln de Visual Studio a démarré.</span><span class="sxs-lookup"><span data-stu-id="1279a-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="1279a-123">fichier de solution Hello contient deux projets : `TaskWebApp` et `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="1279a-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="1279a-124">`TaskWebApp`est une application web MVC hello utilisateur interagit avec.</span><span class="sxs-lookup"><span data-stu-id="1279a-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="1279a-125">`TaskService`est web principal API de l’application hello qui stocke la liste des actions de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1279a-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="1279a-126">Cet article ne couvre pas la construction hello `TaskWebApp` web app ou hello `TaskService` web api.</span><span class="sxs-lookup"><span data-stu-id="1279a-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="1279a-127">toolearn comment toobuild hello .NET web app à l’aide d’Azure AD B2C, consultez notre [didacticiel d’application web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="1279a-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="1279a-128">toolearn comment toobuild hello .NET web API sécurisé à l’aide d’Azure AD B2C, consultez notre [didacticiel d’API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1279a-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="1279a-129">Mettre à jour la configuration de hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="1279a-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="1279a-130">Notre exemple est configuré toouse hello stratégies et ID de client de notre client de démonstration.</span><span class="sxs-lookup"><span data-stu-id="1279a-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="1279a-131">Si vous souhaitez que toouse votre propre locataire :</span><span class="sxs-lookup"><span data-stu-id="1279a-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="1279a-132">Ouvrez `web.config` Bonjour `TaskService` de projet et remplacer les valeurs hello pour</span><span class="sxs-lookup"><span data-stu-id="1279a-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="1279a-133">`ida:Tenant` par le nom de votre locataire</span><span class="sxs-lookup"><span data-stu-id="1279a-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="1279a-134">`ida:ClientId` par votre ID d’application d’API web</span><span class="sxs-lookup"><span data-stu-id="1279a-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="1279a-135">`ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="1279a-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="1279a-136">Ouvrez `web.config` Bonjour `TaskWebApp` de projet et remplacer les valeurs hello pour</span><span class="sxs-lookup"><span data-stu-id="1279a-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="1279a-137">`ida:Tenant` par le nom de votre locataire</span><span class="sxs-lookup"><span data-stu-id="1279a-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="1279a-138">`ida:ClientId` par votre ID d’application web</span><span class="sxs-lookup"><span data-stu-id="1279a-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="1279a-139">`ida:ClientSecret` par votre clé secrète d’application web</span><span class="sxs-lookup"><span data-stu-id="1279a-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="1279a-140">`ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion</span><span class="sxs-lookup"><span data-stu-id="1279a-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="1279a-141">`ida:EditProfilePolicyId` par votre nom de stratégie « Modifier le profil »</span><span class="sxs-lookup"><span data-stu-id="1279a-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="1279a-142">`ida:ResetPasswordPolicyId` par votre nom de stratégie « Modifier le mot de passe »</span><span class="sxs-lookup"><span data-stu-id="1279a-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="1279a-143">Demande et enregistrement d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="1279a-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="1279a-144">Spécifier des autorisations de hello</span><span class="sxs-lookup"><span data-stu-id="1279a-144">Specify hello permissions</span></span>

<span data-ttu-id="1279a-145">Dans l’ordre toomake hello appel toohello API web, vous avez besoin d’un utilisateur de hello tooauthenticate (à l’aide de votre stratégie de connexion-haut/connectez-vous) et [recevoir un jeton d’accès](active-directory-b2c-access-tokens.md) à partir d’Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="1279a-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="1279a-146">Dans l’ordre tooreceive un jeton d’accès, vous devez d’abord spécifier les autorisations hello vous aimeriez toogrant de jeton accès hello.</span><span class="sxs-lookup"><span data-stu-id="1279a-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="1279a-147">les autorisations de Hello sont spécifiées dans hello `scope` paramètre lorsque vous apportez hello demande toohello `/authorize` point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="1279a-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="1279a-148">Par exemple, tooacquire autorisation toohello ressource application qui a un jeton d’accès avec hello « lecture » hello URI ID d’application de `https://contoso.onmicrosoft.com/tasks`, étendue de hello serait `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="1279a-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="1279a-149">étendue de hello toospecify dans notre fichier exemple, ouvrez hello `App_Start\Startup.Auth.cs` et définir hello `Scope` variable OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="1279a-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="1279a-150">Exchange hello le code d’autorisation pour un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="1279a-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="1279a-151">Un utilisateur après une expérience d’inscription ou connectez-vous hello, votre application reçoit un code d’autorisation à partir d’Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="1279a-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="1279a-152">intergiciel (middleware) OWIN OpenID Connect Hello stockera les code hello, mais ne le n'est pas échanger de jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="1279a-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="1279a-153">Vous pouvez utiliser hello [bibliothèque MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) exchange de hello toomake.</span><span class="sxs-lookup"><span data-stu-id="1279a-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="1279a-154">Dans notre exemple, nous avons configuré un rappel de notification dans l’intergiciel (middleware) hello OpenID Connect lorsqu’un code d’autorisation est reçu.</span><span class="sxs-lookup"><span data-stu-id="1279a-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="1279a-155">Dans le rappel hello, nous utiliser le code MSAL tooexchange hello pour un jeton et enregistrer le jeton de hello dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="1279a-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a><span data-ttu-id="1279a-156">Appel de l’API web de hello</span><span class="sxs-lookup"><span data-stu-id="1279a-156">Calling hello web API</span></span>

<span data-ttu-id="1279a-157">Cette section décrit la façon dont le jeton de hello toouse reçu pendant connexion-haut/connectez-vous avec Azure AD B2C dans l’ordre tooaccess hello API web.</span><span class="sxs-lookup"><span data-stu-id="1279a-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="1279a-158">Récupérer le jeton hello enregistré dans les contrôleurs de hello</span><span class="sxs-lookup"><span data-stu-id="1279a-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="1279a-159">Hello `TasksController` est responsable de la communication avec l’API web de hello et d’envoi HTTP demandes toohello API tooread, créer et supprimer des tâches.</span><span class="sxs-lookup"><span data-stu-id="1279a-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="1279a-160">Hello API est sécurisé par Azure AD B2C, vous devez toofirst récupérer le jeton hello que vous avez enregistré dans hello ci-dessus étape.</span><span class="sxs-lookup"><span data-stu-id="1279a-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="1279a-161">Lire des tâches à partir de l’API web de hello</span><span class="sxs-lookup"><span data-stu-id="1279a-161">Read tasks from hello web API</span></span>

<span data-ttu-id="1279a-162">Lorsque vous disposez d’un jeton, vous pouvez attacher toohello HTTP `GET` demande Bonjour `Authorization` appel de toosecurely en-tête `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="1279a-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="1279a-163">Créer et supprimer des tâches sur le web hello API</span><span class="sxs-lookup"><span data-stu-id="1279a-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="1279a-164">Hello suivent même modèle lorsque vous envoyez `POST` et `DELETE` toohello web API, les demandes à l’aide de jeton d’accès hello MSAL tooretrieve à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="1279a-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="1279a-165">Exécutez l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="1279a-165">Run hello sample app</span></span>

<span data-ttu-id="1279a-166">Enfin, générez et exécutez les deux applications hello.</span><span class="sxs-lookup"><span data-stu-id="1279a-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="1279a-167">S’inscrire et se connecter et créer des tâches de l’utilisateur connecté hello.</span><span class="sxs-lookup"><span data-stu-id="1279a-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="1279a-168">Déconnectez-vous et connectez-vous en tant qu’autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1279a-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="1279a-169">Créer des tâches pour cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1279a-169">Create tasks for that user.</span></span> <span data-ttu-id="1279a-170">Notez que les tâches de hello sont stockées par utilisateur sur hello API, étant donné que hello API extrait hello l’identité d’utilisateur à partir du jeton hello qu’il reçoit.</span><span class="sxs-lookup"><span data-stu-id="1279a-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="1279a-171">Essayez également de lire des étendues de hello.</span><span class="sxs-lookup"><span data-stu-id="1279a-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="1279a-172">Supprimer l’autorisation de hello trop « écriture » et réessayez d’ajouter une tâche.</span><span class="sxs-lookup"><span data-stu-id="1279a-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="1279a-173">Assurez-vous simplement que toosign chaque fois que vous modifiez l’étendue de hello.</span><span class="sxs-lookup"><span data-stu-id="1279a-173">Just make sure toosign out each time you change hello scope.</span></span>

