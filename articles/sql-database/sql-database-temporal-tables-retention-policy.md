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
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>Gérer les données d’historique dans les tables temporelles avec la stratégie de rétention
Par rapport aux tables normales, les tables temporelles peuvent augmenter la taille des bases de données, notamment si vous conservez les données d’historique pendant longtemps. Stratégie de rétention pour les données d’historique constitue donc un aspect important de la planification et la gestion du cycle de vie hello de chaque table temporelle. Les tables temporelles dans Azure SQL Database sont fournies avec un mécanisme de rétention facile à utiliser qui vous permet d’accomplir cette tâche.

Rétention de l’historique temporelle peut être configurée au niveau de table individuelle hello, qui permet aux utilisateurs de stratégies de vieillissement de toocreate flexible. Application de la rétention temporelle est simple : il ne requiert qu’un seul paramètre toobe définie pendant la modification de la création ou le schéma de table.

Une fois que vous avez défini la stratégie de rétention, Azure SQL Database commence par vérifier régulièrement s’il existe des lignes d’historique éligibles pour le nettoyage automatique des données. Identification des lignes correspondantes et leur suppression à partir de la table d’historique hello se produisent en toute transparence, dans la tâche d’arrière-plan hello est planifiée et exécutée par le système de hello. Condition d’âge pour les lignes de la table historique hello est vérifiée en fonction de la colonne hello représentant la fin de la période SYSTEM_TIME. Si la période de rétention, par exemple, a la valeur toosix mois, les lignes éligibles pour le nettoyage de la table répondent aux hello suivant la condition :

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

Bonjour précédent exemple, nous avons supposé que **ValidTo** colonne correspond fin toohello de période SYSTEM_TIME.

## <a name="how-tooconfigure-retention-policy"></a>La stratégie de rétention tooconfigure ?
Avant de configurer la stratégie de rétention pour une table temporelle, vérifiez tout d’abord si la rétention historique temporelle est activée *au niveau de base de données hello*.

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

Indicateur de base de données **is_temporal_history_retention_enabled** est tooON ensemble par défaut, mais les utilisateurs peuvent les modifier avec l’instruction ALTER DATABASE. Il est également automatiquement tooOFF ensemble après [point de restauration dans le temps](sql-database-recovery-using-backups.md) opération. nettoyage de rétention d’historique temporelle tooenable pour votre base de données, exécutez hello après l’instruction :

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> Vous pouvez configurer la durée de rétention pour les tables temporelles même si **is_temporal_history_retention_enabled** est DÉSACTIVÉ, mais le nettoyage automatique des lignes anciennes n’est pas déclenché dans ce cas.
> 
> 

Stratégie de rétention est configurée lors de la création de table en spécifiant la valeur de paramètre HISTORY_RETENTION_PERIOD hello :

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

Base de données SQL Azure vous permet de la période de rétention toospecify à l’aide d’unités de temps différent : jours, semaines, mois et les années. Si HISTORY_RETENTION_PERIOD est omis, la rétention INFINITE est utilisée. Vous pouvez également utiliser le mot clé INFINITE de façon explicite.

Dans certains scénarios, vous pouvez tooconfigure rétention après la création de table, ou toochange les valeur configurée précédemment. Dans ce cas, utilisez l’instruction ALTER TABLE :

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> Définition de SYSTEM_VERSIONING tooOFF *ne conserve pas* valeur de période de rétention. Paramètre tooON SYSTEM_VERSIONING sans HISTORY_RETENTION_PERIOD spécifié explicitement des résultats dans la période de rétention infinie hello.
> 
> 

tooreview état actuel de la stratégie de rétention hello, cet indicateur de l’activation de rétention temporelle jointures au niveau de base de données hello avec des périodes de rétention des tables individuelles de requête suivante de hello d’utilisation :

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


## <a name="how-sql-database-deletes-aged-rows"></a>Comment SQL Database supprime les anciennes lignes ?
processus de nettoyage Hello dépend de la mise en page de hello index de table d’historique hello. Il est important toonotice qui *uniquement les tables d’historique avec un index cluster (B-tree ou columnstore) peuvent avoir fini de rétention configurée*. Une tâche en arrière-plan est créée de nettoyage des données d’anciennes données tooperform pour toutes les tables temporelles avec la période de rétention limitée.
Logique de nettoyage pour les index cluster rowstore (B-tree) de hello supprime les anciennes lignes en segments plus petits (haut too10K) en réduisant la pression sur le journal de la base de données et le sous-système d’e/s. Bien que la logique de nettoyage utilise requis index B-tree, ordre de suppressions de lignes hello antérieurs à la période de rétention ne peut pas être garantie bien. Par conséquent, *ne prennent pas de dépendances sur l’ordre de nettoyage hello dans vos applications*.

Hello tâche de nettoyage pour hello clusterisé columnstore supprime entière [des groupes de lignes](https://msdn.microsoft.com/library/gg492088.aspx) à la fois (généralement contient 1 million de lignes chacune), qui est très efficace, en particulier lorsque les données d’historique sont générées à un rythme haute.

![Rétention de cluster columnstore](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

Une compression des données performante et un nettoyage efficace de la rétention font des index cluster columnstore un choix idéal pour les scénarios dans lesquels votre charge de travail génère rapidement de gros volumes de données d’historique. Ce modèle est généralement utilisé pour les [charges de travail de traitement transactionnel intensives qui utilisent des tables temporelles](https://msdn.microsoft.com/library/mt631669.aspx) à des fins de suivi des modifications et l’audit, d’analyse de tendances ou d’ingestion des données IoT.

## <a name="index-considerations"></a>Considérations relatives aux index
tâche de nettoyage Hello pour les tables avec un index cluster rowstore requiert toostart index avec fin correspondantes hello hello colonne de période SYSTEM_TIME. Si cet index n’existe pas, vous ne pouvez pas configurer de période de rétention limitée :

*Msg 13765, niveau 16, état 1 <br> </br> période de rétention finie Échec de la définition de table temporelle avec version système « temporalstagetestdb.dbo.WebsiteUserInfo', car la table d’historique hello » temporalstagetestdb.dbo.WebsiteUserInfoHistory' ne contient pas d’index en cluster requis. Envisagez de créer un columnstore en cluster ou un index B-tree en commençant par la colonne hello qui correspond à la fin de SYSTEM_TIME period, sur la table d’historique hello.*

Il est important de toonotice qui hello table d’historique par défaut déjà créé par la base de données SQL Azure a clustered index, qui est conforme pour la stratégie de rétention. Si vous essayez tooremove cet index sur une table avec une période de rétention finie, opération échoue avec hello l’erreur suivante :

*Msg 13766, niveau 16, état 1 <br> </br> Impossible de supprimer les index de cluster hello 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' car il est utilisé pour le nettoyage automatique des données d’anciennes données. Envisagez de tooINFINITE HISTORY_RETENTION_PERIOD de paramètre sur la table temporelle avec version système correspondant hello si vous avez besoin de toodrop cet index.*

Fonctionne optimal de nettoyage sur un index columnstore cluster hello historiques lignes sont insérées dans hello par ordre croissant (classée par fin hello de colonne de période), qui est toujours le cas de hello lors de la table d’historique hello est remplie exclusivement par hello système Mécanisme VERSIONIOING. Si les lignes dans la table d’historique hello ne sont pas ordonnés en fin de la colonne de période (qui est peut-être hello cas si vous avez migré des données d’historique existantes), vous devez recréer les index cluster columnstore sur les index B-tree rowstore qui est commandé correctement tooachieve optimal performances.

Évitez la reconstruction d’index cluster columnstore sur la table d’historique hello avec la période de rétention finie hello, car il peut changer de classement dans les groupes de lignes hello naturellement imposées par l’opération de contrôle de version système hello. Si vous avez besoin d’index cluster columnstore de toorebuild sur la table d’historique hello, faire en recréant par-dessus conforme index B-tree, en conservant le classement dans les rowgroups hello nécessaires pour le nettoyage de données standard. Hello même approche doit être effectuée si vous créez la table temporelle avec table d’historique existante qui a un index de colonne sans ordre de garantie des données cluster :

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

Lors de la période de rétention finie est configurée pour la table d’historique hello avec un index columnstore cluster hello, vous ne peut pas créer des index non cluster B-tree supplémentaires sur cette table :

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

Un tooexecute tentative au-dessus instruction échoue avec hello l’erreur suivante :

*Msg 13772, niveau 16, état 1 <br></br> Impossible de créer un index non cluster sur la table d’historique temporelle « WebsiteUserInfoHistory » car celle-ci est définie avec une période de rétention limitée et un index cluster columnstore.*

## <a name="querying-tables-with-retention-policy"></a>Interrogation de tables comportant une stratégie de rétention
Toutes les requêtes sur la table temporelle hello éliminer automatiquement les historiques lignes correspondant à la stratégie de rétention finie, tooavoid des résultats imprévisibles et incohérent, étant donné que les anciennes lignes peuvent être supprimés par la tâche de nettoyage de hello, *à n’importe quel point dans le temps et dans ordre arbitraire*.

Hello image suivante montre le plan de requête hello pour une requête simple :

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

requête de Hello plan inclut filtre supplémentaire appliquée tooend de colonne de période (ValidTo) dans hello Clustered Index Scan (opérateur) sur la table d’historique hello (mis en surbrillance). Cet exemple suppose que la période de rétention d’un MOIS a été définie sur la table WebsiteUserInfo.

![Filtre de requête de rétention](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

Cependant, si vous interrogez directement la table d’historique, vous pouvez voir des lignes antérieures à la période de rétention spécifiée, mais sans aucune garantie de bénéficier de résultats de requête reproductibles. Hello image suivante montre plan d’exécution de requête de hello sur la table d’historique hello sans appliquer des filtres supplémentaires :

![Interrogation de l’historique sans filtre de rétention](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

Ne faites pas dépendre votre logique métier sur la lecture de la table d’historique au-delà de la période de rétention, car vous risquez d’obtenir des résultats incohérents ou inattendus. Nous vous recommandons d’utiliser des requêtes temporelles avec la clause FOR SYSTEM_TIME pour l’analyse des données dans les tables temporelles.

## <a name="point-in-time-restore-considerations"></a>Considérations relatives à la limite de restauration dans le temps
Lorsque vous créez la nouvelle base de données par [restauration existant point spécifique tooa de la base de données dans le temps](sql-database-recovery-using-backups.md), il a rétention temporelle désactivée au niveau de base de données hello. (**is_temporal_history_retention_enabled** indicateur défini tooOFF). Cette fonctionnalité vous permet de tooexamine toutes les lignes historique lors de la restauration, sans craindre que les anciennes lignes sont supprimés avant que vous obtenez tooquery les. Vous pouvez l’utiliser trop*Inspecter les données d’historique au-delà de la période de rétention configurée*.

Supposons qu’une table temporelle a une période de rétention de un MOIS. Si votre base de données a été créé dans la couche de Service Premium, vous serez copie de base de données en mesure de toocreate avec l’état de base de données hello jours too35 dans hello passée. Qui efficacement vous permettrait tooanalyze lignes historiques qui ont des too65 jours en interrogeant la table d’historique hello directement.

Si vous souhaitez que le nettoyage de la rétention temporelle tooactivate, exécutez hello après l’instruction Transact-SQL après le point de restauration dans le temps :

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>Étapes suivantes
toolearn toouse des Tables temporelles dans vos applications, consultez Comment [prise en main des Tables temporelles dans la base de données SQL Azure](sql-database-temporal-tables.md).

Visitez Channel 9 toohear un [réussite de mise en œuvre temporelle client réel](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) et Espion un [live démonstration temporelle](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

Pour plus d’informations sur les tables temporelles, consultez la [documentation MSDN](https://msdn.microsoft.com/library/dn935015.aspx).

