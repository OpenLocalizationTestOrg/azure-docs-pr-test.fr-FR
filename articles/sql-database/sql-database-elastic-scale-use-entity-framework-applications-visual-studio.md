---
title: "bibliothèque cliente de base de données élastique aaaUsing avec Entity Framework | Documents Microsoft"
description: "Utilisez la bibliothèque cliente de la base de données élastique et Entity Framework pour le codage de bases de données"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>Bibliothèque cliente de la base de données élastique avec Entity Framework
Ce document montre les modifications hello dans une application Entity Framework qui sont nécessaire toointegrate avec hello [outils de base de données élastique](sql-database-elastic-scale-introduction.md). Hello porte sur la composition de [gestion de carte de partitions](sql-database-elastic-scale-shard-map-management.md) et [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) avec hello Entity Framework **Code First** approche. Hello [Code First - nouvelle base de données](http://msdn.microsoft.com/data/jj193542.aspx) didacticiel pour EF sert de notre exemple en cours d’exécution tout au long de ce document. exemple de code Hello accompagnant ce document fait partie d’outils de base de données élastique de jeu d’échantillons Bonjour les exemples de Code Visual Studio.

## <a name="downloading-and-running-hello-sample-code"></a>Téléchargement et exécution hello, exemple de Code
code de hello toodownload de cet article :

* Visual Studio 2012 ou une version ultérieure est nécessaire. 
* Télécharger hello [élastique outils de base de données pour SQL Azure - exemple d’Entity Framework intégration](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) à partir de MSDN. Décompressez hello exemple tooa d’emplacement de votre choix.
* Démarrez Visual Studio. 
* Dans Visual Studio, sélectionnez Fichier -> Ouvrir un projet/une solution. 
* Bonjour **ouvrir le projet** boîte de dialogue, naviguez exemple toohello vous avez téléchargé et sélectionnez **EntityFrameworkCodeFirst.sln** tooopen hello exemple. 

exemple de hello toorun, vous devez toocreate trois bases de données vides dans la base de données SQL Azure :

* Une base de données du gestionnaire des cartes de partitions
* Une base de données nommée Shard 1
* Une base de données nommée Shard 2

Une fois que vous avez créé ces bases de données, renseignez les espaces réservés hello dans **Program.cs** avec le nom de votre serveur de base de données SQL Azure, les noms de base de données hello et vos bases de données toohello de tooconnect informations d’identification. Générez la solution hello dans Visual Studio. Visual Studio télécharge les packages NuGet hello requis pour la bibliothèque cliente de base de données élastique hello, Entity Framework et gestion dans le cadre du processus de génération hello d’erreurs transitoires. Assurez-vous que la restauration des packages NuGet est activée pour votre solution. Vous pouvez l’activer en cliquant sur le fichier de solution hello Bonjour Explorateur de solutions Visual Studio. 

## <a name="entity-framework-workflows"></a>Flux de travail Entity Framework
Les développeurs de Entity Framework s’appuient sur l’un des hello suivant quatre applications toobuild de flux de travail et de persistance tooensure pour les objets de l’application : 

* **Code First (nouvelle base de données)**: hello développeur d’EF crée un modèle de hello dans le code de l’application hello et EF génère ensuite une base de données hello à partir de celui-ci. 
* **Code First (base de données existante)**: développeur de hello permet de générer le code de l’application hello pour le modèle de hello à partir d’une base de données EF.
* **Modèle premier**: développeur de hello crée un modèle de hello dans le Concepteur EF hello et EF crée ensuite une base de données hello à partir du modèle de hello.
* **Base de données de la première**: développeur de hello utilise EF outils modèle de hello tooinfer à partir d’une base de données existante. 

Toutes ces méthodes reposent sur tootransparently de classe DbContext hello gérer les connexions de base de données et le schéma de base de données pour une application. Que nous allons aborder plus en détail plus loin dans le document de hello, différents des constructeurs de classe de base de DbContext hello autorisent pour différents niveaux de contrôle sur la création de la connexion de base de données d’amorçage et le schéma de la création. Difficultés se présentent essentiellement à partir de faits hello gestion des connexions de base de données hello fournie par EF située à l’intersection avec les fonctionnalités de gestion des connexions hello hello données dépendant d’interfaces de routage fournies par la bibliothèque cliente de base de données élastique hello. 

## <a name="elastic-database-tools-assumptions"></a>Hypothèses des outils de base de données élastique
Vous trouverez les définitions des termes évoqués ici sur la page [Glossaire des outils de base de données élastique](sql-database-elastic-scale-glossary.md).

La bibliothèque cliente de base de données permet de définir des partitions pour les données de votre application. Ces partitions sont nommées shardlets. Shardlets sont identifiées par une clé de partitionnement et de bases de données toospecific mappé. Une application peut avoir qu’un grand nombre de bases de données en fonction des besoins et distribuer hello shardlets tooprovide suffisamment de capacité ou les performances étant donné les besoins de l’entreprise en cours. mappage Hello des bases de données de partitionnement les valeurs de clé toohello est stockée par une carte de partitions fournie par l’API du client de base de données élastique hello. Nous appelons cette fonctionnalité **Gestion des cartes de partitions**, ou GCP. carte de partitions Hello sert également de broker hello de connexions de base de données pour les requêtes qui comportent une clé de partitionnement. Nous nous référons fonctionnalité toothis comme **routage dépendant des données**. 

Gestionnaire de cartes de partitions Hello protège les utilisateurs à partir des vues incohérentes dans les données de shardlet qui peuvent se produire lorsque des opérations de gestion shardlet simultanés (par exemple, le déplacement de données à partir d’une seule partition tooanother) sont produisent. toodo hello par conséquent, les cartes de partitions gérés par des connexions de base de données hello client bibliothèque broker hello pour une application. Ainsi, kill de hello partition carte fonctionnalité tooautomatically une connexion de base de données lorsque les opérations de gestion de partitions peut affecter les shardlets hello connexion de hello a été créée pour. Cette approche doit toointegrate avec certaines des fonctionnalités de EF, telles que la création de nouvelles connexions à partir d’un un toocheck existant pour l’existence de base de données. En règle générale, nous avons observé que les constructeurs DbContext standards hello uniquement fonctionnent de façon fiable pour les connexions de base de données fermée qui peuvent être clonées sans risque pour le travail EF. le principe de conception Hello de base de données élastique est à la place de connexions de broker ouvert de tooonly. On pourrait penser que la fermeture d’une connexion répartie par la bibliothèque cliente de hello avant de le passer sur toohello DbContext EF peut résoudre ce problème. Toutefois, par la fermeture de la connexion de hello et s’appuyer sur EF toore-ouvrir, une foregoes des vérifications de validation et la cohérence hello effectuées par la bibliothèque de hello. fonctionnalités de migrations Hello dans EF, cependant, utilisent ces hello toomanage de connexions sous-jacent du schéma de base de données d’une manière qui est transparente toohello application. Dans l’idéal, nous comme tooretain et associer ces fonctionnalités à partir de la bibliothèque cliente de base de données élastique hello et EF Bonjour même application. Hello section suivante décrit ces propriétés et les exigences de plus en détail. 

## <a name="requirements"></a>Configuration requise
Lorsque vous travaillez avec la bibliothèque cliente de base de données élastique hello et API Entity Framework, nous souhaitons hello tooretain propriétés suivantes : 

* **Montée en puissance parallèle**: tooadd ou supprimer des bases de données de la couche de données hello d’application partitionnée hello en fonction des besoins de capacité hello de l’application hello. Cela signifie que le contrôle sur la création de hello hello et suppression de bases de données et à l’aide de hello de base de données élastique partition carte manager API toomanage bases de données et les mappages de shardlets. 
* **Cohérence**: application hello emploie le partitionnement et utilise hello fonctionnalités routage de données dépendant de la bibliothèque cliente de hello. tooavoid ou corruption des résultats de requête incorrect, les connexions sont réparties via le Gestionnaire de carte de partitions hello. Cela maintient également la validation et la cohérence.
* **Code First**: plus de commodité tooretain hello de paradigme de première du EF code. Dans le Code First, les classes dans l’application hello sont mappées en toute transparence toohello sous-jacente des structures de base de données. code de l’application Hello interagit avec DbSets qui masque la plupart des aspects impliqués dans hello sous-jacent du traitement de la base de données.
* **Schéma**: Entity Framework gère la création initiale de schémas de base de données et l'évolution subséquente des schémas via des migrations. En conservant ces fonctionnalités, adapter votre application est simple comme Bonjour données évoluent. 

Hello guide suivant indique comment toosatisfy ces exigences pour les applications de Code First à l’aide des outils de base de données élastique. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>Routage dépendant des données à l'aide de DbContext EF
Les connexions de base de données avec Entity Framework sont généralement gérées via des classes secondaires de **DbContext**. Créez ces sous-classes en procédant à une dérivation à partir de **DbContext**. C’est ici que vous définissez votre **DbSets** qui implémentent des collections de base de données sauvegardée hello d’objets CLR pour votre application. Dans le contexte de hello de routage dépendant des données, nous pouvons identifier plusieurs propriétés utiles qui ne contiennent pas nécessairement pour d’autres scénarios d’application première EF code : 

* base de données Hello existe déjà et a été inscrit dans la carte de partitions de base de données élastique hello. 
* schéma Hello de l’application hello a déjà été déployé toohello de base de données (voir ci-après). 
* Base de données du toohello de connexions routage dépendant des données sont réparties par carte de partitions hello. 

toointegrate **DbContexts** avec routage dépendant des données pour la montée en puissance parallèle :

1. Créer des connexions de base de données physique via des interfaces client hello élastique de base de données du Gestionnaire de carte de partitions hello, 
2. Retour à la ligne connexion hello avec hello **DbContext** sous-classe
3. Passer de connexion de hello vers le bas dans hello **DbContext** tooensure classes tout traitement hello côté d’EF hello se produit également de base. 

Hello, exemple de code suivant illustre cette approche. (Ce code est également Bonjour accompagnant de projet Visual Studio)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>Points principaux
* Un nouveau constructeur remplace le constructeur par défaut de hello dans une sous-classe de DbContext hello 
* Hello nouveau constructeur prend des arguments hello qui sont requis pour le routage dépendant des données via la bibliothèque cliente de base de données élastique :
  
  * tooaccess de carte de partitions Hello hello interfaces de routage dépendant des données,
  * Hello partitionnement tooidentify clé hello shardlet,
  * chaîne de connexion avec les informations d’identification de hello pour les partitions de toohello de connexion routage hello dépendant des données. 
* constructeur de classe de base toohello Hello appel prend un détournement dans une méthode statique qui effectue toutes les étapes de hello nécessaire pour le routage dépendant des données. 
  
  * Elle utilise appel de OpenConnectionForKey hello d’interfaces de client de base de données élastique hello tooestablish de carte de partitions hello une connexion ouverte.
  * carte de partitions Hello crée les partitions toohello hello connexion ouverte qui contient le shardlet hello pour hello étant donné la clé de partitionnement.
  * Cette connexion ouverte est passée de constructeur de classe de base toohello arrière de tooindicate DbContext que cette connexion est toobe utilisé par EF au lieu de laisser EF à créer une nouvelle connexion automatiquement. Cette connexion de hello moyen a été marquée par l’API du client de base de données élastique hello afin qu’il peut garantir la cohérence dans les opérations de gestion de carte de partitions.

Utilisez le nouveau constructeur de hello pour votre sous-classe DbContext au lieu de constructeur par défaut de hello dans votre code. Voici un exemple : 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

nouveau constructeur de Hello ouvre les partitions toohello hello connexion qui contient les données hello pour shardlet hello identifié par la valeur hello **tenantid1**. Hello code Bonjour **à l’aide de** bloc reste inchangée tooaccess hello **DbSet** pour les blogs utilisant EF sur les partitions hello pour **tenantid1**. Cela modifie la sémantique de code hello Bonjour à l’aide de bloc de telle sorte que toutes les opérations de base de données sont désormais étendue toohello une seule partition où **tenantid1** est conservé. Par exemple, une requête LINQ sur les blogs hello **DbSet** retourner uniquement les blogs stockés sur la partition actuelle de hello, mais pas hello ceux stockés sur les autres partitions.  

#### <a name="transient-faults-handling"></a>Gestion des erreurs temporaires
Hello Microsoft Patterns & Practices équipe hello publiée [hello bloc applicatif de pannes gestion](https://msdn.microsoft.com/library/dn440719.aspx). bibliothèque de Hello est utilisé avec la bibliothèque cliente de mise à l’échelle élastique en combinaison avec EF. Toutefois, assurez-vous que n’importe quelle exception temporaire retourne place tooa où nous pouvons garantir que ce nouveau constructeur de hello est utilisé après une panne temporaire afin que toute nouvelle tentative de connexion à l’aide de constructeurs hello que nous avons modifié. Sinon, un toohello de connexion correct partition n’est pas garantie, et il ne sont a aucuns garanties connexion de hello est conservée en tant que modifications carte de partitions toohello se produisent. 

Hello exemple de code suivant illustre comment une stratégie de nouvelle tentative SQL peut être utilisée autour hello nouvelle **DbContext** constructeurs de la sous-classe : 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** Bonjour code ci-dessus est défini comme un **SqlDatabaseTransientErrorDetectionStrategy** avec un nombre de tentatives de 10 et 5 secondes délai entre deux tentatives. Cette approche est semblable toohello des conseils pour EF et les transactions d’initiée par l’utilisateur (voir [Limitations de nouvelle tentative de stratégies d’exécution (EF6 et versions ultérieures)](http://msdn.microsoft.com/data/dn307226). Les deux situations exigent ce programme d’application hello contrôle hello étendue toowhich hello exception passagère retourne : tooeither rouvrir les transactions hello ou (comme indiqué) recréer le contexte de hello de constructeur approprié de hello qu’utilise hello élastique de base de données bibliothèque cliente.

Hello toocontrol besoin où des exceptions transitoires nous prennent à portée également exclut hello utilisation d’intégrées de hello **SqlAzureExecutionStrategy** qui est livré avec EF. **SqlAzureExecutionStrategy** serait rouvrir une connexion, mais pas utiliser **OpenConnectionForKey** et par conséquent ignorer toute validation hello qui est effectuée dans le cadre de hello **OpenConnectionForKey** appeler. En revanche, exemple de code hello utilise intégrées de hello **DefaultExecutionStrategy** qui est également fourni avec EF. Par opposition trop**SqlAzureExecutionStrategy**, elle fonctionne correctement en association avec la stratégie de nouvelle tentative hello à partir de la gestion d’erreur temporaire. stratégie d’exécution Hello est définie dans hello **ElasticScaleDbConfiguration** classe. Notez que nous avons ne décidé pas toouse **DefaultSqlExecutionStrategy** , car il suggère de toouse **SqlAzureExecutionStrategy** en cas d’exceptions transitoires - qui entraînerait un comportement de toowrong comme indiqué. Pour plus d’informations sur les stratégies de nouvelle tentative autre hello et EF, consultez [résilience des connexions dans EF](http://msdn.microsoft.com/data/dn456835.aspx).     

#### <a name="constructor-rewrites"></a>Réécritures de constructeur
exemples de code ci-dessus Hello illustrent par défaut de hello constructeur réécrit requis pour votre application de données de commandes toouse dépendantes de routage avec hello Entity Framework. Hello tableau suivant permet de généraliser les constructeurs de tooother de cette approche. 

| Constructeur en cours | Constructeur réécrit pour les données | Constructeur de base | Remarques |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |connexion de Hello doit toobe une fonction de la carte de partitions hello et clé de routage dépendant des données hello. Tooby passe la création de la connexion automatique par EF et d’utiliser à la place les connexion de hello partition carte toobroker hello. |
| MyContext(string) |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |connexion de Hello est une fonction de la carte de partitions hello et clé de routage dépendant des données hello. Une chaîne de connexion ou le nom de base de données fixe ne fonctionne pas comme ils validation de dérivation par carte de partitions hello. |
| MyContext(DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |connexion de Hello sera créée pour hello donné de clé de partitionnement et de mappage de partition avec le modèle hello fournis. modèle compilé de Hello est passée sur c'tor de base toohello. |
| MyContext(DbConnection, bool) |ElasticScaleContext(ShardMap, TKey, bool) |DbContext(DbConnection, bool) |connexion de Hello doit toobe déduit à partir de la carte de partitions hello et clé de hello. Il ne peut pas être fourni en tant qu’entrée (sauf si cette entrée a été déjà à l’aide de carte de partitions hello et clé de hello). valeur booléenne de Hello est passée. |
| MyContext(string, DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |connexion de Hello doit toobe déduit à partir de la carte de partitions hello et clé de hello. Il ne peut pas être fourni en tant qu’entrée (sauf si cette entrée a été à l’aide de carte de partitions hello et clé de hello). modèle de compilé Hello est passée. |
| MyContext(ObjectContext, bool) |ElasticScaleContext(ShardMap, TKey, ObjectContext, bool) |DbContext(ObjectContext, bool) |nouveau constructeur de Hello doit tooensure toute connexion Bonjour Qu'objectcontext passée comme une entrée est tooa repositionnés gérés par élastique. Une présentation détaillée des ObjectContexts est abordée dans ce document hello. |
| MyContext(DbConnection, DbCompiledModel,bool) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel, bool) |DbContext(DbConnection, DbCompiledModel, bool); |connexion de Hello doit toobe déduit à partir de la carte de partitions hello et clé de hello. connexion de Hello ne peut pas être fournie en tant qu’entrée (sauf si cette entrée a été déjà à l’aide de carte de partitions hello et clé de hello). Modèle et booléen sont transmis sur le constructeur de classe de base toohello. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>Déploiement de schéma de partition via des migrations Entity Framework
Gestion des schémas automatique est une commodité fournie par hello Entity Framework. Dans le contexte de hello d’applications à l’aide des outils de base de données élastique, nous souhaitons tooretain cette partitions toonewly créé de capacité tooautomatically disposition hello schéma lorsque des bases de données sont ajoutés les application partitionnée toohello. Hello est principalement utilisé capacité tooincrease au niveau de données hello pour les applications partitionnées utilisant EF. S’appuyer sur les fonctionnalités de EF pour la gestion du schéma permet de réduire l’effort d’administration de base de données hello avec une application partitionnée créée sur EF. 

Le déploiement de schéma via des migrations EF fonctionne mieux sur des **connexions non ouvertes**. Il s’agit en revanche toohello scénario de routage dépendant des données qui s’appuie sur connexion hello ouvert fournie par l’API du client de base de données élastique hello. Une autre différence est la spécification de cohérence hello : lors de la cohérence tooensure souhaitable pour toutes les données dépendant de routage connexions tooprotect par rapport à la manipulation de carte de partitions simultanées, il n’est pas un problème avec le schéma initial déploiement tooa nouvelle base de données qui a n’a ne pas encore été enregistré dans la carte de partitions hello et n’a ne pas encore été allouée toohold shardlets. Par conséquent, nous pouvons reposent sur les connexions de base de données normale pour cette scénarios, comme le routage dépendant des toodata exécutée.  

Cela conduit tooan approche où déploiement du schéma via les migrations EF est étroitement lié à l’inscription de hello de base de données hello comme une partition dans la carte de partitions de l’application hello. Il s’appuie sur hello suivant des conditions préalables : 

* base de données Hello a déjà été créé. 
* base de données Hello est vide - il conserve aucun schéma de l’utilisateur et aucune donnée de l’utilisateur.
* base de données Hello ne sont pas encore accessibles via les API du client de base de données élastique hello pour le routage dépendant des données. 

Avec ces conditions préalables en place, nous pouvons créer une expression régulière non ouvert **SqlConnection** tookick off migrations EF pour le déploiement de schéma. Hello suivant l’exemple de code illustre cette approche. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


Cet exemple montre la méthode hello **RegisterNewShard** que les registres hello partition dans la carte de partitions hello, déploie le schéma de hello via les migrations EF et stocke un mappage d’une partition toohello clé de partitionnement. Il s’appuie sur un constructeur de hello **DbContext** sous-classe (**ElasticScaleContext** dans l’exemple hello) qui accepte une chaîne de connexion SQL en tant qu’entrée. code Hello de ce constructeur est simple, comme hello suivant montre l’exemple : 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Un a peut-être utilisé version hello du constructeur hello héritée de la classe de base hello. Mais tooensure de besoins de code hello qui hello initialiseur par défaut pour EF est utilisé lors de la connexion. Par conséquent, hello détournement court dans la méthode statique hello avant l’appel du constructeur de classe de base hello avec la chaîne de connexion hello. Notez que l’inscription de hello de partitions doit s’exécuter dans un tooensure domaine ou le processus d’application différents paramètres initialiseur hello EF pas de conflit entre. 

## <a name="limitations"></a>Limites
les approches Hello décrites dans ce document entraînent quelques limitations : 

* Les applications qui utilisent EF **LocalDb** devez d’abord toomigrate tooa régulière de données SQL Server avant d’utiliser la bibliothèque cliente de base de données élastique. La montée en charge d’une application via le partitionnement avec l’infrastructure élastique n’est pas possible avec **LocalDb**. Notez que le développement peut toujours utiliser **LocalDb**. 
* N’importe quelle application toohello de modifications qui impliquent la modification de schéma de base de données devez toogo via des migrations EF sur toutes les partitions. exemple de code Hello pour ce document ne montre pas comment toodo cela. Envisagez d’utiliser la base de données de mise à jour avec un tooiterate de paramètre ConnectionString sur toutes les partitions ; ou extraction hello T-SQL script pour hello en attente de la migration à l’aide de la mise à jour à la base de données avec hello - option de Script et d’appliquer des partitions de tooyour script hello T-SQL.  
* Étant donné une demande, il est supposé que son traitement de base de données est contenue dans une même partition identifiée par la clé de partitionnement hello fournie par la demande de hello. Cependant, cette hypothèse n'est pas toujours vraie. Par exemple, quand il n’est pas possible de toomake une clé de partitionnement disponible. tooaddress, hello bibliothèque cliente fournit hello **MultiShardQuery** classe qui implémente une abstraction de la connexion pour l’interrogation sur plusieurs partitions. Apprentissage toouse hello **MultiShardQuery** en combinaison avec EF est abordée dans ce document hello

## <a name="conclusion"></a>Conclusion
Hello les étapes décrites dans ce document, EF permet aux applications la capacité de la bibliothèque cliente hello élastique de base de données pour les données dépendantes de routage par refactorisation des constructeurs de hello **DbContext** sous-classes utilisés Bonjour EF application. Cette limite hello les modifications requises toothose chaque endroit où **DbContext** classes existent déjà. En outre, les applications de EF peuvent continuer toobenefit de déploiement de schéma automatique en combinant les étapes hello qui appellent hello nécessaire EF migrations avec l’inscription du hello de nouvelles partitions et des mappages dans la carte de partitions hello. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
