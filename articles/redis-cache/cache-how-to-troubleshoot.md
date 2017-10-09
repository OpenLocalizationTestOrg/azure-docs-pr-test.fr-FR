---
title: aaaHow tootroubleshoot Cache Redis Azure | Documents Microsoft
description: "Découvrez comment tooresolve commun problèmes avec le Cache Redis Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>Comment tootroubleshoot Cache Redis Azure
Cet article fournit des conseils pour résoudre hello suivant des catégories de problèmes de Cache Redis Azure.

* [Résolution des problèmes du côté client](#client-side-troubleshooting) : cette section fournit des instructions sur l’identification et résolution des problèmes dus à l’application hello connexion tooAzure du Cache Redis.
* [Dépannage du côté serveur](#server-side-troubleshooting) : cette section fournit des instructions sur l’identification et résolution des problèmes provoqué hello côté serveur de Cache Redis Azure.
* [Exceptions de délai d’attente StackExchange.Redis](#stackexchangeredis-timeout-exceptions) -cette section fournit des informations sur la résolution des problèmes liés à l’aide du client de StackExchange.Redis hello.

> [!NOTE]
> Plusieurs hello dépannage des étapes de ce guide comprend les instructions toorun commandes Redis et surveiller les diverses mesures de performances. Pour plus d’informations et pour obtenir des instructions, consultez les articles de hello Bonjour [des informations supplémentaires](#additional-information) section.
> 
> 

## <a name="client-side-troubleshooting"></a>Résolution des problèmes côté client
Cette section traite des problèmes qui surviennent à cause d’une condition de l’application cliente de hello.

* [Pression de mémoire sur le client de hello](#memory-pressure-on-the-client)
* [Augmentation de trafic](#burst-of-traffic)
* [Utilisation importante du processeur du client](#high-client-cpu-usage)
* [Bande passante dépassée côté client](#client-side-bandwidth-exceeded)
* [Taille importante de la demande/réponse](#large-requestresponse-size)
* [Les données qui s’est produit toomy dans Redis ?](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>Pression de mémoire sur le client de hello
#### <a name="problem"></a>Problème
Sollicitation de la mémoire sur l’ordinateur client de hello conduit tooall des types de problèmes de performances susceptibles de retarder le traitement des données qui a été envoyés par l’instance de Redis hello sans délai. Lors de la sollicitation de la mémoire atteint, système de hello a généralement toopage les données de la mémoire toovirtual de mémoire physique qui est sur le disque. Cela *page défaillante* causes hello considérablement système tooslow vers le bas.

#### <a name="measurement"></a>Mesure
1. Surveiller l’utilisation de la mémoire sur toomake ordinateur sûr qu’il ne dépasse pas la mémoire disponible. 
2. Hello d’analyse `Page Faults/Sec` compteur de performances. La plupart des systèmes rencontrent des erreurs de page, même lors d’un fonctionnement normal. Donc, surveillez les pics dans ce compteur de performances, car ils correspondent à des délais d’attente.

#### <a name="resolution"></a>Résolution :
Mettre à niveau votre client de plus grande taille de machine virtuelle avec plus de mémoire tooa client ou explorez votre consuption mémoire tooreduce de modèles de l’utilisation de mémoire.

### <a name="burst-of-traffic"></a>Augmentation de trafic
#### <a name="problem"></a>Problème
Pics de trafic combiné avec médiocre `ThreadPool` paramètres peuvent entraîner des retards dans le traitement des données déjà transmises par hello Redis le serveur mais non encore consommé côté client de hello.

#### <a name="measurement"></a>Mesure
Surveillez comment évoluent vos statistiques `ThreadPool` au fil du temps à l’aide d’un code [tel que celui-ci](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs). Vous pouvez également consulter hello `TimeoutException` message à partir de StackExchange.Redis. Voici un exemple :

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

Bonjour au-dessus de message, il existe plusieurs problèmes qui sont intéressants :

1. Notez que hello en `IOCP` section et hello `WORKER` section que vous avez un `Busy` valeur est supérieure à hello `Min` valeur. Cela signifie que vos paramètres de `ThreadPool` ont besoin d’être ajustés.
2. Vous pouvez également voir `in: 64221`. Cela indique que 64211 octets ont été reçus à la couche de socket noyau hello mais n’ont pas été lues par l’application hello (par exemple, StackExchange.Redis). En règle générale, cela signifie que votre application n’est pas la lecture des données à partir du réseau de hello aussi rapidement que le serveur de hello il envoie tooyou.

#### <a name="resolution"></a>Résolution :
Configurer votre [les paramètres de pool de threads](https://gist.github.com/JonCole/e65411214030f0d823cb) toomake sûr que votre pool de threads sera évoluer rapidement sous croître scénarios.

### <a name="high-client-cpu-usage"></a>Utilisation importante du processeur du client
#### <a name="problem"></a>Problème
Utilisation élevée de l’UC sur le client de hello est une indication que le système de hello ne peut pas suivre travail hello tooperform qu’il a été demandé. Cela signifie que le client hello peut échouer tooprocess une réponse de Redis en temps voulu bien Redis envoyé de réponse de hello très rapidement.

#### <a name="measurement"></a>Mesure
Hello du Moniteur système large processeur par le biais hello portail Azure ou hello associés de compteur de performance. Veillez à ne pas toomonitor *processus* , car un seul processus peut avoir de faible utilisation du processeur au processeur hello même temps que l’ensemble du processeur du système peut être élevé. Regardez les pics d’utilisation du processeur qui correspondent à des délais d’expiration. À la suite par le processeur, vous pouvez également voir haute `in: XXX` valeurs `TimeoutException` des messages d’erreur comme décrit dans hello [rafale de trafic](#burst-of-traffic) section.

> [!NOTE]
> StackExchange.Redis 1.1.603 et version ultérieure incluent hello `local-cpu` métrique dans `TimeoutException` messages d’erreur. Veillez à l’aide de la version la plus récente de hello hello [package StackExchange.Redis NuGet](https://www.nuget.org/packages/StackExchange.Redis/). Il sont constamment des bogues corrigés dans toomake de code hello il tootimeouts plus robuste ayant la version la plus récente hello est donc important.
> 
> 

#### <a name="resolution"></a>Résolution :
Mise à niveau de la plus grande taille de machine virtuelle tooa avec plus de capacité de l’UC ou examiner ce qui provoque des pics de consommation UC. 

### <a name="client-side-bandwidth-exceeded"></a>Bande passante dépassée côté client
#### <a name="problem"></a>Problème
Les ordinateurs clients de tailles différentes limitent la bande passante du réseau qu’ils peuvent utiliser. Si hello client dépasse hello la bande passante disponible, puis les données ne seront pas traitées côté client de hello aussi rapidement que le serveur de hello il envoie. Cela peut entraîner des tootimeouts.

#### <a name="measurement"></a>Mesure
Surveillez comment votre utilisation de la bande passante évolue au fil du temps, à l’aide d’un code [tel que celui-ci](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs). Notez que ce code peut ne pas s’exécuter correctement dans certains environnements aux autorisations restreintes (tels que les sites web Azure).

#### <a name="resolution"></a>Résolution :
Augmentez la taille de la machine mémoire du client ou réduisez la consommation de la bande passante du réseau.

### <a name="large-requestresponse-size"></a>Taille importante de la demande/réponse
#### <a name="problem"></a>Problème
Une demande/réponse volumineuse peut entraîner des délais d’expiration. Par exemple, supposons que la durée du délai d’expiration que vous avez configurée sur votre client est de 1 seconde. Votre application demande deux clés (par exemple, « A » et « B ») à hello simultanément (à l’aide de hello même connexion réseau physique). La plupart des clients prennent en charge les « Pipelining » de requêtes, telles que les deux requêtes « A » et « B » sont envoyés sur hello câble toohello serveur après hello autres sans attendre que les réponses hello. Hello serveur envoie les réponses hello sauvegarder Bonjour même ordre. Si la réponse « A » est grande suffisamment il peut manger la plupart du délai d’attente hello pour les demandes suivantes. 

Bonjour à l’exemple suivant illustre ce scénario. Dans ce scénario, la demande « A » et « B » sont envoyés rapidement, serveur de hello commence à envoyer des réponses « A » et « B » rapidement, mais en raison du temps de transfert de données, 'B' coincé derrière hello autres demande et le délai de temporisation expire même si le serveur de hello a répondu rapidement.

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>Mesure
Il s’agit d’un un toomeasure difficile. En fait, vous avez tooinstrument votre client tootrack grand demandes et réponses code. 

#### <a name="resolution"></a>Résolution :
1. Redis est optimisé pour un grand nombre de petites valeurs plutôt que pour quelques grandes valeurs. Hello préféré solution est toobreak vos données en connexes plus petites valeurs. Consultez hello [quelle est la plage de tailles de valeur idéale hello pour redis ? Is 100KB too large?](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) pour savoir pourquoi les valeurs moins élevées sont recommandées.
2. Augmenter la taille de hello de votre machine virtuelle (pour le client et le serveur de Cache Redis), les temps pour les réponses supérieure de transfert de tooget supérieure la bande passante des fonctionnalités, ce qui réduit les données. Notez que l’obtention davantage de bande passante sur juste du serveur hello ou seulement sur les clients hello peuvent ne pas suffire. Mesurer l’utilisation de la bande passante et comparer les fonctionnalités toohello de taille hello de machine virtuelle que vous avez actuellement.
3. Augmenter le nombre de hello de `ConnectionMultiplexer` objets utilisation et les demandes de tourniquet sur différentes connexions.

### <a name="what-happened-toomy-data-in-redis"></a>Les données qui s’est produit toomy dans Redis ?
#### <a name="problem"></a>Problème
Je prévu pour certaines données toobe dans mon instance de Cache Redis Azure, mais il n’a pas été sembler toobe il.

#### <a name="resolution"></a>Résolution :
Consultez [quelles données toomy s’est produit dans Redis ?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) pour les causes et solutions possibles.

## <a name="server-side-troubleshooting"></a>Résolution des problèmes côté serveur
Cette section traite des problèmes qui surviennent à cause d’une condition sur un serveur de cache hello.

* [Pression de mémoire sur le serveur de hello](#memory-pressure-on-the-server)
* [Utilisation élevée du processeur / charge importante du serveur](#high-cpu-usage-server-load)
* [Bande passante dépassée côté serveur](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>Pression de mémoire sur le serveur de hello
#### <a name="problem"></a>Problème
Pression de mémoire sur le côté du serveur hello conduit tooall des types de problèmes de performances susceptibles de retarder le traitement des demandes. Lors de la sollicitation de la mémoire atteint, système de hello a généralement toopage les données de la mémoire toovirtual de mémoire physique qui est sur le disque. Cela *page défaillante* causes hello considérablement système tooslow vers le bas. Plusieurs causes peuvent être à l’origine de cette saturation de la mémoire : 

1. Capacité de toofull hello du cache a été rempli avec des données. 
2. Redis voit la fragmentation de mémoire haute - plus souvent provoquée par le stockage d’objets volumineux (Redis est optimisé pour des objets small - voir hello [quelle est la plage de tailles de valeur idéale hello pour redis ? Is 100KB too large?](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ). 

#### <a name="measurement"></a>Mesure
Redis fournit deux mesures qui peuvent vous aider à identifier ce problème. Hello est tout d’abord `used_memory` et hello autres est `used_memory_rss`. [Ces mesures](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) sont disponibles dans hello portail Azure ou via hello [Redis des informations](http://redis.io/commands/info) commande.

#### <a name="resolution"></a>Résolution :
Il existe plusieurs modifications possibles que vous pouvez rendre l’utilisation de la mémoire toohelp conserver intègre :

1. [Configurez une stratégie de mémoire](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) et définissez des délais d’expiration sur vos clés. Sachez que cela peut ne pas suffire si vous constatez une fragmentation.
2. [Configurez la valeur maxmemory-réservé](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) qui est suffisamment grande toocompensate de fragmentation de la mémoire.
3. Divisez vos objets volumineux mis en cache en objets plus petits.
4. [Mise à l’échelle](cache-how-to-scale.md) tooa de cache de taille supérieure.
5. Si vous utilisez un [cache premium avec le cluster Redis activé](cache-how-to-premium-clustering.md) vous pouvez [augmenter le nombre de hello de partitions](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache).

### <a name="high-cpu-usage--server-load"></a>Utilisation élevée du processeur / charge importante du serveur
#### <a name="problem"></a>Problème
Utilisation élevée du processeur peut signifier que côté client de hello peut échouer tooprocess une réponse de Redis en temps voulu bien Redis envoyé de réponse de hello très rapidement.

#### <a name="measurement"></a>Mesure
Hello du Moniteur système large processeur par le biais hello portail Azure ou hello associés de compteur de performance. Veillez à ne pas toomonitor *processus* , car un seul processus peut avoir de faible utilisation du processeur au processeur hello même temps que l’ensemble du processeur du système peut être élevé. Regardez les pics d’utilisation du processeur qui correspondent à des délais d’expiration.

#### <a name="resolution"></a>Résolution :
[Mise à l’échelle](cache-how-to-scale.md) tooa taille du cache de niveau avec plus de capacité de l’UC ou examiner ce qui provoque des pics de consommation UC. 

### <a name="server-side-bandwidth-exceeded"></a>Bande passante dépassée côté serveur
#### <a name="problem"></a>Problème
Les instances de cache de différentes tailles limitent la bande passante du réseau qu’ils peuvent utiliser. Si le serveur de hello dépasse la bande passante disponible de hello, puis données n’être envoyées toohello client plus rapidement. Cela peut entraîner des tootimeouts.

#### <a name="measurement"></a>Mesure
Vous pouvez surveiller hello `Cache Read` métrique, quantité hello des données lues à partir du cache hello mégaoctets par seconde (Mbits/s) pendant la période de rapport spécifiée hello. Cette valeur correspond à la bande passante du réseau toohello utilisée par ce cache. Si vous souhaitez tooset des alertes pour les limites de la bande passante du réseau côté serveur, vous pouvez les créer à l’aide de ce `Cache Read` compteur. Comparer vos mesures avec des valeurs hello dans [cette table](cache-faq.md#cache-performance) pour hello observé les limites de bande passante pour le cache de différentes tailles et les niveaux de tarification.

#### <a name="resolution"></a>Résolution :
Si vous êtes toujours près hello observé la bande passante maximale pour la taille de votre cache et de couche tarifaire, [mise à l’échelle](cache-how-to-scale.md) tooa tarification couche ou la taille de la bande passante réseau, en utilisant les valeurs hello [cette table](cache-faq.md#cache-performance) comme guide.

## <a name="stackexchangeredis-timeout-exceptions"></a>Exceptions au délai d’expiration de StackExchange.Redis
Pour les opérations synchrones, StackExchange.Redis utilise un paramètre de configuration appelé `synctimeout`, qui a une valeur par défaut de 1000 ms. Si un appel synchrone ne se termine dans hello stipulé heure, hello StackExchange.Redis client lève un délai d’attente erreur similaires toohello l’exemple suivant.

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


Ce message d’erreur contient des mesures qui peuvent aider à vous pointez toohello cause et possible la résolution du problème de hello. Hello tableau suivant contient des détails sur les métriques de message d’erreur hello.

| Mesure de message d’erreur | Détails |
| --- | --- |
| inst |Dans la dernière tranche de temps hello : 0 commandes ont été émis. |
| mgr |le Gestionnaire de socket Hello effectue `socket.select` qui signifie qu’il demande hello du système d’exploitation tooindicate un socket qui a un élément toodo ; en fait : lecteur de hello pas activement lit à partir du réseau de hello, car il ne pensez aucune toodo |
| file d'attente |73 opérations sont en cours. |
| qu |6 des opérations en cours de hello hello la file d’attente en attente et n’ont pas encore été enregistrées réseau sortant des toohello |
| qs |toohello server ont été envoyés à 67 des opérations en cours de he mais une réponse n’est pas disponible. Hello réponse peut être `Not yet sent by hello server` ou`sent by hello server but not yet processed by hello client.` |
| qc |0 des opérations en cours de hello connaissent des réponses mais n’ont pas encore été marqués comme étant exécutée en raison toowaiting sur boucle de saisie semi-automatique hello |
| wr |Il existe un writer actif (ce qui signifie que hello 6 demandes en attente ne sont pas ignorés) octets/activewriters |
| commencer |Aucun lecteur active et zéro octets sont disponible toobe lire sur hello octets/activereaders de carte réseau |

### <a name="steps-tooinvestigate"></a>Étapes tooinvestigate
1. Comme meilleure pratique Assurez-vous que vous utilisez hello suivant le modèle tooconnect lors de l’utilisation du client de StackExchange.Redis hello.

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    Pour plus d’informations, consultez [connecter cache toohello avec StackExchange.Redis](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).

1. Assurez-vous que votre Cache Redis Azure et l’application cliente de hello sont Bonjour même région dans Azure. Par exemple, vous pouvez obtenir des délais d’attente lorsque votre cache est en cours de l’est des États-Unis, mais de client de hello est dans l’ouest des États-Unis et de demande de hello ne se termine dans hello `synctimeout` intervalle, ou vous pouvez obtenir des délais d’attente lorsque vous effectuez un débogage à partir de votre ordinateur de développement local. 
   
    Il est vivement recommandé de cache de hello toohave et dans le client hello dans hello même région Azure. Si vous avez un scénario qui inclut les appels entre régions, vous devez définir hello `synctimeout` intervalle tooa supérieure à intervalle de 1 000 ms hello par défaut en incluant une `synctimeout` propriété dans la chaîne de connexion hello. Hello suivant montre un extrait de chaîne de connexion de cache StackExchange.Redis avec un `synctimeout` de 2 000 ms.
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. Veillez à l’aide de la version la plus récente de hello hello [package StackExchange.Redis NuGet](https://www.nuget.org/packages/StackExchange.Redis/). Il sont constamment des bogues corrigés dans toomake de code hello il tootimeouts plus robuste ayant la version la plus récente hello est donc important.
3. S’il existe des demandes de mise en route liées par des limitations de bande passante sur hello serveur ou client, il prendra plus de temps pour les toocomplete et entraînent des délais d’attente. toosee si le délai d’attente est en raison de la bande passante toonetwork sur le serveur de hello, consultez [la bande passante du côté serveur dépassée](#server-side-bandwidth-exceeded). toosee si le délai d’attente est en raison de la bande passante du réseau tooclient, consultez [la bande passante du côté Client dépassée](#client-side-bandwidth-exceeded).
4. Vous l’obtention de l’UC lié sur le serveur de hello ou hello
   
   * Vérifiez si vous êtes obtention lié par UC sur votre client qui peut provoquer l’hello demande toonot traitée dans hello `synctimeout` intervalle, ce qui entraîne un délai d’attente. Déplacement de tooa plus grande taille de client ou la répartition de charge de hello peut aider à toocontrol cela. 
   * Vérifiez si vous obtenez des UC lié sur le serveur de hello en surveillant hello `CPU` [mettre en cache les mesures de performance](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Requêtes entrantes pendant que Redis est lié à l’UC peut entraîner des demandes tootimeout. tooaddress cette hello distribuer la charge entre plusieurs partitions dans un cache premium ou mettre à niveau tooa plus grande taille ou le niveau tarifaire. Pour plus d’informations, consultez [Bande passante dépassée côté serveur](#server-side-bandwidth-exceeded).
5. Existe-t-il des commandes prend beaucoup de temps tooprocess sur le serveur de hello ? Long terme des commandes qui prenant beaucoup de temps tooprocess sur serveur redis hello peut entraîner des délais d’attente. Les commandes `mget` avec un nombre important de clés, `keys *` ou des scripts mal rédigés prennent notamment beaucoup de temps pour s’exécuter. Vous pouvez connecter l’instance de Cache Redis Azure tooyour à l’aide du client de redis-cli hello ou utilisez hello [Redis de Console](cache-configure.md#redis-console) et exécution hello [SlowLog](http://redis.io/commands/slowlog) toosee de commande s’il existe des demandes plus longue que prévu. Le serveur Redis et StackExchange.Redis sont optimisés pour traiter un grand nombre de petites requêtes plutôt qu’un nombre réduit de demandes volumineuses. Fractionner vos données en segments plus petits peut améliorer les choses. 
   
    Pour plus d’informations sur la connexion de point de terminaison SSL en Cache Azure Redis toohello à l’aide de redis-cli et stunnel, consultez hello [annonce du fournisseur état de Session ASP.NET pour Redis la préversion](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) billet de blog. Pour plus d’informations, consultez [SlowLog](http://redis.io/commands/slowlog).
6. Une charge élevée du serveur Redis peut provoquer des délais d’expiration. Vous pouvez surveiller la charge du serveur hello en surveillant hello `Redis Server Load` [mettre en cache les mesures de performance](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Une charge de serveur de 100 (valeur maximale) signifie que ce serveur de redis hello a été occupé, sans temps d’inactivité, le traitement des demandes. toosee si certaines requêtes sont prend toutes les fonctionnalité de serveur hello, exécutez la commande hello SlowLog comme décrit dans le paragraphe précédent hello. Pour plus d’informations, consultez [Utilisation élevée du processeur / charge importante du serveur](#high-cpu-usage-server-load).
7. Existait tout autre événement côté client hello qui ont pu causer un spots réseau ? Vérifiez sur le client hello (web, rôle de travail ou un VM Iaas) s’il y avait un événement, comme la mise à l’échelle de nombre hello d’instances du client vers le haut ou vers le bas ou le déploiement d’une nouvelle version du client de hello ou à l’échelle automatique est activé ? Dans nos tests, que nous avons constaté que la mise à l’échelle ou la mise à l’échelle vers le haut/bas peut entraîner une connectivité réseau sortantes peut être perdue pendant quelques secondes. Code de StackExchange.Redis est résilient toosuch les événements et se reconnectera. Pendant ce temps de reconnexion toutes les demandes dans la file d’attente hello peuvent expirer.
8. Existait une demande big précédant plusieurs petites requêtes toohello Cache Redis ayant expiré ? Hello paramètre `qs` d’erreur de hello message indique le nombre de requêtes ont été envoyé depuis le serveur de toohello hello client, mais n’avez pas encore traité une réponse. Cette valeur peut continuer d’augmenter car StackExchange.Redis utilise une seule connexion TCP et ne peut lire qu’une réponse à la fois. Même si hello premier délai d’attente, il n’arrête pas les données de salutation envoyées vers ou depuis le serveur de hello, et autres requêtes sont bloquées jusqu'à ce que cette opération terminée, à l’origine de délais d’expiration. Une solution consiste chance de hello toominimize des délais d’attente en garantissant que votre cache est suffisamment grand pour votre charge de travail et en fractionnant les grandes valeurs en plus petits. Une autre solution possible est toouse un pool de `ConnectionMultiplexer` des objets dans votre client et choisissez hello moins chargé `ConnectionMultiplexer` lors de l’envoi d’une nouvelle demande. Cela doit empêcher un délai d’attente unique de provoquer des autres délai d’attente de demandes tooalso.
9. Si vous utilisez `RedisSessionStateprovider`, vous avez définie correctement délai de nouvelle tentative hello. `retrytimeoutInMilliseconds` doit être supérieur à `operationTimeoutinMilliseonds`, sans quoi aucune nouvelle tentative ne se produit. Bonjour à l’exemple suivant `retrytimeoutInMilliseconds` a la valeur too3000. Pour plus d’informations, consultez [fournisseur d’état de Session ASP.NET pour le Cache Redis Azure](cache-aspnet-session-state-provider.md) et [comment toouse hello les paramètres de configuration de fournisseur d’état de Session et de fournisseur de caches de sortie](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration).

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. Vérifier l’utilisation de la mémoire sur le serveur de Cache Redis Azure hello par [analyse](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) `Used Memory RSS` et `Used Memory`. Si une stratégie d’éviction est en place, Redis démarre quand retirer des clés `Used_Memory` atteint hello la taille du cache. Dans l’idéal, `Used Memory RSS` doit être légèrement supérieur à `Used memory`. Une différence importante traduit une fragmentation de la mémoire (interne ou externe). Lorsque `Used Memory RSS` est inférieure à `Used Memory`, cela signifie que la partie de la mémoire cache de hello ont été permuté par système d’exploitation de hello. Dans ce cas, vous pouvez rencontrer des latences importantes. Car Redis n’a pas de contrôle sur les pages de toomemory, haute mappées comment ses allocations sont `Used Memory RSS` est souvent hello résultat d’un pic d’utilisation de mémoire. Lorsque Redis libère de la mémoire, mémoire de hello est rendue toohello allocateur et allocateur de hello peut ou peut ne pas donne hello mémoire toohello précédent système. Il peut y avoir des différences entre hello `Used Memory` la consommation de mémoire et de valeur comme indiqué par le système d’exploitation de hello. Il peut être dû fait toohello mémoire a été utilisée, publiée par Redis, mais pas donné précédent toohello système. toohelp atténuer les problèmes de mémoire vous pouvez effectuer hello comme suit.
   
   * Mettre à niveau hello cache tooa plus volumineux afin que vous n’exécutez pas aux limitations de mémoire sur le système de hello.
   * Définir des délais d’expiration sur les clés de hello afin que les valeurs plus anciens sont supprimés de façon proactive.
   * Hello hello de moniteur `used_memory_rss` métrique de cache. Lorsque cette valeur s’approche de taille hello de leur cache, vous êtes probablement toostart voir les problèmes de performances. Distribuer des données de hello sur plusieurs partitions si vous utilisez un cache premium, ou mettre à niveau tooa de cache de taille supérieure.
   
   Pour plus d’informations, consultez [pression de mémoire sur le serveur de hello](#memory-pressure-on-the-server).

## <a name="additional-information"></a>Informations supplémentaires
* [Que propose Cache Redis et quelle taille dois-je utiliser ?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [Comment puis-je évaluer et tester hello les performances de mon cache ?](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Comment exécuter des commandes Redis ?](cache-faq.md#how-can-i-run-redis-commands)
* [Comment toomonitor Cache Redis Azure](cache-how-to-monitor.md)

