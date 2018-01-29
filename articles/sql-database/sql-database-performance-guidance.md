---
title: "Directives pour l’optimisation des performances Azure SQL Database | Microsoft Docs"
description: "Découvrez l’utilisation des recommandations pour améliorer le niveau de performance des requêtes Azure SQL Database."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: On Demand
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 5dc245a29a9106156c207ed7394f8bb289db729e
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Optimisation des performances dans Azure SQL Database

Azure SQL Database fournit des [recommandations](sql-database-advisor.md) que vous pouvez utiliser pour améliorer les performances de votre base de données, ou vous pouvez laisser Azure SQL Database [s’adapter automatiquement à votre application](sql-database-automatic-tuning.md) et appliquer les modifications qui amélioreront les performances de votre charge de travail.

Si aucune recommandation n’est applicable et si vous avez toujours des problèmes de performances, vous pouvez utiliser les méthodes suivantes pour améliorer les performances :
1. Augmentez les [niveaux de service](sql-database-service-tiers.md) et apportez davantage de ressources à votre base de données.
2. Paramétrez votre application et appliquez quelques meilleures pratiques susceptibles d’améliorer les performances. 
3. Paramétrez la base de données en modifiant les index et les requêtes afin d’utiliser plus efficacement les données.

Ce sont des méthodes manuelles, car vous devez déterminer quels [niveaux de service](sql-database-service-tiers.md) vous devez choisir ou vous sont indispensables pour réécrire le code de l’application ou de la base de données et déployer les changements.

## <a name="increasing-performance-tier-of-your-database"></a>Augmentation du niveau de performance de votre base de données

Azure SQL Database propose quatre [niveaux de service](sql-database-service-tiers.md) : De base, Standard, Premium et Premium RS. Les performances sont mesurées en unités de débit de base de données, ou [DTU](sql-database-what-is-a-dtu.md). Chaque niveau de service isole strictement les ressources pouvant être utilisées par votre base de données SQL et garantit des performances prévisibles. Dans cet article, nous vous offrons des recommandations qui vous aideront à choisir le niveau de service adapté à votre application. Nous abordons également des modes de paramétrage de votre application destinés à tirer le meilleur de Microsoft Azure SQL Database.

> [!NOTE]
> Cet article se concentre sur les recommandations de performances pour les bases de données uniques dans Microsoft Azure SQL Database. Pour un guide des performances relatives aux pools élastiques, consultez [Considérations sur les prix et performances pour les pools élastiques](sql-database-elastic-pool-guidance.md). Notez, cependant, que vous pouvez appliquer un grand nombre des recommandations de cet article sur les bases de données d’un pool élastique, afin d’obtenir des avantages similaires en matière de performances.
> 

* **De base** : le niveau de service De base est conçu de manière à assurer une bonne prévisibilité des performances pour chaque base de données, heure après heure. Dans une base de données De base, des ressources suffisantes prennent en charge de bonnes performances au sein d’une petite instance qui ne présente pas plusieurs requêtes simultanées. Voici quelques cas d’usage classiques pour lesquels vous devez utiliser le niveau de service De base :
  * **Vous débutez juste avec Azure SQL Database**. Bien souvent, les applications en cours de développement ne requièrent pas de hauts niveaux de performances. Les bases de données De base constituent un environnement idéal pour le développement ou le test des bases de données, et ce, à moindre coût.
  * **Vous disposez d’une base de données avec un utilisateur unique**. Généralement, les applications qui associent un seul utilisateur à une base de données n’ont pas des exigences élevées en matière d’accès concurrentiel et de performances. Les applications de ce type font des candidates idéales pour le niveau de service De base.
* **Standard** : le niveau de service Standard offre une meilleure prévisibilité des performances et fournit de bonnes performances pour les bases de données avec plusieurs requêtes simultanées, par exemple les applications web ou de groupe de travail. Lorsque vous choisissez une base de données de niveau de service Standard, vous pouvez dimensionner votre application de base de données en fonction de performances prévisibles, minute après minute.
  * **Votre base de données présente de multiples requêtes simultanées**. Les applications utilisées simultanément par plusieurs utilisateurs requièrent généralement des niveaux de performances plus élevés. Par exemple, un groupe de travail ou des applications web avec des exigences de trafic d’E/S faibles à moyennes et prenant en charge plusieurs requêtes simultanées sont parfaitement adaptés au niveau de service Standard.
* **Premium** : le niveau de service Premium offre des performances prévisibles seconde après seconde pour chaque base de données Premium. Lorsque vous choisissez le niveau de service Premium, vous pouvez dimensionner votre application de base de données en fonction de la charge maximale de votre instance. Le plan supprime les scénarios dans lesquels l’écart de performances peut allonger le traitement des petites requêtes dans les opérations sensibles à la latence. Ce modèle simplifie considérablement les cycles de validation de développement et de produit nécessaires pour les applications qui doivent appliquer des instructions fortes concernant les besoins maximum en ressources, l’écart de performances ou la latence des requêtes. La plupart des cas d’utilisation du niveau de service Premium présentent une ou plusieurs de ces caractéristiques :
  * **Pic de charge élevés**. Une application qui nécessite un volume élevé d’UC, de mémoire ou d’entrée/sortie (E/S) pour exécuter ses opérations requiert un niveau de performances élevé, dédié. Par exemple, si une opération de base de données est connue pour utiliser plusieurs cœurs d’UC pendant une période prolongée, l’utilisation du niveau de service Premium est appropriée.
  * **Plusieurs requêtes simultanées**. Certaines applications de base de données gèrent de nombreuses demandes simultanées, par exemple un site web avec un volume de trafic élevé. Les niveaux de service De base et Standard présentent des limites au nombre de demandes simultanées par base de données. Les applications qui requièrent plus de connexions doivent choisir une taille de réservation appropriée pour traiter le nombre maximum de demandes nécessaires.
  * **Latence faible**. Certaines applications doivent garantir une réponse de la base de données dans un délai minimum. Si une procédure stockée donnée est appelée dans le cadre d’une opération client plus large, il existe peut-être une exigence de renvoi depuis l’appel en moins de 20 millisecondes 99 % du temps. Ce type d’application bénéficie du niveau de service Premium afin de garantir la disponibilité de la puissance de calcul.
* **Premium RS** : le niveau Premium RS est conçu pour les charges de travail intensives en E/S qui ne nécessitent pas de garanties de disponibilité maximale. Parmi les exemples, on peut citer les charges de travail hautes performances ou une charge de travail analytique où la base de données n’est pas le système d’enregistrement.

Le niveau exact dont vous avez besoin pour votre base de données SQL dépend des exigences de charge maximale pour chaque dimension de ressource. Certaines applications utilisent une quantité insignifiante pour une ressource mais ont des exigences considérables pour d’autres.

### <a name="service-tier-capabilities-and-limits"></a>Capacités et limites des niveaux de service

À chaque niveau de service, vous définissez le niveau de performances et disposer ainsi de la possibilité de payer uniquement la capacité nécessaire. Vous pouvez [ajuster la capacité](sql-database-service-tiers.md), en l’augmentant ou en la diminuant, en fonction de l’évolution de la charge de travail. Par exemple, si la charge de travail de votre base de données est élevée au cours de la période des achats de rentrée scolaire, vous pouvez augmenter le niveau de performances pour une durée définie, par exemple entre juillet et septembre. Il est ensuite possible de le réduire à la fin de la période chargée. Vous pouvez réduire vos coûts en optimisant votre environnement cloud conformément aux caractéristiques saisonnières de votre entreprise. Ce modèle fonctionne également bien pour les cycles de version de logiciels. Une équipe de test peut allouer de la capacité pendant des séries de test, et libérer cette capacité une fois les tests terminés. Dans un modèle de requête de capacité, vous payez uniquement la capacité nécessaire, en évitant de financer des ressources dédiées que vous n’utiliseriez que rarement.

### <a name="why-service-tiers"></a>Pourquoi des niveaux de service ?
Bien que la charge de travail de chaque base de données puisse différer, les niveaux de service visent à assurer la prévisibilité des performances dans un large éventail de niveaux de performances. Les clients présentant des exigences d’envergure en matière de ressources de bases de données peuvent opérer dans un environnement informatique davantage dédié.

## <a name="tune-your-application"></a>Paramétrer votre application
Dans un SQL Server local traditionnel, le processus de planification de la capacité initiale est souvent séparé du processus d’exécution d’une application en production. Le matériel et les licences de produit sont achetés dans un premier temps, tandis que le paramétrage des performances est exécuté ultérieurement. Lorsque vous utilisez Microsoft Azure SQL Database, il est judicieux d’imbriquer le processus d’exécution d’une application, puis de le paramétrer. Avec le modèle de paiement de la capacité à la demande, vous pouvez paramétrer votre application pour utiliser les ressources minimales requises immédiatement, au lieu de surprovisionner massivement du matériel en vous appuyant sur des hypothèses de plans de croissance à venir pour une application (qui sont souvent incorrectes). Certains clients peuvent décider de ne pas paramétrer une application et choisir à la place de surprovisionner des ressources matérielles. Cette approche peut s’avérer utile si vous ne souhaitez pas modifier une application clé pendant une période d’activité. Cependant, le paramétrage d’une application peut réduire vos besoins en ressources et diminuer vos factures mensuelles lorsque vous utilisez les niveaux de service dans Azure SQL Database.

### <a name="application-characteristics"></a>Caractéristiques des applications
Bien que les niveaux de service Azure SQL Database soient conçus pour améliorer la stabilité et la prévisibilité des performances d’une application, il existe quelques meilleures pratiques à mettre à profit pour le paramétrage de votre application afin de mieux tirer parti des ressources d’un niveau de performances. Bien que de nombreuses applications gagnent considérablement en performances en passant simplement à un niveau de performances et/ou de service supérieur, certaines d’entre elles nécessitant un paramétrage supplémentaire pour bénéficier de ces avantages. Pour améliorer les performances, envisagez de procéder à un paramétrage supplémentaire sur les applications présentant ces caractéristiques :

* **Les applications dont les performances sont lentes en raison d’un comportement bavard**. Les applications qui se caractérisent par un comportement bavard effectuent trop d’opérations d’accès aux données qui sont sensibles à la latence du réseau. Il vous faudra éventuellement modifier ces types d’applications pour réduire le nombre d’opérations d’accès aux données de la base de données SQL. Par exemple, vous pouvez améliorer les performances applicatives à l’aide de techniques comme le traitement par lot des requêtes ou le déplacement de requêtes vers les procédures stockées. Pour plus d’informations, consultez la section [Traitement par lot des requêtes](#batch-queries).
* **Bases de données présentant une charge de travail intensive ne pouvant pas être prise en charge par un seul ordinateur**. Les bases de données qui dépassent le quota de ressources du niveau supérieur de performance Premium peuvent profiter de la montée en charge de votre charge de travail. Pour plus d’informations, consultez les sections [Partitionnement entre plusieurs bases de données](#cross-database-sharding) et [Partitionnement fonctionnel](#functional-partitioning).
* **Applications présentant des requêtes non optimales**. Les applications, en particulier celles de la couche d’accès aux données, qui présentant des requêtes mal paramétrées peuvent ne pas tirer parti d’un niveau de performance supérieur. Cela inclut les requêtes dépourvues d’une clause WHERE et les requêtes présentant des index manquants ou des statistiques obsolètes. Ces applications bénéficient des techniques de paramétrage des performances de requête standard. For more information, consultez les sections [Index manquants](#identifying-and-adding-missing-indexes) et [Paramétrage/Compréhension de requêtes](#query-tuning-and-hinting).
* **Les applications dotées d’un accès aux données non optimal**. Les applications qui rencontrent des problèmes inhérents de concurrence d’accès aux données, par exemple d’interblocage, peuvent ne pas tirer parti d’un niveau de performances supérieur. Envisagez de réduire les boucles sur l’instance Microsoft Azure SQL Database en mettant en cache des données côté client à l’aide du service Azure Caching ou d’autres technologies de mise en cache. Consultez la section [Mise en cache de la couche Application](#application-tier-caching).

## <a name="tune-your-database"></a>Optimiser votre base de données
Cette section explique certaines techniques que vous pouvez utiliser pour paramétrer Azure SQL Database afin d’obtenir les meilleures performances de votre application et d’être en mesure d’exécuter le plus petit niveau de performances possible. Plusieurs de ces techniques correspondent aux meilleures pratiques de paramétrage SQL Server traditionnelles, mais certaines sont spécifiques à Azure SQL Database. Dans certains cas, vous pouvez examiner les ressources utilisées par une base de données afin de déterminer des zones à paramétrer davantage et d’étendre les techniques traditionnelles SQL Server afin qu’elles fonctionnent dans Azure SQL Database.

### <a name="identify-performance-issues-using-azure-portal"></a>Identifier les problèmes de performances à l’aide du portail Azure
Les outils suivants du portail Azure peuvent vous aider à analyser et à corriger les problèmes de performances de votre base de données SQL :

* [Query Performance Insight](sql-database-query-performance.md)
* [SQL Database Advisor](sql-database-advisor.md)

Le portail Azure comporte davantage d’informations sur ces deux outils et sur les méthodes d’utilisation correspondantes. Pour diagnostiquer et corriger efficacement les problèmes, nous vous recommandons d’essayer dans un premier temps les outils dans le portail Azure. Nous vous recommandons d’utiliser les approches de paramétrage manuel évoquées plus bas, relatives aux index manquants et au paramétrage des requêtes, dans des cas particuliers.

Découvrez plus d’informations sur l’identification des problèmes dans Azure SQL Database dans l’article [Analyse des performances](sql-database-single-database-monitor.md).

### <a name="identifying-and-adding-missing-indexes"></a>Identification et ajout d’index manquants
Un problème courant dans les performances de base de données OLTP est la conception physique de la base de données. Souvent, les schémas de base de données sont conçus et livrés sans test de mise à l’échelle (en charge ou en volume de données). Malheureusement, les performances d’un plan de requête peuvent être acceptables à petite échelle mais se dégrader notablement avec des volumes de données au niveau de la production. La cause la plus courante de ce problème est l’absence d’index appropriés pour satisfaire des filtres ou d’autres restrictions dans une requête. Souvent, cela se manifeste comme une analyse de table là où une recherche d’index pourrait suffire.

Dans cet exemple, le plan de requête sélectionné utilise une analyse là où une recherche suffirait :

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![Un plan de requête avec index manquants](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Azure SQL Database peut vous aider à rechercher et à corriger les conditions communes d’index manquants. Les vues de gestion dynamique intégrées à Microsoft Azure SQL Database analysent les compilations de requêtes dans lesquelles un index réduirait considérablement le coût estimé d’exécution d’une requête. Pendant l’exécution de requêtes, SQL Database suit la fréquence selon laquelle chaque plan de requête est exécuté, ainsi que l’écart estimé entre le plan de requête en cours d’exécution et le plan imaginé dans lequel cet index existait. Ces vues de gestion dynamique vous permettent d’identifier rapidement les modifications de conception physique de la base de données susceptibles d’améliorer le coût total de la charge de travail pour une base de données et sa charge de travail réelle.

Vous pouvez utiliser cette requête pour évaluer les index manquants potentiels :

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

Dans cet exemple, la requête a entraîné cette suggestion :

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Après sa création, cette même instruction SELECT sélectionne un plan différent, qui utilise une recherche en lieu et place d’une analyse, puis exécute plus efficacement le plan :

![Un plan de requête avec index corrigés](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

L’information clé est que la capacité d’E/S d’un système partagé est plus limitée que celle d’un serveur dédié. Il est primordial de réduire les E/S inutiles pour tirer le meilleur parti du système dans la DTU de chaque niveau de performances des niveaux de service dans Azure SQL Database. Des choix appropriés de conception physique de base de données peuvent considérablement améliorer la latence des requêtes individuelles, le débit des requêtes simultanées que vous pouvez traiter par unité d’échelle, et réduire les coûts nécessaires pour satisfaire la requête. Pour plus d’informations sur les DMV d’index manquants , consultez [sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Paramétrage/Compréhension de requêtes
L’optimiseur de requête de Microsoft Azure SQL Database est similaire à l’optimiseur de requête SQL Server traditionnel. La plupart des meilleures pratiques pour le paramétrage des requêtes et la compréhension du raisonnement relatif aux limitations du modèle pour l’optimiseur de requête s’appliquent également à Microsoft Azure SQL Database. Si vous paramétrez des requêtes dans Microsoft Azure SQL Database, vous pouvez profiter de l’avantage supplémentaire de réduction des exigences de ressources globales. Votre application peut s’exécuter à un coût inférieur à celui d’une instance équivalent non paramétrée, car elle peut fonctionner à un niveau de performance moindre.

Un scénario courant dans SQL Server, qui s’applique également à Microsoft Azure SQL Database, est la détection des paramètres par l’optimiseur de requête. Pendant la compilation, l’optimiseur de requête évalue la valeur actuelle d’un paramètre pour déterminer s’il est possible de générer un plan de requête plus optimal. Bien que cette stratégie mène souvent à un plan de requête qui est beaucoup plus rapide qu’un plan compilé sans valeurs de paramètre connues, il fonctionne actuellement de manière imparfaite dans SQL Server et dans Microsoft Azure SQL Database. Parfois le paramètre n’est pas surveillé, et d’autres fois le paramètre est surveillé mais le plan généré n’est pas optimal pour l’ensemble complet de valeurs de paramètres d’une charge de travail. Microsoft inclut des indicateurs de requête (directives) pour vous permettre de spécifier vos intentions plus délibérément et de remplacer le comportement par défaut pour la détection des paramètres. Souvent, l’utilisation d’indicateurs peut résoudre les cas où le comportement de SQL Server/de Microsoft Azure SQL Database par défaut est imparfait pour une charge de travail client donnée.

L’exemple suivant illustre la manière dont le processeur de requêtes peut générer un plan non optimal en matière de performances et de ressources requises. Cet exemple vous montre que si vous utilisez un indicateur de requête, vous pouvez réduire la durée d’exécution et le nombre de ressources requises pour votre base de données SQL :

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

Le code d’installation crée une table qui contient une distribution décalée des données. Le plan de requête optimal varie en fonction du paramètre sélectionné. Malheureusement, le comportement de mise en cache du plan ne recompile pas toujours la requête en fonction de la valeur de paramètre la plus courante. Par conséquent, il est possible de mettre en cache un plan non optimal et de l’utiliser pour plusieurs valeurs, même si un autre plan pourrait constituer un meilleur choix en moyenne. Ensuite, le plan de requête génère deux procédures stockées identiques, sauf que celle-ci présente un indicateur spécifique de requête.

**Exemple, partie 1**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times to show the performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Exemple, partie 2**

(Nous vous recommandons d’attendre au moins 10 minutes avant de commencer la partie 2 de l’exemple, de manière à ce que les résultats soient différents dans les données de télémétrie obtenues.)

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

Chaque partie de cet exemple essaie d’exécuter une instruction insert paramétrable 1 000 fois (pour générer une charge suffisante pour être intéressante sur un jeu de données de test). Lors de l’exécution des procédures stockées, le processeur de requêtes examine la valeur de paramètre transmise à la procédure lors de sa première compilation (appelée détection de paramètres). Le processeur met en cache le plan résultant et l’utilise pour les appels ultérieurs, même si la valeur de paramètre est différente. Le plan optimal peut ne pas être utilisé dans tous les cas. Parfois, les clients doivent guider l’optimiseur vers le choix d’un plan adapté aux situations courantes, plutôt qu’aux situations spécifiques lorsque la requête a été compilée en premier lieu. Dans cet exemple, le plan initial génère un plan de type analyse qui lit toutes les lignes pour trouver chaque valeur qui correspond au paramètre :

![Optimisation des requêtes à l’aide d’un plan d’analyse](./media/sql-database-performance-guidance/query_tuning_1.png)

Étant donné que nous avons exécuté la procédure avec la valeur 1, le plan obtenu était optimal pour 1, mais non optimal pour toutes les autres valeurs dans la table. Le résultat n’est probablement pas ce que vous attendriez en sélectionnant chaque plan de manière aléatoire, car le plan s’exécute plus lentement et utilise davantage de ressources.

Si vous exécutez le test avec `SET STATISTICS IO` défini sur `ON`, la tâche d’analyse logique de cet exemple est effectuée en arrière-plan. Vous pouvez voir que 1 148 lectures sont effectuées par le plan (ce qui est inefficace, si le cas moyen renvoie juste une ligne) :

![Optimisation des requêtes à l’aide d’une analyse logique](./media/sql-database-performance-guidance/query_tuning_2.png)

La deuxième partie de l’exemple utilise un indicateur de requête pour spécifier à l’optimiseur d’utiliser une valeur spécifique pendant le processus de compilation. Dans ce cas, il force le processeur de requêtes à ignorer la valeur transmise en tant que paramètre, et à prendre en compte `UNKNOWN`. Cela fait référence à une valeur présentant la fréquence moyenne de la table (en ignorant le décalage). Le plan obtenu est un plan basé sur la recherche, qui est plus rapide et utilise moins de ressources en moyenne que le plan de la partie 1 de cet exemple :

![Optimisation des requêtes à l’aide d’un indicateur de requête](./media/sql-database-performance-guidance/query_tuning_3.png)

Vous pouvez voir l’effet dans la table **sys.resource_stats** (un délai est respecté entre l’exécution du test et l’ajout des données dans la table). Dans cet exemple, la partie 1 s’est exécutée pendant la fenêtre temporelle 22:25:00, et la partie 2 pendant la fenêtre temporelle 22:35:00. La première fenêtre temporelle a utilisé plus de ressources que la dernière (en raison d’améliorations de l’efficacité du plan).

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Résultats des exemples de paramétrage des requêtes](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Bien que le volume de cet exemple soit intentionnellement petit, l’effet des paramètres non optimaux peut s’avérer conséquent, plus particulièrement sur les bases de données plus grandes. La différence, dans les cas extrêmes, se chiffre en secondes pour les scénarios rapides et en heures pour les scénarios lents.
> 
> 

Vous pouvez examiner **sys.resource_stats** pour déterminer si la ressource d’un test donnée utilise plus ou moins de ressource qu’un autre test. Lorsque vous comparez les données, espacez les tests dans le temps pour qu’ils ne soient pas groupés dans la même fenêtre temporelle de 5 minutes dans la vue **sys.resource_stats**. Le but de cet exercice est de réduire les ressources totales utilisées, et non pas de réduire les ressources. En règle générale, l’optimisation d’une partie de code pour la latence permet également de réduire l’utilisation des ressources. Assurez-vous que les modifications apportées à une application sont nécessaires, et que les modifications n’affectent pas négativement les utilisateurs susceptibles d’utiliser des indicateurs de requêtes dans l’application.

Si une charge de travail présente un ensemble de requêtes répétitives, il est souvent judicieux de capturer et de valider l’optimalité de ces choix de plan, dans la mesure où ils proposeront l’unité de taille de ressource minimum requise pour héberger la base de données. Après la validation, réexaminez régulièrement les plans afin de vous assurer de leur non-dégradation. Pour plus d’informations, consultez la page [Indicateurs de requête (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Partitionnement entre plusieurs bases de données
Microsoft Azure SQL Database s’exécutant sur du matériel, les limites de capacité pour une base de données unique sont inférieures par rapport à une installation SQL Server locale traditionnelle. Certains clients utilisent des techniques de partitionnement pour diffuser les opérations de base de données sur plusieurs bases de données lorsqu’elles ne s’adaptent pas aux limites d’une base de données unique dans Microsoft Azure SQL Database. La plupart des clients utilisant des techniques de partitionnement dans Microsoft Azure SQL Database fractionnent leurs données dans une seule dimension sur plusieurs bases de données. Pour cette approche, vous devez comprendre que les applications OLTP exécutent souvent des transactions s’appliquant uniquement à une ligne ou à un petit groupe de lignes dans le schéma.

> [!NOTE]
> La base de données SQL fournit désormais une bibliothèque pour faciliter le partitionnement. Pour en savoir plus, consultez [Vue d'ensemble de la bibliothèque cliente de bases de données élastiques](sql-database-elastic-database-client-library.md).
> 
> 

Par exemple, si une base de données comporte le nom d’un client, une commande et des détails relatifs à la commande (comme vu dans l’exemple de base de données Northwind classique fourni dans SQL Server), vous pouvez fractionner ces données en plusieurs bases de données, en regroupant un client avec la commande associée et les détails relatifs à cette commande. Vous pouvez garantir que les données du client sont conservées dans une base de données unique. L’application fractionnerait différents clients sur les bases de données, répartissant ainsi efficacement la charge sur celles-ci. Le partitionnement permet non seulement aux clients d’éviter la limite de taille maximum de la base de données, mais également à Microsoft Azure SQL Database de traiter les charges de travail qui sont beaucoup plus volumineuses que les limites des différents niveaux de performances à condition que chaque base de données individuelle s’adapte à sa DTU.

Bien que le partitionnement de base de données ne réduise pas la capacité des ressources globales pour une solution, cette technique est très efficace pour prendre en charge des solutions volumineuses réparties sur plusieurs bases de données. Chaque base de données peut s’exécuter à un niveau de performance différent afin de prendre en charge des bases de données très grandes, efficaces, dont les besoins en ressources sont importants.

### <a name="functional-partitioning"></a>Partitionnement fonctionnel
Les utilisateurs SQL Server combinent bien souvent de nombreuses fonctions dans une seule base de données. Par exemple, si une application contient une logique pour gérer le stock d’un magasin, cette base de données peut contenir la logique associée au stock, le suivi des bons de commande, les procédures stockées et les vues indexées/matérialisées pour la gestion de rapports de fin de mois et d’autres fonctions. Cette technique facilite l’administration de la base de données pour des opérations comme la sauvegarde, mais elle nécessite également que vous redimensionniez le matériel pour gérer la charge maximale sur toutes les fonctions d’une application.

Si vous utilisez une architecture de montée en charge dans Microsoft Azure SQL Database, il peut être judicieux de répartir différentes fonctions d’une application entre plusieurs bases de données. En appliquant cette technique, chaque application est mise à l’échelle indépendamment. Lorsqu’une application devient plus occupée (et reçoit plus de charge sur la base de données), l’administrateur peut choisir des niveaux de performances indépendamment pour chaque fonction dans une application. À la limite, cette architecture permet à une application de devenir plus grande que ce qu’un seul ordinateur peut gérer en diffusant la charge sur plusieurs ordinateurs.

### <a name="batch-queries"></a>Traitement par lot des requêtes
Pour les applications qui accèdent aux données sous la forme de requêtes ad hoc, fréquentes et à volume élevé, une grande partie du temps de réponse est passée sur la communication réseau entre la couche Application et la couche Microsoft Azure SQL Database. Même lorsque l’application et Microsoft Azure SQL Database résident dans le même centre de données, la latence du réseau entre les deux peut être accrue par un nombre élevé d’opérations d’accès aux données. Pour réduire les boucles réseau requises par les opérations d’accès aux données, envisagez d’utiliser l’option pour traiter par lot les requêtes ad hoc, ou pour les compiler en tant que procédures stockées. Si vous traitez par lot les requêtes ad hoc, vous pouvez envoyer plusieurs requêtes sous forme de lot important communiqué dans une boucle unique à destination de l’instance Microsoft Azure SQL Database. Si vous compilez les requêtes ad hoc dans une procédure stockée, vous pouvez obtenir des résultats similaires à ceux du traitement par lot. L’utilisation d’une procédure stockée vous permet également d’augmenter les possibilités de mise en cache des plans de requête dans Azure SQL Database pour les exécutions suivantes de la même procédure stockée.

Certaines applications sont gourmandes en écriture. Parfois, il est possible de réduire la charge d’E/S totale sur une base de données en étudiant comment effectuer des écritures par lot. Souvent, cela est aussi simple que d’utiliser des transactions explicites au lieu des transactions de validation automatique dans les procédures stockées et les lots ad hoc. Vous trouverez une évaluation des différentes techniques utilisables à la page [Comment utiliser le traitement par lots pour améliorer les performances des applications de base de données SQL](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Faites des essais avec votre propre charge de travail afin d’identifier le modèle approprié pour le traitement par lot. Assurez-vous de tenir compte du fait que les modèles peuvent présenter des garanties de cohérence transactionnelle légèrement différentes. L’identification de la charge de travail adaptée pour la réduction de l’utilisation des ressources nécessite de trouver le bon équilibre entre cohérence et performances.

### <a name="application-tier-caching"></a>Mise en cache de la couche Application
Certaines applications de base de données contiennent des charges de travail à lecture intensive. Les couches de mise en cache peuvent contribuer à réduire la charge sur la base de données et éventuellement le niveau de performance requis pour la prise en charge d’une base de données à l’aide d’Azure SQL Database. Le [Cache Redis Azure](https://azure.microsoft.com/services/cache/)permet à un client possédant une charge de travail à lecture intensive de lire les données une seule fois (ou peut-être une seule fois par ordinateur de la couche Application, selon la façon dont il est configuré) et de stocker ces données en dehors de la base de données SQL Azure. Cela permet de réduire la charge de la base de données (UC et E/S de lecture), mais il existe un impact sur la cohérence transactionnelle, étant donné que les données lues à partir du cache peuvent être désynchronisées avec les données de la base de données. Si un certain niveau d’incohérence est acceptable dans de nombreuses applications, cela ne se vérifie pas pour l’ensemble des charges de travail. Assurez-vous de comprendre pleinement les exigences d’une application avant d’utiliser une stratégie de mise en cache de couche Application.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur les niveaux de service, consultez la section [Options et performances de la base de données SQL](sql-database-service-tiers.md)
* Pour de plus amples informations sur les pools élastiques, consultez la page [Qu’est-ce qu’un pool élastique Azure ?](sql-database-elastic-pool.md)
* Pour plus d’informations sur les performances et les pools élastiques, consultez la page [Quand envisager d’utiliser un pool élastique ?](sql-database-elastic-pool-guidance.md)

