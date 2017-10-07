---
title: "aaaMigrate tooRedis applications de Service de Cache géré - Azure | Documents Microsoft"
description: "Découvrez comment les applications de Service de Cache géré et In-Role Cache toomigrate tooAzure Cache Redis"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>Migrer à partir du Service de Cache géré tooAzure Cache Redis
Migration de vos applications qui utilisent le Service de Cache géré Azure tooAzure Cache Redis peut être accomplie à l’application de tooyour des modifications minimes, selon les fonctionnalités du Service de Cache géré hello utilisées par votre application de mise en cache. Alors que hello API ne sont pas exactement hello même, ils sont similaires, et une grande partie de votre code existant qui utilise le Service de Cache géré tooaccess un cache peut être réutilisée avec des modifications minimes. Cette rubrique montre comment application et configuration requise de toomake hello change toomigrate votre toouse d’applications de Service de Cache géré Azure Redis Cache et montre comment certaines des fonctionnalités de hello de Cache Redis Azure peuvent être utilisés tooimplement hello fonctionnalités d’un cache de Service de Cache géré.

>[!NOTE]
>Le service de cache géré et le In-Role Cache ont été [supprimés](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) le 30 novembre 2016. Si vous disposez de tous les déploiements de Cache dans le rôle que vous souhaitez toomigrate tooAzure Cache Redis, vous pouvez suivre les étapes de hello dans cet article.

## <a name="migration-steps"></a>Étapes de la migration
Hello suit est requis toomigrate un toouse d’application de Service de Cache géré Azure Redis Cache.

* Mapper les fonctionnalités de Service de Cache géré tooAzure Cache Redis
* Sélection d’une offre de cache
* Création d’un cache
* Configurer les Clients de Cache hello
  * Supprimer hello Configuration de Service de Cache géré
  * Configurer un client de cache à l’aide de hello NuGet Package StackExchange.Redis
* Migration du code du Service de cache géré
  * Connecter le cache de toohello à l’aide de la classe ConnectionMultiplexer de hello
  * Types de données primitifs d’accès dans le cache de hello
  * Utiliser des objets .NET dans le cache de hello
* Migrer l’état de Session ASP.NET et la sortie mise en cache tooAzure Cache Redis 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>Mapper les fonctionnalités de Service de Cache géré tooAzure Cache Redis
Bien que similaires, le Service de cache géré Azure et le Cache Redis Azure implémentent certaines de leurs fonctionnalités de différentes façons. Cette section décrit quelques-unes des différences de hello et fournit des conseils sur l’implémentation des fonctionnalités de hello du Service de Cache géré dans le Cache Redis Azure.

| Fonctionnalité du Service de cache géré | Prise en charge du Service de cache géré | Prise en charge du Cache Redis Azure |
| --- | --- | --- |
| Caches nommés |Un cache par défaut est configuré et Bonjour Standard et Premium offres de cache, les toonine supplémentaire cache nommés peuvent être configurés si vous le souhaitez. |Les caches Redis Azure ont un nombre configurable de bases de données (valeur par défaut de 16) qui peuvent être utilisé tooimplement un toonamed de fonctionnalités similaires met en cache. Pour plus d’informations, consultez les sections [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Que sont les bases de données Redis ?) et [Configuration du serveur Redis par défaut](cache-configure.md#default-redis-server-configuration). |
| Haute disponibilité |Fournit une haute disponibilité pour les éléments dans le cache dans les offres de cache Standard et Premium hello hello. Si les éléments sont perdues en raison de l’échec de tooa, les copies de sauvegarde des éléments hello dans le cache de hello sont toujours disponibles. Écrit le cache secondaire de toohello sont effectuées de façon synchrone. |Haute disponibilité est disponible dans hello Standard et Premium offres de cache, qui ont une configuration de principal/réplica à deux nœuds (chaque partition dans un cache Premium a une paire principal/réplica). Écritures toohello réplica sont effectuées de façon asynchrone. Pour plus d’informations, consultez [Tarification - Cache Redis Azure](https://azure.microsoft.com/pricing/details/cache/). |
| Notifications |Autorise les clients tooreceive recevoir des notifications asynchrones lorsque diverses opérations de cache surviennent sur un cache nommé. |Applications clientes peuvent utiliser Redis pub/sub ou [notifications d’espace de clés](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve une toonotifications de fonctionnalités similaires. |
| Cache local |Stocke une copie des objets mis en cache localement sur le client hello pour un accès très rapide. |Les applications clientes doivent tooimplement cette fonctionnalité à l’aide d’un dictionnaire ou une structure de données similaire. |
| Stratégie d’éviction |Aucune ou LRU. stratégie par défaut de Hello est LRU. |Cache Redis Azure prend en charge hello suivant des stratégies d’éviction : volatile-lru, allkeys-lru, volatile aléatoire, aléatoire allkeys-volatile-durée de vie, noeviction. stratégie par défaut de Hello est volatile-lru. Pour plus d’informations, consultez la section [Configuration du serveur Redis par défaut](cache-configure.md#default-redis-server-configuration). |
| Stratégie d’expiration |stratégie d’expiration par défaut des Hello est absolue et intervalle d’expiration hello par défaut est de dix minutes. Les stratégies « Fenêtre coulissante » et « Jamais » sont également disponibles. |Par défaut des éléments dans le cache de hello n’expirent pas, mais un délai d’expiration peut être configuré sur une base par écriture à l’aide de surcharges d’ensemble de cache. Pour plus d’informations, consultez [ajouter et récupérer des objets à partir du cache de hello](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache). |
| Régions et balisage |Les régions sont des sous-groupes d’éléments mis en cache. Régions prennent également en charge l’annotation hello des éléments mis en cache avec les chaînes descriptives supplémentaires appelées « balises ». Régions prennent en charge les opérations de recherche hello capacité tooperform sur n’importe quel élément balisé dans cette région. Tous les éléments dans une région sont situés dans un seul nœud du cluster de cache hello. |Un cache Redis se compose d’un seul nœud (sauf si le cluster Redis est activé) afin de concept hello des régions de Service de Cache géré ne s’applique pas. Redis prend en charge la recherche et les opérations génériques lors de la récupération de clés afin de balises descriptives peuvent être incorporés dans les noms de clés hello et utilisé des éléments tooretrieve hello plus tard. Pour obtenir un exemple d’implémentation d’une solution de balisage à l’aide de Redis, voir la page relative à l’ [implémentation de balisage de cache avec Redis](http://stackify.com/implementing-cache-tagging-redis/). |
| Sérialisation |Cache géré prend en charge NetDataContractSerializer, BinaryFormatter et utilisation de hello de sérialiseurs personnalisés. valeur par défaut Hello est NetDataContractSerializer. |Il incombe hello hello client tooserialize .NET des objets d’application avant de les placer dans le cache hello avec choix hello du sérialiseur hello de développeur d’applications client toohello. Pour plus d’informations et des exemples de code, consultez [travailler avec des objets .NET dans le cache de hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache). |
| Émulateur de cache |Le cache géré fournit un émulateur de cache local. |Cache Redis Azure n’a pas d’un émulateur, mais vous pouvez [exécuter localement de génération de MSOpenTech hello de redis-server.exe](cache-faq.md#cache-emulator) tooprovide une expérience d’émulateur. |

## <a name="choose-a-cache-offering"></a>Sélection d’une offre de cache
Le Cache Redis Microsoft Azure est disponible dans hello suivant niveaux :

* **De base** , avec un seul nœud. Plusieurs tailles de too53 go.
* **Standard** : avec deux nœuds, principal et réplica. Plusieurs tailles de too53 go. Un contrat SLA de 99,9 %.
* **Premium** – deux nœuds principal/réplica avec les partitions de too10. Tailles multiples de 6 Go too530 go. Toutes les fonctionnalités du niveau Standard et d’autres, y compris la prise en charge du [cluster Redis](cache-how-to-premium-clustering.md), la [persistance Redis](cache-how-to-premium-persistence.md) et le [réseau virtuel Azure](cache-how-to-premium-vnet.md). Un contrat SLA de 99,9 %.

Chaque option diffère en termes de fonctionnalités et de tarification. Hello fonctionnalités sont abordées plus loin dans ce guide et pour plus d’informations sur la tarification, consultez [détails de la tarification du Cache](https://azure.microsoft.com/pricing/details/cache/).

Un point de départ pour la migration est toopick hello taille qui correspond à la taille de hello de votre cache de Service de Cache géré précédente, puis augmenter ou diminuer en fonction des besoins hello de votre application. Pour plus d’informations sur le choix d’offre de Cache Redis Azure hello appropriée, consultez [offre de Cache Redis et de la taille dois-je utiliser ?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="create-a-cache"></a>Création d’un cache
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Configurer les Clients de Cache hello
Une fois que le cache de hello est créé et configuré, étape suivante de hello est la configuration de Service de Cache géré tooremove hello et ajouter hello ajouter la configuration du Cache Redis Azure hello et les références afin que les clients de cache peuvent accéder au cache de hello.

* Supprimer hello Configuration de Service de Cache géré
* Configurer un client de cache à l’aide de hello NuGet Package StackExchange.Redis

### <a name="remove-hello-managed-cache-service-configuration"></a>Supprimer hello Configuration de Service de Cache géré
Avant de hello les applications clientes peuvent être configurées pour Azure Redis Cache, configuration de Service de Cache géré existante hello et références d’assembly doivent être supprimées en désinstallant le package NuGet de Service de Cache géré de hello.

toouninstall hello package NuGet de Service de Cache géré avec le bouton droit de projet de client hello dans **l’Explorateur de solutions** et choisissez **gérer les Packages NuGet**. Sélectionnez hello **les packages installés** nœud et type W**indowsAzure.Caching** dans hello recherche installé, boîte de packages. Sélectionnez **Windows** **Azure Cache** (ou **Windows** **mise en cache Azure** selon la version de hello du package NuGet de hello), cliquez sur  **Désinstaller**, puis cliquez sur **fermer**.

![Désinstaller le package NuGet du Service de cache géré Azure](./media/cache-migrate-to-redis/IC757666.jpg)

Package de NuGet de Service de Cache géré hello désinstallation supprime les assemblys de Service de Cache géré hello et les entrées du Service de Cache géré hello dans hello app.config ou web.config de l’application cliente de hello. Étant donné que certains paramètres personnalisés ne peuvent pas être supprimés lors de la désinstallation du package NuGet de hello, ouvrez le fichier web.config ou app.config et assurez-vous que hello suivant d’éléments sont complètement supprimés.

Vérifiez que hello `dataCacheClients` est supprimée de hello `configSections` élément. Ne supprimez pas l’ensemble de hello `configSections` élément ; simplement supprimer hello `dataCacheClients` entrée, si elle est présente.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

Vérifiez que hello `dataCacheClients` section est supprimée. Hello `dataCacheClients` section sera similaire toohello l’exemple suivant.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

Une fois la configuration du Service de Cache géré hello est supprimée, vous pouvez configurer client de cache hello comme décrit dans hello suivant la section.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Configurer un client de cache à l’aide de hello NuGet Package StackExchange.Redis
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>Migration du code du Service de cache géré
API de Hello pour le client de cache StackExchange.Redis hello est similaire toohello Service de Cache géré. Cette section fournit une vue d’ensemble des différences de hello.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>Connecter le cache de toohello à l’aide de la classe ConnectionMultiplexer de hello
Dans le Service de Cache géré, cache toohello de connexions ont été traitées par hello `DataCacheFactory` et `DataCache` classes. Dans le Cache Redis Azure, ces connexions sont gérées par hello `ConnectionMultiplexer` classe.

Ajoutez hello qui suit à l’aide du haut de toohello d’instruction d’un fichier à partir de laquelle vous souhaitez tooaccess hello du cache.

```c#
using StackExchange.Redis
```

Si cet espace de noms ne résout pas, assurez-vous que vous avez ajouté hello package StackExchange.Redis NuGet comme décrit dans [configurer les clients de cache hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

> [!NOTE]
> Notez que le client StackExchange.Redis hello nécessite .NET Framework 4 ou version ultérieure.
> 
> 

instance de Cache Redis Azure tooconnect tooan, appel hello statique `ConnectionMultiplexer.Connect` méthode et passe dans le point de terminaison hello et la clé. Une approche toosharing un `ConnectionMultiplexer` instance dans votre application est toohave une propriété statique qui retourne une instance connectée, toohello similaire, l’exemple suivant. Cela fournit un tooinitialize de façon thread-safe qu’un seul connecté `ConnectionMultiplexer` instance. Dans cet exemple `abortConnect` est toofalse ensemble, ce qui signifie que les appels hello réussira même si un cache de toohello de connexion n’est pas établi. Une fonction clé `ConnectionMultiplexer` est qu’elle restaure automatiquement du cache de connectivité toohello une fois le problème de réseau hello ou d’autres causes sont résolus.

```c#
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
```

Hello point de terminaison du cache, les clés et les ports peuvent être obtenus à partir de hello **Cache Redis** panneau pour votre instance de cache. Pour plus d’informations, consultez les [propriétés du Cache Redis](cache-configure.md#properties).

Une fois que hello est établie, retourner une base de données de référence toohello Redis cache en appelant hello `ConnectionMultiplexer.GetDatabase` (méthode). objet de Hello retourné par hello `GetDatabase` méthode est un objet léger transmis directement et n’a pas besoin toobe stockée.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

client de StackExchange.Redis Hello utilise hello `RedisKey` et `RedisValue` types pour l’accès aux éléments et les stocker dans le cache de hello. Ces types correspondent aux types de langages les plus primitifs, y compris les chaînes, et sont rarement utilisés directement. Redis chaînes sont plus simples au type hello de valeur et peuvent contenir de nombreux types de données, y compris les flux de données binaires sérialisées, alors que vous ne pouvez pas utiliser directement les type hello, vous allez utiliser les méthodes qui contiennent des `String` dans le nom de hello. Pour les types de données primitifs plus vous stocker et extraire des éléments de cache de hello à l’aide de hello `StringSet` et `StringGet` méthodes, sauf si vous stockez les collections ou autres types de données Redis dans le cache de hello. 

`StringSet`et `StringGet` sont très similaire toohello Service de Cache géré `Put` et `Get` méthodes, principale différence étant qu’avant de définir et obtenir un objet .NET dans le cache de hello vous devez d’abord sérialiser. 

Lors de l’appel `StringGet`, si l’objet de hello existe, elle est retournée, et si elle n’est pas le cas, la valeur null est retournée. Dans ce cas, vous pouvez récupérer la valeur de hello à partir de la source de données souhaitée hello et stockez-le dans le cache de hello pour une utilisation ultérieure. Il s’agit en tant que modèle de type cache-aside hello.

expiration de hello toospecify d’un élément dans le cache de hello, utilisez hello `TimeSpan` paramètre de `StringSet`.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Le Cache Redis Azure est compatible aussi bien avec les objets .NET qu’avec les types de données primitifs, mais avant qu’un objet .NET puisse être mis en cache, il doit être sérialisé. Il s’agit de responsabilité hello hello développeur d’applications. Flexibilité hello développeur dans le choix de hello du sérialiseur de hello. Pour plus d’informations et des exemples de code, consultez [travailler avec des objets .NET dans le cache de hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>Migrer l’état de Session ASP.NET et la sortie mise en cache tooAzure Cache Redis
Le Cache Redis Azure dispose de fournisseurs pour l’état de session ASP.NET et pour la mise en cache de sortie de pages. toomigrate votre application qui utilise les versions de Service de Cache géré hello de ces fournisseurs, supprimez d’abord hello sections existantes de votre fichier web.config, puis configurez les versions de Cache Redis Azure hello des fournisseurs de hello. Pour obtenir des instructions sur l’utilisation de hello fournisseurs Azure Redis Cache ASP.NET, consultez [fournisseur d’état de Session ASP.NET pour le Cache Redis Azure](cache-aspnet-session-state-provider.md) et [fournisseur de Cache de sortie ASP.NET pour le Cache Redis Azure](cache-aspnet-output-cache-provider.md).

## <a name="next-steps"></a>Étapes suivantes
Explorer hello [documentation du Cache Redis Azure](https://azure.microsoft.com/documentation/services/cache/) pour les didacticiels, des exemples, des vidéos et bien plus encore.

