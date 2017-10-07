---
title: aaaHow tooconfigure Cache Redis Azure | Documents Microsoft
description: "Configuration de Redis hello par défaut pour le Cache Redis Azure de découvrir et comprendre comment tooconfigure votre Azure Redis Cache des instances"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>Comment tooconfigure Cache Redis Azure
Cette rubrique décrit comment tooreview et mise à jour hello configuration pour vos instances de Cache Redis Azure et la configuration du serveur Redis couvre hello par défaut pour les instances de Cache Redis Azure.

> [!NOTE]
> Pour plus d’informations sur la configuration et l’utilisation des fonctionnalités de cache premium, consultez [la persistance de tooconfigure](cache-how-to-premium-persistence.md), [comment tooconfigure clustering](cache-how-to-premium-clustering.md), et [comment tooconfigure réseau virtuel prend en charge ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Configuration des paramètres de cache Redis
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Les paramètres de Cache Redis Azure sont affichés et configurés sur hello **Cache Redis** panneau à l’aide de hello **ressource Menu**.

![Paramètres de Cache Redis](./media/cache-configure/redis-cache-settings.png)

Vous pouvez afficher et configurer hello suivant les paramètres à l’aide de hello **ressource Menu**.

* [Vue d'ensemble](#overview)
* [Journal d’activité](#activity-log)
* [Contrôle d’accès (IAM)](#access-control-iam)
* [Balises](#tags)
* [Diagnostiquer et résoudre les problèmes](#diagnose-and-solve-problems)
* [Paramètres](#settings)
    * [Clés d’accès](#access-keys)
    * [Paramètres avancés](#advanced-settings)
    * [Redis Cache Advisor](#redis-cache-advisor)
    * [Mettre à l'échelle](#scale)
    * [Taille du cluster Redis](#cluster-size)
    * [Persistance des données Redis](#redis-data-persistence)
    * [Planification de mises à jour](#schedule-updates)
    * [Géoréplication](#geo-replication)
    * [Réseau virtuel](#virtual-network)
    * [Pare-feu](#firewall)
    * [Propriétés](#properties)
    * [Verrous](#locks)
    * [Script Automation](#automation-script)
* [Administration](#administration)
    * [Importer des données](#importexport)
    * [Exporter des données](#importexport)
    * [Reboot](#reboot)
* [Surveillance](#monitoring)
    * [Mesures Redis](#redis-metrics)
    * [Règles d'alerte](#alert-rules)
    * [Diagnostics](#diagnostics)
* [Paramètres de support et dépannage](#support-amp-troubleshooting-settings)
    * [Intégrité des ressources](#resource-health)
    * [Nouvelle demande de support](#new-support-request)


## <a name="overview"></a>Vue d'ensemble

La **Vue d’ensemble** fournit des informations de base sur votre cache, notamment le nom, les ports, le niveau tarifaire et des mesures de cache sélectionnées.

### <a name="activity-log"></a>Journal d’activité

Cliquez sur **le journal d’activité** tooview actions exécutées sur votre cache. Vous pouvez également utiliser tooexpand filtrage tooinclude de cette vue autres ressources. Pour en savoir plus sur l’utilisation des journaux d’audit, voir [Afficher les journaux d’activité pour auditer les actions sur les ressources](../azure-resource-manager/resource-group-audit.md). Pour plus d’informations sur la surveillance des événements du Cache Redis Azure, consultez [Opérations et alertes](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Contrôle d’accès (IAM)

Hello **(IAM) de contrôle d’accès** section prend en charge pour le contrôle d’accès basé sur un rôle (RBAC) dans les organisations hello toohelp portail Azure à de leurs exigences de gestion des accès purement et simplement. Pour plus d’informations, consultez [contrôle d’accès en fonction du rôle Bonjour portail Azure](../active-directory/role-based-access-control-configure.md).

### <a name="tags"></a>Tags

Hello **balises** section vous aide à organiser vos ressources. Pour plus d’informations, consultez [à l’aide des balises tooorganize vos ressources Azure](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Diagnostiquer et résoudre les problèmes

Cliquez sur **diagnostiquer et résoudre les problèmes** toobe fourni avec des problèmes courants et des stratégies pour les résoudre.



## <a name="settings"></a>Paramètres
Hello **paramètres** section vous permet de tooaccess et configurer hello suivant les paramètres de votre cache.

* [Clés d’accès](#access-keys)
* [Paramètres avancés](#advanced-settings)
* [Redis Cache Advisor](#redis-cache-advisor)
* [Mettre à l'échelle](#scale)
* [Taille du cluster Redis](#cluster-size)
* [Persistance des données Redis](#redis-data-persistence)
* [Planification de mises à jour](#schedule-updates)
* [Géoréplication](#geo-replication)
* [Réseau virtuel](#virtual-network)
* [Pare-feu](#firewall)
* [Propriétés](#properties)
* [Verrous](#locks)
* [Script Automation](#automation-script)



### <a name="access-keys"></a>Clés d’accès
Cliquez sur **clés d’accès** tooview ou régénérez l’accès hello clés pour votre cache. Ces clés sont utilisées par les clients hello tooyour cache de connexion.

![Clés d’accès de Cache Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Paramètres avancés
Hello paramètres suivants sont configurés sur hello **paramètres avancés** panneau.

* [Ports d’accès](#access-ports)
* [Stratégies de mémoire](#memory-policies)
* [Notifications de Keyspace (paramètres avancés)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>Ports d’accès
Par défaut, l’accès non SSL est désactivé pour les nouveaux caches. tooenable hello non-SSL du port, cliquez sur **non** pour **autoriser l’accès uniquement via SSL** sur hello **paramètres avancés** panneau, puis cliquez sur **enregistrer**.

![Ports d’accès de Cache Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Stratégies de mémoire
Hello **stratégie Maxmemory**, **réservés maxmemory**, et **réservés maxfragmentationmemory** paramètres hello **paramètresavancés**panneau configurer des stratégies de mémoire hello pour le cache de hello.

![Stratégie Maxmemory de Cache Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Stratégie MaxMemory** configure la stratégie d’éviction hello pour le cache de hello et vous permet de toochoose de hello suivant des stratégies d’éviction :

* `volatile-lru`-Il s’agit par défaut de hello.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Pour plus d’informations sur les stratégies `maxmemory`, voir [Stratégies d’éviction](http://redis.io/topics/lru-cache#eviction-policies).

Hello **réservés maxmemory** paramètre configure la quantité hello de mémoire en Mo est réservé pour les opérations telles que la réplication pendant le basculement non mises en cache. Ce paramètre vous permet de toohave un environnement de serveur Redis cohérent dans la varie en fonction de votre charge. Cette valeur doit être plus élevée pour les charges de travail comportant de nombreuses écritures. Lorsque la mémoire est réservée pour ces opérations, elle n’est pas disponible pour le stockage des données mises en cache.

Hello **maxfragmentationmemory réservés** paramètre configure la quantité hello de mémoire en Mo est tooaccommodate réservé pour la fragmentation de mémoire. Ce paramètre vous permet de toohave un environnement de serveur Redis cohérent lorsque hello cache est plein ou fermer les taux de fragmentation toofull et hello sont également élevée. Lorsque la mémoire est réservée pour ces opérations, elle n’est pas disponible pour le stockage des données mises en cache.

Une chose tooconsider lors du choix d’une nouvelle valeur de réserve de mémoire (**réservés maxmemory** ou **maxfragmentationmemory réservés**) est la manière dont cette modification peut affecter un cache qui est déjà en cours d’exécution avec grandes quantités de données. Par exemple, si vous avez un cache 53 Go 49 Go de données, puis modifiez hello réservation valeur too8 Go, cela supprimera hello maximale de mémoire disponible pour système hello too45 go. Si le paramètre actuel `used_memory` ou votre `used_memory_rss` valeurs sont supérieures à la nouvelle limite de hello de 45 Go, puis hello système n’aura tooevict données tant que les `used_memory` et `used_memory_rss` sont inférieure à 45 Go. La suppression de données peut augmenter la fragmentation de la charge et de la mémoire du serveur. Pour plus d’informations sur les métriques de cache, telles que `used_memory` et `used_memory_rss`, voir [Mesures disponibles et intervalles de création des rapports](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).

> [!IMPORTANT]
> Hello **réservés maxmemory** et **maxfragmentationmemory réservés** paramètres sont uniquement disponibles pour Standard et Premium met en cache.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Notifications de Keyspace (paramètres avancés)
Les notifications sont configurées sur hello espace de clés de redis **paramètres avancés** panneau. Notifications de l’espace de clés permettent aux clients de tooreceive notifications lorsque certains événements se produisent.

![Paramètres avancés de Cache Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Espace de clés des notifications et hello **événements espace de clés notifier** sont uniquement disponibles pour les caches Standard et Premium.
> 
> 

Pour plus d’informations, voir [Notifications de keyspace Redis](http://redis.io/topics/notifications). Pour un exemple de code, consultez hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) fichier Bonjour [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemple.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Redis Cache Advisor
Hello **Advisor de Cache Redis** panneau affiche les recommandations pour votre cache. Pendant les opérations normales, aucune recommandation n’est affichée. 

![Recommandations](./media/cache-configure/redis-cache-no-recommendations.png)

Si toutes les conditions se produisent lors des opérations de hello de votre cache, telles que l’utilisation de mémoire haute, la bande passante du réseau ou de charge du serveur, une alerte s’affiche sur hello **Cache Redis** panneau.

![Recommandations](./media/cache-configure/redis-cache-recommendations-alert.png)

Vous trouverez plus d’informations sur hello **recommandations** panneau.

![Recommandations](./media/cache-configure/redis-cache-recommendations.png)

Vous pouvez surveiller ces métriques sur hello [graphiques de surveillance](cache-how-to-monitor.md#monitoring-charts) et [graphiques d’utilisation](cache-how-to-monitor.md#usage-charts) sections Hello **Cache Redis** panneau.

Chaque niveau tarifaire est associé à des limites spécifiques concernant les connexions clientes, la mémoire et la bande passante. Si votre cache est proche de la capacité maximale pour ces mesures pendant une période prolongée, une recommandation est créée. Pour plus d’informations sur les métriques hello et limites révisées par hello **recommandations** outil, consultez hello tableau suivant :

| Mesure du Cache Redis | Plus d’informations |
| --- | --- |
| Utilisation de la bande passante réseau |[Performances du cache - Bande passante disponible](cache-faq.md#cache-performance) |
| Clients connectés |[Configuration du serveur Redis par défaut - maxclients](#maxclients) |
| Charge du serveur |[Graphiques d’utilisation - Charge du serveur Redis](cache-how-to-monitor.md#usage-charts) |
| Utilisation de la mémoire |[Performance du cache - Taille](cache-faq.md#cache-performance) |

tooupgrade votre cache, cliquez sur **mettre à niveau maintenant** hello toochange niveau tarifaire et [échelle](#scale) votre cache. Pour plus d’informations sur le choix d’un niveau tarifaire, voir la section [Que propose Cache Redis et quelle taille dois-je utiliser ?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Mettre à l'échelle
Cliquez sur **échelle** hello tooview ou modification de niveau tarifaire pour votre cache. Pour plus d’informations sur la mise à l’échelle, consultez [comment tooScale Cache Redis Azure](cache-how-to-scale.md).

![Niveau de tarification de Cache Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Taille du cluster Redis
Cliquez sur **taille du Cluster Redis (version préliminaire)** avec activation des clusters de cache de taille de cluster toochange hello pour une prime en cours d’exécution.

> [!NOTE]
> Notez que lorsque hello Azure Redis Cache Premium couche a été publié tooGeneral disponibilité, la fonctionnalité de taille de Cluster Redis hello est actuellement en version préliminaire.
> 
> 

![Taille du cluster Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

taille de cluster toochange hello, utilisez hello curseur ou tapez un nombre compris entre 1 et 10 dans hello **nombre de partitions** zone de texte et cliquez sur **OK** toosave.

> [!IMPORTANT]
> Le clustering Redis est disponible uniquement pour les caches de niveau Premium. Pour plus d’informations, consultez [comment tooconfigure clustering Premium Azure Redis cache](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Persistance des données Redis
Cliquez sur **Redis la persistance des données** tooenable, désactiver ou configurer la persistance des données pour votre cache premium. Cache Redis Azure offre la persistance Redis grâce à la [persistance RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) et à la [persistance AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).

Pour plus d’informations, consultez [la persistance tooconfigure cache Redis Azure Premium](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> La persistance des données Redis est disponible uniquement pour les caches de niveau Premium. 
> 
> 

### <a name="schedule-updates"></a>Planifier les mises à jour
Hello **planifier les mises à jour** panneau vous permet de toodesignate une fenêtre de maintenance des mises à jour du serveur Redis pour votre cache. 

> [!IMPORTANT]
> fenêtre de maintenance Hello s’applique uniquement les mises à jour du serveur tooRedis et pas tooany Azure met à jour ou mises à jour du système d’exploitation de toohello de machines virtuelles hello qui hébergent le cache de hello.
> 
> 

![Planifier les mises à jour](./media/cache-configure/redis-schedule-updates.png)

toospecify une fenêtre de maintenance, vérifiez les jours hello souhaité et spécifier l’heure de début de fenêtre de maintenance hello pour chaque jour, puis cliquez sur **OK**. Notez que l’heure de la fenêtre maintenance hello est au format UTC. 

> [!IMPORTANT]
> Hello **planifier les mises à jour** fonctionnalité est disponible uniquement pour les caches de niveau Premium. Pour plus d’informations et pour obtenir des instructions, consultez la page [Administration du cache Redis Azure - Planification de mises à jour](cache-administration.md#schedule-updates).
> 
> 

### <a name="geo-replication"></a>Géoréplication

Hello **géo-réplication** panneau fournit un mécanisme permettant de lier les deux instances de Cache Redis Azure de niveau Premium. Un cache est désigné comme le cache de lié principal hello et hello autre en tant que cache de lié secondaire hello. cache lié de Hello secondaire devient en lecture seule, et les données toohello écrit le cache principal est répliquée toohello cache lié secondaire. Cette fonctionnalité peut être utilisé tooreplicate un cache entre les régions Azure.

> [!IMPORTANT]
> La **Géoréplication** est uniquement disponible pour les caches de niveau Premium. Pour plus d’informations et pour obtenir des instructions, consultez [comment tooconfigure géo-réplication Azure Redis cache](cache-how-to-geo-replication.md).
> 
> 

### <a name="virtual-network"></a>Réseau virtuel
Hello **réseau virtuel** section vous permet de paramètres de réseau virtuel tooconfigure hello pour votre cache. Pour plus d’informations sur la création d’un cache premium avec le réseau virtuel prend en charge et la mise à jour ses paramètres, consultez [comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> Les paramètres de réseau virtuel sont disponibles uniquement pour les caches Premium qui ont été configurés avec la prise en charge de réseau virtuel lors de la création du cache. 
> 
> 

### <a name="firewall"></a>Pare-feu

Cliquez sur **pare-feu** tooview et configurer des règles de pare-feu pour votre Premium le Cache Redis Azure.

![Pare-feu](./media/cache-configure/redis-firewall-rules.png)

Vous pouvez spécifier des règles de pare-feu avec une des valeurs de début et de fin de plage d’adresses IP. Lorsque les règles de pare-feu sont configurés, uniquement les connexions client à partir de hello spécifié de plages d’adresses IP peuvent se connecter toohello cache. Lorsqu’une règle de pare-feu est enregistrée est un bref délai avant de la règle de hello est effective. Ce délai est généralement inférieur à une minute.

> [!IMPORTANT]
> Les connexions depuis les systèmes de surveillance de cache Redis Azure sont toujours autorisées, même si des règles de pare-feu sont configurées.
> 
> Les règles de pare-feu son uniquement disponibles pour les caches de niveau Premium.
> 
> 

### <a name="properties"></a>Propriétés
Cliquez sur **propriétés** tooview plus d’informations sur le cache, y compris le point de terminaison de cache hello et ports.

![Propriétés de Cache Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Verrous
Hello **verrouille** section vous permet de toolock un abonnement, groupe de ressources ou ressource tooprevent autres utilisateurs de votre organisation d’accidentellement supprimer ou modifier des ressources critiques. Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

### <a name="automation-script"></a>Script Automation

Cliquez sur **script d’automatisation** toobuild et exporter un modèle de vos ressources déployées pour les déploiements futurs. Pour plus d’informations sur le fonctionnement des modèles, consultez [Déployer des ressources à l’aide de modèles Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Paramètres d’administration
Hello paramètres Bonjour **Administration** section permettent de hello tooperform suivant des tâches d’administration pour votre cache. 

![Administration](./media/cache-configure/redis-cache-administration.png)

* [Importer des données](#importexport)
* [Exporter des données](#importexport)
* [Reboot](#reboot)


### <a name="importexport"></a>Importation/Exportation
Importation/exportation est une opération de gestion de données de Cache Redis Azure, qui vous permet de tooimport et exporter des données dans le cache de hello par importation et exportation d’un instantané de base de données de Cache Redis (RDB) à partir de premium cache tooa objet blob de pages dans un compte de stockage Azure. Importation/exportation vous permet de toomigrate entre différentes instances de Cache Redis Azure ou remplir le cache de hello avec les données avant des utiliser.

Importation peut être des fichiers compatibles RDB toobring utilisé Redis à partir de n’importe quel serveur Redis en cours d’exécution dans n’importe quel cloud ou l’environnement, y compris Redis en cours d’exécution sur Linux, Windows ou n’importe quel fournisseur de cloud comme Amazon Web Services et d’autres. L’importation de données est un toocreate facilement un cache de données prédéfinis. Au cours du processus d’importation hello, le Cache Redis Azure charge les fichiers RDB hello depuis le stockage Azure en mémoire et les insère les clés hello dans le cache de hello.

Exportation vous permet des données de salutation tooexport stockées dans les fichiers de Cache Redis Azure tooRedis compatibles RDB. Vous pouvez utiliser ces données toomove de fonctionnalité à partir d’un Cache Redis Azure instance tooanother ou tooanother Redis server. Au cours du processus d’exportation hello, un fichier temporaire est créé sur hello VM que hôtes hello l’instance de serveur de Cache Redis Azure et hello fichier téléchargé toohello désigné du compte de stockage. Lors de l’opération d’exportation hello se termine avec l’état de réussite ou l’échec, le fichier temporaire de hello est supprimé.

> [!IMPORTANT]
> L’importation/exportation est uniquement disponible pour les caches de niveau Premium. Pour plus d’informations et pour obtenir des instructions, consultez la rubrique [Importer et exporter des données dans le cache Redis Azure](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Reboot
Hello **redémarrer** panneau vous permet de nœuds de hello tooreboot de votre cache. Cette fonctionnalité de redémarrage permet de vous tootest votre application pour assurer la résilience en cas de panne d’un nœud de cache.

![Reboot](./media/cache-configure/redis-cache-reboot.png)

Si vous avez un cache premium avec activation des clusters, vous pouvez sélectionner les partitions de hello cache tooreboot.

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot un ou plusieurs nœuds de votre cache, sélectionnez les nœuds de hello souhaité et cliquez sur **redémarrer**. Si vous avez un cache premium avec activation des clusters, sélectionnez hello partitions tooreboot puis **redémarrer**. Après quelques minutes, hello redémarrage d’un ou plusieurs nœuds sélectionnés et sont en ligne quelques minutes plus tard.

> [!IMPORTANT]
> Le redémarrage est désormais disponible pour tous les niveaux de tarification. Pour plus d’informations et pour obtenir des instructions, consultez la page [Administration du cache Redis Azure - Redémarrage](cache-administration.md#reboot).
> 
> 


## <a name="monitoring"></a>Surveillance

Hello **analyse** section vous permet de tooconfigure diagnostics et analyse pour votre Cache Redis. Pour plus d’informations sur la surveillance de Cache Redis Azure et de diagnostics, consultez [comment toomonitor Cache Redis Azure](cache-how-to-monitor.md).

![Diagnostics](./media/cache-configure/redis-cache-diagnostics.png)

* [Mesures Redis](#redis-metrics)
* [Règles d'alerte](#alert-rules)
* [Diagnostics](#diagnostics)

### <a name="redis-metrics"></a>Mesures Redis
Cliquez sur **Redis métriques** trop[afficher les métriques](cache-how-to-monitor.md#view-cache-metrics) pour votre cache.

### <a name="alert-rules"></a>Règles d'alerte

Cliquez sur **règles d’alerte** tooconfigure alertes en fonction des métriques de Cache Redis. Pour plus d'informations, consultez [Alertes](cache-how-to-monitor.md#alerts).

### <a name="diagnostics"></a>Diagnostics

Par défaut, les mesures de cache dans Azure Monitor sont [stockées pendant 30 jours](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive), puis supprimées. Cliquez sur les métriques de votre cache pendant plus de 30 jours, toopersist **Diagnostics** trop[configurer le compte de stockage hello](cache-how-to-monitor.md#export-cache-metrics) utilisé toostore les diagnostics de cache.

>[!NOTE]
>En outre tooarchiving votre toostorage de métriques de cache, vous pouvez également [les diffuser un concentrateur d’événements tooan ou les envoyer tooLog Analytique](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Paramètres de support et dépannage
Hello paramètres Bonjour **prise en charge + dépannage** section vous fournir des options pour la résolution des problèmes avec votre cache.

![prise en charge et à la résolution des problèmes](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Intégrité des ressources](#resource-health)
* [Nouvelle demande de support](#new-support-request)

### <a name="resource-health"></a>Intégrité des ressources
**Resource Health** surveille vos ressources et vous indique si elles s’exécutent comme prévu. Pour plus d’informations sur hello service d’intégrité de ressource Azure, consultez [vue d’ensemble du contrôle d’intégrité Azure Resource](../resource-health/resource-health-overview.md).

> [!NOTE]
> L’intégrité des ressources est actuellement incapable de tooreport intégrité hello d’instances de Cache Redis Azure hébergée dans un réseau virtuel. Pour plus d’informations, voir [Toutes les fonctionnalités fonctionnent-elles lorsque vous hébergez un cache dans un réseau virtuel ?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>Nouvelle demande de support
Cliquez sur **nouveau prend en charge la demande** tooopen une demande de support pour votre cache.





## <a name="default-redis-server-configuration"></a>Configuration du serveur Redis par défaut
Nouveau Cache Redis Azure sont configurées avec hello suivant de valeurs de configuration par défaut Redis.

> [!NOTE]
> paramètres Hello dans cette section ne peut pas être modifiés à l’aide de hello `StackExchange.Redis.IServer.ConfigSet` (méthode). Si cette méthode est appelée avec une des commandes hello dans cette section, une suivant toohello similaire d’exception est levée :  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> Toutes les valeurs qui sont configurables, telles que **max-mémoire-policy**, sont configurables via hello portail Azure ou des outils de gestion de ligne de commande tel que Azure CLI ou PowerShell.
> 
> 

| Paramètre | Valeur par défaut | Description |
| --- | --- | --- |
| `databases` |16 |nombre de bases de données par défaut de Hello est 16, mais vous pouvez configurer un autre hello selon numéro niveau tarifaire. <sup>1</sup> hello par défaut est DB 0, vous pouvez sélectionner une autre sur une base de chaque connexion à l’aide de `connection.GetDatabase(dbid)` où `dbid` est un nombre compris entre `0` et `databases - 1`. |
| `maxclients` |Varie selon le niveau tarifaire de hello<sup>2</sup> |Il s’agit hello le nombre maximal de clients connectés autorisé à hello même temps. Hello limite atteinte Redis ferme toutes les connexions de la nouvelle hello, une erreur « nombre maximal de clients atteint ». |
| `maxmemory-policy` |`volatile-lru` |Stratégie MaxMemory est un paramètre de hello pour comment Redis sélectionne le tooremove lorsque `maxmemory` (hello la taille du cache hello offre vous avez sélectionné lors de la création du cache de hello) est atteinte. Valeur par défaut de Cache Redis Azure hello paramètre est `volatile-lru`, qui supprime les clés hello avec un délai d’expiration défini à l’aide d’un algorithme LRU. Ce paramètre peut être configuré dans hello portail Azure. Pour plus d’informations, voir [Stratégies de mémoire](#memory-policies). |
| `maxmemory-samples` |3 |toosave mémoire, LRU et les algorithmes de durée de vie minimale sont des algorithmes approximatives au lieu d’algorithmes précis. Par défaut, Redis vérifie trois clés et récupère hello un moins récemment utilisé. |
| `lua-time-limit` |5 000 |Temps d’exécution maximal d’un script Lua en millisecondes. Si la durée d’exécution maximale de hello est atteinte, Redis consigne qu’un script est toujours en exécution après hello maximale autorisée de temps et démarre tooreply tooqueries avec une erreur. |
| `lua-event-limit` |500 |Taille maximale de la file d’attente des événements de script. |
| `client-output-buffer-limit``normalclient-output-buffer-limit``pubsub` |0 0 032mb 8mb 60 |Hello limites de mémoire tampon de sortie de client peuvent être utilisé tooforce une déconnexion des clients qui ne lisent pas les données à partir du serveur hello suffisamment rapide pour une raison quelconque (une raison courante est qu’un client Pub/Sub ne peuvent pas consommer les messages aussi rapidement qu’hello éditeur les produit). Pour plus d’informations, consultez [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup>limite hello pour `databases` est différent pour chaque Cache Azure Redis au niveau de tarification et peut être définie lors de la création du cache. Si aucun `databases` paramètre est spécifié lors de la création du cache, par défaut de hello est 16.

* Caches De base et Standard
  * C0 (250 Mo) de cache - des bases de données too16
  * C1 cache de (1 Go) - les bases de données too16
  * C2 cache de (2,5 Go) - les bases de données too16
  * C3 (6 Go) cache - les bases de données too16
  * C4 cache de (13 Go) - les bases de données too32
  * C5 (26 Go) de cache - les bases de données too48
  * C6 (53 Go) de cache - les bases de données too64
* Caches Premium
  * P1 (6 Go - 60 Go) - les bases de données too16
  * P2 (13 à 130 Go) - les bases de données too32
  * P3 (26 à 260 Go) - les bases de données too48
  * P4 (53 à 530 Go) - les bases de données too64
  * Tous les caches de niveau premium avec le cluster Redis activé - Redis cluster prend uniquement en charge l’utilisation de la base de données 0 hello donc `databases` limiter pour n’importe quel cache premium avec le cluster Redis activé est effectivement 1 et hello [sélectionnez](http://redis.io/commands/select) commande n’est pas autorisée. Pour plus d’informations, consultez [dois-je toomake tout toouse d’application de modifications toomy client clustering ?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

Pour plus d’informations sur les bases de données, consultez [Quelles sont les bases de données Redis ?](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> Hello `databases` paramètre peut être configuré uniquement pendant la création du cache et uniquement à l’aide de PowerShell, CLI ou autres clients de gestion. Pour obtenir un exemple de configuration de `databases` lors de la création du cache à l’aide de PowerShell, voir [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a>
<sup>2</sup>`maxclients` est différent pour chaque niveau tarifaire du cache Redis Azure.

* Caches De base et Standard
  * C0 cache de (250 Mo) - les connexions de too256
  * C1 cache de (1 Go) - des too1, 000 connexions
  * C2 (2,5 Go) cache - des too2, 000 connexions
  * C3 (6 Go) cache - des too5, 000 connexions
  * C4 (13 Go) cache - des too10, 000 connexions
  * C5 (26 Go) cache - des too15, 000 connexions
  * C6 (53 Go) cache - des too20, 000 connexions
* Caches Premium
  * P1 (6 Go - 60 Go) - des too7, 500 connexions
  * P2 (13 à 130 Go) - des too15, 000 connexions
  * P3 (26 à 260 Go) - des too30, 000 connexions
  * P4 (53 à 530 Go) - des too40, 000 connexions

> [!NOTE]
> Tandis que chaque taille de cache permet aux *jusqu'à* un certain nombre de connexions, chaque tooRedis connexion surcharge associée. Un exemple d’une telle surcharge est l’utilisation du processeur et de la mémoire à la suite d’un chiffrement TLS/SSL. limite du nombre maximal de connexions Hello pour une taille de cache donné suppose un cache peu chargé. Si charger à partir de la charge de la connexion *plus* charge à partir d’opérations du client dépasse la capacité pour le système de hello, le cache de hello peut rencontrer des problèmes de capacité même si vous ne dépassez pas la limite de connexions hello pour hello taille actuelle du cache.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Commandes Redis non prises en charge dans le Cache Redis Azure
> [!IMPORTANT]
> Étant donné que la configuration et la gestion des instances de Cache Redis Azure est géré par Microsoft, hello commandes suivantes sont désactivées. Si vous essayez de tooinvoke les, vous recevez un message d’erreur similaire trop`"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIG
> * DEBUG
> * MIGRATE
> * Enregistrer
> * SHUTDOWN
> * SLAVEOF
> * CLUSTER : les commandes d’écriture du cluster sont désactivées, mais celles de lecture seule sont autorisées.
> 
> 

Pour plus d’informations sur les commandes Redis, consultez [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Console Redis
Vous pouvez exécuter en toute sécurité des commandes tooyour instances de Cache Redis Azure à l’aide de hello **Redis de Console**, qui est disponible dans le portail Azure pour tous les niveaux de cache de hello.

> [!IMPORTANT]
> - Hello Redis Console ne fonctionne pas avec [réseau virtuel](cache-how-to-premium-vnet.md). Lorsque votre cache fait partie d’un réseau virtuel, uniquement les clients Bonjour réseau virtuel peuvent accéder les cache hello. Console de Redis s’exécutant dans votre navigateur, qui est en dehors de hello réseau virtuel, il ne peut pas se connecter tooyour cache.
> - Les commandes Redis ne sont pas toutes prises en charge dans le Cache Redis Azure. Pour obtenir la liste des commandes de Redis sont désactivées pour le Cache Redis Azure, consultez hello précédente [Redis commandes non prises en charge dans le Cache Redis Azure](#redis-commands-not-supported-in-azure-redis-cache) section. Pour plus d’informations sur les commandes Redis, consultez [http://redis.io/commands](http://redis.io/commands).
> 
> 

tooaccess hello Console Redis, cliquez sur **Console** de hello **Cache Redis** panneau.

![Console Redis](./media/cache-configure/redis-console-menu.png)

commandes de tooissue sur votre instance de cache, hello de type simplement souhaité commande dans la console de hello.

![Console Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>À l’aide de hello Redis de Console avec une prime en cluster du cache

Lorsque le cache à l’aide de hello Redis de Console avec une prime de cluster, vous pouvez émettre des commandes tooa même partition du cache de hello. tooissue une partition spécifique tooa de commande, connectez-vous d’abord toohello partition de votre choix en cliquant dessus dans le sélecteur de partitions hello.

![Console Redis](./media/cache-configure/redis-console-premium-cluster.png)

Si vous essayez de tooaccess une clé qui est stockée dans une autre partition que hello partition connectée, vous recevez une erreur message similaire toohello message suivant.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

Dans l’exemple précédent de hello, partition 1 est la partition sélectionnée de hello, mais `myKey` se trouve dans la partition 0, comme indiqué par hello `(shard 0)` partie du message d’erreur hello. Dans cet exemple, tooaccess `myKey`, sélectionnez à l’aide de la partition 0 hello sélecteur de partition, puis commande hello souhaité de problème.


## <a name="move-your-cache-tooa-new-subscription"></a>Déplacez votre cache tooa un nouvel abonnement
Vous pouvez déplacer votre cache tooa un nouvel abonnement en cliquant sur **déplacer**.

![Déplacer le Cache Redis](./media/cache-configure/redis-cache-move.png)

Pour plus d’informations sur le déplacement de ressources à partir d’une ressource groupe tooanother et à partir d’un seul abonnement tooanother, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur l’utilisation des commandes Redis, voir [Exécution des commandes Redis](cache-faq.md#how-can-i-run-redis-commands).

