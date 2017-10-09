---
title: aaaHow tooUse Cache Redis Azure | Documents Microsoft
description: "Découvrez comment tooimprove hello les performances de vos applications Azure avec le Cache Redis Azure"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="2b3d7-103">Comment tooUse Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="2b3d7-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b3d7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="2b3d7-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="2b3d7-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2b3d7-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="2b3d7-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2b3d7-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="2b3d7-107">Java</span><span class="sxs-lookup"><span data-stu-id="2b3d7-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="2b3d7-108">Python</span><span class="sxs-lookup"><span data-stu-id="2b3d7-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="2b3d7-109">Ce guide vous explique comment tooget main **Cache Redis Azure**.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="2b3d7-110">Le Cache Redis Microsoft Azure est basé sur hello open source populaires du Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="2b3d7-111">Elle vous donne accès tooa sécurisé Redis cache dédié, géré par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="2b3d7-112">Un cache créé avec Cache Redis Azure est accessible à partir de toutes les applications dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="2b3d7-113">Le Cache Redis Microsoft Azure est disponible dans hello suivant niveaux :</span><span class="sxs-lookup"><span data-stu-id="2b3d7-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="2b3d7-114">**De base** , avec un seul nœud.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-114">**Basic** – Single node.</span></span> <span data-ttu-id="2b3d7-115">Plusieurs tailles de too53 go.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="2b3d7-116">**Standard** : avec deux nœuds, principal et réplica.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="2b3d7-117">Plusieurs tailles de too53 go.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="2b3d7-118">Un contrat SLA de 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-118">99.9% SLA.</span></span>
* <span data-ttu-id="2b3d7-119">**Premium** – deux nœuds principal/réplica avec les partitions de too10.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="2b3d7-120">Tailles multiples de 6 Go too530 go.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="2b3d7-121">Toutes les fonctionnalités du niveau Standard et d’autres, y compris la prise en charge du [cluster Redis](cache-how-to-premium-clustering.md), la [persistance Redis](cache-how-to-premium-persistence.md) et le [réseau virtuel Azure](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="2b3d7-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="2b3d7-122">Un contrat SLA de 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-122">99.9% SLA.</span></span>

<span data-ttu-id="2b3d7-123">Chaque option diffère en termes de fonctionnalités et de tarification.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="2b3d7-124">Pour plus d’informations sur la tarification, consultez la rubrique [Détails de tarification Cache][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="2b3d7-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="2b3d7-125">Ce guide vous montre comment toouse hello [StackExchange.Redis] [ StackExchange.Redis] client à l’aide de C\# code.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="2b3d7-126">Hello scénarios abordés incluent **création et configuration d’un cache**, **configuration des clients de cache**, et **Ajout et suppression d’objets du cache de hello**.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="2b3d7-127">Pour plus d’informations sur l’utilisation du Cache Redis Azure, consultez [Étapes suivantes][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="2b3d7-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="2b3d7-128">Pour obtenir un didacticiel de création d’application web avec le Cache Redis un ASP.NET MVC, consultez [comment toocreate une application Web avec le Cache Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="2b3d7-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="2b3d7-129">Prise en main de Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="2b3d7-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="2b3d7-130">La prise en main de Cache Redis Azure est aisée.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="2b3d7-131">tooget démarré, vous approvisionner et configurer un cache.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="2b3d7-132">Ensuite, vous configurez les clients de cache hello afin de pouvoir accéder à cache de hello.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="2b3d7-133">Une fois que les clients de cache hello sont configurés, vous pouvez commencer leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="2b3d7-134">[Créer le cache de hello][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="2b3d7-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="2b3d7-135">[Configurer les clients de cache hello][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="2b3d7-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="2b3d7-136">Création d'un cache</span><span class="sxs-lookup"><span data-stu-id="2b3d7-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="2b3d7-137">tooaccess votre cache après qu’il est créé.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="2b3d7-138">Pour plus d’informations sur la configuration de votre cache, consultez [comment tooconfigure le Cache Redis Azure](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="2b3d7-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="2b3d7-139">Configurer les clients de cache hello</span><span class="sxs-lookup"><span data-stu-id="2b3d7-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="2b3d7-140">Une fois votre projet client est configuré pour la mise en cache, vous pouvez utiliser les techniques de hello décrites Bonjour les sections pour travailler avec votre cache suivantes.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="2b3d7-141">Utilisation des caches</span><span class="sxs-lookup"><span data-stu-id="2b3d7-141">Working with Caches</span></span>
<span data-ttu-id="2b3d7-142">étapes de Hello dans cette section décrivent des tâches de tooperform commun avec le Cache.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="2b3d7-143">[Se connecter toohello cache][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="2b3d7-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="2b3d7-144">[Ajouter et récupérer des objets à partir du cache de hello][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="2b3d7-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="2b3d7-145">Utiliser des objets .NET dans le cache de hello</span><span class="sxs-lookup"><span data-stu-id="2b3d7-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="2b3d7-146">Se connecter toohello cache</span><span class="sxs-lookup"><span data-stu-id="2b3d7-146">Connect toohello cache</span></span>
<span data-ttu-id="2b3d7-147">travail de tooprogrammatically avec un cache, vous avez besoin d’un cache de toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="2b3d7-148">Ajoutez hello suivant haut toohello de tous les fichiers à partir de laquelle vous souhaitez toouse hello StackExchange.Redis client tooaccess un cache Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="2b3d7-149">client de Hello StackExchange.Redis nécessite .NET Framework 4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="2b3d7-150">Hello toohello connexion Cache Redis Azure est géré par hello `ConnectionMultiplexer` classe.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="2b3d7-151">Cette classe doit être partagée réutilisée dans votre application cliente et n’a pas besoin toobe créé sur chaque opération.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="2b3d7-152">tooconnect tooan Cache Redis Azure et retourner une instance de connecté `ConnectionMultiplexer`, hello appel statique `Connect` (méthode) et passez hello cache point de terminaison et la clé.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="2b3d7-153">Utiliser la clé hello généré à partir de hello portail Azure en tant que paramètre de mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="2b3d7-154">Avertissement : ne stockez jamais d’informations d’identification dans du code source.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="2b3d7-155">tookeep ce simple exemple, je suis leur affichage dans le code source de hello.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="2b3d7-156">Consultez [comment les chaînes d’Application et de travail des chaînes de connexion] [ How Application Strings and Connection Strings Work] pour plus d’informations sur la façon des informations d’identification de toostore.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="2b3d7-157">Si vous ne souhaitez pas toouse SSL, soit définir `ssl=false` ou omettez hello `ssl` paramètre.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="2b3d7-158">port non-SSL de Hello est désactivé par défaut pour les nouveaux caches.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="2b3d7-159">Pour obtenir des instructions sur l’activation du port de hello non-SSL, consultez [Ports d’accès](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="2b3d7-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="2b3d7-160">Une approche toosharing un `ConnectionMultiplexer` instance dans votre application est toohave une propriété statique qui retourne une instance connectée, toohello similaire, l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="2b3d7-161">Cette approche fournit un tooinitialize de façon thread-safe qu’un seul connecté `ConnectionMultiplexer` instance.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="2b3d7-162">Dans ces exemples `abortConnect` est toofalse ensemble, ce qui signifie que les appels hello réussit même si un toohello de connexions du Cache Redis Azure n’est pas établie.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="2b3d7-163">Une fonction clé `ConnectionMultiplexer` est qu’elle restaure automatiquement du cache de connectivité toohello une fois le problème de réseau hello ou d’autres causes sont résolus.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="2b3d7-164">Pour plus d'informations sur les options avancées de configuration de connexion, consultez la rubrique [Modèle de configuration StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="2b3d7-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="2b3d7-165">Une fois que hello est établie, retourner une base de données de référence toohello redis cache en appelant hello `ConnectionMultiplexer.GetDatabase` (méthode).</span><span class="sxs-lookup"><span data-stu-id="2b3d7-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="2b3d7-166">objet de Hello retourné par hello `GetDatabase` méthode est un objet léger transmis directement et n’a pas besoin toobe stockée.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="2b3d7-167">Les caches Redis Azure ont un nombre configurable de bases de données (valeur par défaut de 16) qui peuvent être toologically utilisé hello distincte des données dans un cache Redis.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="2b3d7-168">Pour plus d’informations, consultez les sections [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Que sont les bases de données Redis ?) et [Configuration du serveur Redis par défaut](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="2b3d7-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="2b3d7-169">Maintenant que vous savez comment instance de Cache Redis Azure tooconnect tooan et retournent un toohello de référence du cache de base de données, examinons fonctionne avec le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="2b3d7-170">Ajouter et récupérer des objets à partir du cache de hello</span><span class="sxs-lookup"><span data-stu-id="2b3d7-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="2b3d7-171">Éléments peuvent être stockés dans et récupérés à partir d’un cache à l’aide de hello `StringSet` et `StringGet` méthodes.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="2b3d7-172">Redis stocke la plupart des données en tant que chaînes de Redis, mais ces chaînes peuvent contenir de nombreux types de données, y compris les données binaires sérialisées, ce qui peuvent être utilisées lorsque le stockage .NET des objets dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="2b3d7-173">Lors de l’appel `StringGet`, si l’objet de hello existe, elle est retournée, et si elle n’est pas le cas `null` est retourné.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="2b3d7-174">Si `null` est retourné, vous pouvez récupérer la valeur de hello à partir de la source de données souhaitée hello et stockez-le dans le cache de hello pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="2b3d7-175">Ce modèle d’utilisation est connu en tant que modèle de type cache-aside hello.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="2b3d7-176">Vous pouvez également utiliser `RedisValue`, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="2b3d7-177">`RedisValue` a des opérateurs implicites pour l’utilisation des types de données intégraux et peut être utile si `null` est une valeur attendue pour un élément mis en cache.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="2b3d7-178">expiration de hello toospecify d’un élément dans le cache de hello, utilisez hello `TimeSpan` paramètre de `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="2b3d7-179">Utiliser des objets .NET dans le cache de hello</span><span class="sxs-lookup"><span data-stu-id="2b3d7-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="2b3d7-180">Cache Redis Azure peut mettre en cache des objets .NET et des types de données primitifs, mais avant qu’un objet .NET puisse être mis en cache, il doit être sérialisé.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="2b3d7-181">Cette sérialisation des objets .NET hello incombe développeur de l’application hello et hello developer permet choix hello du sérialiseur de hello.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="2b3d7-182">Un moyen simple tooserialize des objets toouse hello `JsonConvert` méthodes de sérialisation dans [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) et sérialiser tooand à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="2b3d7-183">Hello exemple suivant montre un get et set utilise une `Employee` instance d’objet.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="2b3d7-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2b3d7-184">Next Steps</span></span>
<span data-ttu-id="2b3d7-185">Maintenant que vous avez appris les notions de base de hello, suivez ces liens de toolearn plus d’informations sur le Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="2b3d7-186">Consultez les fournisseurs ASP.NET pour le Cache Redis Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="2b3d7-187">Fournisseur de l'état de session Redis Azure</span><span class="sxs-lookup"><span data-stu-id="2b3d7-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="2b3d7-188">Fournisseur de caches de sortie ASP.NET du Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="2b3d7-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="2b3d7-189">[Activer les diagnostics de cache](cache-how-to-monitor.md#enable-cache-diagnostics) afin de pouvoir [moniteur](cache-how-to-monitor.md) hello d’intégrité de votre cache.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="2b3d7-190">Vous pouvez afficher hello dans hello portail Azure et vous peuvent également [Téléchargez et lisez](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) les à l’aide des outils hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="2b3d7-191">Extraire hello [documentation du client de cache StackExchange.Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="2b3d7-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="2b3d7-192">Le Cache Redis Azure est accessible depuis de nombreux clients Redis et langages de développement.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="2b3d7-193">Pour plus d’informations, voir [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="2b3d7-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="2b3d7-194">Le Cache Redis Azure est également utilisable avec des services et outils tiers tels que Redsmin et Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="2b3d7-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="2b3d7-195">Pour plus d’informations sur Redsmin, consultez [comment tooretrieve une connexion Redis Azure de chaîne et l’utiliser avec Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="2b3d7-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="2b3d7-196">Accédez à vos données et inspectez-les dans le Cache Redis Azure avec une interface graphique utilisateur à l’aide de [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="2b3d7-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="2b3d7-197">Consultez hello [redis] [ redis] documentation et en savoir plus sur [redis des types de données] [ redis data types] et [une présentation de 15 minutes types de données tooRedis][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="2b3d7-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


