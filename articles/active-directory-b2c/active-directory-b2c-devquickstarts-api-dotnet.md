---
title: aaaAzure AD B2C | Documents Microsoft
description: "Comment toobuild une API Web de .NET à l’aide de B2C d’Active Directory Azure, sécurisés à l’aide des jetons d’accès OAuth 2.0 pour l’authentification."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C : générer une API web .NET

Avec Azure Active Directory (Azure AD) B2C, vous pouvez sécuriser une API web à l’aide de jetons d’accès OAuth 2.0, Ces jetons permettent à votre client applications tooauthenticate toohello API. Cet article explique comment toocreate une API de la « liste de tâches » MVC .NET qui permet aux utilisateurs de votre client de tâches tooCRUD de l’application. Hello web API est sécurisé à l’aide d’Azure AD B2C et autorise uniquement les utilisateurs authentifiés toomanage leur liste de tâches.

## <a name="create-an-azure-ad-b2c-directory"></a>Créer un répertoire Azure AD B2C

Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client. Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc. Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant d’aller plus loin dans ce guide.

> [!NOTE]
> application cliente de Hello et API web doivent utiliser Active de B2C hello même instance Azure AD.
>

## <a name="create-a-web-api"></a>Créer une API Web

Ensuite, vous devez toocreate une application d’API web dans votre répertoire B2C. Cela fournit des informations AD Azure qu’il a besoin toosecurely communiquer avec votre application. toocreate une application, procédez comme [ces instructions](active-directory-b2c-app-registration.md). Veillez à effectuer les opérations suivantes :

* Inclure un **application web** ou **web API** dans l’application hello.
* Hello d’utilisation **URI de redirection** `https://localhost:44332/` pour l’application web de hello. Il s’agit d’emplacement par défaut de hello du client de l’application web hello pour cet exemple de code.
* Hello de copie **ID d’Application** qui est attribué tooyour application. Vous en aurez besoin ultérieurement.
* Entrez un identificateur d’application dans **l’URI d’ID d’application**.
* Ajouter des autorisations via hello **publié étendues** menu.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Création de vos stratégies

Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md). Vous devez toocreate un toocommunicate de stratégie avec Azure Active Directory B2C. Nous recommandons à l’aide de hello combinées de stratégie de connexion-haut/connectez-vous, comme décrit dans hello [article de référence de stratégie](active-directory-b2c-reference-policies.md). Lorsque vous créez la stratégie, prenez soin de :

* Choisir un **Nom d’affichage** et d’autres attributs d’inscription dans votre stratégie.
* Choisir les revendications **Nom d’affichage** et **ID d’objet** comme revendications d’application pour chaque stratégie. Vous pouvez aussi choisir d'autres revendications.
* Hello de copie **nom** de chaque stratégie après l’avoir créée. Vous aurez besoin nom de la stratégie hello plus tard.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Une fois que vous avez créé la stratégie de hello, vous êtes prêt toobuild votre application.

## <a name="download-hello-code"></a>Télécharger le code de hello

code Hello pour ce didacticiel est conservée sur [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Vous pouvez cloner l’exemple hello en exécutant :

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Après avoir téléchargé l’exemple de code hello, ouvrez hello tooget du fichier .sln de Visual Studio a démarré. fichier de solution Hello contient deux projets : `TaskWebApp` et `TaskService`. `TaskWebApp`est une application web MVC hello utilisateur interagit avec. `TaskService`est web principal API de l’application hello qui stocke la liste des actions de chaque utilisateur. Cet article traite uniquement hello `TaskService` application. toolearn comment toobuild `TaskWebApp` à l’aide d’Azure AD B2C, consultez [notre didacticiel d’application web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Mettre à jour la configuration de hello Azure AD B2C

Notre exemple est configuré toouse hello stratégies et ID de client de notre client de démonstration. Si vous souhaitez que toouse votre propre client, vous devez hello toodo suivant :

1. Ouvrez `web.config` Bonjour `TaskService` de projet et remplacer les valeurs hello pour
    * `ida:Tenant` par le nom de votre locataire
    * `ida:ClientId` avec votre ID d’application d’API web
    * `ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion

2. Ouvrez `web.config` Bonjour `TaskWebApp` de projet et remplacer les valeurs hello pour
    * `ida:Tenant` par le nom de votre locataire
    * `ida:ClientId` par votre ID d’application web
    * `ida:ClientSecret` par votre clé secrète d’application web
    * `ida:SignUpSignInPolicyId` par votre nom de stratégie d’inscription ou de connexion
    * `ida:EditProfilePolicyId` par votre nom de stratégie « Modifier le profil »
    * `ida:ResetPasswordPolicyId` par votre nom de stratégie « Réinitialiser le mot de passe »


## <a name="secure-hello-api"></a>Sécuriser les API hello

Lorsque l’un de vos clients appelle votre API, vous pouvez la sécuriser (par exemple, `TaskService`) à l’aide de jetons du porteur OAuth 2.0. Cela garantit que chaque API de tooyour demande sera uniquement valide si la demande de hello possède un jeton de support. Votre API peut accepter et valider les jetons du porteur à l’aide de la bibliothèque OWIN (Open Web Interface for .NET) de Microsoft.

### <a name="install-owin"></a>Installer OWIN

Commencez par installer un pipeline de l’authentification OWIN OAuth hello à l’aide de hello Console du Gestionnaire de Package Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Ceci installe hello OWIN intergiciel (middleware) qui accepte et valide les jetons de support.

### <a name="add-an-owin-startup-class"></a>Ajouter une classe de démarrage OWIN

Ajouter un toohello de classe de démarrage OWIN API appelée `Startup.cs`.  Avec le bouton droit sur le projet hello, sélectionnez **ajouter** et **un nouvel élément**, puis recherchez OWIN. intergiciel (middleware) OWIN de Hello appellera hello `Configuration(…)` méthode au démarrage de votre application.

Dans notre exemple, nous avons modifié trop déclaration de classe hello`public partial class Startup` et implémenté hello autre partie de la classe hello dans `App_Start\Startup.Auth.cs`. À l’intérieur hello `Configuration` (méthode), nous avons ajouté un appel trop`ConfigureAuth`, qui est défini dans `Startup.Auth.cs`. Après modification de hello, `Startup.cs` ressemble à hello qui suit :

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a>Configurer l’authentification OAuth 2.0

Les fichiers ouverts hello `App_Start\Startup.Auth.cs`et mettre en œuvre hello `ConfigureAuth(...)` (méthode). Par exemple, il peut se présenter comme hello ci-après :

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>Contrôleur de tâche hello sécurisé

Une fois l’application hello l’authentification configurée toouse OAuth 2.0, vous pouvez sécuriser votre API web en ajoutant un `[Authorize]` contrôleur de tâche toohello de balise. Il s’agit de contrôleur hello où toutes les manipulations de liste de tâches a lieu, donc vous devez sécuriser le contrôleur d’entier hello au niveau de la classe hello. Vous pouvez également ajouter hello `[Authorize]` tooindividual des actions pour un contrôle plus précis de la balise.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Obtenir des informations sur l’utilisateur à partir de hello jeton

`TasksController`stocke les tâches dans une base de données où chaque tâche a un utilisateur associé qui « possède » la tâche hello. propriétaire de Hello est identifié par l’utilisateur hello **ID d’objet**. (C’est pourquoi vous avez besoin d’ID d’objet tooadd hello en tant qu’application par toutes les stratégies de votre demande.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Valider les autorisations hello dans le jeton de hello

Une exigence courante pour l’API web est toovalidate hello « étendues » présents dans le jeton de hello. Cela garantit que l’utilisateur hello a consenti service de liste de tâches toohello autorisations requis tooaccess hello.

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>Exécutez l’exemple d’application hello

Pour finir, générez et exécutez `TaskWebApp` et `TaskService`. Créer des tâches sur la liste des tâches de l’utilisateur hello et notez comment elles sont conservées dans hello API même après l’arrêt et redémarrez hello client.

## <a name="edit-your-policies"></a>Modifier vos stratégies

Une fois que vous avez sécurisé une API à l’aide d’Azure AD B2C, vous pouvez tester votre stratégie de connexion-dans/connexion-haut et afficher les effets hello (ou son manque) sur hello API. Vous pouvez manipuler les revendications d’application hello dans les stratégies de hello et modifier les informations utilisateur hello qui est disponibles dans l’API web de hello. Toutes les revendications que vous ajoutez sera disponible tooyour .NET MVC web API Bonjour `ClaimsPrincipal` de l’objet, comme décrit précédemment dans cet article.
