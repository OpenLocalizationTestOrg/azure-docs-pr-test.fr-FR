---
title: "TSQL : Lancer un basculement pour Azure SQL Database | Microsoft Docs"
description: "Lancer un basculement planifié ou non planifié pour une base de données SQL Azure avec Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Lancer un basculement planifié ou non planifié pour une base de données SQL Azure avec Transact-SQL

Cet article vous montre comment tooinitiate basculement tooa base de données SQL secondaire à l’aide de Transact-SQL. tooconfigure géo-réplication, consultez [configurer géo-réplication pour la base de données SQL Azure](sql-database-geo-replication-transact-sql.md).

basculement de tooinitiate, hello éléments suivants sont nécessaires :

* Une connexion qui est un DBManager sur hello principal
* Ont db_ownership de base de données locale hello que vous allez géo-réplication
* Être DBManager sur hello partenaire ou les serveurs toowhich, vous allez configurer la géo-réplication
* Dernière version de SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Il est recommandé de toujours utiliser hello dernière version de Management Studio tooremain synchronisés avec les mises à jour tooMicrosoft Azure et base de données SQL. [Mettre à jour SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>Initiez un basculement planifié promouvoir un base de données secondaire toobecome hello nouveau réplica principal
Vous pouvez utiliser hello **ALTER DATABASE** instruction toopromote un base de données secondaire toobecome hello nouveau principal de base de données de manière planifiée, la rétrogradation toobecome principal existant de hello une base de données secondaire. Cette instruction est exécutée sur la base de données master hello sur serveur de logique de base de données SQL Azure hello dans le hello géorépliqué base de données secondaire qui est promu réside. Cette fonctionnalité est conçue pour le basculement planifié, comme pendant les exercices de récupération d’urgence de hello et requiert que cette base de données primaire hello soient disponibles.

commande Hello exécute hello suivant du flux de travail :

1. Temporairement les commutateurs toosynchronous mode de réplication à l’origine de toutes les transactions en attente toobe vidées toohello secondaire et le blocage de toutes les nouvelles transactions ;
2. Commutateurs hello rôles hello deux bases de données en partenariat de géo-réplication hello.  

Cette séquence garantit que hello deux bases de données sont synchronisées avant que les rôles hello basculer et par conséquent, aucune perte de données ne se produit. Il existe une courte période pendant laquelle les deux bases de données ne sont pas disponibles (dans l’ordre hello de 0 seconde too25) pendant le basculement des rôles de hello. Si la base de données primaire hello a plusieurs bases de données secondaires, commande hello sera automatiquement reconfigure hello autres bases de données secondaires tooconnect toohello nouveau réplica principal.  toute l’opération Hello doit prendre moins d’une minute toocomplete dans des circonstances normales. Pour plus d’informations, consultez [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) et [Niveaux de service](sql-database-service-tiers.md).

Utilisez hello suivant les étapes tooinitiate un basculement planifié.

1. Dans Management Studio, connectez-vous serveur logique de toohello base de données SQL Azure dans lequel réside une base de données secondaire géo-répliquées.
2. Ouvrez le dossier de bases de données hello, développez hello **bases de données système** dossier, avec le bouton droit sur **master**, puis cliquez sur **nouvelle requête**.
3. Utilisez hello suivante **ALTER DATABASE** rôle principal toohello de base de données secondaire hello instruction tooswitch.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Cliquez sur **Execute** requête de hello toorun.

> [!NOTE]
> Dans de rares cas, il est possible que les opération hello ne peut pas terminer et qu’il peuvent apparaître bloquée. Dans ce cas, utilisateur de hello peut exécuter la commande de basculement de force hello et accepter la perte de données.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>Initier un basculement non planifié à partir de la base de données secondaire de toohello base de données primaire hello
Vous pouvez utiliser hello **ALTER DATABASE** instruction toopromote un base de données secondaire toobecome hello nouveau principal de base de données de façon non planifiée, en forçant la rétrogradation de toobecome principal existant de hello hello une base de données secondaire à la fois lorsque hello base de données primaire n’est plus disponible. Cette instruction est exécutée sur la base de données master hello sur serveur de logique de base de données SQL Azure hello dans le hello géorépliqué base de données secondaire qui est promu réside.

Cette fonctionnalité est conçue pour la récupération d’urgence lors de la disponibilité de restauration de base de données hello est importante et une perte de données est acceptable. Lorsque le basculement forcé est appelé, hello spécifié de base de données secondaire devient la base de données primaire hello immédiatement et commence à accepter les transactions d’écriture. Dès que la base de données primaire d’origine hello est en mesure de tooreconnect avec cette nouvelle base de données primaire, une sauvegarde incrémentielle est effectuée sur la base de données primaire d’origine hello et base de données primaire ancien hello est effectuée dans une base de données secondaire pour hello nouvelle base de données primaire ; par la suite, il est simplement un réplica de synchroniser de nouveau réplica principal de hello.

Toutefois, étant donné que la limite de temps de restauration n'est pas pris en charge sur les bases de données secondaires hello, si hello glissière toorecover les données validées toohello ancienne base de données primaire qui n’avait pas été répliquées toohello base de données primaire avant hello forcé basculement s’est produite, Hello devra tooengage prise en charge toorecover cette perte de données.

Si la base de données primaire hello a plusieurs bases de données secondaires, commande hello sera automatiquement reconfigure hello autres bases de données secondaires tooconnect toohello nouveau réplica principal.

Utilisez hello suivant les étapes tooinitiate un basculement non planifié.

1. Dans Management Studio, connectez-vous serveur logique de toohello base de données SQL Azure dans lequel réside une base de données secondaire géo-répliquées.
2. Ouvrez le dossier de bases de données hello, développez hello **bases de données système** dossier, avec le bouton droit sur **master**, puis cliquez sur **nouvelle requête**.
3. Utilisez hello suivante **ALTER DATABASE** rôle principal toohello de base de données secondaire hello instruction tooswitch.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Cliquez sur **Execute** requête de hello toorun.

> [!NOTE]
> Si la commande hello est émis lorsque le principal et secondaire sont en ligne ancien serveur principal de hello deviendra hello nouveau serveur secondaire immédiatement, sans la synchronisation des données. Si hello principal est la validation des transactions lors de la commande hello est émise une perte de données peuvent se produire.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Après le basculement, vérifiez les conditions d’authentification hello pour votre serveur et de la base de données sont configurées sur le nouveau réplica principal de hello. Pour plus d’informations, consultez [Gestion de la sécurité de la base de données SQL Azure après la récupération d’urgence](sql-database-geo-replication-security-config.md).
* toolearn reprise après un sinistre à l’aide de géo-réplication active, y compris les étapes de récupération avant et après la reprise et l’exécution d’un exercice de récupération d’urgence, consultez [la récupération d’urgence](sql-database-disaster-recovery.md)
* Consultez le billet de blog publié par Sasha Nosov concernant la géoréplication active : [Coup de projecteur sur les nouvelles fonctionnalités de géoréplication](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/).
* Pour plus d’informations sur la conception de cloud applications toouse géo-réplication active, consultez [conception d’applications cloud pour la continuité d’activité à l’aide de géo-réplication](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Pour plus d’informations sur la géoréplication active avec des pools élastiques, voir [Stratégies de récupération d’urgence de pool élastique](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* Pour une vue d’ensemble de la continuité des activités, voir [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).

