---
title: aaaHow tooScale Cache Redis Azure | Documents Microsoft
description: "Découvrez comment tooscale votre Azure Redis Cache des instances"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a>Comment tooScale Cache Redis Azure
Cache Redis Azure a différentes offres de cache, qui fournissent une certaine flexibilité hello les choix de la taille du cache et de fonctionnalités. Après la création d’un cache, vous pouvez adapter la taille de hello et hello tarification du cache de hello si hello les besoins de votre application changent. Cet article vous explique comment tooscale votre cache dans hello portail Azure et à l’aide des outils tels que Azure PowerShell et CLI d’Azure.

## <a name="when-tooscale"></a>Lorsque tooscale
Vous pouvez utiliser hello [analyse](cache-how-to-monitor.md) fonctionnalités de Cache Redis Azure toomonitor hello intégrité et les performances de votre cache et vous aider à déterminer quand tooscale hello du cache. 

Vous pouvez surveiller les éléments suivants de hello métriques toohelp déterminer si vous avez besoin de tooscale.

* Charge du serveur Redis
* Utilisation de la mémoire
* Bande passante réseau
* Utilisation du processeur

Si vous déterminez que votre cache n’est plus répond bien aux exigences de votre application, vous pouvez faire évoluer tooa ou réduire la taille du cache tarification est adapté aux besoins de votre application. Pour plus d’informations sur la détermination de qui mettent en cache toouse de niveau tarifaire, consultez [offre de Cache Redis et de la taille d’utilisation](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="scale-a-cache"></a>Mise à l’échelle d’un cache
tooscale votre cache, [parcourir le cache de toohello](cache-configure.md#configure-redis-cache-settings) Bonjour [portail Azure](https://portal.azure.com) et cliquez sur **échelle** de hello **menu ressource**.

![Mettre à l'échelle](./media/cache-how-to-scale/redis-cache-scale-menu.png)

Sélectionnez hello souhaité niveau tarifaire de hello **sélectionnez tarification** panneau, cliquez sur **sélectionnez**.

![Niveau tarifaire ][redis-cache-pricing-tier-blade]


Vous pouvez faire évoluer tooa autre niveau de tarification par hello suivant restrictions :

* Vous ne pouvez pas mettre à l’échelle à partir d’un tooa niveau tarifaire la plus élevée plus faible niveau de tarification.
  * Vous ne pouvez pas mettre à l’échelle à partir d’un **Premium** cache vers le bas tooa **Standard** ou un **base** cache.
  * Vous ne pouvez pas mettre à l’échelle à partir d’un **Standard** cache vers le bas tooa **base** cache.
* Vous pouvez mettre à l’échelle d’un **base** cache tooa **Standard** cache, mais que vous ne pouvez pas modifier la taille de hello en hello même temps. Si vous avez besoin d’une taille différente, vous pouvez effectuer une taille suivantes toohello souhaité d’opération mise à l’échelle.
* Vous ne pouvez pas mettre à l’échelle à partir d’un **base** mettre en cache directement tooa **Premium** cache. Vous devez mettre à l’échelle à partir de **base** trop**Standard** en une seule opération de mise à l’échelle, puis de **Standard** trop**Premium** dans une mise à l’échelle suivantes opération.
* Vous ne peut pas mettre à l’échelle à partir d’une plus grande taille vers le bas toohello **C0 (250 Mo)** taille.
 
Alors que le cache de hello est mise à l’échelle toohello nouveau tarification, un **mise à l’échelle** état est affiché dans hello **Cache Redis** panneau.

![Mise à l'échelle][redis-cache-scaling]

Lors de la mise à l’échelle est terminée, hello état à partir de **mise à l’échelle** trop**en cours d’exécution**.

## <a name="how-tooautomate-a-scaling-operation"></a>Comment tooautomate une opération de mise à l’échelle
En outre tooscaling vos instances de cache dans hello portail Azure, vous pouvez mettre à l’échelle à l’aide des applets de commande PowerShell CLI d’Azure et à l’aide de hello Microsoft Azure Management bibliothèques (MAML). 

* [Mise à l’échelle à l’aide de PowerShell](#scale-using-powershell)
* [Mise à l’échelle à l’aide de l’interface de ligne de commande Azure](#scale-using-azure-cli)
* [Mise à l’échelle à l’aide de MAML](#scale-using-maml)

### <a name="scale-using-powershell"></a>Mise à l’échelle à l’aide de PowerShell
Vous pouvez faire évoluer vos instances de Cache Redis Azure avec PowerShell à l’aide de hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) quand hello `Size`, `Sku`, ou `ShardCount` propriétés sont modifiées. Hello suivant montre comment tooscale un cache nommé `myCache` tooa 2,5 Go de cache. 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Pour plus d’informations sur la mise à l’échelle avec PowerShell, consultez [tooscale un Redis cache à l’aide de Powershell](cache-howto-manage-redis-cache-powershell.md#scale).

### <a name="scale-using-azure-cli"></a>Mise à l’échelle à l’aide de l’interface de ligne de commande Azure
appel de vos instances de Cache Redis Azure à l’aide d’Azure CLI, tooscale hello `azure rediscache set` commande et passez les modifications de configuration hello souhaité qui incluent une nouvelle taille, référence (SKU) ou taille de cluster, en fonction de hello souhaité opération de mise à l’échelle.

Pour plus d’informations sur la mise à l’échelle avec l’interface de ligne de commande Azure, consultez [Modification des paramètres d’un Cache Redis existant](cache-manage-cli.md#scale).

### <a name="scale-using-maml"></a>Mise à l’échelle à l’aide de MAML
tooscale vos instances de Cache Redis Azure à l’aide de hello [Microsoft Azure Management bibliothèques (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), appel hello `IRedisOperations.CreateOrUpdate` (méthode) et passez hello nouvelle taille pour hello `RedisProperties.SKU.Capacity`.

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

Pour plus d’informations, consultez hello [gérer le Cache Redis à l’aide MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) exemple.

## <a name="scaling-faq"></a>FAQ sur la mise à l’échelle
Hello liste suivante contient toocommonly des réponses aux questions sur la mise à l’échelle le Cache Redis Azure.

* [Puis-je mettre à l’échelle vers, depuis ou au sein d’un cache Premium ?](#can-i-scale-to-from-or-within-a-premium-cache)
* [Après la mise à l’échelle, dois-je toochange mes clés d’accès ou le nom du cache ?](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [Comment fonctionne la mise à l’échelle ?](#how-does-scaling-work)
* [Vais-je perdre mes données de cache durant la mise à l’échelle ?](#will-i-lose-data-from-my-cache-during-scaling)
* [Les paramètres personnalisés de mes bases de données sont-ils affectés au cours de la mise à l’échelle ?](#is-my-custom-databases-setting-affected-during-scaling)
* [Mon cache reste-t-il disponible durant la mise à l’échelle ?](#will-my-cache-be-available-during-scaling)
* [Quelles sont les opérations qui ne sont pas prises en charge ?](#operations-that-are-not-supported)
* [Quelle est la durée d’une mise à l’échelle ?](#how-long-does-scaling-take)
* [Comment savoir quand la mise à l’échelle est terminée ?](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>Puis-je mettre à l’échelle vers, depuis ou au sein d’un cache Premium ?
* Vous ne pouvez pas mettre à l’échelle à partir d’un **Premium** cache vers le bas tooa **base** ou **Standard** niveau tarifaire.
* Vous pouvez mettre à l’échelle à partir d’un **Premium** cache tooanother de niveau de tarification.
* Vous ne pouvez pas mettre à l’échelle à partir d’un **base** mettre en cache directement tooa **Premium** cache. Vous devez tout d’abord mettre à l’échelle à partir de **base** trop**Standard** en une seule opération de mise à l’échelle, puis de **Standard** trop**Premium** dans une ultérieure opération de mise à l’échelle.
* Si vous avez activé la gestion de clusters lorsque vous avez créé votre **Premium** cache, vous pouvez [modifier la taille de cluster hello](cache-how-to-premium-clustering.md#cluster-size). Si votre cache a été créé sans clustering activé, vous ne pouvez pas configurer le clustering à une date ultérieure.
  
  Pour plus d’informations, consultez [comment tooconfigure clustering Premium Azure Redis cache](cache-how-to-premium-clustering.md).

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>Après la mise à l’échelle, dois-je toochange mes clés d’accès ou le nom du cache ?
Non, le nom et les clés d’accès de votre cache n’ont pas à être modifiés durant une opération de mise à l’échelle.

### <a name="how-does-scaling-work"></a>Comment fonctionne la mise à l’échelle ?
* Lorsqu’un **base** cache est mis à l’échelle tooa de taille différente, il est arrêté et un nouveau cache configuré à l’aide de la nouvelle taille de hello. Pendant ce temps, le cache de hello n’est pas disponible, et toutes les données dans le cache de hello est perdu.
* Lorsqu’un **base** cache est mis à l’échelle tooa **Standard** cache, un cache de réplica est configuré et les données de salutation sont copiées à partir du cache de hello cache principal toohello réplica. cache de Hello reste disponible pendant le processus de mise à l’échelle de hello.
* Lorsqu’un **Standard** cache est mis à l’échelle tooa une taille différente ou tooa **Premium** cache, un des réplicas de hello est arrêté et redéployées toohello nouvelle taille et hello données transférées sur, puis hello autres réplica effectue un basculement avant qu’il est remis en service, le processus toohello similaire qui se produit lors d’une défaillance de l’un des nœuds de cache hello.

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>Vais-je perdre mes données de cache durant la mise à l’échelle ?
* Lorsqu’un **base** cache est mis à l’échelle tooa nouvelle taille, toutes les données est perdue et cache de hello n’est pas disponible pendant l’opération de mise à l’échelle de hello.
* Lorsqu’un **base** cache est mis à l’échelle tooa **Standard** de cache, hello les données dans le cache de hello sont généralement conservées.
* Lorsqu’un **Standard** cache est tooa à l’échelle plus grande taille ou la couche, ou un **Premium** cache est mis à l’échelle tooa plus grande taille, toutes les données est généralement conservée. Lors de la mise à l’échelle un **Standard** ou **Premium** cache vers le bas tooa plus petite taille, données peut-être être perdue selon la quantité de données est dans le cache de hello liées toohello nouvelle taille lorsqu’il est mis à l’échelle. Si les données sont perdues lors de la mise à l’échelle vers le bas, les clés sont supprimés à l’aide de hello [allkeys-lru](http://redis.io/topics/lru-cache) stratégie d’éviction. 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>Les paramètres personnalisés de mes bases de données sont-ils affectés au cours de la mise à l’échelle ?
Certains niveaux de tarification ont différents [limites des bases de données](cache-configure.md#databases), donc il existe certaines considérations lors de la mise à l’échelle vers le bas if vous configuré une valeur personnalisée pour hello `databases` paramètre lors de la création du cache.

* Lorsque mise à l’échelle tooa tarification avec une faible `databases` limite au niveau actuel de hello :
  * Si vous utilisez le nombre par défaut de hello de `databases` qui n’est 16 pour tous les niveaux de tarification, aucune donnée n’est perdue.
  * Si vous utilisez un nombre de `databases` qui se situe dans les limites de hello pour hello toowhich de couche vous à l’échelle, cela `databases` est conservé et aucune donnée n’est perdue.
  * Si vous utilisez un nombre de `databases` qui dépasse les limites de hello du nouveau niveau de hello, hello `databases` paramètre est garantie toohello les limites du nouveau niveau de hello et toutes les données dans les bases de données hello supprimé sont perdues.
* Lorsque mise à l’échelle tooa tarification identique ou ultérieure avec hello `databases` limite au niveau actuel de hello votre `databases` est conservé et aucune donnée n’est perdue.

Notez que, si les caches Standard et Premium ont un contrat SLA proposant une disponibilité de 99,9 %, il n’existe pas de contrat SLA contre la perte de données.

### <a name="will-my-cache-be-available-during-scaling"></a>Mon cache reste-t-il disponible durant la mise à l’échelle ?
* **Standard** et **Premium** caches restent disponibles pendant l’opération de mise à l’échelle de hello.
* **Base** caches sont hors connexion pendant la mise à l’échelle de taille différente de tooa opérations, mais restent disponibles lors de la mise à l’échelle à partir de **base** trop**Standard**.

### <a name="operations-that-are-not-supported"></a>Quelles sont les opérations qui ne sont pas prises en charge ?
* Vous ne pouvez pas mettre à l’échelle à partir d’un tooa niveau tarifaire la plus élevée plus faible niveau de tarification.
  * Vous ne pouvez pas mettre à l’échelle à partir d’un **Premium** cache vers le bas tooa **Standard** ou un **base** cache.
  * Vous ne pouvez pas mettre à l’échelle à partir d’un **Standard** cache vers le bas tooa **base** cache.
* Vous pouvez mettre à l’échelle d’un **base** cache tooa **Standard** cache, mais que vous ne pouvez pas modifier la taille de hello en hello même temps. Si vous avez besoin d’une taille différente, vous pouvez effectuer une taille suivantes toohello souhaité d’opération mise à l’échelle.
* Vous ne pouvez pas mettre à l’échelle à partir d’un **base** mettre en cache directement tooa **Premium** cache. Vous devez tout d’abord mettre à l’échelle à partir de **base** trop**Standard** en une seule opération de mise à l’échelle, puis de **Standard** trop**Premium** dans une ultérieure opération de mise à l’échelle.
* Vous ne peut pas mettre à l’échelle à partir d’une plus grande taille vers le bas toohello **C0 (250 Mo)** taille.

En cas d’une opération de mise à l’échelle, service de hello va essayer d’opération de hello toorevert et cache de hello reviendra de taille d’origine de toohello.

### <a name="how-long-does-scaling-take"></a>Quelle est la durée d’une mise à l’échelle ?
Mise à l’échelle de la prend environ 20 minutes, selon la quantité de données est dans le cache de hello.

### <a name="how-can-i-tell-when-scaling-is-complete"></a>Comment savoir quand la mise à l’échelle est terminée ?
Bonjour portail Azure, vous pouvez voir hello mise à l’échelle d’opération en cours. Lors de la mise à l’échelle est terminée, l’état des modifications de cache hello hello trop**en cours d’exécution**.

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



