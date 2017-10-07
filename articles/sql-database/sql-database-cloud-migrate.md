---
title: "tooAzure de migration de base de données aaaSQL serveur de base de données SQL | Documents Microsoft"
description: "Découvrez comment sur SQL Server de base de données tooAzure de migration de la base de données SQL dans le cloud de hello. Utilisez la migration de base de données migration tools tootest compatibilité toodatabase préalable."
keywords: "migration de base de données, migration de base de données sql server, outils de migration de base de données, migrer la base de données, migrer la base de données sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>TooSQL de migration de base de données SQL Server de la base de données dans le cloud de hello
Dans cet article, vous allez découvrir hello deux méthodes principales pour la migration d’un SQL Server 2005 ou une ultérieure tooAzure de base de données de la base de données SQL. Hello première méthode est plus simple, mais requiert certains, éventuellement substantiel, temps d’arrêt pendant la migration de hello. méthode deuxième Hello est plus complexe, mais élimine sensiblement les temps d’arrêt pendant la migration de hello.

Dans les deux cas, vous devez tooensure cette base de données source hello est compatible avec la base de données SQL Azure à l’aide de hello [données Migration Assistant (DMA)](https://www.microsoft.com/download/details.aspx?id=53595). L’approche de base de données SQL V12 [similarité des fonctionnalités](sql-database-features.md) avec SQL Server, autres que des problèmes au niveau du tooserver et bases de données croisées les opérations associées. Bases de données et les applications qui reposent sur [partiellement pris en charge ou non pris en charge des fonctions](sql-database-transact-sql-information.md) besoin de certaines [refonte toofix ces incompatibilités](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) hello SQL Server avant de la base de données peut être migré.

> [!NOTE]
> une base de données non SQL Server, y compris Microsoft Access, Sybase, MySQL Oracle et DB2 tooAzure base de données SQL, reportez-vous à toomigrate [Assistant Migration SQL Server](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/).
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Méthode 1 : La Migration avec un temps mort pendant la migration de hello

 Utilisez cette méthode si vous pouvez vous permettre un temps d’arrêt ou si vous effectuez un test de migration d’une base de données de production que vous envisagez de migrer. Pour un didacticiel, consultez [Migrer une base de données SQL Server](sql-database-migrate-your-sql-server-database.md).

Hello liste suivante contient des flux de travail général hello pour une migration de base de données SQL Server à l’aide de cette méthode.

  ![Schéma de migration VSSSDT](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. Évaluer la base de données hello pour assurer la compatibilité à l’aide de la version la plus récente de hello [données Migration Assistant (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).
2. Préparez les corrections nécessaires en tant que scripts Transact-SQL.
3. Effectuer une copie cohérente de la base de données source hello en cours de migration - et vérifiez aucune des modifications supplémentaires ne sont apportées toohello base de données source (ou vous pouvez appliquer manuellement de telles modifications après la migration de hello). Il existe plusieurs méthodes tooquiesce une base de données, la désactivation de toocreating de connectivité client un [instantané de base de données](https://msdn.microsoft.com/library/ms175876.aspx).
4. Déployez hello tooapply de hello Transact-SQL scripts correctifs toohello une copie de base de données.
5. [Exporter](sql-database-export.md) hello tooa de copie de base de données. Fichier BACPAC sur un lecteur local.
6. [Importation](sql-database-import.md) hello. Fichier BACPAC en tant qu’une nouvelle base de données SQL Azure à l’aide de plusieurs BACPAC importer outils, avec SQLPackage.exe en cours hello recommandé outil pour de meilleures performances.

### <a name="optimizing-data-transfer-performance-during-migration"></a>Optimisation des performances de transfert de données pendant la migration 

Hello suivant liste contient des recommandations pour de meilleures performances pendant le processus d’importation hello.

* Choisissez hello plus haut niveau de service et les performances de niveau que votre budget autorise les performances du transfert toomaximize hello. Vous pouvez l’échelle une fois la migration hello terminée toosave money. 
* Réduire la distance hello entre votre. BACPAC de fichiers et de hello destination Datacenter.
* Désactivez les statistiques automatiques pendant la migration.
* Partitionnez les tables et les index.
* Supprimez les vues indexées et recréez-les une fois la migration terminée.
* Supprimer des données historiques rarement interrogées tooanother base de données et la faire migrer les données d’historique tooa distinct SQL Azure. Vous pourrez ensuite interroger ces données historiques à l’aide de [requêtes élastiques](sql-database-elastic-query-overview.md).

### <a name="optimize-performance-after-hello-migration-completes"></a>Optimiser les performances une fois hello migration terminée

[Mettre à jour les statistiques](https://msdn.microsoft.com/library/ms187348.aspx) avec une analyse complète après la migration hello est terminée.

## <a name="method-2-use-transactional-replication"></a>Méthode 2: Utiliser la réplication transactionnelle

Lorsque vous ne pouvez pas vous permettre tooremove votre base de données SQL Server à partir de la production pendant la migration de hello, vous pouvez utiliser la réplication transactionnelle SQL Server en tant que votre solution de migration. toouse cette méthode, la base de données source hello doit respecter hello [configuration requise pour la réplication transactionnelle](https://msdn.microsoft.com/library/mt589530.aspx) et être compatible avec la base de données SQL Azure. Pour plus d’informations sur la réplication SQL avec AlwaysOn, consultez [Configurer la réplication pour les groupes de disponibilité AlwaysOn (SQL Server)](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server).

toouse cette solution, vous configurez votre base de données SQL Azure comme une instance de SQL Server toohello abonné que vous souhaitez toomigrate. serveur de distribution de la réplication transactionnelle Hello synchronise les données à partir de hello toobe de base de données synchronisée (éditeur hello) alors que les nouvelles transactions continuent de se produire. 

Avec la réplication transactionnelle, toutes les modifications tooyour données ou le schéma apparaissent dans votre base de données SQL Azure. Une fois hello synchronisation est terminée et que vous êtes prêt toomigrate, modifiez la chaîne de connexion de hello de vos applications de toopoint les tooyour base de données SQL Azure. Une fois que la réplication transactionnelle draine le reste de toutes les modifications sur votre base de données source et de toutes vos applications point tooAzure base de données, vous pouvez désinstaller la réplication transactionnelle. Votre Base de données SQL Azure est maintenant votre système de production.

 ![Diagramme SeedCloudTR](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> Vous pouvez également utiliser la réplication transactionnelle toomigrate un sous-ensemble de votre base de données source. publication Hello répliquer tooAzure base de données SQL peut être sous-ensemble limité tooa de tables hello hello de base de données en cours de réplication. Pour chaque table répliquée, vous pouvez limiter le sous-ensemble de tooa données hello de lignes de hello et/ou un sous-ensemble de colonnes de hello.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>TooSQL de migration de base de données à l’aide de flux de travail de réplication des transactions

> [!IMPORTANT]
> Utiliser hello la dernière version de SQL Server Management Studio tooremain synchronisé avec les mises à jour tooMicrosoft Azure et base de données SQL. Les versions antérieures de SQL Server Management Studio ne peuvent pas configurer Base de données SQL en tant qu’abonné. [Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. Configurer la distribution
   -  [Avec SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [Avec Transact-SQL](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. Créer une publication
   -  [Avec SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [Avec Transact-SQL](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. Créer un abonnement
   -  [Avec SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [Avec Transact-SQL](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>Quelques conseils et les différences de migration tooSQL de base de données

1. Utilisez un serveur de distribution local 
   - Cela provoque un impact sur les performances sur le serveur de hello. 
   - Si l’impact sur les performances hello est inacceptable, vous pouvez utiliser un autre serveur, mais il ajoute une complexité de la gestion et l’administration.
2. Lors de la sélection d’un dossier de capture instantanée, le dossier hello qu’Assurez-vous que vous sélectionnez est suffisamment grande toohold un BCP de chaque table vous souhaitez tooreplicate. 
3. Verrous de la création de capture instantanée hello tables associées jusqu'à son terme, donc planifier correctement votre instantané. 
4. Seuls les abonnements par émission de données sont pris en charge dans Azure SQL Database. Vous pouvez uniquement ajouter des abonnés à partir de la base de données source hello.

## <a name="resolving-database-migration-compatibility-issues"></a>Résolution des problèmes de compatibilité de migration de la base de données
Il existe un large éventail de problèmes de compatibilité que vous pouvez rencontrer, à la fois sur la version de hello de SQL Server en hello source de base de données et hello plus complexe de base de données hello que vous effectuez la migration. Les versions antérieures de SQL Server ont plus de problèmes de compatibilité. Utilisez hello suivant des ressources, en outre tooa ciblés recherche sur Internet à l’aide de votre moteur de recherche de choix :

* [Fonctionnalités de base de données SQL Server non prises en charge dans Azure SQL Database](sql-database-transact-sql-information.md)
* [Discontinued Database Engine Functionality in SQL Server 2016 (Fonctionnalités du moteur de base de données supprimées dans SQL Server 2016)](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [Discontinued Database Engine Functionality in SQL Server 2014 (Fonctionnalités du moteur de base de données non disponibles dans SQL Server 2014)](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [Discontinued Database Engine Functionality in SQL Server 2012 (Fonctionnalités du moteur de base de données non disponibles dans SQL Server 2012)](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [Discontinued Database Engine Functionality in SQL Server 2008 R2 (Fonctionnalités du moteur de base de données non disponibles dans SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [Discontinued Database Engine Functionality in SQL Server 2005 (Fonctionnalités du moteur de base de données supprimées dans SQL Server 2005)](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

En outre toosearching hello Internet et à l’aide de ces ressources, utilisez hello [forums de communauté MSDN SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) ou [StackOverflow](http://stackoverflow.com/).

## <a name="next-steps"></a>Étapes suivantes
* Utilisez le script de hello sur le blog des ingénieurs EMEA de SQL Azure hello trop[surveiller l’utilisation de tempdb pendant la migration](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/).
* Utilisez le script de hello sur le blog des ingénieurs EMEA de SQL Azure hello trop[surveiller l’espace de journal des transactions hello de votre base de données pendant la migration](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0).
* Pour une équipe de consultants clients SQL Server à l’aide des fichiers BACPAC, consultez le blog sur la migration [migration à partir de SQL Server tooAzure de la base de données SQL à l’aide des fichiers BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Pour plus d’informations sur l’utilisation de l’heure UTC après la migration, consultez [modification hello fuseau horaire par défaut votre fuseau horaire local](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/).
* Pour plus d’informations sur la modification de la langue par défaut de hello d’une base de données après la migration, consultez [comment toochange hello langue par défaut de la base de données SQL Azure](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/).


