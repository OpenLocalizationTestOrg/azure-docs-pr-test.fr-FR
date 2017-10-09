---
title: "conseils de réglage des performances de base de données SQL aaaAzure | Documents Microsoft"
description: "Cet article peut vous aider à déterminer quels toochoose de niveau de service pour votre application. Il recommande également des méthodes tootune votre hello de tooget application plus à partir de la base de données SQL Azure."
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
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Optimisation des performances dans Azure SQL Database

Base de données SQL Azure fournit [recommandations](sql-database-advisor.md) que vous pouvez utiliser tooimprove les performances de votre base de données, ou vous pouvez laisser la base de données SQL Azure [automatiquement adapter tooyour application](sql-database-automatic-tuning.md) et appliquer les modifications qui améliore les performances de votre charge de travail.

Vous n’avez pas de recommandations applicables et vous rencontrez toujours des problèmes de performances, vous pouvez utiliser hello suivant performances tooimprove de méthodes :
1. Augmenter [niveaux de service](sql-database-service-tiers.md) et fournir la base de données de plusieurs ressources tooyour.
2. Paramétrez votre application et appliquez quelques meilleures pratiques susceptibles d’améliorer les performances. 
3. Paramétrer la base de données de hello en modifiant des index et des requêtes toomore travailler efficacement avec des données.

Il s’agit des méthodes manuelles, car vous devez toodecide que [niveaux de service](sql-database-service-tiers.md) vous choisiriez ou que vous avez besoin de toorewrite application ou le code de base de données et deply des modifications de hello.

## <a name="increasing-performance-tier-of-your-database"></a>Augmentation du niveau de performance de votre base de données

Azure SQL Database propose quatre [niveaux de service](sql-database-service-tiers.md) : De base, Standard, Premium et Premium RS. Les performances sont mesurées en unités de débit de base de données, ou [DTU](sql-database-what-is-a-dtu.md). Chaque niveau de service isole strictement ressources hello que votre base de données SQL peut utiliser et de garantie des performances prévisibles pour ce niveau de service. Dans cet article, nous vous proposons des conseils qui peuvent vous aider à choisir le niveau de service hello pour votre application. Nous abordons également les méthodes que vous pouvez paramétrer votre hello de tooget application plus à partir de la base de données SQL Azure.

> [!NOTE]
> Cet article se concentre sur les recommandations de performances pour les bases de données uniques dans Microsoft Azure SQL Database. Pour obtenir des conseils de performances des pools de tooelastic connexes, consultez [considérations de prix et de performances pour les pools élastiques](sql-database-elastic-pool-guidance.md). Notez, cependant, que vous pouvez appliquer un grand nombre de recommandations dans ce toodatabases article dans un pool élastique de paramétrage de hello et obtenir les avantages de performances similaires.
> 

* **Base**: hello du service de base niveau offres bonne prévisibilité de performance pour chaque base de données, à l’heure sur l’heure. Dans une base de données De base, des ressources suffisantes prennent en charge de bonnes performances au sein d’une petite instance qui ne présente pas plusieurs requêtes simultanées. Voici quelques cas d’usage classiques pour lesquels vous devez utiliser le niveau de service De base :
  * **Vous débutez juste avec Azure SQL Database**. Bien souvent, les applications en cours de développement ne requièrent pas de hauts niveaux de performances. Les bases de données De base constituent un environnement idéal pour le développement ou le test des bases de données, et ce, à moindre coût.
  * **Vous disposez d’une base de données avec un utilisateur unique**. Généralement, les applications qui associent un seul utilisateur à une base de données n’ont pas des exigences élevées en matière d’accès concurrentiel et de performances. Ces applications sont des candidats pour le niveau de service Basic de hello.
* **Standard**: niveau de service Standard hello offre prévisibilité des performances améliorées et fournit de bonnes performances pour les bases de données qui ont plusieurs demandes simultanées, telles que les applications web et de groupe de travail. Lorsque vous choisissez une base de données de niveau de service Standard, vous pouvez dimensionner votre application de base de données en fonction de performances prévisibles, minute après minute.
  * **Votre base de données présente de multiples requêtes simultanées**. Les applications utilisées simultanément par plusieurs utilisateurs requièrent généralement des niveaux de performances plus élevés. Par exemple, les applications web ou de groupe de travail qui ont des exigences de trafic d’e/s toomedium basse prenant en charge plusieurs requêtes simultanées sont idéales pour un niveau de service Standard hello.
* **Premium**: niveau de service Premium hello fournit des performances prévisibles, deuxième par seconde, pour chaque base de données Premium. Lorsque vous choisissez le niveau de service Premium hello, vous pouvez redimensionner votre application de base de données basée sur les pics de charge hello pour cette base de données. plan de Hello supprime un cas dans lequel écart de performances peut entraîner des tootake de petites requêtes plus longtemps que prévu dans des opérations sensibles. Ce modèle peut considérablement simplifier cycles hello développement et de produit de la validation pour les applications qui doivent toomake des instructions fortes sur les besoins en ressources pointe, écart de performance ou latence de la requête. La plupart des cas d’utilisation du niveau de service Premium présentent une ou plusieurs de ces caractéristiques :
  * **Pic de charge élevés**. Une application qui nécessite d’importante UC, la mémoire ou entrée/sortie (e/s) toocomplete ses opérations requiert un niveau de dédié, hautes performances. Par exemple, une opération de base de données appelée tooconsume plusieurs cœurs d’UC pendant une période prolongée est un candidat pour la couche de service Premium hello.
  * **Plusieurs requêtes simultanées**. Certaines applications de base de données gèrent de nombreuses demandes simultanées, par exemple un site web avec un volume de trafic élevé. Base et Standard niveaux de service de limitent le nombre de hello de demandes simultanées par base de données. Les applications qui nécessitent des connexions plus doivent toochoose un réservation appropriée taille toohandle hello nombre maximal de demandes nécessaires.
  * **Latence faible**. Certaines applications ont besoin tooguarantee une réponse à partir de la base de données hello dans un minimum de temps. Si une procédure stockée spécifique est appelée dans le cadre d’une opération de client plus large, vous pouvez avoir une exigence toohave un retour de cet appel dans pas plus de 20 millisecondes, 99 % du temps de hello. Ce type d’avantages des applications à partir de la couche de service Premium hello, toomake, vérifiez que ce hello nécessaires de puissance de calcul est disponible.
* **Premium RS**: hello de niveau Premium RS est conçu pour les charges de travail gourmandes en e/s qui ne nécessitent pas hello garanties de disponibilité le plus élevés. Exemples incluent le test des charges de travail hautes performances, ou une charge de travail analytique où la base de données hello n’est pas système hello d’enregistrement.

niveau de service Hello dont vous avez besoin pour votre base de données SQL varie selon les conditions de charge maximale hello pour chaque dimension de ressource. Certaines applications utilisent une quantité insignifiante pour une ressource mais ont des exigences considérables pour d’autres.

### <a name="service-tier-capabilities-and-limits"></a>Capacités et limites des niveaux de service

À chaque niveau de service, vous définissez les niveaux de performances hello afin que vous ayez toopay de flexibilité hello uniquement pour la capacité de hello que nécessaire. Vous pouvez [ajuster la capacité](sql-database-service-tiers.md), en l’augmentant ou en la diminuant, en fonction de l’évolution de la charge de travail. Par exemple, si votre charge de travail de base de données est élevée pendant la saison d’achat de hello précédent à l’école, vous pouvez augmenter le niveau de performance hello pour la base de données hello pendant une période définie, juillet à septembre. Il est ensuite possible de le réduire à la fin de la période chargée. Vous pouvez réduire les frais en optimisant votre saisonnalité de toohello environnement cloud de votre entreprise. Ce modèle fonctionne également bien pour les cycles de version de logiciels. Une équipe de test peut allouer de la capacité pendant des séries de test, et libérer cette capacité une fois les tests terminés. Dans un modèle de requête de capacité, vous payez uniquement la capacité nécessaire, en évitant de financer des ressources dédiées que vous n’utiliseriez que rarement.

### <a name="why-service-tiers"></a>Pourquoi des niveaux de service ?
Bien que chaque charge de travail de base de données peut être différentes, hello des niveaux de service vise tooprovide prévisibilité des performances à différents niveaux de performances. Les clients présentant des exigences d’envergure en matière de ressources de bases de données peuvent opérer dans un environnement informatique davantage dédié.

## <a name="tune-your-application"></a>Paramétrer votre application
Dans SQL Server local traditionnel, hello processus de planification de la capacité initiale souvent est distinct hello processus d’exécution d’une application en production. Le matériel et les licences de produit sont achetés dans un premier temps, tandis que le paramétrage des performances est exécuté ultérieurement. Lorsque vous utilisez la base de données SQL Azure, il est un processus de hello toointerweave bonne idée de l’exécution d’une application et son paramétrage. Avec le modèle hello de paiement pour la capacité à la demande, vous pouvez paramétrer votre application toouse hello ressources minimales maintenant, au lieu de ressources matérielles en fonction de conjectures de plans de croissance future pour une application, qui sont souvent incorrects. Certains clients peuvent choisir tootune pas une application et choisissez plutôt toooverprovision des ressources matérielles. Cette approche peut s’avérer utile si vous ne souhaitez pas toochange une clé de l’application pendant une période d’activité. Toutefois, le paramétrage d’une application peut réduire les besoins en ressources et les factures mensuelles lorsque vous utilisez des niveaux de service hello dans la base de données SQL Azure.

### <a name="application-characteristics"></a>Caractéristiques des applications
Bien que les niveaux de service de base de données SQL Azure de configuration et la stabilité des performances tooimprove conçu pour une application, certaines meilleures pratiques peuvent vous aider à optimiser votre toobetter tirer parti des applications de ressources hello à un niveau de performances. Bien que de nombreuses applications ont des gains de performances significatifs simplement en commutation tooa plus élevé de niveau de performance ou de service de niveau, certaines applications ont besoin réglage toobenefit à partir d’un niveau plus élevé de service supplémentaire. Pour améliorer les performances, envisagez de procéder à un paramétrage supplémentaire sur les applications présentant ces caractéristiques :

* **Les applications dont les performances sont lentes en raison d’un comportement bavard**. Applications bavardes effectuer des opérations d’accès aux données excessive qui sont sensibles toonetwork latence. Vous devrez peut-être toomodify ces types de nombre de hello tooreduce applications de base de données de données access operations toohello SQL. Par exemple, vous pouvez améliorer les performances de l’application à l’aide de techniques telles que le traitement par lot des requêtes ad hoc ou déplacement hello interroge toostored procédures. Pour plus d’informations, consultez la section [Traitement par lot des requêtes](#batch-queries).
* **Bases de données présentant une charge de travail intensive ne pouvant pas être prise en charge par un seul ordinateur**. Bases de données qui dépassent les ressources hello de plus haut niveau de performance Premium hello peuvent tirer parti de la montée en charge de travail hello. Pour plus d’informations, consultez les sections [Partitionnement entre plusieurs bases de données](#cross-database-sharding) et [Partitionnement fonctionnel](#functional-partitioning).
* **Applications présentant des requêtes non optimales**. Applications, particulièrement celles qui sont dans la couche d’accès aux données hello, qui ont des requêtes mal paramétrées ne peuvent pas bénéficier d’un niveau de performance supérieur. Cela inclut les requêtes dépourvues d’une clause WHERE et les requêtes présentant des index manquants ou des statistiques obsolètes. Ces applications bénéficient des techniques de paramétrage des performances de requête standard. For more information, consultez les sections [Index manquants](#identifying-and-adding-missing-indexes) et [Paramétrage/Compréhension de requêtes](#query-tuning-and-hinting).
* **Les applications dotées d’un accès aux données non optimal**. Les applications qui rencontrent des problèmes inhérents de concurrence d’accès aux données, par exemple d’interblocage, peuvent ne pas tirer parti d’un niveau de performances supérieur. Envisagez de réduire les allers-retours sur hello base de données SQL Azure en cache des données côté client de hello avec hello service Caching de Azure ou une autre technologie de mise en cache. Consultez la section [Mise en cache de la couche Application](#application-tier-caching).

## <a name="tune-your-database"></a>Optimiser votre base de données
Dans cette section, nous examiner quelques techniques que vous pouvez utiliser les meilleures performances tootune base de données SQL Azure toogain hello pour votre application et l’exécuter au niveau de performances possibles hello plus bas. Certaines de ces techniques correspondent aux meilleures pratiques de paramétrage de traditionnel SQL Server, mais d’autres sont spécifique tooAzure de base de données SQL. Dans certains cas, vous pouvez examiner les ressources hello consommée pour un paramétrage de base de données toofind zones toofurther et étendre toowork de techniques traditionnel SQL Server dans la base de données SQL Azure.

### <a name="identify-performance-issues-using-azure-portal"></a>Identifier les problèmes de performances à l’aide du portail Azure
Hello suivant outils Bonjour portail Azure peut vous aider à analyser et résoudre les problèmes de performances avec votre base de données SQL :

* [Query Performance Insight](sql-database-query-performance.md)
* [SQL Database Advisor](sql-database-advisor.md)

portail Azure Hello a plus d’informations sur ces deux outils et comment toouse les. tooefficiently diagnostiquer et corriger les problèmes, nous vous recommandons d’essayer les outils hello Bonjour portail Azure. Nous vous recommandons d’utiliser manuel hello approches que nous avons abordées ensuite, index et paramétrage des requêtes, dans certains cas manquent de paramétrage.

Découvrez plus d’informations sur l’identification des problèmes dans Azure SQL Database dans l’article [Analyse des performances](sql-database-single-database-monitor.md).

### <a name="identifying-and-adding-missing-indexes"></a>Identification et ajout d’index manquants
Un problème courant dans les performances de base de données OLTP concerne la conception de base de données physique toohello. Souvent, les schémas de base de données sont conçus et livrés sans test de mise à l’échelle (en charge ou en volume de données). Malheureusement, les performances de hello d’un plan de requête peuvent être acceptables à petite échelle, mais dégrader considérablement sous les volumes de données au niveau de la production. Hello plus courante de ce problème est le manque de hello de filtres de toosatisfy index appropriés ou d’autres restrictions dans une requête. Souvent, cela se manifeste comme une analyse de table là où une recherche d’index pourrait suffire.

Dans cet exemple, le plan de requête sélectionné hello utilise une analyse lorsqu’une recherche suffit :

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

Azure SQL Database peut vous aider à rechercher et à corriger les conditions communes d’index manquants. Vues de gestion dynamique qui sont intégrées à la base de données SQL Azure examiner de compilations de requête dans laquelle un index réduit de manière significative hello estimé coût toorun une requête. Pendant l’exécution de la requête SQL de base de données effectue le suivi de la fréquence à laquelle chaque plan de requête est exécutée, et hello de pistes estimé écart entre hello hello et plan de requête d’exécution imaginer un où cet index existait. Vous pouvez utiliser ces estimation de tooquickly DMV quelle conception de base de données physique tooyour modifications peut améliorer le coût de la charge de travail global pour une base de données et sa charge de travail réelle.

Vous pouvez utiliser ce potentiel tooevaluate de requête index manquants :

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

Dans cet exemple, hello requête a généré cette suggestion :

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Après sa création, cette même instruction SELECT sélectionne un autre plan, qui utilise une recherche au lieu d’une analyse, puis exécute le plan de hello plus efficacement :

![Un plan de requête avec index corrigés](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

un aperçu de la clé de Hello est cette capacité d’e/s d’une salutation, système est plus limitée que celle d’un ordinateur serveur dédié. Il est primordial de réduire inutile d’e/s tootake au mieux les capacités du système hello Bonjour DTU de chaque niveau de performance des niveaux de service de base de données SQL Azure hello. Choix de conception physique appropriée de la base de données peut considérablement améliorer la latence hello pour les requêtes individuelles, améliorer le débit hello de demandes simultanées traitées par unité d’échelle et réduire la requête de hello hello coûts toosatisfy requis. Pour plus d’informations sur hello manquant index DMV, consultez [sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Paramétrage/Compréhension de requêtes
optimiseur de requête Hello dans la base de données SQL Azure est semblable toohello optimiseur de requête SQL Server traditionnel. La plupart des méthodes conseillées pour le paramétrage des requêtes et hello compréhension raisonnement également les limitations du modèle pour l’optimiseur de requête hello hello s’appliquent tooAzure base de données SQL. Si vous ajustez les requêtes dans la base de données SQL Azure, vous pouvez obtenir l’avantage supplémentaire de hello de réduire les besoins de ressources globales. Votre application peut être en mesure de toorun à un coût inférieur à un équivalent non paramétré, car il s’exécute à un niveau de performances inférieur.

Un exemple qui est courant dans SQL Server et qui s’applique également tooAzure base de données SQL est comment hello optimiseur « espionne » des paramètres de requête. Lors de la compilation, optimiseur de requête hello renvoie la valeur actuelle de hello d’un paramètre de toodetermine si elle peut générer un plan de requête plus optimal. Bien que cette stratégie mène souvent plan de requête tooa beaucoup plus rapide qu’un plan compilé sans valeurs de paramètre connus, il fonctionne actuellement pourtour à la fois dans SQL Server et dans la base de données SQL Azure. Parfois, le paramètre hello n’est pas surveillé et parfois paramètre hello est surveillé, mais les plan généré hello est optimal pour hello les ensemble de valeurs de paramètre dans une charge de travail. Microsoft inclut des indicateurs de requête (directives) afin que vous pouvez spécifier l’intention plus délibérément et remplacer le comportement par défaut de hello de détection de paramètres. Souvent, si vous utilisez des indicateurs, vous pouvez corriger le cas dans lesquels le comportement de SQL Server ou de la base de données SQL Azure hello par défaut est imparfait pour une charge de travail client spécifique.

Hello l’exemple suivant montre comment processeur de requêtes hello peut générer un plan qui n’est pas optimal pour les performances et besoins en ressources. Cet exemple vous montre que si vous utilisez un indicateur de requête, vous pouvez réduire la durée d’exécution et le nombre de ressources requises pour votre base de données SQL :

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

le code de configuration Hello crée une table qui a dévié distribution des données. requête optimal de Hello diffère de plan basés sur le paramètre est sélectionné. Malheureusement, comportement de mise en cache de plan de hello ne recompilez toujours requête hello en fonction de la valeur du paramètre hello plus courantes. Par conséquent, il est possible pour un toobe de plans non optimaux en cache et utilisé pour de nombreuses valeurs, même si un autre plan peut être un meilleur choix de plan en moyenne. Plan de requête hello crée ensuite deux procédures stockées qui sont identiques, sauf qu’un a un indicateur de requête spéciaux.

**Exemple, partie 1**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Exemple, partie 2**

(Nous vous recommandons de patienter au moins 10 minutes avant de commencer la partie 2 de l’exemple de hello, afin que les résultats de hello sont distinctes dans hello résultant des données de télémétrie.)

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

Chaque partie de cet exemple tente toorun une instruction insert paramétrable 1 000 fois (toogenerate un toouse charge suffisante comme un jeu de données de test). Lorsqu’il exécute des procédures stockées, processeur de requêtes hello examine la valeur de paramètre hello est passé toohello procédure lors de sa première compilation (« détection des paramètres »). processeur de Hello met en cache de plan obtenu de hello et utilise pour les appels ultérieurs, même si la valeur du paramètre hello est différente. plan optimal de Hello ne peut pas être utilisé dans tous les cas. Vous devez parfois tooguide hello optimiseur toopick un plan qui est préférable pour les cas moyen hello plutôt que des cas hello de lorsque hello a été tout d’abord de compiler la requête. Dans cet exemple, le plan initial de hello génère un plan de « analyse » qui lit toutes les lignes toofind chaque valeur qui correspond au paramètre hello :

![Optimisation des requêtes à l’aide d’un plan d’analyse](./media/sql-database-performance-guidance/query_tuning_1.png)

Étant donné que nous avons exécuté la procédure de hello à l’aide de la valeur de hello 1, hello le plan obtenu était optimal pour la valeur de hello 1 mais était optimal pour toutes les autres valeurs dans la table de hello. résultat de Hello probable n’est pas ce que vous pouvez si vous étiez toopick chaque plan de façon aléatoire, car le plan de hello s’exécute plus lentement et utilise davantage de ressources.

Si vous exécutez le test hello avec `SET STATISTICS IO` défini trop`ON`, le travail d’analyse logique de hello dans cet exemple est effectué coulisses hello. Vous pouvez voir qu’il y 1,148 lectures effectuées par plan hello (ce qui est inefficace, si les cas moyen hello est tooreturn une seule ligne) :

![Optimisation des requêtes à l’aide d’une analyse logique](./media/sql-database-performance-guidance/query_tuning_2.png)

Hello deuxième partie de hello exemple utilise un toouse de l’optimiseur de requête indicateur tootell hello une valeur spécifique au cours du processus de compilation hello. Dans ce cas, il force hello processeur tooignore hello valeur de requête qui est passée comme paramètre de hello, et à la place tooassume `UNKNOWN`. Valeur tooa ayant une fréquence moyenne de hello dans la table hello (en ignorant l’inclinaison) fait référence. plan obtenu de Hello est un plan en fonction de recherche qui est plus rapide et utilise moins de ressources, en moyenne, que le plan de hello dans la partie 1 de cet exemple :

![Optimisation des requêtes à l’aide d’un indicateur de requête](./media/sql-database-performance-guidance/query_tuning_3.png)

Vous pouvez voir effet hello Bonjour **sys.resource_stats** table (il existe un délai entre hello que vous exécutez un test de hello et lorsque les données de salutation remplissent la table de hello). Pour cet exemple, partie 1 exécutées au cours de la fenêtre de temps 22:25:00 hello et partie 2 exécutée à 22:35:00. Hello fenêtre temporelle a utilisé plus de ressources dans cette fenêtre de temps que hello une version ultérieure (en raison de l’amélioration de l’efficacité du plan).

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Résultats des exemples de paramétrage des requêtes](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Bien que le volume de hello dans cet exemple est intentionnellement petit, effet hello des paramètres non optimaux peut être substantiel, notamment sur les bases de données volumineuses. différence de Hello, dans les cas extrêmes, peut être comprise entre secondes pour les cas rapides et des heures pour les cas lentes.
> 
> 

Vous pouvez examiner **sys.resource_stats** toodetermine si la ressource hello pour un test utilise plus ou moins de ressources qu’un autre test. Lorsque vous comparez des données, séparez minutage hello de tests afin qu’ils ne soient pas hello même fenêtre de 5 minutes dans hello **sys.resource_stats** vue. Hello exercice de hello vise toominimize hello quantité de ressources utilisées et pas toominimize hello ressources. En règle générale, l’optimisation d’une partie de code pour la latence permet également de réduire l’utilisation des ressources. Vérifiez que hello modifications tooan application sont nécessaires, et que les modifications de hello n’affectent à l’expérience utilisateur hello pour une personne qui peut être à l’aide des indicateurs de requête dans une application hello.

Si une charge de travail est un ensemble de répétition des requêtes, souvent il rend le sens toocapture et valider l’Optimalité de hello de votre choix de plan car elle détermine hello minimale des ressources taille unité toohost requis hello base de données. Une fois que vous le validez, parfois réexaminer les plans hello que toohelp pour vous assurer qu’ils se ne sont pas dégradés. Pour plus d’informations, consultez la page [Indicateurs de requête (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Partitionnement entre plusieurs bases de données
Étant donné que la base de données SQL Azure s’exécute sur du matériel, les limites de capacité hello pour une base de données sont plus faible que pour une installation de SQL Server locale traditionnelle. Certains clients utilisent des opérations de base de données de partitionnement techniques toospread sur plusieurs bases de données lors des opérations de hello ne correspondent pas à l’intérieur des limites de hello d’une base de données dans la base de données SQL Azure. La plupart des clients utilisant des techniques de partitionnement dans Microsoft Azure SQL Database fractionnent leurs données dans une seule dimension sur plusieurs bases de données. Pour cette approche, vous devez toounderstand que les applications OLTP exécutent souvent les transactions qui s’appliquent tooonly un tooa petit groupe de lignes ou de lignes de schéma de hello.

> [!NOTE]
> Base de données SQL fournit désormais une tooassist bibliothèque avec le partitionnement. Pour en savoir plus, consultez [Vue d'ensemble de la bibliothèque cliente de bases de données élastiques](sql-database-elastic-database-client-library.md).
> 
> 

Par exemple, si une base de données a le nom du client, l’ordre et les détails de commande (par exemple hello de base de données exemple Northwind fournie avec SQL Server), vous pourriez fractionner ces données dans plusieurs bases de données en regroupant un client avec hello liées order et order detail plus d’informations. Vous pouvez garantir que les données de ce client hello restent dans une base de données. application Hello fractionne différents clients entre les bases de données, en répartissant efficacement hello charge entre plusieurs bases de données. Avec le partitionnement, les clients non seulement peuvent éviter de limite de taille maximale de la base de données hello, mais la base de données SQL Azure peut également traiter des charges de travail qui sont beaucoup plus importantes que les limites de hello de hello différents niveaux de performance, tant que chaque base de données s’adapte à son DTU.

Partitionnement de base de données ne réduit la capacité des ressources globales hello pour une solution, mais il est très efficace au niveau de la prise en charge de très grandes solutions qui sont réparties sur plusieurs bases de données. Chaque base de données peut exécuter à un autre performances au niveau toosupport très volumineux, des bases de données « efficaces » avec des besoins importants en ressources.

### <a name="functional-partitioning"></a>Partitionnement fonctionnel
Les utilisateurs SQL Server combinent bien souvent de nombreuses fonctions dans une seule base de données. Par exemple, si une application possède un inventaire de toomanage logique d’un magasin, cette base de données peut avoir la logique associée à l’inventaire, le suivi des bons de commande, des procédures stockées et vues indexées ou matérialisées qui gèrent la création de rapports de fin de mois. Cette technique rend plus facile tooadminister hello base de données pour les opérations telles que la sauvegarde, mais elle nécessite également vous toosize hello matériel toohandle hello pics de charge toutes les fonctions d’une application.

Si vous utilisez une architecture de montée en puissance parallèle dans la base de données SQL Azure, il est une bonne idée toosplit différentes fonctions d’une application dans différentes bases de données. En appliquant cette technique, chaque application est mise à l’échelle indépendamment. Comme une application devient plus occupée (et hello charge sur les augmentations de base de données hello), administrateur de hello peut choisir des niveaux de performance indépendants pour chaque fonction dans l’application hello. La limite hello, avec cette architecture, une application peut être plus grande qu’un seul ordinateur peut gérer, car la charge de hello est répartie sur plusieurs ordinateurs.

### <a name="batch-queries"></a>Traitement par lot des requêtes
Pour les applications qui accèdent aux données à l’aide de haut volume, fréquentes, ad hoc d’interrogation, une quantité substantielle de temps de réponse est passée sur la communication réseau entre les couches d’application de hello et base de données SQL Azure hello. Même si les deux hello d’application et de base de données SQL Azure sont Bonjour même centre de données, latence du réseau hello entre hello deux peut être accru par un grand nombre d’opérations d’accès aux données. réseau de hello tooreduce round voyages pour les données de salutation opérations d’accès, envisagez d’utiliser des requêtes ad hoc hello du lot tooeither hello option ou toocompile en tant que procédures stockées. Si les requêtes ad hoc hello par lot, vous pouvez envoyer plusieurs requêtes comme un lot volumineux dans une base de données SQL de tooAzure voyage unique. Si vous compilez les requêtes ad hoc dans une procédure stockée, vous pourriez obtenir hello que même résultat comme si leur traitement par lots. Utiliser une procédure stockée également donne vous hello avantage d’augmenter les possibilités de hello de mise en cache des plans de requête hello dans la base de données SQL Azure afin de pouvoir utiliser hello procédure stockée à nouveau.

Certaines applications sont gourmandes en écriture. Parfois, vous pouvez réduire les charge e/s total hello sur une base de données en considérant comment toobatch écrit ensemble. Souvent, cela est aussi simple que d’utiliser des transactions explicites au lieu des transactions de validation automatique dans les procédures stockées et les lots ad hoc. Vous trouverez une évaluation des différentes techniques utilisables à la page [Comment utiliser le traitement par lots pour améliorer les performances des applications de base de données SQL](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Faites des essais avec votre propre charge de travail toofind hello bon modèle pour le traitement par lot. Soient vraiment toounderstand susceptibles de présenter un modèle garantit la cohérence transactionnelle différentes. Recherche de hello charge de travail qui réduit l’utilisation des ressources exige de trouver hello bonne combinaison entre cohérence et les performances des compromis.

### <a name="application-tier-caching"></a>Mise en cache de la couche Application
Certaines applications de base de données contiennent des charges de travail à lecture intensive. La mise en cache des couches peut réduire la charge de hello sur la base de données hello et peut réduire potentiellement toosupport requis au niveau de performances de hello une base de données à l’aide de base de données SQL Azure. Avec [Cache Redis Azure](https://azure.microsoft.com/services/cache/), si vous avez une charge de travail de lectures, vous pouvez lire les données de hello qu’une seule fois (ou peut-être une fois par les ordinateurs de couche application, selon la façon dont il est configuré), puis à stocker ces données à l’extérieur de votre base de données SQL. Il s’agit d’une charge de base de données tooreduce moyen (UC et la lecture d’e/s), mais il existe une incidence sur la cohérence transactionnelle, car les données hello lues à partir du cache de hello peuvent être synchronisées avec des données dans la base de données hello hello. Si un certain niveau d’incohérence est acceptable dans de nombreuses applications, cela ne se vérifie pas pour l’ensemble des charges de travail. Assurez-vous de comprendre pleinement les exigences d’une application avant d’utiliser une stratégie de mise en cache de couche Application.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur les niveaux de service, consultez la section [Options et performances de la base de données SQL](sql-database-service-tiers.md)
* Pour de plus amples informations sur les pools élastiques, consultez la page [Qu’est-ce qu’un pool élastique Azure ?](sql-database-elastic-pool.md)
* Pour plus d’informations sur les pools élastiques et de performances, consultez [lorsque tooconsider un pool élastique](sql-database-elastic-pool-guidance.md)

