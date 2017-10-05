---
title: Guide pratique pour utiliser Cache Redis Azure avec Node.js | Microsoft Docs
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
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="45839-103">Utilisation du Cache Redis Azure avec Node.js</span><span class="sxs-lookup"><span data-stu-id="45839-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45839-104">.NET</span><span class="sxs-lookup"><span data-stu-id="45839-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="45839-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="45839-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="45839-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="45839-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="45839-107">Java</span><span class="sxs-lookup"><span data-stu-id="45839-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="45839-108">Python</span><span class="sxs-lookup"><span data-stu-id="45839-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="45839-109">Le Cache Redis Azure permet d'accéder à un cache Redis sécurisé et dédié, géré par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="45839-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="45839-110">Votre cache est accessible à partir de n'importe quelle application dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="45839-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="45839-111">Cette rubrique montre comment utiliser le Cache Redis Azure avec Node.js.</span><span class="sxs-lookup"><span data-stu-id="45839-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="45839-112">Pour obtenir un autre exemple d'utilisation du Cache Redis Azure avec Node.js, consultez la rubrique [Créer une application de conversation instantanée Node.js avec Socket.IO sur un site web Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="45839-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45839-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="45839-113">Prerequisites</span></span>
<span data-ttu-id="45839-114">Installez [node_redis](https://github.com/mranney/node_redis) :</span><span class="sxs-lookup"><span data-stu-id="45839-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="45839-115">Ce didacticiel utilise [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="45839-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="45839-116">Pour obtenir des exemples d’utilisation des autres clients Node.js, consultez la documentation individuelle pour les [clients Redis Node.js](http://redis.io/clients#nodejs)répertoriés.</span><span class="sxs-lookup"><span data-stu-id="45839-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="45839-117">Créer un Cache Redis sur Azure</span><span class="sxs-lookup"><span data-stu-id="45839-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="45839-118">Récupérer les clés d’accès et le nom hôte</span><span class="sxs-lookup"><span data-stu-id="45839-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="45839-119">Connexion au cache en toute sécurité à l’aide de SSL</span><span class="sxs-lookup"><span data-stu-id="45839-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="45839-120">Les dernières versions de [node_redis](https://github.com/mranney/node_redis) prennent en charge la connexion au Cache Redis Azure avec SSL.</span><span class="sxs-lookup"><span data-stu-id="45839-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="45839-121">L’exemple suivant montre comment se connecter au Cache Redis Azure à l’aide du point de terminaison SSL 6380.</span><span class="sxs-lookup"><span data-stu-id="45839-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="45839-122">Remplacez `<name>` par le nom de votre cache et `<key>` par votre clé primaire ou secondaire tel que décrit dans la section précédente [Récupérer les clés d’accès et le nom hôte](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="45839-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="45839-123">Le port non SSL est désactivé pour les nouvelles instances Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="45839-123">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="45839-124">Si vous utilisez un autre client qui ne prend pas en charge SSL, la procédure d’activation du port non SSL est expliquée [ici](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="45839-124">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="45839-125">Ajouter un élément au cache et le récupérer</span><span class="sxs-lookup"><span data-stu-id="45839-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="45839-126">L’exemple suivant montre comment se connecter à une instance du Cache Redis Azure et de stocker ou récupérer un élément dans le cache.</span><span class="sxs-lookup"><span data-stu-id="45839-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="45839-127">Pour plus d’exemples d’utilisation de Redis avec le client [node_redis](https://github.com/mranney/node_redis), consultez [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="45839-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="45839-128">Output:</span><span class="sxs-lookup"><span data-stu-id="45839-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="45839-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45839-129">Next steps</span></span>
* <span data-ttu-id="45839-130">[Activez les diagnostics du cache](cache-how-to-monitor.md#enable-cache-diagnostics) afin de pouvoir [surveiller](cache-how-to-monitor.md) l’intégrité de votre cache.</span><span class="sxs-lookup"><span data-stu-id="45839-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="45839-131">Lisez la [documentation Redis](http://redis.io/documentation)officielle.</span><span class="sxs-lookup"><span data-stu-id="45839-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>

