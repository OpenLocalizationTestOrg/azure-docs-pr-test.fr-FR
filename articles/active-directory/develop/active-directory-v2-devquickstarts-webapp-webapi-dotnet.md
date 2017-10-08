---
title: aaaAzure AD v2.0 .NET web application appelant API est prise en main | Documents Microsoft
description: "Comment toobuild application Web MVC .NET qui appelle web services à l’aide de Microsoft personnel des comptes et de travail ou d’établissement scolaire pour la connexion."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a>Appeler une API web à partir d’une application web .NET
Avec le point de terminaison hello v2.0, vous pouvez rapidement ajouter des applications web d’authentification tooyour et API web avec prise en charge pour les deux comptes personnels de Microsoft et comptes professionnels ou scolaires.  Ici, nous allons créer une application web MVC qui connecte les utilisateurs à l’aide d’OpenID Connect, avec l’aide de l’intergiciel OWIN de Microsoft.  Hello web application sera obtenir des jetons d’accès OAuth 2.0 pour un site web api sécurisée par OAuth 2.0 qui permet de créer, lire et supprimer un utilisateur donné « liste des tâches ».

Ce didacticiel est concentrer principalement sur l’utilisation de MSAL tooacquire et utilise des jetons d’accès dans une application web, une description complète [ici](active-directory-v2-flows.md#web-apps).  En tant que composants requis, vous souhaiterez peut-être toofirst apprendre comment trop[ajouter une application web de base connectez-vous tooa](active-directory-v2-devquickstarts-dotnet-web.md) ou comment trop[sécuriser correctement une API web](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Télécharger l’exemple de code
code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) ou un clone hello squelette :

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

Vous pouvez également [télécharger une application hello terminée comme un fichier zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ou le clonage d’application hello terminée :

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>Inscription d’une application
Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).  Veillez à respecter les points suivants :

* Copie vers le bas hello **Id d’Application** affecté tooyour application, vous en aurez besoin plus rapidement.
* Créer un **Secret d’application** Hello **mot de passe** type et copie vers le bas de sa valeur pour une date ultérieure
* Ajouter hello **Web** plate-forme pour votre application.
* Entrez hello correct **URI de redirection**. uri de redirection Hello indique tooAzure AD dans lequel les réponses d’authentification doivent être dirigées - valeur par défaut de hello pour ce didacticiel est `https://localhost:44326/`.

## <a name="install-owin"></a>Installer OWIN
Ajouter hello OWIN intergiciel (middleware) NuGet packages toohello `TodoList-WebApp` projet à l’aide de hello Console du Gestionnaire de Package.  intergiciel (middleware) OWIN de Hello est tooissue utilisé les demandes de connexion et déconnexion, gérer la session de l’utilisateur hello et obtenir des informations sur l’utilisateur hello, entre autres.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a>Utilisateur de hello signe dans
À présent configurer Bonjour OWIN intergiciel (middleware) toouse Bonjour [protocole d’authentification OpenID Connect](active-directory-v2-protocols.md).  

* Ouvrez hello `web.config` fichier racine hello hello `TodoList-WebApp` le projet, puis entrez les valeurs de configuration de votre application Bonjour `<appSettings>` section.
  * Hello `ida:ClientId` est hello **Id d’Application** affecté application tooyour dans le portail de l’enregistrement hello.
  * Hello `ida:ClientSecret` est hello **Secret d’application** vous avez créé dans le portail de l’enregistrement hello.
  * Hello `ida:RedirectUri` est hello **Uri de redirection** vous avez entré dans le portail de hello.
* Ouvrez hello `web.config` fichier racine hello hello `TodoList-Service` le projet, puis remplacez hello `ida:Audience` avec hello même **Id d’Application** comme indiqué ci-dessus.
* Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et ajoutez `using` instructions pour les bibliothèques hello ci-dessus.
* Dans l’hello du même fichier, implémenter hello `ConfigureAuth(...)` (méthode).  Hello les paramètres que vous fournissez dans `OpenIDConnectAuthenticationOptions` servira de coordonnées pour toocommunicate de votre application auprès d’Azure AD.

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a>Utiliser des jetons d’accès MSAL tooget
Bonjour `AuthorizationCodeReceived` notification, nous souhaitons toouse [OAuth 2.0 en tandem avec OpenID Connect](active-directory-v2-protocols.md) authorization_code de hello tooredeem pour un toohello de jeton d’accès Service de liste de tâches.  La bibliothèque MSAL peut vous faciliter ce processus :

* Pour commencer, installez hello préversion de MSAL :

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* Et ajouter un autre `using` instruction toohello `App_Start\Startup.Auth.cs` fichier MSAL.
* Maintenant ajouter une nouvelle méthode hello `OnAuthorizationCodeReceived` Gestionnaire d’événements.  Ce gestionnaire utilisera MSAL tooacquire un toohello de jeton d’accès API de liste de tâches et stocke le jeton de hello dans le cache de jeton de MSAL pour une date ultérieure :

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* Dans les applications web, MSAL a un cache de jeton extensible qui peut être des jetons de toostore utilisé.  Cet exemple implémente hello `NaiveSessionCache` qui utilise des jetons de toocache de stockage de session http.

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a>Appel hello API Web
Il est maintenant temps tooactually utiliser access_token hello vous avez acquis à l’étape 3.  L’application hello ouvrir web `Controllers\TodoListController.cs` de fichiers, ce qui rend tous les hello CRUD demande toohello API de liste de tâches.

* Vous pouvez utiliser MSAL à nouveau ici access_tokens toofetch de hello du cache MSAL.  Tout d’abord, ajoutez un `using` instruction pour MSAL toothis fichier.
  
    `using Microsoft.Identity.Client;`
* Bonjour `Index` , MSAL d’utiliser l’action `AcquireTokenSilentAsync` méthode tooget un access_token qui peuvent être utilisés tooread des données à partir de hello service de liste de tâches :

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* Hello exemple puis ajoute demande hello obtenue toohello jeton HTTP GET comme hello `Authorization` en-tête, le service de liste de tâches hello utilise la demande de hello tooauthenticate.
* Si hello service de liste de tâches renvoie un `401 Unauthorized` réponse, access_tokens hello dans MSAL sont devenues non valides pour une raison quelconque.  Dans ce cas, vous devez supprimer n’importe quel access_tokens de hello du cache MSAL et afficher les utilisateur hello un message qu’ils peuvent avoir besoin toosign dans là encore, ce qui va redémarrer le flux d’acquisition de jeton hello.

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* De même, si MSAL est impossible de tooreturn un access_token pour une raison quelconque, vous devez demander à nouveau toosign d’utilisateur hello dans.  Cette opération n’est pas plus compliquée que la récupération d’un élément `MSALException` :

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* Hello exacte même `AcquireTokenSilentAsync` appel est implementd Bonjour `Create` et `Delete` actions.  Dans les applications web, vous pouvez utiliser cette access_tokens de tooget MSAL méthode chaque fois que vous avez besoin dans votre application.  MSAL se charge de l’acquisition, de la mise en cache et de l’actualisation des jetons.

Enfin, générez et exécutez votre application.  Connectez-vous avec un Account Microsoft ou un compte Azure et notez comment l’identité d’utilisateur hello est reflétée dans la barre de navigation supérieure hello.  Ajouter et supprimer des éléments à partir de la liste des tâches de l’utilisateur hello hello toosee Qu'oauth 2.0 sécurisés API appelle en action.  Vous disposez désormais d’une application Web et d’une API Web, toutes deux sécurisées à l’aide de protocoles standard et pouvant authentifier les utilisateurs avec leurs comptes personnels et professionnels/scolaires.

Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fourni ici](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des ressources supplémentaires, consultez :

* [guide du développeur v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Balise StackOverflow "azure-active-directory" &gt;&gt;](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obtenir les mises à jour de sécurité de nos produits
Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.

