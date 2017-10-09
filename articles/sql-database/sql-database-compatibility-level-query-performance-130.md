---
title: "niveau de compatibilité aaaDatabase 130 - base de données SQL Azure | Documents Microsoft"
description: "Dans cet article, nous Découvrez les avantages de hello de votre base de données SQL Azure en cours d’exécution au niveau de compatibilité 130 et tirant parti des avantages de hello du nouvel optimiseur de requête hello et interroger les fonctionnalités du processeur. Nous avons également adresser hello possible des effets sur les performances des requêtes hello pour les applications SQL existantes hello."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Amélioration des performances des requêtes avec le niveau de compatibilité 130 dans Azure SQL Database
Base de données SQL Azure est en cours d’exécution en toute transparence des centaines de milliers de bases de données à plusieurs niveaux de compatibilité, ce qui garantit la version correspondante du toohello hello compatibilité descendante de Microsoft SQL Server pour tous ses clients et de conservation !

Dans cet article, nous Découvrez les avantages de hello de votre base de données SQL Azure en cours d’exécution au niveau de compatibilité 130 et tirant parti des avantages de hello du nouvel optimiseur de requête hello et interroger les fonctionnalités du processeur. Nous avons également adresser hello possible des effets sur les performances des requêtes hello pour les applications SQL existantes hello.

En guise de rappel de l’historique, alignement hello de niveaux de compatibilité SQL versions toodefault sont les suivantes :

* 100 : dans SQL Server 2008 et Azure SQL Database V11.
* 110 : dans SQL Server 2012 et Azure SQL Database V11.
* 120 : dans SQL Server 2014 et Azure SQL Database V12.
* 130 : dans SQL Server 2016 et Azure SQL Database V12.

> [!IMPORTANT]
> À compter de **mid-juin 2016**, dans la base de données SQL Azure, le niveau de compatibilité par défaut hello sera 130 au lieu de 120 pour **nouvellement créé** bases de données.
> 
> Les bases de données créées avant mi-juin 2016 ne sont *pas* concernées et conservent leur niveau de compatibilité actuel (100, 110 ou 120). Bases de données migrées à partir de la version de base de données SQL Azure V11 tooV12 aura un niveau de compatibilité de 110 ou 100. 
> 

## <a name="about-compatibility-level-130"></a>À propos du niveau de compatibilité 130
Tout d’abord, si vous souhaitez tooknow hello niveau de compatibilité actuel de votre base de données, exécutez hello instruction Transact-SQL suivante.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


Avant cette modification toolevel 130 se pour **qui vient d’être** créé les bases de données, nous allons examiner cette modification Nouveautés concernant le parcourir des exemples de requête très basique et voir comment tout le monde peut bénéficier à partir de celui-ci.

Le traitement des requêtes dans les bases de données relationnelles peut être très complexe et peut entraîner des toolots de l’ordinateur pour la science et mathématiques toounderstand hello inhérents aux choix de conception et les comportements. Dans ce document, le contenu de hello a été intentionnellement simplifié tooensure que toute personne disposant d’un contexte technique minimal peut comprendre l’impact de hello de modification du niveau de compatibilité hello et déterminer comment il peut bénéficier des applications.

Nous allons ont un coup de œil rapide à quel niveau de compatibilité 130 hello met dans la table de hello.  Vous trouverez plus de détails dans [Niveau de compatibilité ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), mais voici un bref résumé :

* peut être multithread Hello opération d’insertion d’une instruction Insert select ou peut avoir un plan parallèle, alors que cette opération n’était pas monothread.
* La table optimisée en mémoire et les requêtes de variables de table peuvent désormais avoir des plans parallèles. Auparavant, cette opération était également monothread.
* Les statistiques de la table optimisée en mémoire peuvent maintenant être échantillonnées et sont mises à jour automatiquement. Pour plus d’informations, consultez [Nouveautés : OLTP en mémoire (optimisation en mémoire)](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) .
* Traitement en mode batch ou en mode ligne avec index columnstore
  * Les tris sur une table avec un index columnstore s’effectuent maintenant en mode batch.
  * Les agrégats de fenêtres fonctionnent maintenant en mode batch, comme les instructions TSQL LAG/LEAD.
  * Les requêtes exécutées sur les tables columnstore avec plusieurs clauses distinctes sont traitées en mode batch.
  * Les requêtes exécutées sous DOP=1 ou avec un plan série sont également traitées en mode batch.
* Enfin, améliorations de l’Estimation de cardinalité proviennent en fait avec le niveau de compatibilité 120, mais pour ceux en cours d’exécution au niveau de compatibilité inférieure au niveau (par exemple, 100 et 110), hello déplacement toocompatibility niveau 130 sera également mettre ces améliorations et ces sites peuvent également améliorer les performances des requêtes hello de vos applications.

## <a name="practicing-compatibility-level-130"></a>Mise en pratique du niveau de compatibilité 130
Première passons certaines tables, les index et les données aléatoires créées toopractice certaines de ces nouvelles fonctionnalités. exemples de script TSQL Hello peuvent être exécutées sous SQL Server 2016, ou base de données SQL Azure. Toutefois, lors de la création d’une base de données SQL Azure, assurez-vous que vous choisissez à hello minimale P2 de base de données, car vous devez au moins deux cœurs tooallow de multi-threading et donc tirer parti de ces fonctionnalités.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


Maintenant, nous allons ont un toosome détaillée des fonctionnalités de traitement des requêtes hello avec le niveau de compatibilité 130.

## <a name="parallel-insert"></a>Opération INSERT parallèle
L’exécution d’instructions de TSQL hello ci-dessous exécute hello l’opération d’insertion au niveau de compatibilité 120 et 130, qui exécute respectivement hello l’opération d’insertion dans un modèle de thread unique (120) et dans un modèle multithread (130).

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


En demandant le plan de requête réel hello hello, examinez sa représentation sous forme de graphique ou de son contenu XML, vous pouvez déterminer quels Estimation de cardinalité fonction est au cœur. En examinant les plans hello côte à côte sur la figure 1, nous pouvons voir clairement que l’exécution du magasin de colonne INSERT hello s’étende de série dans les 120 tooparallel à 130. En outre, notez cette modification hello d’icône d’itérateur hello dans hello 130 effectifs deux flèches parallèles, illustrant les faits hello qui maintenant hello exécution de l’itérateur est effectivement parallèle. Si vous avez grand toocomplete d’opérations INSERT, l’exécution parallèle hello, nombre toohello lié du noyau, que vous avez à votre disposition pour la base de données hello, est plus performantes ; en fonction de votre situation des tooa 100 fois plus rapide !

*Figure 1 : Insérer des modifications de l’opération à partir de la série tooparallel avec le niveau de compatibilité 130.*

![La figure 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>Mode Batch SÉRIE
De même, le déplacement toocompatibility niveau 130 lors du traitement des lignes de données active en mode de traitement par lots. Tout d’abord, les opérations en mode batch ne sont disponibles que si vous avez un index columnstore. En second lieu, un lot généralement représente environ 900 lignes et utilise une logique de code optimisée pour le processeur multicœur, débit de mémoire et directement tire parti hello données compressées de hello banque des colonnes chaque fois que possible. Dans ces conditions, SQL Server 2016 peut traiter environ 900 lignes à la fois, au lieu de 1 ligne au moment de hello, et par conséquent, hello globalement les frais de fonctionnement de hello sont maintenant partagé par lot entier hello, réduisant hello globale des coûts par ligne. Ce montant partagé d’opérations combinées avec compression de la banque de colonne hello fondamentalement réduit la latence de hello impliquée dans une opération en mode de sélection de lot. Vous pouvez trouver plus d’informations sur la banque des colonnes hello et mode de traitement par lots [Guide des index Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Comme visible ci-dessous, en observant hello requête plans côte à côte sur la figure 2, nous pouvons voir que le mode de traitement hello a changé avec le niveau de compatibilité hello, et par conséquent, lors de l’exécution des requêtes hello à la fois au niveau de compatibilité complètement, nous constatons que la plupart du temps de traitement hello est passé en mode batch ligne mode (86 %) comparé toohello (14 %), où 2 lots ont été traités. Augmenter le jeu de données hello, hello avantage augmente.

*Figure 2 : Sélectionner les modifications de l’opération à partir du mode toobatch série avec un niveau de compatibilité 130.*

![Figure 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Opération SORT en mode batch
Transition de hello similaire toohello ci-dessus, mais l’opération de tri appliquée tooa, à partir de la ligne (niveau de compatibilité 120) toobatch modes (niveau de compatibilité 130) améliore les performances de hello Hello l’opération de tri pour hello mêmes raisons.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Visible côte à côte sur la figure 3, nous pouvons voir que l’opération de tri en mode ligne hello représente 81 % Hello coût, tandis que le mode de traitement par lots hello représente uniquement 19 % du coût hello (respectivement 81 et 56 % lors du tri hello lui-même).

*Figure 3 : L’opération de tri change du mode de toobatch de ligne avec le niveau de compatibilité 130.*

![Figure 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Évidemment, ces exemples contiennent uniquement des dizaines de milliers de lignes, qui a la valeur nothing lorsque vous examinez les données de salutation disponibles dans la plupart des serveurs SQL ces jours. Juste de projet ces par rapport à des millions de lignes à la place, et cela peut se traduire en quelques minutes d’exécution neutralisé chaque jour en attente de la nature de hello de votre charge de travail.

## <a name="cardinality-estimation-ce-improvements"></a>Améliorations de l’estimation de la cardinalité
Introduites avec SQL Server 2014, une base de données en cours d’exécution à un niveau de compatibilité 120 ou ci-dessus permettront à utiliser de nouvelles fonctionnalités de cardinalité hello. Estimation de la cardinalité est essentiellement une logique hello utilisé toodetermine comment SQL server exécute une requête en fonction de son coût estimé. estimation de Hello est calculée à l’aide de l’entrée à partir des statistiques associées aux objets impliqués dans cette requête. En pratique, à un niveau élevé, fonctions d’Estimation de cardinalité sont des estimations de nombre de lignes ainsi que des informations sur la distribution de hello de valeurs hello, les nombres de valeur distincte, et les nombres en double contenues dans hello des tables et des objets référencés dans la requête de hello. Obtention de ces estimations incorrect, peut entraîner des e/s de disque toounnecessary en raison des allocations de mémoire tooinsufficient (autrement dit, les vidages de TempDB), ou tooa la sélection d’une exécution de plan en série via une représentation parallèle de planifier l’exécution, tooname quelques. Conclusion, estimations incorrectes peuvent entraîner des tooan une dégradation des performances globales de l’exécution des requêtes hello. Sur hello autre côté, mieux estime, estimation plus précise, les exécutions de la requête toobetter prospects !

Comme mentionné précédemment, les optimisations de requête et les estimations sont quelque chose de complexe, mais si vous souhaitez toolearn plus d’informations sur les plans de requête et estimateur de cardinalité, vous pouvez faire référence document toohello à [optimiser vos Plans de requête avec hello SQL Server 2014 Estimateur de cardinalité](https://msdn.microsoft.com/library/dn673537.aspx) pour une présentation plus approfondie.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>Quelle estimation de la cardinalité utilisez-vous actuellement ?
toodetermine sous les Estimation de cardinalité vos requêtes sont en cours d’exécution, nous allons utiliser simplement la requête de hello exemples ci-dessous. Notez que ce premier exemple s’exécute sous le niveau de compatibilité est 110, ce qui implique d’utilisation hello de fonctions d’Estimation de cardinalité ancien hello.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Une fois l’exécution terminée, cliquez sur le lien XML hello et examiner les propriétés de hello du premier itérateur de hello comme indiqué ci-dessous. Notez le nom de la propriété hello appelé CardinalityEstimationModelVersion actuellement définie sur 70. Cela ne signifie pas que le niveau de compatibilité de base de données hello a la valeur version de SQL Server 7.0 toohello (il est défini sur 110 comme visible dans les instructions de TSQL hello ci-dessus), mais la valeur de hello 70 représente simplement la fonctionnalité Estimation de cardinalité hello héritée disponible à partir de SQL Serveur 7.0, qui n’avait aucune révision majeure jusqu'à ce que SQL Server 2014 (qui est fourni avec un niveau de compatibilité 120).

*Figure 4 : hello CardinalityEstimationModelVersion a la valeur too70 lors de l’utilisation d’un niveau de compatibilité de 110 ou inférieur.*

![Figure 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

Ou bien, vous pouvez modifier too130 au niveau de compatibilité hello et désactiver l’utilisation de hello de la fonction d’Estimation de cardinalité nouvelle hello à l’aide de hello LEGACY_CARDINALITY_ESTIMATION définir tooON avec [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx). Cela sera être exactement hello identique à l’aide de 110 à partir d’une Estimation de cardinalité fonction point de vue, lors de l’utilisation du niveau de compatibilité de traitement des requêtes plus récente hello. Ce faisant, vous pouvez tirer parti de hello nouvelle requête avec le niveau de compatibilité plus récente hello (c'est-à-dire en mode batch) des fonctionnalités de traitement, mais toujours s’appuient sur les fonctionnalités d’Estimation de cardinalité ancien hello si nécessaire.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Déplaçant toohello le niveau de compatibilité 120 ou 130 permet de nouvelles fonctionnalités de cardinalité hello. Dans ce cas, la valeur par défaut de hello CardinalityEstimationModelVersion sera définie en conséquence too120 ou 130 comme visible ci-dessous.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*Figure 5 : hello CardinalityEstimationModelVersion a la valeur too130 lors de l’utilisation d’un niveau de compatibilité de 130.*

![Figure 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Différences d’Estimation de cardinalité hello de contrôleur
Maintenant, nous allons exécuter légèrement plus complexe impliquant une jointure interne avec une clause WHERE avec des prédicats de requête et examinons hello estimation du nombre de lignes à partir de la fonction d’Estimation de cardinalité ancien hello tout d’abord.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


L’exécution de cette requête efficacement retourne des lignes de 200,704, alors que l’estimation de ligne hello avec la fonctionnalité d’Estimation de cardinalité ancien hello revendications 194,284 lignes. Évidemment, comme indiqué précédemment, ces résultats de nombre de lignes dépendront également la fréquence à laquelle vous avez exécuté hello précédents exemples, qui remplit les tables d’exemple hello indéfiniment à chaque exécution. Évidemment, les prédicats hello dans votre requête aura également une incidence sur l’estimation de réel hello à part la forme de table hello, le contenu de données et comment ces données réellement mettre en corrélation les uns avec les autres.

*Figure 6 : estimation du nombre de lignes hello est 194,284 ou 6 000 lignes désactivé à partir des lignes de 200,704 hello attendus.*

![Figure 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

Bonjour même façon, nous allons à présent exécuter hello même requête avec de nouvelles fonctionnalités de cardinalité hello.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


En examinant hello ci-dessous, vous pouvez désormais voir que cette estimation de la ligne hello est 202,877, ou beaucoup plus proche et supérieure hello Estimation de cardinalité ancien.

*Figure 7 : estimation du nombre de lignes hello est désormais 202,877, au lieu de 194,284.*

![Figure 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

En réalité, le jeu de résultats hello est 200,704 lignes (tout dépend de la fréquence à laquelle vous n’avez exécuté les requêtes hello Hello exemples précédents, mais plus important encore, comme hello TSQL utilise l’instruction de RAND() hello, les valeurs réelles hello retournées peuvent varier à partir d’un toohello exécution suivant). Par conséquent, dans cet exemple particulier, hello nouvelle Estimation de cardinalité est plus efficace au niveau de l’estimation de nombre hello de lignes, car 202,877 est beaucoup plus proches too200, 704, que 194,284 ! Enfin, si vous modifiez hello tooequality des prédicats de clause WHERE (au lieu de « > » pour l’instance), cela pourrait rendre encore plus différentes estimations hello entre hello ancienne et nouvelle fonction de cardinalité, en fonction du nombre maximal de correspondances, vous pouvez obtenir.

En l’occurrence, une estimation inférieure de 6 000 lignes par rapport au nombre réel ne représente pas une grande quantité de données dans certaines situations. Maintenant, transposer cette toomillions de lignes sur plusieurs tables et des requêtes plus complexes, et parfois hello estimation peut être désactivé par des millions de lignes et par conséquent, hello risque de hello de prise en charge incorrect de plan d’exécution, ou que la demande de mémoire insuffisante accorde début les vidages de tooTempDB et donc plus d’e/s, sont beaucoup plus important.

Si vous avez la possibilité de hello, entraîner cette comparaison avec vos requêtes les plus classiques et les jeux de données et voir par vous-même par la quantité des estimations de hello anciennes et nouvelles sont affectés, tandis que certaines pourraient vient d’être plus hors tension à partir de la réalité de hello, ou certaines autres simplement le nombre de lignes de réel toohello proche réellement retournés dans les jeux de résultats hello. Tout dépend de forme hello des requêtes, des caractéristiques de base de données SQL Azure hello, nature de hello et taille hello des jeux de données et des statistiques hello disponibles à leur sujet. Si vous venez de créer votre instance de base de données SQL Azure, la requête hello optimiseur aura toobuild ses connaissances de toutes pièces au lieu de la réutilisation des statistiques de requête précédente de hello s’exécute. Par conséquent, les estimations de hello sont situation de serveur et d’application tooevery très contextuelles et presque spécifiques. Il s’agit d’un tookeep aspect important, n’oubliez pas !

## <a name="some-considerations-tootake-into-account"></a>Certaines tootake de considérations en compte
Bien que la plupart des charges de travail bénéficierait de niveau de compatibilité 130, hello avant d’adopter le niveau de compatibilité hello pour votre environnement de production, vous avez essentiellement 3 options :

1. Vous déplacez toocompatibility niveau 130 et voir les choses. Si vous remarquez des régressions, vous définissez simplement les tooits arrière au niveau de compatibilité hello niveau d’origine, ou conserver 130 et uniquement inverser le mode hérité hello Estimation de cardinalité précédent toohello (comme expliqué ci-dessus, ce seul pourrait résoudre hello).
2. Vous testez vos applications existantes sous la même charge de production, affiner et validez les performances hello avant le cours tooproduction. En cas de problèmes, même en tant que ci-dessus, vous pouvez toujours revenir au niveau de compatibilité d’origine toohello, ou simplement inverser en mode hérité hello Estimation de cardinalité précédent toohello.
3. En tant qu’option finale, hello tooaddress de façon plus récent ces questions, est le magasin de requêtes tooleverage hello. Et c’est l’option recommandée aujourd’hui ! analyse de hello tooassist de vos requêtes sous compatibilité niveau 120 ou ci-dessous par rapport à 130, nous ne pouvons pas vous encourageons suffisamment toouse magasin de requêtes. Magasin de requêtes est disponible avec la version la plus récente de la base de données de SQL Azure V12 hello, et il est conçu toohelp vous requête résolution des problèmes de performances. Considérez hello magasin de requêtes comme une boîte noire de données pour votre base de données collecter et présenter des informations historiques détaillées sur toutes les requêtes. Cela considérablement simplifie l’analyse des performances en réduisant hello temps toodiagnose et résoudre les problèmes. Pour en savoir plus, consultez [Magasin des requêtes : un enregistreur de données pour votre base de données](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

À hello de haut niveau, si vous disposez d’un ensemble de bases de données en cours d’exécution au niveau de compatibilité 120 ou en dessous et planifiez toomove certains d'entre eux too130, ou parce que votre charge de travail configurer automatiquement les nouvelles bases de données qui seront bientôt être définis par défaut too130, pensez à qui suit de Hello :

* Avant de modifier le niveau de compatibilité de toohello en production, activer le magasin de requêtes. Vous pouvez faire référence trop[modifier le magasin de requêtes hello en Mode de compatibilité de base de données et l’utilisation des hello](https://msdn.microsoft.com/library/bb895281.aspx) pour plus d’informations.
* Ensuite, testez les charges de travail critiques à l’aide de requêtes d’un environnement de production et comparer les performances hello a rencontré et comme signalé par le magasin de requêtes et données représentatif. Si vous rencontrez des régressions, vous pouvez identifier hello régression des requêtes avec hello magasin de requêtes et utiliser l’option à partir du magasin de requêtes de forçage de plan de hello (également appelé plan épinglage). Dans ce cas, vous définitivement Restez avec le niveau de compatibilité hello 130 et utilisez le plan de requête précédent hello comme suggéré par hello magasin de requêtes.
* Si vous souhaitez tooleverage nouvelles fonctionnalités et fonctions de base de données SQL Azure (qui est en cours d’exécution SQL Server 2016), mais sont sensibles toochanges par niveau de compatibilité 130, hello en dernier recours, vous pouvez envisager de forcer le niveau de compatibilité hello précédent niveau toohello adapté à votre charge de travail à l’aide d’une instruction ALTER DATABASE. Mais tout d’abord, gardez à l’esprit ce plan de requête magasin hello épinglage option est la meilleure option car vous n’utilisez ne pas 130 restent essentiellement au niveau de fonctionnalité hello une ancienne version de SQL Server.
* Si vous avez des applications mutualisées couvrant plusieurs bases de données, il peut être hello tooupdate nécessaires configuration logique de vos bases de données de tooensure un niveau de compatibilité de cohérence sur toutes les bases de données ; ceux ancien et qui vient d’être mis en service. Performances de charge de travail de votre application peut être fait de toohello sensibles que certaines bases de données sont exécutent à des niveaux de compatibilité, et par conséquent, la cohérence au niveau de compatibilité entre les bases de données peut être requise tooprovide hello même ordre expérience tooyour clients tout tableau de hello. Notez qu’il n’est pas, cela dépend bien sûr comment votre application est affectée par le niveau de compatibilité hello.
* Enfin, concernant l’Estimation de la cardinalité de hello et tout comme la modification du niveau de compatibilité hello, avant de continuer en production, il est recommandé de votre charge de travail de production sous hello nouvelles conditions toodetermine tootest si votre application tire parti de améliorations d’Estimation de cardinalité Hello.

## <a name="conclusion"></a>Conclusion
À l’aide de la base de données SQL Azure toobenefit à partir de toutes les améliorations de SQL Server 2016 peut améliorer nettement les exécutions de la requête. C’est vrai ! Bien entendu, comme toute nouvelle fonctionnalité, une évaluation appropriée doit être effectuée les conditions exactes hello toodetermine sous lequel votre charge de travail de base de données opère hello mieux. L’expérience montre que la plupart des charges de travail sont attendu tooat moins exécuté de façon transparente au niveau de compatibilité 130, tout en tirant parti des nouvelles fonctions et la nouvelle Estimation de cardinalité de traitement des requêtes. C'est-à-dire Ceci dit, dans la pratique, il existe toujours des exceptions et procéder à une échéance appropriée diligence un toodetermine évaluation important combien vous pouvez bénéficier de ces améliorations. Et là encore, le magasin de requêtes hello peut être une aide précieuse dans ce travail !

Évolution de SQL Azure, vous pouvez espérer un niveau de compatibilité 140 Bonjour futures. Le temps venu, nous discuterons des apports de ce niveau de compatibilité 140, comme nous venons d’expliquer brièvement les avantages du niveau 130 aujourd’hui.

Pour l’instant, nous allons n'oubliez pas, à partir de juin 2016, base de données SQL Azure ne pourra le niveau de compatibilité par défaut hello too130 120 pour les bases de données nouvellement créées. Prenez date !

## <a name="references"></a>Références
* [Nouveautés (moteur de base de données)](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Blog : Le magasin des requêtes : un enregistreur de données pour votre base de données par Borko Novakovic, 8 juin 2016](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [Niveau de compatibilité ALTER TABLE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx)
* [Niveau de compatibilité 130 pour Azure SQL Database V12](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Optimisation de votre requête de Plans par hello estimateur de cardinalité SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)
* [Description des index columnstore](https://msdn.microsoft.com/library/gg492088.aspx)
* [Blog : Amélioration des performances des requêtes avec le niveau de compatibilité 130 dans Azure SQL Database, par Alain Lissoir, 6 mai 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
