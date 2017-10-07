---
title: "récupération d’urgence de base de données d’aaaSQL | Documents Microsoft"
description: "Découvrez comment toorecover une base de données à partir d’un centre de données régional ou panne avec hello active géo-réplication de base de données SQL Azure et des fonctions de géo-restauration."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>Restaurer une base de données SQL Azure ou le basculement de tooa secondaire
Base de données SQL Azure offre hello suivant les fonctionnalités de récupération à partir d’une panne :

* [Géo-réplication active](sql-database-geo-replication-overview.md)
* [Géorestauration](sql-database-recovery-using-backups.md#point-in-time-restore)

toolearn sur les scénarios de continuité des activités et les fonctionnalités de hello prenant en charge ces scénarios, consultez [continuité](sql-database-business-continuity.md).

### <a name="prepare-for-hello-event-of-an-outage"></a>Préparer pour l’événement hello d’une indisponibilité
Pour la réussite de région de données tooanother de récupération à l’aide de géo-réplication active ou sauvegardes géo-redondant, vous devez tooprepare un serveur dans un autre données center panne toobecome hello nouveau serveur principal doit hello doivent survenir ainsi que des étapes bien définis tooensure documentée et testée une récupération lisse. Les étapes de préparation sont les suivantes :

* Identifiez le serveur logique de hello dans une autre région toobecome hello nouveau serveur principal. Avec la géo-réplication active, il s’agit d’au moins un et peut-être chacun des serveurs secondaires de hello. Pour la géo-restauration, il s’agira généralement un serveur Bonjour [région associée](../best-practices-availability-paired-regions.md) pour la région de hello dans lequel se trouve votre base de données.
* Identifier et éventuellement définir, les règles de pare-feu de niveau serveur hello nécessaires sur des utilisateurs tooaccess hello nouvelle base de données primaire.
* Déterminez comment vous allez tooredirect utilisateurs toohello nouveau serveur principal, par exemple en modifiant des chaînes de connexion ou en modifiant les entrées DNS.
* Identifier, vous pouvez également créer, hello connexions qui doivent être présents dans la base de données master hello sur le serveur principal de hello nouvelle, vérifiez que ces connexions disposer des autorisations appropriées dans la base de données master hello, le cas échéant. Pour plus d’informations, consultez [Gestion de la sécurité de la base de données SQL après la récupération d’urgence](sql-database-geo-replication-security-config.md)
* Identifier les règles d’alerte qui devront toobe toomap mis à jour toohello nouvelle base de données primaire.
* Configuration de l’audit hello document sur la base de données primaire actuelle hello
* Effectuez une [simulation d’une récupération d'urgence](sql-database-disaster-recovery-drills.md). toosimulate une interruption de géo-restauration, vous pouvez supprimer ou renommer l’échec de connectivité d’application toocause hello source de base de données. toosimulate une interruption de géo-réplication active, vous pouvez désactiver hello web défaillances des applications ou ordinateur virtuel connecté toohello base de données ou de basculement hello de base de données toocause application connectivité.

## <a name="when-tooinitiate-recovery"></a>Lors de la récupération de tooinitiate
opération de récupération Hello affecte l’application hello. Il nécessite la modification de la chaîne de connexion SQL hello ou une redirection à l’aide de DNS et peut entraîner une perte de données permanentes. Par conséquent, il doit être effectuée uniquement lors de la panne de hello est probablement toolast plu de l’objectif de temps de récupération de votre application. Lors de l’application hello est tooproduction déployée, vous devez effectuer une surveillance régulière d’intégrité d’application hello et utiliser hello tooassert points qui hello récupération est garantie des données suivantes :

1. Échec de la connexion permanente à partir de la base de données toohello application hello.
2. Hello portail Azure affiche une alerte sur un incident dans la région de hello avec un large impact.
3. serveur de base de données SQL Azure Hello est marqué comme étant dégradé.

En fonction de votre responsabilité de business application tolérance toodowntime et possible, vous pouvez envisager hello suivant les options de récupération.

Hello d’utilisation [obtenir une base de données récupérables](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) tooget hello géo-répliquées de restauration les plus récentes.

## <a name="wait-for-service-recovery"></a>Attendre le rétablissement du service
Bonjour Azure équipes travaillent soigneusement toorestore disponibilité du service comme rapidement que possible, mais en fonction de la cause première hello peut prendre heures ou jours.  Si votre application peut tolérer des temps d’arrêt important, vous pouvez simplement attendre hello récupération toocomplete. Dans ce cas, aucune action n’est requise de votre part. Vous pouvez voir l’état du service actuel hello sur notre [tableau de bord d’intégrité de Service Azure](https://azure.microsoft.com/status/). Après la récupération de hello de région de hello disponibilité de votre application sera restaurée.

## <a name="fail-over-toogeo-replicated-secondary-database"></a>Basculer répliqué toogeo la base de données secondaire
Si les temps d’arrêt peuvent mettre en cause la responsabilité de votre entreprise, vous devez utiliser des bases de données géo-répliquées dans votre application. Cela activera la disponibilité de restauration hello application tooquickly dans une région différente en cas de panne. Découvrez comment trop[configurer la géo-réplication](sql-database-geo-replication-portal.md).

disponibilité toorestore Hello bases de données vous devez tooinitiate hello basculement toohello géorépliqué base de données secondaire à l’aide d’une des méthodes de hello pris en charge.

Utilisez une des hello suivant toofail de guides sur tooa géorépliqué base de données secondaire :

* [Basculer tooa géorépliqué base de données secondaire à l’aide du portail Azure](sql-database-geo-replication-portal.md)
* [Basculer secondaire de géo-répliquées tooa à l’aide de PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [Basculer tooa géorépliqué base de données secondaire à l’aide de T-SQL](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>Récupérer à l’aide de la géorestauration
Si le temps d’arrêt de votre application n’entraîne pas de la responsabilité de l’entreprise, vous pouvez utiliser [géo-restauration](sql-database-recovery-using-backups.md) comme une méthode toorecover vos bases de données d’application. Il crée une copie de base de données hello à partir de sa dernière sauvegarde géo-redondant.

## <a name="configure-your-database-after-recovery"></a>Configurer votre base de données après récupération
Si vous utilisez la géo-réplication de basculement ou de toorecover géo-restauration en cas de panne, il se peut que vous devez vous assurer que hello connectivité toohello nouvelles bases de données est correctement configuré afin que la fonction d’application normal hello peut être reprise. Ceci est une liste des tâches tooget votre prêt de production de base de données récupérée.

### <a name="update-connection-strings"></a>Mettre à jour les chaînes de connexion
Étant donné que votre base de données récupérée résident dans un autre serveur, vous devez tooupdate de connexion chaîne toopoint toothat du serveur de votre application.

Pour plus d’informations sur la modification des chaînes de connexion, consultez le langage de développement appropriée hello pour votre [bibliothèque de connexions de](sql-database-libraries.md).

### <a name="configure-firewall-rules"></a>Configurer les règles de pare-feu
Vous devez toomake que les règles de pare-feu hello configuré sur le serveur et sur la correspondance de base de données hello ceux qui ont été configurées sur le serveur principal de hello et de la base de données primaire. Pour plus d’informations, voir [Procédure : configuration des paramètres du pare-feu (Base de données SQL Azure)](sql-database-configure-firewall-settings.md).

### <a name="configure-logins-and-database-users"></a>Configurer les identifiants de connexion et les utilisateurs de la base de données
Vous devez toomake que toutes les connexions hello sont utilisées par votre application existent sur le serveur hello qui héberge votre base de données récupérée. Pour plus d’informations, voir [Configuration de la sécurité de la géoréplication](sql-database-geo-replication-security-config.md).

> [!NOTE]
> Vous devez configurer et tester les règles et les connexions (et leurs autorisations) du pare-feu de votre serveur pendant un exercice de récupération d’urgence. Ces objets au niveau du serveur et leur configuration peut-être pas disponibles pendant une panne de hello.
> 
> 

### <a name="setup-telemetry-alerts"></a>Configurer les alertes de télémétrie
Vous devez toomake que vos paramètres de règle d’alerte existants sont mis à jour toomap toohello hello et base de données différents serveur récupéré.

Pour en savoir plus, voir [Réception de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) et [Suivi de l’intégrité du service](../monitoring-and-diagnostics/insights-service-health.md).

### <a name="enable-auditing"></a>Activer la fonction d’audit
Si l’audit est requis tooaccess votre base de données, vous devez tooenable l’audit après la récupération de base de données hello. Pour plus d’informations, consultez [Audit de base de données](sql-database-auditing.md).

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur les sauvegardes de base de données SQL Azure automatisée, consultez [sauvegardes automatisées de base de données SQL](sql-database-automated-backups.md)
* toolearn sur les scénarios conception et de restauration de la continuité des activités métier, consultez [des scénarios de continuité des activités](sql-database-business-continuity.md)
* toolearn sur l’utilisation des sauvegardes automatisées pour la récupération, consultez [restaurer une base de données à partir de sauvegardes de hello initiées par le service](sql-database-recovery-using-backups.md)

