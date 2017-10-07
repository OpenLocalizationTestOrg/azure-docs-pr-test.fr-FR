---
title: "bibliothèque cliente de base de données élastique aaaUsing avec Dapper | Documents Microsoft"
description: "Utilisation de la bibliothèque cliente de la base de données élastique avec Dapper."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Utilisation de la bibliothèque cliente de la base de données élastique avec Dapper
Ce document est destiné aux développeurs qui s’appuient sur les applications toobuild Dapper, mais aussi tooembrace [outils de base de données élastique](sql-database-elastic-scale-introduction.md) toocreate applications qui implémentent partitionnement tooscale-hors de leur couche données.  Ce document illustre les modifications hello dans les applications Dapper qui sont nécessaire toointegrate avec les outils de base de données élastique. Notre le focus est sur la composition de gestion de partition de base de données élastique hello et dépendant des données de l’acheminement avec Dapper. 

**Exemple de code**: [outils de base de données élastique pour l’intégration de la base de données SQL Azure avec Dapper](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

Intégration **Dapper** et **DapperExtensions** avec hello bibliothèque cliente de base de données élastique pour base de données SQL Azure est facile. Les applications peuvent utiliser les données dépendantes de routage par la modification de la création de hello et l’ouverture des nouveaux [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello de toouse objets [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) appeler à partir de hello [client bibliothèque](http://msdn.microsoft.com/library/azure/dn765902.aspx). Cela limite les modifications dans votre tooonly application où les nouvelles connexions sont créées et ouvert. 

## <a name="dapper-overview"></a>Vue d’ensemble de Dapper
**Dapper** est un mappeur relationnel objet. Il mappe des objets .NET à partir de votre base de données relationnelle tooa application (et vice versa). première partie de Hello hello exemple de code illustre comment vous pouvez intégrer la bibliothèque cliente de base de données élastique hello avec les applications Dapper. deuxième partie de Hello hello exemple de code illustre comment toointegrate lorsque vous utilisez Dapper et DapperExtensions.  

fonctionnalité du Mappeur Hello dans Dapper fournit des méthodes d’extension sur les connexions de base de données qui simplifient l’envoi instructions T-SQL pour l’exécution ou l’interrogation de la base de données hello. Par exemple, Dapper permet de facilement toomap entre vos objets .NET et les paramètres hello des instructions SQL pour **Execute** appels ou résultats de hello tooconsume de vos requêtes SQL en objets .NET à l’aide de **requête**appels à partir de Dapper. 

Lorsque vous utilisez DapperExtensions, vous n’avez plus besoin des instructions SQL tooprovide hello. Méthodes d’extension comme **GetList** ou **insérer** via une connexion de base de données hello créer hello instructions SQL coulisses hello.

Un autre avantage de Dapper et DapperExtensions est que les contrôles de l’application hello hello la création d’une connexion de base de données hello. Cela permet d’interagir avec la bibliothèque cliente de base de données élastique hello qui courtiers selon le mappage hello de shardlets toodatabases de connexions de base de données.

assemblys de Dapper hello tooget, consultez [Dapper point net](http://www.nuget.org/packages/Dapper/). Pour les extensions Dapper hello, consultez [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Un coup de œil rapide à la bibliothèque cliente de base de données élastique hello
Avec la bibliothèque cliente de base de données élastique hello, définissez les partitions de vos données d’application appelées *shardlets* , mapper les toodatabases et les identifier par *clés de partitionnement*. Vous pouvez avoir autant de bases de données que nécessaire et distribuer vos shardlets sur ces bases de données. mappage Hello des bases de données de partitionnement les valeurs de clé toohello est stockée par une carte de partitions fournie par l’API de la bibliothèque hello. Cette fonctionnalité s’appelle la **gestion des cartes de partitions**. carte de partitions Hello sert également de broker hello de connexions de base de données pour les requêtes qui comportent une clé de partitionnement. Cette fonctionnalité est désignée tooas **routage dépendant des données**.

![Cartes de partitions et routage dépendant des données][1]

Gestionnaire de cartes de partitions Hello protège les utilisateurs à partir des vues incohérentes dans les données de shardlet qui peuvent se produire lorsque les opérations de gestion de shardlet simultanées sont produisent sur les bases de données hello. toodo hello par conséquent, les connexions de base de données partition maps broker hello pour une application générée avec la bibliothèque de hello. Lorsque les opérations de gestion de partitions peut affecter les shardlets hello, ainsi, kill de hello partition carte fonctionnalité tooautomatically une connexion de base de données. 

Au lieu d’utiliser des connexions de toocreate méthode traditionnelle hello pour Dapper, nous devons toouse hello [OpenConnectionForKey méthode](http://msdn.microsoft.com/library/azure/dn824099.aspx). Cela garantit que tous les hello la validation a lieu et les connexions sont gérées correctement quand les données sont déplacées entre les partitions.

### <a name="requirements-for-dapper-integration"></a>Configuration requise pour l’intégration Dapper
Lorsque vous travaillez avec la bibliothèque cliente de base de données élastique hello et hello API Dapper, nous souhaitons hello tooretain propriétés suivantes :

* **Montée en puissance parallèle**: nous souhaitez tooadd ou supprimer des bases de données de la couche de données hello d’application partitionnée hello en fonction des besoins de capacité hello de l’application hello. 
* **Cohérence**: notre application est à l’échelle à l’aide de partitionnement, nous avons besoin de routage dépendant des données tooperform. Par conséquent, nous souhaitons toouse hello données dépendantes capacités de routage de hello bibliothèque toodo. En particulier, nous la validation tooretain hello et cohérence garantie fournie par les connexions qui sont réparties via le Gestionnaire de carte de partitions hello altération de tooavoid de commande ou les résultats de requête incorrect. Cela garantit que tooa connexions étant donné les shardlets sont rejetés ou arrêtée si (par exemple) hello shardlet tooa actuellement déplacé d’une autre partition à l’aide des API de fractionnement/fusion.
* **Mappage d’objet**: nous souhaitons tooretain hello offerts par les mappages hello fournie par Dapper tootranslate entre les classes dans l’application hello et hello sous-jacent des structures de base de données. 

Hello section suivante fournit des conseils pour cette configuration requise pour les applications basées sur **Dapper** et **DapperExtensions**.

## <a name="technical-guidance"></a>Conseils techniques
### <a name="data-dependent-routing-with-dapper"></a>Routage dépendant des données avec Dapper
Avec Dapper, l’application hello est généralement responsable de la création et l’ouverture toohello de connexions hello sous-jacent de base de données. Étant donné un type T à l’application hello, Dapper renvoie les résultats de la requête en collections .NET de type T. Dapper effectue le mappage de hello de hello T-SQL résultat lignes toohello objets de type T. De même, Dapper mappe des objets .NET en valeurs SQL ou des paramètres pour les instructions data manipulation language (DML). Dapper offre cette fonctionnalité via les méthodes d’extension sur hello régulière [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objet à partir de bibliothèques de ADO .NET SQL Client hello. Hello connexion SQL retournée par hello API infrastructure élastique pour DDR sont également régulière [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objets. Cela nous permet toodirectly utilisent des extensions de Dapper sur le type hello retourné par DDR API la bibliothèque cliente de hello, car il s’agit également d’une connexion SQL Client simple.

Ces observations rendent connexions toouse simple demandées par la bibliothèque cliente de base de données élastique hello pour Dapper.

Cet exemple de code (à partir de hello exemple d’accompagnement) illustre l’approche hello où clé de partitionnement hello est fournie par hello application toohello bibliothèque toobroker hello connexion toohello droite partitions.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

Hello appel toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API remplace la création par défaut de hello et à l’ouverture d’une connexion SQL Client. Hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) appel prend des arguments de hello qui sont requis pour le routage dépendant des données : 

* tooaccess de carte de partitions Hello hello interfaces de routage dépendant de données
* Hello partitionnement tooidentify clé hello shardlet
* partition de toohello tooconnect Hello les informations d’identification (nom d’utilisateur et mot de passe)

objet de mappage de partitions Hello crée une partition de toohello de connexion qui contient le shardlet hello pour hello étant donné la clé de partitionnement. API du client de base de données élastique Hello également baliser hello tooimplement de connexion sa cohérence garantit. Depuis hello appeler trop[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) retourne un objet de connexion SQL Client normal, les hello appeler toohello **Execute** méthode d’extension à partir de Dapper suit hello Dapper standard pratique.

Requêtes travail hello très même façon - vous ouvrez d’abord à l’aide de connexion hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) à partir de l’API du client hello. Puis vous utilisez hello régulière extension Dapper méthodes toomap hello résultats de votre requête SQL en objets .NET :

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

Notez que hello **à l’aide de** bloquer des étendues de connexion hello DDR toutes les opérations de base de données dans une seule partition hello bloc toohello où tenantId1 est conservé. requête de Hello retourne uniquement les blogs stockés sur la partition actuelle de hello, mais pas hello ceux qui sont stockés sur toutes les autres partitions. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Routage dépendant des données avec Dapper et DapperExtensions
Dapper est fourni avec un écosystème d’extensions supplémentaires qui peut fournir plus de commodité et d’abstraction de base de données hello lors du développement d’applications de base de données. DapperExtensions est un exemple. 

L’utilisation de DapperExtensions dans votre application ne change pas la gestion ni la création des connexions de base de données. Il est toujours responsabilité tooopen connexions l’application hello et les objets de connexion SQL Client régulières sont attendus par les méthodes d’extension hello. Nous pouvons s’appuient sur hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) comme indiqué ci-dessus. En tant que hello exemples de code suivants affichent, hello seule différence est que les instructions T-SQL de hello toowrite ne ne plus avoir :

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

Et Voici des exemples de code hello pour la requête de hello : 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>Gestion des erreurs temporaires
Hello Microsoft Patterns & Practices équipe hello publiée [bloc applicatif de pannes gestion](http://msdn.microsoft.com/library/hh680934.aspx) les développeurs d’applications toohelp atténuer les conditions courantes d’erreurs transitoires rencontrées lors de l’exécution dans le cloud de hello. Pour plus d’informations, consultez [Perseverance, le Secret de toutes les luttes : à l’aide de hello bloc applicatif de pannes gestion](http://msdn.microsoft.com/library/dn440719.aspx).

exemple de code Hello s’appuie sur hello erreurs transitoires bibliothèque tooprotect contre les erreurs transitoires. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** Bonjour code ci-dessus est défini comme un **SqlDatabaseTransientErrorDetectionStrategy** avec un nombre de tentatives de 10 et 5 secondes délai entre deux tentatives. Si vous utilisez des transactions, assurez-vous que vos objectifs de nouvelle tentative repasse toohello début de la transaction hello dans les cas de hello d’une erreur temporaire.

## <a name="limitations"></a>Limites
les approches Hello décrites dans ce document entraînent quelques limitations :

* exemple de code Hello pour ce document ne montre pas comment schéma toomanage entre les partitions.
* Étant donné une demande, nous partons du principe que tous les traitements de sa base de données sont contenue dans une même partition identifiée par la clé de partitionnement hello fournie par la demande de hello. Toutefois, cette hypothèse ne pas toujours maintenir, par exemple, lorsqu’il n’est pas possible de toomake une clé de partitionnement disponible. tooaddress, hello bibliothèque cliente de base de données élastique inclut hello [MultiShardQuery classe](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). classe Hello implémente une abstraction de la connexion pour l’interrogation sur plusieurs partitions. L’utilisation de MultiShardQuery en association avec Dapper est abordée dans ce document hello.

## <a name="conclusion"></a>Conclusion
Les applications utilisant Dapper et DapperExtensions peuvent facilement tirer parti des outils de la base de données élastique pour la base de données SQL Azure. Hello les étapes décrites dans ce document, ces applications peuvent utiliser la fonctionnalité de l’outil hello pour les données dépendantes de routage par la modification de la création de hello et l’ouverture des nouveaux [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello de toouse objets [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) appel d’une bibliothèque cliente de base de données élastique hello. Cela limite les emplacements de toothose requis de modifications hello application où les nouvelles connexions sont créées et ouvert. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
