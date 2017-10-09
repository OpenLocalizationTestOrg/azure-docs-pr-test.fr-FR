---
title: aaaHow toocreate une application Web avec le Cache Redis | Documents Microsoft
description: "Découvrez comment toocreate une application Web avec le Cache Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>Comment toocreate une application Web avec le Cache Redis
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Ce didacticiel montre comment toocreate et déployer une application ASP.NET web application tooa web dans Azure App Service à l’aide de Visual Studio 2017. exemple d’application Hello affiche la liste des statistiques sur les équipes à partir d’une base de données et montre les différentes façons toouse Cache Redis Azure toostore et récupérer des données à partir du cache de hello. Lorsque vous effectuez le didacticiel de hello vous avez une application web en cours d’exécution qui lit et écrit la base de données tooa, optimisée avec le Cache Redis Azure et hébergés dans Azure.

Vous apprendrez ce qui suit :

* Comment toocreate un ASP.NET MVC 5 web application dans Visual Studio.
* Comment tooaccess des données à partir d’une base de données à l’aide d’Entity Framework.
* Comment tooimprove le débit des données et réduire la charge de la base de données en stockage et la récupération des données à l’aide du Cache Redis Azure.
* Comment toouse un Redis triés ensemble tooretrieve hello top 5 les équipes.
* Comment tooprovision hello ressources Azure pour l’application hello à l’aide d’un modèle de gestionnaire de ressources.
* Comment toopublish hello tooAzure d’application à l’aide de Visual Studio.

## <a name="prerequisites"></a>Composants requis
didacticiel de hello toocomplete, vous devez avoir hello suivant des conditions préalables.

* [Compte Azure](#azure-account)
* [Visual Studio 2017, avec hello Azure SDK pour .NET](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Compte Azure
Vous avez besoin d’un didacticiel de hello toocomplete compte Azure. Vous pouvez :

* [Ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Vous obtenez des crédits qui peuvent être utilisé tootry out à payer des services Azure. Même après que hello crédits épuisés, vous pouvez conserver le compte de hello et utiliser des fonctionnalités et des services Azure gratuits.
* [Activez les avantages d’abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Visual Studio 2017, avec hello Azure SDK pour .NET
didacticiel de Hello est écrit pour Visual Studio 2017 avec hello [Azure SDK pour .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools). Bonjour Azure SDK 2.9.5 est inclus avec le programme d’installation de Visual Studio hello.

Si vous avez Visual Studio 2015, vous pouvez suivre le didacticiel hello avec hello [Azure SDK pour .NET](../dotnet-sdk.md) point 2.8.2 ou version ultérieure. [Téléchargement hello plus récentes de Windows Azure SDK pour Visual Studio 2015 ici](http://go.microsoft.com/fwlink/?linkid=518003). Visual Studio est installé automatiquement avec le Kit de développement logiciel de hello si vous n’est pas déjà installé. Certains écrans diffèrent des illustrations hello indiquées dans ce didacticiel.

Si vous avez Visual Studio 2013, vous pouvez [téléchargement hello plus récentes de Windows Azure SDK pour Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322). Certains écrans diffèrent des illustrations hello indiquées dans ce didacticiel.

## <a name="create-hello-visual-studio-project"></a>Créer le projet de Visual Studio hello
1. Ouvrez Visual Studio et cliquez sur **Fichier**, **Nouveau**, **Projet**.
2. Développez hello **Visual C#** nœud Bonjour **modèles** liste, sélectionnez **Cloud**, puis cliquez sur **Application Web ASP.NET**. Vérifiez que l’option **.NET Framework 4.5.2** est sélectionnée.  Type **ContosoTeamStats** dans hello **nom** zone de texte et cliquez sur **OK**.
   
    ![Créer un projet][cache-create-project]
3. Sélectionnez **MVC** en tant que type de projet hello. 

    Vérifiez que **aucune authentification** est spécifié pour hello **authentification** paramètres. Selon votre version de Visual Studio, par défaut de hello peut être défini toosomething else. toochange, cliquez sur **modifier l’authentification** et sélectionnez **aucune authentification**.

    Si vous suivez avec Visual Studio 2015, désactivez hello **hôte hello cloud** case à cocher. Vous allez [configurer hello ressources Azure](#provision-the-azure-resources) et [publier hello application tooAzure](#publish-the-application-to-azure) dans les étapes suivantes dans le didacticiel de hello. Pour obtenir un exemple de configuration d’une application Service web d’application à partir de Visual Studio en laissant **hôte hello cloud** activée, consultez [prise en main Web Apps dans Azure App Service, à l’aide d’ASP.NET et Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
    ![Sélectionner un modèle de projet][cache-select-template]
4. Cliquez sur **OK** projet hello de toocreate.

## <a name="create-hello-aspnet-mvc-application"></a>Créer hello application ASP.NET MVC
Dans cette section du didacticiel de hello, vous allez créer l’application de base hello qui lit et affiche des statistiques sur les équipes à partir d’une base de données.

* [Ajoutez le package NuGet Entity Framework de hello](#add-the-entity-framework-nuget-package)
* [Ajouter un modèle de hello](#add-the-model)
* [Ajouter un contrôleur de hello](#add-the-controller)
* [Configurer des vues de hello](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>Ajoutez le package NuGet Entity Framework de hello

1. Cliquez sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu.
2. Exécution hello après une commande à partir de hello **Package Manager Console** fenêtre.
    
    ```
    Install-Package EntityFramework
    ```

Pour plus d’informations sur ce package, consultez hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.

### <a name="add-hello-model"></a>Ajouter un modèle de hello
1. Cliquez avec le bouton droit sur **Modèles** dans l’**Explorateur de solutions** et sélectionnez **Ajouter**, **Classe**. 
   
    ![Ajouter un modèle][cache-model-add-class]
2. Entrez `Team` pour le nom de la classe hello et cliquez sur **ajouter**.
   
    ![Ajouter une classe de modèle][cache-model-add-class-dialog]
3. Remplacez hello `using` instructions haut hello hello `Team.cs` fichier avec les éléments suivants de hello `using` instructions.

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. Remplacez la définition hello Hello `Team` classe avec hello suivant extrait de code qui contient une mise à jour `Team` classe Définition ainsi que d’autres classes d’assistance de Entity Framework. Pour plus d’informations sur hello code première approche tooEntity Framework qui est utilisé dans ce didacticiel, consultez [Code premier tooa nouvelle base de données](https://msdn.microsoft.com/data/jj193542).

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. Dans **l’Explorateur de solutions**, double-cliquez sur **web.config** tooopen il.
   
    ![Web.config][cache-web-config]
2. Ajoutez hello suit `connectionStrings` section. nom Hello hello de chaîne de connexion doit correspondre au nom hello Hello classe de contexte de base de données Entity Framework qui est `TeamContext`.

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Vous pouvez ajouter hello nouvelle `connectionStrings` section afin qu’elle suive `configSections`, comme indiqué dans hello l’exemple suivant.

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > Votre chaîne de connexion peut être différent selon la version de hello de Visual Studio et SQL Server Express edition utilisé didacticiel de hello toocomplete. modèle de web.config Hello doit être configuré toomatch votre installation et peut contenir `Data Source` comme des entrées `(LocalDB)\v11.0` (à partir de SQL Server Express 2012) ou `Data Source=(LocalDB)\MSSQLLocalDB` (SQL Server Express 2014 et version ultérieure). Pour plus d’informations sur les chaînes de connexion et les versions de SQL Express, consultez [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).

### <a name="add-hello-controller"></a>Ajouter un contrôleur de hello
1. Appuyez sur **F6** projet hello de toobuild. 
2. Dans **l’Explorateur de solutions**, avec le bouton hello **contrôleurs** dossier et choisissez **ajouter**, **contrôleur**.
   
    ![Ajouter un contrôleur][cache-add-controller]
3. Sélectionnez **Contrôleur MVC 5 avec vues, en utilisant Entity Framework**, puis cliquez sur **Ajouter**. Si vous obtenez une erreur après avoir cliqué sur **ajouter**, assurez-vous que vous avez créé un projet de hello tout d’abord.
   
    ![Ajouter une classe de contrôleur][cache-add-controller-class]
4. Sélectionnez **Team (ContosoTeamStats.Models)** de hello **classe de modèle** liste déroulante. Sélectionnez **TeamContext (ContosoTeamStats.Models)** de hello **classe de contexte de données** liste déroulante. Type `TeamsController` Bonjour **contrôleur** zone de texte Nom (si elle n’est pas remplie automatiquement). Cliquez sur **ajouter** toocreate hello de classe de contrôleur et ajouter des vues par défaut hello.
   
    ![Configurer un contrôleur][cache-configure-controller]
5. Dans **l’Explorateur de solutions**, développez **Global.asax** et double-cliquez sur **Global.asax.cs** tooopen il.
   
    ![Global.asax.cs][cache-global-asax]
6. Ajouter hello suivant deux `using` instructions haut hello du fichier hello sous hello autres `using` instructions.

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. Ajouter hello suivant la ligne de code à fin hello Hello `Application_Start` (méthode).

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. Dans l’**Explorateur de solutions**, développez `App_Start` et double-cliquez sur `RouteConfig.cs`.
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. Remplacez `controller = "Home"` Bonjour suivant code Bonjour `RegisterRoutes` méthode avec `controller = "Teams"` comme indiqué dans hello l’exemple suivant.

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>Configurer des vues de hello
1. Dans **l’Explorateur de solutions**, développez hello **vues** dossier puis hello **Shared** dossier, puis double-cliquez sur **_Layout.cshtml**. 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. Modifier le contenu hello Hello `title` élément et remplacer `My ASP.NET Application` avec `Contoso Team Stats` comme indiqué dans hello l’exemple suivant.

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. Bonjour `body` section, mise à jour de hello tout d’abord `Html.ActionLink` instruction et remplacer `Application name` avec `Contoso Team Stats` et remplacer `Home` avec `Teams`.
   
   * Avant : `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * Après : `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![Modifications du code][cache-layout-cshtml-code]
2. Appuyez sur **Ctrl + F5** toobuild et exécuter l’application hello. Cette version de l’application hello lit les résultats hello directement à partir de la base de données hello. Hello de note **créer un nouveau**, **modifier**, **détails**, et **supprimer** les actions qui ont été automatiquement ajouté toohello application par hello **Contrôleur MVC 5 avec vues, utilisant Entity Framework** structure. Dans la section suivante de hello du didacticiel de hello vous ajouterez des données de Cache Redis toooptimize hello accéder et fournissent des fonctionnalités supplémentaires toohello application.

![Application de départ][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>Configurer hello application toouse Cache Redis
Dans cette section du didacticiel de hello, vous allez configurer toostore d’application exemple hello et extraire des statistiques sur les équipes Contoso à partir d’une instance de Cache Redis Azure à l’aide de hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) client de cache.

* [Configurer l’application de hello toouse StackExchange.Redis](#configure-the-application-to-use-stackexchangeredis)
* [Mettre à jour hello TeamsController classe tooreturn résultats à partir du cache de hello ou base de données hello](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [Hello, créer, modifier, de mettre à jour et supprimer des toowork méthodes avec un cache de hello](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [Mettre à jour hello équipes Index vue toowork avec le cache de hello](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>Configurer l’application de hello toouse StackExchange.Redis
1. tooconfigure une application cliente dans Visual Studio à l’aide de hello package StackExchange.Redis NuGet, cliquez sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu.
2. Exécution hello après une commande à partir de hello `Package Manager Console` fenêtre.
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    Hello NuGet package télécharge et ajoute hello obligatoire des références d’assembly pour votre tooaccess d’application client du Cache Redis Azure avec le client de cache StackExchange.Redis hello. Si vous préférez toouse une version de nom fort de hello `StackExchange.Redis` bibliothèque cliente, installation hello `StackExchange.Redis.StrongName` package.
3. Dans **l’Explorateur de solutions**, développez hello **contrôleurs** et double-cliquez sur **TeamsController.cs** tooopen il.
   
    ![Contrôleur Teams][cache-teamscontroller]
4. Ajouter hello suivant deux `using` instructions trop**TeamsController.cs**.

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. Ajouter hello suivant deux propriétés toohello `TeamsController` classe.

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. Créer un fichier sur votre ordinateur nommé `WebAppPlusCacheAppSecrets.config` et les placer dans un emplacement qui ne sont pas vérifiées avec le code source de hello de votre application d’exemple, si vous décidez toocheck dans un emplacement. Dans cette hello exemple `AppSettingsSecrets.config` fichier se trouve dans `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.
   
    Modifier hello `WebAppPlusCacheAppSecrets.config` et ajoutez hello suivant le contenu. Si vous exécutez des application hello localement cette information est instance de Cache Redis Azure tooyour tooconnect utilisé. Plus loin dans le didacticiel de hello, vous allez configurer une instance de Cache Redis Azure et mettre à jour le mot de passe et le nom du cache hello. Si vous ne prévoyez pas toorun hello exemple d’application localement, vous pouvez ignorer la création de hello de ce fichier et les étapes suivantes hello qui font référence les fichiers hello, car lorsque vous déployez tooAzure hello application récupère les informations de connexion hello du cache à partir de l’application hello paramètre de hello Web App et non à partir de ce fichier. Depuis hello `WebAppPlusCacheAppSecrets.config` n’est pas déployée tooAzure avec votre application, vous n’en avez besoin, sauf si vous envisagez d’application de hello toorun localement.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Dans **l’Explorateur de solutions**, double-cliquez sur **web.config** tooopen il.
   
    ![Web.config][cache-web-config]
2. Ajoutez hello suivant `file` attribut toohello `appSettings` élément. Si vous avez utilisé un autre nom de fichier ou un emplacement, remplacez par les valeurs hello ceux indiqués dans l’exemple de hello.
   
   * Avant : `<appSettings>`
   * Après : ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   Hello ASP.NET runtime fusionne contenu hello du fichier externe de hello avec balisage hello Bonjour `<appSettings>` élément. Hello runtime ignore l’attribut de fichier hello si hello spécifié ne se trouve. Vos secrets (cache tooyour chaîne hello connexion) ne sont pas inclus dans le cadre du code source de hello pour une application hello. Lorsque vous déployez votre tooAzure d’application web, hello `WebAppPlusCacheAppSecrests.config` fichier ne sera pas déployé (c’est ce que vous souhaitez). Il existe plusieurs façons toospecify ces clés secrètes dans Azure, et dans ce didacticiel qu’ils sont configurés automatiquement pour vous lorsque vous [configurer hello ressources Azure](#provision-the-azure-resources) dans une étape ultérieure du didacticiel. Pour plus d’informations sur l’utilisation des clés secrètes dans Azure, consultez [meilleures pratiques pour le déploiement de mots de passe et d’autres données sensibles tooASP.NET et Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>Mettre à jour hello TeamsController classe tooreturn résultats à partir du cache de hello ou base de données hello
Dans cet exemple, les statistiques sur les équipes peuvent être récupérés à partir de la base de données hello ou à partir du cache de hello. Statistiques sur les équipes sont stockés dans le cache de hello sous la forme sérialisée `List<Team>`et également comme un ensemble trié à l’aide des types de données Redis. Lors de la récupération des éléments d’un ensemble trié, vous pouvez récupérer certains éléments, récupérer tous les éléments ou effectuer une requête sur certains éléments. Dans cet exemple, vous devez interroger ensemble hello triée pour les équipes top 5 hello classés par nombre de wins.

> [!NOTE]
> Il n’est pas requis toostore hello statistiques sur les équipes dans plusieurs formats dans le cache de hello dans l’ordre toouse Cache Redis Azure. Ce didacticiel utilise plusieurs formats toodemonstrate certaines des différentes façons de hello et différents types de données, vous pouvez utiliser les données toocache.
> 
> 

1. Ajoutez hello suivant `using` instructions toohello `TeamsController.cs` fichier en haut hello avec hello autres `using` instructions.

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. Remplacez hello actuel `public ActionResult Index()` implémentation de méthode avec hello après mise en oeuvre.

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. Ajouter hello suivant trois méthodes toohello `TeamsController` hello tooimplement de classe `playGames`, `clearCache`, et `rebuildDB` types d’action de hello switch, instruction ajoutée dans l’extrait de code précédent hello.
   
    Hello `PlayGames` méthode met à jour les statistiques sur les équipes hello en simulant une saison des jeux et enregistre hello de base de données de résultats toohello efface hello maintenant les données à partir du cache de hello est obsolète.

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hello `RebuildDB` méthode réinitialise hello base de données avec l’ensemble des équipes, par défaut de hello génère des statistiques pour les et efface hello maintenant les données à partir du cache de hello est obsolète.

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hello `ClearCachedTeams` méthode supprime toutes les statistiques de l’équipe de mise en cache à partir du cache de hello.

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. Ajouter hello suivant quatre méthodes toohello `TeamsController` hello tooimplement de classe différentes façons de récupérer des statistiques sur les équipes hello à partir du cache de hello et base de données hello. Chacune de ces méthodes retourne une `List<Team>` qui est ensuite affiché en vue de hello.
   
    Hello `GetFromDB` méthode lit les statistiques sur les équipes hello à partir de la base de données hello.
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    Hello `GetFromList` méthode lit les statistiques sur les équipes hello cache sous la forme sérialisée `List<Team>`. S’il existe une absence dans le cache, statistiques sur les équipes hello sont lus à partir de la base de données hello et ensuite stockées dans le cache de hello pour la prochaine fois. Dans cet exemple, nous utilisons JSON.NET sérialisation tooserialize hello .NET objets tooand à partir du cache de hello. Pour plus d’informations, consultez [comment les objets dans le Cache Redis Azure toowork avec .NET](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    Hello `GetFromSortedSet` méthode lit les statistiques sur les équipes hello à partir d’un ensemble trié mis en cache. S’il existe une absence dans le cache, statistiques sur les équipes hello sont lus à partir de la base de données hello et stockées dans le cache de hello sous la forme d’un ensemble trié.

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    Hello `GetFromSortedSetTop5` méthode lit l’ensemble d’équipes 5 à partir de la mise en cache de hello triées supérieur hello. Il commence par la vérification du cache de hello existence hello Hello `teamsSortedSet` clé. Si cette clé n’est pas présente, hello `GetFromSortedSet` méthode est appelée statistiques sur les équipes tooread hello et les stocker dans le cache de hello. Ensuite, hello ensemble trié mis en cache est interrogé pour hello top 5 équipes qui sont retournées.

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>Hello, créer, modifier, de mettre à jour et supprimer des toowork méthodes avec un cache de hello
code de génération de modèles automatique Hello qui a été généré comme partie de cet exemple inclut des méthodes tooadd, modifier et supprimer des équipes. Chaque fois qu’une équipe est ajoutée, modifiée ou supprimée, les données de salutation dans le cache de hello devient obsolètes. Dans cette section, que vous allez modifier ces hello tooclear de trois méthodes mis en cache les équipes afin que le cache de hello ne sera pas synchronisé avec la base de données hello.

1. Parcourir toohello `Create(Team team)` méthode Bonjour `TeamsController` classe. Ajouter un appel toohello `ClearCachedTeams` méthode, comme indiqué dans hello l’exemple suivant.

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. Parcourir toohello `Edit(Team team)` méthode Bonjour `TeamsController` classe. Ajouter un appel toohello `ClearCachedTeams` méthode, comme indiqué dans hello l’exemple suivant.

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. Parcourir toohello `DeleteConfirmed(int id)` méthode Bonjour `TeamsController` classe. Ajouter un appel toohello `ClearCachedTeams` méthode, comme indiqué dans hello l’exemple suivant.

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>Mettre à jour hello équipes Index vue toowork avec le cache de hello
1. Dans **l’Explorateur de solutions**, développez hello **vues** dossier, puis hello **équipes** dossier, puis double-cliquez sur **Index.cshtml**.
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. Haut hello du fichier de hello, recherchez hello après l’élément de paragraphe.
   
    ![Table d’actions][cache-teams-index-table]
   
    Il s’agit de lien de hello toocreate une nouvelle équipe. Remplacez l’élément de paragraphe hello avec hello tableau suivant. Cette table comporte des liens d’action pour la création d’une nouvelle équipe, la lecture d’une nouvelle saison des jeux, l’effacement du cache de hello, récupérant les équipes de hello cache hello dans plusieurs formats, la récupération des équipes de hello à partir de la base de données hello et la reconstruction de base de données avec les données exemple nouvelle hello.

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. Défiler vers le bas de hello toohello **Index.cshtml** et ajoutez les suivant hello `tr` élément afin qu’il soit hello dernière ligne hello dernière table dans le fichier de hello.
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    Cette ligne affiche la valeur hello `ViewBag.Msg` qui contient un rapport d’état sur l’opération en cours hello. Hello `ViewBag.Msg` est définie lorsque vous cliquez sur un des liens d’action hello à partir de l’étape précédente de hello.   
   
    ![Message d’état][cache-status-message]
2. Appuyez sur **F6** projet hello de toobuild.

## <a name="provision-hello-azure-resources"></a>Configurer hello ressources Azure
toohost votre application dans Azure, vous devez d’abord configurer hello des services Azure que votre application requiert. exemple d’application Hello dans ce didacticiel utilise hello suivant des services Azure.

* Cache Redis Azure
* Application web App Service
* Base de données SQL

toodeploy ces services tooa nouvelle ou existante de la ressource de groupe de votre choix, cliquez sur hello suivant **déployer tooAzure** bouton.

[! [Déploiement tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

Cela **déployer tooAzure** bouton utilise hello [créer une application Web ainsi que le Cache Redis et la base de données SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) modèle tooprovision ces services et le jeu de hello chaîne de connexion pour le paramètre hello hello et de base de données SQL de l’application pour hello chaîne de connexion du Cache Redis Azure.

> [!NOTE]
> Si vous ne possédez pas de compte Azure, vous pouvez [créer un compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) en quelques minutes.
> 
> 

En cliquant sur hello **déployer tooAzure** bouton vous permet de toohello portail Azure et lance hello le processus de création de ressources hello décrits par le modèle de hello.

![Déployer tooAzure][cache-deploy-to-azure-step-1]

1. Bonjour **notions de base** section, sélectionnez toouse d’abonnement Azure hello, sélectionnez un groupe de ressources existant ou créez-en un et spécifier l’emplacement du groupe de ressources hello.
2. Bonjour **paramètres** section, spécifiez une **connexion administrateur** (n’utilisez pas **admin**), **mot de passe administrateur**et  **Nom de base de données**. Hello autres paramètres sont configurés pour un Service d’applications libre qui héberge le plan et les options de faible coût de hello de base de données SQL et du Cache Redis Azure, qui ne sont fournis avec un niveau gratuit.

    ![Déployer tooAzure][cache-deploy-to-azure-step-2]

3. Après avoir configuré les paramètres de hello souhaité, faites défiler fin toohello de page de hello hello lecture et les conditions et vérifiez hello **J’accepte les termes du contrat de toohello et conditions susmentionnées** case à cocher.
4. toobegin configurer les ressources hello, cliquez sur **bon**.

progression de hello tooview de votre déploiement, cliquez sur l’icône de hello et cliquez sur **déploiement démarré**.

![Le déploiement a commencé][cache-deployment-started]

Vous pouvez afficher l’état hello de votre déploiement sur hello **Microsoft.Template** panneau.

![Déployer tooAzure][cache-deploy-to-azure-step-3]

Lors de la configuration est terminée, vous pouvez publier votre tooAzure d’application à partir de Visual Studio.

> [!NOTE]
> Toutes les erreurs qui peuvent se produire pendant le processus d’approvisionnement de hello sont affichés sur hello **Microsoft.Template** panneau. Les erreurs courantes sont liées à un trop grand nombre de serveurs SQL ou de plans d’hébergement Free App Service par abonnement. Corrigez les erreurs et redémarrer le processus de hello en cliquant sur **redéployer** sur hello **Microsoft.Template** panneau ou hello **déployer tooAzure** bouton dans ce didacticiel.
> 
> 

## <a name="publish-hello-application-tooazure"></a>Publier hello application tooAzure
Dans cette étape du didacticiel de hello, vous allez publier hello application tooAzure et l’exécuter dans le cloud de hello.

1. Avec le bouton hello **ContosoTeamStats** de projet dans Visual Studio et choisissez **publier**.
   
    ![Publier][cache-publish-app]
2. Cliquez sur **Microsoft Azure App Service**, choisissez **Select Existing** (Sélectionner existant), puis cliquez sur **Publier**.
   
    ![Publier][cache-publish-to-app-service]
3. Sélectionnez l’abonnement hello utilisé lors de la création hello ressources Azure, développez groupe de ressources hello contenant des ressources hello et sélectionnez hello souhaité de l’application Web. Si vous avez utilisé hello **déployer tooAzure** bouton commence par le nom de votre application Web **site Web** suivi par des caractères supplémentaires.
   
    ![Sélectionner l’application web][cache-select-web-app]
4. Cliquez sur **OK** hello toobegin processus de publication. Après quelques instants hello processus de publication est terminée et un navigateur est lancé par hello, exemple d’application en cours d’exécution. Si vous obtenez une erreur DNS lors de la validation ou de la publication et hello pour le processus de fourniture hello ressources Azure pour l’application hello récemment terminée, patientez quelques instants, puis réessayez.
   
    ![Cache ajouté][cache-added-to-application]

Hello tableau suivant décrit chaque lien d’action à partir de l’exemple d’application hello.

| Action | Description |
| --- | --- |
| Création |Crée une équipe. |
| Play Season |Lire une saison des jeux, des statistiques de mise à jour hello équipe, et désactivez les obsolète des données de l’équipe à partir du cache de hello. |
| Clear Cache |Statistiques d’équipe hello clair à partir du cache de hello. |
| List from Cache |Récupérer les statistiques d’équipe hello à partir du cache de hello. S’il existe une absence dans le cache, les statistiques hello de charge à partir de la base de données hello et enregistrer toohello cache pour la prochaine fois. |
| Sorted Set from Cache |Extraire les statistiques équipe hello cache hello à l’aide d’un ensemble trié. S’il existe une absence dans le cache, les statistiques hello de charge à partir de la base de données hello et enregistrer cache toohello à l’aide d’un ensemble trié. |
| Top 5 Teams from Cache |Extraire les équipes de 5 premières hello cache hello à l’aide d’un ensemble trié. S’il existe une absence dans le cache, les statistiques hello de charge à partir de la base de données hello et enregistrer cache toohello à l’aide d’un ensemble trié. |
| Load from DB |Récupérer les statistiques hello équipe à partir de la base de données hello. |
| Rebuild DB |Reconstruire la base de données hello et recharger les exemples de données team. |
| Edit / Details / Delete |Modifie une équipe, affiche les détails d’une équipe, supprime une équipe. |

Cliquez sur certaines des actions de hello et faire des essais avec la récupération des données de salutation à partir de sources différentes de hello. Pas les différences de hello dans hello temps toocomplete hello différentes façons de récupérer des données de salutation à partir de la base de données hello et cache de hello.

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>Supprimer des ressources de hello lorsque vous avez terminé avec l’application hello
Lorsque vous avez terminé avec l’application hello du didacticiel de l’exemple, vous pouvez supprimer hello Azure utilisées dans tooconserve commande coût des ressources et des ressources. Si vous utilisez hello **déployer tooAzure** bouton Bonjour [configurer hello ressources Azure](#provision-the-azure-resources) section et toutes vos ressources sont contenus dans hello même groupe de ressources, vous pouvez les supprimer ensemble dans un opération en supprimant le groupe de ressources hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) et cliquez sur **groupes de ressources**.
2. Nom de votre groupe de ressources dans hello hello de type **filtrer les éléments...**  zone de texte.
3. Cliquez sur **...**  toohello à droite de votre groupe de ressources.
4. Cliquez sur **Supprimer**.
   
    ![Supprimer][cache-delete-resource-group]
5. Hello nom de type votre groupe de ressources et cliquez sur **supprimer**.
   
    ![Confirmation de suppression][cache-delete-confirm]

Une fois les ressources de hello quelques instants groupe et toutes ses ressources de relation contenant-contenus sont supprimés.

> [!IMPORTANT]
> Notez que la suppression d’un groupe de ressources est irréversible et ce groupe de ressources hello et toutes les ressources hello qu’il contient sont supprimés définitivement. Assurez-vous que vous ne supprimez pas accidentellement groupe de ressource incorrect hello ou des ressources. Si vous avez créé des ressources hello pour l’hébergement de cet exemple à l’intérieur d’un groupe de ressources existant, vous pouvez supprimer individuellement chaque ressource à partir de leurs panneaux respectifs.
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>Exécutez l’exemple d’application hello sur votre ordinateur local
application de hello toorun localement sur votre ordinateur, vous avez besoin d’un cache Azure Redis Cache d’instance dans le toocache vos données. 

* Si vous avez publié votre tooAzure application comme décrit dans la section précédente de hello, vous pouvez utiliser l’instance de Cache Redis Azure hello qui a été configuré lors de cette étape.
* Si vous avez une autre instance de Cache Redis Azure existante, vous pouvez utiliser ce toorun cet exemple localement.
* Si vous devez toocreate une instance de Cache Redis Azure, vous pouvez suivre les étapes de hello dans [créer un cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

Une fois que vous avez sélectionnée ou créée hello cache toouse, parcourir le cache toohello Bonjour portail Azure et récupérer hello [nom d’hôte](cache-configure.md#properties) et [clés d’accès](cache-configure.md#access-keys) pour votre cache. Pour obtenir des instructions, consultez la page [Configuration des paramètres de cache Redis](cache-configure.md#configure-redis-cache-settings).

1. Ouvrez hello `WebAppPlusCacheAppSecrets.config` fichier que vous avez créé au cours de hello [configurer hello application toouse Cache Redis](#configure-the-application-to-use-redis-cache) étape de ce didacticiel à l’aide de l’éditeur hello de votre choix.
2. Modifier hello `value` d’attribut et remplacez `MyCache.redis.cache.windows.net` avec hello [nom d’hôte](cache-configure.md#properties) de votre cache et spécifiez soit hello [clé primaire ou secondaire](cache-configure.md#access-keys) de votre cache en tant que mot de passe hello.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Appuyez sur **Ctrl + F5** application hello de toorun.

> [!NOTE]
> Notez qu’étant donné que l’application hello, y compris la base de données hello, s’exécute localement et le Cache Redis hello est hébergé dans Azure, hello cache peut apparaître toounder-réaliser hello de bases de données. Pour de meilleures performances, hello application cliente et l’instance de Cache Redis Azure doit être Bonjour même emplacement. 
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [mise en route avec ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) sur hello [ASP.NET](http://asp.net/) site.
* Pour plus d’exemples de création d’une application Web ASP.NET dans le Service d’applications, consultez [créer et déployer une application de web ASP.NET dans Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) de hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 connexion [démonstration](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * Pour plus des Démarrages rapides à partir de la démonstration de HealthClinic.biz hello, consultez [Démarrages rapides outils de développement Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
* En savoir plus sur hello [Code premier tooa nouvelle base de données](https://msdn.microsoft.com/data/jj193542) approche tooEntity Framework qui est utilisé dans ce didacticiel.
* Apprenez-en davantage sur les [applications web dans Azure App Service](../app-service-web/app-service-web-overview.md).
* Découvrez comment trop[moniteur](cache-how-to-monitor.md) votre cache Bonjour portail Azure.
* Explorez les fonctionnalités Premium du Cache Redis Azure
  
  * [La persistance tooconfigure Premium Azure Redis cache](cache-how-to-premium-persistence.md)
  * [Comment tooconfigure clustering Premium Azure Redis cache](cache-how-to-premium-clustering.md)
  * [Comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache](cache-how-to-premium-vnet.md)
  * Consultez hello [Azure Redis Cache-FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) pour plus d’informations sur la taille, le débit et la bande passante avec des caches de niveau premium.

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

