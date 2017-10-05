---
title: "Tables temporaires dans SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: fd8c31a727dae3b011aa8294a81f005bad72a278
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="3fa0b-103">Tables temporaires dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3fa0b-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3fa0b-104">[Vue d’ensemble][Overview]</span><span class="sxs-lookup"><span data-stu-id="3fa0b-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3fa0b-105">[Types de données][Data Types]</span><span class="sxs-lookup"><span data-stu-id="3fa0b-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="3fa0b-106">[Distribuer][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3fa0b-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="3fa0b-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="3fa0b-107">[Index][Index]</span></span>
> * <span data-ttu-id="3fa0b-108">[Partition][Partition]</span><span class="sxs-lookup"><span data-stu-id="3fa0b-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="3fa0b-109">[Statistiques][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3fa0b-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="3fa0b-110">[Temporaire][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3fa0b-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="3fa0b-111">Les tables temporaires sont très utiles lors du traitement des données, notamment lors d’une transformation, lorsque les résultats intermédiaires sont temporaires.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-111">Temporary tables are very useful when processing data - especially during transformation where the intermediate results are transient.</span></span> <span data-ttu-id="3fa0b-112">Les tables temporaires se trouvent au niveau de la session dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-112">In SQL Data Warehouse temporary tables exist at the session level.</span></span>  <span data-ttu-id="3fa0b-113">Elles sont uniquement visibles dans la session dans laquelle elles ont été créées et sont automatiquement supprimées lorsque cette session se déconnecte.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-113">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="3fa0b-114">Les tables temporaires offrent un gain de performances, car leurs résultats sont écrits en local et non dans un stockage distant.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-114">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span></span>  <span data-ttu-id="3fa0b-115">Dans Azure SQL Data Warehouse, les tables temporaires diffèrent légèrement par rapport à la base de données SQL Azure, car elles sont accessibles à partir de tout point à l’intérieur de la session, notamment à l’intérieur et à l’extérieur d’une procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="3fa0b-116">Cet article contient des conseils de base pour l’utilisation des tables temporaires et met en évidence les principes des tables temporaires au niveau de la session.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-116">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span></span> <span data-ttu-id="3fa0b-117">L’utilisation des informations de cet article peut vous aider à modulariser votre code, et à améliorer sa réutilisabilité et sa facilité de maintenance.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-117">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="3fa0b-118">Créer une table temporaire</span><span class="sxs-lookup"><span data-stu-id="3fa0b-118">Create a temporary table</span></span>
<span data-ttu-id="3fa0b-119">Les tables temporaires sont créées en faisant simplement précéder le nom de votre table de `#`.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="3fa0b-120">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3fa0b-120">For example:</span></span>

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

<span data-ttu-id="3fa0b-121">Vous pouvez également utiliser `CTAS` pour créer des tables temporaires à l’aide de la même approche :</span><span class="sxs-lookup"><span data-stu-id="3fa0b-121">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span></span>

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
> <span data-ttu-id="3fa0b-122">`CTAS` est une commande très puissante et présente l’avantage d’être très efficace dans son utilisation de l’espace de journal des transactions.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-122">`CTAS` is a very powerful command and has the added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="3fa0b-123">Suppression de tables temporaires</span><span class="sxs-lookup"><span data-stu-id="3fa0b-123">Dropping temporary tables</span></span>
<span data-ttu-id="3fa0b-124">Lorsqu’une nouvelle session est créée, aucune table temporaire ne doit exister.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="3fa0b-125">Toutefois, si vous appelez la même procédure stockée, qui crée une table temporaire avec le même nom, pour vous assurer de la réussite de vos instructions `CREATE TABLE`, une simple vérification d’existence préalable avec `DROP` peut être utilisée comme dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3fa0b-125">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="3fa0b-126">Pour la cohérence de codage, il convient d’utiliser ce modèle pour les tables et les tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-126">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="3fa0b-127">Il est également judicieux d’utiliser `DROP TABLE` pour supprimer les tables temporaires lorsque vous avez terminé de les utiliser dans votre code.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-127">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="3fa0b-128">Dans le développement de procédure stockée, il est assez courant de voir les commandes de suppression regroupées ensemble à la fin d’une procédure pour s’assurer que ces objets sont nettoyés.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-128">In stored procedure development it is quite common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="3fa0b-129">Modularisation du code</span><span class="sxs-lookup"><span data-stu-id="3fa0b-129">Modularizing code</span></span>
<span data-ttu-id="3fa0b-130">Étant donné que les tables temporaires peuvent être affichées depuis n’importe quel point d’une session utilisateur, cela peut vous aider à modulariser votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-130">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span></span>  <span data-ttu-id="3fa0b-131">Par exemple, la procédure stockée ci-dessous réunit les pratiques recommandées ci-dessus pour générer le DDL qui va mettre à jour toutes les statistiques dans la base de données par nom de statistique.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-131">For example, the stored procedure below brings together the recommended practices from above to generate DDL which will update all statistics in the database by statistic name.</span></span>

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

<span data-ttu-id="3fa0b-132">À ce stade, la seule action qui s’est produite est la création d’une procédure stockée qui va simplement générer une table temporaire, #stats_ddl, avec des instructions DDL.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-132">At this stage the only action that has occurred is the creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="3fa0b-133">Cette procédure stockée va abandonner la table #stats_ddl si elle existe déjà pour assurer l’absence d’échec en cas d’exécution multiple dans une session.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-133">This stored procedure will drop #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="3fa0b-134">Toutefois, étant donné l’absence de `DROP TABLE` à la fin de la procédure stockée, lorsque la procédure stockée se termine, elle quitte la table créée afin de pouvoir être lue en dehors de la procédure stockée.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-134">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it will leave the created table so that it can be read outside of the stored procedure.</span></span>  <span data-ttu-id="3fa0b-135">Dans SQL Data Warehouse, contrairement à d’autres bases de données SQL, il est possible d’utiliser la table temporaire en dehors de la procédure qui l’a créée.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span></span>  <span data-ttu-id="3fa0b-136">Les tables temporaires SQL Data Warehouse peuvent être utilisées à **n’importe quel point** de la session.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-136">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span></span> <span data-ttu-id="3fa0b-137">Cela peut optimiser la facilité de gestion et la modularité du code comme dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3fa0b-137">This can lead to more modular and manageable code as in the below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="3fa0b-138">Limitations relatives aux tables temporaires</span><span class="sxs-lookup"><span data-stu-id="3fa0b-138">Temporary table limitations</span></span>
<span data-ttu-id="3fa0b-139">SQL Data Warehouse impose quelques restrictions lors de l’implémentation de tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="3fa0b-140">Actuellement, seules les tables temporaires de la session sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="3fa0b-141">Les tables temporaires globales ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="3fa0b-142">En outre, vous ne pouvez pas créer de vues sur des tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="3fa0b-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fa0b-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3fa0b-143">Next steps</span></span>
<span data-ttu-id="3fa0b-144">Pour plus d’informations, consultez les articles [Vue d’ensemble des tables][Overview], [Types de données de table][Data Types], [Distribution d’une table][Distribute], [Indexation d’une table][Index], [Partitionnement d’une table][Partition] et [Maintenance des statistiques de table][Statistics].</span><span class="sxs-lookup"><span data-stu-id="3fa0b-144">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="3fa0b-145">Pour en savoir plus sur les meilleures pratiques, consultez [Meilleures pratiques relatives à SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="3fa0b-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
