---
title: "aaaManage des données historiques dans les Tables temporelles avec la stratégie de rétention | Documents Microsoft"
description: "Découvrez comment toouse rétention temporelle stratégie tookeep données d’historique sous votre contrôle."
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
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="4e105-103">Gérer les données d’historique dans les tables temporelles avec la stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="4e105-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="4e105-104">Par rapport aux tables normales, les tables temporelles peuvent augmenter la taille des bases de données, notamment si vous conservez les données d’historique pendant longtemps.</span><span class="sxs-lookup"><span data-stu-id="4e105-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="4e105-105">Stratégie de rétention pour les données d’historique constitue donc un aspect important de la planification et la gestion du cycle de vie hello de chaque table temporelle.</span><span class="sxs-lookup"><span data-stu-id="4e105-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="4e105-106">Les tables temporelles dans Azure SQL Database sont fournies avec un mécanisme de rétention facile à utiliser qui vous permet d’accomplir cette tâche.</span><span class="sxs-lookup"><span data-stu-id="4e105-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="4e105-107">Rétention de l’historique temporelle peut être configurée au niveau de table individuelle hello, qui permet aux utilisateurs de stratégies de vieillissement de toocreate flexible.</span><span class="sxs-lookup"><span data-stu-id="4e105-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="4e105-108">Application de la rétention temporelle est simple : il ne requiert qu’un seul paramètre toobe définie pendant la modification de la création ou le schéma de table.</span><span class="sxs-lookup"><span data-stu-id="4e105-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="4e105-109">Une fois que vous avez défini la stratégie de rétention, Azure SQL Database commence par vérifier régulièrement s’il existe des lignes d’historique éligibles pour le nettoyage automatique des données.</span><span class="sxs-lookup"><span data-stu-id="4e105-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="4e105-110">Identification des lignes correspondantes et leur suppression à partir de la table d’historique hello se produisent en toute transparence, dans la tâche d’arrière-plan hello est planifiée et exécutée par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="4e105-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="4e105-111">Condition d’âge pour les lignes de la table historique hello est vérifiée en fonction de la colonne hello représentant la fin de la période SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="4e105-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="4e105-112">Si la période de rétention, par exemple, a la valeur toosix mois, les lignes éligibles pour le nettoyage de la table répondent aux hello suivant la condition :</span><span class="sxs-lookup"><span data-stu-id="4e105-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="4e105-113">Bonjour précédent exemple, nous avons supposé que **ValidTo** colonne correspond fin toohello de période SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="4e105-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="4e105-114">La stratégie de rétention tooconfigure ?</span><span class="sxs-lookup"><span data-stu-id="4e105-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="4e105-115">Avant de configurer la stratégie de rétention pour une table temporelle, vérifiez tout d’abord si la rétention historique temporelle est activée *au niveau de base de données hello*.</span><span class="sxs-lookup"><span data-stu-id="4e105-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="4e105-116">Indicateur de base de données **is_temporal_history_retention_enabled** est tooON ensemble par défaut, mais les utilisateurs peuvent les modifier avec l’instruction ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="4e105-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="4e105-117">Il est également automatiquement tooOFF ensemble après [point de restauration dans le temps](sql-database-recovery-using-backups.md) opération.</span><span class="sxs-lookup"><span data-stu-id="4e105-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="4e105-118">nettoyage de rétention d’historique temporelle tooenable pour votre base de données, exécutez hello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="4e105-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="4e105-119">Vous pouvez configurer la durée de rétention pour les tables temporelles même si **is_temporal_history_retention_enabled** est DÉSACTIVÉ, mais le nettoyage automatique des lignes anciennes n’est pas déclenché dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="4e105-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="4e105-120">Stratégie de rétention est configurée lors de la création de table en spécifiant la valeur de paramètre HISTORY_RETENTION_PERIOD hello :</span><span class="sxs-lookup"><span data-stu-id="4e105-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

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

<span data-ttu-id="4e105-121">Base de données SQL Azure vous permet de la période de rétention toospecify à l’aide d’unités de temps différent : jours, semaines, mois et les années.</span><span class="sxs-lookup"><span data-stu-id="4e105-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="4e105-122">Si HISTORY_RETENTION_PERIOD est omis, la rétention INFINITE est utilisée.</span><span class="sxs-lookup"><span data-stu-id="4e105-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="4e105-123">Vous pouvez également utiliser le mot clé INFINITE de façon explicite.</span><span class="sxs-lookup"><span data-stu-id="4e105-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="4e105-124">Dans certains scénarios, vous pouvez tooconfigure rétention après la création de table, ou toochange les valeur configurée précédemment.</span><span class="sxs-lookup"><span data-stu-id="4e105-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="4e105-125">Dans ce cas, utilisez l’instruction ALTER TABLE :</span><span class="sxs-lookup"><span data-stu-id="4e105-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="4e105-126">Définition de SYSTEM_VERSIONING tooOFF *ne conserve pas* valeur de période de rétention.</span><span class="sxs-lookup"><span data-stu-id="4e105-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="4e105-127">Paramètre tooON SYSTEM_VERSIONING sans HISTORY_RETENTION_PERIOD spécifié explicitement des résultats dans la période de rétention infinie hello.</span><span class="sxs-lookup"><span data-stu-id="4e105-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="4e105-128">tooreview état actuel de la stratégie de rétention hello, cet indicateur de l’activation de rétention temporelle jointures au niveau de base de données hello avec des périodes de rétention des tables individuelles de requête suivante de hello d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="4e105-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

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


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="4e105-129">Comment SQL Database supprime les anciennes lignes ?</span><span class="sxs-lookup"><span data-stu-id="4e105-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="4e105-130">processus de nettoyage Hello dépend de la mise en page de hello index de table d’historique hello.</span><span class="sxs-lookup"><span data-stu-id="4e105-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="4e105-131">Il est important toonotice qui *uniquement les tables d’historique avec un index cluster (B-tree ou columnstore) peuvent avoir fini de rétention configurée*.</span><span class="sxs-lookup"><span data-stu-id="4e105-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="4e105-132">Une tâche en arrière-plan est créée de nettoyage des données d’anciennes données tooperform pour toutes les tables temporelles avec la période de rétention limitée.</span><span class="sxs-lookup"><span data-stu-id="4e105-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="4e105-133">Logique de nettoyage pour les index cluster rowstore (B-tree) de hello supprime les anciennes lignes en segments plus petits (haut too10K) en réduisant la pression sur le journal de la base de données et le sous-système d’e/s.</span><span class="sxs-lookup"><span data-stu-id="4e105-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="4e105-134">Bien que la logique de nettoyage utilise requis index B-tree, ordre de suppressions de lignes hello antérieurs à la période de rétention ne peut pas être garantie bien.</span><span class="sxs-lookup"><span data-stu-id="4e105-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="4e105-135">Par conséquent, *ne prennent pas de dépendances sur l’ordre de nettoyage hello dans vos applications*.</span><span class="sxs-lookup"><span data-stu-id="4e105-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="4e105-136">Hello tâche de nettoyage pour hello clusterisé columnstore supprime entière [des groupes de lignes](https://msdn.microsoft.com/library/gg492088.aspx) à la fois (généralement contient 1 million de lignes chacune), qui est très efficace, en particulier lorsque les données d’historique sont générées à un rythme haute.</span><span class="sxs-lookup"><span data-stu-id="4e105-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Rétention de cluster columnstore](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="4e105-138">Une compression des données performante et un nettoyage efficace de la rétention font des index cluster columnstore un choix idéal pour les scénarios dans lesquels votre charge de travail génère rapidement de gros volumes de données d’historique.</span><span class="sxs-lookup"><span data-stu-id="4e105-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="4e105-139">Ce modèle est généralement utilisé pour les [charges de travail de traitement transactionnel intensives qui utilisent des tables temporelles](https://msdn.microsoft.com/library/mt631669.aspx) à des fins de suivi des modifications et l’audit, d’analyse de tendances ou d’ingestion des données IoT.</span><span class="sxs-lookup"><span data-stu-id="4e105-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="4e105-140">Considérations relatives aux index</span><span class="sxs-lookup"><span data-stu-id="4e105-140">Index considerations</span></span>
<span data-ttu-id="4e105-141">tâche de nettoyage Hello pour les tables avec un index cluster rowstore requiert toostart index avec fin correspondantes hello hello colonne de période SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="4e105-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="4e105-142">Si cet index n’existe pas, vous ne pouvez pas configurer de période de rétention limitée :</span><span class="sxs-lookup"><span data-stu-id="4e105-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="4e105-143">*Msg 13765, niveau 16, état 1 <br> </br> période de rétention finie Échec de la définition de table temporelle avec version système « temporalstagetestdb.dbo.WebsiteUserInfo', car la table d’historique hello » temporalstagetestdb.dbo.WebsiteUserInfoHistory' ne contient pas d’index en cluster requis. Envisagez de créer un columnstore en cluster ou un index B-tree en commençant par la colonne hello qui correspond à la fin de SYSTEM_TIME period, sur la table d’historique hello.*</span><span class="sxs-lookup"><span data-stu-id="4e105-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="4e105-144">Il est important de toonotice qui hello table d’historique par défaut déjà créé par la base de données SQL Azure a clustered index, qui est conforme pour la stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="4e105-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="4e105-145">Si vous essayez tooremove cet index sur une table avec une période de rétention finie, opération échoue avec hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="4e105-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="4e105-146">*Msg 13766, niveau 16, état 1 <br> </br> Impossible de supprimer les index de cluster hello 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' car il est utilisé pour le nettoyage automatique des données d’anciennes données. Envisagez de tooINFINITE HISTORY_RETENTION_PERIOD de paramètre sur la table temporelle avec version système correspondant hello si vous avez besoin de toodrop cet index.*</span><span class="sxs-lookup"><span data-stu-id="4e105-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="4e105-147">Fonctionne optimal de nettoyage sur un index columnstore cluster hello historiques lignes sont insérées dans hello par ordre croissant (classée par fin hello de colonne de période), qui est toujours le cas de hello lors de la table d’historique hello est remplie exclusivement par hello système Mécanisme VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="4e105-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="4e105-148">Si les lignes dans la table d’historique hello ne sont pas ordonnés en fin de la colonne de période (qui est peut-être hello cas si vous avez migré des données d’historique existantes), vous devez recréer les index cluster columnstore sur les index B-tree rowstore qui est commandé correctement tooachieve optimal performances.</span><span class="sxs-lookup"><span data-stu-id="4e105-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="4e105-149">Évitez la reconstruction d’index cluster columnstore sur la table d’historique hello avec la période de rétention finie hello, car il peut changer de classement dans les groupes de lignes hello naturellement imposées par l’opération de contrôle de version système hello.</span><span class="sxs-lookup"><span data-stu-id="4e105-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="4e105-150">Si vous avez besoin d’index cluster columnstore de toorebuild sur la table d’historique hello, faire en recréant par-dessus conforme index B-tree, en conservant le classement dans les rowgroups hello nécessaires pour le nettoyage de données standard.</span><span class="sxs-lookup"><span data-stu-id="4e105-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="4e105-151">Hello même approche doit être effectuée si vous créez la table temporelle avec table d’historique existante qui a un index de colonne sans ordre de garantie des données cluster :</span><span class="sxs-lookup"><span data-stu-id="4e105-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="4e105-152">Lors de la période de rétention finie est configurée pour la table d’historique hello avec un index columnstore cluster hello, vous ne peut pas créer des index non cluster B-tree supplémentaires sur cette table :</span><span class="sxs-lookup"><span data-stu-id="4e105-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="4e105-153">Un tooexecute tentative au-dessus instruction échoue avec hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="4e105-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="4e105-154">*Msg 13772, niveau 16, état 1 <br></br> Impossible de créer un index non cluster sur la table d’historique temporelle « WebsiteUserInfoHistory » car celle-ci est définie avec une période de rétention limitée et un index cluster columnstore.*</span><span class="sxs-lookup"><span data-stu-id="4e105-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="4e105-155">Interrogation de tables comportant une stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="4e105-155">Querying tables with retention policy</span></span>
<span data-ttu-id="4e105-156">Toutes les requêtes sur la table temporelle hello éliminer automatiquement les historiques lignes correspondant à la stratégie de rétention finie, tooavoid des résultats imprévisibles et incohérent, étant donné que les anciennes lignes peuvent être supprimés par la tâche de nettoyage de hello, *à n’importe quel point dans le temps et dans ordre arbitraire*.</span><span class="sxs-lookup"><span data-stu-id="4e105-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="4e105-157">Hello image suivante montre le plan de requête hello pour une requête simple :</span><span class="sxs-lookup"><span data-stu-id="4e105-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="4e105-158">requête de Hello plan inclut filtre supplémentaire appliquée tooend de colonne de période (ValidTo) dans hello Clustered Index Scan (opérateur) sur la table d’historique hello (mis en surbrillance).</span><span class="sxs-lookup"><span data-stu-id="4e105-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="4e105-159">Cet exemple suppose que la période de rétention d’un MOIS a été définie sur la table WebsiteUserInfo.</span><span class="sxs-lookup"><span data-stu-id="4e105-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Filtre de requête de rétention](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="4e105-161">Cependant, si vous interrogez directement la table d’historique, vous pouvez voir des lignes antérieures à la période de rétention spécifiée, mais sans aucune garantie de bénéficier de résultats de requête reproductibles.</span><span class="sxs-lookup"><span data-stu-id="4e105-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="4e105-162">Hello image suivante montre plan d’exécution de requête de hello sur la table d’historique hello sans appliquer des filtres supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="4e105-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![Interrogation de l’historique sans filtre de rétention](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="4e105-164">Ne faites pas dépendre votre logique métier sur la lecture de la table d’historique au-delà de la période de rétention, car vous risquez d’obtenir des résultats incohérents ou inattendus.</span><span class="sxs-lookup"><span data-stu-id="4e105-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="4e105-165">Nous vous recommandons d’utiliser des requêtes temporelles avec la clause FOR SYSTEM_TIME pour l’analyse des données dans les tables temporelles.</span><span class="sxs-lookup"><span data-stu-id="4e105-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="4e105-166">Considérations relatives à la limite de restauration dans le temps</span><span class="sxs-lookup"><span data-stu-id="4e105-166">Point in time restore considerations</span></span>
<span data-ttu-id="4e105-167">Lorsque vous créez la nouvelle base de données par [restauration existant point spécifique tooa de la base de données dans le temps](sql-database-recovery-using-backups.md), il a rétention temporelle désactivée au niveau de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4e105-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="4e105-168">(**is_temporal_history_retention_enabled** indicateur défini tooOFF).</span><span class="sxs-lookup"><span data-stu-id="4e105-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="4e105-169">Cette fonctionnalité vous permet de tooexamine toutes les lignes historique lors de la restauration, sans craindre que les anciennes lignes sont supprimés avant que vous obtenez tooquery les.</span><span class="sxs-lookup"><span data-stu-id="4e105-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="4e105-170">Vous pouvez l’utiliser trop*Inspecter les données d’historique au-delà de la période de rétention configurée*.</span><span class="sxs-lookup"><span data-stu-id="4e105-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="4e105-171">Supposons qu’une table temporelle a une période de rétention de un MOIS.</span><span class="sxs-lookup"><span data-stu-id="4e105-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="4e105-172">Si votre base de données a été créé dans la couche de Service Premium, vous serez copie de base de données en mesure de toocreate avec l’état de base de données hello jours too35 dans hello passée.</span><span class="sxs-lookup"><span data-stu-id="4e105-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="4e105-173">Qui efficacement vous permettrait tooanalyze lignes historiques qui ont des too65 jours en interrogeant la table d’historique hello directement.</span><span class="sxs-lookup"><span data-stu-id="4e105-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="4e105-174">Si vous souhaitez que le nettoyage de la rétention temporelle tooactivate, exécutez hello après l’instruction Transact-SQL après le point de restauration dans le temps :</span><span class="sxs-lookup"><span data-stu-id="4e105-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="4e105-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e105-175">Next steps</span></span>
<span data-ttu-id="4e105-176">toolearn toouse des Tables temporelles dans vos applications, consultez Comment [prise en main des Tables temporelles dans la base de données SQL Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="4e105-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="4e105-177">Visitez Channel 9 toohear un [réussite de mise en œuvre temporelle client réel](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) et Espion un [live démonstration temporelle](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="4e105-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="4e105-178">Pour plus d’informations sur les tables temporelles, consultez la [documentation MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e105-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

