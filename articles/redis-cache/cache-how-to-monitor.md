---
title: aaaHow toomonitor Cache Redis Azure | Documents Microsoft
description: "Découvrez comment toomonitor hello intégrité et les performances vos instances de Cache Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 7e70b153-9c87-4290-85af-2228f31df118
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: c474d485dfcbb109d5bb634a980f6db080598e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-azure-redis-cache"></a>Comment toomonitor Cache Redis Azure
Cache Redis Azure utilise [moniteur Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) tooprovide plusieurs options pour l’analyse vos instances de cache. Vous pouvez afficher les métriques, épingler des graphiques de métriques toohello tableau d’accueil, personnaliser la plage de date et d’heure hello des graphiques de surveillance, ajouter et supprimer des métriques à partir de graphiques de hello et définir des alertes lorsque certaines conditions sont remplies. Ces outils permettent de vous toomonitor hello d’intégrité de vos instances de Cache Redis Azure et vous aider à gérer vos applications de mise en cache.

Métriques pour les instances de Cache Redis Azure sont collectées à l’aide de hello Redis [INFO](http://redis.io/commands/info) commande environ deux fois par minute et automatiquement stockées pendant 30 jours (consultez [exporter les métriques de cache](#export-cache-metrics) tooconfigure un stratégie de rétention différente) afin de pouvoir être affichés dans les graphiques de métriques hello et évaluées par les règles d’alerte. Pour plus d’informations sur les valeurs hello différentes informations utilisées pour chaque métrique du cache, consultez [métriques disponibles et les périodes de rapport](#available-metrics-and-reporting-intervals).

<a name="view-cache-metrics"></a>

métriques de cache tooview, [Parcourir](cache-configure.md#configure-redis-cache-settings) tooyour instance de cache Bonjour [portail Azure](https://portal.azure.com).  Cache Redis Azure fournit certains graphiques intégrés sur hello **vue d’ensemble** lame et hello **Redis métriques** panneau. Chaque graphique peut être personnalisé en ajoutant ou supprimant des métriques et la modification hello intervalle de rapports.

![Mesures Redis](./media/cache-how-to-monitor/redis-cache-redis-metrics-blade.png)

## <a name="view-pre-configured-metrics-charts"></a>Afficher des graphiques de mesures préconfigurés

Hello **vue d’ensemble** panneau a hello suivant préconfigurés graphiques de surveillance.

* [Graphiques de surveillance](#monitoring-charts)
* [Graphiques d’utilisation](#usage-charts)

### <a name="monitoring-charts"></a>Graphiques de surveillance
Hello **analyse** section Bonjour **vue d’ensemble** panneau a **correspondances et absences**, **Obtient et définit**, **connexions**, et **nombre Total de commandes** graphiques.

![Graphiques de surveillance](./media/cache-how-to-monitor/redis-cache-monitoring-part.png)

### <a name="usage-charts"></a>Graphiques d’utilisation
Hello **utilisation** section Bonjour **vue d’ensemble** panneau a **charge du serveur Redis**, **utilisation de la mémoire**, **bande passante réseau** , et **l’utilisation du processeur** graphiques et affiche également hello **niveau tarifaire** pour l’instance de cache hello.

![Graphiques d’utilisation](./media/cache-how-to-monitor/redis-cache-usage-part.png)

Hello **niveau tarifaire** tarification du cache affiche hello niveau et peut être utilisé trop[échelle](cache-how-to-scale.md) hello tooa de cache autre niveau tarifaire.

## <a name="view-metrics-with-azure-monitor"></a>Afficher les mesures avec Azure Monitor
tooview Redis des métriques et créer des graphiques personnalisés à l’aide du moniteur de Windows Azure, cliquez sur **métriques** de hello **menu ressource**et personnaliser votre graphique à l’aide des métriques de hello souhaité, l’intervalle, le type de graphique, de rapports et plus.

![Mesures Redis](./media/cache-how-to-monitor/redis-cache-monitor.png)

Pour plus d’informations sur l’utilisation des mesures à l’aide d’Azure Monitor, consultez [Vue d’ensemble des mesures dans Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

<a name="how-to-view-metrics-and-customize-chart"></a>
<a name="enable-cache-diagnostics"></a>
## <a name="export-cache-metrics"></a>Exporter les mesures de cache
Par défaut, les mesures de cache dans Azure Monitor sont [stockées pendant 30 jours](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive), puis supprimées. toopersist vos métriques de cache pendant plus de 30 jours, vous pouvez [désignez un compte de stockage](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md) et spécifiez un **rétention (jours)** stratégie pour vos métriques de cache. 

tooconfigure un compte de stockage pour vos métriques de cache :

1. Cliquez sur **Diagnostics** de hello **menu ressource** Bonjour **Cache Redis** panneau.
2. Cliquez **Sur**.
3. Vérifiez **archiver le compte de stockage tooa**.
4. Sélectionnez le compte de stockage hello dans les métriques de cache toostore hello.
5. Vérifiez hello **1 minute** case à cocher et spécifiez un **rétention (jours)** stratégie. Si vous inutile tooapply toute stratégie de rétention et conserver les données indéfiniment, définissez **rétention (jours)** trop**0**.
6. Cliquez sur **Enregistrer**.

![Diagnostics Redis](./media/cache-how-to-monitor/redis-cache-diagnostics.png)

>[!NOTE]
>En outre tooarchiving votre toostorage de métriques de cache, vous pouvez également [les diffuser un concentrateur d’événements tooan ou les envoyer tooLog Analytique](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

tooaccess vos métriques, vous pouvez les visualiser dans hello portail Azure, comme décrit précédemment dans cet article, et vous pouvez également y accéder à l’aide de hello [API REST de Azure moniteur métriques](../monitoring-and-diagnostics/monitoring-overview-metrics.md#access-metrics-via-the-rest-api).

> [!NOTE]
> Si vous modifiez des comptes de stockage, données hello dans le compte de stockage hello configuré précédemment restent disponibles en téléchargement, mais il n’est pas affiché dans hello portail Azure.  
> 
> 

## <a name="available-metrics-and-reporting-intervals"></a>Mesures disponibles et intervalles de création des rapports
Les mesures de cache font l’objet de rapports à différents intervalles : **Dernière heure**, **Aujourd’hui**, **Semaine dernière** et **Personnalisé**. Hello **métrique** panneau pour chaque graphique des métriques affiche les valeurs moyenne, minimale et maximale de hello pour chaque mesure dans le graphique de hello, et certaines métriques indiquent un total pour hello intervalle de rapports. 

Chaque mesure inclut deux versions. Métrique d’une mesure de performances pour l’intégralité du cache hello et pour les caches qui utilisent [clustering](cache-how-to-premium-clustering.md), une deuxième version de métrique hello incluant `(Shard 0-9)` nom hello mesures des performances pour une partition unique dans un cache. Par exemple, si un cache comporte 4 partitions, `Cache Hits` hello la quantité totale d’accès pour l’intégralité du cache hello, et `Cache Hits (Shard 3)` est simplement les correspondances hello pour cette partition du cache de hello.

> [!NOTE]
> Même lorsque le cache de hello est inactif sans applications clientes actives connectées, vous pouvez constater une activité du cache, telles que les opérations en cours d’exécution, l’utilisation de mémoire et les clients connectés. Cette activité est normale pendant l’opération hello d’une instance de Cache Redis Azure.
> 
> 

| Mesure | Description |
| --- | --- |
| Présences dans le cache |nombre de Hello de clé trouvées pendant la période de rapport spécifiée hello. Cette opération mappe trop`keyspace_hits` de hello Redis [INFO](http://redis.io/commands/info) commande. |
| Absences dans le cache |nombre de Hello de recherches de clés ayant échouées au cours de la période de rapport spécifiée hello. Cette opération mappe trop`keyspace_misses` à partir de la commande Redis les informations de hello. Absences dans le cache ne signifient pas nécessairement qu'un problème avec le cache de hello. Par exemple, lorsque vous utilisez le modèle de programmation de type cache-aside de hello, une application commence dans le cache de hello pour un élément. Si hello élément ne fait pas (absence dans le cache), élément de hello est récupérée à partir de la base de données hello et ajouté des toohello cache pour la prochaine fois. Absences dans le cache sont un comportement normal pour le modèle de programmation de type cache-aside de hello. Si le nombre de hello d’absences dans le cache est plus élevée que prévu, examinez la logique de l’application hello qui remplit et lit à partir du cache de hello. Si les éléments sont supprimés du cache hello en raison d’une sollicitation de la toomemory alors qu’il peut y avoir des absences dans le cache, mais un meilleur toomonitor métrique pour la sollicitation de la mémoire serait `Used Memory` ou `Evicted Keys`. |
| Clients connectés |nombre de Hello du cache de toohello des connexions client au cours de la période de rapport spécifiée hello. Cette opération mappe trop`connected_clients` à partir de la commande Redis les informations de hello. Une fois hello [limite de connexion](cache-configure.md#default-redis-server-configuration) est atteinte des tentatives de connexion ultérieures toohello cache échouera. Notez que même s’il n’existe aucune application client actif, il peut encore être quelques instances de clients connectés en raison de connexions et les processus toointernal. |
| Clés exclues |période de rapport spécifiée Hello nombre d’éléments supprimés du cache de hello pendant hello échéance toohello `maxmemory` limite. Cette opération mappe trop`evicted_keys` à partir de la commande Redis les informations de hello. |
| Clés expirées |nombre Hello d’éléments arrivés à expiration dans le cache de hello pendant la période de rapport spécifiée hello. Cette valeur correspond trop`expired_keys` à partir de la commande Redis les informations de hello. |
| Nombre total de clés  | nombre maximal de Hello de clés dans le cache de hello pendant hello au-delà de la période de création de rapports. Cette opération mappe trop`keyspace` à partir de la commande Redis les informations de hello. En raison de la limitation tooa Hello sous-jacent du système de mesures, des caches avec clustering activé, nombre Total de clés retourne le nombre maximal de hello de clés de partition hello de nombre maximal de hello de clés lors hello intervalle de rapports.  |
| Gets |nombre de Hello d’opérations get à partir du cache de hello pendant la période de rapport spécifiée hello. Cette valeur est la somme de hello suivants de hello valeurs hello Redis des informations à partir de toutes les commandes : `cmdstat_get`, `cmdstat_hget`, `cmdstat_hgetall`, `cmdstat_hmget`, `cmdstat_mget`, `cmdstat_getbit`, et `cmdstat_getrange`, et est somme toohello équivalent d’accès au cache et échecs au cours de hello intervalle de rapports. |
| Charge du serveur Redis |pourcentage de Hello de cycles qui Bonjour serveur Redis est occupé par le traitement et ne pas attendre inactive pour les messages. Si ce compteur atteint 100, cela signifie que le serveur Redis de hello a atteint un plafond de performances et de hello du processeur ne peut pas traiter de travail les plus rapidement. Si vous voyez la charge du serveur Redis haute vous verrez des exceptions de délai d’attente dans le client de hello. Dans ce cas, vous devez envisager d’effectuer une mise à l’échelle ou bien de partitionner vos données sur plusieurs caches. |
| Sets |nombre de Hello du cache de toohello opérations ensemble pendant hello spécifié période de rapport. Cette valeur est la somme de hello suivants de hello valeurs hello Redis des informations à partir de toutes les commandes : `cmdstat_set`, `cmdstat_hset`, `cmdstat_hmset`, `cmdstat_hsetnx`, `cmdstat_lset`, `cmdstat_mset`, `cmdstat_msetnx`, `cmdstat_setbit`, `cmdstat_setex`, `cmdstat_setrange` , et `cmdstat_setnx`. |
| Total des opérations |Nombre total de Hello de commandes traitées par le serveur de cache hello pendant hello spécifié période de rapport. Cette valeur correspond trop`total_commands_processed` à partir de la commande Redis les informations de hello. Notez que lorsque le Cache Redis Azure est uniquement utilisé pour pub/sub il n’y a aucune mesure pour `Cache Hits`, `Cache Misses`, `Gets`, ou `Sets`, mais il y aura `Total Operations` métriques qui reflètent l’utilisation du cache de hello pour les opérations de pub/sub. |
| Mémoire utilisée |quantité de Hello de mémoire cache utilisée pour les paires clé/valeur dans le cache de hello en Mo pendant hello spécifiée période de rapport. Cette valeur correspond trop`used_memory` à partir de la commande Redis les informations de hello. Elle n’inclut pas les métadonnées ou la fragmentation. |
| Taille de la mémoire résidente utilisée |quantité Hello de mémoire cache utilisée en Mo pendant hello période de rapport spécifiée, y compris la fragmentation et métadonnées. Cette valeur correspond trop`used_memory_rss` à partir de la commande Redis les informations de hello. |
| UC |Hello l’utilisation du processeur du serveur de Cache Redis Azure hello sous forme de pourcentage au cours de hello spécifié période de rapport. Cette valeur correspond à système d’exploitation de toohello `\Processor(_Total)\% Processor Time` compteur de performances. |
| Lecture du cache |quantité de Hello des données lues à partir du cache hello mégaoctets par seconde (Mbits/s) pendant hello spécifiée période de rapport. Cette valeur est dérivée de cartes d’interface réseau hello qui prennent en charge de la machine virtuelle de hello qui héberge le cache de hello et n’est ne pas Redis spécifique. **Cette valeur correspond à la bande passante du réseau toohello utilisée par ce cache. Si vous souhaitez tooset des alertes pour les limites de la bande passante du réseau côté serveur, puis créez à l’aide de ce `Cache Read` compteur. Consultez [cette table](cache-faq.md#cache-performance) pour hello observé les limites de bande passante pour le cache de différentes tailles et les niveaux de tarification.** |
| Cache d’écriture |Bonjour la quantité de données écrites toohello cache en mégaoctets par seconde (Mo/s) pendant la période de rapport spécifiée hello. Cette valeur est dérivée de cartes d’interface réseau hello qui prennent en charge de la machine virtuelle de hello qui héberge le cache de hello et n’est ne pas Redis spécifique. Cette valeur correspond à la bande passante du réseau toohello des données envoyées toohello cache à partir du client de hello. |

<a name="operations-and-alerts"></a>
## <a name="alerts"></a>Alertes
Vous pouvez configurer des alertes tooreceive basés sur les journaux d’activité et de métriques. Moniteur de Azure vous permet de tooconfigure un hello toodo alerte suivant lorsqu’il déclenche :

* Envoyer un e-mail de notification
* Appeler un webhook
* Appeler une application logique Azure

règles d’alerte tooconfigure pour votre cache, cliquez sur **règles d’alerte** de hello **menu ressource**.

![Surveillance](./media/cache-how-to-monitor/redis-cache-monitoring.png)

Pour plus d’informations sur la configuration et l’utilisation des Alertes, consultez [Vue d’ensemble des Alertes](../monitoring-and-diagnostics/insights-alerts-portal.md).

## <a name="activity-logs"></a>Journaux d’activité
Journaux d’activité donnent une idée des opérations hello qui ont été effectuées sur vos instances de Cache Redis Azure. Ils étaient auparavant nommés « Journaux d’audit » ou « Journaux des opérations ». À l’aide des journaux d’activité, vous pouvez déterminer hello », qui et à quel moment » pour toutes les opérations (PUT, POST, DELETE) effectuées sur vos instances de Cache Redis Azure d’écriture. 

> [!NOTE]
> Les journaux d’activité n’incluent pas les opérations (GET) de lecture.
>
>

journaux d’activité tooview pour votre cache, cliquez sur **journaux d’activité** de hello **menu ressource**.

Pour plus d’informations sur les journaux d’activité, consultez [vue d’ensemble du journal des activités Azure de hello](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).











