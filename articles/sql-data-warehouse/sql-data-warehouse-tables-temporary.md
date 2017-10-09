---
title: tables aaaTemporary SQL Data Warehouse | Documents Microsoft
description: Prise en main des tables temporaires dans Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a>Tables temporaires dans SQL Data Warehouse
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

Les tables temporaires sont très utiles lors du traitement de données - en particulier au cours de la transformation où les résultats intermédiaires hello sont temporaires. Dans l’entrepôt de données SQL des tables temporaires existent au niveau de session hello.  Ils sont uniquement visibles toohello session dans laquelle ils ont été créés et sont automatiquement supprimés lorsque cette session se déconnecte.  Tables temporaires offrent un gain de performances, car leurs résultats sont écrits toolocal plutôt que le stockage étendu.  Les tables temporaires sont légèrement différentes dans l’entrepôt de données SQL Azure de base de données SQL Azure comme ils sont accessibles à partir de n’importe où à l’intérieur de session hello, y compris à l’intérieur et en dehors d’une procédure stockée.

Cet article contient des conseils essentiels pour l’utilisation de tables temporaires et met en évidence les principes de hello de tables temporaires de niveau de session. À l’aide des informations de hello dans cet article, vous pouvez moduler votre code, améliorer la réutilisabilité et facilité de maintenance de votre code.

## <a name="create-a-temporary-table"></a>Créer une table temporaire
Les tables temporaires sont créées en faisant simplement précéder le nom de votre table de `#`.  Par exemple :

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

Les tables temporaires peuvent également être créés avec un `CTAS` à l’aide de hello exactement la même approche :

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> `CTAS`est une commande très puissante et a hello ajouté avantage d’être très efficace dans son utilisation de l’espace du journal des transactions. 
> 
> 

## <a name="dropping-temporary-tables"></a>Suppression de tables temporaires
Lorsqu’une nouvelle session est créée, aucune table temporaire ne doit exister.  Toutefois, si vous appelez hello même procédure stockée, qui crée un fichier temporaire avec hello même nom, tooensure que votre `CREATE TABLE` instructions réussissent une vérification d’existence préalable simple avec un `DROP` peut être utilisé comme hello exemple ci-dessous :

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

Pour le codage de la cohérence, il s’agit d’une bonne pratique toouse ce modèle pour les tables et les tables temporaires.  Il est également une bonne idée toouse `DROP TABLE` tooremove des tables temporaires lorsque vous avez fini de les utiliser dans votre code.  Dans le développement de la procédure stockée, il est assez courant toosee hello commandes drop regroupées à fin hello d’une procédure de tooensure que ces objets sont nettoyés.

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a>Modularisation du code
Étant donné que les tables temporaires peuvent être visibles dans une session utilisateur, cela peut être exploitée toohelp modulariser de votre code d’application.  Par exemple, hello procédure stockée ci-dessous réunit hello recommandée supérieure toogenerate DDL qui met à jour toutes les statistiques dans la base de données hello par nom de statistique.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

À ce stade hello seule action qui s’est produite est la création d’une procédure stockée qui sera hello généré simplement une table temporaire, stats_ddl #, avec des instructions DDL.  Cette procédure stockée supprime #stats_ddl s’il existe déjà tooensure que n’échoue pas si vous exécutez plusieurs fois dans une session.  Toutefois, étant donné qu’aucun `DROP TABLE` à fin hello de procédure stockée hello, quand hello procédure stockée se termine, elle laisse les table hello créé afin qu’il puisse être lu en dehors de la procédure stockée hello.  Dans l’entrepôt de données SQL, contrairement à d’autres bases de données SQL Server, il est possible toouse hello table temporaire en dehors de la procédure hello qui l’a créée.  Tables temporaires de l’entrepôt de données SQL peuvent être utilisés **n’importe où** au sein de la session de hello. Cela peut entraîner des toomore modulaire et facile à gérer le code comme dans hello exemple ci-dessous :

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a>Limitations relatives aux tables temporaires
SQL Data Warehouse impose quelques restrictions lors de l’implémentation de tables temporaires.  Actuellement, seules les tables temporaires de la session sont prises en charge.  Les tables temporaires globales ne sont pas prises en charge.  En outre, vous ne pouvez pas créer de vues sur des tables temporaires.

## <a name="next-steps"></a>Étapes suivantes
toolearn, voir les articles hello sur [vue d’ensemble de la Table][Overview], [les Types de données de Table][Data Types], [distribution d’une Table] [ Distribute], [L’indexation d’une Table][Index], [partitionnement d’une Table] [ Partition] et [ Gestion des statistiques de Table][Statistics].  Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].

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

<!--Other Web references-->
