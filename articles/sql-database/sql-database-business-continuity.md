---
title: "continuité des activités aaaCloud - récupération de base de données - base de données SQL | Documents Microsoft"
description: "Découvrez comment Azure SQL Database prend en charge la continuité des activités cloud et la récupération de base de données et vous aide à maintenir les applications cloud opérationnelles."
keywords: "continuité des activités, continuité des activités cloud, récupération d’urgence de base de données, récupération de base de données"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>Vue d’ensemble de la continuité de l’activité avec la base de données Azure SQL

Cette présentation décrit les fonctions hello servant de base de données SQL Azure pour la continuité d’activité et de récupération d’urgence. En savoir plus sur les options, les recommandations et les didacticiels de récupération à partir des interruptions qui pourraient provoquer une perte de données ou votre toobecome de base de données et d’application non disponible. Découvrez quels toodo lorsqu’une erreur de l’utilisateur ou l’application affecte l’intégrité des données, une région Azure a une panne ou votre application requiert une maintenance.

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>Fonctionnalités de base de données SQL que vous pouvez utiliser la continuité des activités tooprovide

La base de données SQL fournit plusieurs fonctionnalités de continuité d’activité, notamment des sauvegardes automatisées et une réplication facultative de la base de données. Chacune de ces fonctionnalités possède des caractéristiques spécifiques concernant le temps de récupération estimé (ERT) et le risque de perte de données pour les transactions récentes. Une fois que vous avez compris ces options, vous pouvez choisir celles qui vous conviennent et, dans la plupart des scénarios, les utiliser ensemble dans différents scénarios. Lorsque vous développez votre plan de continuité des activités, vous devez toounderstand hello acceptable durée maximale avant que l’application hello récupère entièrement après un événement perturbateur de hello - il s’agit votre objectif de temps de récupération (RTO). Vous devez également toounderstand quantité maximale de hello d’application de hello récentes données mises à jour (intervalle de temps) peut tolérer perdre lors de la récupération après un événement perturbateur de hello - il s’agit votre objectif de point de récupération (RPO).

Hello suivant compare la table hello ERT et le RPO pour les scénarios les plus courants hello trois.

| Fonctionnalité | Niveau de base | Niveau standard | Niveau Premium |
| --- | --- | --- | --- |
| Limite de restauration dans le temps à partir de la sauvegarde |Tout point de restauration dans un délai de 7 jours |Tout point de restauration dans un délai de 35 jours |Tout point de restauration dans un délai de 35 jours |
| Géo-restauration à partir de sauvegardes répliquées géographiquement |ERT < 12 h, RPO < 1 h |ERT < 12 h, RPO < 1 h |ERT < 12 h, RPO < 1 h |
| Restauration à partir d’Azure Backup Vault |ERT < 12 h, RPO < 1 sem. |ERT < 12 h, RPO < 1 sem. |ERT < 12 h, RPO < 1 sem. |
| Géo-réplication active |ERT < 30s, RPO < 5s |ERT < 30s, RPO < 5s |ERT < 30s, RPO < 5s |

### <a name="use-database-backups-toorecover-a-database"></a>Utilisez des sauvegardes de base de données toorecover une base de données

Base de données SQL effectue automatiquement une combinaison de sauvegardes de base de données complète une fois par semaine, toutes les heures des sauvegardes différentielles de base de données, journaux des transactions et sauvegardes de toutes les cinq-dix minutes tooprotect votre entreprise contre la perte de données. Ces sauvegardes sont stockées dans le stockage géo-redondant de 35 jours pour les bases de données dans les niveaux de service Standard et Premium hello et 7 jours pour les bases de données de niveau de service Basic de hello. Pour en savoir plus, consultez les [niveaux de service](sql-database-service-tiers.md). Si la période de rétention hello pour votre niveau de service ne répond pas à vos besoins, vous pouvez augmenter la période de rétention hello en [la modification du niveau de service hello](sql-database-service-tiers.md). Hello sauvegardes complètes et différentielles de base de données sont également répliquée tooa [centre de données associés](../best-practices-availability-paired-regions.md) pour la protection contre la panne du centre de données. Pour plus d’informations, consultez la rubrique concernant les [sauvegardes de base de données automatiques](sql-database-automated-backups.md).

Si la période de rétention intégrés hello n’est pas suffisante pour votre application, vous pouvez l’étendre en configurant une stratégie de rétention à long terme de base de données. Pour plus d’informations, consultez [rétention à long terme](sql-database-long-term-retention.md).

Vous pouvez utiliser ces toorecover de sauvegardes de base de données automatique une base de données à partir de divers événements d’interruption de service, à la fois au sein de votre centre de données et le centre de données tooanother. À l’aide de sauvegardes de base de données automatique, hello estimé temps de récupération dépend de plusieurs facteurs, notamment le nombre total de hello de bases de données de récupération Bonjour même région de hello en même temps, hello la taille de la base de données, taille du journal de transactions de hello et la bande passante réseau. temps de récupération Hello est généralement inférieure à 12 heures. Lorsque vous récupérez la région de données tooanother, la perte potentielle de données hello est heure too1 limité par le stockage géo-redondant hello des sauvegardes de base de données différentielle toutes les heures.

> [!IMPORTANT]
> toorecover à l’aide des sauvegardes automatisées, vous devez être membre du rôle de collaborateur du serveur SQL hello ou propriétaire de l’abonnement hello - voir [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md). Vous pouvez récupérer à l’aide de hello portail Azure, PowerShell ou hello API REST. Vous ne pouvez pas utiliser Transact-SQL.
>

Utilisez des sauvegardes automatisées comme mécanisme de continuité d’activité et de récupération si votre application :

* N'est pas essentielle.
* N’a pas de contrat SLA contraignant, une interruption de service de 24 heures ou plus n’entraîne pas la responsabilité financière.
* A un faible taux de modification des données (basses transactions par heure) et la perte de tooan heure de modification est une perte de données acceptable.
* Est sensible aux coûts.

Si vous avez besoin d’une récupération plus rapide, utilisez une [géo-réplication active](sql-database-geo-replication-overview.md) (abordée plus loin). Si vous avez besoin d’une période antérieure à 35 jours toobe toorecover en mesure de données, utilisez [rétention de sauvegarde à long terme](sql-database-long-term-retention.md). 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>Utiliser active géo-réplication et le basculement automatique groupes (en version préliminaire) tooreduce récupération temps et limite de perte de données associée à une récupération

En outre toousing les sauvegardes de base de données pour la base de données récupération si une interruption se produit, vous pouvez utiliser [géo-réplication active](sql-database-geo-replication-overview.md) tooconfigure un toohave de base de données toofour lisible secondaire bases de données dans des régions hello de votre choix. Ces bases de données secondaires sont synchronisés avec la base de données primaire hello à l’aide d’un mécanisme de réplication asynchrone. Cette fonctionnalité est tooprotect utilisé par rapport à l’interruption de service en cas de panne du centre de données ou une mise à niveau de l’application. Géo-réplication Active peut également être utilisé tooprovide de meilleures performances de requête pour les utilisateurs toogeographically dispersé de requêtes en lecture seule.

tooenable automatisée et de basculement transparent, vous devez organiser vos bases de données répliquées en groupes à l’aide de hello [groupe de basculement automatique](sql-database-geo-replication-overview.md) fonctionnalité de base de données SQL (en version préliminaire).

Si la base de données primaire hello est mise hors connexion de façon inattendue ou si vous devez tootake hors connexion pour les activités de maintenance, vous pouvez rapidement promouvoir principal hello toobecome secondaire (également appelé un basculement) et de configurer des principal de toohello promue tooconnect applications. Si votre application se connecte toohello de bases de données à l’aide d’écouteur du groupe de basculement hello, vous n’avez pas besoin configuration de chaîne de connexion toochange hello SQL après le basculement. Le basculement planifié évite toute perte de données. Un basculement non planifié, il peut être d’une petite quantité de perte de données pour les transactions en raison de la nature de toohello très récentes de la réplication asynchrone. À l’aide de groupes de basculement automatique (en version préliminaire), vous pouvez personnaliser hello basculement stratégie toominimize hello perdre des données. Après un basculement, vous pouvez la restauration ultérieure - conséquente tooa plan ou lorsque du centre de données de hello revient en ligne. Dans tous les cas, les utilisateurs rencontrer une petite quantité de temps d’arrêt et doivent tooreconnect.

> [!IMPORTANT]
> géo-réplication active toouse et les groupes de basculement automatique (en version préliminaire), vous devez être propriétaire de l’abonnement de hello ou disposer des autorisations d’administration dans SQL Server. Vous pouvez configurer et basculer à l’aide de hello portail Azure, PowerShell ou hello API REST à l’aide d’autorisations d’abonnement Azure ou à l’aide de Transact-SQL avec des autorisations SQL Server.
> 

Utilisez la géo-réplication active et les groupes de basculement automatique (en version préliminaire) si votre application répond à l’un des critères suivants :

* Est essentielle.
* A un contrat de niveau de service (SLA) qui n’autorise pas plus de 24 heures d’interruption de service.
* Toute interruption de service peut engager la responsabilité financière.
* Affiche un taux élevé de données modifiées et la perte d’une heure de données n’est pas acceptable.
* coût supplémentaire en Hello géo-réplication active est inférieure à la responsabilité financière hello et entraîne une perte de l’entreprise.

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>Récupérer une base de données après une erreur d’utilisateur ou d’application
* Personne n’est parfait ! Un utilisateur peut supprimer par inadvertance des données, un tableau important voire une base de données tout entière. Ou bien, une application peut accidentellement bonnes données avec des données erronées en raison de l’erreur d’application tooan.

Dans ce scénario, voici les options de récupération dont vous disposez.

### <a name="perform-a-point-in-time-restore"></a>Effectuer une limite de restauration dans le temps
Vous pouvez utiliser hello automatisée sauvegardes toorecover une copie de votre tooa de base de données appelée point de référence dans le temps, pour autant que l’heure est au sein de la période de rétention de base de données hello. Après la restauration de la base de données hello, vous pouvez remplacer la base de données d’origine hello avec la base de données restaurée de hello ou copier des données de hello nécessité à partir des données de hello restauré dans la base de données d’origine hello. Si la base de données hello utilise la géo-réplication active, nous vous recommandons de copier les données de hello requis à partir de la copie de hello restauré dans la base de données d’origine hello. Si vous remplacez la base de données d’origine hello avec la base de données restaurée de hello, vous devez tooreconfigure et resynchronisez les géo-réplication active (ce qui peut prendre un certain temps pour une base de données volumineux).

Pour plus d’informations et pour obtenir des instructions détaillées pour la restauration d’un point de tooa de base de données à l’aide de l’heure hello portail Azure ou à l’aide de PowerShell, consultez [point-à-temps restauration](sql-database-recovery-using-backups.md#point-in-time-restore). Vous ne pouvez pas effectuer une récupération à l’aide de Transact-SQL.

### <a name="restore-a-deleted-database"></a>restauration d’une base de données supprimée.
Si hello de base de données est supprimée, mais le serveur logique de hello n’a pas été supprimé, vous pouvez restaurer le point de toohello hello supprimé de base de données à laquelle il a été supprimé. Cette opération restaure un toohello de sauvegarde de base de données même logique SQL server à partir de laquelle il a été supprimé. Vous pouvez restaurer à l’aide du nom d’origine de hello ou fournir un nouveau nom ou la base de données restaurée de hello.

Pour plus d’informations et pour obtenir des instructions détaillées pour la restauration d’une base de données supprimée à l’aide de hello portail Azure ou à l’aide de PowerShell, consultez [restaurer une base de données supprimée](sql-database-recovery-using-backups.md#deleted-database-restore). Vous ne pouvez pas restaurer à l’aide de Transact-SQL.

> [!IMPORTANT]
> Si le serveur logique de hello est supprimé, vous ne pouvez pas récupérer une base de données supprimée.
>
>

### <a name="restore-from-azure-backup-vault"></a>Restauration à partir d’Azure Backup Vault
Si la perte de données hello s’est produite en dehors de la période de rétention actuelle hello pour les sauvegardes automatisées et votre base de données est configurée pour la rétention à long terme, vous pouvez restaurer à partir d’une sauvegarde hebdomadaire dans le coffre de sauvegarde Azure tooa nouvelle base de données. À ce stade, vous pouvez remplacer la base de données d’origine hello avec la base de données restaurée de hello ou copier des données de hello nécessité à partir de la base de données hello restauré dans la base de données d’origine hello. Si vous devez tooretrieve une ancienne version de votre mise à niveau de base de données antérieure tooa application majeures, satisfaire une demande à partir de comptes ou d’un ordre juridique, que vous pouvez créer une base de données à l’aide d’une sauvegarde complète est enregistrée dans hello coffre de sauvegarde Azure.  Pour plus d’informations, consultez [Rétention à long terme](sql-database-long-term-retention.md).

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>Récupérer une région tooanother de base de données à partir d’une panne de centre de données régional Azure
<!-- Explain this scenario -->

Bien que le fait soit rare, un centre de données Azure peut subir une panne. En cas de panne, il entraîne une interruption de service qui peut durer de quelques minutes à plusieurs heures.

* Une option consiste toowait pour votre toocome de la base de données en ligne lors de la panne de centre de données hello. Cela fonctionne pour les applications qui supportent toohave hello de base de données hors connexion. Par exemple, un projet de développement ou de la version d’évaluation gratuite vous n’avez pas besoin toowork sur constamment. Lorsqu’un centre de données a une panne, vous ne connaissez pas la durée pendant laquelle la panne de hello peut durer, afin que cette option fonctionne uniquement si vous n’avez pas besoin votre base de données pendant un certain temps.
* Une autre option consiste tooeither échouent sur la région de données tooanother si vous utilisez géo-réplication active ou hello récupérer une base de données à l’aide de sauvegardes de base de données de géo-redondant (géo-restauration). Un basculement ne prend que quelques secondes, tandis qu’une récupération de base de données à partir de sauvegardes nécessite des heures.

Lorsque vous intervenez, combien de temps cela vous prend toorecover et combien vous entraîner une perte de données dépend de votre décision toouse ces fonctionnalités de continuité d’activité d’entreprise dans votre application. En effet, vous pouvez choisir toouse une combinaison de sauvegardes de base de données et de géo-réplication active en fonction des exigences de votre application. Pour plus d’informations sur la conception d’applications pour des bases de données autonomes et des pools élastiques à l’aide de ces fonctionnalités de continuité d’activité, consultez [Conception d’applications pour la récupération d’urgence cloud](sql-database-designing-cloud-solutions-for-disaster-recovery.md) et [Stratégies de récupération d’urgence de pool élastique](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

Hello sections suivantes fournissent une vue d’ensemble de toorecover d’étapes hello à l’aide de sauvegardes de base de données ou de géo-réplication active. Pour des instructions détaillées, y compris la planification de la configuration requise, des étapes de récupération post et plus d’informations sur comment toosimulate un tooperform panne une récupération d’urgence permet d’accéder, consultez [récupérer une base de données SQL à partir d’une panne](sql-database-disaster-recovery.md).

### <a name="prepare-for-an-outage"></a>Se préparer à une panne
Quelle que soit la fonctionnalité de continuité des activités métier hello que vous utilisez, vous devez :

* Identifiez et préparer le serveur cible de hello, y compris les règles de pare-feu de niveau serveur, les connexions et les autorisations de niveau base de données master.
* Déterminer comment tooredirect client applications toohello nouveau serveur et les clients
* Documenter les autres dépendances, notamment les paramètres d’audit et les alertes

Si la préparation n’est pas effectuée correctement, la mise en ligne de vos applications après un basculement ou une récupération de base de données prend plus de temps et nécessite probablement de résoudre certains problèmes dans une situation de stress, ce qui constitue une combinaison très risquée.

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>Basculer tooa géorépliqué base de données secondaire
Si vous utilisez la géo-réplication active et les groupes de basculement automatique (en version préliminaire) comme mécanisme de récupération, vous pouvez configurer une stratégie de basculement automatique ou utiliser le [basculement manuel](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database). Une fois démarrée, hello basculement causes hello secondaire toobecome hello nouveau principal et prêt toorecord nouvelles transactions et répondre tooqueries - avec perte de données minimale pour les données de salutation n’ont pas encore été répliquées. Pour plus d’informations sur la conception de processus de basculement hello, consultez [concevoir une application cloud de récupération d’urgence](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

> [!NOTE]
> Lorsque le centre de données hello revient en ligne indistinctement ancien de hello automatiquement reconnecter toohello nouveau réplica principal et deviennent des bases de données secondaires. Si vous avez besoin de la région d’origine toorelocate hello principal toohello précédent, vous pouvez lancer manuellement un basculement planifié (restauration). 
> 

### <a name="perform-a-geo-restore"></a>Effectuer une restauration géographique
Si vous utilisez des sauvegardes automatisées avec une réplication de stockage géo-redondant comme mécanisme de récupération, [lancez une récupération de base de données à l’aide de la géo-restauration](sql-database-disaster-recovery.md#recover-using-geo-restore). Récupération a généralement lieu dans les 12 heures, avec une perte de données les horaires tooone déterminé par lors hello de la dernière horaire sauvegarde différentielle effectuée et répliquées. Jusqu'à ce que la récupération de hello terminée, hello ou base de données toorecord Impossible de toutes les transactions répond tooany requêtes. Cette opération restaure un base de données toohello dernier disponible point dans le temps, restauration hello géo-réplication secondaire tooany point dans le temps n'est pas actuellement prise en charge.

> [!NOTE]
> Si le centre de données hello revient en ligne avant de basculer sur la base de données récupérée toohello votre application, vous pouvez annuler la récupération de hello.  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>Exécution de tâches de post-basculement/récupération
Après la récupération à partir d’un mécanisme de récupération, vous devez effectuer hello suivant des tâches supplémentaires avant de sauvegarder vos utilisateurs et les applications et en cours d’exécution :

* Rediriger les clients et de client applications toohello nouveau serveur et de base de données restaurée
* Vérifiez les règles de pare-feu au niveau du serveur appropriées sont en place pour les utilisateurs tooconnect (ou utilisez [pare-feu de niveau base de données](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* Vérifier que les connexions et les autorisations appropriées au niveau de la base de données MASTER sont en place (ou utiliser des [utilisateurs contenus](https://msdn.microsoft.com/library/ff929188.aspx))
* Configurer l’audit, selon les besoins
* Configurer les alertes, selon les besoins

## <a name="upgrade-an-application-with-minimal-downtime"></a>Mettre à niveau une application avec un temps d’arrêt minimal
Parfois, une application doit être déconnectée en raison d’une maintenance planifiée, par exemple une mise à niveau. [Gérer les mises à niveau de l’application](sql-database-manage-application-rolling-upgrade.md) décrit comment tooenable de géo-réplication active toouse propagée de votre cloud toominimize interruptions de service au cours de mises à niveau et de fournir un chemin de récupération si une erreur survient. 

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la conception d’applications pour des bases de données autonomes et des pools élastiques, consultez [Conception d’applications pour la récupération d’urgence cloud](sql-database-designing-cloud-solutions-for-disaster-recovery.md) et [Stratégies de récupération d’urgence de pool élastique](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
