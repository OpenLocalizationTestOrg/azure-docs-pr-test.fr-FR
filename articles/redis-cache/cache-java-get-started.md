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
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="49d6b-103">Comment toouse Azure Redis Cache avec Java</span><span class="sxs-lookup"><span data-stu-id="49d6b-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49d6b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="49d6b-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="49d6b-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="49d6b-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="49d6b-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="49d6b-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="49d6b-107">Java</span><span class="sxs-lookup"><span data-stu-id="49d6b-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="49d6b-108">Python</span><span class="sxs-lookup"><span data-stu-id="49d6b-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="49d6b-109">Azure Cache Redis vous donne accès tooa dédié Redis cache, géré par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="49d6b-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="49d6b-110">Votre cache est accessible à partir de n'importe quelle application dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="49d6b-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="49d6b-111">Cette rubrique vous indique comment tooget a démarré avec le Cache Redis Azure à l’aide de Java.</span><span class="sxs-lookup"><span data-stu-id="49d6b-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49d6b-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="49d6b-112">Prerequisites</span></span>
<span data-ttu-id="49d6b-113">[Jedis](https://github.com/xetorthio/jedis) : client Java pour Redis</span><span class="sxs-lookup"><span data-stu-id="49d6b-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="49d6b-114">Ce didacticiel utilise Jedis, mais vous pouvez utiliser n'importe quel client Java parmi ceux répertoriés ici : [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="49d6b-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="49d6b-115">Créer un Cache Redis sur Azure</span><span class="sxs-lookup"><span data-stu-id="49d6b-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="49d6b-116">Récupérer les clés d’accès et nom d’hôte hello</span><span class="sxs-lookup"><span data-stu-id="49d6b-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="49d6b-117">Se connecter cache toohello en toute sécurité à l’aide de SSL</span><span class="sxs-lookup"><span data-stu-id="49d6b-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="49d6b-118">Hello dernières builds de [jedis](https://github.com/xetorthio/jedis) prennent en charge pour la connexion tooAzure Cache Redis à l’aide de SSL.</span><span class="sxs-lookup"><span data-stu-id="49d6b-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="49d6b-119">Hello, l’exemple suivant montre comment la tooconnect tooAzure Redis Cache à l’aide hello point de terminaison SSL de 6380.</span><span class="sxs-lookup"><span data-stu-id="49d6b-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="49d6b-120">Remplacez `<name>` avec nom hello de votre cache et `<key>` avec l’option votre clé primaire ou secondaire comme décrit dans hello précédente [récupérer les clés d’accès et nom d’hôte hello](#retrieve-the-host-name-and-access-keys) section.</span><span class="sxs-lookup"><span data-stu-id="49d6b-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="49d6b-121">port non-SSL de Hello est désactivé pour les nouvelles instances de Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="49d6b-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="49d6b-122">Si vous utilisez un autre client qui ne prennent pas en charge SSL, consultez [comment tooenable hello port non-SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="49d6b-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="49d6b-123">Ajoutez un élément toohello mettre en cache et récupérer</span><span class="sxs-lookup"><span data-stu-id="49d6b-123">Add something toohello cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="49d6b-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49d6b-124">Next steps</span></span>
* <span data-ttu-id="49d6b-125">[Activer les diagnostics de cache](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) afin de pouvoir [moniteur](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello d’intégrité de votre cache.</span><span class="sxs-lookup"><span data-stu-id="49d6b-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="49d6b-126">Lecture hello officielle [Redis documentation](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="49d6b-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
