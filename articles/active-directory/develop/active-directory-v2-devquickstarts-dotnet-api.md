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
# <a name="secure-an-mvc-web-api"></a>Sécurisation d’une API Web MVC
Avec le point de terminaison Azure Active Directory hello v2.0, vous pouvez protéger un à l’aide de l’API Web [OAuth 2.0](active-directory-v2-protocols.md) jetons d’accès, l’activation des utilisateurs avec les deux compte Microsoft personnel et les comptes professionnels ou scolaires toosecurely accéder à votre API Web.

> [!NOTE]
> Pas tous les scénarios Azure Active Directory et les fonctionnalités sont prises en charge par le point de terminaison hello v2.0.  toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
>
>

Dans les API web ASP.NET, vous pouvez y parvenir en utilisant l’intergiciel OWIN de Microsoft inclus dans .NET Framework 4.5.  Ici, nous allons utiliser OWIN toobuild une API Web MVC « tooDo liste » qui permet aux clients des tâches toocreate et en lecture à partir de la liste des actions d’un utilisateur.  API web de Hello validera que les demandes entrantes contiennent un jeton d’accès valide et rejettent les demandes qui ne passent pas de validation sur un itinéraire protégé.  Cet exemple a été créé à l’aide de Visual Studio 2015.

## <a name="download"></a>Télécharger
code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou un clone hello squelette :

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

application squelette Hello inclut tout le code réutilisable hello pour une API simple, mais il manque l’intégralité des hello liées à l’identité. Si vous ne souhaitez pas toofollow le long, vous pouvez à la place cloner ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>Inscription d’une application
Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).  Veillez à respecter les points suivants :

* Copie vers le bas hello **Id d’Application** affecté tooyour application, vous en aurez besoin plus rapidement.

Cette solution Visual Studio contient également une valeur « TodoListClient », qui est une application simple WPF.  Hello TodoListClient est utilisé toodemonstrate comment un utilisateur se connecte en et comment un client peut émettre des demandes tooyour API Web.  Dans ce cas, hello TodoListClient et hello TodoListService sont représentées par hello même application.  tooconfigure hello TodoListClient, vous devez également :

* Ajouter hello **Mobile** plate-forme pour votre application.

## <a name="install-owin"></a>Installer OWIN
Maintenant que vous avez inscrit une application, vous avez besoin tooset toocommunicate de votre application avec le point de terminaison hello v2.0 dans un ordre toovalidate les demandes entrantes et les jetons.

* toobegin, ouvrez la solution de hello et ajoutez hello OWIN intergiciel (middleware) NuGet packages toohello TodoListService projet à l’aide de la Console du Gestionnaire de Package de hello.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>Configurer l’authentification OAuth
* Ajouter un projet de démarrage OWIN la TodoListService de toohello de la classe appelé `Startup.cs`.  Un clic droit sur le projet de hello--> **ajouter** --> **un nouvel élément** --> Recherchez « OWIN ».  intergiciel (middleware) OWIN de Hello appellera hello `Configuration(…)` méthode au démarrage de votre application.
* Modifier trop de déclaration de classe hello`public partial class Startup` -nous avons déjà implémenté le cadre de cette classe pour vous dans un autre fichier.  Bonjour `Configuration(…)` (méthode), effectuer un tooset de tooConfgureAuth(...) d’appel de l’authentification pour votre application web.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* Les fichiers ouverts hello `App_Start\Startup.Auth.cs` et implémenter hello `ConfigureAuth(…)` (méthode), qui définit les jetons de tooaccept hello API Web à partir du point de terminaison hello v2.0.

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

* Vous pouvez désormais utiliser `[Authorize]` attributs tooprotect vos contrôleurs et vos actions avec l’authentification du support OAuth 2.0.  Décorer hello `Controllers\TodoListController.cs` classe avec une balise authorize.  Cela obligera toosign d’utilisateur hello dans avant d’accéder à cette page.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Quand un appelant autorisé correctement appelle l’une des hello `TodoListController` API, action de hello peut-être besoin d’accès tooinformation sur l’appelant de hello.  OWIN fournit des revendications toohello d’accès à l’intérieur du jeton de support hello via hello `ClaimsPrincpal` objet.  

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

* Enfin, ouvrez hello `web.config` fichier racine hello du projet TodoListService de hello et entrez les valeurs de configuration Bonjour `<appSettings>` section.
  * Votre `ida:Audience` est hello **Id d’Application** de l’application hello que vous avez entré dans le portail de hello.

## <a name="configure-hello-client-app"></a>Configurer l’application cliente de hello
Avant de pouvoir afficher hello Service de liste de tâches en action, vous devez tooconfigure hello Client de liste de tâches afin de pouvoir obtenir des jetons à partir du point de terminaison v2.0 hello et effectuer des appels toohello service.

* Dans le projet de TodoListClient hello, ouvrez `App.config` et entrez les valeurs de configuration Bonjour `<appSettings>` section.
  * Votre `ida:ClientId` vous avez copié à partir du portail de hello Id d’Application.

Enfin, nettoyez, générez et exécutez chaque projet.  Vous disposez maintenant d’une API web MVC .NET qui accepte les jetons des comptes Microsoft personnels et des comptes professionnels ou scolaires.  Connectez-vous à hello TodoListClient et appelez la liste de tâches web api tooadd tâches toohello de vos utilisateurs.

Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie en tant qu’un fichier zip ici](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), ou vous pouvez le cloner à partir de GitHub :

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez à présent passer à d’autres rubriques.  Vous souhaiterez peut-être tootry :

[Appeler une API web à partir d’une application web &gt;&gt;](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Pour obtenir des ressources supplémentaires, consultez :

* [guide du développeur v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Balise StackOverflow "azure-active-directory" &gt;&gt;](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obtenir les mises à jour de sécurité de nos produits
Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.
