---
title: aaaAzure Redis Cache-FAQ | Documents Microsoft
description: "En savoir hello répond aux questions de toocommon, modèles et meilleures pratiques pour le Cache Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Forum aux questions sur le Cache Redis Azure
Découvrez hello répond aux questions de toocommon, modèles et meilleures pratiques pour le Cache Redis Azure.

## <a name="what-if-my-question-isnt-answered-here"></a>Que dois-je faire si je n’ai pas trouvé de réponse à ma question ici ?
Si votre question n’est pas répertoriée ici, faites-le-nous savoir et nous vous aiderons à trouver une réponse.

* Vous pouvez publier une question dans les commentaires hello à fin hello de ce forum aux questions et prendre contact avec l’équipe de Cache Azure hello et d’autres membres de la Communauté sur cet article.
* tooreach une audience plus large, vous pouvez publier une question sur hello [Forum MSDN de Cache Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) et collaborer avec l’équipe de Cache Azure hello et d’autres membres de la Communauté de hello.
* Si vous souhaitez toomake une demande de fonctionnalité, vous pouvez soumettre vos demandes et des idées trop[Azure Redis Cache User Voice](https://feedback.azure.com/forums/169382-cache).
* Vous pouvez également envoyer un courrier électronique toous à [commentaires externes du Cache Azure](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Principes fondamentaux du Cache Redis Azure
Hello Foire aux questions de cette section couvrent certains des concepts de base hello du Cache Redis Azure.

* [Présentation du Cache Redis Azure](#what-is-azure-redis-cache)
* [Comment commencer avec Cache Redis Azure ?](#how-can-i-get-started-with-azure-redis-cache)

Hello Foire aux questions suivantes couvre les concepts de base et des questions sur le Cache Redis Azure et est traités dans un des hello autres sections du Forum aux questions.

* [Que propose Cache Redis et quelle taille dois-je utiliser ?](#what-redis-cache-offering-and-size-should-i-use)
* [Quels clients de cache Redis puis-je utiliser ?](#what-redis-cache-clients-can-i-use)
* [Existe-t-il un émulateur local pour le Cache Redis Azure ?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Comment surveiller l’intégrité de hello et les performances de mon cache ?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Forum aux questions sur la planification
* [Que propose Cache Redis et quelle taille dois-je utiliser ?](#what-redis-cache-offering-and-size-should-i-use)
* [Performance du Cache Redis Azure](#azure-redis-cache-performance)
* [Dans quelle région dois-je placer mon cache ?](#in-what-region-should-i-locate-my-cache)
* [Combien me coûte le Cache Redis Azure ?](#how-am-i-billed-for-azure-redis-cache)
* [Puis-je utiliser le Cache Redis Azure avec le cloud Azure Government, le cloud Azure China ou Microsoft Azure Germany ?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Forum aux questions sur le développement
* [Que faire des options de configuration StackExchange.Redis hello ?](#what-do-the-stackexchangeredis-configuration-options-do)
* [Quels clients de cache Redis puis-je utiliser ?](#what-redis-cache-clients-can-i-use)
* [Existe-t-il un émulateur local pour le Cache Redis Azure ?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Comment exécuter des commandes Redis ?](#how-can-i-run-redis-commands)
* [Pourquoi le Cache Redis Azure dépourvu d’une référence de bibliothèque de classes MSDN comme des hello autres services Azure ?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Puis-je utiliser le Cache Redis Azure comme un cache de session PHP ?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [Quelles sont les bases de données Redis ?](#what-are-redis-databases)

## <a name="security-faqs"></a>Forum aux questions sur la sécurité
* [Quand dois-je activer le port non-SSL de hello pour la connexion tooRedis ?](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Forum aux questions sur la production
* [Quelles sont les meilleures pratiques en matière de production ?](#what-are-some-production-best-practices)
* [Quelles sont les considérations hello lors de l’utilisation des commandes courantes Redis ?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [Comment puis-je évaluer et tester hello les performances de mon cache ?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Informations importantes sur la croissance du pool de threads](#important-details-about-threadpool-growth)
* [Activer le plus grand débit de client de hello tooget du garbage collector pour serveur lors de l’utilisation de StackExchange.Redis](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [Considérations relatives aux performances de connexion](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>Forum aux questions sur la surveillance et le dépannage
Hello FAQ dans cette section couvre communes de surveillance et les questions de dépannage. Pour plus d’informations sur l’analyse et résolution des problèmes de vos instances de Cache Redis Azure, consultez [comment toomonitor Cache Redis Azure](cache-how-to-monitor.md) et [comment tootroubleshoot Cache Redis Azure](cache-how-to-troubleshoot.md).

* [Comment surveiller l’intégrité de hello et les performances de mon cache ?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [Pourquoi est-ce que je reçois des erreurs d’expiration du délai ?](#why-am-i-seeing-timeouts)
* [Pourquoi mon client a été déconnecté du cache de hello ?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Forum aux questions sur les offres de cache précédentes
* [Quelle est l'offre Azure Cache qui me convient ?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>Présentation du Cache Redis Azure
Cache Redis Azure est basé sur open-source populaires hello [cache Redis](http://redis.io). Elle vous donne accès tooa sécurisé Redis cache dédié, géré par Microsoft et est accessible à partir de n’importe quelle application dans Azure. Pour obtenir une présentation plus détaillée, consultez hello [Cache Redis Azure](https://azure.microsoft.com/services/cache/) page produit sur Azure.com.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Comment commencer avec Cache Redis Azure ?
Il existe plusieurs façons de démarrer avec Cache Redis Azure.

* Vous pouvez consulter nos didacticiels disponibles pour [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md) et [Python](cache-python-get-started.md).
* Vous pouvez regarder [comment tooBuild hautes performances applications à l’aide de Microsoft Azure Redis Cache](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* Vous pouvez extraire la documentation du client pour les clients hello qui correspondent au langage de développement hello de votre toosee projet comment toouse Redis hello. Il existe de nombreux clients Redis qui peuvent être utilisés avec le Cache Redis Azure. Pour obtenir la liste des clients Redis, consultez [http://redis.io/clients](http://redis.io/clients).

Si vous n’avez pas encore de compte Azure, vous pouvez :

* [Ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Vous obtenez des crédits qui peuvent être utilisé tootry out à payer des services Azure. Même après que hello crédits épuisés, vous pouvez conserver le compte de hello et utiliser des fonctionnalités et des services Azure gratuits.
* [Activez les avantages d’abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>Que propose Cache Redis et quelle taille dois-je utiliser ?
Chaque offre Cache Redis Azure propose différents niveaux de **taille**, de **bande passante**, de **haute disponibilité** et de **contrat SLA**.

Hello Voici les considérations relatives au choix d’une offre de Cache.

* **Mémoire**: hello les niveaux de base et Standard offrent des 250 Mo à 53 go. niveau de Hello Premium offre jusqu'à too530 go. Pour plus d'informations, consultez [Tarification - Cache Redis Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Les performances réseau**: Si vous avez une charge de travail qui nécessite un débit élevé, niveau de hello Premium offre plus tooStandard de bande passante ou Basic. Également dans chaque niveau, les caches de plus grandes taille ont davantage de bande passante en raison de hello sous-jacent de machine virtuelle qui héberge le cache de hello. Consultez hello [tableau suivant](#cache-performance) pour plus d’informations.
* **Débit**: niveau Premium de hello offre un débit maximal disponible hello. Si le client ou serveur de cache hello atteint les limites de bande passante hello, vous pouvez recevoir des délais d’attente côté client de hello. Pour plus d’informations, consultez hello tableau suivant.
* **Haute disponibilité/SLA**: le Cache Redis Azure garantit qu’un cache Standard/Premium est disponible au moins 99,9 % du temps de hello. toolearn en savoir plus sur notre contrat SLA, consultez [tarification du cache Azure Redis](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). Hello SLA couvre uniquement les points de terminaison de connectivité toohello du Cache. Hello SLA ne couvre pas la protection contre la perte de données. Nous recommandons d’utiliser la fonctionnalité de persistance des données Redis hello dans la résilience hello Premium couche tooincrease contre la perte de données.
* **Persistance des données de redis**: niveau de hello Premium vous permet de données du cache de hello toopersist dans un compte de stockage Azure. Dans un cache de base/Standard, toutes les données hello est stocké uniquement dans la mémoire. En cas de problème lié à l’infrastructure sous-jacente, il existe un risque de perte de données. Nous recommandons d’utiliser la fonctionnalité de persistance des données Redis hello dans la résilience hello Premium couche tooincrease contre la perte de données. Le Cache Redis Azure propose des options RDB et AOF (à venir) de persistance Redis. Pour plus d’informations, consultez [la persistance tooconfigure cache Redis Azure Premium](cache-how-to-premium-persistence.md).
* **Redis Cluster**: toocreate met en cache supérieure à 53 Go ou tooshard des données sur plusieurs nœuds de Redis, vous pouvez utiliser le clustering Redis, qui est disponible dans le niveau Premium de hello. Chaque nœud se compose d’une paire de caches principal/réplica pour la haute disponibilité. Pour plus d’informations, consultez [comment tooconfigure clustering Premium Azure Redis cache](cache-how-to-premium-clustering.md).
* **Amélioré la sécurité et l’isolement réseau**: déploiement du réseau virtuel Azure (VNET) offre une sécurité accrue et isolation pour votre Cache Redis Azure, ainsi que des sous-réseaux, les stratégies de contrôle d’accès, et d’autres fonctionnalités toofurther restreindre l’accès. Pour plus d’informations, consultez [comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache](cache-how-to-premium-vnet.md).
* **Configurer Redis**: hello Standard et les niveaux Premium, vous pouvez configurer Redis pour les notifications de l’espace de clés.
* **Nombre maximal de connexions de client**: niveau de hello Premium offre nombre maximal de hello de clients qui peuvent se connecter tooRedis, avec un nombre élevé de connexions pour les caches de tailles supérieure. Pour plus d’informations, consultez [Tarification - Cache Redis Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Dédié Core pour le serveur de Redis**: niveau Premium de hello, toutes les tailles de cache ont un cœur dédié pour Redis. Dans les niveaux de base/Standard hello, hello C1 taille et versions ultérieures ont un cœur dédié pour le serveur Redis.
* **Redis étant monothread** , le fait d’avoir plus de deux cœurs n’offre aucun avantage supplémentaire, mais les machines virtuelles de grande taille ont généralement plus de bande passante que les plus petites. Si le client ou serveur de cache hello atteint les limites de bande passante hello, vous recevez des délais d’attente côté client de hello.
* **Améliorations des performances**: Caches de niveau Premium de hello sont déployés sur le matériel qui a des processeurs plus rapides, en donnant une meilleure performance toohello comparés Standard niveaux de base ou. Les caches de niveau Premium ont un débit supérieur et des latences moindres.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Performance du Cache Redis Azure
Hello tableau suivant montre les valeurs de la bande passante maximale hello observées lors du test de différentes tailles de Standard et Premium met en cache à l’aide de `redis-benchmark.exe` à partir d’un VM Iaas sur le point de terminaison du Cache Redis Azure hello. 

>[!NOTE] 
>Ces valeurs ne sont pas garanties et il n’y a pas de contrat SLA pour ces chiffres, mais ils sont à peu près normaux. Vous devez charger votre propre taille de cache adaptée application toodetermine hello pour votre application de test.
>
>

Dans ce tableau, nous pouvons dessiner hello suivant conclusions :

* Débit pour les caches de hello sont hello même taille est plus élevé dans hello niveau Premium en tant que niveau Standard de toohello comparés. Par exemple, avec un Cache de 6 Go, débit de P1 est 180 000 RPS comme too49 comparés, 000 pour C3.
* Avec Redis clustering, débit augmente de façon linéaire lorsque vous augmentez le nombre de hello de partitions (nœuds) dans un cluster de hello. Par exemple, si vous créez un cluster P4 de 10 partitions, le débit disponible hello est 400 000 * 10 = 4 millions RPS.
* Le débit pour les tailles de clé plus grandes est plus élevé dans le niveau Premium de hello comme comparé toohello niveau Standard.

| Niveau tarifaire  | Taille | Cœurs d’unité centrale | Bande passante disponible | Taille de la valeur 1 Ko |
| --- | --- | --- | --- | --- |
| **Tailles de cache Standard** | | |**Mégabits par seconde (Mbit/s) / mégaoctets par seconde (Mo/s)** |**Demandes par seconde (RPS)** |
| C0 |250 Mo |Partagé |5 / 0,625 |600 |
| C1 |1 Go |1 |100 / 12,5 |12 200 |
| C2 |2,5 Go |2 |200 / 25 |24 000 |
| C3 |6 Go |4 |400 / 50 |49 000 |
| C4 |13 Go |2 |500 / 62,5 |61 000 |
| C5 |26 Go |4 |1 000 / 125 |115 000 |
| C6 |53 Go |8 |2 000 / 250 |150 000 |
| **Tailles de cache Premium** | |**Cœurs de processeur par partition** | **Mégabits par seconde (Mbit/s) / mégaoctets par seconde (Mo/s)** |**Demandes par seconde (RPS), par partition** |
| P1 |6 Go |2 |1 500 / 187,5 |180 000 |
| P2 |13 Go |4 |3 000 / 375 |360 000 |
| P3 |26 Go |4 |3 000 / 375 |360 000 |
| P4 |53 Go |8 |6 000 / 750 |400 000 |

Pour obtenir des instructions sur le téléchargement hello Redis des outils tels que `redis-benchmark.exe`, consultez hello [comment puis-je exécuter des commandes de Redis ?](#cache-commands) section.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>Dans quelle région dois-je placer mon cache ?
Pour optimiser les performances et la latence la plus faible, localisez votre le Cache Redis Azure Bonjour même région que votre application de client de cache.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Combien me coûte le Cache Redis Azure ?
La tarification du cache Redis Azure est disponible [ici](https://azure.microsoft.com/pricing/details/cache/). Hello, page de tarification répertorie la tarification à un taux horaire. Les caches sont facturés sur une base par minute à partir de hello cache de hello est créé jusqu’au moment de hello un cache est supprimé. Il n’existe aucune option pour arrêter ou suspendre facturation hello d’un cache.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>Puis-je utiliser le Cache Redis Azure avec le cloud Azure Government, le cloud Azure China ou Microsoft Azure Germany ?
Oui, le Cache Redis Azure est disponible dans le cloud Azure Government, le cloud Azure China et Microsoft Azure Germany. URL de Hello pour l’accès et la gestion du Cache Redis Azure sont différentes dans ces clouds comparés au Cloud Public Azure. 

| Cloud   | Suffixe DNS pour Redis            |
|---------|---------------------------------|
| Public  | *.redis.cache.windows.net       |
| Gouvernement des États-Unis  | *.redis.cache.usgovcloudapi.net |
| Allemagne | *.redis.cache.cloudapi.de       |
| Chine   | *.redis.cache.chinacloudapi.cn  |

Pour plus d’informations sur les considérations sur l’utilisation du Cache Redis Azure avec d’autres clouds, consultez hello suivant liens.

- [Bases de données Azure Government - Cache Redis Azure](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Cloud Azure China - Cache Redis Azure](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/)

Pour plus d’informations sur l’utilisation du Cache Redis Azure avec PowerShell dans le Cloud Azure gouvernement, Azure en Chine Cloud et Microsoft Azure situés en Allemagne, consultez [comment tooconnect tooother clouds - Azure Redis Cache PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>Que faire des options de configuration StackExchange.Redis hello ?
StackExchange.Redis présente de nombreuses options. Cette section présente une partie des paramètres communs de hello. Pour plus d’informations sur les options de StackExchange.Redis, consultez la page [Configuration StackExchange.Redis](https://stackexchange.github.io/StackExchange.Redis/Configuration).

| ConfigurationOptions | Description | Recommandation |
| --- | --- | --- |
| AbortOnConnectFail |Lorsque la valeur tootrue, connexion de hello ne se reconnecte pas après une panne réseau. |Définissez toofalse et StackExchange.Redis permettent de se reconnecter automatiquement. |
| ConnectRetry |nombre de Hello maximal de tentatives de connexion de toorepeat pendant initiale se connecter. |Hello suit notes pour obtenir des instructions, consultez. |
| ConnectTimeout |Délai d’expiration en millisecondes pour les opérations de connexion. |Hello suit notes pour obtenir des instructions, consultez. |

Généralement les valeurs par défaut de hello du client de hello sont suffisants. Vous pouvez régler les options de hello en fonction de votre charge de travail.

* **Nouvelle tentatives**
  * Pour le ConnectRetry et ConnectTimeout, des conseils généraux hello est toofail rapide et réessayez. Ce guide est basé sur votre charge de travail et combien de temps sur moyenne prend pour votre tooissue client une commande Redis et recevoir une réponse.
  * Laissez StackExchange.Redis se reconnecter automatiquement au lieu de vérifier l’état de la connexion et de vous reconnecter vous-même. **Évitez d’utiliser hello ConnectionMultiplexer.IsConnected propriété**.
  * Snowballing - parfois vous risquez de rencontrer un problème où vous effectuent une nouvelle tentative et hello +++ Snowball afin de tentatives et récupère jamais. Si snowballing se produit, vous devez envisager d’utiliser un algorithme de tentative d’interruption exponentielle, comme décrit dans [réessayer conseils généraux](../best-practices-retry-general.md) publiée par le groupe Microsoft Patterns & Practices de hello.
* **Valeurs de délai d’expiration**
  * Envisagez de votre charge de travail et définissez les valeurs de hello en conséquence. Si vous stockez les valeurs élevées, valeur hello du délai d’attente tooa plus élevée.
  * Définissez `AbortOnConnectFail` toofalse et StackExchange.Redis permettent de vous reconnecter pour vous.
  * Utiliser une seule instance ConnectionMultiplexer pour l’application hello. Vous pouvez utiliser un toocreate LazyConnection une seule instance qui est retournée par une propriété de connexion, comme indiqué dans [connecter cache toohello à l’aide de la classe ConnectionMultiplexer de hello](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Ensemble hello `ConnectionMultiplexer.ClientName` propriété tooan instance unique nom d’application pour établir un diagnostic.
  * Utilisez plusieurs instances `ConnectionMultiplexer` pour les charges de travail personnalisées.
      * Vous pouvez suivre ce modèle si vous savez que la charge de votre application est variable. Par exemple :
      * Vous pouvez avoir un multiplexeur pour gérer les clés de grande taille.
      * Vous pouvez avoir un multiplexeur pour gérer les clés de petite taille.
      * Vous pouvez définir différentes valeurs pour l’expiration du délai et la logique des nouvelles tentatives pour chaque ConnectionMultiplexer que vous utilisez.
      * Ensemble hello `ClientName` propriété sur chaque toohelp multiplexeur avec diagnostics.
      * Ce guide peut entraîner une latence toomore rationalisé par `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>Quels clients de cache Redis puis-je utiliser ?
Un des points forts hello Redis est qu’il n’y a de nombreux clients prenant en charge de nombreux langages de développement différents. Pour obtenir la liste actuelle des clients, consultez la page des [clients Redis](http://redis.io/clients). Pour consulter des didacticiels qui couvrent plusieurs langues différentes et les clients, consultez [comment toouse Cache Redis Azure](cache-dotnet-how-to-use-azure-redis-cache.md) sur la langue à partir du sélecteur de langue hello haut hello d’article de hello hello souhaité.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Existe-t-il un émulateur local pour le Cache Redis Azure ?
Il n’existe aucun émulateur local pour le Cache Redis Azure, mais vous pouvez exécuter la version de MSOpenTech hello de redis-server.exe de hello [Redis des outils de ligne de commande](https://github.com/MSOpenTech/redis/releases/) sur votre ordinateur local de l’ordinateur et connecter tooit tooget un similaire expérience tooa le cache local émulateur, comme indiqué dans hello l’exemple suivant :

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


Vous pouvez éventuellement configurer un [redis.conf](http://redis.io/topics/config) fichier toomore correspondent étroitement aux hello [les paramètres de cache par défaut](cache-configure.md#default-redis-server-configuration) votre en ligne Azure Redis cache si vous le souhaitez.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>Comment exécuter des commandes Redis ?
Vous pouvez utiliser une des commandes hello répertoriés au [commandes Redis](http://redis.io/commands#) à l’exception des commandes hello répertoriés au [Redis commandes non prises en charge dans le Cache Redis Azure](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). Vous avez plusieurs commandes de Redis toorun options.

* Si vous avez un cache Standard ou Premium, vous pouvez exécuter des commandes de Redis à l’aide de hello [Redis de Console](cache-configure.md#redis-console). console de Redis Hello fournit un toorun de manière sécurisée les commandes Redis Bonjour portail Azure.
* Vous pouvez également utiliser les outils de ligne de commande hello Redis. toouse, effectuer hello comme suit :
* Télécharger hello [Redis des outils de ligne de commande](https://github.com/MSOpenTech/redis/releases/).
* Connectez-vous à l’aide du cache toohello `redis-cli.exe`. Transmettez le point de terminaison de cache hello à l’aide du commutateur -h de hello et hello clé à l’aide : un comme indiqué dans hello l’exemple suivant :
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> Hello Redis des outils de ligne de commande ne fonctionnent pas avec hello port SSL, mais vous pouvez utiliser un utilitaire tel que `stunnel` toosecurely connecter le port SSL de hello outils toohello en suivant les instructions de hello Bonjour [annonce du fournisseur état de Session ASP.NET pour Version préliminaire de redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) billet de blog.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Pourquoi le Cache Redis Azure dépourvu d’une référence de bibliothèque de classes MSDN comme des hello autres services Azure ?
Le Cache Redis Microsoft Azure est basé sur hello open source populaires Cache Redis et est accessible à un large éventail de [clients Redis](http://redis.io/clients) pour de nombreux langages de programmation. Chaque client possède sa propre API que rend appelle toohello Redis cache instance à l’aide [commandes Redis](http://redis.io/commands).

Étant donné que chaque client est différent, il n’y a pas de référence centralisée au sujet des classes sur MSDN. Chaque client a sa propre documentation de référence. En outre la documentation de référence toohello, il existe plusieurs didacticiels montrant comment tooget démarrer avec le Cache Redis Azure à l’aide de différentes langues et les clients de cache. consultez de ces didacticiels, tooaccess [comment toouse Cache Redis Azure](cache-dotnet-how-to-use-azure-redis-cache.md) sur la langue à partir du sélecteur de langue hello haut hello d’article de hello hello souhaité.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Puis-je utiliser le Cache Redis Azure comme un cache de session PHP ?
Oui, toouse du Cache Redis Azure comme un cache de session PHP, spécifiez instance de Cache Redis Azure hello connexion chaîne tooyour dans `session.save_path`.

> [!IMPORTANT]
> Lors de l’utilisation du Cache Redis Azure comme un cache de session PHP, vous devez URL encoder du cache toohello tooconnect utilisé clé sécurité hello, comme indiqué dans hello l’exemple suivant :
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Si la clé de hello n’est pas encodé en URL, vous pouvez recevoir une exception avec un message comme :`Failed tooparse session.save_path`
>
>

Pour plus d’informations sur l’utilisation du Cache Redis comme un cache de session PHP avec le client de PhpRedis hello, consultez [Gestionnaire de Session de PHP](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>Quelles sont les bases de données Redis ?

Bases de données redis sont simplement une séparation logique des données au sein de hello même instance Redis. la mémoire cache Hello est partagée entre toutes les bases de données hello et la consommation de mémoire réelle d’une base de données dépend de hello clés/valeurs stockées dans cette base de données. Par exemple, un cache C6 dispose de 53 Go de mémoire. Vous pouvez choisir toutes les 53 Go tooput dans une base de données, ou vous pouvez le diviser entre plusieurs bases de données. 

> [!NOTE]
> Lorsque vous utilisez un Cache Redis Azure Premium avec le clustering activé, seule la base de données 0 est disponible. Cette limitation est une limitation de Redis intrinsèque et n’est pas tooAzure spécifique du Cache Redis. Pour plus d’informations, consultez [dois-je toomake tout toouse d’application de modifications toomy client clustering ?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>Quand dois-je activer le port non-SSL de hello pour la connexion tooRedis ?
Le serveur Redis ne prend pas en charge SSL de façon native, contrairement au cache Redis Azure. Si vous vous connectez tooAzure Cache Redis et que votre client prend en charge SSL, comme StackExchange.Redis, vous devez utiliser SSL.

>[!NOTE]
>port non-SSL de Hello est désactivé par défaut pour les nouvelles instances de Cache Redis Azure. Si votre client ne prend pas en charge SSL, vous devez activer le port non-SSL de hello en suivant les instructions de hello Bonjour [accéder aux ports](cache-configure.md#access-ports) section Hello [configurer un cache dans le Cache Redis Azure](cache-configure.md) l’article.
>
>

Redis des outils tels que `redis-cli` ne fonctionnent pas avec hello port SSL, mais vous pouvez utiliser un utilitaire tel que `stunnel` toosecurely connecter le port SSL de hello outils toohello en suivant les instructions de hello Bonjour [annonce du fournisseur d’état de Session ASP.NET pour la préversion de Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) billet de blog.

Pour obtenir des instructions sur le téléchargement hello Redis outils, consultez hello [comment puis-je exécuter des commandes de Redis ?](#cache-commands) section.

### <a name="what-are-some-production-best-practices"></a>Quelles sont les meilleures pratiques en matière de production ?
* [Meilleures pratiques StackExchange.Redis](#stackexchangeredis-best-practices)
* [Configuration et concepts](#configuration-and-concepts)
* [Tests de performances](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>Meilleures pratiques StackExchange.Redis
* Définissez `AbortConnect` toofalse, puis laissez hello ConnectionMultiplexer se reconnecter automatiquement. [Vous trouverez plus d’informations ici](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Réutiliser hello ConnectionMultiplexer - ne pas créer un nouveau pour chaque demande. Hello `Lazy<ConnectionMultiplexer>` modèle [illustré ici](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) est recommandé.
* Redis fonctionne de manière optimale avec des valeurs plus petites et il est donc recommandé de fractionner les données plus volumineuses dans plusieurs clés. Dans [cette discussion Redis](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ), 100 ko est considéré comme volumineux. Listez [cet article](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) illustrant un exemple de problème pouvant être provoqué par des valeurs élevées.
* Configurer votre [les paramètres de pool de threads](#important-details-about-threadpool-growth) tooavoid des délais d’attente.
* Utilisez hello au moins connectTimeout par défaut de 5 secondes. Cet intervalle donnerait StackExchange.Redis suffisamment temps toore-connexion hello, en cas d’un spots de réseau.
* Tenez compte des coûts de performance hello associés à différentes opérations que vous exécutez. Par exemple, hello `KEYS` commande est une opération o (n) et doit être évitée. Hello [redis.io site](http://redis.io/commands/) a plus d’informations sur la complexité temporelle de hello pour chaque opération qui prend en charge. Cliquez sur chaque commande toosee hello de complexité pour chaque opération.

#### <a name="configuration-and-concepts"></a>Configuration et concepts
* Utilisez le niveau Standard ou Premium pour les systèmes de production. Hello niveau de base est un système de nœud unique sans réplication des données et aucun contrat SLA. En outre, utilisez au moins un cache C1. Les caches C0 s’appliquent généralement aux scénarios de développement/test simples.
* N’oubliez pas que Redis est un magasin de données **In-Memory** . Lisez [cet article](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) pour identifier les scénarios où une perte de données peut se produire.
* Développer votre système de sorte qu’il peut gérer blips de connexion [toopatching et basculement](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Tests de performances
* Démarrer à l’aide de `redis-benchmark.exe` tooget une idée de débit possible avant d’écrire vos propres tests de performances. Étant donné que `redis-benchmark` ne prend pas en charge SSL, vous devez [activer le port hello Non-SSL via hello portail Azure](cache-configure.md#access-ports) avant d’exécuter le test de hello. Pour obtenir des exemples, consultez [comment puis-je évaluer et tester hello les performances de mon cache ?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* le client de Hello utilisé pour le test de machine virtuelle doit être Bonjour même région que votre instance de cache Redis.
* Nous recommandons d’utiliser des séries de machines virtuelles Dv2 pour votre client qu’ils ont une meilleure matériel et doivent donner des résultats optimaux hello.
* Assurez-vous que votre client que vous choisissez de machine virtuelle a au moins autant de fonctionnalités informatiques et de la bande passante en tant que cache hello que vous testez.
* Activer VRSS sur l’ordinateur client de hello si vous êtes sous Windows. [Vous trouverez plus d’informations ici](https://technet.microsoft.com/library/dn383582.aspx).
* Les instances Redis de niveau Premium offriront une meilleure latence de réseau et un débit supérieur car elles s’exécutent sur un matériel plus performant en termes de processeur et de réseau.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>Quelles sont les considérations hello lors de l’utilisation des commandes courantes Redis ?
* Vous ne devez pas exécuter certaines commandes Redis qui prennent un toocomplete beaucoup de temps, sans avoir à comprendre l’impact de hello de ces commandes.
  * Par exemple, n’exécutez pas de hello [clés](http://redis.io/commands/keys) commande en production, car elle peut prendre un tooreturn beaucoup de temps selon le nombre de clés hello. Redis est un serveur à thread unique qui traite une commande à la fois. Si vous avez d’autres commandes émises après avoir des clés, ils ne seront pas traités tant que Redis traite la commande de clés hello. Hello [redis.io site](http://redis.io/commands/) a plus d’informations sur la complexité temporelle de hello pour chaque opération qui prend en charge. Cliquez sur chaque commande toosee hello de complexité pour chaque opération.
* Taille des clés : dois-je utiliser des petites clés/valeurs ou de grandes clés/valeurs ? En règle générale, il convient de scénario de hello. Si votre scénario requiert des clés plus volumineuses, vous pouvez ajuster hello ConnectionTimeout et tentatives et ajuster votre logique de nouvelle tentative. Du point de vue serveur Redis, plus petites valeurs sont observés toohave de meilleur performances.
* Ces considérations ne signifient que vous ne peut pas stocker des valeurs supérieures dans Redis ; Vous devez être conscient de hello suivant considérations. Les temps de latence seront plus élevés. Si vous avez un jeu de données sont supérieure et une qui est plus petit, vous pouvez utiliser plusieurs instances de ConnectionMultiplexer, chacun configuré avec un autre ensemble de valeurs de délai d’attente et de nouvelle tentative, comme décrit dans hello précédente [que hello Options de configuration StackExchange.Redis](#cache-configuration) section.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>Comment puis-je évaluer et tester hello les performances de mon cache ?
* [Activer les diagnostics de cache](cache-how-to-monitor.md#enable-cache-diagnostics) afin de pouvoir [moniteur](cache-how-to-monitor.md) hello d’intégrité de votre cache. Vous pouvez afficher hello dans hello portail Azure et vous peuvent également [Téléchargez et lisez](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) les à l’aide des outils hello de votre choix.
* Vous pouvez utiliser le test de tooload redis-benchmark.exe votre serveur Redis.
* Assurez-vous que le client de test de charge hello et le cache Redis hello sont Bonjour même région.
* Utiliser redis-cli.exe et surveiller de cache hello à l’aide de la commande INFO hello.
* Si votre charge provoque la fragmentation de mémoire haute, vous devez puissance tooa de cache de taille supérieure.
* Pour obtenir des instructions sur le téléchargement hello Redis outils, consultez hello [comment puis-je exécuter des commandes de Redis ?](#cache-commands) section.

Hello les commandes suivantes fournissent un exemple d’utilisation de redis-benchmark.exe. Pour obtenir des résultats précis, exécutez ces commandes à partir d’une machine virtuelle dans hello même région que votre cache.

* Test de requêtes SET en pipeline à l’aide d’une charge utile de 1 ko

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Testez des requêtes GET en pipeline à l’aide d’une charge utile de 1 ko.
  Remarque : Exécutez hello SET test ci-dessus le premier cache toopopulate

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>Informations importantes sur la croissance du pool de threads
Hello pool de threads CLR a deux types de threads - « Travail » et « Port de terminaison d’e/s » (également appelé IOCP) de threads.

* Les threads Worker sont utilisés notamment pour le traitement des méthodes `Task.Run(…)` ou `ThreadPool.QueueUserWorkItem(…)`. Ces threads sont également utilisés par les divers composants Bonjour CLR lorsque le travail doit toohappen sur un thread d’arrière-plan.
* Les threads IOCP sont utilisés lorsque les e/s asynchrone se produit (par exemple, lors de la lecture à partir du réseau de hello).

pool de threads Hello fournit de nouveaux threads de travail ou threads de terminaison d’e/s à la demande (sans toute limitation) jusqu'à ce qu’il atteigne le paramètre de « Minimum » hello pour chaque type de thread. Par défaut, le nombre minimal de hello de threads est définie nombre toohello de processeurs sur un système.

Une fois hello nombre d’existant threads (occupé) accès hello « minimale » de threads, hello ThreadPool sera taux d’accélération hello auquel elle injecte nouveau thread tooone de threads par 500 millisecondes. Généralement, si votre système reçoit une rafale de tâches nécessitant un thread IOCP, la tâche sera traitée très rapidement. Toutefois, si la croissance hello de travail est supérieur à ce hello configuré le paramètre de « Minimum », il y aura un certain délai lors du traitement de certains travaux de hello hello ThreadPool attend une des deux choses toohappen.

1. Un thread existant devient tooprocess libre hello travail.
2. Aucun thread existant ne se libère pendant 500 ms, auquel cas un nouveau thread est créé.

En fait, cela signifie que lorsque le nombre de hello de threads occupés est supérieur au nombre minimum de threads, vous probablement payez un délai de 500 ms avant que le trafic réseau soit traité par l’application hello. En outre, il est important toonote que lorsqu’un existant thread reste inactif pendant plus de 15 secondes (selon ce que je n’oubliez pas), il est nettoyé et ce cycle de croissance et de retrait peut se répéter.

Observons cet exemple de message d’erreur de StackExchange.Redis (build 1.0.450 ou version ultérieure) ; vous voyez que les statistiques de pool de threads s’affichent désormais (voir les détails IOCP et WORKER ci-dessous).

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

Dans l’exemple précédent de hello, vous pouvez voir que pour le thread IOCP il sont 6 threads occupés et système de hello est configuré tooallow 4 minimal de threads. Dans ce cas, les clients hello aurait probablement vu deux délais de 500 ms car 6 > 4.

Notez que StackExchange.Redis peut atteindre les délais d’expiration si la croissance des threads IOCP ou WORKER est limitée.

### <a name="recommendation"></a>Recommandation
Par conséquent, nous recommandons vivement que les clients la valeur hello configuration minimale pour toosomething de threads IOCP et de travail supérieure à la valeur par défaut hello. Nous ne pouvons pas donner conséquente obtenir des conseils sur ce que cette valeur doit être car hello bonne valeur pour une application est trop élevée ou de faible pour une autre application. Ce paramètre peut également affecter les performances de hello des autres composants d’applications complexes, par conséquent, chaque client doit ajuster toofine qu'a besoin de cette tootheir de paramètre spécifique. Le mieux est de commencer à 200 ou 300, puis de tester et d’ajuster cette valeur en fonction des besoins.

Comment tooconfigure ce paramètre :

* Dans ASP.NET, utilisez hello [paramètre de configuration « minIoThreads »] [ "minIoThreads" configuration setting] sous hello `<processModel>` élément de configuration dans le fichier web.config. Si vous exécutez à l’intérieur de sites Web Azure, ce paramètre n’est pas exposé par le biais des options de configuration hello. Toutefois, vous devez toujours être en mesure de tooconfigure ce paramètre par programmation (voir ci-dessous) à partir de votre méthode Application_Start global.asax.cs.

  > [!NOTE] 
  > Hello valeur spécifiée dans cet élément de configuration est un *par cœur* paramètre. Par exemple, si vous avez un ordinateur 4 cœurs et que vous souhaitez que votre toobe de paramètre minIOThreads 200 lors de l’exécution, vous utiliseriez `<processModel minIoThreads="50"/>`.
  >

* En dehors d’ASP.NET, utilisez hello [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>Activer le plus grand débit de client de hello tooget du garbage collector pour serveur lors de l’utilisation de StackExchange.Redis
L’activation du serveur dans le catalogue global, vous pouvez optimiser les client hello et fournir de meilleures performances et débit lors de l’utilisation de StackExchange.Redis. Pour plus d’informations sur le serveur de catalogue global et comment tooenable, consultez hello suivant des articles :

* [garbage collector pour serveur tooenable](https://msdn.microsoft.com/library/ms229357.aspx)
* [Principes de base du Garbage Collection](https://msdn.microsoft.com/library/ee787088.aspx)
* [Garbage Collection et performances](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>Considérations relatives aux performances de connexion

Chaque niveau tarifaire est associé à des limites spécifiques concernant les connexions clientes, la mémoire et la bande passante. Tandis que chaque taille de cache permet aux *jusqu'à* un certain nombre de connexions, chaque tooRedis connexion surcharge associée. Un exemple d’une telle surcharge est l’utilisation du processeur et de la mémoire à la suite d’un chiffrement TLS/SSL. limite du nombre maximal de connexions Hello pour une taille de cache donné suppose un cache peu chargé. Si charger à partir de la charge de la connexion *plus* charge à partir d’opérations du client dépasse la capacité pour le système de hello, le cache de hello peut rencontrer des problèmes de capacité même si vous ne dépassez pas la limite de connexions hello pour hello taille actuelle du cache.

Pour plus d’informations sur les limites de différentes connexions hello pour chaque niveau, consultez [tarification du Cache Redis Azure](https://azure.microsoft.com/pricing/details/cache/). Pour plus d’informations sur les connexions et les autres configurations par défaut, consultez la page [Configuration du serveur Redis par défaut](cache-configure.md#default-redis-server-configuration).

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>Comment surveiller l’intégrité de hello et les performances de mon cache ?
Les instances de Microsoft Azure Redis Cache peuvent être surveillées Bonjour [portail Azure](https://portal.azure.com). Vous pouvez afficher les métriques, épingler des graphiques de métriques toohello tableau d’accueil, personnaliser la plage de date et d’heure hello des graphiques de surveillance, ajouter et supprimer des métriques à partir de graphiques de hello et définir des alertes lorsque certaines conditions sont remplies. Pour plus d’informations, voir [Surveillance du cache Redis Azure](cache-how-to-monitor.md).

Hello Cache Redis **menu ressource** contient également plusieurs outils pour surveiller et dépanner vos caches.

* **Diagnostiquer et résoudre les problèmes** fournit des informations sur les problèmes courants et les stratégies de résolutions associées.
* **Resource Health** surveille vos ressources et vous indique si elles s’exécutent comme prévu. Pour plus d’informations sur hello service d’intégrité de ressource Azure, consultez [vue d’ensemble du contrôle d’intégrité Azure Resource](../resource-health/resource-health-overview.md).
* **Nouvelle demande de support** fournit des options tooopen une demande de support pour votre cache.

Ces outils permettent de vous toomonitor hello d’intégrité de vos instances de Cache Redis Azure et vous aider à gérer vos applications de mise en cache. Pour plus d’informations, voir hello « Prise en charge et les paramètres de résolution des problèmes » section [comment tooconfigure Cache Redis Azure](cache-configure.md).

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>Pourquoi est-ce que je reçois des erreurs d’expiration du délai ?
Délais d’attente se produisent dans le client de hello que vous utilisez tootalk tooRedis. Lorsqu’une commande est envoyée toohello Redis server, commande hello est la file d’attente et finit par serveur Redis récupère commande hello et l’exécute. Toutefois le client de hello peut expirer pendant ce processus et s’il existe une exception est déclenché sur hello appel côté. Pour plus d’informations sur la résolution des problèmes de délai d’attente, voir [Résolution des problèmes côté client](cache-how-to-troubleshoot.md#client-side-troubleshooting) et [Exceptions au délai d’expiration de StackExchange.Redis](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>Pourquoi mon client a été déconnecté du cache de hello ?
Hello Voici certains raison courante de déconnexion d’un cache.

* Causes côté client
  * application cliente de Hello a été redéployée.
  * application cliente de Hello a effectué une opération de mise à l’échelle.
    * Dans les cas de hello de Services de cloud computing ou des applications Web, cela peut être dû tooauto-mise à l’échelle.
  * couche de mise en réseau Hello côté client de hello modifié.
  * Erreurs temporaires s’est produite dans le client de hello ou dans les nœuds du réseau entre le client de hello et le serveur de hello hello.
  * limites de seuil de bande passante Hello a été atteint.
  * Processeur de manière intensive des opérations a nécessité toocomplete trop long.
* Causes côté serveur
  * Hello service de Cache Redis Azure hello offre de cache standard, ouvert un basculement à partir du nœud secondaire du toohello hello nœud principal.
  * Azure a été mise à jour corrective instance hello où le cache de hello a été déployé
    * Il peut s’agir de mises à jour du serveur Redis ou d’une maintenance générale de la machine virtuelle.

### <a name="which-azure-cache-offering-is-right-for-me"></a>Quelle est l'offre Azure Cache qui me convient ?
> [!IMPORTANT]
> Conformément à ce qui a été [annoncé](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) l’année dernière, le service de cache géré Azure et le service In-Role Cache Azure **ont été supprimés** le 30 novembre 2016. Notre recommandation est toouse [Cache Redis Azure](https://azure.microsoft.com/services/cache/). Pour plus d’informations sur la migration, consultez [migrer à partir du Service de Cache géré tooAzure Cache Redis](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>Cache Redis Azure
Cache Redis Azure est généralement disponible dans des tailles de too53 Go et a un contrat SLA de 99,9 % de disponibilité. Hello nouvelle [niveau premium](cache-premium-tier-intro.md) propose des tailles de too530 Go et la prise en charge pour le clustering, le réseau virtuel et la persistance, avec un contrat SLA de 99,9 %.

Azure Cache Redis permet aux clients hello capacité toouse un cache Redis sécurisé et dédié, géré par Microsoft. Avec cette offre, vous obtenez ensemble complet de fonctionnalités de hello tooleverage et l’écosystème fournis par Redis et fiable d’hébergement et de contrôle de Microsoft.

À la différence des caches classiques qui traitent uniquement des paires clé-valeur, Redis est réputé pour ses types de données hautement performants. Redis également prend en charge l’exécution d’opérations atomiques sur ces types, comme l’ajout de chaîne de tooa ; valeur d’incrémentation hello dans un hachage ; liste de push tooa ; calcul d’intersection définie, union et différence ; ou lors de l’obtention de membre hello avec classement le plus élevé dans un ensemble trié. D’autres fonctionnalités incluent la prise en charge des transactions, pub/sub, l’écriture de scripts Lua, des clés avec la durée de vie limitée, et toomake de paramètres de configuration Redis se comporter plus comme un cache classique.

Réussite de tooRedis un autre aspect clé est hello sain et puissant qui écosystème open source autour de lui. Il apparaît dans un ensemble diversifié de hello des clients Redis disponibles dans plusieurs langues. Cet écosystème et un large éventail de clients autorisent toobe Cache Redis Azure utilisé par pratiquement toute charge de travail à l’intérieur de Azure.

Pour plus d’informations sur la mise en route avec le Cache Redis Azure, consultez [comment tooUse Cache Redis Azure](cache-dotnet-how-to-use-azure-redis-cache.md) et [documentation du Cache Redis Azure](index.md).

### <a name="managed-cache-service"></a>Service de cache géré
[Le service de cache géré a été supprimé le 30 novembre 2016.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview archivé documentation, consultez [Documentation du Service Cache managé archivés](https://msdn.microsoft.com/library/azure/dn386094.aspx).

### <a name="in-role-cache"></a>In-Role Cache
[In-Role Cache a été supprimé le 30 novembre 2016.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview archivé documentation, consultez [Documentation de Cache In-Role archivés](https://msdn.microsoft.com/library/azure/dn386103.aspx).

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
