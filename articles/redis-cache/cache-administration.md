---
title: aaaHow tooadminister Cache Redis Azure | Documents Microsoft
description: "Découvrez comment redémarrer tels que les tâches d’administration tooperform et planification des mises à jour pour le Cache Redis Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>Comment tooadminister Cache Redis Azure
Cette rubrique décrit des tâches telles que de tooperform administration [redémarrage](#reboot) et [planification des mises à jour](#schedule-updates) pour vos instances de Cache Redis Azure.

## <a name="reboot"></a>Reboot
Hello **redémarrer** panneau vous permet de tooreboot un ou plusieurs nœuds de votre cache. Cette fonctionnalité de redémarrage permet de vous tootest votre application pour assurer la résilience en cas de panne d’un nœud de cache.

![Reboot](./media/cache-administration/redis-cache-administration-reboot.png)

Sélectionnez tooreboot de nœuds hello et cliquez sur **redémarrer**.

![Reboot](./media/cache-administration/redis-cache-reboot.png)

Si vous avez un cache premium avec activation des clusters, vous pouvez sélectionner les partitions de hello cache tooreboot.

![Reboot](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot un ou plusieurs nœuds de votre cache, sélectionnez les nœuds de hello souhaité et cliquez sur **redémarrer**. Si vous avez un cache premium avec activation des clusters, sélectionnez tooreboot de partitions hello souhaité, puis **redémarrer**. Après quelques minutes, hello redémarrage des nœuds sélectionnés et sont en ligne quelques minutes plus tard.

impact de Hello sur les applications clientes varie selon les nœuds de redémarrer votre ordinateur.

* **Master** : quand un nœud principal de hello est redémarré, Azure échoue de Cache Redis sur le nœud de réplica toohello et la promeut toomaster. Au cours de ce basculement, il existe peut-être un court intervalle dans lequel les connexions peuvent échouer toohello cache.
* **Esclave** : quand un nœud subordonné de hello est redémarré, il n’y a généralement aucun client de toocache impact.
* **Maître et esclave** : quand les deux nœuds de cache sont redémarrés, toutes les données sont perdues dans hello du cache et les connexions toohello cache échouent jusqu'à ce que le nœud principal de hello revient en ligne. Si vous avez configuré [persistance des données](cache-how-to-premium-persistence.md), sauvegarde la plus récente hello est restaurée lorsque le cache de hello revient en ligne, mais des écritures de cache qui se sont produites après la sauvegarde la plus récente hello sont perdues.
* **Mettre en cache des nœuds d’une prime avec activation des clusters** : quand vous redémarrez une ou plusieurs nœuds d’un cache premium avec clustering activé, hello comportement pour hello sélectionné nœuds est hello même que lorsque vous redémarrez hello correspondants ou les nœuds d’un non cluster cache.

> [!IMPORTANT]
> Le redémarrage est désormais disponible pour tous les niveaux de tarification.
> 
> 

## <a name="reboot-faq"></a>Forum aux questions sur le redémarrage
* [Le nœud dois-je je redémarre tootest mon application ?](#which-node-should-i-reboot-to-test-my-application)
* [Puis-je redémarrer des connexions de client tooclear hello du cache ?](#can-i-reboot-the-cache-to-clear-client-connections)
* [Vais-je perdre les données dans mon cache si je redémarre ?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [Est-il possible de redémarrer mon cache à l’aide de PowerShell, de l’interface de ligne de commande ou d’autres outils de gestion ?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [Quelle tarification niveaux peut utiliser la fonctionnalité de redémarrage hello ?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>Le nœud dois-je je redémarre tootest mon application ?
résilience de hello tootest de votre application contre les défaillances de nœud principal de hello de votre cache, redémarrage hello **Master** nœud. résilience de hello tootest de votre application contre les défaillances de nœud secondaire hello, redémarrage hello **esclave** nœud. résilience de hello tootest de votre application contre une défaillance totale du cache de hello, redémarrez **les deux** nœuds.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>Puis-je redémarrer des connexions de client tooclear hello du cache ?
Oui, si vous redémarrez cache hello toutes les connexions clientes sont effacées. Le redémarrage peut être utile dans les cas de hello où toutes les connexions clientes sont utilisées en raison d’une erreur logique tooa ou d’un bogue dans l’application cliente de hello. Chaque niveau de tarification dispose de différents [limites de connexion client](cache-configure.md#default-redis-server-configuration) pour hello différentes tailles et une fois ces limites sont atteintes, aucune autre connexion client n’est acceptées. Redémarrage du cache de hello fournit un tooclear de façon toutes les connexions clientes.

> [!IMPORTANT]
> Si vous réinitialisez vos connexions de client de cache tooclear, StackExchange.Redis se reconnecte automatiquement une fois que le nœud de Redis hello est remis en ligne. Si le problème sous-jacent de hello n’est pas résolu, les connexions client hello peuvent continuer toobe utilisé.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>Vais-je perdre les données dans mon cache si je redémarre ?
Si vous redémarrez les deux hello **Master** et **esclave** nœuds, toutes les données dans le cache de hello (ou dans cette partition si vous utilisez un cache premium avec activation des clusters) sont perdues. Si vous avez configuré [persistance des données](cache-how-to-premium-persistence.md), sauvegarde la plus récente hello sera restaurée lorsque le cache de hello revient en ligne, mais des écritures de cache qui se sont produites après la sauvegarde hello sont perdues.

Si vous réinitialisez un seul des nœuds de hello, données ne seront pas perdues en général, mais il peut toujours être. Par exemple, si le nœud principal de hello est réinitialisé et une écriture dans le cache est en cours d’exécution, les données de salutation à partir de l’écriture dans le cache hello est perdue. Un autre scénario de perte de données serait si vous redémarrez un nœud et hello autre nœud produit toogo vers le bas en raison de la panne tooa hello même temps. Pour plus d’informations sur les causes possibles d’une perte de données, consultez [quelles données toomy s’est produit dans Redis ?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>Est-il possible de redémarrer mon cache à l’aide de PowerShell, de l’interface de ligne de commande ou d’autres outils de gestion ?
Oui, pour PowerShell instructions voir [tooreboot un cache Redis](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>Quelle tarification niveaux peut utiliser la fonctionnalité de redémarrage hello ?
Le redémarrage est disponible pour tous les niveaux de tarification.

## <a name="schedule-updates"></a>Planifier les mises à jour
Hello **planifier les mises à jour** panneau vous permet de toodesignate une fenêtre de maintenance de votre cache de niveau Premium. Lors de la fenêtre de maintenance hello est spécifié, les mises à jour du serveur Redis sont effectuées au cours de cette fenêtre. 

> [!NOTE] 
> fenêtre de maintenance Hello s’applique uniquement les mises à jour du serveur tooRedis et pas tooany Azure met à jour ou mises à jour du système d’exploitation de toohello de machines virtuelles hello qui hébergent le cache de hello.
> 
> 

![Planifier les mises à jour](./media/cache-administration/redis-schedule-updates.png)

toospecify une fenêtre de maintenance, vérifiez les jours hello souhaité et spécifier l’heure de début de fenêtre de maintenance hello pour chaque jour, puis cliquez sur **OK**. Notez que l’heure de la fenêtre maintenance hello est au format UTC. 

> [!NOTE]
> fenêtre de maintenance Hello par défaut pour les mises à jour est de cinq heures. Cette valeur n’est pas configurable de hello portail Azure, mais vous pouvez le configurer dans PowerShell à l’aide de hello `MaintenanceWindow` paramètre Hello [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) applet de commande. Pour plus d’informations, voir [Puis-je gérer les mises à jour planifiées à l’aide de PowerShell, de l’interface de ligne de commande ou de tout autre outil de gestion ?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>Forum aux questions de la planification des mises à jour
* [Lorsque les mises à jour se produisent-elles si je n’utilise pas la fonctionnalité mises à jour hello planification ?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [Le type de mises à jour apportées au hello de planifier la fenêtre de maintenance ?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [Puis-je gérer les mises à jour planifiées à l’aide de PowerShell, de l’interface de ligne de commande ou de tout autre outil de gestion ?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [Quelle tarification niveaux peut utiliser la fonctionnalité de mises à jour de planification hello ?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>Lorsque les mises à jour se produisent-elles si je n’utilise pas la fonctionnalité mises à jour hello planification ?
Si vous ne spécifiez pas une fenêtre de maintenance, les mises à jour peuvent être effectuées à tout moment.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>Le type de mises à jour apportées au hello de planifier la fenêtre de maintenance ?
Redis uniquement les mises à jour sont effectuées au cours de la fenêtre de maintenance planifiée hello de serveur. fenêtre de maintenance Hello ne s’applique pas les mises à jour tooAzure ou met à jour de système d’exploitation de l’ordinateur virtuel toohello.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>Puis-je gérer les mises à jour planifiées à l’aide de PowerShell, de l’interface de ligne de commande ou de tout autre outil de gestion ?
Oui, vous pouvez gérer vos mises à jour planifiées à l’aide de hello suivant d’applets de commande PowerShell :

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [New-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Remove-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>Quelle tarification niveaux peut utiliser la fonctionnalité de mises à jour de planification hello ?
Hello **planifier les mises à jour** fonctionnalité est uniquement disponible dans le niveau tarifaire premium de hello.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez plus de fonctionnalités de [niveau Premium du cache Redis Azure](cache-premium-tier-intro.md) .

