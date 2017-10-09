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
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="59a13-103">Tables temporaires dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="59a13-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="59a13-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="59a13-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="59a13-105">[Types de données][Data Types]</span><span class="sxs-lookup"><span data-stu-id="59a13-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="59a13-106">[Distribuer][Distribute]</span><span class="sxs-lookup"><span data-stu-id="59a13-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="59a13-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="59a13-107">[Index][Index]</span></span>
> * <span data-ttu-id="59a13-108">[Partition][Partition]</span><span class="sxs-lookup"><span data-stu-id="59a13-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="59a13-109">[Statistiques][Statistics]</span><span class="sxs-lookup"><span data-stu-id="59a13-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="59a13-110">[Temporaire][Temporary]</span><span class="sxs-lookup"><span data-stu-id="59a13-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="59a13-111">Les tables temporaires sont très utiles lors du traitement de données - en particulier au cours de la transformation où les résultats intermédiaires hello sont temporaires.</span><span class="sxs-lookup"><span data-stu-id="59a13-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="59a13-112">Dans l’entrepôt de données SQL des tables temporaires existent au niveau de session hello.</span><span class="sxs-lookup"><span data-stu-id="59a13-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="59a13-113">Ils sont uniquement visibles toohello session dans laquelle ils ont été créés et sont automatiquement supprimés lorsque cette session se déconnecte.</span><span class="sxs-lookup"><span data-stu-id="59a13-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="59a13-114">Tables temporaires offrent un gain de performances, car leurs résultats sont écrits toolocal plutôt que le stockage étendu.</span><span class="sxs-lookup"><span data-stu-id="59a13-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="59a13-115">Les tables temporaires sont légèrement différentes dans l’entrepôt de données SQL Azure de base de données SQL Azure comme ils sont accessibles à partir de n’importe où à l’intérieur de session hello, y compris à l’intérieur et en dehors d’une procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="59a13-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="59a13-116">Cet article contient des conseils essentiels pour l’utilisation de tables temporaires et met en évidence les principes de hello de tables temporaires de niveau de session.</span><span class="sxs-lookup"><span data-stu-id="59a13-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="59a13-117">À l’aide des informations de hello dans cet article, vous pouvez moduler votre code, améliorer la réutilisabilité et facilité de maintenance de votre code.</span><span class="sxs-lookup"><span data-stu-id="59a13-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="59a13-118">Créer une table temporaire</span><span class="sxs-lookup"><span data-stu-id="59a13-118">Create a temporary table</span></span>
<span data-ttu-id="59a13-119">Les tables temporaires sont créées en faisant simplement précéder le nom de votre table de `#`.</span><span class="sxs-lookup"><span data-stu-id="59a13-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="59a13-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="59a13-120">For example:</span></span>

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

<span data-ttu-id="59a13-121">Les tables temporaires peuvent également être créés avec un `CTAS` à l’aide de hello exactement la même approche :</span><span class="sxs-lookup"><span data-stu-id="59a13-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

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
> <span data-ttu-id="59a13-122">`CTAS`est une commande très puissante et a hello ajouté avantage d’être très efficace dans son utilisation de l’espace du journal des transactions.</span><span class="sxs-lookup"><span data-stu-id="59a13-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="59a13-123">Suppression de tables temporaires</span><span class="sxs-lookup"><span data-stu-id="59a13-123">Dropping temporary tables</span></span>
<span data-ttu-id="59a13-124">Lorsqu’une nouvelle session est créée, aucune table temporaire ne doit exister.</span><span class="sxs-lookup"><span data-stu-id="59a13-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="59a13-125">Toutefois, si vous appelez hello même procédure stockée, qui crée un fichier temporaire avec hello même nom, tooensure que votre `CREATE TABLE` instructions réussissent une vérification d’existence préalable simple avec un `DROP` peut être utilisé comme hello exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="59a13-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="59a13-126">Pour le codage de la cohérence, il s’agit d’une bonne pratique toouse ce modèle pour les tables et les tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="59a13-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="59a13-127">Il est également une bonne idée toouse `DROP TABLE` tooremove des tables temporaires lorsque vous avez fini de les utiliser dans votre code.</span><span class="sxs-lookup"><span data-stu-id="59a13-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="59a13-128">Dans le développement de la procédure stockée, il est assez courant toosee hello commandes drop regroupées à fin hello d’une procédure de tooensure que ces objets sont nettoyés.</span><span class="sxs-lookup"><span data-stu-id="59a13-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="59a13-129">Modularisation du code</span><span class="sxs-lookup"><span data-stu-id="59a13-129">Modularizing code</span></span>
<span data-ttu-id="59a13-130">Étant donné que les tables temporaires peuvent être visibles dans une session utilisateur, cela peut être exploitée toohelp modulariser de votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="59a13-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="59a13-131">Par exemple, hello procédure stockée ci-dessous réunit hello recommandée supérieure toogenerate DDL qui met à jour toutes les statistiques dans la base de données hello par nom de statistique.</span><span class="sxs-lookup"><span data-stu-id="59a13-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

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

<span data-ttu-id="59a13-132">À ce stade hello seule action qui s’est produite est la création d’une procédure stockée qui sera hello généré simplement une table temporaire, stats_ddl #, avec des instructions DDL.</span><span class="sxs-lookup"><span data-stu-id="59a13-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="59a13-133">Cette procédure stockée supprime #stats_ddl s’il existe déjà tooensure que n’échoue pas si vous exécutez plusieurs fois dans une session.</span><span class="sxs-lookup"><span data-stu-id="59a13-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="59a13-134">Toutefois, étant donné qu’aucun `DROP TABLE` à fin hello de procédure stockée hello, quand hello procédure stockée se termine, elle laisse les table hello créé afin qu’il puisse être lu en dehors de la procédure stockée hello.</span><span class="sxs-lookup"><span data-stu-id="59a13-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="59a13-135">Dans l’entrepôt de données SQL, contrairement à d’autres bases de données SQL Server, il est possible toouse hello table temporaire en dehors de la procédure hello qui l’a créée.</span><span class="sxs-lookup"><span data-stu-id="59a13-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="59a13-136">Tables temporaires de l’entrepôt de données SQL peuvent être utilisés **n’importe où** au sein de la session de hello.</span><span class="sxs-lookup"><span data-stu-id="59a13-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="59a13-137">Cela peut entraîner des toomore modulaire et facile à gérer le code comme dans hello exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="59a13-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="59a13-138">Limitations relatives aux tables temporaires</span><span class="sxs-lookup"><span data-stu-id="59a13-138">Temporary table limitations</span></span>
<span data-ttu-id="59a13-139">SQL Data Warehouse impose quelques restrictions lors de l’implémentation de tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="59a13-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="59a13-140">Actuellement, seules les tables temporaires de la session sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="59a13-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="59a13-141">Les tables temporaires globales ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="59a13-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="59a13-142">En outre, vous ne pouvez pas créer de vues sur des tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="59a13-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59a13-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59a13-143">Next steps</span></span>
<span data-ttu-id="59a13-144">toolearn, voir les articles hello sur [vue d’ensemble de la Table][Overview], [les Types de données de Table][Data Types], [distribution d’une Table] [ Distribute], [L’indexation d’une Table][Index], [partitionnement d’une Table] [ Partition] et [ Gestion des statistiques de Table][Statistics].</span><span class="sxs-lookup"><span data-stu-id="59a13-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="59a13-145">Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="59a13-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
