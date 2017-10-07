---
title: exemples de Cache Redis aaaAzure | Documents Microsoft
description: "Découvrez comment toouse Cache Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Exemples de Cache Redis Azure
Cette rubrique fournit une liste d’exemples de Cache Redis Azure, qui couvrent des scénarios tels que la connexion tooa cache, la lecture et l’écriture des données tooand à partir d’un cache à l’aide des fournisseurs de Cache de Redis ASP.NET hello. Certains des exemples de hello sont téléchargeables projets, et certains fournissent des instructions et incluent les extraits de code, mais ne pas lier le projet téléchargeable de tooa.

## <a name="hello-world-samples"></a>Exemples Hello world
exemples Hello dans cette section montrent les principes fondamentaux de hello de connexion d’instance de Cache Redis Azure tooan lors de la lecture et l’écriture et toohello du cache des données à l’aide de divers langages d’et clients Redis.

Hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemple montre comment tooperform différents du cache des opérations à l’aide de hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) client .NET.

Cet exemple montre comment :

* Utiliser les différentes options de connexion
* Lire et écrire des objets tooand à partir du cache de hello à l’aide des opérations synchrones et asynchrones
* Utilisez Redis MGET/MSET commandes tooreturn les valeurs de clés spécifiées.
* Effectuer des opérations Redis transactionnelles
* Utiliser des listes Redis et des ensembles triés
* Stocker des objets .NET à l’aide des sérialiseurs JsonConvert
* Utilisez Redis définit un marquage tooimplement
* Travailler avec le Cluster Redis

Pour plus d’informations, consultez hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) documentation sur github et pour les scénarios d’utilisation plus voir hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) tests unitaires.

[Comment toouse Azure Redis Cache avec Python](cache-python-get-started.md) indique comment tooget a démarré avec le Cache Redis Azure à l’aide de Python et hello [redis-pier](https://github.com/andymccurdy/redis-py) client.

[Utiliser des objets .NET dans le cache de hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) montre vous tooserialize monodirectionnelle .NET des objets afin de pouvoir les écrire tooand les lire à partir d’une instance de Cache Redis Azure. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>Utiliser le Cache Redis comme un fond de panier de montée en puissance pour ASP.NET SignalR
Hello [utiliser Redis Cache comme une montée en charge l’infrastructure d’intégration pour ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) exemple illustre comment vous pouvez utiliser le Cache Redis Azure comme infrastructure d’intégration SignalR. Pour plus d’informations sur le fond de panier, consultez [SignalR Scaleout with Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).

## <a name="redis-cache-customer-query-sample"></a>Exemple de requête client dans le Cache Redis
Cet exemple compare les performances entre l'accès aux données à partir d'un cache et l'accès aux données à partir d'un espace de persistance. Cet exemple comporte deux projets.

* [Démonstration de l’amélioration des performances par la mise en cache des données avec le cache Redis](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [Valeur de départ hello base de données et de Cache pour une démonstration de hello](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>État de session ASP.NET et mise en cache de la sortie
Hello [toostore d’utiliser Azure Redis Cache ASP.NET SessionState et OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) exemple illustre la façon dont le Cache Redis Azure toouse vous toostore Session ASP.NET et à l’aide du Cache de sortie hello SessionState et OutputCache fournisseurs pour Redis.

## <a name="manage-azure-redis-cache-with-maml"></a>Gérer le Cache Redis Azure avec MAML
Hello [gérer le Cache Redis Azure à l’aide des bibliothèques de gestion Azure](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) exemple illustre comment vous pouvez utiliser les bibliothèques de gestion Azure toomanage - (créer / mettre à jour / Supprimer) votre Cache. 

## <a name="custom-monitoring-sample"></a>Exemple de surveillance personnalisée
Hello [des données d’analyse d’accès Redis Cache](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) exemple illustre comment vous pouvez accéder à des données d’analyse pour votre Cache Redis Azure en dehors de hello portail Azure.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>Un clone de style Twitter écrit avec PHP et Redis
Hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis) exemple est hello Redis Hello World. Il s’agit d’un clone de réseau social Twitter style minimale écrit à l’aide de Redis et PHP à l’aide de hello [Predis](https://github.com/nrk/predis) client. code source de Hello est conçue toobe très simple et à hello même moment tooshow différentes structures de données Redis.

## <a name="bandwidth-monitor"></a>Surveiller la bande passante
Hello [moniteur de la bande passante](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) exemple vous permet de toomonitor hello la bande passante utilisée sur le client de hello. toomeasure hello la bande passante, d’exécuter l’exemple hello sur l’ordinateur client de cache hello, effectuer des appels toohello cache et observer la bande passante hello signalée par exemple analyse de la bande passante hello.

