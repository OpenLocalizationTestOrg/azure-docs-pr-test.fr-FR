---
title: aaaHow toouse du Cache Redis Azure avec Java | Documents Microsoft
description: Prise en main du Cache Redis Azure avec Java
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a>Comment toouse Azure Redis Cache avec Java
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure Cache Redis vous donne accès tooa dédié Redis cache, géré par Microsoft. Votre cache est accessible à partir de n'importe quelle application dans Microsoft Azure.

Cette rubrique vous indique comment tooget a démarré avec le Cache Redis Azure à l’aide de Java.

## <a name="prerequisites"></a>Composants requis
[Jedis](https://github.com/xetorthio/jedis) : client Java pour Redis

Ce didacticiel utilise Jedis, mais vous pouvez utiliser n'importe quel client Java parmi ceux répertoriés ici : [http://redis.io/clients](http://redis.io/clients).

## <a name="create-a-redis-cache-on-azure"></a>Créer un Cache Redis sur Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Récupérer les clés d’accès et nom d’hôte hello
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Se connecter cache toohello en toute sécurité à l’aide de SSL
Hello dernières builds de [jedis](https://github.com/xetorthio/jedis) prennent en charge pour la connexion tooAzure Cache Redis à l’aide de SSL. Hello, l’exemple suivant montre comment la tooconnect tooAzure Redis Cache à l’aide hello point de terminaison SSL de 6380. Remplacez `<name>` avec nom hello de votre cache et `<key>` avec l’option votre clé primaire ou secondaire comme décrit dans hello précédente [récupérer les clés d’accès et nom d’hôte hello](#retrieve-the-host-name-and-access-keys) section.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> port non-SSL de Hello est désactivé pour les nouvelles instances de Cache Redis Azure. Si vous utilisez un autre client qui ne prennent pas en charge SSL, consultez [comment tooenable hello port non-SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Ajoutez un élément toohello mettre en cache et récupérer
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a>Étapes suivantes
* [Activer les diagnostics de cache](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) afin de pouvoir [moniteur](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello d’intégrité de votre cache.
* Lecture hello officielle [Redis documentation](http://redis.io/documentation).
