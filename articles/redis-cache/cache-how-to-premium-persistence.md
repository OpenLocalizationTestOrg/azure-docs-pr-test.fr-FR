---
title: "Comment configurer la persistance des données pour un Cache Redis Azure Premium"
description: "Découvrez comment configurer et gérer la persistance des données pour vos instances de Cache Redis Azure de niveau Premium"
services: redis-cache
documentationcenter: 
author: wesmc7777
manager: cfowler
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: wesmc
ms.openlocfilehash: 270158bbf85a58a48a367a091ad2b09a9d114b2b
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-configure-data-persistence-for-a-premium-azure-redis-cache"></a>Comment configurer la persistance des données pour un Cache Redis Azure Premium
Le Cache Redis Azure offre différents types de caches permettant de choisir en toute flexibilité parmi plusieurs tailles et fonctionnalités de caches en toute flexibilité, notamment les fonctionnalités de couche Premium telles que le clustering, la persistance et la prise en charge du réseau virtuel. Cet article décrit comment configurer la persistance dans une instance Premium de Cache Redis Azure.

Pour plus d’informations sur les autres fonctionnalités du cache Premium, consultez [Introduction au niveau Premium du Cache Redis Azure](cache-premium-tier-intro.md).

## <a name="what-is-data-persistence"></a>Qu’est-ce que la persistance des données ?
La [persistance Redis](https://redis.io/topics/persistence) vous permet de conserver les données stockées dans Redis. Vous pouvez également prendre des instantanés et sauvegarder les données que vous pouvez charger en cas de défaillance matérielle. Il s’agit d’un avantage substantiel par rapport au niveau De base ou Standard, où toutes les données sont stockées en mémoire et il existe un risque de perte de données en cas de défaillance des nœuds de cache. 

Le Cache Redis Azure offre la persistance Redis à l’aide des modèles suivants :

* **Persistance RDB** : Quand la persistance RDB (base de données Redis) est configurée, le Cache Redis Azure conserve un instantané du cache Redis dans un format binaire Redis sur le disque selon une fréquence de sauvegarde configurable. Si un événement catastrophique se produit et provoque la désactivation du cache principal et du réplica, le cache est reconstruit à l’aide de l’instantané le plus récent. Découvrez-en plus sur les [avantages](https://redis.io/topics/persistence#rdb-advantages) et les [inconvénients](https://redis.io/topics/persistence#rdb-disadvantages) de la persistance RDB.
* **Persistance AOF** : Lorsque la persistance AOF (Append Only File) est configurée, le Cache Redis Azure enregistre chaque opération d’écriture dans un journal qui est enregistré au moins une fois par seconde dans un compte de stockage Azure. Si un événement catastrophique se produit et provoque la désactivation du cache principal et du réplica, le cache est reconstruit à l’aide des opérations d’écriture stockées. Découvrez-en plus sur les [avantages](https://redis.io/topics/persistence#aof-advantages) et les [inconvénients](https://redis.io/topics/persistence#aof-disadvantages) de la persistance AOF.

La persistance est configurée à partir du panneau **Nouveau Cache Redis** lors de la création du cache et du **menu Ressource** pour les caches Premium existants.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Une fois que vous avez sélectionné un niveau tarifaire Premium, cliquez sur **Persistance Redis**.

![Persistance Redis][redis-cache-persistence]

Les étapes de la section suivante décrivent comment configurer la persistance Redis sur votre nouveau cache Premium. Une fois la persistance Redis configurée, cliquez sur **Créer** pour créer votre cache Premium avec la persistance Redis.

## <a name="enable-redis-persistence"></a>Activation de la persistance Redis

Le panneau **Persistance des données Redis** permet de configurer la persistance Redis en sélectionnant la persistance **RDB** ou **AOF**. Pour les nouveaux caches, ce panneau est accessible pendant la création du cache, comme décrit dans la section précédente. Pour les caches existants, le panneau **Persistance des données Redis** est accessible à partir du **menu Ressource** de votre cache.

![Paramètres Redis][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>Configuration de la persistance RDB

Pour activer la persistance RDB, cliquez sur **RDB**. Pour désactiver la persistance RDB sur un cache Premium précédemment activé, cliquez sur **Désactivé**.

![Persistance RDB Redis][redis-cache-rdb-persistence]

Pour configurer l’intervalle de sauvegarde, sélectionnez une **Fréquence de sauvegarde** dans la liste déroulante. Vous avez le choix entre **15 minutes**, **30 minutes**, **60 minutes**, **6 heures**, **12 heures** et **24 heures**. Cet intervalle débute au moment où l’opération de sauvegarde précédente s’est terminée correctement. Une fois l’intervalle écoulé, une nouvelle sauvegarde est lancée.

Cliquez sur **Compte de stockage** pour sélectionner le compte de stockage à utiliser, puis, dans la liste déroulante **Clé de stockage**, choisissez d’utiliser la **Clé primaire** ou la **Clé secondaire**. Vous devez choisir un compte de stockage situé dans la même région que le cache. Un compte **Stockage Premium** est recommandé, car ce type de stockage offre un débit plus élevé. 

> [!IMPORTANT]
> Si la clé de stockage pour votre compte de persistance est régénérée, vous devez reconfigurer la clé souhaitée dans la liste déroulante **Clé de stockage** .
> 
> 

Cliquez sur **OK** pour enregistrer la configuration de persistance.

La sauvegarde suivante (ou première sauvegarde pour les nouveaux caches) est lancée une fois que l'intervalle de fréquence de sauvegarde est écoulé.

## <a name="configure-aof-persistence"></a>Configuration de la persistance AOF

Pour activer la persistance AOF, cliquez sur **AOF**. Pour désactiver la persistance AOF sur un cache Premium précédemment activé, cliquez sur **Désactivé**.

![Persistance AOF Redis][redis-cache-aof-persistence]

Pour configurer la persistance AOF, spécifiez un **Premier compte de stockage**. Ce compte de stockage doit se trouver dans la même région que le cache. Un compte **Stockage Premium** est recommandé, car ce type de stockage offre un débit plus élevé. Vous pouvez éventuellement configurer un compte de stockage supplémentaire nommé **Deuxième compte de stockage**. Si un deuxième compte de stockage est configuré, les opérations d’écriture dans le cache de réplica sont enregistrées dans ce deuxième compte de stockage. Pour chaque compte de stockage configuré, sélectionnez la **clé primaire** ou **clé secondaire** à utiliser dans la liste déroulante **Clé de stockage**. 

> [!IMPORTANT]
> Si la clé de stockage pour votre compte de persistance est régénérée, vous devez reconfigurer la clé souhaitée dans la liste déroulante **Clé de stockage** .
> 
> 

Lorsque la persistance AOF est activée, les opérations d’écriture dans le cache sont enregistrées dans le compte de stockage désigné (ou les comptes si vous avez configuré un deuxième compte de stockage). En cas de défaillance catastrophique affectant à la fois le cache principal et le réplica, le journal AOF stocké est utilisé pour reconstruire le cache.

## <a name="persistence-faq"></a>Forum aux questions sur la persistance
La liste suivante présente différentes réponses aux questions les plus fréquemment posées sur la persistance du Cache Redis Azure.

* [Puis-je activer la persistance sur un cache créé précédemment ?](#can-i-enable-persistence-on-a-previously-created-cache)
* [Puis-je activer la persistance AOF et RDB en même temps ?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [Quel modèle de persistance dois-je choisir ?](#which-persistence-model-should-i-choose)
* [Que se passe-t-il si j’ai mis à l’échelle vers une taille différente et si une sauvegarde antérieure à l’opération de mise à l’échelle, est restaurée ?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>Persistance RDB
* [Puis-je modifier la fréquence de sauvegarde RDB après avoir créé le cache ?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [Pourquoi, si la fréquence de sauvegarde RDB est de 60 minutes, y a-t-il un délai supérieur à 60 minutes entre les sauvegardes ?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [Qu’advient-il des anciennes sauvegardes RDB quand une nouvelle sauvegarde est effectuée ?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>Persistance AOF
* [Quand dois-je utiliser un deuxième compte de stockage ?](#when-should-i-use-a-second-storage-account)
* [La persistance AOF affecte-t-elle le débit, la latence ou les performances de mon cache ?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [Comment puis-je supprimer le deuxième compte de stockage ?](#how-can-i-remove-the-second-storage-account)
* [Qu’est-ce qu’une réécriture et comment affecte-t-elle mon cache ?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [À quoi dois-je attendre lors de la mise à l’échelle d’un cache avec la persistance AOF activée ?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [Comment sont organisées mes données AOF dans le stockage ?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>Puis-je activer la persistance sur un cache créé précédemment ?
Oui, la persistance Redis peut être configurée lors de la création du cache ou sur les caches Premium existants.

### <a name="can-i-enable-aof-and-rdb-persistence-at-the-same-time"></a>Puis-je activer la persistance AOF et RDB en même temps ?

Non, vous pouvez uniquement activer RDB ou AOF, mais pas les deux en même temps.

### <a name="which-persistence-model-should-i-choose"></a>Quel modèle de persistance dois-je choisir ?

La persistance AOF enregistre chaque écriture dans un journal, ce qui a un impact sur le débit, par rapport à la persistance RDB qui enregistre des sauvegardes à l’intervalle de sauvegarde configuré, avec un impact minimal sur les performances. Choisissez la persistance AOF si votre objectif principal est de minimiser la perte de données et si vous pouvez gérer une réduction du débit de votre cache. Choisissez la persistance RDB si vous souhaitez maintenir un débit optimal de votre cache mais avez quand même besoin d’un mécanisme de récupération de données.

* Découvrez-en plus sur les [avantages](https://redis.io/topics/persistence#rdb-advantages) et les [inconvénients](https://redis.io/topics/persistence#rdb-disadvantages) de la persistance RDB.
* Découvrez-en plus sur les [avantages](https://redis.io/topics/persistence#aof-advantages) et les [inconvénients](https://redis.io/topics/persistence#aof-disadvantages) de la persistance AOF.

Pour plus d’informations sur les performances lors de l’utilisation de persistance AOF, consultez [La persistance affecte-t-elle le débit, la latence ou les performances de mon cache ?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation"></a>Que se passe-t-il si j’ai mis à l’échelle vers une taille différente et si une sauvegarde antérieure à l’opération de mise à l’échelle, est restaurée ?

Pour la persistance RDB et AOF :

* Si vous avez mis à l’échelle vers une plus grande taille, cela n’a aucun impact.
* Si vous avez mis à l’échelle vers une taille plus petite et que vous avez un paramètre personnalisé de [bases de données](cache-configure.md#databases) supérieur à la [limite des bases de données](cache-configure.md#databases) pour votre nouvelle taille, les données de ces bases de données ne sont pas restaurées. Pour en savoir plus, voir [Les paramètres personnalisés de mes bases de données sont-ils affectés au cours de la mise à l’échelle ?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Si vous avez mis à l’échelle vers une plus petite taille et que l’espace est insuffisant pour contenir toutes les données issues de la dernière sauvegarde, les clés sont supprimées lors du processus de restauration, généralement à l’aide de la stratégie d’éviction [allkeys-lru](http://redis.io/topics/lru-cache) .

### <a name="can-i-change-the-rdb-backup-frequency-after-i-create-the-cache"></a>Puis-je modifier la fréquence de sauvegarde RDB après avoir créé le cache ?
Oui, vous pouvez modifier la fréquence de sauvegarde pour la persistance RDB dans le panneau **Persistance des données Redis**. Pour obtenir des instructions, consultez la page [Configuration de la persistance Redis](#configure-redis-persistence).

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>Pourquoi, si la fréquence de sauvegarde RDB est de 60 minutes, y a-t-il un délai supérieur à 60 minutes entre les sauvegardes ?
L’intervalle de fréquence de sauvegarde avec la persistance RDB ne démarre qu’une fois le processus de sauvegarde précédent terminé. Si la fréquence de sauvegarde est de 60 minutes et que l’exécution d’un processus de sauvegarde prend 15 minutes, la sauvegarde suivante ne démarre que 75 minutes après l’heure de début de la sauvegarde précédente.

### <a name="what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made"></a>Qu’advient-il des anciennes sauvegardes RDB quand une nouvelle sauvegarde est effectuée ?
Toutes les sauvegardes avec la persistance RDB à l’exception de la plus récente sont supprimées automatiquement. Cette suppression peut ne pas avoir lieu immédiatement, mais les anciennes sauvegardes ne sont pas conservées indéfiniment.


### <a name="when-should-i-use-a-second-storage-account"></a>Quand dois-je utiliser un deuxième compte de stockage ?

Vous devez utiliser un deuxième compte de stockage pour la persistance AOF lorsque vous pensez que vous avez plus d’opérations que prévues définies sur le cache.  La configuration du deuxième compte de stockage permet de vous assurer que votre cache n’atteindra pas les limites de bande passante de stockage.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>La persistance AOF affecte-t-elle le débit, la latence ou les performances de mon cache ?

La persistance AOF affecte le débit d’environ 15 à 20 % lorsque le cache n’a pas atteint la charge maximale (charges de l’UC et du serveur inférieures à 90 %). Il ne devrait pas y avoir de problèmes de latence lorsque le cache se trouve dans ces limites. Toutefois, le cache atteindra plus rapidement ces limites avec la persistance AOF activée.

### <a name="how-can-i-remove-the-second-storage-account"></a>Comment puis-je supprimer le deuxième compte de stockage ?

Vous pouvez supprimer le compte de stockage secondaire pour la persistance AOF en définissant le deuxième compte de stockage de manière à ce qu’il soit identique au premier compte de stockage. Pour obtenir des instructions, consultez la page [Configuration de la persistance AOF](#configure-aof-persistence).

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>Qu’est-ce qu’une réécriture et comment affecte-t-elle mon cache ?

Lorsque le fichier AOF devient suffisamment volumineux, une réécriture est automatiquement mise en file d’attente dans le cache. La réécriture redimensionne le fichier AOF avec l’ensemble minimal d’opérations nécessaires pour créer le jeu de données en cours. Durant les réécritures, attendez-vous à atteindre plus rapidement les limites de performances, en particulier lors du traitement de grands jeux de données. Les réécritures s’effectueront moins souvent au fur et à mesure que le fichier AOF deviendra volumineux, mais elles prendront un temps considérable le cas échéant.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>À quoi dois-je attendre lors de la mise à l’échelle d’un cache avec la persistance AOF activée ?

Si le fichier AOF est particulièrement volumineux au moment de la mise à l’échelle, attendez-vous à ce que l’opération de mise à l’échelle soit plus longue que prévue, étant donné qu’elle rechargera le fichier une fois la mise à l’échelle terminée.

Pour en savoir plus sur la mise à l’échelle, consultez [Que se passe-t-il si j’ai mis à l’échelle vers une taille différente et si une sauvegarde antérieure à l’opération de mise à l’échelle est restaurée ?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>Comment sont organisées mes données AOF dans le stockage ?

Les données stockées dans des fichiers AOF sont divisées en plusieurs objets blob de pages par nœud afin d’augmenter les performances d’enregistrement des données dans le stockage. Le tableau suivant montre comment de nombreux objets blob de pages sont utilisés pour chaque niveau tarifaire :

| Niveau Premium | Objets blob |
|--------------|-------|
| P1           | 4 par partition    |
| P2           | 8 par partition    |
| P3           | 16 par partition   |
| P4           | 20 par partition   |

Lorsque le clustering est activé, chaque partition dans le cache a son propre ensemble d’objets blob de pages, comme indiqué dans le tableau précédent. Par exemple, un cache P2 avec trois partitions distribue son fichier AOF entre 24 objets blob de pages (8 objets blob par partition, avec 3 partitions).

Après une réécriture, deux jeux de fichiers AOF se trouvent dans le stockage. Les réécritures s’effectuent en arrière-plan et s’ajoutent au premier jeu de fichiers, alors que les opérations définies qui sont envoyées dans le cache lors de la réécriture s’ajoutent au deuxième jeu. Une sauvegarde est temporairement stockée pendant les réécritures en cas d’échec, mais elle est immédiatement supprimée à la fin de la réécriture.


## <a name="next-steps"></a>étapes suivantes
Découvrez comment utiliser davantage de fonctionnalités de cache de niveau Premium.

* [Introduction au niveau Premium du Cache Redis Azure](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
