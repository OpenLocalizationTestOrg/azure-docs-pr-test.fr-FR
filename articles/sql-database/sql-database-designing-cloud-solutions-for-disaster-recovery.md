---
title: "aaaDesign service hautement disponible à l’aide de la base de données SQL Azure | Documents Microsoft"
description: "Découvrez comment concevoir des applications pour des services hautement disponibles à l’aide d’Azure SQL Database."
keywords: "récupération d’urgence cloud, solutions de récupération d’urgence, sauvegarde de données d’application, géo-réplication, planification de la continuité des activités"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Conception de services hautement disponibles à l’aide d’Azure SQL Database

Pour créer et déployer des services hautement disponibles sur la base de données SQL Azure, vous utilisez [basculement géo-réplication active et les groupes](sql-database-geo-replication-overview.md) échecs de tooregional tooprovide résilience et les pannes catastrophiques et activer une récupération rapidement toohello des bases de données secondaires. Cet article se concentre sur les modèles d’application courants et explique les avantages de hello et les compromis de chaque option selon les exigences de déploiement application hello, contrat de niveau de service hello vous ciblez, la latence du trafic et les coûts. Pour plus d’informations sur la géoréplication active avec des pools élastiques, voir [Stratégies de récupération d’urgence de pool élastique](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Modèle de conception 1 : Déploiement actif/passif pour la récupération d’urgence cloud avec une base de données colocalisée
Cette option est idéale pour les applications avec hello suivant caractéristiques :

* Instance active dans une seule région Azure
* Forte dépendance sur toodata d’accès en lecture-écriture (RW)
* Connectivité entre régions entre l’application web hello et de la base de données hello n’est pas acceptable en raison du coût toolatency et le trafic    

Dans ce cas, topologie de déploiement d’application hello est optimisée pour la gestion des sinistres régionales lorsque tous les composants d’application sont affectés et doivent toofailover en tant qu’unité. Pour assurer la redondance géographique, logique de l’application hello et la base de données hello sont répliquées tooanother région, mais elles ne sont utilisées pour la charge de travail application hello dans des conditions normales hello. application Hello dans la région secondaire hello doit être configuré toouse SQL connexion chaîne toohello base de données secondaire. Gestionnaire de trafic est configuré toouse [méthode de routage de basculement](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) est utilisé dans cet article aux fins d’illustration uniquement. Vous pouvez utiliser toute solution d’équilibrage de charge qui prend en charge la méthode de routage du trafic par basculement.    
>

Hello suivant le diagramme illustre cette configuration avant la panne.

![Configuration de la géoréplication de SQL Database. Récupération d’urgence cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Après une panne dans la région principale de hello, service de base de données SQL hello détecte cette base de données primaire hello n’est pas accessible et déclencher un basculement toohello base de données secondaire basé sur les paramètres de stratégie de basculement automatique hello hello. Selon le contrat SLA de votre application, vous pouvez décider tooconfigure une période de grâce entre la détection de panne de hello hello et basculement hello lui-même. Configuration d’une période de grâce de réduit le risque de hello de cas de toohello perte données où la panne de hello est grave et la disponibilité dans la région de hello ne peut pas être restaurée rapidement. Si le basculement de point de terminaison hello est initiée par le Gestionnaire de trafic hello avant que les déclencheurs de groupe de basculement hello hello basculement de base de données hello, application hello n’est pas en mesure de tooreconnect toohello base de données. tooreconnect de tentative de l’application Hello réussit automatiquement dès que le basculement de base de données hello est terminé. 

> [!NOTE]
> tooachieve coordonnée entièrement le basculement d’application hello et bases de données hello, vous devez concevoir votre propre méthode d’analyse et utiliser le basculement manuel de terminaison d’application web hello et bases de données hello.
>

Après basculement hello de l’application hello points de terminaison et de la base de données hello, application hello redémarre le traitement des demandes d’utilisateur hello dans la région de hello B et restera colocalisée avec la base de données hello, car la base de données primaire hello est désormais dans région B. Ce scénario est illustré dans hello suivant schéma. Dans tous les diagrammes, des lignes pleines indiquent les connexions actives, des lignes en pointillé indiquent les connexions suspendues et les symboles « stop » indiquent les déclencheurs d’action.

![Géo-réplication : Base de données basculement toosecondary. Sauvegarde de données d’application.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

Si une panne se produit dans la région secondaire hello, hello le lien de réplication entre hello principal et de la base de données secondaire hello est suspendu mais hello basculement n’est pas déclenché, car la base de données primaire hello n’est pas affectée. disponibilité de l’application Hello n’est pas modifiée dans ce cas, mais application hello fonctionne exposé, et par conséquent à des risques plus élevés dans les cas les deux régions échouent à la suite.

> [!NOTE]
> Récupération d’urgence, nous vous recommandons de configuration hello avec application déploiement limité tootwo régions. C’est parce que la plupart des Hello géographiques Azure ont uniquement deux régions. Cette configuration ne protège pas votre application d’une défaillance irrémédiable simultanée des deux régions.  Dans le cas peu probable d’une telle défaillance, vous pouvez restaurer vos bases de données dans une région tierce à l’aide de [l’opération de géo-restauration](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Une fois la panne de hello est atténuée, base de données secondaire hello RE-synchronise automatiquement avec hello principal. Pendant la synchronisation, performances de hello principal pourraient être affectées légèrement en fonction du montant hello de données qui doivent toobe synchronisé. Hello diagramme suivant illustre une panne dans la région secondaire hello.

![Synchronisation de la base de données secondaire avec la base de données primaire. Récupération d’urgence cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

clé de Hello **avantages** de ce modèle de conception sont :

* Bonjour même application web est régions tooboth déployé sans aucune configuration spécifique à la région et aucun basculement ne toohello tooreact une logique supplémentaire. 
* performances de l’application Hello ne sont pas affecté par le basculement en tant qu’application web de hello et base de données hello sont toujours colocalisés.

Hello principal **compromis** qui est l’application redondant hello instance dans la région secondaire hello est uniquement utilisée pour la récupération d’urgence.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Modèle de conception 2 : Déploiement actif / actif pour l’équilibrage de charge d’applications
Cette option de récupération d’urgence cloud est idéale pour les applications avec hello suivant caractéristiques :

* Taux élevé de base de données lit toowrites
* Base de données de latence de lecture est plus importante pour l’utilisateur final hello que la latence d’écriture hello 
* La logique de lecture seule peut être séparée de la logique de lecture-écriture à l’aide d’une chaîne de connexion différente.
* Logique en lecture seule ne dépend pas de données qui est entièrement synchronisées avec les dernières mises à jour de hello  

Si vos applications ont ces caractéristiques, équilibrage de charge les connexions de l’utilisateur final hello sur plusieurs instances d’application dans différentes régions peut améliorer considérablement hello expérience utilisateur globale. Deux des régions de hello doit être sélectionné en tant que paire de récupération d’urgence de hello et groupe de basculement hello doit inclure des bases de données hello dans ces régions. tooimplement équilibrage de charge, chaque région doit avoir une instance active de l’application hello avec hello en lecture-écriture (RW) logique connectée toohello en lecture-écriture écouteur point de terminaison du groupe de basculement hello. Il garantit que le basculement hello va être lancé automatiquement si la base de données primaire hello est affectée par une panne. Hello en lecture seule logique (RO) dans l’application web de hello doit se connecter directement de la base de données toohello dans cette région. Traffic manager doit être défini toouse [performances routage](../traffic-manager/traffic-manager-configure-performance-routing-method.md) avec [surveillance de point de terminaison](../traffic-manager/traffic-manager-monitoring.md) activé pour chaque instance d’application.

Comme dans le modèle 1, vous devez envisager le déploiement d’une application de surveillance similaire. Mais contrairement au modèle #1, hello analyse de l’application ne sera pas chargé de déclencher le basculement de point de terminaison hello.

> [!NOTE]
> Bien que ce modèle utilise plusieurs bases de données secondaires, uniquement les hello secondaire dans la région B serait utilisée pour le basculement et doit faire partie du groupe de basculement hello.
>

Gestionnaire de trafic doit être configuré pour l’emplacement géographique de performances routage toodirect hello connexions toohello application instance le plus proche toohello utilisateur. Hello suivant le diagramme illustre cette configuration avant la panne.

![Aucune panne : application toonearest routage de performances. Géoréplication.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Si une panne de la base de données est détectée dans la région de hello A, groupe de basculement hello lance automatiquement le basculement de la base de données primaire hello dans la région A toohello secondaire dans la région B. Il met automatiquement à jour tooregion de point de terminaison en lecture-écriture écouteur hello B pour les connexions en lecture-écriture dans l’application web de hello ne seront pas affectées. Gestionnaire de trafic Hello exclura point d’arrêt hello hors connexion à partir de la table de routage hello mais continue de routage hello par l’utilisateur le trafic toohello restantes des instances en ligne. Hello en lecture seule des chaînes de connexion SQL ne sont pas affectés car elles pointent toujours de la base de données toohello Bonjour même région. 

Hello suivant schéma illustre la nouvelle configuration de hello après le basculement de hello.

![Configuration après le basculement. Récupération d’urgence cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

En cas de panne de l’une des zones secondaires de hello, Gestionnaire de trafic hello supprimera automatiquement point de terminaison hors connexion hello dans cette région à partir de la table de routage hello. Hello réplication canal toohello base de données secondaire dans cette région sera interrompu. Étant donné que les autres zones de hello obtenir le trafic des utilisateurs supplémentaires dans ce scénario, les performances de l’application hello seront affectés pendant une panne de hello. Une fois la panne de hello est atténuée, hello une base de données secondaire dans la région concernée hello est immédiatement synchronisé avec hello principal. Au cours de hello des performances de synchronisation de hello principal pourraient être affectées légèrement en fonction du montant hello de données qui doivent toobe synchronisé. Hello suivant schéma illustre une panne dans la région B.

![Panne dans une région secondaire. Récupération d’urgence cloud - géoréplication.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

clé de Hello **parti** de cette conception de modèle est que vous pouvez faire évoluer la charge de travail application hello entre les performances optimales de l’utilisateur final de plusieurs bases de données secondaires tooachieve hello. Hello **compromis** de cette option sont :

* Connexions en lecture-écriture entre les instances de l’application hello et la base de données ont différentes de latence et de coût
* Panne de hello sont affecte les performances de l’application

> [!NOTE]
> Une approche similaire peut être utilisée toooffload spécialisé des charges de travail tels que reporting des travaux, les outils d’analyse décisionnelle ou les sauvegardes. En règle générale, ces charges de travail consomment des ressources de base de données importantes par conséquent, il est recommandé de désigner un des hello bases de données secondaires pour les hello performances toohello correspondant au niveau anticipé la charge de travail.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Modèle de conception 3 : Déploiement actif / passif pour la conservation des données
Cette option est idéale pour les applications avec hello suivant caractéristiques :

* Toute perte de données constitue un risque élevé pour l’entreprise. basculement de base de données Hello utilisable uniquement en dernier recours si une panne de hello est grave.
* application Hello prend en charge les modes lecture seule et en lecture-écriture d’opérations et peut fonctionner en « mode en lecture seule » pendant une période de temps.

Dans ce modèle, application hello bascule en mode tooread uniquement lorsque les connexions en lecture-écriture hello commencent à recevoir des erreurs de délai d’attente. Hello Application Web est déployée tooboth régions et inclure un point de terminaison de connexion toohello en lecture-écriture écouteur et le point de terminaison de connexion différentes toohello écouteur en lecture seule. Hello Traffic manager doit être défini toouse [basculement routage](../traffic-manager/traffic-manager-configure-failover-routing-method.md) avec [surveillance de point de terminaison](../traffic-manager/traffic-manager-monitoring.md) activée pour le point de terminaison application hello dans chaque région.

Hello suivant le diagramme illustre cette configuration avant la panne.

![Déploiement actif/passif avant le basculement. Récupération d’urgence cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Lorsque hello traffic manager détecte une tooregion Échec de connectivité A, il bascule automatiquement instance application toohello du trafic utilisateur dans la région B. Avec ce modèle, il est important que vous définissiez période de grâce de hello avec une valeur suffisamment élevée des données perte tooa, par exemple, 24 heures. Elle ne garantit pas que la perte de données est bloquée si la panne de hello est atténuée dans ce délai. Lorsque hello application Web dans la région de hello B est activé les opérations de lecture-écriture hello mettent à échouer. À ce stade, il doit basculer toohello en lecture seule. Bonjour de ce mode, les requêtes seront toohello automatiquement vers la base de données secondaire. Dans les cas de hello d’un Bonjour défaillance grave panne n’est pas réduit au sein de la période de grâce de hello et groupe de basculement hello déclenchera hello basculement. Après cette hello en lecture-écriture écouteur devient disponible et hello appels tooit arrête échouent. Cela est illustré par hello suivant schéma.

![Panne : l’application en mode lecture seule. Récupération d’urgence cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Si la panne hello dans la région principale de hello est atténuée au sein de la période de grâce de hello, traffic manager détecte restauration hello de connectivité dans la région principale de hello et bascule l’instance d’application utilisateur trafic toohello précédent dans la région A. Cette instance de l’application reprend et qu’il fonctionne en mode lecture-écriture à l’aide de la base de données primaire hello dans la région A.

En cas de panne dans la région de hello B, hello traffic manager détecte les échec hello de point de terminaison application hello dans la région B et hello basculement groupe commutateurs hello écouteur en lecture seule tooregion A. Cette panne n’affecte pas l’utilisateur final hello mais la base de données primaire hello sera exposé panne hello. Cela est illustré par hello suivant schéma.

![Panne : base de données secondaire. Récupération d’urgence cloud.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Une fois la panne de hello est atténuée, hello base de données secondaire est immédiatement synchronisé avec hello principal et écouteur en lecture seule de hello est commuté toohello précédent la base de données secondaire dans la région B. Lors de la synchronisation de hello principal peut légèrement affecte les performances en fonction du montant hello de données qui doivent toobe synchronisé.

Ce modèle de conception offre plusieurs **avantages**:

* Elle évite la perte de données pendant les pannes temporaires hello.
* Temps d’arrêt dépend uniquement la rapidité avec laquelle traffic manager détecte la panne de connectivité hello, qui est configurable.

Hello **compromis** est :

* Application doit être en mesure de toooperate en mode lecture seule.

> [!NOTE]
> En cas de panne de service permanente dans la région de hello, vous manuellement activez le basculement de la base de données et acceptez la perte de données hello. application Hello seront fonctionnelle dans la région secondaire hello avec la base de données toohello accès en lecture-écriture.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>Planification de la continuité des activités : choisir une conception d’application pour la récupération d’urgence cloud
Votre stratégie de récupération d’urgence cloud spécifique peut combiner ou étendre ces modèles de conception toobest les besoins de hello satisfait de votre application.  Comme indiqué précédemment, les choix de la stratégie hello est basée sur hello SLA vous souhaiter que les clients de tooyour toooffer et hello topologie de déploiement d’application. toohelp guider votre décision, hello tableau suivant compare les choix de hello en fonction de hello données estimée perte ou récupération objectif de point (RPO) et le temps de récupération estimé (ERT).

| Modèle | RPO | ERT |
|:--- |:--- |:--- |
| Déploiement actif / passif pour la récupération d’urgence avec accès à la base de données colocalisée |Accès en lecture-écriture < 5 s |Temps de détection des défaillances + TTL du DNS |
| Déploiement actif / actif pour l’équilibrage de charge d’applications |Accès en lecture-écriture < 5 s |Temps de détection des défaillances + TTL du DNS |
| Déploiement actif / passif pour la conservation des données |Accès en lecture seule < 5 s | Accès en lecture seule = 0 |
||Accès en lecture-écriture = 0 | Accès en lecture-écriture = temps de détection de défaillances + période de grâce en cas de risque de perte de données |
|||

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur les sauvegardes de base de données SQL Azure automatisée, consultez [sauvegardes automatisées de base de données SQL](sql-database-automated-backups.md)
* Pour une vue d’ensemble de la continuité des activités et des scénarios, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md)
* toolearn sur l’utilisation des sauvegardes automatisées pour la récupération, consultez [restaurer une base de données à partir de sauvegardes de hello initiées par le service](sql-database-recovery-using-backups.md)
* toolearn sur les options de récupération plus rapides, consultez [géo-réplication active](sql-database-geo-replication-overview.md)  
* toolearn sur l’utilisation des sauvegardes automatisées pour l’archivage, consultez [copie de base de données](sql-database-copy.md)
* Pour plus d’informations sur la géoréplication active avec des pools élastiques, voir [Stratégies de récupération d’urgence de pool élastique](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
