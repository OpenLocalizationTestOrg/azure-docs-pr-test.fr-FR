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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="75457-103">Comment toouse Azure Redis Cache avec Node.js</span><span class="sxs-lookup"><span data-stu-id="75457-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75457-104">.NET</span><span class="sxs-lookup"><span data-stu-id="75457-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="75457-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="75457-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="75457-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="75457-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="75457-107">Java</span><span class="sxs-lookup"><span data-stu-id="75457-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="75457-108">Python</span><span class="sxs-lookup"><span data-stu-id="75457-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="75457-109">Azure Cache Redis vous donne accès au tooa sécurisé Redis cache dédié, géré par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="75457-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="75457-110">Votre cache est accessible à partir de n'importe quelle application dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="75457-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="75457-111">Cette rubrique vous indique comment tooget a démarré avec le Cache Redis Azure à l’aide de Node.js.</span><span class="sxs-lookup"><span data-stu-id="75457-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="75457-112">Pour obtenir un autre exemple d'utilisation du Cache Redis Azure avec Node.js, consultez la rubrique [Créer une application de conversation instantanée Node.js avec Socket.IO sur un site web Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="75457-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75457-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="75457-113">Prerequisites</span></span>
<span data-ttu-id="75457-114">Installez [node_redis](https://github.com/mranney/node_redis) :</span><span class="sxs-lookup"><span data-stu-id="75457-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="75457-115">Ce didacticiel utilise [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="75457-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="75457-116">Pour obtenir des exemples d’utilisation d’autres clients Node.js, consultez la documentation d’individuels de hello pour les clients de Node.js hello répertoriés au [clients de Node.js Redis](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="75457-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="75457-117">Créer un Cache Redis sur Azure</span><span class="sxs-lookup"><span data-stu-id="75457-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="75457-118">Récupérer les clés d’accès et nom d’hôte hello</span><span class="sxs-lookup"><span data-stu-id="75457-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="75457-119">Se connecter cache toohello en toute sécurité à l’aide de SSL</span><span class="sxs-lookup"><span data-stu-id="75457-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="75457-120">Hello dernières builds de [node_redis](https://github.com/mranney/node_redis) prennent en charge pour la connexion tooAzure Cache Redis à l’aide de SSL.</span><span class="sxs-lookup"><span data-stu-id="75457-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="75457-121">Hello, l’exemple suivant montre comment la tooconnect tooAzure Redis Cache à l’aide hello point de terminaison SSL de 6380.</span><span class="sxs-lookup"><span data-stu-id="75457-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="75457-122">Remplacez `<name>` avec nom hello de votre cache et `<key>` avec l’option votre clé primaire ou secondaire comme décrit dans hello précédente [récupérer les clés d’accès et nom d’hôte hello](#retrieve-the-host-name-and-access-keys) section.</span><span class="sxs-lookup"><span data-stu-id="75457-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="75457-123">port non-SSL de Hello est désactivé pour les nouvelles instances de Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="75457-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="75457-124">Si vous utilisez un autre client qui ne prennent pas en charge SSL, consultez [comment tooenable hello port non-SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="75457-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="75457-125">Ajoutez un élément toohello mettre en cache et récupérer</span><span class="sxs-lookup"><span data-stu-id="75457-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="75457-126">Hello suivant montre l’exemple vous comment tooconnect tooan Azure redis-Cache instance et stockez et récupérer un élément à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="75457-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="75457-127">Pour plus d’exemples d’utilisation de Redis par hello [node_redis](https://github.com/mranney/node_redis) client, consultez [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="75457-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="75457-128">Output:</span><span class="sxs-lookup"><span data-stu-id="75457-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="75457-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="75457-129">Next steps</span></span>
* <span data-ttu-id="75457-130">[Activer les diagnostics de cache](cache-how-to-monitor.md#enable-cache-diagnostics) afin de pouvoir [moniteur](cache-how-to-monitor.md) hello d’intégrité de votre cache.</span><span class="sxs-lookup"><span data-stu-id="75457-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="75457-131">Lecture hello officielle [Redis documentation](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="75457-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

