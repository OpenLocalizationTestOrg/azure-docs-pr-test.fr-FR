---
title: "Utilisation de la bibliothèque cliente de la base de données élastique avec Dapper | Microsoft Docs"
description: "Utilisation de la bibliothèque cliente de la base de données élastique avec Dapper."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c258b1859e14d9783a3dfa75431b69bef4d640fd
ms.sourcegitcommit: dfd49613fce4ce917e844d205c85359ff093bb9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Utilisation de la bibliothèque cliente de la base de données élastique avec Dapper
Ce document est destiné aux développeurs qui utilisent Dapper pour générer des applications, mais veulent également adopter les [outils de base de données élastique](sql-database-elastic-scale-introduction.md) pour créer des applications implémentant le partitionnement pour la montée en puissance parallèle de la couche Données.  Ce document présente les modifications devant être appliquées aux applications basées sur Dapper pour intégrer des outils de base de données élastique. Nous nous concentrerons sur la composition de la gestion de partition de base de données élastique et du routage dépendant des données avec Dapper. 

**Exemple de code**: [outils de base de données élastique pour l’intégration de la base de données SQL Azure avec Dapper](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

L’intégration de **Dapper** et de **DapperExtensions** avec la bibliothèque cliente de la base de données élastique pour la base de données SQL Azure est simple. Les applications peuvent utiliser le routage dépendant des données en modifiant la création et l’ouverture de nouveaux objets [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) pour utiliser l’appel [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) à partir de la [bibliothèque cliente](http://msdn.microsoft.com/library/azure/dn765902.aspx). Cela limite les modifications au sein de votre application à la création et l’ouverture de nouvelles connexions uniquement. 

## <a name="dapper-overview"></a>Vue d’ensemble de Dapper
**Dapper** est un mappeur relationnel objet. Il mappe les objets .NET de votre application à une base de données relationnelle (et inversement). La première partie de l’exemple de code illustre comment vous pouvez intégrer la bibliothèque client de base de données élastique avec les applications Dapper. La deuxième partie de l’exemple de code illustre comment effectuer l’intégration lors de l’utilisation de Dapper et de DapperExtensions.  

La fonctionnalité de mappeur de Dapper fournit des méthodes d’extension sur les connexions de base de données qui simplifient la soumission d’instructions T-SQL pour l’exécution ou l’interrogation de la base de données. Par exemple, Dapper facilite le mappage entre vos objets .NET et les paramètres des instructions SQL pour les appels **Execute**, ou pour utiliser les résultats de vos requêtes SQL dans des objets .NET à l’aide des appels **Query** de Dapper. 

Lorsque vous utilisez DapperExtensions, vous n’avez plus besoin de fournir les instructions SQL. Les méthodes d’extensions telles que **GetList** ou **Insert** sur la connexion de base de données créent les instructions SQL en arrière-plan.

Un autre avantage de Dapper et de DapperExtensions est que l’application contrôle la création de la connexion de base de données. Cela permet d’interagir avec la bibliothèque cliente de la base de données élastique qui alloue les connexions de base de données en fonction du mappage de shardlets aux bases de données.

Pour obtenir les assemblys Dapper, consultez [Dapper point net](http://www.nuget.org/packages/Dapper/). Pour les extensions Dapper, consultez [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-the-elastic-database-client-library"></a>Un coup de œil rapide à la bibliothèque cliente de la base de données élastique
Avec la bibliothèque cliente de la base de données élastique, vous définissez les partitions de vos données d’application appelées *shardlets*, vous les mappez à des bases de données et les identifier à l’aide de *clés de partitionnement*. Vous pouvez avoir autant de bases de données que nécessaire et distribuer vos shardlets sur ces bases de données. Le mappage des valeurs de clé de partitionnement vers les bases de données est stocké par une carte de partitions fournie par les API de la bibliothèque. Cette fonctionnalité s’appelle la **gestion des cartes de partitions**. La carte de partitions sert également de service Broker de connexion de base de données pour les demandes transportant une clé de partitionnement. Cette fonctionnalité s’appelle le **routage dépendant des données**.

![Cartes de partitions et routage dépendant des données][1]

Le gestionnaire des cartes de partitions empêche tout affichage incohérent des données shardlet pouvant perturber les utilisateurs lors des opérations de gestion de shardlet simultanées dans les bases de données. Pour ce faire, la partition mappe dans le service Broker les connexions de base de données pour une application construite avec la bibliothèque. Cela permet à la fonctionnalité de mappage de partition d’arrêter automatiquement une connexion de base de données lorsque les opérations de gestion de partition peuvent affecter le shardlet. 

Plutôt que d’utiliser la méthode traditionnelle de création des connexions pour Dapper, vous devez utiliser la méthode [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn824099.aspx). Cela garantit que toutes les validations ont lieu et que les connexions sont gérées correctement lors du déplacement de données entre les partitions.

### <a name="requirements-for-dapper-integration"></a>Configuration requise pour l’intégration Dapper
Durant l’utilisation des API de la bibliothèque cliente de la base de données élastique et de Dapper, vous souhaitez conserver les propriétés suivantes :

* **Montée en puissance parallèle** : vous souhaitez ajouter ou supprimer des bases de données de la couche Données de l’application partitionnée si nécessaire pour les demandes de capacité de l’application. 
* **Cohérence** : étant donné que l’application est redimensionnée à l’aide du partitionnement, vous devez utiliser le routage dépendant des données. Pour ce faire, vous souhaitez utiliser les fonctionnalités de routage dépendant des données de la bibliothèque. En particulier, vous souhaitez conserver les garanties de validation et de cohérence fournies par les connexions réparties via le Gestionnaire de carte de partition afin d’éviter une corruption ou des résultats de requête incorrects. Cela garantit que les connexions à un shardlet donné sont rejetées ou arrêtées si (par exemple) le shardlet est en cours de déplacement vers une partition différente à l’aide des API de fractionnement et de fusion.
* **Mappage d’objets**: nous souhaitons conserver la commodité des mappages fournis par Dapper pour la traduction entre les classes dans l’application et les structures de base de données sous-jacentes. 

La section suivante fournit des instructions relatives aux exigences pour les applications basées sur **Dapper** et **DapperExtensions**.

## <a name="technical-guidance"></a>Conseils techniques
### <a name="data-dependent-routing-with-dapper"></a>Routage dépendant des données avec Dapper
Avec Dapper, l’application est généralement responsable de la création et de l’ouverture des connexions à la base de données sous-jacente. Après avoir reçu un type T de l’application, Dapper renvoie les résultats de la requête sous forme de collections .NET de type T. Dapper effectue le mappage des lignes de résultat T-SQL aux objets de type T. De même, Dapper mappe les objets .NET en valeurs SQL ou en paramètres pour les instructions de langage de manipulation de données. Dapper offre cette fonctionnalité via les méthodes d’extension sur l’objet [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) ordinaire à partir des bibliothèques clientes ADO .NET SQL. La connexion SQL renvoyée par les API d’infrastructure élastique pour les DDR présente également des objets [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) ordinaires. Cela permet d’utiliser directement des extensions Dapper sur le type retourné par l’API DDR de la bibliothèque cliente, étant donné que c’est également une connexion SQL Client simple.

Ces observations simplifient l’utilisation des connexions réparties par la bibliothèque cliente de la base de données élastique pour Dapper.

Cet exemple de code (de l’exemple qui accompagne cet article) illustre l’approche où la clé de partitionnement est fournie par l’application à la bibliothèque pour attribuer la connexion à la partition appropriée.   

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

L’appel à l’API [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) remplace la création et l’ouverture par défaut d’une connexion SQL Client. L’appel [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) accepte les arguments qui sont requis pour le routage dépendant des données : 

* la carte de partitions pour accéder aux interfaces de routage dépendant des données,
* la clé de partition pour identifier le shardlet,
* les informations d’identification (nom d’utilisateur et mot de passe) pour se connecter à la partition

L’objet de carte de partitions crée une connexion ouverte vers la partition hébergeant le shardlet pour la clé de partitionnement donnée. Les API du client de base de données élastique marquent également la connexion pour implémenter ses garanties de cohérence. Étant donné que l’appel à [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) retourne un objet de connexion SQL Client normal, l’appel suivant à la méthode d’extension **Execute** à partir de Dapper suit la pratique Dapper standard.

Les requêtes fonctionnent de la même façon : une première ouverture de la connexion a lieu à l’aide de [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) de l’API du client. Vous utilisez ensuite les méthodes d’extension Dapper ordinaires pour mapper les résultats de votre requête SQL dans des objets .NET :

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

Notez que le bloc **using** avec la connexion DDR définit l’étendue de toutes les opérations de base de données dans le bloc à la seule partition où tenantId1 est conservé. La requête retourne uniquement les blogs stockés sur la partition actuelle et non ceux stockés sur les autres partitions. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Routage dépendant des données avec Dapper et DapperExtensions
Dapper est fourni avec un écosystème d’extensions supplémentaires qui peuvent fournir plus de commodité et d’abstraction à partir de la base de données lors du développement d’applications de base de données. DapperExtensions est un exemple. 

L’utilisation de DapperExtensions dans votre application ne change pas la gestion ni la création des connexions de base de données. Il incombe toujours à l’application d’ouvrir des connexions et les méthodes d’extension attendent des objets de connexion SQL Client ordinaires. Nous pouvons utiliser [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) comme indiqué ci-dessus. Les exemples de code suivants montrent que la seule différence est que vous n’avez plus à écrire les instructions T-SQL :

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

Voici l’exemple de code pour la requête : 

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
L’équipe Microsoft Patterns & Practices a publié le [bloc d’applications de gestion des erreurs temporaires](http://msdn.microsoft.com/library/hh680934.aspx) afin d’aider les développeurs d’applications à atténuer les erreurs transitoires courantes rencontrées lors de l’exécution dans le cloud. Pour plus d’informations, consultez [La persévérance, le secret de la réussite : utilisation du bloc applicatif de gestion des erreurs temporaires](http://msdn.microsoft.com/library/dn440719.aspx).

L’exemple de code s’appuie sur la bibliothèque d’erreurs transitoires pour vous protéger contre les défaillances temporaires. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** du code ci-dessus est définie comme une **SqlDatabaseTransientErrorDetectionStrategy** avec un nombre de tentatives de 10 et un délai d’attente de 5 secondes entre chaque tentative. Si vous utilisez des transactions, assurez-vous que la portée de votre nouvelle tentative revient au début de la transaction en cas d’erreur transitoire.

## <a name="limitations"></a>Limitations
Les approches décrites dans ce document entraînent quelques limitations :

* L’exemple de code pour ce document ne montre pas comment gérer le schéma entre les partitions.
* Nous partons du principe que tous les traitements de base de données d’une demande donnée sont contenus dans une seule partition, identifiée par la clé de partitionnement fournie par la demande. Cependant, cette hypothèse n’est pas toujours valide, par exemple, lorsqu’il n’est pas possible de rendre une clé de partitionnement disponible. Pour résoudre ce problème, la bibliothèque cliente  de base de données élastique inclut la [classe MultiShardQuery](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). La classe implémente une abstraction de la connexion pour l’interrogation sur plusieurs partitions. Ce document ne permet pas d’apprendre à utiliser la MultiShardQuery conjointement à Dapper.

## <a name="conclusion"></a>Conclusion
Les applications utilisant Dapper et DapperExtensions peuvent facilement tirer parti des outils de la base de données élastique pour la base de données SQL Azure. À travers les étapes décrites dans ce document, ces applications peuvent utiliser la capacité d’outil pour le routage dépendant des données en modifiant la création et l’ouverture de nouveaux objets [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) pour utiliser l’appel [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) de la bibliothèque cliente de la base de données élastique. Cela limite les modifications au sein de votre application aux endroits où de nouvelles connexions sont créées et ouvertes. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
