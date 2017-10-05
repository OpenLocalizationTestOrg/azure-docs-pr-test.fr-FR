---
title: Utilisation du Cache Redis Azure | Microsoft Docs
description: "Découvrez comment améliorer les performances de vos applications Azure grâce au Cache Redis Azure"
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
ms.openlocfilehash: 3dfc026490093523446650c510dbebdd660e8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-redis-cache"></a><span data-ttu-id="1223e-103">Utilisation du Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="1223e-103">How to Use Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1223e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1223e-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="1223e-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1223e-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="1223e-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="1223e-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="1223e-107">Java</span><span class="sxs-lookup"><span data-stu-id="1223e-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="1223e-108">Python</span><span class="sxs-lookup"><span data-stu-id="1223e-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="1223e-109">Ce guide décrit la prise en main du **Cache Redis Azure**.</span><span class="sxs-lookup"><span data-stu-id="1223e-109">This guide shows you how to get started using **Azure Redis Cache**.</span></span> <span data-ttu-id="1223e-110">Le Cache Microsoft Azure Redis se base sur le cache Redis open source connu.</span><span class="sxs-lookup"><span data-stu-id="1223e-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span></span> <span data-ttu-id="1223e-111">Il vous donne accès à un cache Redis dédié et sécurisé, qui est géré par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1223e-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="1223e-112">Un cache créé avec Cache Redis Azure est accessible à partir de toutes les applications dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1223e-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="1223e-113">Cache Redis Microsoft Azure est disponible dans les niveaux suivants :</span><span class="sxs-lookup"><span data-stu-id="1223e-113">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="1223e-114">**De base** , avec un seul nœud.</span><span class="sxs-lookup"><span data-stu-id="1223e-114">**Basic** – Single node.</span></span> <span data-ttu-id="1223e-115">Plusieurs tailles jusqu'à 53 Go.</span><span class="sxs-lookup"><span data-stu-id="1223e-115">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="1223e-116">**Standard** : avec deux nœuds, principal et réplica.</span><span class="sxs-lookup"><span data-stu-id="1223e-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="1223e-117">Plusieurs tailles jusqu'à 53 Go.</span><span class="sxs-lookup"><span data-stu-id="1223e-117">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="1223e-118">Un contrat SLA de 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="1223e-118">99.9% SLA.</span></span>
* <span data-ttu-id="1223e-119">**Premium** - Deux nœuds (principal / réplica) contenant jusqu’à 10 partitions.</span><span class="sxs-lookup"><span data-stu-id="1223e-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="1223e-120">Plusieurs tailles de 6 Go à 530 Go.</span><span class="sxs-lookup"><span data-stu-id="1223e-120">Multiple sizes from 6 GB to 530 GB.</span></span> <span data-ttu-id="1223e-121">Toutes les fonctionnalités du niveau Standard et d’autres, y compris la prise en charge du [cluster Redis](cache-how-to-premium-clustering.md), la [persistance Redis](cache-how-to-premium-persistence.md) et le [réseau virtuel Azure](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="1223e-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="1223e-122">Un contrat SLA de 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="1223e-122">99.9% SLA.</span></span>

<span data-ttu-id="1223e-123">Chaque option diffère en termes de fonctionnalités et de tarification.</span><span class="sxs-lookup"><span data-stu-id="1223e-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="1223e-124">Pour plus d’informations sur la tarification, consultez la rubrique [Détails de tarification Cache][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="1223e-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="1223e-125">Ce guide vous montre comment utiliser le client [StackExchange.Redis][StackExchange.Redis] à l’aide du code C\#.</span><span class="sxs-lookup"><span data-stu-id="1223e-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="1223e-126">Les scénarios couverts incluent **la création et la configuration d’un cache**, **la configuration des clients de cache** et **l’ajout et la suppression d’objets dans le cache**.</span><span class="sxs-lookup"><span data-stu-id="1223e-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span></span> <span data-ttu-id="1223e-127">Pour plus d’informations sur l’utilisation du Cache Redis Azure, consultez [Étapes suivantes][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="1223e-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="1223e-128">Pour obtenir un didacticiel pas à pas dédié à la création d’une application web ASP.NET MVC avec le Cache Redis, consultez [Création d’une application web avec le Cache Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="1223e-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="1223e-129">Prise en main de Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="1223e-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="1223e-130">La prise en main de Cache Redis Azure est aisée.</span><span class="sxs-lookup"><span data-stu-id="1223e-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="1223e-131">Pour commencer, vous mettez en service et configurez un cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-131">To get started, you provision and configure a cache.</span></span> <span data-ttu-id="1223e-132">Ensuite, vous configurez les clients du cache pour qu'ils puissent accéder au cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-132">Next, you configure the cache clients so they can access the cache.</span></span> <span data-ttu-id="1223e-133">Une fois les clients du cache configurés, vous pouvez commencer à les utiliser.</span><span class="sxs-lookup"><span data-stu-id="1223e-133">Once the cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="1223e-134">[Création du cache][Create the cache]</span><span class="sxs-lookup"><span data-stu-id="1223e-134">[Create the cache][Create the cache]</span></span>
* <span data-ttu-id="1223e-135">[Configuration des clients de cache][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="1223e-135">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="1223e-136">Création d'un cache</span><span class="sxs-lookup"><span data-stu-id="1223e-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="to-access-your-cache-after-its-created"></a><span data-ttu-id="1223e-137">Pour accéder à votre cache après sa création</span><span class="sxs-lookup"><span data-stu-id="1223e-137">To access your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="1223e-138">Pour plus d’informations sur la configuration de votre cache, voir [Configuration de Cache Redis Azure](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1223e-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="1223e-139">Configuration des clients de cache</span><span class="sxs-lookup"><span data-stu-id="1223e-139">Configure the cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="1223e-140">Une fois que votre projet client est configuré pour la mise en cache, vous pouvez utiliser les techniques décrites dans les sections suivantes pour utiliser votre cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="1223e-141">Utilisation des caches</span><span class="sxs-lookup"><span data-stu-id="1223e-141">Working with Caches</span></span>
<span data-ttu-id="1223e-142">Cette section décrit l'exécution des tâches courantes avec Cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-142">The steps in this section describe how to perform common tasks with Cache.</span></span>

* <span data-ttu-id="1223e-143">[Connexion au cache][Connect to the cache]</span><span class="sxs-lookup"><span data-stu-id="1223e-143">[Connect to the cache][Connect to the cache]</span></span>
* <span data-ttu-id="1223e-144">[Ajout et récupération d’objets dans le cache][Add and retrieve objects from the cache]</span><span class="sxs-lookup"><span data-stu-id="1223e-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span></span>
* [<span data-ttu-id="1223e-145">Utilisation des objets .NET dans le cache</span><span class="sxs-lookup"><span data-stu-id="1223e-145">Work with .NET objects in the cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-to-the-cache"></a><span data-ttu-id="1223e-146">Connexion au cache</span><span class="sxs-lookup"><span data-stu-id="1223e-146">Connect to the cache</span></span>
<span data-ttu-id="1223e-147">Pour utiliser un cache par programmation, vous avez besoin d’une référence au cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-147">To programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="1223e-148">Ajoutez ce qui suit au début des fichiers qui doivent utiliser le client StackExchange.Redis pour accéder à un cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="1223e-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="1223e-149">Le client StackExchange.Redis a besoin de .NET Framework 4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1223e-149">The StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="1223e-150">La connexion au Cache Redis Azure est gérée par la classe `ConnectionMultiplexer` .</span><span class="sxs-lookup"><span data-stu-id="1223e-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="1223e-151">Cette classe doit être partagée et réutilisée dans toute votre application cliente et ne doit pas être créée pour chaque opération.</span><span class="sxs-lookup"><span data-stu-id="1223e-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span></span> 

<span data-ttu-id="1223e-152">Pour vous connecter au Cache Redis Azure et recevoir en retour une instance `ConnectionMultiplexer` connectée, appelez la méthode statique `Connect`, puis passez le point de terminaison et la clé du cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span></span> <span data-ttu-id="1223e-153">Utilisez la clé Azure générée sur le portail Azure comme paramètre du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1223e-153">Use the key generated from the Azure portal as the password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="1223e-154">Avertissement : ne stockez jamais d’informations d’identification dans du code source.</span><span class="sxs-lookup"><span data-stu-id="1223e-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="1223e-155">Pour ne pas alourdir cet exemple, elles sont montrées dans le code source.</span><span class="sxs-lookup"><span data-stu-id="1223e-155">To keep this sample simple, I’m showing them in the source code.</span></span> <span data-ttu-id="1223e-156">Consultez [Fonctionnement des chaînes d’application et de connexion][How Application Strings and Connection Strings Work] pour plus d’informations sur le stockage des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="1223e-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how to store credentials.</span></span>
> 
> 

<span data-ttu-id="1223e-157">Si vous ne souhaitez pas utiliser SSL, configurez `ssl=false` ou omettez le paramètre `ssl`.</span><span class="sxs-lookup"><span data-stu-id="1223e-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="1223e-158">Le port non SSL est désactivé par défaut pour les nouveaux caches.</span><span class="sxs-lookup"><span data-stu-id="1223e-158">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="1223e-159">Pour obtenir des instructions sur l’activation du port non-SSL, consultez [Ports d’accès](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="1223e-159">For instructions on enabling the non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="1223e-160">Pour partager une instance `ConnectionMultiplexer` dans votre application, vous pouvez utiliser une propriété statique qui renvoie une instance connectée, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1223e-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="1223e-161">Cette approche fournit une méthode thread-safe permettant d’initialiser une seule instance `ConnectionMultiplexer` connectée.</span><span class="sxs-lookup"><span data-stu-id="1223e-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="1223e-162">Dans ces exemples, `abortConnect` est défini sur false, ce qui signifie que l’appel réussit même si aucune connexion au Cache Redis Azure n’est établie.</span><span class="sxs-lookup"><span data-stu-id="1223e-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="1223e-163">Une fonctionnalité clé de `ConnectionMultiplexer` est qu’il restaure automatiquement la connectivité au cache une fois que le problème réseau ou d’autres causes sont résolus.</span><span class="sxs-lookup"><span data-stu-id="1223e-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="1223e-164">Pour plus d'informations sur les options avancées de configuration de connexion, consultez la rubrique [Modèle de configuration StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="1223e-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="1223e-165">Une fois la connexion établie, renvoyez une référence à la base de données du Cache Redis en appelant la méthode `ConnectionMultiplexer.GetDatabase` .</span><span class="sxs-lookup"><span data-stu-id="1223e-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="1223e-166">L’objet renvoyé à partir de la méthode `GetDatabase` est un objet direct léger qui n’a pas besoin d’être stocké.</span><span class="sxs-lookup"><span data-stu-id="1223e-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

    // Connection refers to a property that returns a ConnectionMultiplexer
    // as shown in the previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using the cache object...
    // Simple put of integral data types into the cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from the cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="1223e-167">Les caches Redis Azure disposent d’un nombre configurable de bases de données (16 par défaut) pouvant être utilisées pour séparer de manière logique les données dans un cache Redis.</span><span class="sxs-lookup"><span data-stu-id="1223e-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span></span> <span data-ttu-id="1223e-168">Pour plus d’informations, consultez les sections [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Que sont les bases de données Redis ?) et [Configuration du serveur Redis par défaut](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="1223e-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="1223e-169">Maintenant que vous savez vous connecter à une instance Cache Redis Azure et renvoyer une référence à la base de données du cache, regardons comment utiliser le cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-the-cache"></a><span data-ttu-id="1223e-170">Ajout et récupération d’objets dans le cache</span><span class="sxs-lookup"><span data-stu-id="1223e-170">Add and retrieve objects from the cache</span></span>
<span data-ttu-id="1223e-171">Les objets peuvent être stockés dans le cache et en être extraits en utilisant les méthodes `StringSet` et `StringGet`.</span><span class="sxs-lookup"><span data-stu-id="1223e-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="1223e-172">Redis stocke la plupart des données sous la forme de chaînes Redis, mais ces chaînes peuvent contenir de nombreux types de données, notamment des données binaires sérialisées, qui peuvent être utilisées lors du stockage d'objets .NET dans le cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="1223e-173">Lors de l’appel de `StringGet`, si l’objet existe, il est renvoyé ; sinon, `null` est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="1223e-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="1223e-174">Si `null` est renvoyé, vous pouvez extraire la valeur de la source de données de votre choix et la stocker dans le cache pour un usage ultérieur.</span><span class="sxs-lookup"><span data-stu-id="1223e-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="1223e-175">Ce modèle d’utilisation est appelé modèle de type cache-aside.</span><span class="sxs-lookup"><span data-stu-id="1223e-175">This usage pattern is known as the cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // The item keyed by "key1" is not in the cache. Obtain
        // it from the desired data source and add it to the cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="1223e-176">Vous pouvez également utiliser `RedisValue`, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="1223e-176">You can also use `RedisValue`, as shown in the following example.</span></span> <span data-ttu-id="1223e-177">`RedisValue` a des opérateurs implicites pour l’utilisation des types de données intégraux et peut être utile si `null` est une valeur attendue pour un élément mis en cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="1223e-178">Pour spécifier l’expiration d’un élément du cache, utilisez le paramètre `TimeSpan` de `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="1223e-178">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="1223e-179">Utilisation des objets .NET dans le cache</span><span class="sxs-lookup"><span data-stu-id="1223e-179">Work with .NET objects in the cache</span></span>
<span data-ttu-id="1223e-180">Cache Redis Azure peut mettre en cache des objets .NET et des types de données primitifs, mais avant qu’un objet .NET puisse être mis en cache, il doit être sérialisé.</span><span class="sxs-lookup"><span data-stu-id="1223e-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="1223e-181">La sérialisation d’objet .NET échoit au développeur d’applications, qui a toute latitude pour choisir le sérialiseur.</span><span class="sxs-lookup"><span data-stu-id="1223e-181">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="1223e-182">Une méthode simple pour sérialiser des objets consiste à utiliser les méthodes de sérialisation `JsonConvert` dans [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) et à sérialiser vers et à partir de JSON.</span><span class="sxs-lookup"><span data-stu-id="1223e-182">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span></span> <span data-ttu-id="1223e-183">L’exemple suivant montre des méthodes get et set utilisant une instance d’objet `Employee` .</span><span class="sxs-lookup"><span data-stu-id="1223e-183">The following example shows a get and set using an `Employee` object instance.</span></span>

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

    // Store to cache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="1223e-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1223e-184">Next Steps</span></span>
<span data-ttu-id="1223e-185">Maintenant que vous connaissez les bases, consultez les liens suivants pour en savoir plus sur le Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="1223e-185">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="1223e-186">Découvrez les fournisseurs ASP.NET pour le Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="1223e-186">Check out the ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="1223e-187">Fournisseur de l'état de session Redis Azure</span><span class="sxs-lookup"><span data-stu-id="1223e-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="1223e-188">Fournisseur de caches de sortie ASP.NET du Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="1223e-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="1223e-189">[Activez les diagnostics du cache](cache-how-to-monitor.md#enable-cache-diagnostics) afin de pouvoir [surveiller](cache-how-to-monitor.md) l’intégrité de votre cache.</span><span class="sxs-lookup"><span data-stu-id="1223e-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span> <span data-ttu-id="1223e-190">Vous pouvez afficher les mesures dans le portail Azure, et [les télécharger et les analyser](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) à l’aide des outils de votre choix.</span><span class="sxs-lookup"><span data-stu-id="1223e-190">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span></span>
* <span data-ttu-id="1223e-191">Consultez la [Documentation du client du cache StackExchange.Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="1223e-191">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="1223e-192">Le Cache Redis Azure est accessible depuis de nombreux clients Redis et langages de développement.</span><span class="sxs-lookup"><span data-stu-id="1223e-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="1223e-193">Pour plus d’informations, voir [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="1223e-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="1223e-194">Le Cache Redis Azure est également utilisable avec des services et outils tiers tels que Redsmin et Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="1223e-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="1223e-195">Pour plus d’informations, consultez la [page expliquant comment récupérer une chaîne de connexion Redis Azure pour l’utiliser avec Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="1223e-195">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="1223e-196">Accédez à vos données et inspectez-les dans le Cache Redis Azure avec une interface graphique utilisateur à l’aide de [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="1223e-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="1223e-197">Consultez la documentation [redis][redis] et notamment les [types de données Redis][redis data types] et [quinze minutes de présentation des types de données Redis][a fifteen minute introduction to Redis data types].</span><span class="sxs-lookup"><span data-stu-id="1223e-197">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction to Azure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project to Use Azure Caching]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create the cache]: #create-cache
[Configure the cache]: #enable-caching
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect to the cache]: #connect-to-cache
[Add and retrieve objects from the cache]: #add-object
[Specify the expiration of an object in the cache]: #specify-expiration
[Store ASP.NET session state in the cache]: #store-session


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
[How to retrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in the cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate to Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups to manage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction to Redis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


