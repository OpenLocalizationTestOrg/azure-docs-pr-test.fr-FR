---
title: aaaHow tooconfigure Redis clustering Premium Azure Redis cache | Documents Microsoft
description: "Découvrez comment toocreate et gérer Redis clustering pour vos instances de Cache Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Comment tooconfigure Redis clustering Premium Azure Redis cache
Cache Redis Azure a différentes offres de cache, qui fournissent une certaine flexibilité hello les choix de la taille du cache et de fonctionnalités, y compris les fonctionnalités de niveau Premium telles que le clustering, la persistance et la prise en charge du réseau virtuel. Cet article décrit comment tooconfigure clustering dans une prime Cache Redis Azure instance.

Pour plus d’informations sur d’autres fonctionnalités de cache premium, consultez [couche de présentation toohello Azure Redis Cache Premium](cache-premium-tier-intro.md).

## <a name="what-is-redis-cluster"></a>Qu’est-ce que le cluster Redis ?
Le Cache Redis Azure propose le cluster Redis tel qu' [implémenté dans Redis](http://redis.io/topics/cluster-tutorial). Avec le Cluster Redis, vous obtenez hello avantages suivants : 

* Bonjour tooautomatically possibilité fractionner votre jeu de données entre plusieurs nœuds. 
* opérations toocontinue Hello possibilité lorsqu’un sous-ensemble de nœuds de hello connaît des échecs ou sont toocommunicate impossible avec rest hello du cluster de hello. 
* Plus grand débit : débit augmente de façon linéaire lorsque vous augmentez le nombre de hello de partitions. 
* Taille de la mémoire : augmente de façon linéaire lorsque vous augmentez le nombre de hello de partitions.  

Pour plus d’informations sur la taille, le débit et la bande passante des caches Premium, consultez [Que propose Cache Redis et quelle taille dois-je utiliser ?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

Dans Azure, le cluster Redis est proposé en tant que principal/réplica modèle où chaque partition a une paire principal/réplica avec la réplication dans lequel la réplication hello est gérée par le service de Cache Redis Azure. 

## <a name="clustering"></a>Clustering
Le clustering est activé sur hello **nouveau Cache Redis** panneau lors de la création du cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Gestion de clusters est configurée sur hello **Redis de Cluster** panneau.

![Clustering][redis-cache-clustering]

Vous pouvez utiliser jusqu'à too10 des partitions dans un cluster de hello. Cliquez sur **activé** et faites glisser le curseur de hello ou tapez un nombre compris entre 1 et 10 pour **nombre de partitions** et cliquez sur **OK**.

Chaque partition est une paire de cache principal/réplica gérée par Azure, et taille totale de hello du cache de hello est calculée en multipliant le nombre hello de partitions par taille de cache de hello sélectionné Bonjour niveau tarifaire. 

![Clustering][redis-cache-clustering-selected]

Après la création d’un cache de hello vous vous connectez tooit et utiliser simplement comme un cache non cluster et Redis distribue des données de hello dans l’ensemble de partitions du Cache hello. Si les diagnostics sont [activé](cache-how-to-monitor.md#enable-cache-diagnostics), métriques sont capturés séparément pour chaque partition et peut être [affichés](cache-how-to-monitor.md) dans le panneau de Cache Redis hello. 

> [!NOTE]
> 
> Il doit exister quelques différences mineures dans votre application cliente lorsque le clustering est configuré. Pour plus d’informations, consultez [dois-je toomake tout toouse d’application de modifications toomy client clustering ?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Pour un exemple de code sur l’utilisation de la gestion de clusters avec le client StackExchange.Redis de hello, consultez hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) partie Hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemple.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>Modifier la taille de cluster hello sur en cours d’exécution cache premium
taille du cluster toochange hello sur une prime en cours d’exécution du cache avec le clustering des activé, cliquez sur **taille de Cluster Redis** de hello **menu ressource**.

> [!NOTE]
> Alors que hello Azure Redis Cache Premium couche a été publié tooGeneral disponibilité, hello taille de Cluster Redis fonctionnalité est actuellement en version préliminaire.
> 
> 

![Taille du cluster Redis][redis-cache-redis-cluster-size]

taille de cluster toochange hello, utilisez hello curseur ou tapez un nombre compris entre 1 et 10 dans hello **nombre de partitions** zone de texte et cliquez sur **OK** toosave.

> [!NOTE]
> Mise à l’échelle d’un cluster s’exécute hello [migration](https://redis.io/commands/migrate) commande, qui est une commande coûteuse, par conséquent, pour minimiser l’impact, envisagez d’exécuter cette opération pendant les heures creuses. Au cours du processus de migration hello, vous verrez un pic de charge du serveur. Mise à l’échelle d’un cluster est un entier long en cours d’exécution processus et durée hello de varie selon le nombre de hello de clés et la taille des valeurs hello associés à ces clés.
> 
> 

## <a name="clustering-faq"></a>Forum aux questions sur le clustering
Hello liste suivante contient toocommonly des réponses aux questions sur les clusters de Cache Redis Azure.

* [Dois-je toomake tout toouse d’application de modifications toomy client clustering ?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [Comment les clés sont-elles distribuées dans un cluster ?](#how-are-keys-distributed-in-a-cluster)
* [Quelle est la plus grande taille du cache Bonjour, que je peux créer ?](#what-is-the-largest-cache-size-i-can-create)
* [Tous les clients Redis prennent-ils en charge le clustering ?](#do-all-redis-clients-support-clustering)
* [Comment connecter toomy cache lors de la mise en cluster est activé ?](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [Puis-je connecter directement toohello différentes partitions de mon cache ?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [Puis-je configurer le clustering pour un cache créé précédemment ?](#can-i-configure-clustering-for-a-previously-created-cache)
* [Puis-je configurer le clustering pour un cache De base ou Standard ?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [Puis-je utiliser le clustering avec les fournisseurs d’état de Session ASP.NET Redis et la mise en cache de sortie hello ?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [J’obtiens des exceptions MOVE lorsque j’utilise StackExchange.Redis et le clustering, que dois-je faire ?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>Dois-je toomake tout toouse d’application de modifications toomy client clustering ?
* Lorsque le clustering est activé, seule la base de données 0 est disponible. Si votre application cliente utilise plusieurs bases de données et il tente de base de données tooread ou écriture tooa différente de 0, hello exception suivante est levée. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->``StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  Pour plus d’informations, consultez [Redis Cluster Specification - Implemented subset](http://redis.io/topics/cluster-spec#implemented-subset)(Spécification de cluster Redis - Implémentation de jeu de données).
* Si vous utilisez [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), vous devez utiliser la version 1.0.481 ou une version ultérieure. Vous vous connectez toohello cache à l’aide de hello même [clés, les ports et les points de terminaison](cache-configure.md#properties) que vous utilisez lors de la connexion tooa cache qui n’a pas l’activation des clusters. Hello seule différence est que toutes les lectures et écritures doivent être effectuées toodatabase 0.
  
  * D’autres clients peuvent avoir des exigences différentes. Consultez [Tous les clients Redis prennent-ils en charge le clustering ?](#do-all-redis-clients-support-clustering)
* Si votre application utilise plusieurs opérations traitées par lot dans une commande unique, toutes les clés doivent se trouver dans hello même ID de partition. les clés toolocate dans hello même ID de partition, consultez [comment les clés sont distribuées dans un cluster ?](#how-are-keys-distributed-in-a-cluster)
* Si vous utilisez un fournisseur d’état de session ASP.NET Redis, vous devez utiliser la version 2.0.1 ou une version ultérieure. Consultez [puis-je utiliser le clustering avec les fournisseurs d’état de Session ASP.NET Redis et la mise en cache de sortie hello ?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>Comment les clés sont-elles distribuées dans un cluster ?
Par hello Redis [modèle de distribution de clés](http://redis.io/topics/cluster-spec#keys-distribution-model) documentation : espace de clé hello est fractionnée en 16384 emplacements. Chaque clé est haché et affecté tooone de ces emplacements, qui sont réparties entre les nœuds hello du cluster de hello. Vous pouvez configurer la partie de la clé de hello est haché tooensure appartenant à plusieurs clés hello même ID de partition à l’aide de balises de hachage.

* Si une partie de la clé de hello est placé entre des clés avec une balise de hachage - `{` et `}`, seule la partie de clé de hello est hachée à des fins hello permettant de déterminer l’emplacement de hachage hello d’une clé. Par exemple, hello suivant 3 clés se trouvent dans hello même ID de partition : `{key}1`, `{key}2`, et `{key}3` depuis uniquement hello `key` partie du nom de hello est haché. Pour obtenir une liste complète des spécifications de balises de hachage de clés, consultez [Balises de hachage de clés](http://redis.io/topics/cluster-spec#keys-hash-tags).
* Clés sans une balise de hachage - nom de la clé entière hello est utilisé pour le hachage. Cela entraîne une répartition statistiquement entre les partitions hello du cache de hello.

Pour meilleures performances et le débit, nous vous recommandons de distribuer les clés de hello uniformément. Si vous utilisez des clés avec une balise de hachage, il est responsabilité tooensure hello les clés de l’application hello sont distribuées uniformément.

Pour plus d’informations, consultez [Modèle de distribution de clés](http://redis.io/topics/cluster-spec#keys-distribution-model), [Partitionnement de données de cluster Redis](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding) et [Balises de hachage de clés](http://redis.io/topics/cluster-spec#keys-hash-tags).

Pour un exemple de code sur l’utilisation avec le clustering et la localisation des clés dans hello même ID de partition avec le client StackExchange.Redis de hello, consultez hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) partie Hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemple.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>Quelle est la plus grande taille du cache Bonjour, que je peux créer ?
plus grande taille de cache premium Hello est 53 go. Vous pouvez créer des partitions too10 ce qui vous donne une taille maximale de 530 Go. Si vous avez besoin d’une plus grande taille, vous pouvez en [faire la demande](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). Pour plus d'informations, consultez [Tarification - Cache Redis Azure](https://azure.microsoft.com/pricing/details/cache/).

### <a name="do-all-redis-clients-support-clustering"></a>Tous les clients Redis prennent-ils en charge le clustering ?
À hello actuellement que pas tous les clients prennent en charge Redis clustering. StackExchange.Redis est l’un de ceux qui le prennent en charge. Pour plus d’informations sur d’autres clients, consultez hello [lecture avec un cluster de hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) section Hello [didacticiel de cluster Redis](http://redis.io/topics/cluster-tutorial).

> [!NOTE]
> Si vous utilisez StackExchange.Redis comme client, assurez-vous de vous utilisez la version la plus récente de hello [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 ou version ultérieure pour le clustering toowork correctement. Si vous rencontrez des problèmes avec les exceptions MOVE, consultez la [section consacrée aux exceptions MOVE](#move-exceptions) pour plus d’informations.
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>Comment connecter toomy cache lors de la mise en cluster est activé ?
Vous pouvez vous connecter tooyour cache à l’aide de hello même [points de terminaison](cache-configure.md#properties), [ports](cache-configure.md#properties), et [clés](cache-configure.md#access-keys) que vous utilisez lors de la connexion tooa cache qui n’a pas l’activation des clusters. Redis gère hello clustering sur hello principal, vous n’avez pas toomanage à partir de votre client.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>Puis-je connecter directement toohello différentes partitions de mon cache ?
Cela n’est pas officiellement pris en charge. Ceci étant dit, chaque partition composée d’une paire de caches principal/réplica désignés collectivement sous le nom d’« instance de cache ». Vous pouvez vous connecter à l’aide d’utilitaire de redis-cli hello Bonjour des instances de cache toothese [instable](http://redis.io/download) branche du référentiel de Redis hello dans GitHub. Cette version implémente la prise en charge de base lors de la main hello `-c` basculer. Pour plus d’informations, consultez [lecture avec un cluster de hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) sur [http://redis.io](http://redis.io) Bonjour [didacticiel de cluster Redis](http://redis.io/topics/cluster-tutorial).

Non-SSL, utilisez hello suivant les commandes.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

Avec SSL, remplacez `1300N` par `1500N`.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>Puis-je configurer le clustering pour un cache créé précédemment ?
Actuellement, vous pouvez activer le clustering uniquement quand vous créez un cache. Vous pouvez modifier la taille de cluster hello après hello cache est créé, mais Impossible d’ajouter du cache de clustering tooa premium ou de supprimer les clusters à partir d’un cache premium après que hello cache est créé. Un cache premium avec activation des clusters et qu’une seule partition est différent de celle d’un cache premium Hello même taille avec aucun des clusters.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>Puis-je configurer le clustering pour un cache De base ou Standard ?
Le clustering est disponible uniquement pour les caches de niveau Premium.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>Puis-je utiliser le clustering avec les fournisseurs d’état de Session ASP.NET Redis et la mise en cache de sortie hello ?
* **Fournisseur de caches de sortie Redis** : aucune modification requise.
* **Fournisseur d’état de Session redis** -toouse clustering, vous devez utiliser [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 ou plus élevé ou une exception est levée. Il s’agit d’une modification avec rupture. Pour plus d’informations, consultez [Détails de la modification avec rupture pour la version 2.0.0](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>J’obtiens des exceptions MOVE lorsque j’utilise StackExchange.Redis et le clustering, que dois-je faire ?
Si vous utilisez StackExchange.Redis et recevez des exceptions `MOVE` lors du clustering, assurez-vous que vous utilisez [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) ou version ultérieure. Pour obtenir des instructions sur la configuration de votre toouse d’applications .NET StackExchange.Redis, consultez [configurer les clients de cache hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment mettre en cache des fonctionnalités par toouse plus premium.

* [Couche de présentation toohello Azure Redis Cache Premium](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







