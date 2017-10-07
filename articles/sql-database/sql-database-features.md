---
title: "vue d’ensemble des fonctionnalités de base de données SQL d’aaaAzure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de bases de données et les serveurs logiques de base de données SQL Azure hello et inclut une matrice de prise en charge des fonctionnalités avec des liens de chaque fonctionnalité répertoriée."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d1a46fa4-53d2-4d25-a0a7-92e8f9d70828
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/25/2017
ms.author: carlrab
ms.openlocfilehash: 463c88edcd38eabbc768cfb701bc74461836aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-features"></a>Fonctionnalités Azure SQL Database

Partage d’une base de code avec SQL Server de base de données SQL Azure et, au niveau de base de données hello, prend en charge de la plupart des hello mêmes fonctionnalités. Hello principales différences entre la base de données SQL Azure et SQL Server sont au niveau de l’instance hello. 

Nous continuons tooadd tooAzure de fonctionnalités de base de données SQL. Donc nous vous invitons à vous toovisit notre Service mises à jour page Web pour Azure et toouse ses filtres :

* Filtré toohello [service de base de données SQL](https://azure.microsoft.com/updates/?service=sql-database).
* Filtré tooGeneral disponibilité [les annonces (GA)](http://azure.microsoft.com/updates/?service=sql-database&update-type=general-availability) pour les fonctionnalités de base de données SQL.

## <a name="sql-server-and-sql-database-feature-support"></a>Prise en charge des fonctionnalités SQL Server et SQL Database

Hello tableau suivant répertorie les principales fonctionnalités de hello de SQL Server et fournit des informations si chaque fonctionnalité particulière est pris en charge et un lien toomore des informations sur la fonctionnalité de hello. Pour les différences de Transact-SQL tooconsider lors de la migration d’une solution de base de données existante, consultez [les différences de résolution de Transact-SQL au cours de la migration tooSQL de base de données](sql-database-transact-sql-information.md).


| **Fonctionnalité SQL Server** | **Prise en charge dans Azure SQL Database** | 
| --- | --- |  
| [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) | Oui - voir [Magasin de certificats](sql-database-always-encrypted.md) et [Coffre de clés](sql-database-always-encrypted-azure-key-vault.md)|
| [Groupes de disponibilité AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) | Non - voir [Groupes de basculement et géo-réplication active](sql-database-geo-replication-overview.md) |
| [Attacher une base de données](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) | Non |
| [Rôles d’application](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/application-roles) | Oui |
| [Fichier BACPAC (exporter)](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) | Oui - voir [Exportation de base de données SQL](sql-database-export.md) |
| [Fichier BACPAC (importer)](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database) | Oui - voir [Importation de base de données SQL](sql-database-import.md) |
| [Commande de sauvegarde](https://docs.microsoft.com/sql/t-sql/statements/backup-transact-sql) | Non - voir [Sauvegardes automatisées](sql-database-automated-backups.md) |
| [Fonctions intégrées](https://docs.microsoft.com/sql/t-sql/functions/functions) | La plupart - voir Fonctions individuelles |
| [Modifier la capture de données](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-data-capture-sql-server) | Non |
| [Suivi des modifications](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server) | Oui |
| [Instructions de classement](https://docs.microsoft.com/sql/t-sql/statements/collations) | Oui |
| [Index Columnstore](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) | Oui - [Édition Premium uniquement](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) |
| [Common Language Runtime (CLR)](https://docs.microsoft.com/sql/relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts) | Non |
| [Bases de données à relation contenant-contenu](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases) | Oui |
| [Utilisateurs contenus](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable) | Oui |
| [Contrôle des mots clés de langage de flux](https://docs.microsoft.com/sql/t-sql/language-elements/control-of-flow) | Oui |
| [Requêtes entre plusieurs bases de données](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/cross-database-queries) | Partiellement - voir [Requêtes élastiques](sql-database-elastic-query-overview.md) |
| [Curseurs](https://docs.microsoft.com/sql/t-sql/language-elements/cursors-transact-sql) | Oui | 
| [Compression des données](https://docs.microsoft.com/sql/relational-databases/data-compression/data-compression) | Oui |
| [Messagerie de base de données](https://docs.microsoft.com/sql/relational-databases/database-mail/database-mail) | Non |
| [Mise en miroir de bases de données](https://docs.microsoft.com/sql/database-engine/database-mirroring/database-mirroring-sql-server) | Non |
| [Paramètres de configuration de base de données](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) | Oui |
| [Data Quality Services (DQS)](https://docs.microsoft.com/sql/data-quality-services/data-quality-services) | Non |
| [Instantanés de base de données](https://docs.microsoft.com/sql/relational-databases/databases/database-snapshots-sql-server) | Non |
| [Types de données](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql) | Oui |  
| [Instructions DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) | La plupart - voir Instructions individuelles |
| [Instructions DDL](https://docs.microsoft.com/sql/t-sql/statements/statements) | La plupart - voir Instructions individuelles
| [Déclencheurs DDL](https://docs.microsoft.com/sql/relational-databases/triggers/ddl-triggers) | Base de données uniquement |
| [Transactions distribuées - MS DTC](https://docs.microsoft.com/sql/relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions) | Non - voir [Transactions élastiques](sql-database-elastic-transactions-overview.md) |
| [Instructions DML](https://docs.microsoft.com/sql/t-sql/queries/queries) | La plupart - voir Instructions individuelles |
| [Déclencheurs DML](https://docs.microsoft.com/sql/relational-databases/triggers/dml-triggers) |
| [DMV](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views) | Certains - voir DMV individuels |
| [Notifications d’événement](https://docs.microsoft.com/sql/relational-databases/service-broker/event-notifications) | Non - voir [Alertes](sql-database-insights-alerts-portal.md) |
| [Expressions](https://docs.microsoft.com/sql/t-sql/language-elements/expressions-transact-sql) |Oui |
| [Événements étendus](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events) | Certains - voir Événements individuels |
| [Procédures stockées étendues](https://docs.microsoft.com/sql/relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures) | Non |
| [Fichiers et groupes de fichiers](https://docs.microsoft.com/sql/relational-databases/databases/database-files-and-filegroups) | Groupe de fichiers principal uniquement |
| [FileStream](https://docs.microsoft.com/sql/relational-databases/blob/filestream-sql-server) | Non |
| [Recherche en texte intégral](https://docs.microsoft.com/sql/relational-databases/search/full-text-search) | Analyseurs lexicaux tiers non pris en charge |
| [Fonctions](https://docs.microsoft.com/sql/t-sql/functions/functions) | La plupart - voir Fonctions individuelles |
| [Traitement de graphe](/sql/relational-databases/graphs/sql-graph-overview) | Oui |
| [Optimisation en mémoire](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization) | Oui - [Édition Premium uniquement](sql-database-in-memory.md) |
| [Prise en charge des données JSON](https://docs.microsoft.com/sql/relational-databases/json/json-data-sql-server) | Oui |
| [Éléments de langage](https://docs.microsoft.com/sql/t-sql/language-elements/language-elements-transact-sql) | La plupart - voir Éléments individuels |  
| [Serveurs liés](https://docs.microsoft.com/sql/relational-databases/linked-servers/linked-servers-database-engine) | Non - voir [Requête élastique](sql-database-elastic-query-horizontal-partitioning.md) |
| [Copie des journaux de transaction](https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server) | Non - voir [Groupes de basculement et géo-réplication active](sql-database-geo-replication-overview.md) |
| [Master Data Services (MDS)](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds) | Non |
| [Journalisation minimale dans l’importation en bloc](https://docs.microsoft.com/sql/relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import) | Non |
| [Modification des données système](https://docs.microsoft.com/sql/relational-databases/databases/system-databases) | Non |
| [Opérations d’index en ligne](https://docs.microsoft.com/sql/relational-databases/indexes/perform-index-operations-online) | Pris en charge - taille des transactions limitée en fonction du niveau de service |
| [Opérateurs](https://docs.microsoft.com/sql/t-sql/language-elements/operators-transact-sql) | La plupart - voir Opérateurs individuels |
| [Limite de restauration dans le temps d’une base de données](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model) | Oui - voir [Récupération de base de données SQL](sql-database-recovery-using-backups.md#point-in-time-restore) |
| [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) | Non |
| [Gestion basée sur des stratégies](https://docs.microsoft.com/sql/relational-databases/policy-based-management/administer-servers-by-using-policy-based-management) | Non |
| [Prédicats](https://docs.microsoft.com/sql/t-sql/queries/predicates) | La plupart - voir Prédicats individuels |
| [R Services](https://docs.microsoft.com/sql/advanced-analytics/r-services/sql-server-r-services) | Non |
| [Gouverneur de ressources](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor) | Non |
| [Instructions RESTORE](https://docs.microsoft.com/sql/t-sql/statements/restore-statements-for-restoring-recovering-and-managing-backups-transact-sql) | Non | 
| [Restauration de la base de données à partir de la sauvegarde](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases#restore-data-backups) | À partir des sauvegardes intégrées uniquement - voir [Récupération de base de données SQL](sql-database-recovery-using-backups.md) |
| [Sécurité au niveau des lignes](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) | Oui |
| [Recherche sémantique](https://docs.microsoft.com/sql/relational-databases/search/semantic-search-sql-server) | Non |
| [Numéros de séquence](https://docs.microsoft.com/sql/relational-databases/sequence-numbers/sequence-numbers) | Oui |
| [Service Broker](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-service-broker) | Non |
| [Paramètres de configuration du serveur](https://docs.microsoft.com/sql/database-engine/configure-windows/server-configuration-options-sql-server) | Non |
| [Instructions SET](https://docs.microsoft.com/sql/t-sql/statements/set-statements-transact-sql) | La plupart - voir Instructions individuelles 
| [Spatial](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-sql-server) | Oui |
| [SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) | Non - voir [Tâches élastiques](sql-database-elastic-jobs-getting-started.md) |
| [SQL Server Analysis Services (SSAS)](https://docs.microsoft.com/sql/analysis-services/analysis-services) | Non - voir [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) |
| [Audit SQL Server](https://docs.microsoft.com/sql/relational-databases/security/auditing/sql-server-audit-database-engine) | Non - voir [Audit de base de données SQL](sql-database-auditing.md) |
| [SQL Server Integration Services (SSIS)](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services) | Non - voir [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) |
| [SQL Server PowerShell](https://docs.microsoft.com/sql/relational-databases/scripting/sql-server-powershell) | Oui |
| Générateur de profils SQL Server | [Pris en charge](https://docs.microsoft.com/sql/tools/sql-server-profiler/sql-server-profiler) | Non - voir [Événements étendus](sql-database-xevent-db-diff-from-svr.md) |
| [Réplication SQL Server](https://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication) | [Abonné à la réplication transactionnelle et de capture instantanée uniquement](sql-database-cloud-migrate.md) |
| [SQL Server Reporting Services (SSRS)](https://docs.microsoft.com/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports) | Non |
| [Procédures stockées](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) | Oui |
| [Fonctions stockées sur système](https://docs.microsoft.com/sql/relational-databases/system-functions/system-functions-for-transact-sql) | La plupart - voir Fonctions individuelles |
| [Procédures stockées sur système](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql) | Certaines - voir Procédures stockées individuelles |
| [Tables système](https://docs.microsoft.com/sql/relational-databases/system-tables/system-tables-transact-sql) | Certaines - voir Tables individuelles |
| [Vues catalogue système](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/catalog-views-transact-sql) | Certaines - voir Vues individuelles |
| [Partitionnement de table](https://docs.microsoft.com/sql/relational-databases/partitions/partitioned-tables-and-indexes) | Oui - Groupe de fichiers principal uniquement |
| [Tables temporaires](https://docs.microsoft.com/sql/t-sql/statements/create-table-transact-sql#temporary-tables) | Tables temporaires globales niveau base de données ou local uniquement |
| [Tables temporelles](https://docs.microsoft.com/sql/relational-databases/tables/temporal-tables) | Oui |
| [Transactions](https://docs.microsoft.com/sql/t-sql/language-elements/transactions-transact-sql) | Non |
| [Variables](https://docs.microsoft.com/sql/t-sql/language-elements/variables-transact-sql) | Oui | 
| [Chiffrement transparent des données (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) | Oui |
| [Clustering de basculement Windows Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server) | Non - voir [Groupes de basculement et géo-réplication active](sql-database-geo-replication-overview.md) |
| [Index XML](https://docs.microsoft.com/sql/t-sql/statements/create-xml-index-transact-sql) | Oui |

## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations sur hello service de base de données SQL Azure, consultez [quelle est la base de données SQL ?](sql-database-technical-overview.md)
- Pour plus d’informations sur la prise en charge de Transact-SQL et les différences, consultez [les différences de résolution de Transact-SQL au cours de la migration tooSQL de base de données](sql-database-transact-sql-information.md).
