---
title: aaaManage du Cache Redis Azure avec Azure PowerShell | Documents Microsoft
description: "Découvrez comment tooperform les tâches d’administration pour le Cache Redis Azure à l’aide d’Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a>Gestion du Cache Redis Azure avec Azure PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](cache-howto-manage-redis-cache-powershell.md)
> * [Interface de ligne de commande Azure](cache-manage-cli.md)
> 
> 

Cette rubrique vous montre comment tooperform courants des tâches telles que créer, mettre à jour et mettre à l’échelle vos instances de Cache Redis Azure, comment tooregenerate clés d’accès et la manière dont les informations de tooview sur vos caches. Pour obtenir une liste complète des applets de commande PowerShell de cache Redis Azure, consultez [Applets de commande de cache Redis Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

Pour plus d’informations sur le modèle de déploiement classique de hello, consultez [Azure Resource Manager et déploiement classique : comprendre les modèles de déploiement et état de vos ressources de hello](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).

## <a name="prerequisites"></a>Composants requis
Si vous avez déjà installé Azure PowerShell, vous devez disposer d’Azure PowerShell version 1.0.0 ou ultérieure. Vous pouvez vérifier la version de hello d’Azure PowerShell que vous avez installé avec cette commande à l’invite de commande Azure PowerShell hello.

    Get-Module azure | format-table version


Tout d’abord, vous devez vous connecter tooAzure avec cette commande.

    Login-AzureRmAccount

Spécifiez l’adresse de messagerie de hello de votre compte Azure et son mot de passe dans la boîte de dialogue hello signe dans Microsoft Azure.

Si vous avez plusieurs abonnements Azure, vous devez ensuite tooset votre abonnement Azure. toosee une liste de vos abonnements en cours, exécutez la commande.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

abonnement de hello toospecify, exécutez hello commande suivante. Dans l’exemple suivant de hello, nom de l’abonnement hello est `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

Avant de pouvoir utiliser Windows PowerShell avec Azure Resource Manager, vous devez suivant de hello :

* Windows PowerShell, version 3.0 ou 4.0. version de hello toofind de Windows PowerShell, tapez :`$PSVersionTable` et vérifiez la valeur hello `PSVersion` est 3.0 ou 4.0. tooinstall une version compatible, consultez [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

tooget détaillées aide pour une applet de commande que vous voyez dans ce didacticiel, l’applet de commande Get-Help utilisez hello.

    Get-Help <cmdlet-name> -Detailed

Par exemple, tooget aide hello `New-AzureRmRedisCache` applet, tapez :

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a>Comment tooconnect tooother clouds
Par hello de valeur par défaut Azure environnement est `AzureCloud`, qui représente hello instance globale de cloud Azure. tooconnect tooa instance différente, utilisez hello `Add-AzureRmAccount` avec hello `-Environment` ou -`EnvironmentName` commutateur de ligne de commande avec l’environnement désiré de hello ou nom de l’environnement.

liste de hello toosee des environnements disponibles, exécutez hello `Get-AzureRmEnvironment` applet de commande.

### <a name="tooconnect-toohello-azure-government-cloud"></a>tooconnect toohello le Cloud Azure Government
tooconnect toohello Azure Government Cloud, utilisez une des hello suivant les commandes.

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

ou

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

toocreate un cache Bonjour Azure Government Cloud, utilisez un des emplacements suivants de hello.

* Gouvernement américain - Virginie
* USGov Iowa

Pour plus d’informations sur hello gouvernement le Cloud Azure, consultez [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) et [Guide de développement Microsoft Azure Government](../azure-government-developer-guide.md).

### <a name="tooconnect-toohello-azure-china-cloud"></a>tooconnect toohello le Cloud Azure en Chine
tooconnect toohello Azure en Chine Cloud, utilisez une des hello suivant les commandes.

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

ou

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

toocreate un cache Bonjour Azure en Chine Cloud, utilisez un des emplacements suivants de hello.

* Chine orientale
* Chine du Nord

Pour plus d’informations sur hello le Cloud Azure en Chine, consultez [AzureChinaCloud pour Azure géré par 21Vianet en Chine](http://www.windowsazure.cn/).

### <a name="tooconnect-toomicrosoft-azure-germany"></a>tooconnect tooMicrosoft Azure situés en Allemagne
tooconnect tooMicrosoft Allemagne d’Azure, utilisez une des hello suivant les commandes.

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


ou

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

toocreate un cache dans Microsoft Azure Allemagne, utilisez un des emplacements suivants de hello.

* Centre de l’Allemagne
* Nord-Est de l’Allemagne

Pour plus d’informations sur Microsoft Azure Allemagne, consultez [Microsoft Azure Allemagne](https://azure.microsoft.com/overview/clouds/germany/).

### <a name="properties-used-for-azure-redis-cache-powershell"></a>Propriétés utilisées pour le cache Redis Azure PowerShell
Hello tableau suivant contient les propriétés et les descriptions de paramètres couramment utilisés lors de la création et la gestion de vos instances de Cache Redis Azure à l’aide d’Azure PowerShell.

| Paramètre | Description | Default |
| --- | --- | --- |
| Nom |Nom du cache de hello | |
| Lieu |Emplacement du cache de hello | |
| ResourceGroupName |Nom de groupe de ressources dans le cache de hello toocreate | |
| Taille |taille de Hello du cache de hello. Les valeurs valides sont : P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 Mo, 1 Go, 2,5 Go, 6 Go, 13 Go, 26 Go, 53 Go |1 Go |
| Nombre de partitions |nombre de Hello de partitions toocreate lors de la création d’un cache premium avec activation des clusters. Les valeurs valides sont : 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 | |
| SKU |Spécifie les hello référence (SKU) du cache de hello. Les valeurs valides sont : De base, Standard, Premium |Standard |
| RedisConfiguration |Spécifie les paramètres de configuration de Redis. Pour plus d’informations sur chaque paramètre, voir hello [RedisConfiguration propriétés](#redisconfiguration-properties) table. | |
| enableNonSslPort |Indique si le port de hello non-SSL est activé. |False |
| MaxMemoryPolicy |Ce paramètre est obsolète. Utilisez RedisConfiguration à la place. | |
| StaticIP |Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie une adresse IP unique dans un sous-réseau hello pour le cache de hello. Si n’est fourni, une est choisie pour vous à partir du sous-réseau de hello. | |
| Sous-réseau |Lorsque vous hébergez votre cache dans un réseau virtuel, spécifie le nom hello du sous-réseau de hello dans le cache de hello toodeploy. | |
| VirtualNetwork |Lorsque votre cache dans un réseau virtuel, d’hébergement spécifie hello les ID de ressource de hello réseau virtuel dans le cache de hello toodeploy. | |
| KeyType |Spécifie la clé d’accès tooregenerate lors du renouvellement de clés d’accès. Les valeurs valides sont : Primaire, Secondaire | |

### <a name="redisconfiguration-properties"></a>Propriétés RedisConfiguration
| Propriété | Description | Niveaux de tarification |
| --- | --- | --- |
| rdb-backup-enabled |Indique si [la persistance des données Redis](cache-how-to-premium-persistence.md) est activée |Premium uniquement |
| rdb-storage-connection-string |Hello compte de stockage de toohello de chaîne de connexion pour [Redis la persistance des données](cache-how-to-premium-persistence.md) |Premium uniquement |
| rdb-backup-frequency |Hello fréquence de sauvegarde pour [Redis la persistance des données](cache-how-to-premium-persistence.md) |Premium uniquement |
| maxmemory-reserved |Configure hello [mémoire réservée](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) pour les processus non mises en cache |Standard et Premium |
| maxmemory-policy |Configure hello [stratégie d’éviction](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) pour cache de hello |Tous les niveaux de tarification |
| notify-keyspace-events |Configure les [notifications d’espace de clés](cache-configure.md#keyspace-notifications-advanced-settings) |Standard et Premium |
| hash-max-ziplist-entries |Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées |Standard et Premium |
| hash-max-ziplist-value |Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées |Standard et Premium |
| set-max-intset-entries |Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées |Standard et Premium |
| zset-max-ziplist-entries |Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées |Standard et Premium |
| zset-max-ziplist-value |Configure [l’optimisation de la mémoire](http://redis.io/topics/memory-optimization) pour les petites quantités de types de données agrégées |Standard et Premium |
| bases de données |Configure le nombre de hello de bases de données. Cette propriété ne peut être configurée qu’au moment de la création du cache. |Standard et Premium |

## <a name="toocreate-a-redis-cache"></a>toocreate un Cache Redis
Nouvelle instance de Cache Redis Azure est créée à l’aide de hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) applet de commande.

> [!IMPORTANT]
> Hello lors de la création d’un cache Redis dans un abonnement à l’aide de hello portail Azure, le portail de hello inscrit hello `Microsoft.Cache` espace de noms pour cet abonnement. Si vous essayez toocreate hello Redis tout d’abord le cache d’un abonnement à l’aide de PowerShell, vous devez d’abord inscrire cet espace de noms à l’aide de hello suivant de commande ; applets de commande sinon comme `New-AzureRmRedisCache` et `Get-AzureRmRedisCache` échouent.
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

toosee une liste des paramètres disponibles et leurs descriptions pour `New-AzureRmRedisCache`, exécutez hello après une commande.

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

toocreate un cache avec les paramètres par défaut, exécutez hello commande suivante.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

`ResourceGroupName`, `Name`, et `Location` sont des paramètres obligatoires, mais le reste de hello sont facultative et leurs valeurs par défaut. Exécute la commande précédente hello de crée une instance Standard référence (SKU) du Cache Redis Azure avec le nom spécifié de hello, l’emplacement et groupe de ressources, qui est de 1 Go de taille avec hello non-SSL port est désactivé.

toocreate un cache premium, spécifiez une taille de P1 (6 Go - 60 Go), P2 (13 à 130 Go), P3 (26 à 260 Go), ou P4 (53 à 530 Go). tooenable clustering, spécifiez un nombre de partitions à l’aide de hello `ShardCount` paramètre. Hello exemple suivant crée un cache premium de P1 avec 3 partitions. Un cache premium de P1 est de 6 Go de taille, et étant donné que nous avons spécifié trois partitions hello taille totale est 18 (3 x 6 Go).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

valeurs toospecify pour hello `RedisConfiguration` paramètre, placer les valeurs à l’intérieur de hello `{}` en tant que clé/valeur comme paires `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`. Hello exemple suivant crée un cache de 1 Go standard avec `allkeys-random` maxmemory de stratégie et d’espace de clés les notifications configurées avec `KEA`. Pour plus d’informations, voir [Notifications de keyspace (paramètres avancés)](cache-configure.md#keyspace-notifications-advanced-settings) et [Stratégies de mémoire](cache-configure.md#memory-policies).

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a>tooconfigure hello paramètre bases de données lors de la création du cache
Hello `databases` paramètre peut être configuré uniquement pendant la création du cache. Hello exemple suivant crée un premium P3 (26 Go) de cache avec 48 bases de données à l’aide de hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) applet de commande.

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

Pour plus d’informations sur hello `databases` propriété, consultez [configuration du serveur par défaut le Cache Redis Azure](cache-configure.md#default-redis-server-configuration). Pour plus d’informations sur la création d’un cache à l’aide de hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) applet de commande, consultez hello précédente [toocreate un Cache Redis](#to-create-a-redis-cache) section.

## <a name="tooupdate-a-redis-cache"></a>tooupdate un cache Redis
Les instances de Cache Redis Azure sont mis à jour à l’aide de hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) applet de commande.

toosee une liste des paramètres disponibles et leurs descriptions pour `Set-AzureRmRedisCache`, exécutez hello après une commande.

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Hello `Set-AzureRmRedisCache` applet de commande peut être utilisé tooupdate des propriétés, telles que `Size`, `Sku`, `EnableNonSslPort`et hello `RedisConfiguration` valeurs. 

Hello commande suivante, les mises à jour hello maxmemory-policy pour hello Cache Redis nommé myCache.

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a>tooscale un cache Redis
`Set-AzureRmRedisCache`peut être utilisé tooscale une instance de cache Redis Azure lorsque hello `Size`, `Sku`, ou `ShardCount` propriétés sont modifiées. 

> [!NOTE]
> Mise à l’échelle un cache à l’aide de PowerShell est sujet toohello mêmes limites et des recommandations en tant que la mise à l’échelle un cache à partir de hello portail Azure. Vous pouvez faire évoluer tooa autre niveau de tarification par hello suivant des restrictions.
> 
> * Vous ne pouvez pas mettre à l’échelle à partir d’un tooa niveau tarifaire la plus élevée plus faible niveau de tarification.
> * Vous ne pouvez pas mettre à l’échelle à partir d’un **Premium** cache vers le bas tooa **Standard** ou un **base** cache.
> * Vous ne pouvez pas mettre à l’échelle à partir d’un **Standard** cache vers le bas tooa **base** cache.
> * Vous pouvez mettre à l’échelle d’un **base** cache tooa **Standard** cache, mais que vous ne pouvez pas modifier la taille de hello en hello même temps. Si vous avez besoin d’une taille différente, vous pouvez effectuer une taille suivantes toohello souhaité d’opération mise à l’échelle.
> * Vous ne pouvez pas mettre à l’échelle à partir d’un **base** mettre en cache directement tooa **Premium** cache. Vous devez mettre à l’échelle à partir de **base** trop**Standard** en une seule opération de mise à l’échelle, puis de **Standard** trop**Premium** dans une mise à l’échelle suivantes opération.
> * Vous ne peut pas mettre à l’échelle à partir d’une plus grande taille vers le bas toohello **C0 (250 Mo)** taille.
> 
> Pour plus d’informations, consultez [comment tooScale Cache Redis Azure](cache-how-to-scale.md).
> 
> 

Hello suivant montre comment tooscale un cache nommé `myCache` tooa 2,5 Go de cache. Notez que cette commande fonctionne pour un cache De base ou un cache Standard.

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Une fois cette commande est émise, état hello du cache de hello est retourné (similaire toocalling `Get-AzureRmRedisCache`). Notez que hello `ProvisioningState` est `Scaling`.

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

Lorsque hello mise à l’échelle d’opération est terminée, hello `ProvisioningState` change également`Succeeded`. Si vous avez besoin de toomake une opération de mise à l’échelle suivante, telles que la modification de base tooStandard et puis taille de hello, vous devez attendre jusqu'à ce que l’opération précédente hello est terminée ou vous recevez un suivant de toohello erreur similaire.

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a>informations de tooget sur un cache Redis
Vous pouvez récupérer des informations sur un cache à l’aide de hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) applet de commande.

toosee une liste des paramètres disponibles et leurs descriptions pour `Get-AzureRmRedisCache`, exécutez hello après une commande.

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooreturn plus d’informations sur tous les caches de l’abonnement actuel de hello, exécutez `Get-AzureRmRedisCache` sans aucun paramètre.

    Get-AzureRmRedisCache

tooreturn plus d’informations sur tous les caches dans le groupe de ressources spécifique, exécutez `Get-AzureRmRedisCache` avec hello `ResourceGroupName` paramètre.

    Get-AzureRmRedisCache -ResourceGroupName myGroup

tooreturn plus d’informations sur un cache en particulier, exécutez `Get-AzureRmRedisCache` avec hello `Name` paramètre contenant le nom hello du cache de hello et hello `ResourceGroupName` paramètre avec le groupe de ressources hello contenant ce cache.

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a>touches d’accès tooretrieve hello pour un cache Redis
touches d’accès tooretrieve hello pour votre cache, vous pouvez utiliser hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) applet de commande.

toosee une liste des paramètres disponibles et leurs descriptions pour `Get-AzureRmRedisCacheKey`, exécutez hello après une commande.

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

tooretrieve hello clés pour votre cache, appel hello `Get-AzureRmRedisCacheKey` applet de commande et passez nom hello de votre cache hello nom hello du groupe de ressources qui contient le cache de hello.

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a>touches d’accès tooregenerate pour votre cache Redis
touches d’accès tooregenerate hello pour votre cache, vous pouvez utiliser hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) applet de commande.

toosee une liste des paramètres disponibles et leurs descriptions pour `New-AzureRmRedisCacheKey`, exécutez hello après une commande.

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

clé de principale ou secondaire de hello pour votre cache, appel hello tooregenerate `New-AzureRmRedisCacheKey` applet de commande et passez hello nom, groupe de ressources et spécifier `Primary` ou `Secondary` pour hello `KeyType` paramètre. Bonjour l’exemple suivant, la clé d’accès secondaire hello pour un cache est régénéré.

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a>toodelete un cache Redis
toodelete un cache Redis, utilisez hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) applet de commande.

toosee une liste des paramètres disponibles et leurs descriptions pour `Remove-AzureRmRedisCache`, exécutez hello après une commande.

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

Dans l’exemple suivant de hello, hello cache nommé `myCache` est supprimé.

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a>tooimport un cache Redis
Vous pouvez importer des données dans une instance de Cache Redis Azure à l’aide de hello `Import-AzureRmRedisCache` applet de commande.

> [!IMPORTANT]
> L’importation/exportation est uniquement disponible pour les caches de niveau [Premium](cache-premium-tier-intro.md) . Pour plus d’informations sur l’importation/exportation, voir [Importer et exporter des données dans le cache Redis Azure](cache-how-to-import-export-data.md).
> 
> 

toosee une liste des paramètres disponibles et leurs descriptions pour `Import-AzureRmRedisCache`, exécutez hello après une commande.

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello commande suivante importe les données d’objet blob de hello spécifié par l’uri SAS hello dans le Cache Redis Azure.

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a>tooexport un cache Redis
Vous pouvez exporter des données à partir d’une instance de Cache Redis Azure à l’aide de hello `Export-AzureRmRedisCache` applet de commande.

> [!IMPORTANT]
> L’importation/exportation est uniquement disponible pour les caches de niveau [Premium](cache-premium-tier-intro.md) . Pour plus d’informations sur l’importation/exportation, voir [Importer et exporter des données dans le cache Redis Azure](cache-how-to-import-export-data.md).
> 
> 

toosee une liste des paramètres disponibles et leurs descriptions pour `Export-AzureRmRedisCache`, exécutez hello après une commande.

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello commande suivante exporte les données à partir d’une instance de Cache Redis Azure dans le conteneur de hello spécifié par l’uri SAS hello.

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a>tooreboot un cache Redis
Vous pouvez redémarrer votre instance de Cache Redis Azure à l’aide de hello `Reset-AzureRmRedisCache` applet de commande.

> [!IMPORTANT]
> Le redémarrage est uniquement disponible pour les caches de [niveau Premium](cache-premium-tier-intro.md) . Pour plus d’informations sur le redémarrage de votre cache, voir [Administration du cache - Redémarrage](cache-administration.md#reboot).
> 
> 

toosee une liste des paramètres disponibles et leurs descriptions pour `Reset-AzureRmRedisCache`, exécutez hello après une commande.

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


Hello commande suivante redémarre les deux nœuds de hello spécifié cache.

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur l’utilisation de Windows PowerShell avec Azure, consultez hello suivant des ressources :

* [Documentation relative à l’applet de commande Cache Redis Azure sur MSDN](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* [Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): découvrir toouse hello applets de commande dans le module du Gestionnaire de ressources Azure hello.
* [À l’aide de la ressource groupes toomanage vos ressources Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Découvrez comment toocreate et gérer des groupes de ressources de hello portail Azure.
* [Blog Azure](http://blogs.msdn.com/windowsazure): découvrez les nouvelles fonctionnalités d'Azure.
* [Blog Windows PowerShell](http://blogs.msdn.com/powershell): découvrez les nouvelles fonctionnalités de Windows PowerShell.
* [Blog Blog](http://blogs.technet.com/b/heyscriptingguy/): obtenir réel trucs et astuces de hello Communauté de Windows PowerShell.

