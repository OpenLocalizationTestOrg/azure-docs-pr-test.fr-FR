---
title: tables aaaIndexing SQL Data Warehouse | Microsoft Azure
description: "Prise en main de l’indexation de tables dans Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 3e617674-7b62-43ab-9ca2-3f40c41d5a88
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/12/2016
ms.author: shigu;barbkess
ms.openlocfilehash: e614d63c8fb871f2ba388f14576cf9f282d4b818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-tables-in-sql-data-warehouse"></a>Indexation de tables dans SQL Data Warehouse
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

SQL Data Warehouse propose plusieurs options d’indexation, notamment [les index columnstore en cluster][clustered columnstore indexes], [les index en cluster et les index non cluster][clustered indexes and nonclustered indexes].  En outre, il propose aussi une option sans index, également appelée [segment de mémoire][heap].  Cet article traite des avantages de hello de chaque type d’index ainsi que les conseils toogetting hello la plupart des performances de vos index. Consultez [créer une syntaxe de table] [ create table syntax] pour plus d’informations sur la façon de toocreate une table dans l’entrepôt de données SQL.

## <a name="clustered-columnstore-indexes"></a>Index columnstore en cluster
Par défaut, SQL Data Warehouse crée un index columnstore en cluster lorsqu’aucune option d’index n’est spécifiée sur une table. Les tables columnstore en cluster offrent deux hello plus haut niveau de compression de données, ainsi que hello meilleures performances globales des requêtes.  Les tables en cluster seront généralement surpassent les tables cluster d’index ou segment de mémoire et sont généralement hello meilleur choix pour les tables volumineuses.  Pour ces raisons, columnstore en cluster est hello meilleures place toostart lorsque vous n’êtes pas sûr de la façon tooindex votre table.  

toocreate une table columnstore en cluster, spécifiez un INDEX cluster COLUMNSTORE dans la clause WITH de hello simplement ou omettre la clause WITH de hello :

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED COLUMNSTORE INDEX );
```

Il existe quelques scénarios où un columnstore en cluster peut ne pas être pas une bonne option :

* Les tables columnstore ne prennent pas en charge varchar(max), nvarchar(max) et varbinary(max).  Envisagez plutôt les segments de mémoire ou les index en cluster.
* Les tables columnstore peuvent être moins efficaces pour les données temporaires.  Envisagez les segments de mémoire, voire les tables temporaires.
* Petites tables avec moins de 100 millions de lignes.  Envisagez les tables de segments de mémoire.

## <a name="heap-tables"></a>Tables de segments de mémoire
Lorsque vous sont temporairement lancement des données sur SQL Data Warehouse, vous découvrirez peut-être qu’à l’aide d’une table de segment de mémoire effectue hello processus global plus rapidement.  Il s’agit, car les charges tooheaps sont plus rapides que les tables tooindex et dans certains hello cas lecture suivante peut être effectué à partir du cache.  Si vous chargez toostage uniquement de données il avant d’exécuter d’autres transformations, le chargement hello table tooheap de la table sera beaucoup plus rapide que le chargement de hello données tooa en cluster de table columnstore. En outre, le chargement données tooa [table temporaire] [ Temporary] charge beaucoup plus rapidement que le chargement d’un stockage de toopermanent table également.  

Pour les petites tables de choix de moins de 100 millions de lignes, souvent, l’utilisation de tables de segments de mémoire est judicieuse.  Les tables columnstore cluster commencent compression optimal de tooachieve une fois qu’il existe plus de 100 millions de lignes.

toocreate une table de segment de mémoire, spécifiez simplement le segment de mémoire dans la clause WITH de hello :

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( HEAP );
```

## <a name="clustered-and-nonclustered-indexes"></a>Index en cluster et non cluster
Index ordonnés en clusters peuvent surpassent les tables columnstore en cluster lorsqu’une seule ligne doit toobe récupéré rapidement.  Pour les requêtes où une seule ou très peu recherche ligne est tooperformance requis avec une fréquence extrêmes, prenons un index de cluster ou d’un index secondaire non ordonnés en clusters.  Hello inconvénient toousing un index cluster est que seules les requêtes qui utilisent un filtre hautement sélectif sur la colonne d’index cluster hello bénéficient.  filtre de tooimprove sur d’autres colonnes de qu'un index non cluster peut être ajouté tooother colonnes.  Toutefois, chaque index qui est ajouté à la table de tooa ajoutera espace et tooloads de temps de traitement.

toocreate une table d’index cluster, spécifiez simplement l’INDEX cluster dans la clause WITH de hello :

```SQL
CREATE TABLE myTable   
  (  
    id int NOT NULL,  
    lastName varchar(20),  
    zipCode varchar(6)  
  )  
WITH ( CLUSTERED INDEX (id) );
```

tooadd un index non cluster sur une table, utilisez simplement hello selon la syntaxe :

```SQL
CREATE INDEX zipCodeIndex ON t1 (zipCode);
```

## <a name="optimizing-clustered-columnstore-indexes"></a>Optimisation des index columnstore en cluster
Les tables columnstore en cluster sont organisées en données dans les segments.  La qualité élevée de segment est critique tooachieving performances optimales des requêtes sur une table columnstore.  Qualité de segment peut être mesurée par un nombre de lignes dans un groupe de lignes compressés hello.  Qualité de segment est optimale lorsqu’il y a au moins 100 Ko lignes par ligne compressée de groupe et de gagner en performances comme hello nombre de lignes par ligne groupe approche 1 048 576 lignes, hello un groupe de lignes peut contenir la plupart des lignes.

Hello sous vue peut être créé et utilisé sur votre hello de toocompute système lignes moyenne par ligne de groupe et identifier tous les index columnstore cluster optimales.  Hello dernière colonne à cette vue génère en tant qu’instruction SQL qui peut être utilisé toorebuild votre index.

```sql
CREATE VIEW dbo.vColumnstoreDensity
AS
SELECT
        GETDATE()                                                               AS [execution_date]
,       DB_Name()                                                               AS [database_name]
,       s.name                                                                  AS [schema_name]
,       t.name                                                                  AS [table_name]
,    COUNT(DISTINCT rg.[partition_number])                    AS [table_partition_count]
,       SUM(rg.[total_rows])                                                    AS [row_count_total]
,       SUM(rg.[total_rows])/COUNT(DISTINCT rg.[distribution_id])               AS [row_count_per_distribution_MAX]
,    CEILING    ((SUM(rg.[total_rows])*1.0/COUNT(DISTINCT rg.[distribution_id]))/1048576) AS [rowgroup_per_distribution_MAX]
,       SUM(CASE WHEN rg.[State] = 0 THEN 1                   ELSE 0    END)    AS [INVISIBLE_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE 0    END)    AS [INVISIBLE_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 0 THEN rg.[total_rows]     ELSE NULL END)    AS [INVISIBLE_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 1 THEN 1                   ELSE 0    END)    AS [OPEN_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE 0    END)    AS [OPEN_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 1 THEN rg.[total_rows]     ELSE NULL END)    AS [OPEN_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 2 THEN 1                   ELSE 0    END)    AS [CLOSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE 0    END)    AS [CLOSED_rowgroup_rows]
,       MIN(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 2 THEN rg.[total_rows]     ELSE NULL END)    AS [CLOSED_rowgroup_rows_AVG]
,       SUM(CASE WHEN rg.[State] = 3 THEN 1                   ELSE 0    END)    AS [COMPRESSED_rowgroup_count]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE 0    END)    AS [COMPRESSED_rowgroup_rows]
,       SUM(CASE WHEN rg.[State] = 3 THEN rg.[deleted_rows]   ELSE 0    END)    AS [COMPRESSED_rowgroup_rows_DELETED]
,       MIN(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MIN]
,       MAX(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_MAX]
,       AVG(CASE WHEN rg.[State] = 3 THEN rg.[total_rows]     ELSE NULL END)    AS [COMPRESSED_rowgroup_rows_AVG]
,       'ALTER INDEX ALL ON ' + s.name + '.' + t.NAME + ' REBUILD;'             AS [Rebuild_Index_SQL]
FROM    sys.[pdw_nodes_column_store_row_groups] rg
JOIN    sys.[pdw_nodes_tables] nt                   ON  rg.[object_id]          = nt.[object_id]
                                                    AND rg.[pdw_node_id]        = nt.[pdw_node_id]
                                                    AND rg.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_table_mappings] mp                 ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[tables] t                              ON  mp.[object_id]          = t.[object_id]
JOIN    sys.[schemas] s                             ON t.[schema_id]            = s.[schema_id]
GROUP BY
        s.[name]
,       t.[name]
;
```

Maintenant que vous avez créé la vue de hello, exécutez cette requête tooidentify avec des groupes de lignes comportant moins de lignes de 100 Ko.  Bien sûr, vous voudrez seuil de hello tooincrease de 100 Ko si vous cherchez plus la qualité optimale de segment. 

```sql
SELECT    *
FROM    [dbo].[vColumnstoreDensity]
WHERE    COMPRESSED_rowgroup_rows_AVG < 100000
        OR INVISIBLE_rowgroup_rows_AVG < 100000
```

Une fois que vous avez exécuté la requête de hello, vous pouvez commencer toolook les données hello et analyser vos résultats. Ce tableau explique quelles toolook pour dans votre analyse de groupe de lignes.

| Colonne | Comment toouse ces données |
| --- | --- |
| [table_partition_count] |Si la table de hello est partitionnée, vous pouvez attendre toosee nombre du groupe lignes ouvrir plus élevé. Chaque partition de la distribution de hello peut-être, en théorie, un groupe de lignes ouvert associé. Tenez-en compte dans votre analyse. Une petite table a été partitionnée peut être optimisée en supprimant hello partitionnement totalement car cela améliore la compression. |
| [row_count_total] |Nombre total de lignes pour la table de hello. Par exemple, vous pouvez utiliser ce pourcentage de toocalculate valeur de lignes en état de hello compressé. |
| [row_count_per_distribution_MAX] |Si toutes les lignes sont réparties de cette valeur doit être le nombre de cible de hello de lignes par la distribution. Comparez cette valeur avec hello compressed_rowgroup_count. |
| [COMPRESSED_rowgroup_rows] |Nombre total de lignes dans le format de columnstore pour la table de hello. |
| [COMPRESSED_rowgroup_rows_AVG] |Si hello nombre moyen de lignes est considérablement inférieur à hello maximale # de lignes pour un groupe de lignes, envisagez d’utiliser SACT ou toorecompress de ALTER INDEX REBUILD hello des données |
| [COMPRESSED_rowgroup_count] |Nombre de groupes de lignes au format columnstore. Si ce nombre est très élevé dans la table des relations de toohello, il est un indicateur que la densité de columnstore hello est faible. |
| [COMPRESSED_rowgroup_rows_DELETED] |Les lignes sont logiquement supprimées au format columnstore. Si nombre de hello est grande taille de tootable relative, envisagez recréer la partition de hello ou la reconstruction des index de hello comme cela les supprime physiquement. |
| [COMPRESSED_rowgroup_rows_MIN] |Utilisez-le conjointement avec hello AVG et MAX colonnes toounderstand hello plage de valeurs pour les groupes de lignes hello dans le columnstore. Un nombre faible au-dessus du seuil de chargement hello (102 400 par distribution de la partition alignée) suggère que les optimisations sont disponibles dans le chargement des données hello |
| [COMPRESSED_rowgroup_rows_MAX] |Identique à ce qui précède |
| [OPEN_rowgroup_count] |Les groupes de lignes ouverts sont normaux. On peut raisonnablement s’attendre à un groupe de lignes ouvert par distribution de tables (60). Les nombres excessifs suggèrent un chargement des données sur plusieurs partitions de données. Vérifiez les hello partitionnement toomake stratégie qu’il s’agit de son |
| [OPEN_rowgroup_rows] |Chaque groupe de lignes peut contenir 1 048 576 lignes maximum. Utilisez cette valeur toosee remplissage groupes de lignes ouvert hello sont actuellement |
| [OPEN_rowgroup_rows_MIN] |Ouvrez groupes indiquent que les données sont progressif chargées dans la table de hello ou qui hello répandu sur les lignes restantes dans ce groupe de lignes de chargement précédent. Hello utilisez MIN, MAX, AVG toosee de colonnes est sat la quantité de données dans des groupes de lignes ouvert. Pour les tables de petite taille, il peut être 100 % de toutes les données hello ! Dans ce cas tooforce de ALTER INDEX REBUILD hello toocolumnstore de données. |
| [OPEN_rowgroup_rows_MAX] |Identique à ce qui précède |
| [OPEN_rowgroup_rows_AVG] |Identique à ce qui précède |
| [CLOSED_rowgroup_rows] |Examinez les lignes de groupe de ligne hello fermé comme un contrôle de validité. |
| [CLOSED_rowgroup_count] |nombre de Hello de groupes de lignes fermés doit être faible si les sont visibles à tout. Les groupes de lignes fermés peuvent être roups de rowg toocompressed converti à l’aide de hello ALTER INDEX... REORGANISE. Toutefois, cela n’est généralement pas nécessaire. Groupes fermés sont automatiquement convertis toocolumnstore des groupes de lignes par processus de « moteur de tuple » hello en arrière-plan. |
| [CLOSED_rowgroup_rows_MIN] |Les groupes de lignes fermés doivent avoir un taux de remplissage très élevé. Si le taux de remplissage hello pour un groupe de lignes fermés est faible, une analyse plus approfondie de hello columnstore est requise. |
| [CLOSED_rowgroup_rows_MAX] |Identique à ce qui précède |
| [CLOSED_rowgroup_rows_AVG] |Identique à ce qui précède |
| [Rebuild_Index_SQL] |Index de columnstore toorebuild SQL pour une table |

## <a name="causes-of-poor-columnstore-index-quality"></a>Causes de la qualité médiocre des index columnstore
Si vous avez identifié les tables avec une qualité médiocre de segment, vous devez la cause première tooidentify hello.  Voici quelques causes courantes d’une qualité médiocre des segments :

1. Saturation de la mémoire lors de la construction de l’index
2. Volume élevé d’opérations DML
3. Opérations de chargement progressives ou légères
4. Nombre trop important de partitions

Ces facteurs peuvent provoquer un toohave d’index columnstore considérablement inférieur au hello optimale 1 million de lignes par groupe de lignes.  Ils peuvent également entraîner le groupe de lignes delta lignes toogo toohello au lieu d’un groupe de lignes compressé. 

### <a name="memory-pressure-when-index-was-built"></a>Saturation de la mémoire lors de la construction de l’index
nombre de Hello de lignes par groupe de lignes compressés ont une largeur de ligne de hello toohello directement liées et hello la quantité de mémoire disponibles tooprocess hello groupe de lignes.  Lors de l’écriture des lignes dans les tables toocolumnstore sollicitation de la mémoire, qualité de segment columnstore risquent d’en pâtir.  Par conséquent, hello meilleure pratique consiste aux session hello toogive qui écrit des tables d’index columnstore tooyour accéder tooas quantité de mémoire que possible.  Dans la mesure où il existe un compromis entre la mémoire et d’accès concurrentiel, conseils hello sur hello droite mémoire allocation dépend des données hello dans chaque ligne de votre table, la quantité de hello de DWU vous avez alloué tooyour système et d’emplacements de quantité hello d’accès concurrentiel vous permettent de toohello session qui est l’écriture de table de données tooyour.  Comme meilleure pratique, nous vous recommandons de commencer les avec xlargerc si vous utilisez DW300 ou moins, largerc si vous utilisez DW400 tooDW600 et mediumrc si vous utilisez DW1000 et versions ultérieures.

### <a name="high-volume-of-dml-operations"></a>Volume élevé d’opérations DML
Un volume élevé d’opérations DML mettre à jour et supprimer des lignes peut introduire des complications dans hello columnstore. Cela est particulièrement vrai lorsque la majorité de hello de lignes hello dans un groupe de lignes sont modifiées.

* Suppression d’une ligne à partir d’un groupe de lignes compressés uniquement logiquement de marque la ligne de hello comme étant supprimé. ligne de Hello reste dans le groupe de lignes compressé de hello jusqu'à la régénération de partition de hello ou une table.
* Insertion d’une ligne ajoute appelée un groupe de lignes delta pour la table hello ligne tootooan rowstore interne. ligne de Hello inséré n’est pas converti toocolumnstore jusqu'à ce que le groupe de lignes delta hello est plein et qu’il est marqué comme étant fermé. Groupes de lignes sont fermés une fois qu’ils atteignent la capacité maximale de hello de 1 048 576 lignes. 
* La mise à jour d’une ligne au format columnstore est traitée en tant que suppression logique, puis en tant qu’insertion. ligne de Hello insérée peut-être être stockée dans le magasin de delta hello.

Mise à jour groupée et insérer les opérations qui dépassent le seuil de bloc hello de 102 400 lignes par partition alignée distribution est écrits directement toohello columnstore mettre en forme. Toutefois, en supposant une distribution uniforme, vous devez modifier plusieurs 6.144 millions de lignes en une seule opération pour cette toooccur de toobe. Si hello nombre de lignes pour une partition donnée aligné de distribution est inférieur à 102 400 lignes de hello sortent banque delta de toohello et sont reste jusqu'à ce que suffisamment de lignes ont été insérées ou modifiées tooclose hello ligne hello ou groupe d’index a été reconstruit.

### <a name="small-or-trickle-load-operations"></a>Opérations de chargement progressives ou légères
Les charges légères entrant dans SQL Data Warehouse sont parfois appelées charges progressives. En général, ils représentent un flux constant proche des données en cours ingérés par le système de hello. Toutefois, comme ce flux est proche de volume hello continue de lignes n’est pas particulièrement volumineux. Plus souvent les données hello sont considérablement inférieure au seuil hello requis pour un format de toocolumnstore charge directe.

Dans ces situations, il est souvent des données de salutation tooland mieux tout d’abord dans le stockage blob Azure et laissez-le s’accumulent tooloading préalable. Cette technique est souvent appelée *micro-batching*ou micro-traitement par lots.

### <a name="too-many-partitions"></a>Nombre trop important de partitions
Une autre chose que tooconsider est impact hello de partitionnement sur les tables columnstore en cluster.  Avant de partitionner, SQL Data Warehouse divise déjà vos données en 60 bases de données.  Un partitionnement plus approfondi divise vos données.  Si vous partitionnez vos données, vous pouvez tooconsider qui **chaque** partition aura besoin toobenefit de lignes toohave au moins 1 million d’un index cluster columnstore.  Si vous partitionnez votre table en 100 partitions, alors que votre table doit toobenefit de lignes toohave au moins 6 milliards d’un index cluster columnstore (60 distributions * 100 partitions * 1 million de lignes). Si votre table de 100 partition n’a pas de 6 milliards de lignes, réduisez le nombre hello de partitions ou envisagez d’utiliser une table de segment de mémoire à la place.

Une fois vos tables ont été chargés avec des données, suivez hello ci-dessous les étapes tooidentify et recréez les tables avec des index columnstore cluster optimales.

## <a name="rebuilding-indexes-tooimprove-segment-quality"></a>La reconstruction de qualité de segment tooimprove index
### <a name="step-1-identify-or-create-user-which-uses-hello-right-resource-class"></a>Étape 1 : Identifier ou créer un utilisateur qui utilise la classe de ressource droite hello
Un moyen rapide tooimmediately améliorer la qualité du segment est un index de hello toorebuild.  Hello SQL retourné par hello au-dessus de vue retourne une instruction ALTER INDEX REBUILD, qui peut être utilisé toorebuild votre index.  Lors de la reconstruction de votre index, assurez-vous d’allouer suffisamment de mémoire toohello session votre index est reconstruit.  toodo, classe de ressource hello augmentation d’un utilisateur qui a un index de hello toorebuild autorisations sur cette valeur minimale recommandée de toohello de table.  classe de ressource Hello de l’utilisateur propriétaire de la base de données hello ne peut pas être modifié, si vous n’avez pas créé un utilisateur sur le système de hello, vous devez tout d’abord toodo.  minimum Hello recommandé est xlargerc si vous utilisez DW300 ou moins, largerc si vous utilisez DW400 tooDW600 et mediumrc si vous utilisez DW1000 et versions ultérieures.

Voici un exemple de procédure tooallocate plus utilisateur tooa de mémoire en augmentant leur classe de ressource.  Pour plus d’informations sur les classes de ressources et comment toocreate un nouvel utilisateur se trouve dans hello [gestion d’accès concurrentiel et la charge de travail] [ Concurrency] l’article.

```sql
EXEC sp_addrolemember 'xlargerc', 'LoadUser'
```

### <a name="step-2-rebuild-clustered-columnstore-indexes-with-higher-resource-class-user"></a>Étape 2 : Reconstruire les index columnstore en cluster avec un utilisateur de la classe de ressources la plus élevée
Ouvrez une session en tant qu’hello utilisateur à l’étape 1 (par exemple, LoadUser), qui est maintenant à l’aide d’une classe de ressource plus élevée et exécutez les instructions ALTER INDEX hello.  Assurez-vous que cet utilisateur possède des tables de toohello d’autorisation ALTER où hello index est reconstruit.  Ces exemples montrent comment toorebuild hello index columnstore entier, ou comment toorebuild une seule partition. Sur des tables volumineuses, il est plus pratiques index toorebuild une seule partition à la fois.

Vous pouvez également, au lieu de reconstruire les index hello, vous pouvez copier hello table tooa nouvelle table à l’aide de [SACT][CTAS].  Quelle méthode est la meilleure ? Pour les gros volumes de données, [CTAS][CTAS] est généralement plus rapide que [ALTER INDEX][ALTER INDEX]. Pour les petits volumes de données, [ALTER INDEX] [ ALTER INDEX] est toouse plus facile et aurez pas besoin de tooswap table de hello.  Consultez **la reconstruction des index avec SACT et le basculement de partition** ci-dessous pour plus d’informations sur la façon dont toorebuild indexe avec SACT.

```sql
-- Rebuild hello entire clustered index
ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD
```

```sql
-- Rebuild a single partition
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5
```

```sql
-- Rebuild a single partition with archival compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE)
```

```sql
-- Rebuild a single partition with columnstore compression
ALTER INDEX ALL ON [dbo].[FactInternetSales] REBUILD Partition = 5 WITH (DATA_COMPRESSION = COLUMNSTORE)
```

La reconstruction d’un index dans SQL Data Warehouse est une opération hors connexion.  Pour plus d’informations sur la reconstruction d’index, consultez hello ALTER INDEX REBUILD section [défragmentation des index Columnstore] [ Columnstore Indexes Defragmentation] et la rubrique syntaxe hello [ALTER INDEX] [ALTER INDEX].

### <a name="step-3-verify-clustered-columnstore-segment-quality-has-improved"></a>Étape 3 : Vérifier que la qualité de segment columnstore en cluster a été améliorée
Relancer la requête hello identifiée de table avec une médiocre qualité de segment et vérifier la qualité de segment a été amélioré.  Si la qualité de segment n’a pas été améliorer, il peut être que des lignes de hello dans votre table soient très larges.  Utilisez une classe de ressources supérieure ou une base de données DWU lors de la reconstruction de vos index.

## <a name="rebuilding-indexes-with-ctas-and-partition-switching"></a>Reconstruire des index avec CTAS et le basculement de partitions
Cet exemple utilise [SACT] [ CTAS] et basculement toorebuild une partition de table de partition. 

```sql
-- Step 1: Select hello partition of data and write it out tooa new table using CTAS
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

-- Step 2: Create a SWITCH out table
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE   1=2 -- Note this table will be empty

-- Step 3: Switch OUT hello data 
ALTER TABLE [dbo].[FactInternetSales] SWITCH PARTITION 2 too [dbo].[FactInternetSales_20000101] PARTITION 2;

-- Step 4: Switch IN hello rebuilt data
ALTER TABLE [dbo].[FactInternetSales_20000101_20010101] SWITCH PARTITION 2 too [dbo].[FactInternetSales] PARTITION 2;
```

Pour plus d’informations sur la recréation des partitions à l’aide de `CTAS`, consultez hello [Partition] [ Partition] l’article.

## <a name="next-steps"></a>Étapes suivantes
toolearn, voir les articles hello sur [vue d’ensemble de la Table][Overview], [les Types de données de Table][Data Types], [distribution d’une Table] [ Distribute], [Partitionnement d’une Table][Partition], [gestion de statistiques de Table] [ Statistics] et [ Tables temporaires][Temporary].  toolearn en savoir plus sur les meilleures pratiques, consultez [meilleures pratiques de l’entrepôt de données SQL][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[ALTER INDEX]: https://msdn.microsoft.com/library/ms188388.aspx
[heap]: https://msdn.microsoft.com/library/hh213609.aspx
[clustered indexes and nonclustered indexes]: https://msdn.microsoft.com/library/ms190457.aspx
[create table syntax]: https://msdn.microsoft.com/library/mt203953.aspx
[Columnstore Indexes Defragmentation]: https://msdn.microsoft.com/library/dn935013.aspx#Anchor_1
[clustered columnstore indexes]: https://msdn.microsoft.com/library/gg492088.aspx

<!--Other Web references-->
