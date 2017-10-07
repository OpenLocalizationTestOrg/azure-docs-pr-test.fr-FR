---
title: aaaHow toouse du Cache Redis Azure avec Node.js | Documents Microsoft
description: Prise en main du Cache Redis Azure avec Node.js et node_redis
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Comment toouse Azure Redis Cache avec Node.js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Cache Redis vous donne accès au tooa sécurisé Redis cache dédié, géré par Microsoft. Votre cache est accessible à partir de n'importe quelle application dans Microsoft Azure.

Cette rubrique vous indique comment tooget a démarré avec le Cache Redis Azure à l’aide de Node.js. Pour obtenir un autre exemple d'utilisation du Cache Redis Azure avec Node.js, consultez la rubrique [Créer une application de conversation instantanée Node.js avec Socket.IO sur un site web Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).

## <a name="prerequisites"></a>Composants requis
Installez [node_redis](https://github.com/mranney/node_redis) :

    npm install redis

Ce didacticiel utilise [node_redis](https://github.com/mranney/node_redis). Pour obtenir des exemples d’utilisation d’autres clients Node.js, consultez la documentation d’individuels de hello pour les clients de Node.js hello répertoriés au [clients de Node.js Redis](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Créer un Cache Redis sur Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Récupérer les clés d’accès et nom d’hôte hello
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Se connecter cache toohello en toute sécurité à l’aide de SSL
Hello dernières builds de [node_redis](https://github.com/mranney/node_redis) prennent en charge pour la connexion tooAzure Cache Redis à l’aide de SSL. Hello, l’exemple suivant montre comment la tooconnect tooAzure Redis Cache à l’aide hello point de terminaison SSL de 6380. Remplacez `<name>` avec nom hello de votre cache et `<key>` avec l’option votre clé primaire ou secondaire comme décrit dans hello précédente [récupérer les clés d’accès et nom d’hôte hello](#retrieve-the-host-name-and-access-keys) section.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> port non-SSL de Hello est désactivé pour les nouvelles instances de Cache Redis Azure. Si vous utilisez un autre client qui ne prennent pas en charge SSL, consultez [comment tooenable hello port non-SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Ajoutez un élément toohello mettre en cache et récupérer
Hello suivant montre l’exemple vous comment tooconnect tooan Azure redis-Cache instance et stockez et récupérer un élément à partir du cache de hello. Pour plus d’exemples d’utilisation de Redis par hello [node_redis](https://github.com/mranney/node_redis) client, consultez [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Output:

    OK
    value


## <a name="next-steps"></a>Étapes suivantes
* [Activer les diagnostics de cache](cache-how-to-monitor.md#enable-cache-diagnostics) afin de pouvoir [moniteur](cache-how-to-monitor.md) hello d’intégrité de votre cache.
* Lecture hello officielle [Redis documentation](http://redis.io/documentation).

