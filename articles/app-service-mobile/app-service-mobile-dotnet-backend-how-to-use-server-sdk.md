---
title: toowork aaaHow avec serveur principal de .NET hello SDK pour applications mobiles | Documents Microsoft
description: "Découvrez comment toowork avec hello serveur principal de .NET SDK pour applications de Azure App Service Mobile."
keywords: "app service, azure app service, application mobile, service mobile, mise à l’échelle, évolutif, déploiement d’application, déploiement d’application azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Travailler avec serveur principal de .NET hello Kit de développement logiciel pour les applications mobiles Azure
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Cette rubrique vous montre comment toouse hello .NET back-end server SDK dans les scénarios de clés Azure App Service Mobile Apps. Bonjour Azure Mobile Apps SDK vous permet de travailler avec des clients mobiles à partir de votre application ASP.NET.

> [!TIP]
> Hello [.NET server SDK pour les applications mobiles Azure] [ 2] est open source sur GitHub. référentiel de Hello contient tout le code source, y compris la suite de tests unitaires hello ensemble du serveur SDK et des exemples de projets.
>
>

## <a name="reference-documentation"></a>Documentation de référence
documentation de référence Hello pour le serveur hello SDK se trouve ici : [référence .NET de Azure Mobile Apps][1].

## <a name="create-app"></a>Comment : créer un serveur principal d’une application Mobile .NET
Si vous démarrez un nouveau projet, vous pouvez créer une application de Service d’applications à l’aide soit hello [portail Azure] ou Visual Studio. Vous pouvez exécuter hello application de Service de l’application localement ou publier le projet tooyour en nuage du Service d’applications mobile application hello.

Si vous ajoutez un projet existant tooan fonctionnalités mobiles, consultez hello [télécharger et initialiser hello SDK](#install-sdk) section.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Créer un service principal de .NET à l’aide de hello portail Azure
toocreate un serveur principal de Service d’applications mobile, soit suivre hello [didacticiel de démarrage rapide] [ 3] ou procédez comme suit :

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Dans hello *prise en main* panneau, sous **créer une table API**, choisissez **c#** en tant que votre **principal langage**. Cliquez sur **télécharger**, extraire l’ordinateur local de tooyour de fichiers de projet compressée et ouvrez la solution de hello dans Visual Studio.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Créer un backend .NET à l’aide de Visual Studio 2013 et de Visual Studio 2015
Installer hello [Azure SDK pour .NET] [ 4] (version 2.9.0 ou version ultérieure) toocreate un projet Azure Mobile Apps dans Visual Studio. Une fois que vous avez installé hello SDK, créez une application ASP.NET à l’aide de hello comme suit :

1. Ouvrez hello **nouveau projet** boîte de dialogue (à partir de *fichier* > **nouveau** > **projet...** ).
2. Développez **Modèles** > **Visual C#**, puis sélectionnez **Web**.
3. Sélectionnez **Application web ASP.NET**.
4. Renseignez le nom du projet hello. Cliquez ensuite sur **OK**.
5. Sous *Modèles ASP.NET 4.5.2*, sélectionnez **Application mobile Azure**. Vérifiez **hôte hello cloud** toocreate un backend mobile Bonjour cloud toowhich, vous pouvez publier ce projet.
6. Cliquez sur **OK**.

## <a name="install-sdk"></a>Comment : télécharger et initialiser hello SDK
Hello SDK est disponible sur [NuGet.org]. Ce package comprend tooget de fonctionnalités de base requises hello démarré à l’aide du Kit de développement logiciel de hello. tooinitialize hello SDK, vous devez les actions tooperform sur hello **HttpConfiguration** objet.

### <a name="install-hello-sdk"></a>Installer hello SDK
tooinstall hello SDK, avec le bouton droit sur le projet de serveur hello dans Visual Studio, sélectionnez **gérer les Packages NuGet**, recherchez hello [Microsoft.Azure.Mobile.Server] du package, puis cliquez sur  **Installer**.

### <a name="server-project-setup"></a>Initialiser le projet de serveur hello
Un projet de serveur principal .NET est initialisé similaire tooother les projets ASP.NET, en incluant une classe de démarrage OWIN. Assurez-vous que vous avez référencé package NuGet de hello `Microsoft.Owin.Host.SystemWeb`. tooadd cette classe dans Visual Studio, avec le bouton droit sur votre projet de serveur, puis sélectionnez **ajouter** >
**un nouvel élément**, puis **Web**  >  ** Général** > **classe de démarrage OWIN**.  Une classe est générée avec hello suivant attribut :

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

Bonjour `Configuration()` méthode de votre classe de démarrage OWIN, utilisez un **HttpConfiguration** environnement d’applications mobiles Azure objet tooconfigure hello.
Hello, l’exemple suivant initialise le projet de serveur hello sans fonctionnalités non ajoutés :

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable des fonctionnalités individuelles, vous devez appeler les méthodes d’extension sur hello **MobileAppConfiguration** objet avant d’appeler **ApplyTo**. Par exemple, hello suivant code ajoute par défaut de hello achemine les contrôleurs tooall API qui ont l’attribut de hello `[MobileAppController]` lors de l’initialisation :

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

démarrage rapide de serveur Hello de hello appels portails Azure **UseDefaultConfiguration()**. Cette toohello équivalente après l’installation :

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

méthodes d’extension Hello utilisées sont :

* `AddMobileAppHomeController()`Fournit la page d’accueil Azure Mobile Apps hello par défaut.
* `MapApiControllers()`Fournit des fonctions personnalisées de l’API pour les contrôleurs WebAPI décorées avec hello `[MobileAppController]` attribut.
* `AddTables()`fournit un mappage de hello `/tables` contrôleurs tootable de points de terminaison.
* `AddTablesWithEntityFramework()`est un abrégé pour hello de mappage `/tables` contrôleurs basés sur des points de terminaison à l’aide d’Entity Framework.
* `AddPushNotifications()` fournit une méthode simple pour l’inscription d’appareils au service Notification Hubs.
* `MapLegacyCrossDomainController()` fournit des en-têtes CORS standard pour le développement local.

### <a name="sdk-extensions"></a>Extensions de Kit de développement logiciel (SDK)
Hello suivant les packages NuGet d’extension fourniture diverses fonctionnalités mobiles qui peuvent être utilisées par votre application. Vous activez les extensions lors de l’initialisation à l’aide de hello **MobileAppConfiguration** objet.

* [Microsoft.Azure.Mobile.Server.Quickstart] prend en charge hello le programme d’installation de base applications mobiles. Configuration toohello ajouté par l’appelant hello **UseDefaultConfiguration** méthode d’extension lors de l’initialisation. Cette extension comprend les extensions suivantes : packages Notifications, Authentication, Entity, Tables, Cross-domain et Home. Ce package est utilisé par hello démarrage rapide pour des applications mobiles disponible sur hello portail Azure.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implémente par défaut de hello *cette application mobile est en cours d’exécution page* pour la racine du site web hello. Ajouter la configuration de toohello en appelant le **AddMobileAppHomeController** méthode d’extension.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) comprend des classes pour l’utilisation des données et configuration du pipeline de données hello. Ajouter des toohello configuration en appelant hello **AddTables** méthode d’extension.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Active hello Entity Framework tooaccess données Bonjour de la base de données SQL. Ajouter des toohello configuration en appelant hello **AddTablesWithEntityFramework** méthode d’extension.
* [Microsoft.Azure.Mobile.Server.Authentication] permet l’authentification et configuration hello OWIN intergiciel (middleware) utilisé toovalidate jetons. Ajouter des toohello configuration en appelant hello **AddAppServiceAuthentication** et **IAppBuilder**. **UseAppServiceAuthentication** les méthodes d’extension.
* [Microsoft.Azure.Mobile.Server.Notifications] active les notifications Push et définit un point de terminaison d’inscription Push. Ajouter des toohello configuration en appelant hello **AddPushNotifications** méthode d’extension.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) crée un contrôleur qui fait Office de données toolegacy navigateurs web à partir de votre application Mobile. Ajouter la configuration de toohello en appelant le **MapLegacyCrossDomainController** méthode d’extension.
* [Microsoft.Azure.Mobile.Server.Login] fournit une méthode AppServiceLoginHandler.CreateToken() hello, qui est une méthode statique utilisée durant les scénarios d’authentification personnalisée.

## <a name="publish-server-project"></a>Comment : publier le projet de serveur hello
Cette section vous montre comment toopublish votre serveur principal .NET project à partir de Visual Studio. Vous pouvez également déployer votre projet de service principal à l’aide de Git ou des hello autres méthodes présentées dans hello [documentation sur le déploiement du Service d’applications Azure](../app-service-web/web-sites-deploy.md).

1. Dans Visual Studio, régénérez les packages NuGet de hello projet toorestore.
2. Dans l’Explorateur de solutions, projets de hello avec le bouton droit, cliquez sur **publier**. Hello première fois que vous publiez, vous devez toodefine un profil de publication. Si vous disposez déjà d’un profil, vous pouvez le sélectionner et cliquer sur **Publier**.
3. Si vous êtes invité tooselect une cible de publication, cliquez sur **Microsoft Azure App Service** > **suivant**, puis (si nécessaire) connectez-vous avec vos informations d’identification Azure.
   Visual Studio récupère vos paramètres de publication depuis Azure et les stocke en sécurité.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. Choisissez votre **Abonnement**, sélectionnez **Type de ressource** dans **Affichage**, développez **Application mobile** et cliquez sur votre backend Mobile App, puis cliquez sur **OK**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Vérifiez que hello publier des informations de profil et cliquez sur **publier**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    Une fois le backend Mobile App publié, une page vous indique que l’opération a réussi.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a> Définir un contrôleur de table
Définir un tooexpose de contrôleur de la Table des clients de toomobile une table SQL.  La configuration d’un contrôleur de table requiert trois étapes :

1. Créer une classe d’objet de transfert de données (DTO).
2. Configurez une référence de table Bonjour classe Mobile DbContext.
3. Créer un contrôleur de table.

Un objet de transfert de données (DTO) est un objet C# simple qui hérite de `EntityData`.  Par exemple :

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

Hello DTO est la table de hello toodefine utilisés au sein de la base de données SQL hello.  toocreate hello de base de données d’entrée, ajoutez un `DbSet<>` propriété Hello DbContext que vous utilisez.  Dans le modèle de projet hello par défaut pour les applications mobiles Azure, hello DbContext est appelée `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Si vous avez hello Qu'azure SDK est installé, vous pouvez maintenant créer un contrôleur de table de modèle comme suit :

1. Avec le bouton droit sur le dossier de contrôleurs hello et sélectionnez **ajouter** > **contrôleur...** .
2. Sélectionnez hello **contrôleur de Table Azure Mobile Apps** option, puis cliquez sur **ajouter**.
3. Bonjour **ajouter un contrôleur** boîte de dialogue :
   * Bonjour **classe de modèle** liste déroulante, sélectionnez votre nouvelle DTO.
   * Bonjour **DbContext** liste déroulante, la classe DbContext du Service Mobile de hello select.
   * nom du contrôleur Hello est créé pour vous.
4. Cliquez sur **Add**.

projet de serveur Hello quickstart contient un exemple d’un simple **TodoItemController**.

### <a name="adjust-pagesize"></a>Comment : redimensionner la pagination hello table
Par défaut, Azure Mobile Apps retourne 50 enregistrements par demande.  La pagination garantit que le client hello n’occupe pas leur serveur de l’interface utilisateur thread ni hello trop longtemps, garantissant une expérience utilisateur optimale. taille de la pagination du tableau toochange hello, augmentation hello SSI « taille de la requête autorisé » et hello SSI de page côté client de hello de taille « taille de la requête d’autorisé » est ajustée à l’aide de hello `EnableQuery` attribut :

    [EnableQuery(PageSize = 500)]

Vérifiez que hello PageSize est hello égale ou supérieure à la taille de hello demandée par le client de hello.  Pour plus d’informations sur la modification de taille de page hello client, consultez la documentation de faire du client spécifique toohello.

## <a name="how-to-define-a-custom-api-controller"></a>Définir un contrôleur d’API personnalisé
contrôleur d’API personnalisée Hello fournit le principal de l’application Mobile hello plus simple fonctionnalité tooyour en exposant un point de terminaison. Vous pouvez enregistrer un contrôleur d’API mobile spécifique à l’aide des attributs de hello [MobileAppController]. Hello `MobileAppController` attribut enregistre hello itinéraire, configure le sérialiseur JSON des applications mobiles de hello et Active [la vérification de la version client](app-service-mobile-client-and-server-versioning.md).

1. Dans Visual Studio, le dossier de contrôleurs hello avec le bouton droit, puis cliquez sur **ajouter** > **contrôleur**, sélectionnez **Web API 2 contrôleur&mdash;vide** et Cliquez sur **ajouter**.
2. Spécifiez un **nom de contrôleur**, tel que `CustomController`, puis cliquez sur **Ajouter**.
3. Dans le nouveau fichier de classe de contrôleur hello, ajoutez hello qui suit à l’aide d’instruction :

        using Microsoft.Azure.Mobile.Server.Config;
4. Appliquer hello **[MobileAppController]** attribut de définition de classe de contrôleur toohello API, comme dans hello l’exemple suivant :

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. Dans le fichier de App_Start/Startup.MobileApp.cs, ajouter un appel toohello **MapApiControllers** méthode d’extension, comme dans hello l’exemple suivant :

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

Vous pouvez également utiliser hello `UseDefaultConfiguration()` méthode d’extension à la place de `MapApiControllers()`. Tous les contrôleurs auxquels **MobileAppControllerAttribute** n’est pas appliqué restent accessibles aux clients, mais ils peuvent ne pas être utilisés correctement par les clients à l’aide d’un Kit de développement logiciel (SDK) client d’application mobile.

## <a name="how-to-work-with-authentication"></a>Utiliser l’authentification
Les applications mobiles Azure utilise l’authentification du Service application / d’autorisation toosecure votre serveur principal mobile.  Cette section vous montre comment hello tooperform liés à l’authentification des tâches dans votre projet de serveur principal .NET suivantes :

* [Comment : ajouter un projet de serveur d’authentification tooa](#add-auth)
* [Utiliser l’authentification personnalisée pour votre application](#custom-auth)
* [Récupérer des informations utilisateur authentifiées](#user-info)
* [Limiter l’accès aux données pour les utilisateurs autorisés](#authorize)

### <a name="add-auth"></a>Comment : ajouter un projet de serveur d’authentification tooa
Vous pouvez ajouter le projet de serveur d’authentification tooyour en étendant hello **MobileAppConfiguration** objet et la configuration d’intergiciel (middleware) OWIN. Lorsque vous installez hello [Microsoft.Azure.Mobile.Server.Quickstart] hello package et appelez **UseDefaultConfiguration** méthode d’extension, vous pouvez ignorer toostep 3.

1. Dans Visual Studio, installez hello [Microsoft.Azure.Mobile.Server.Authentication] package.
2. Dans le fichier de projet Startup.cs hello, ajouter hello suivant la ligne de code au début de hello Hello **Configuration** méthode :

        app.UseAppServiceAuthentication(config);

    Ce composant d’intergiciel (middleware) OWIN valide les jetons émis par la passerelle de Service de l’application hello associé.
3. Ajouter hello `[Authorize]` contrôleur de tooany d’attribut ou une méthode qui requiert une authentification.

toolearn comment tooauthenticate clients tooyour principal des applications mobiles, consultez [ajouter l’authentification tooyour application](app-service-mobile-ios-get-started-users.md).

### <a name="custom-auth"></a>Utiliser l’authentification personnalisée pour votre application
Si vous ne souhaitez pas toouse un des fournisseurs d’authentification/autorisation du Service application hello, vous pouvez implémenter votre propre système de connexion. Installer hello [Microsoft.Azure.Mobile.Server.Login] tooassist de génération de jetons d’authentification du package.  Fournissez votre propre code pour valider les informations d’identification utilisateur. Par exemple, vous pouvez définir des mots de passe salés et hachés dans une base de données. Dans l’exemple hello ci-dessous, hello `isValidAssertion()` (méthode) (définie ailleurs) est chargé de ces vérifications.

authentification personnalisée de Hello est exposée par un ApiController de créer et d’exposer `register` et `login` actions. client de Hello doit utiliser une interface utilisateur toocollect hello des informations personnalisées à partir de l’utilisateur de hello.  informations de Hello sont soumis toohello API avec un HTTP POST standard l’appeler. Une fois que le serveur de hello valide l’assertion de hello, un jeton est émis à l’aide de hello `AppServiceLoginHandler.CreateToken()` (méthode).  Hello ApiController **ne doivent pas** utiliser hello `[MobileAppController]` attribut.

Un exemple d’action `login` :

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

Bonjour précédent exemple, LoginResult et LoginResultUser sont des objets sérialisables qui exposent des propriétés requises. client de Hello attend toobe de réponses de connexion en tant qu’objets JSON sous forme de hello :

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

Hello `AppServiceLoginHandler.CreateToken()` méthode inclut un *public* et un *émetteur* paramètre. Ces deux paramètres sont définies toohello des URL de la racine de votre application, à l’aide du schéma HTTPS de hello. De même, vous devez définir *secretKey* clé de signature de la valeur de hello toobe de votre application. Ne distribuez pas hello signer la clé dans un client peut être utilisé toomint clés et emprunter l’identité des utilisateurs. Vous pouvez obtenir hello tandis que hébergée dans le Service d’applications en référençant hello de clé de signature *site Web\_AUTH\_signature\_clé* variable d’environnement. Si nécessaire dans un contexte de débogage local, suivez les instructions de hello Bonjour [débogage Local avec l’authentification](#local-debug) section clé de hello tooretrieve et stocker en tant que paramètre d’application.

jeton de Hello émis peut-être également inclure les autres revendications et une date d’expiration.  Au minimum, jeton de hello émis doit inclure un sujet (**sub**) de revendication.

Vous pouvez prendre en charge client standard de hello `loginAsync()` méthode en surchargeant l’itinéraire d’authentification hello.  Si hello client appelle `client.loginAsync('custom');` toolog dans, l’itinéraire doit être `/.auth/login/custom`.  Vous pouvez définir des itinéraires hello pour hello de contrôleur d’authentification personnalisée à l’aide `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> À l’aide de hello `loginAsync()` approche garantit que ce jeton d’authentification hello est attaché tooevery appeler toohello service.
>
>

### <a name="user-info"></a>Récupérer des informations utilisateur authentifiées
Lorsqu’un utilisateur est authentifié par le Service d’applications, vous pouvez accéder à hello affecté des ID d’utilisateur et d’autres informations dans votre code de serveur principal .NET. informations d’utilisateur de Hello peuvent être utilisées pour prendre des décisions d’autorisation dans le service principal hello. Hello de code suivant obtient hello ID d’utilisateur associé à une demande :

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

Hello SID est dérivé de l’ID d’utilisateur spécifique au fournisseur hello et est statique pour un utilisateur donné et le fournisseur de connexion.  Hello SID est null pour les jetons d’authentification non valide.

App Service vous permet également de demander des revendications spécifiques à votre fournisseur de connexion. Chaque fournisseur d’identité peut fournir des informations supplémentaires à l’aide du Kit de développement logiciel (SDK) du fournisseur d’identité.  Par exemple, vous pouvez utiliser hello API Graph Facebook pour les informations de vos amis.  Vous pouvez spécifier les revendications qui sont demandées dans le panneau de fournisseur hello Bonjour portail Azure. Certaines demandes nécessitent une configuration supplémentaire avec un fournisseur d’identité hello.

hello d’appels de code suivant de Hello **GetAppServiceIdentityAsync** extension méthode tooget hello informations d’identification, notamment les demandes de jeton toomake nécessaires d’accès hello contre hello API Graph Facebook :

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

Ajouter un à l’aide de l’instruction pour `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** méthode d’extension.

### <a name="authorize"></a>Limiter l’accès aux données pour les utilisateurs autorisés
Dans la section précédente de hello, nous vous avons montré comment tooretrieve hello ID d’utilisateur d’un utilisateur authentifié. Vous pouvez restreindre l’accès toodata et autres ressources en fonction de cette valeur. Par exemple, ajout d’un tootables de la colonne ID d’utilisateur et le filtrage des résultats de la requête par ID d’utilisateur hello hello sont un toolimit de façon simple retourné utilisateurs tooauthorized uniquement des données. Hello de code suivant retourne les lignes de données uniquement lorsque hello SID correspond à la valeur de colonne de UserId hello sur la table TodoItem de hello :

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

Hello `Query()` méthode retourne un `IQueryable` qui peuvent être manipulées par filtrage de toohandle LINQ.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>Comment : ajouter un projet de serveur de tooa de notifications push
Ajouter un projet de serveur push notifications tooyour en étendant hello **MobileAppConfiguration** objet et la création d’un client de concentrateurs de Notification.

1. Dans Visual Studio, cliquez sur le projet de serveur hello et cliquez sur **gérer les Packages NuGet**, recherchez `Microsoft.Azure.Mobile.Server.Notifications`, puis cliquez sur **installer**.
2. Répétez cette hello de tooinstall étape `Microsoft.Azure.NotificationHubs` package, qui inclut la bibliothèque cliente de concentrateurs de Notification hello.
3. Dans App_Start/Startup.MobileApp.cs et ajoutez un appel toohello **AddPushNotifications()** méthode d’extension lors de l’initialisation :

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. Ajoutez hello suivant le code qui crée un client de concentrateurs de Notification :

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

Vous pouvez maintenant utiliser hello concentrateurs de Notification toosend push notifications tooregistered les périphériques clients. Pour plus d’informations, consultez [ajouter push notifications tooyour application](app-service-mobile-ios-get-started-push.md). toolearn en savoir plus sur les concentrateurs de Notification, consultez [vue d’ensemble des concentrateurs de Notification](../notification-hubs/notification-hubs-push-notification-overview.md).

## <a name="tags"></a>Activer les notifications Push ciblées à l’aide de balises
Concentrateurs de notification vous permet d’envoyer des notifications ciblées toospecific inscriptions à l’aide de balises. Plusieurs balises sont créées automatiquement :

* Hello ID d’Installation identifie un périphérique spécifique.
* Hello Id d’utilisateur en fonction de hello authentifié SID identifie un utilisateur spécifique.

Hello installation ID est accessible à partir de hello **installationId** propriété hello **MobileServiceClient**.  Hello exemple suivant montre comment utiliser un tooadd de ID d’installation une installation spécifique de balise tooa dans des concentrateurs de Notification :

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

Toutes les balises fournies par le client de hello lors de l’enregistrement des notifications push sont ignorés par hello principal lors de la création d’une installation de hello. tooenable un tooadd client balises toohello installation, vous devez créer une API personnalisée qui ajoute des balises à l’aide de hello précédant le modèle.

Consultez [balises de notification push de Client ajouté] [ 5] dans l’exemple de démarrage rapide terminée hello App Service Mobile Apps pour obtenir un exemple.

## <a name="push-user"></a>Comment : envoyer push notifications tooan de l’utilisateur authentifié
Lorsqu’un utilisateur authentifié s’inscrit pour les notifications push, une balise d’ID utilisateur est automatiquement ajoutée l’enregistrement de toohello. À l’aide de cette balise, vous pouvez envoyer par émission de données des appareils tooall notifications inscrits par cette personne. Hello de code suivant obtient hello SID de l’utilisateur qui effectue la requête et envoie une inscription de périphérique modèle push notification tooevery pour cette personne :

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

Quand vous vous inscrivez à des notifications Push à partir d’un client authentifié, assurez-vous au préalable que l’authentification est bien terminée. Pour plus d’informations, consultez [Push toousers] [ 6] dans exemple de démarrage rapide terminée App Service Mobile Apps hello pour le service principal .NET.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>Comment : déboguer et résoudre les problèmes de hello .NET Server SDK
Azure App Service fournit plusieurs techniques de débogage et de résolution des problèmes pour les applications ASP.NET.

* [Surveiller les applications web dans Microsoft Azure App Service](../app-service-web/web-sites-monitor.md)
* [Activer la journalisation des diagnostics pour les applications web dans Azure App Service](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Dépanner un service Azure App dans Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>Journalisation
Vous pouvez écrire des journaux de diagnostic Service tooApp à l’aide d’écriture de trace ASP.NET standard hello. Avant de pouvoir écrire des journaux de toohello, vous devez activer les diagnostics de votre serveur principal de l’application Mobile.

tooenable diagnostics et écriture toohello des journaux :

1. Suivez les étapes de hello dans [comment tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).
2. Ajoutez hello qui suit à l’aide d’instruction dans votre fichier de code :

        using System.Web.Http.Tracing;
3. Créez un toowrite d’enregistreur de trace à partir de hello .NET principal toohello journaux de diagnostic, comme suit :

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. Publier à nouveau votre projet de serveur et accéder hello application Mobile back-end tooexecute hello code au chemin avec une journalisation hello.
5. Téléchargez et évaluez les journaux de hello, comme décrit dans [Comment : télécharger les journaux](../app-service-web/web-sites-enable-diagnostic-log.md#download).

### <a name="local-debug"></a>Débogage local avec authentification
Vous pouvez exécuter votre application localement tootest change avant leur publication toohello cloud. Pour la plupart des backends Azure Mobile Apps, appuyez sur *F5* lorsque vous êtes dans Visual Studio. Toutefois, certains points spécifiques sont à prendre en compte en lien avec l’authentification.

Vous devez disposer d’une application mobile sur le cloud avec application d’authentification/autorisation du Service configurée, et que votre client doit avoir hello cloud point de terminaison spécifié en tant qu’hôte de connexion de substitution hello. Consultez la documentation hello pour votre plateforme de client pour connaître la procédure hello requis.

Assurez-vous que [Microsoft.Azure.Mobile.Server.Authentication] est installé sur votre backend mobile. Puis, dans la classe de démarrage de votre application OWIN, ajoutez après suivantes de hello, `MobileAppConfiguration` a été appliqué tooyour `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

Bonjour précédent exemple, vous devez configurer hello *authAudience* et *authIssuer* paramètres d’application dans votre fichier Web.config du fichier tooeach l’URL de la racine de votre application, à l’aide de hello HTTPS schéma. De même, vous devez définir *authSigningKey* clé de signature de la valeur de hello toobe de votre application.
clé de signature hello tooobtain :

1. Accédez application tooyour dans hello [portail Azure]
2. Cliquez sur **Outils**, **Kudu**, **Accéder**.
3. Dans le site d’administration de Kudu hello, cliquez sur **environnement**.
4. Rechercher la valeur hello pour *site Web\_AUTH\_signature\_clé*.

Hello utilisez la signature de clé pour hello *authSigningKey* paramètre dans votre configuration de l’application locale.  Votre serveur principal mobile est maintenant toovalidate équipés jetons lors de l’exécution localement, quel client hello Obtient un jeton de hello du point de terminaison sur le cloud hello.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portail Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
