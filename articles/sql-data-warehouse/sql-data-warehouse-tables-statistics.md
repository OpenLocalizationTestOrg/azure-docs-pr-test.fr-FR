---
title: "aaaManaging des statistiques sur les tables de l’entrepôt de données SQL | Documents Microsoft"
description: Prise en main des statistiques sur les tables dans Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>Gestion des statistiques sur les tables dans SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Vue d’ensemble][Overview]
> * [Types de données][Data Types]
> * [Distribuer][Distribute]
> * [Index][Index]
> * [Partition][Partition]
> * [Statistiques][Statistics]
> * [Temporaire][Temporary]
> 
> 

Hello plus SQL Data Warehouse connaît vos données, hello plus rapidement qu’il peut exécuter des requêtes sur vos données.  Hello qui vous indiquent à SQL Data Warehouse sur vos données, consiste à collecter des statistiques sur vos données.  Contenant des statistiques sur vos données est un des points les plus importants hello faire toooptimize vos requêtes.  Statistiques de ménager de l’entrepôt de données SQL hello meilleur plan pour vos requêtes.  Il s’agit, car l’optimiseur fondés sur une requête de SQL Data Warehouse hello optimiseur est un coût.  Autrement dit, il compare le coût de hello de différents plans de requête et choisit ensuite le plan hello hello onéreux, qui doit également être plan hello qui exécutera hello plus rapide.

Les statistiques peuvent être créées sur une colonne unique, sur plusieurs colonnes ou sur un index d’une table.  Les statistiques sont stockées dans un histogramme qui capture la plage de hello et la sélectivité des valeurs.  Cela présente un intérêt particulier lors de l’optimiseur de hello doit tooevaluate jointures, GROUP BY, HAVING et une clause WHERE dans une requête.  Par exemple, si l’optimiseur hello que date hello vous filtrez dans votre requête retourne 1 ligne, il peut choisir un autre plan que si elle estimations qu’ils date vous ont sélectionné va renvoyer 1 million de lignes.  Lors de la création de statistiques est extrêmement important, il est tout aussi important que les statistiques *précisément* refléter l’état actuel de hello de table de hello.  Des statistiques à jour permet de garantir qu’un plan correct est sélectionné par l’optimiseur de hello.  plans de Hello créés par l’optimiseur de hello ne sont pas aussi bien que les statistiques hello sur vos données.

Hello processus de création et de mise à jour des statistiques est actuellement un processus manuel, mais est très simple toodo.  Cela diffère de SQL Server qui crée et met à jour automatiquement les statistiques sur les colonnes uniques et les index.  À l’aide des informations de hello ci-dessous, vous pouvez considérablement automatiser la gestion de hello de statistiques de hello sur vos données. 

## <a name="getting-started-with-statistics"></a>Prise en main des statistiques
 Les statistiques échantillonnées sur chaque colonne est un moyen simple de tooget début de la création des statistiques.  Dans la mesure où il est tout aussi important tookeep les statistiques à jour, une méthode plus classique peut être tooupdate vos statistiques tous les jours ou après chaque charge. Il existe toujours un compromis entre performances et hello coût toocreate et mise à jour des statistiques.  Si vous trouvez que cela prend trop de temps toomaintain toutes vos statistiques, vous souhaiterez peut-être toobe tootry plus sélective sur les colonnes qui possèdent des statistiques ou les colonnes doive souvent mises à jour.  Vous pourriez par exemple, les colonnes de date tooupdate tous les jours, comme les nouvelles valeurs peuvent être ajoutées au lieu d’après chaque charge. Là encore, vous bénéficierez hello plus avantageux en ayant des statistiques sur des colonnes impliquées dans les jointures, GROUP BY, HAVING et une clause WHERE.  Si vous avez une table avec un grand nombre de colonnes qui sont utilisés uniquement dans hello SELECT (clause), ne permettent pas de statistiques sur ces colonnes et un peu plus tooidentify d’effort de dépense uniquement les colonnes hello où aidera à des statistiques, peuvent réduire hello temps toomaintain vos statistiques .

## <a name="multi-column-statistics"></a>Statistiques sur plusieurs colonnes
En outre toocreating des statistiques sur les colonnes uniques, vous découvrirez peut-être que vos requêtes bénéficient de statistiques de colonnes multiples.  Les statistiques sur plusieurs colonnes sont des données créées sur un ensemble de colonnes.  Ils comprennent les statistiques de colonne unique sur la première colonne de hello dans la liste de hello, ainsi que certaines informations de corrélation entre les colonnes appelée densités.  Par exemple, si vous avez une table qui s’attache tooanother sur deux colonnes, vous souhaiterez peut-être que l’entrepôt de données SQL peut améliorer le plan de hello s’il comprend la relation hello entre deux colonnes.   Les statistiques sur plusieurs colonnes peuvent améliorer les performances des requêtes lors de certaines opérations, comme les clauses « group by » et les associations composites.

## <a name="updating-statistics"></a>Mettre à jour les statistiques
Mettre à jour les statistiques est une composante importante de votre routine de gestion des bases de données.  Lors de la distribution de hello des données dans la base de données hello change, les statistiques doivent toobe mis à jour.  Les statistiques obsolètes entraîne des performances de requête optimales de toosub.

Une meilleure solution consiste tooupdate des statistiques sur les colonnes de date chaque jour lors de l’ajout de nouvelles dates.  Chaque heure nouvelle sont chargées dans l’entrepôt de données hello, nouvelles dates de la charge ou les dates de transaction sont ajoutés. Modifier la distribution des données hello et les rendre les statistiques hello obsolètes. À l’inverse, statistiques sur une colonne « pays » dans une table customer peut-être jamais toobe mis à jour, comme la distribution hello de valeurs généralement ne change pas. En supposant que la distribution de hello est constante entre les clients, ajout de nouveaux variation de la table toohello lignes ne va pas la distribution des données toochange hello. Toutefois, si votre entrepôt de données contient uniquement un pays et que vous importez des données à partir d’un nouveau pays, ce qui entraîne des données à partir de plusieurs pays doit être stockées, vous définitivement devez tooupdate des statistiques sur la colonne « pays » de hello.

Un des hello première questions tooask cas de dépannage d’une requête, » sont des statistiques de hello à jour ? »

Cette question n’est pas un objet qui peuvent être satisfaites par âge hello de données de hello. Un objet de statistiques toodate haut peut être très anciens si il n’y a eu aucune toohello matériel les données sous-jacentes. Lorsque nombre hello de lignes a sensiblement changé ou il existe une modification significative de la distribution de hello des valeurs pour une colonne donnée *puis* il s’agit des statistiques de temps de tooupdate.  

Pour référence, **SQL Server** (et non SQL Data Warehouse) met automatiquement à jour les statistiques dans les cas suivants :

* Si vous avez des lignes nulles dans une table de hello, lorsque vous ajoutez des lignes, vous obtiendrez une mise à jour automatique des statistiques
* Lorsque vous ajoutez plus de 500 table tooa de lignes à compter moins de 500 lignes (par exemple, au démarrage de l’avoir 499 et ajoutez-les au total tooa lignes 500 999 lignes), vous obtiendrez une mise à jour automatique 
* Une fois que vous êtes plus de 500 lignes avoir tooadd de 500 lignes supplémentaires + 20 % de la taille de hello de table de hello avant que vous verrez une mise à jour automatique des statistiques de hello de

Comme il n’existe aucun toodetermine DMV si les données dans la table de hello ont changé dans la mesure où les mises à jour les statistiques de temps dernière hello, connaître l’ancienneté hello de vos statistiques peut vous permettent de partie de l’image de hello.  Vous pouvez utiliser hello suivant toodetermine hello dernière vos statistiques de requête lorsque la mise à jour sur chaque table.  

> [!NOTE]
> N’oubliez pas que s’il existe une modification significative de la distribution de hello des valeurs pour une colonne donnée, vous devez mettre à jour statistiques indépendamment hello dernière, qu'ils ont été mis à jour.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

Par exemple, les statistiques des colonnes de date d’un entrepôt de données doivent souvent être mises à jour. Chaque heure nouvelle sont chargées dans l’entrepôt de données hello, nouvelles dates de la charge ou les dates de transaction sont ajoutés. Modifier la distribution des données hello et les rendre les statistiques hello obsolètes.  À l’inverse, des statistiques sur une colonne sexe sur une table ne peuvent jamais besoin toobe mis à jour. En supposant que la distribution de hello est constante entre les clients, ajout de nouveaux variation de la table toohello lignes ne va pas la distribution des données toochange hello. Toutefois, si votre entrepôt de données ne contient qu’un sexe et une nouvelle spécification entraîne plusieurs sexes, vous définitivement devez tooupdate des statistiques sur la colonne de genre hello.

Pour en savoir plus, consultez la section [Statistiques][Statistics] de MSDN.

## <a name="implementing-statistics-management"></a>Implémentation de fonctions de gestion des statistiques
Il est souvent une bonne idée tooextend votre tooensure processus mises à jour des statistiques au niveau de chargement des données hello fin du chargement de hello. chargement des données Hello est lorsque les tables changent plus souvent leur taille et/ou la répartition des valeurs. Par conséquent, il s’agit d’un tooimplement emplacement logique des processus de gestion.

Certains principes sont fournies ci-dessous pour mettre à jour vos statistiques au cours du processus de chargement hello :

* Assurez-vous que chaque table chargée présente au moins un objet de statistiques mis à jour. Les tables cette hello mises à jour les informations de taille (nombre de lignes et le nombre de pages) dans le cadre de la mise à jour des statistiques de hello.
* Concentrez-vous sur les colonnes participant aux clauses JOIN, GROUP BY, ORDER BY et DISTINCT.
* Envisagez la mise à jour de « par ordre croissant de clé » des colonnes telles que les transactions plus fréquemment car ces valeurs ne seront pas inclus dans l’histogramme des statistiques de hello des dates.
* Envisagez de mettre moins souvent à jour les colonnes de distribution statiques.
* N’oubliez pas que chaque objet de statistiques est mis à jour à son tour. L’implémentation de l’élément `UPDATE STATISTICS <TABLE_NAME>` peut ne pas suffire, notamment lorsque les tables sont volumineuses et incluent un grand nombre d’objets de statistiques.

> [!NOTE]
> Pour plus d’informations sur [croissant clé] consultez toohello SQL Server 2014 livre blanc estimation de la cardinalité.
> 
> 

Pour en savoir plus, consultez la section [Estimation de la cardinalité][Cardinality Estimation] de MSDN.

## <a name="examples-create-statistics"></a>Exemples de création de statistiques
Ces exemples montrent comment toouse diverses options pour la création de statistiques. options de Hello que vous utilisez pour chaque colonne dépendent de caractéristiques hello de vos données et comment hello colonne sera utilisée dans les requêtes.

### <a name="a-create-single-column-statistics-with-default-options"></a>R : Créer des statistiques sur une colonne en utilisant les options par défaut
toocreate des statistiques sur une colonne, il suffit de fournir un nom pour l’objet de statistiques hello et hello de colonne de hello.

Cette syntaxe utilise toutes les options par défaut de hello. Par défaut, SQL Data Warehouse exemples 20 pour cent de la table de hello lorsqu’il crée des statistiques.

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

Par exemple :

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. Créer des statistiques sur plusieurs colonnes en examinant chaque ligne
taux d’échantillonnage par défaut Hello de 20 % est suffisant pour la plupart des situations. Toutefois, vous pouvez ajuster les taux d’échantillonnage de hello.

hello toosample complète de table, utilisez la syntaxe suivante :

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

Par exemple :

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. Créer des statistiques de colonne unique en spécifiant la taille de l’exemple hello
Vous pouvez également spécifier la taille de l’exemple hello sous forme de pourcentage :

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. Créer des statistiques de colonne unique sur certaines lignes de hello
Une autre option, vous pouvez créer des statistiques sur une partie des lignes de hello dans votre table. On parle alors de « statistiques filtrées ».

Par exemple, vous pouvez utiliser les statistiques filtrées lorsque vous planifiez tooquery une partition spécifique d’une grande table partitionnée. En créant des statistiques sur hello uniquement les valeurs de partition, précision hello de statistiques de hello améliorer et par conséquent, améliorer les performances des requêtes.

Dans cet exemple, des statistiques sont créées sur une plage de valeurs. les valeurs Hello peut être défini de plage de hello toomatch de valeurs dans une partition.

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Pour hello tooconsider d’optimiseur de requête à l’aide de statistiques filtrées lorsqu’il choisit le plan de requête distribuée hello, requête de hello doit tenir dans la définition de hello hello d’objet de statistiques. À l’aide de hello précédent exemple, hello la requête où clause a besoin de valeurs de col1 toospecify entre 2000101 et 20001231.
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. Créer des statistiques de colonne unique avec toutes les options de hello
Vous pouvez, bien entendu, de combiner les options hello. exemple Hello ci-dessous crée un objet de statistiques filtrées avec une taille d’échantillon personnalisé :

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

Pour la référence complète de hello, consultez [CREATE STATISTICS] [ CREATE STATISTICS] sur MSDN.

### <a name="f-create-multi-column-statistics"></a>F. Créer des statistiques sur plusieurs colonnes
toocreate un statistiques multicolonnes, simplement utiliser les exemples précédents hello, mais spécifier plus de colonnes.

> [!NOTE]
> Histogramme Hello, qui est utilisé tooestimate nombre de lignes dans le résultat de la requête hello, est uniquement disponible pour hello première colonne répertorié dans la définition de l’objet statistiques hello.
> 
> 

Dans cet exemple, histogramme de hello est sur *produit\_catégorie*. Les statistiques portant sur différentes colonnes sont calculées sur la base des éléments *product\_category* et *product\_sub_c\ategory* :

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

Dans la mesure où il existe une corrélation entre *produit\_catégorie* et *produit\_sub\_catégorie*, un état à plusieurs colonne peut être utile si ces colonnes sont accessibles. à hello même temps.

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>G. Créer des statistiques sur toutes les colonnes hello dans une table
Statistiques d’une façon toocreate sont tooissues les commandes CREATE STATISTICS après avoir créé la table de hello.

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>H. Utilisez une statistiques toocreate de procédure stockée sur toutes les colonnes dans une base de données
Entrepôt de données SQL n’a pas un équivalent de la procédure stockée système trop [] de [sp_create_stats] dans SQL Server. Cette procédure stockée crée un objet de statistiques de colonne unique sur chaque colonne de base de données hello qui ne possède pas de statistiques.

Cela vous aidera à commencer à concevoir votre base de données. Pensez tooadapt libre il tooyour a besoin.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

toocreate des statistiques sur toutes les colonnes de table hello avec cette procédure, appelez simplement la procédure de hello.

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>Exemple de mise à jour des statistiques
statistiques de tooupdate, vous pouvez :

1. Mettez à jour un objet de statistiques. Spécifiez nom hello Hello vous souhaitez tooupdate de l’objet de statistiques.
2. Mettez à jour tous les objets de statistiques sur une table. Spécifiez nom hello de table hello au lieu d’un objet de statistiques spécifiques.

### <a name="a-update-one-specific-statistics-object"></a>R : Mettre à jour un objet de statistiques spécifique
Utilisez hello suivant de syntaxe tooupdate un objet de statistiques spécifique :

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

Par exemple :

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

En mettant à jour les objets de statistiques spécifique, vous pouvez réduire hello temps et des ressources requises toomanage des statistiques. Cela requiert que certains considéré, bien que, toochoose hello meilleures statistiques objets tooupdate.

### <a name="b-update-all-statistics-on-a-table"></a>B. Mettre à jour tous les objets de statistiques dans une table
Voici une méthode simple pour mettre à jour tous les objets de statistiques hello sur une table.

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

Par exemple :

```sql
UPDATE STATISTICS dbo.table1;
```

Cette instruction est toouse facile. N’oubliez pas que cela met à jour toutes les statistiques sur la table de hello et par conséquent peut travailler plus qu’il n’est nécessaire. Si les performances hello ne sont pas un problème, cela est moyen plus simple et la plus complète hello tooguarantee statistiques sont à jour.

> [!NOTE]
> Lors de la mise à jour toutes les statistiques d’une table, l’entrepôt de données SQL est une table de hello toosample analyse pour chaque statistiques. Si la table de hello est volumineuse, a le nombre de colonnes et de nombreuses statistiques, il peut être plus efficace tooupdate individuels des statistiques en fonction des besoins.
> 
> 

Pour une implémentation d’un `UPDATE STATISTICS` procédure consultez hello [Tables temporaires] [ Temporary] l’article. méthode d’implémentation Hello est légèrement différent toohello `CREATE STATISTICS` procédure ci-dessus, mais le résultat final de hello est hello identiques.

Pour la syntaxe complète de hello, consultez [Update Statistics] [ Update Statistics] sur MSDN.

## <a name="statistics-metadata"></a>Métadonnées de statistiques
Il existe plusieurs vue système et fonctions que vous pouvez utiliser toofind des informations sur les statistiques. Par exemple, vous pouvez voir si un objet de statistiques sont obsolète à l’aide de hello statistiques-date fonction toosee lorsque les statistiques de dernière création ou mise à jour.

### <a name="catalog-views-for-statistics"></a>Vues de catalogue des statistiques
Ces vues système fournissent des informations sur les statistiques :

| Vue de catalogue | Description |
|:--- |:--- |
| [sys.columns][sys.columns] |Une ligne pour chaque colonne. |
| [sys.objects][sys.objects] |Une ligne pour chaque objet de base de données hello. |
| [sys.schemas][sys.schemas] |Une ligne pour chaque schéma de base de données hello. |
| [sys.stats][sys.stats] |Une ligne pour chaque objet de statistiques. |
| [sys.stats_columns][sys.stats_columns] |Une ligne pour chaque colonne dans l’objet de statistiques hello. Revient toosys.columns. |
| [sys.tables][sys.tables] |Une ligne pour chaque table (y compris les tables externes). |
| [sys.table_types][sys.table_types] |Une ligne pour chaque type de données. |

### <a name="system-functions-for-statistics"></a>Fonctions système relatives aux statistiques
Ces fonctions système sont utiles lorsque vous gérez des statistiques :

| Fonction système | Description |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |Objet de statistiques hello date a été modifié. |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Fournit des informations de résumé et détaillées sur la distribution des valeurs de hello comme comprise par l’objet de statistiques hello. |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>Combiner des fonctions et des colonnes de statistiques en une seule vue
Cette vue affiche les colonnes liées ensemble toostatistics et les résultats à partir de la fonction de hello [STATS_DATE()] [].

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>Exemples portant sur la fonction DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() affiche les données de hello contenues dans un objet de statistiques. Ces données sont affichées en trois parties.

1. En-tête
2. Vecteur de densité
3. Histogramme

métadonnées d’en-tête Hello sur les statistiques de hello. histogramme de Hello affiche la distribution hello des valeurs dans la première colonne clé hello hello d’objet de statistiques. vecteur de densité Hello mesure la corrélation entre les colonnes. SQLDW calcule les estimations de cardinalité avec les données hello dans l’objet de statistiques hello.

### <a name="show-header-density-and-histogram"></a>Afficher l’en-tête, la densité et l’histogramme
Cet exemple simple illustre les trois parties d’un objet de statistiques.

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

Par exemple :

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>Afficher une ou plusieurs parties de la fonction DBCC SHOW_STATISTICS();
Si vous êtes uniquement intéressé par des composants spécifiques, utilisez hello `WITH` clause et spécifiez ce qui les parties que vous voulez toosee :

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

Par exemple :

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>Différences liées à la fonction DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() est plus strictement implémenté dans SQL Data Warehouse comparées tooSQL Server.

1. Les fonctions non documentées ne sont pas prises en charge.
2. Impossible d’utiliser le paramètre « Stats_stream ».
3. Impossible de joindre les résultats de sous-ensembles spécifiques de données de statistiques, par exemple : STAT_HEADER JOIN DENSITY_VECTOR.
4. L’élément NO_INFOMSGS ne peut pas être défini pour la suppression des messages.
5. Vous ne pouvez pas placer de crochets autour des noms de statistiques.
6. Impossible d’utiliser les objets de statistiques de colonne noms tooidentify
7. L’erreur personnalisée 2767 n’est pas prise en charge.

## <a name="next-steps"></a>Étapes suivantes
Pour en savoir plus, consultez la section [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] de MSDN.  toolearn, voir les articles hello sur [vue d’ensemble de la Table][Overview], [les Types de données de Table][Data Types], [distribution d’une Table] [ Distribute], [L’indexation d’une Table][Index], [partitionnement d’une Table] [ Partition] et [ Tables temporaires][Temporary].  Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
