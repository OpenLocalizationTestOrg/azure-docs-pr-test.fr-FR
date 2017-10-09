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
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C : appel d’une API web .NET à partir d’une application web .NET

À l’aide de Azure AD B2C, vous pouvez ajouter des fonctionnalités puissantes identité gestion tooyour des applications web et des API web. Cet article explique comment toorequest jetons d’accès et effectuer des appels à partir d’une « liste de tâches » .NET tooa d’application web .NET web api.

Cet article ne couvre pas comment tooimplement connectez-vous, d’abonnement et de profil de gestion avec Azure Active Directory B2C. Il se concentre sur des API web appelant après que hello utilisateur est déjà authentifié. Si vous ne l’avez pas déjà fait, consultez :

* Bien démarrer avec une [application web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* Bien démarrer avec une [API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>Configuration requise

toobuild une application web qui appelle une web api, vous devez :

1. [Créez un locataire Azure AD B2C](active-directory-b2c-get-started.md).
2. [Inscrivez une API web](active-directory-b2c-app-registration.md#register-a-web-api).
3. [Inscrivez une application web](active-directory-b2c-app-registration.md#register-a-web-app).
4. [Configurez des stratégies](active-directory-b2c-reference-policies.md).
5. [Grant Bonjour web application autorisations toouse Bonjour web api](active-directory-b2c-access-tokens.md#publishing-permissions).

> [!IMPORTANT]
> application cliente de Hello et API web doivent utiliser Active de B2C hello même instance Azure AD.
>

## <a name="download-hello-code"></a>Télécharger le code de hello

code Hello pour ce didacticiel est conservée sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Vous pouvez cloner l’exemple hello en exécutant :

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Après avoir téléchargé l’exemple de code hello, ouvrez hello tooget du fichier .sln de Visual Studio a démarré. fichier de solution Hello contient deux projets : `TaskWebApp` et `TaskService`. `TaskWebApp`est une application web MVC hello utilisateur interagit avec. `TaskService`est web principal API de l’application hello qui stocke la liste des actions de chaque utilisateur. Cet article ne couvre pas la construction hello `TaskWebApp` web app ou hello `TaskService` web api. toolearn comment toobuild hello .NET web app à l’aide d’Azure AD B2C, consultez notre [didacticiel d’application web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md). toolearn comment toobuild hello .NET web API sécurisé à l’aide d’Azure AD B2C, consultez notre [didacticiel d’API web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Mettre à jour la configuration de hello Azure AD B2C

Notre exemple est configuré toouse hello stratégies et ID de client de notre client de démonstration. Si vous souhaitez que toouse votre propre locataire :

1. Ouvrez `web.config` Bonjour `TaskService` de projet et remplacer les valeurs hello pour

    * `ida:Tenant` par le nom de votre locataire
    * `ida:ClientId` par votre ID d’application d’API web
    * `ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion

2. Ouvrez `web.config` Bonjour `TaskWebApp` de projet et remplacer les valeurs hello pour

    * `ida:Tenant` par le nom de votre locataire
    * `ida:ClientId` par votre ID d’application web
    * `ida:ClientSecret` par votre clé secrète d’application web
    * `ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion
    * `ida:EditProfilePolicyId` par votre nom de stratégie « Modifier le profil »
    * `ida:ResetPasswordPolicyId` par votre nom de stratégie « Modifier le mot de passe »



## <a name="requesting-and-saving-an-access-token"></a>Demande et enregistrement d’un jeton d’accès

### <a name="specify-hello-permissions"></a>Spécifier des autorisations de hello

Dans l’ordre toomake hello appel toohello API web, vous avez besoin d’un utilisateur de hello tooauthenticate (à l’aide de votre stratégie de connexion-haut/connectez-vous) et [recevoir un jeton d’accès](active-directory-b2c-access-tokens.md) à partir d’Azure Active Directory B2C. Dans l’ordre tooreceive un jeton d’accès, vous devez d’abord spécifier les autorisations hello vous aimeriez toogrant de jeton accès hello. les autorisations de Hello sont spécifiées dans hello `scope` paramètre lorsque vous apportez hello demande toohello `/authorize` point de terminaison. Par exemple, tooacquire autorisation toohello ressource application qui a un jeton d’accès avec hello « lecture » hello URI ID d’application de `https://contoso.onmicrosoft.com/tasks`, étendue de hello serait `https://contoso.onmicrosoft.com/tasks/read`.

étendue de hello toospecify dans notre fichier exemple, ouvrez hello `App_Start\Startup.Auth.cs` et définir hello `Scope` variable OpenIdConnectAuthenticationOptions.

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

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>Exchange hello le code d’autorisation pour un jeton d’accès

Un utilisateur après une expérience d’inscription ou connectez-vous hello, votre application reçoit un code d’autorisation à partir d’Azure Active Directory B2C. intergiciel (middleware) OWIN OpenID Connect Hello stockera les code hello, mais ne le n'est pas échanger de jeton d’accès. Vous pouvez utiliser hello [bibliothèque MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) exchange de hello toomake. Dans notre exemple, nous avons configuré un rappel de notification dans l’intergiciel (middleware) hello OpenID Connect lorsqu’un code d’autorisation est reçu. Dans le rappel hello, nous utiliser le code MSAL tooexchange hello pour un jeton et enregistrer le jeton de hello dans le cache de hello.

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

## <a name="calling-hello-web-api"></a>Appel de l’API web de hello

Cette section décrit la façon dont le jeton de hello toouse reçu pendant connexion-haut/connectez-vous avec Azure AD B2C dans l’ordre tooaccess hello API web.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Récupérer le jeton hello enregistré dans les contrôleurs de hello

Hello `TasksController` est responsable de la communication avec l’API web de hello et d’envoi HTTP demandes toohello API tooread, créer et supprimer des tâches. Hello API est sécurisé par Azure AD B2C, vous devez toofirst récupérer le jeton hello que vous avez enregistré dans hello ci-dessus étape.

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

### <a name="read-tasks-from-hello-web-api"></a>Lire des tâches à partir de l’API web de hello

Lorsque vous disposez d’un jeton, vous pouvez attacher toohello HTTP `GET` demande Bonjour `Authorization` appel de toosecurely en-tête `TaskService`:

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

### <a name="create-and-delete-tasks-on-hello-web-api"></a>Créer et supprimer des tâches sur le web hello API

Hello suivent même modèle lorsque vous envoyez `POST` et `DELETE` toohello web API, les demandes à l’aide de jeton d’accès hello MSAL tooretrieve à partir du cache de hello.

## <a name="run-hello-sample-app"></a>Exécutez l’exemple d’application hello

Enfin, générez et exécutez les deux applications hello. S’inscrire et se connecter et créer des tâches de l’utilisateur connecté hello. Déconnectez-vous et connectez-vous en tant qu’autre utilisateur. Créer des tâches pour cet utilisateur. Notez que les tâches de hello sont stockées par utilisateur sur hello API, étant donné que hello API extrait hello l’identité d’utilisateur à partir du jeton hello qu’il reçoit. Essayez également de lire des étendues de hello. Supprimer l’autorisation de hello trop « écriture » et réessayez d’ajouter une tâche. Assurez-vous simplement que toosign chaque fois que vous modifiez l’étendue de hello.

