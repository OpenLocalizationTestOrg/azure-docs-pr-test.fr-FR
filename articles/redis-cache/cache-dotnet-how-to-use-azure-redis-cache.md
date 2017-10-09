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
# <a name="how-toouse-azure-redis-cache"></a>Comment tooUse Cache Redis Azure
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.JS](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Ce guide vous explique comment tooget main **Cache Redis Azure**. Le Cache Redis Microsoft Azure est basé sur hello open source populaires du Cache Redis. Elle vous donne accès tooa sécurisé Redis cache dédié, géré par Microsoft. Un cache créé avec Cache Redis Azure est accessible à partir de toutes les applications dans Microsoft Azure.

Le Cache Redis Microsoft Azure est disponible dans hello suivant niveaux :

* **De base** , avec un seul nœud. Plusieurs tailles de too53 go.
* **Standard** : avec deux nœuds, principal et réplica. Plusieurs tailles de too53 go. Un contrat SLA de 99,9 %.
* **Premium** – deux nœuds principal/réplica avec les partitions de too10. Tailles multiples de 6 Go too530 go. Toutes les fonctionnalités du niveau Standard et d’autres, y compris la prise en charge du [cluster Redis](cache-how-to-premium-clustering.md), la [persistance Redis](cache-how-to-premium-persistence.md) et le [réseau virtuel Azure](cache-how-to-premium-vnet.md). Un contrat SLA de 99,9 %.

Chaque option diffère en termes de fonctionnalités et de tarification. Pour plus d’informations sur la tarification, consultez la rubrique [Détails de tarification Cache][Cache Pricing Details].

Ce guide vous montre comment toouse hello [StackExchange.Redis] [ StackExchange.Redis] client à l’aide de C\# code. Hello scénarios abordés incluent **création et configuration d’un cache**, **configuration des clients de cache**, et **Ajout et suppression d’objets du cache de hello**. Pour plus d’informations sur l’utilisation du Cache Redis Azure, consultez [Étapes suivantes][Next Steps]. Pour obtenir un didacticiel de création d’application web avec le Cache Redis un ASP.NET MVC, consultez [comment toocreate une application Web avec le Cache Redis](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Prise en main de Cache Redis Azure
La prise en main de Cache Redis Azure est aisée. tooget démarré, vous approvisionner et configurer un cache. Ensuite, vous configurez les clients de cache hello afin de pouvoir accéder à cache de hello. Une fois que les clients de cache hello sont configurés, vous pouvez commencer leur utilisation.

* [Créer le cache de hello][Create hello cache]
* [Configurer les clients de cache hello][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Création d'un cache
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess votre cache après qu’il est créé.
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Pour plus d’informations sur la configuration de votre cache, consultez [comment tooconfigure le Cache Redis Azure](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Configurer les clients de cache hello
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

Une fois votre projet client est configuré pour la mise en cache, vous pouvez utiliser les techniques de hello décrites Bonjour les sections pour travailler avec votre cache suivantes.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Utilisation des caches
étapes de Hello dans cette section décrivent des tâches de tooperform commun avec le Cache.

* [Se connecter toohello cache][Connect toohello cache]
* [Ajouter et récupérer des objets à partir du cache de hello][Add and retrieve objects from hello cache]
* [Utiliser des objets .NET dans le cache de hello](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Se connecter toohello cache
travail de tooprogrammatically avec un cache, vous avez besoin d’un cache de toohello de référence. Ajoutez hello suivant haut toohello de tous les fichiers à partir de laquelle vous souhaitez toouse hello StackExchange.Redis client tooaccess un cache Azure Redis Cache.

    using StackExchange.Redis;

> [!NOTE]
> client de Hello StackExchange.Redis nécessite .NET Framework 4 ou version ultérieure.
> 
> 

Hello toohello connexion Cache Redis Azure est géré par hello `ConnectionMultiplexer` classe. Cette classe doit être partagée réutilisée dans votre application cliente et n’a pas besoin toobe créé sur chaque opération. 

tooconnect tooan Cache Redis Azure et retourner une instance de connecté `ConnectionMultiplexer`, hello appel statique `Connect` (méthode) et passez hello cache point de terminaison et la clé. Utiliser la clé hello généré à partir de hello portail Azure en tant que paramètre de mot de passe hello.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Avertissement : ne stockez jamais d’informations d’identification dans du code source. tookeep ce simple exemple, je suis leur affichage dans le code source de hello. Consultez [comment les chaînes d’Application et de travail des chaînes de connexion] [ How Application Strings and Connection Strings Work] pour plus d’informations sur la façon des informations d’identification de toostore.
> 
> 

Si vous ne souhaitez pas toouse SSL, soit définir `ssl=false` ou omettez hello `ssl` paramètre.

> [!NOTE]
> port non-SSL de Hello est désactivé par défaut pour les nouveaux caches. Pour obtenir des instructions sur l’activation du port de hello non-SSL, consultez [Ports d’accès](cache-configure.md#access-ports).
> 
> 

Une approche toosharing un `ConnectionMultiplexer` instance dans votre application est toohave une propriété statique qui retourne une instance connectée, toohello similaire, l’exemple suivant. Cette approche fournit un tooinitialize de façon thread-safe qu’un seul connecté `ConnectionMultiplexer` instance. Dans ces exemples `abortConnect` est toofalse ensemble, ce qui signifie que les appels hello réussit même si un toohello de connexions du Cache Redis Azure n’est pas établie. Une fonction clé `ConnectionMultiplexer` est qu’elle restaure automatiquement du cache de connectivité toohello une fois le problème de réseau hello ou d’autres causes sont résolus.

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

Pour plus d'informations sur les options avancées de configuration de connexion, consultez la rubrique [Modèle de configuration StackExchange.Redis][StackExchange.Redis configuration model].

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

Une fois que hello est établie, retourner une base de données de référence toohello redis cache en appelant hello `ConnectionMultiplexer.GetDatabase` (méthode). objet de Hello retourné par hello `GetDatabase` méthode est un objet léger transmis directement et n’a pas besoin toobe stockée.

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

Les caches Redis Azure ont un nombre configurable de bases de données (valeur par défaut de 16) qui peuvent être toologically utilisé hello distincte des données dans un cache Redis. Pour plus d’informations, consultez les sections [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Que sont les bases de données Redis ?) et [Configuration du serveur Redis par défaut](cache-configure.md#default-redis-server-configuration).

Maintenant que vous savez comment instance de Cache Redis Azure tooconnect tooan et retournent un toohello de référence du cache de base de données, examinons fonctionne avec le cache de hello.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Ajouter et récupérer des objets à partir du cache de hello
Éléments peuvent être stockés dans et récupérés à partir d’un cache à l’aide de hello `StringSet` et `StringGet` méthodes.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

Redis stocke la plupart des données en tant que chaînes de Redis, mais ces chaînes peuvent contenir de nombreux types de données, y compris les données binaires sérialisées, ce qui peuvent être utilisées lorsque le stockage .NET des objets dans le cache de hello.

Lors de l’appel `StringGet`, si l’objet de hello existe, elle est retournée, et si elle n’est pas le cas `null` est retourné. Si `null` est retourné, vous pouvez récupérer la valeur de hello à partir de la source de données souhaitée hello et stockez-le dans le cache de hello pour une utilisation ultérieure. Ce modèle d’utilisation est connu en tant que modèle de type cache-aside hello.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

Vous pouvez également utiliser `RedisValue`, comme indiqué dans hello l’exemple suivant. `RedisValue` a des opérateurs implicites pour l’utilisation des types de données intégraux et peut être utile si `null` est une valeur attendue pour un élément mis en cache.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


expiration de hello toospecify d’un élément dans le cache de hello, utilisez hello `TimeSpan` paramètre de `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Utiliser des objets .NET dans le cache de hello
Cache Redis Azure peut mettre en cache des objets .NET et des types de données primitifs, mais avant qu’un objet .NET puisse être mis en cache, il doit être sérialisé. Cette sérialisation des objets .NET hello incombe développeur de l’application hello et hello developer permet choix hello du sérialiseur de hello.

Un moyen simple tooserialize des objets toouse hello `JsonConvert` méthodes de sérialisation dans [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) et sérialiser tooand à partir de JSON. Hello exemple suivant montre un get et set utilise une `Employee` instance d’objet.

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

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello, suivez ces liens de toolearn plus d’informations sur le Cache Redis Azure.

* Consultez les fournisseurs ASP.NET pour le Cache Redis Azure hello.
  * [Fournisseur de l'état de session Redis Azure](cache-aspnet-session-state-provider.md)
  * [Fournisseur de caches de sortie ASP.NET du Cache Redis Azure](cache-aspnet-output-cache-provider.md)
* [Activer les diagnostics de cache](cache-how-to-monitor.md#enable-cache-diagnostics) afin de pouvoir [moniteur](cache-how-to-monitor.md) hello d’intégrité de votre cache. Vous pouvez afficher hello dans hello portail Azure et vous peuvent également [Téléchargez et lisez](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) les à l’aide des outils hello de votre choix.
* Extraire hello [documentation du client de cache StackExchange.Redis][StackExchange.Redis cache client documentation].
  * Le Cache Redis Azure est accessible depuis de nombreux clients Redis et langages de développement. Pour plus d’informations, voir [http://redis.io/clients][http://redis.io/clients].
* Le Cache Redis Azure est également utilisable avec des services et outils tiers tels que Redsmin et Redis Desktop Manager.
  * Pour plus d’informations sur Redsmin, consultez [comment tooretrieve une connexion Redis Azure de chaîne et l’utiliser avec Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Accédez à vos données et inspectez-les dans le Cache Redis Azure avec une interface graphique utilisateur à l’aide de [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).
* Consultez hello [redis] [ redis] documentation et en savoir plus sur [redis des types de données] [ redis data types] et [une présentation de 15 minutes types de données tooRedis][a fifteen minute introduction tooRedis data types].

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


