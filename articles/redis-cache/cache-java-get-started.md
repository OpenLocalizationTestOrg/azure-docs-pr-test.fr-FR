---
title: Utilisation du Cache Redis Azure avec Java | Microsoft Docs
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
ms.openlocfilehash: 3cfad3a7279b5f9bbff1e6cd9794c492e3544752
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-java"></a><span data-ttu-id="4c2ed-103">Utilisation du Cache Redis Azure avec Java</span><span class="sxs-lookup"><span data-stu-id="4c2ed-103">How to use Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c2ed-104">.NET</span><span class="sxs-lookup"><span data-stu-id="4c2ed-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="4c2ed-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4c2ed-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="4c2ed-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="4c2ed-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="4c2ed-107">Java</span><span class="sxs-lookup"><span data-stu-id="4c2ed-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="4c2ed-108">Python</span><span class="sxs-lookup"><span data-stu-id="4c2ed-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="4c2ed-109">Le Cache Redis Azure permet d’accéder à un cache Redis dédié géré par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4c2ed-109">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="4c2ed-110">Votre cache est accessible à partir de n'importe quelle application dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4c2ed-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="4c2ed-111">Cette rubrique montre comment utiliser le Cache Redis Azure avec Java.</span><span class="sxs-lookup"><span data-stu-id="4c2ed-111">This topic shows you how to get started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c2ed-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4c2ed-112">Prerequisites</span></span>
<span data-ttu-id="4c2ed-113">[Jedis](https://github.com/xetorthio/jedis) : client Java pour Redis</span><span class="sxs-lookup"><span data-stu-id="4c2ed-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="4c2ed-114">Ce didacticiel utilise Jedis, mais vous pouvez utiliser n'importe quel client Java parmi ceux répertoriés ici : [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="4c2ed-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="4c2ed-115">Créer un Cache Redis sur Azure</span><span class="sxs-lookup"><span data-stu-id="4c2ed-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="4c2ed-116">Récupérer les clés d’accès et le nom hôte</span><span class="sxs-lookup"><span data-stu-id="4c2ed-116">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="4c2ed-117">Connexion au cache en toute sécurité à l’aide de SSL</span><span class="sxs-lookup"><span data-stu-id="4c2ed-117">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="4c2ed-118">Les dernières versions de [jedis](https://github.com/xetorthio/jedis) prennent en charge la connexion au Cache Redis Azure avec SSL.</span><span class="sxs-lookup"><span data-stu-id="4c2ed-118">The latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="4c2ed-119">L’exemple suivant montre comment se connecter au Cache Redis Azure à l’aide du point de terminaison SSL 6380.</span><span class="sxs-lookup"><span data-stu-id="4c2ed-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="4c2ed-120">Remplacez `<name>` par le nom de votre cache et `<key>` par votre clé primaire ou secondaire tel que décrit dans la section précédente [Récupérer les clés d’accès et le nom hôte](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="4c2ed-120">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="4c2ed-121">Le port non SSL est désactivé pour les nouvelles instances Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="4c2ed-121">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="4c2ed-122">Si vous utilisez un autre client qui ne prend pas en charge SSL, la procédure d’activation du port non SSL est expliquée [ici](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="4c2ed-122">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="4c2ed-123">Ajouter un élément au cache et le récupérer</span><span class="sxs-lookup"><span data-stu-id="4c2ed-123">Add something to the cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="4c2ed-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c2ed-124">Next steps</span></span>
* <span data-ttu-id="4c2ed-125">[Activez les diagnostics du cache](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) afin de pouvoir [surveiller](https://msdn.microsoft.com/library/azure/dn763945.aspx) l’intégrité de votre cache.</span><span class="sxs-lookup"><span data-stu-id="4c2ed-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) the health of your cache.</span></span>
* <span data-ttu-id="4c2ed-126">Lisez la [documentation Redis](http://redis.io/documentation)officielle.</span><span class="sxs-lookup"><span data-stu-id="4c2ed-126">Read the official [Redis documentation](http://redis.io/documentation).</span></span>
