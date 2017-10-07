---
title: "aaaConfigure géo-réplication pour la base de données SQL Azure avec Transact-SQL | Documents Microsoft"
description: "Configurer la géoréplication pour Azure SQL Database à l’aide de Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Configurer la géoréplication active pour Base de données SQL Azure avec Transact-SQL

Cet article vous montre comment tooconfigure géo-réplication active pour une base de données SQL Azure avec Transact-SQL.

basculement de tooinitiate à l’aide de Transact-SQL, consultez [initier un basculement planifié ou non planifié pour la base de données SQL Azure avec Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Lorsque vous utilisez la géo-réplication active (secondaires) pour la récupération d’urgence, vous devez configurer un groupe de basculement pour toutes les bases de données dans un application tooenable le basculement automatique et transparent. Cette fonctionnalité est en préversion. Pour plus d’informations, voir [Groupes de basculement automatique et géoréplication](sql-database-geo-replication-overview.md).
> 
> 

géo-réplication active tooconfigure à l’aide de Transact-SQL, hello éléments suivants sont nécessaires :

* Un abonnement Azure
* Un serveur de base de données SQL Azure logique <MyLocalServer> et une base de données SQL <MyDB> -base de données primaire hello que vous souhaitez tooreplicate
* Une ou plusieurs base de données SQL Azure serveurs logiques < MySecondaryServer(n) > - les serveurs logiques hello qui seront des serveurs partenaires de hello dans lequel vous allez créer des bases de données secondaires
* Une connexion qui est un DBManager sur hello principal
* Ont db_ownership de base de données locale hello que vous allez géo-réplication
* Être DBManager sur hello partenaire ou les serveurs toowhich, vous allez configurer la géo-réplication
* version la plus récente de SQL Server Management Studio (SSMS) Hello

> [!IMPORTANT]
> Il est recommandé de toujours utiliser hello dernière version de Management Studio tooremain synchronisés avec les mises à jour tooMicrosoft Azure et base de données SQL. [Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Ajout d'une base de données secondaire
Vous pouvez utiliser hello **ALTER DATABASE** instruction toocreate géorépliqué base de données secondaire sur un serveur partenaire. Vous exécutez cette instruction sur la base de données master hello de hello serveur contenant hello de base de données toobe répliquée. Hello base de données géo-répliquées (hello « base de données primaire ») aura hello même nom que celui en cours de réplication de la base de données hello et sera, par défaut, ont hello même niveau de service en tant que base de données primaire hello. Hello base de données secondaire peut être accessible en lecture ou non lisible et peut être une base de données ou d’un pool élastique. Pour plus d’informations, consultez [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) et [Niveaux de service](sql-database-service-tiers.md).
Une fois que la base de données secondaire hello est créée et amorcée, données commence à répliquer de façon asynchrone à partir de la base de données primaire hello. étapes Hello ci-dessous décrivent comment tooconfigure géo-réplication à l’aide de Management Studio. Étapes toocreate non lisible et plus lisibles bases de données secondaires, comme une base de données ou dans un pool élastique, sont fournis.

> [!NOTE]
> Si une base de données existe sur le serveur partenaire hello hello même nom en tant que principal de hello commande hello de base de données échoue.
> 

### <a name="add-readable-secondary-single-database"></a>Ajouter une base de données secondaire accessible en lecture (base de données unique)
Utilisez hello suivant les étapes toocreate un réplica secondaire en tant qu’une seule base de données.

1. Dans Management Studio, connectez-vous serveur logique de base de données SQL Azure tooyour.
2. Ouvrez le dossier de bases de données hello, développez hello **bases de données système** dossier, avec le bouton droit sur **master**, puis cliquez sur **nouvelle requête**.
3. Utilisez hello suivante **ALTER DATABASE** instruction toomake une base de données local dans un principal de géo-réplication avec une base de données secondaire accessible en lecture sur un serveur secondaire.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Cliquez sur **Execute** requête de hello toorun.

### <a name="add-readable-secondary-elastic-pool"></a>Ajouter une base de données secondaire accessible en lecture (pool élastique)
Utilisez hello suivant les étapes toocreate secondaires lisibles dans un pool élastique.

1. Dans Management Studio, connectez-vous serveur logique de base de données SQL Azure tooyour.
2. Ouvrez le dossier de bases de données hello, développez hello **bases de données système** dossier, avec le bouton droit sur **master**, puis cliquez sur **nouvelle requête**.
3. Utilisez hello suivante **ALTER DATABASE** instruction toomake une base de données local dans un principal de géo-réplication avec une base de données secondaire accessible en lecture sur un serveur secondaire d’un pool élastique.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Cliquez sur **Execute** requête de hello toorun.

## <a name="remove-secondary-database"></a>Supprimer une base de données secondaire
Vous pouvez utiliser hello **ALTER DATABASE** instruction toopermanently terminer le partenariat de réplication hello entre une base de données secondaire et principal. Cette instruction est exécutée sur la base de données master hello sur quel hello réside une base de données primaire. Après l’arrêt de relation hello, base de données secondaire hello devient une base de données en lecture-écriture. Si la base de données toosecondary de connectivité hello est rompue hello commande réussit mais hello secondaire n’est plus en lecture-écriture une fois que la connectivité est rétablie. Pour plus d’informations, consultez [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) et [Niveaux de service](sql-database-service-tiers.md).

Utilisez hello suivant secondaire de géo-répliquées tooremove étapes à partir d’un partenariat de géo-réplication.

1. Dans Management Studio, connectez-vous serveur logique de base de données SQL Azure tooyour.
2. Ouvrez le dossier de bases de données hello, développez hello **bases de données système** dossier, avec le bouton droit sur **master**, puis cliquez sur **nouvelle requête**.
3. Utilisez hello suivante **ALTER DATABASE** secondaire tooremove géo-répliquées de déclaration.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Cliquez sur **Execute** requête de hello toorun.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Surveillance de la configuration et de l’état de la géoréplication active

Tâches d’analyse incluent l’analyse de configuration de géo-réplication hello et du contrôle d’intégrité de la réplication de données.  Vous pouvez utiliser hello **sys.dm_geo_replication_links** vue de gestion dynamique dans hello base de données master tooreturn d’informations sur tous les liens de réplication existants pour chaque base de données sur le serveur logique de base de données SQL Azure hello. Cette vue contient une ligne pour chaque lien de réplication hello entre bases de données primaires et secondaires. Vous pouvez utiliser hello **sys.dm_replication_link_status** vue de gestion dynamique tooreturn une ligne pour chaque base de données SQL Azure impliquée actuellement dans un lien de réplication de la réplication. Cela inclut les bases de données primaires et secondaires. S’il existe plus d’un lien de réplication continue pour une base de données primaire donnée, cette table contient une ligne pour chacune des relations de hello. affichage de Hello est créé dans toutes les bases de données master logique de hello. Toutefois, l’interrogation de cette vue dans master logique de hello retourne un jeu vide. Vous pouvez utiliser hello **sys.dm_operation_status** état de hello tooshow vue de gestion dynamique pour toutes les opérations, y compris l’état hello hello des liens de réplication de la base de données. Pour plus d’informations, consultez [sys.geo_replication_links (Base de données SQL Azure)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Base de données SQL Azure)](https://msdn.microsoft.com/library/mt575504.aspx) et [sys.dm_operation_status (Base de données SQL Azure)](https://msdn.microsoft.com/library/dn270022.aspx).

Utilisez hello suivant partenariat de toomonitor une géo-réplication active comme suit.

1. Dans Management Studio, connectez-vous serveur logique de base de données SQL Azure tooyour.
2. Ouvrez le dossier de bases de données hello, développez hello **bases de données système** dossier, avec le bouton droit sur **master**, puis cliquez sur **nouvelle requête**.
3. Utilisez hello suivant l’instruction tooshow toutes les bases de données avec des liens de géo-réplication.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Cliquez sur **Execute** requête de hello toorun.
5. Ouvrez le dossier de bases de données hello, développez hello **bases de données système** dossier, avec le bouton droit sur **MyDB**, puis cliquez sur **nouvelle requête**.
6. Hello d’utilisation après la réplication de hello tooshow instruction est en retard et de la dernière heure de la réplication de mes bases de données secondaire de MyDB.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Cliquez sur **Execute** requête de hello toorun.
8. Utilisez hello suivant l’instruction tooshow hello plus récent géo-réplication des opérations liées à la base de données MyDB.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Cliquez sur **Execute** requête de hello toorun.

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur les groupes de basculement et de géo-réplication active, consultez - [groupes de basculement](sql-database-geo-replication-overview.md)
* Pour une vue d’ensemble de la continuité des activités et des scénarios, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md)

