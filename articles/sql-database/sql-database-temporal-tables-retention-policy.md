---
title: "Gérer les données d’historique dans les tables temporelles avec la stratégie de rétention | Microsoft Docs"
description: "Découvrez comment utiliser la stratégie de rétention temporelle pour conserver les données d’historique sous votre contrôle."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: 8975d7a7d39114b2758d64a4df9f992cba6bf561
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="a3f85-103">Gérer les données d’historique dans les tables temporelles avec la stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="a3f85-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="a3f85-104">Par rapport aux tables normales, les tables temporelles peuvent augmenter la taille des bases de données, notamment si vous conservez les données d’historique pendant longtemps.</span><span class="sxs-lookup"><span data-stu-id="a3f85-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="a3f85-105">Par conséquent, une stratégie de rétention des données d’historique est un aspect important de la planification et de la gestion du cycle de vie de chaque table temporelle.</span><span class="sxs-lookup"><span data-stu-id="a3f85-105">Hence, retention policy for historical data is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="a3f85-106">Les tables temporelles dans Azure SQL Database sont fournies avec un mécanisme de rétention facile à utiliser qui vous permet d’accomplir cette tâche.</span><span class="sxs-lookup"><span data-stu-id="a3f85-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="a3f85-107">La rétention d’historique temporelle peut être configurée au niveau de tables spécifiques, ce qui permet aux utilisateurs de créer des stratégies d’ancienneté flexibles.</span><span class="sxs-lookup"><span data-stu-id="a3f85-107">Temporal history retention can be configured at the individual table level, which allows users to create flexible aging polices.</span></span> <span data-ttu-id="a3f85-108">L’application de la rétention temporelle est simple : elle ne requiert qu’un seul paramètre à définir lors de la modification du schéma ou de la création de la table.</span><span class="sxs-lookup"><span data-stu-id="a3f85-108">Applying temporal retention is simple: it requires only one parameter to be set during table creation or schema change.</span></span>

<span data-ttu-id="a3f85-109">Une fois que vous avez défini la stratégie de rétention, Azure SQL Database commence par vérifier régulièrement s’il existe des lignes d’historique éligibles pour le nettoyage automatique des données.</span><span class="sxs-lookup"><span data-stu-id="a3f85-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="a3f85-110">L’identification des lignes correspondantes et leur suppression de la table d’historique se produisent en toute transparence, dans la tâche d’arrière-plan planifiée et exécutée par le système.</span><span class="sxs-lookup"><span data-stu-id="a3f85-110">Identification of matching rows and their removal from the history table occur transparently, in the background task that is scheduled and run by the system.</span></span> <span data-ttu-id="a3f85-111">La condition d’ancienneté des lignes de la table d’historique est vérifiée en fonction de la colonne représentant la fin de la période SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="a3f85-111">Age condition for the history table rows is checked based on the column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="a3f85-112">Par exemple, si la période de rétention est définie sur six mois, les lignes de table éligibles pour le nettoyage répondent à la condition suivante :</span><span class="sxs-lookup"><span data-stu-id="a3f85-112">If retention period, for example, is set to six months, table rows eligible for cleanup satisfy the following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="a3f85-113">Dans l’exemple précédent, nous avons supposé que la colonne **ValidTo** correspond à la fin de la période SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="a3f85-113">In the preceding example, we assumed that **ValidTo** column corresponds to the end of SYSTEM_TIME period.</span></span>

## <a name="how-to-configure-retention-policy"></a><span data-ttu-id="a3f85-114">Configuration d’une stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="a3f85-114">How to configure retention policy?</span></span>
<span data-ttu-id="a3f85-115">Avant de configurer la stratégie de rétention d’une table temporelle, vérifiez si la rétention historique temporelle est activée *au niveau de la base de données*.</span><span class="sxs-lookup"><span data-stu-id="a3f85-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at the database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="a3f85-116">L’indicateur de base de données **is_temporal_history_retention_enabled** est défini sur Activé par défaut, mais les utilisateurs peuvent le modifier avec l’instruction ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="a3f85-116">Database flag **is_temporal_history_retention_enabled** is set to ON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="a3f85-117">Il est automatiquement défini sur Désactivé après une opération de [limite de restauration dans le temps](sql-database-recovery-using-backups.md).</span><span class="sxs-lookup"><span data-stu-id="a3f85-117">It is also automatically set to OFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="a3f85-118">Pour activer le nettoyage de la rétention d’historique temporelle pour votre base de données, exécutez l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="a3f85-118">To enable temporal history retention cleanup for your database, execute the following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="a3f85-119">Vous pouvez configurer la durée de rétention pour les tables temporelles même si **is_temporal_history_retention_enabled** est DÉSACTIVÉ, mais le nettoyage automatique des lignes anciennes n’est pas déclenché dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="a3f85-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="a3f85-120">La stratégie de rétention est configurée lors de la création de table en spécifiant la valeur du paramètre HISTORY_RETENTION_PERIOD :</span><span class="sxs-lookup"><span data-stu-id="a3f85-120">Retention policy is configured during table creation by specifying value for the HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="a3f85-121">Azure SQL Database permet de spécifier la période de rétention à l’aide de différentes unités de temps : JOURS, SEMAINES, MOIS et ANNÉES.</span><span class="sxs-lookup"><span data-stu-id="a3f85-121">Azure SQL Database allows you to specify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="a3f85-122">Si HISTORY_RETENTION_PERIOD est omis, la rétention INFINITE est utilisée.</span><span class="sxs-lookup"><span data-stu-id="a3f85-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="a3f85-123">Vous pouvez également utiliser le mot clé INFINITE de façon explicite.</span><span class="sxs-lookup"><span data-stu-id="a3f85-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="a3f85-124">Dans certains scénarios, vous pouvez configurer la rétention après la création de la table ou pour modifier la valeur configurée précédemment.</span><span class="sxs-lookup"><span data-stu-id="a3f85-124">In some scenarios, you may want to configure retention after table creation, or to change previously configured value.</span></span> <span data-ttu-id="a3f85-125">Dans ce cas, utilisez l’instruction ALTER TABLE :</span><span class="sxs-lookup"><span data-stu-id="a3f85-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="a3f85-126">Le fait de définir SYSTEM_VERSIONING sur Désactivé *ne préserve pas* la valeur de période de rétention.</span><span class="sxs-lookup"><span data-stu-id="a3f85-126">Setting SYSTEM_VERSIONING to OFF *does not preserve* retention period value.</span></span> <span data-ttu-id="a3f85-127">La définition de SYSTEM_VERSIONING sur Activé sans spécifier HISTORY_RETENTION_PERIOD résulte de façon explicite en une période de rétention illimitée (INFINITE).</span><span class="sxs-lookup"><span data-stu-id="a3f85-127">Setting SYSTEM_VERSIONING to ON without HISTORY_RETENTION_PERIOD specified explicitly results in the INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="a3f85-128">Pour vérifier l’état actuel de la stratégie de rétention, utilisez la requête suivante qui joint l’indicateur d’activation de la rétention temporelle au niveau de la base de données avec des périodes de rétention pour les tables individuelles :</span><span class="sxs-lookup"><span data-stu-id="a3f85-128">To review current state of the retention policy, use the following query that joins temporal retention enablement flag at the database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="a3f85-129">Comment SQL Database supprime les anciennes lignes ?</span><span class="sxs-lookup"><span data-stu-id="a3f85-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="a3f85-130">Le processus de nettoyage dépend de la disposition de l’index de la table d’historique.</span><span class="sxs-lookup"><span data-stu-id="a3f85-130">The cleanup process depends on the index layout of the history table.</span></span> <span data-ttu-id="a3f85-131">Il est important de noter que *seules les tables d’historique avec un index cluster (B-tree ou columnstore) peuvent avoir une stratégie de rétention limitée configurée*.</span><span class="sxs-lookup"><span data-stu-id="a3f85-131">It is important to notice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="a3f85-132">Une tâche en arrière-plan est créée pour effectuer le nettoyage des anciennes données pour toutes les tables temporelles avec une période de rétention limitée.</span><span class="sxs-lookup"><span data-stu-id="a3f85-132">A background task is created to perform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="a3f85-133">La logique de nettoyage de l’index cluster rowstore (B-tree) supprime les anciennes lignes dans des blocs plus petits (jusqu’à 10 K) en réduisant la pression sur le journal de la base de données et le sous-système d’E/S.</span><span class="sxs-lookup"><span data-stu-id="a3f85-133">Cleanup logic for the rowstore (B-tree) clustered index deletes aged row in smaller chunks (up to 10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="a3f85-134">Bien que la logique de nettoyage utilise l’index B-tree, l’ordre des suppressions de lignes antérieures à la période de rétention ne peut pas être garanti complètement.</span><span class="sxs-lookup"><span data-stu-id="a3f85-134">Although cleanup logic utilizes required B-tree index, order of deletions for the rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="a3f85-135">Par conséquent, *ne dépendez pas de l’ordre de nettoyage dans vos applications*.</span><span class="sxs-lookup"><span data-stu-id="a3f85-135">Hence, *do not take any dependency on the cleanup order in your applications*.</span></span>

<span data-ttu-id="a3f85-136">La tâche de nettoyage pour le cluster columnstore supprime l’ensemble [des groupes de lignes](https://msdn.microsoft.com/library/gg492088.aspx) en une fois (ceux-ci contiennent généralement 1 million de lignes chacun), ce qui est très efficace, en particulier lorsque les données d’historique sont générées à un rythme élevé.</span><span class="sxs-lookup"><span data-stu-id="a3f85-136">The cleanup task for the clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Rétention de cluster columnstore](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="a3f85-138">Une compression des données performante et un nettoyage efficace de la rétention font des index cluster columnstore un choix idéal pour les scénarios dans lesquels votre charge de travail génère rapidement de gros volumes de données d’historique.</span><span class="sxs-lookup"><span data-stu-id="a3f85-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="a3f85-139">Ce modèle est généralement utilisé pour les [charges de travail de traitement transactionnel intensives qui utilisent des tables temporelles](https://msdn.microsoft.com/library/mt631669.aspx) à des fins de suivi des modifications et l’audit, d’analyse de tendances ou d’ingestion des données IoT.</span><span class="sxs-lookup"><span data-stu-id="a3f85-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="a3f85-140">Considérations relatives aux index</span><span class="sxs-lookup"><span data-stu-id="a3f85-140">Index considerations</span></span>
<span data-ttu-id="a3f85-141">La tâche de nettoyage des tables avec un index cluster rowstore requiert que l’index démarre avec la colonne correspondant à la fin de la période SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="a3f85-141">The cleanup task for tables with rowstore clustered index requires index to start with the column corresponding the end of SYSTEM_TIME period.</span></span> <span data-ttu-id="a3f85-142">Si cet index n’existe pas, vous ne pouvez pas configurer de période de rétention limitée :</span><span class="sxs-lookup"><span data-stu-id="a3f85-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="a3f85-143">*Msg 13765, niveau 16, état 1 <br></br> Échec de la définition d’une période de rétention limitée sur la table temporelle avec version gérée par le système « temporalstagetestdb.dbo.WebsiteUserInfo », car la table d’historique 'temporalstagetestdb.dbo.WebsiteUserInfoHistory » ne contient pas l’index cluster nécessaire. Vous devez créer un index cluster columnstore ou d’arbre B dans lequel la première colonne correspond à la fin de la période SYSTEM_TIME, sur la table d'historique.*</span><span class="sxs-lookup"><span data-stu-id="a3f85-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because the history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with the column that matches end of SYSTEM_TIME period, on the history table.*</span></span>

<span data-ttu-id="a3f85-144">Il est important de noter que la table d’historique par défaut déjà créée par Azure SQL Database a un index cluster, ce qui est compatible avec la stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="a3f85-144">It is important to notice that the default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="a3f85-145">Si vous essayez de supprimer cet index sur une table avec une période de rétention limitée, l’opération échoue avec l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="a3f85-145">If you try to remove that index on a table with finite retention period, operation fails with the following error:</span></span>

<span data-ttu-id="a3f85-146">*Msg 13766, niveau 16, état 1 <br></br> Impossible de supprimer l’index cluster « WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory », car il est utilisé pour le nettoyage automatique des données anciennes. Pour supprimer cet index, attribuez la valeur INFINITE à HISTORY_RETENTION_PERIOD sur la table temporelle avec version gérée par le système correspondante.*</span><span class="sxs-lookup"><span data-stu-id="a3f85-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop the clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD to INFINITE on the corresponding system-versioned temporal table if you need to drop this index.*</span></span>

<span data-ttu-id="a3f85-147">Le nettoyage de l’index cluster columnstore fonctionne de façon optimale si des lignes d’historique sont insérées dans l’ordre croissant (par la fin de la colonne de période), ce qui est toujours le cas lorsque la table d’historique est remplie exclusivement par le mécanisme SYSTEM_VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="a3f85-147">Cleanup on the clustered columnstore index works optimally if historical rows are inserted in the ascending order (ordered by the end of period column), which is always the case when the history table is populated exclusively by the SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="a3f85-148">Si les lignes de la table d’historique ne sont pas ordonnées par la fin de la colonne de période (ce qui peut arriver si vous avez migré des données d’historique existantes), vous devez recréer les index cluster columnstore sur les index d’arbre B rowstore correctement triés, pour optimiser les performances.</span><span class="sxs-lookup"><span data-stu-id="a3f85-148">If rows in the history table are not ordered by end of period column (which may be the case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, to achieve optimal performance.</span></span>

<span data-ttu-id="a3f85-149">Évitez de reconstruire l’index cluster columnstore sur la table d’historique avec la période de rétention limitée, car cela risque de modifier l’ordre des groupes de lignes naturellement imposé par l’opération de système de version.</span><span class="sxs-lookup"><span data-stu-id="a3f85-149">Avoid rebuilding clustered columnstore index on the history table with the finite retention period, because it may change ordering in the row groups naturally imposed by the system-versioning operation.</span></span> <span data-ttu-id="a3f85-150">Si vous devez reconstruire l’index cluster columnstore sur la table d’historique, faites-le en le recréant par-dessus l’index d’arbre B conforme, en conservant l’ordre des groupes de lignes nécessaire au nettoyage de données standard.</span><span class="sxs-lookup"><span data-stu-id="a3f85-150">If you need to rebuild clustered columnstore index on the history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in the rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="a3f85-151">La même approche convient si vous créez la table temporelle avec une table d’historique existante qui a un index de colonne cluster sans ordre de données garanti :</span><span class="sxs-lookup"><span data-stu-id="a3f85-151">The same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by the end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="a3f85-152">Lorsque la période de rétention limitée est configurée pour la table d’historique avec l’index cluster columnstore, vous ne pouvez pas créer d’index d’arbre B supplémentaire non cluster sur cette table :</span><span class="sxs-lookup"><span data-stu-id="a3f85-152">When finite retention period is configured for the history table with the clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="a3f85-153">Une tentative d’exécution de l’instruction ci-dessus échoue avec l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="a3f85-153">An attempt to execute above statement fails with the following error:</span></span>

<span data-ttu-id="a3f85-154">*Msg 13772, niveau 16, état 1 <br></br> Impossible de créer un index non cluster sur la table d’historique temporelle « WebsiteUserInfoHistory » car celle-ci est définie avec une période de rétention limitée et un index cluster columnstore.*</span><span class="sxs-lookup"><span data-stu-id="a3f85-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="a3f85-155">Interrogation de tables comportant une stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="a3f85-155">Querying tables with retention policy</span></span>
<span data-ttu-id="a3f85-156">Toutes les requêtes effectuées sur une table temporelle filtrent automatiquement les lignes d’historique correspondant à la stratégie de rétention limitée, afin d’éviter des résultats imprévisibles et incohérents, étant donné que les anciennes lignes peuvent être supprimées par la tâche de nettoyage, *à n’importe quel point dans le temps et dans un ordre arbitraire*.</span><span class="sxs-lookup"><span data-stu-id="a3f85-156">All queries on the temporal table automatically filter out historical rows matching finite retention policy, to avoid unpredictable and inconsistent results, since aged rows can be deleted by the cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="a3f85-157">L’illustration suivante montre le plan de requête pour une requête simple :</span><span class="sxs-lookup"><span data-stu-id="a3f85-157">The following picture shows the query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="a3f85-158">Le plan de requête inclut un filtre supplémentaire appliqué à la fin de la colonne de période (ValidTo) dans l’opérateur Analyse d’index cluster sur la table d’historique (mise en surbrillance).</span><span class="sxs-lookup"><span data-stu-id="a3f85-158">The query plan includes additional filter applied to end of period column (ValidTo) in the Clustered Index Scan operator on the history table (highlighted).</span></span> <span data-ttu-id="a3f85-159">Cet exemple suppose que la période de rétention d’un MOIS a été définie sur la table WebsiteUserInfo.</span><span class="sxs-lookup"><span data-stu-id="a3f85-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Filtre de requête de rétention](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="a3f85-161">Cependant, si vous interrogez directement la table d’historique, vous pouvez voir des lignes antérieures à la période de rétention spécifiée, mais sans aucune garantie de bénéficier de résultats de requête reproductibles.</span><span class="sxs-lookup"><span data-stu-id="a3f85-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="a3f85-162">L’illustration suivante montre le plan d’exécution de la requête sur la table d’historique sans appliquer de filtres supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="a3f85-162">The following picture shows query execution plan for the query on the history table without additional filters applied:</span></span>

![Interrogation de l’historique sans filtre de rétention](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="a3f85-164">Ne faites pas dépendre votre logique métier sur la lecture de la table d’historique au-delà de la période de rétention, car vous risquez d’obtenir des résultats incohérents ou inattendus.</span><span class="sxs-lookup"><span data-stu-id="a3f85-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="a3f85-165">Nous vous recommandons d’utiliser des requêtes temporelles avec la clause FOR SYSTEM_TIME pour l’analyse des données dans les tables temporelles.</span><span class="sxs-lookup"><span data-stu-id="a3f85-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="a3f85-166">Considérations relatives à la limite de restauration dans le temps</span><span class="sxs-lookup"><span data-stu-id="a3f85-166">Point in time restore considerations</span></span>
<span data-ttu-id="a3f85-167">Lorsque vous créez une base de données en [restaurant une base de données existante à un point spécifique dans le temps](sql-database-recovery-using-backups.md), sa rétention temporelle est désactivée au niveau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="a3f85-167">When you create new database by [restoring existing database to a specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at the database level.</span></span> <span data-ttu-id="a3f85-168">L’indicateur **is_temporal_history_retention_enabled** est défini sur Désactivé.</span><span class="sxs-lookup"><span data-stu-id="a3f85-168">(**is_temporal_history_retention_enabled** flag set to OFF).</span></span> <span data-ttu-id="a3f85-169">Cette fonctionnalité vous permet d’examiner toutes les lignes d’historique lors de la restauration, sans craindre que les anciennes lignes soient supprimées avant qu’elles aient été interrogées.</span><span class="sxs-lookup"><span data-stu-id="a3f85-169">This functionality allows you to examine all historical rows upon restore, without worrying that aged rows are removed before you get to query them.</span></span> <span data-ttu-id="a3f85-170">Vous pouvez l’utiliser pour *inspecter les données d’historique au-delà de la période de rétention configurée*.</span><span class="sxs-lookup"><span data-stu-id="a3f85-170">You can use it to *inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="a3f85-171">Supposons qu’une table temporelle a une période de rétention de un MOIS.</span><span class="sxs-lookup"><span data-stu-id="a3f85-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="a3f85-172">Si votre base de données a été créée dans le niveau de service Premium, vous ne pouvez pas créer de copie de base de données avec l’état de la base de données jusqu’à 35 jours dans le passé.</span><span class="sxs-lookup"><span data-stu-id="a3f85-172">If your database was created in Premium Service tier, you would be able to create database copy with the database state up to 35 days back in the past.</span></span> <span data-ttu-id="a3f85-173">Cela vous permet d’analyser avec efficacité les lignes d’historique qui sont anciennes de moins de 65 jours en interrogeant la table d’historique directement.</span><span class="sxs-lookup"><span data-stu-id="a3f85-173">That effectively would allow you to analyze historical rows that are up to 65 days old by querying the history table directly.</span></span>

<span data-ttu-id="a3f85-174">Si vous souhaitez activer le nettoyage de la rétention temporelle, exécutez l’instruction Transact-SQL suivante après le point de restauration dans le temps :</span><span class="sxs-lookup"><span data-stu-id="a3f85-174">If you want to activate temporal retention cleanup, run the following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="a3f85-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3f85-175">Next steps</span></span>
<span data-ttu-id="a3f85-176">Pour apprendre à utiliser les tables temporelles dans vos applications, consultez [Prise en main des tables temporelles dans Azure SQL Database](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="a3f85-176">To learn how to use Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="a3f85-177">Visitez Channel 9 pour écouter le [témoignage d’un client sur l’implémentation temporelle](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) et regardez une [démonstration de table temporelle en direct](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="a3f85-177">Visit Channel 9 to hear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="a3f85-178">Pour plus d’informations sur les tables temporelles, consultez la [documentation MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3f85-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

