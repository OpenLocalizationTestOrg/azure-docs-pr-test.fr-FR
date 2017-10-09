---
title: "persistance des données aaaHow tooconfigure Premium Azure Redis cache"
description: "Découvrez comment tooconfigure et gérer persistance des données de vos instances de Cache Redis Azure de niveau Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>La persistance des données tooconfigure Premium Azure Redis cache
Cache Redis Azure a différentes offres de cache qui fournissent une certaine flexibilité hello les choix de la taille du cache et de fonctionnalités, y compris les fonctionnalités de niveau Premium telles que le clustering, la persistance et la prise en charge du réseau virtuel. Cet article décrit comment persistance tooconfigure dans une prime Cache Redis Azure instance.

Pour plus d’informations sur d’autres fonctionnalités de cache premium, consultez [couche de présentation toohello Azure Redis Cache Premium](cache-premium-tier-intro.md).

## <a name="what-is-data-persistence"></a>Qu’est-ce que la persistance des données ?
[Persistance de redis](https://redis.io/topics/persistence) vous permet de toopersist les données stockées dans Redis. Vous pouvez également effectuer des captures instantanées et sauvegarder les données hello, que vous pouvez charger en cas de défaillance matérielle. Il s’agit d’un énorme avantage par rapport Basic ou niveau Standard où tous les hello les données est stockée en mémoire et il peut y avoir de perdre des données en cas de défaillance dans lequel les nœuds de Cache sont arrêtés. 

Cache Redis Azure offre la persistance de Redis à l’aide de hello suivant de modèles :

* **Persistance de RDB** -persistance de RDB lorsque (base de données Redis) est configuré, le Cache Redis Azure persiste un instantané du cache Redis de hello dans un format binaire toodisk selon une fréquence de sauvegarde peut être configurée de Redis. Si un événement catastrophique désactive hello principal et cache de réplica se produit, le cache de hello est reconstruit à l’aide d’instantané le plus récent hello. En savoir plus sur hello [avantages](https://redis.io/topics/persistence#rdb-advantages) et [inconvénients](https://redis.io/topics/persistence#rdb-disadvantages) de persistance de RDB.
* **Persistance d’UNEDE** -persistance d’UNEDE lorsque (ajouter un seul fichier) est configuré, le Cache Redis Azure enregistre chaque journal de tooa écriture opération qui est enregistré au moins une fois par seconde à un compte de stockage Azure. Si un événement catastrophique désactive hello principal et cache de réplica se produit, le cache de hello est reconstruit à l’aide d’opérations d’écriture stockée hello. En savoir plus sur hello [avantages](https://redis.io/topics/persistence#aof-advantages) et [inconvénients](https://redis.io/topics/persistence#aof-disadvantages) de persistance d’UNEDE.

Persistance est configurée de hello **nouveau Cache Redis** panneau pendant la création du cache et sur hello **menu ressource** pour premium existante met en cache.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Une fois que vous avez sélectionné un niveau tarifaire Premium, cliquez sur **Persistance Redis**.

![Persistance Redis][redis-cache-persistence]

Hello étapes dans la section suivante de hello décrivent comment tooconfigure persistance Redis sur votre nouveau cache premium. Une fois que la persistance de Redis est configuré, cliquez sur **créer** toocreate votre premium nouveau cache avec Redis persistance.

## <a name="enable-redis-persistence"></a>Activation de la persistance Redis

Redis la persistance est activée sur hello **Redis la persistance des données** panneau en choisissant soit **RDB** ou **UNEDE** persistance. Pour les nouveaux caches, ce panneau est accessible au cours du processus de création du cache hello, comme décrit dans la section précédente de hello. Pour les caches existants, hello **Redis la persistance des données** lame est accessible à partir de hello **menu ressource** pour votre cache.

![Paramètres Redis][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>Configuration de la persistance RDB

persistance de RDB tooenable, cliquez sur **RDB**. persistance de RDB toodisable sur un cache premium précédemment activé, cliquez sur **désactivé**.

![Persistance RDB Redis][redis-cache-rdb-persistence]

tooconfigure hello intervalle de sauvegarde, sélectionnez un **fréquence de sauvegarde** à partir de la liste déroulante de hello. Vous avez le choix entre **15 minutes**, **30 minutes**, **60 minutes**, **6 heures**, **12 heures** et **24 heures**. Cet intervalle commence le comptage vers le bas après l’opération de sauvegarde précédente hello terminée avec succès et quand il s’écoule une nouvelle sauvegarde est lancée.

Cliquez sur **compte de stockage** tooselect hello toouse de compte de stockage et choisissez soit hello **clé primaire** ou **clé secondaire** toouse de hello **stockage Clé** liste déroulante. Vous devez choisir un compte de stockage Bonjour même région que le cache de hello et un **stockage Premium** compte est recommandé, car le stockage premium a un débit plus élevé. 

> [!IMPORTANT]
> Si la clé de stockage hello pour votre compte de persistance est régénérée, vous devez reconfigurer la clé souhaitée hello hello **clé de stockage** liste déroulante.
> 
> 

Cliquez sur **OK** configuration de persistance toosave hello.

prochaine sauvegarde Hello (ou première sauvegarde pour les nouveaux caches) est lancée une fois que l’intervalle de fréquence de sauvegarde hello est écoulé.

## <a name="configure-aof-persistence"></a>Configuration de la persistance AOF

persistance d’UNEDE tooenable, cliquez sur **UNEDE**. persistance d’UNEDE toodisable sur un cache premium précédemment activé, cliquez sur **désactivé**.

![Persistance AOF Redis][redis-cache-aof-persistence]

persistance d’UNEDE tooconfigure, spécifiez un **premier compte de stockage**. Ce compte de stockage doit être Bonjour même région que le cache de hello et un **stockage Premium** compte est recommandé, car le stockage premium a un débit plus élevé. Vous pouvez éventuellement configurer un compte de stockage supplémentaire nommé **Deuxième compte de stockage**. Si un deuxième compte de stockage est configuré, hello écritures toohello réplica cache sont écrites toothis deuxième compte de stockage. Pour chaque compte de stockage configuré, choisissez soit hello **clé primaire** ou **clé secondaire** toouse de hello **clé de stockage** liste déroulante. 

> [!IMPORTANT]
> Si la clé de stockage hello pour votre compte de persistance est régénérée, vous devez reconfigurer la clé souhaitée hello hello **clé de stockage** liste déroulante.
> 
> 

Lors de la persistance UNEDE est activée, écrire le cache de toohello opérations sont enregistrées toohello désigné du compte de stockage (ou des comptes si vous avez configuré un deuxième compte de stockage). En cas de hello d’une défaillance catastrophique que prend deux vers le bas hello principal et le cache de réplica, hello stockée UNEDE journal est utilisé du cache de toorebuild hello.

## <a name="persistence-faq"></a>Forum aux questions sur la persistance
Hello liste suivante contient toocommonly des réponses aux questions sur la persistance du Cache Redis Azure.

* [Puis-je activer la persistance sur un cache créé précédemment ?](#can-i-enable-persistence-on-a-previously-created-cache)
* [Puis-je activer la persistance UNEDE et RDB à hello même temps ?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [Quel modèle de persistance dois-je choisir ?](#which-persistence-model-should-i-choose)
* [Que se passe-t-il si j’ai mis à l’échelle tooa une taille différente et la restauration d’une sauvegarde effectuée avant l’opération de mise à l’échelle de hello ?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>Persistance RDB
* [Puis-je modifier la fréquence de sauvegarde RDB hello après avoir créé le cache de hello ?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [Pourquoi, si la fréquence de sauvegarde RDB est de 60 minutes, y a-t-il un délai supérieur à 60 minutes entre les sauvegardes ?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [Que passe-t-il d’anciennes sauvegardes RDB toohello lorsqu’une nouvelle sauvegarde est effectuée ?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>Persistance AOF
* [Quand dois-je utiliser un deuxième compte de stockage ?](#when-should-i-use-a-second-storage-account)
* [La persistance AOF affecte-t-elle le débit, la latence ou les performances de mon cache ?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [Comment puis-je supprimer le compte de stockage deuxième hello ?](#how-can-i-remove-the-second-storage-account)
* [Qu’est-ce qu’une réécriture et comment affecte-t-elle mon cache ?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [À quoi dois-je attendre lors de la mise à l’échelle d’un cache avec la persistance AOF activée ?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [Comment sont organisées mes données AOF dans le stockage ?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>Puis-je activer la persistance sur un cache créé précédemment ?
Oui, la persistance Redis peut être configurée lors de la création du cache ou sur les caches Premium existants.

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>Puis-je activer la persistance UNEDE et RDB à hello même temps ?

Non, vous pouvez activer uniquement RDB ou UNEDE, mais pas les deux à hello même temps.

### <a name="which-persistence-model-should-i-choose"></a>Quel modèle de persistance dois-je choisir ?

Persistance d’UNEDE enregistre chaque tooa écriture du journal, qui a un impact sur le débit, persistance qui enregistre les sauvegardes en fonction de hello comparé RDB configuré d’intervalle de sauvegarde, avec un impact minimal sur les performances. Choisissez la persistance d’UNEDE si votre objectif principal est toominimize une perte de données, et vous pouvez gérer une diminution du débit de votre cache. Choisissez la persistance de RDB si vous le souhaitez toomaintain un débit optimal sur votre cache, mais toujours un mécanisme de récupération de données.

* En savoir plus sur hello [avantages](https://redis.io/topics/persistence#rdb-advantages) et [inconvénients](https://redis.io/topics/persistence#rdb-disadvantages) de persistance de RDB.
* En savoir plus sur hello [avantages](https://redis.io/topics/persistence#aof-advantages) et [inconvénients](https://redis.io/topics/persistence#aof-disadvantages) de persistance d’UNEDE.

Pour plus d’informations sur les performances lors de l’utilisation de persistance AOF, consultez [La persistance affecte-t-elle le débit, la latence ou les performances de mon cache ?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>Que se passe-t-il si j’ai mis à l’échelle tooa une taille différente et la restauration d’une sauvegarde effectuée avant l’opération de mise à l’échelle de hello ?

Pour la persistance RDB et AOF :

* Si vous avez mis à l’échelle tooa plus grande taille, il n’existe aucun impact.
* Si vous avez monté en tooa plus petite taille, et que vous avez personnalisé [bases de données](cache-configure.md#databases) qui est supérieur à hello [limite de bases de données](cache-configure.md#databases) pour votre nouvelle taille, dans les bases de données n’est pas restaurées. Pour en savoir plus, voir [Les paramètres personnalisés de mes bases de données sont-ils affectés au cours de la mise à l’échelle ?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Si vous avez à l’échelle tooa plus petite taille, et il n’est pas assez de place dans hello toohold de taille plus petite toutes les données de hello depuis la dernière clés de sauvegarde, hello seront supprimés pendant le processus de restauration hello, généralement à l’aide hello [allkeys-lru](http://redis.io/topics/lru-cache) éviction stratégie.

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>Puis-je modifier la fréquence de sauvegarde RDB hello après avoir créé le cache de hello ?
Oui, vous pouvez modifier la fréquence de sauvegarde hello pour la persistance RDB sur hello **Redis la persistance des données** panneau. Pour obtenir des instructions, consultez la page [Configuration de la persistance Redis](#configure-redis-persistence).

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>Pourquoi, si la fréquence de sauvegarde RDB est de 60 minutes, y a-t-il un délai supérieur à 60 minutes entre les sauvegardes ?
intervalle de fréquence de sauvegarde Hello RDB persistance ne démarre pas jusqu'à ce que le processus de sauvegarde précédente hello est bien terminée. Si la fréquence de sauvegarde hello est de 60 minutes, et il prend une toosuccessfully de 15 minutes de processus de sauvegarde complète, de sauvegarde suivant hello ne démarre pas tant que 75 minutes après hello heure de début de sauvegarde précédente de hello.

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>Que passe-t-il d’anciennes sauvegardes RDB toohello lorsqu’une nouvelle sauvegarde est effectuée ?
Toutes les sauvegardes de persistance RDB à l’exception de hello plus récente sont automatiquement supprimés. Cette suppression peut ne pas avoir lieu immédiatement, mais les anciennes sauvegardes ne sont pas conservées indéfiniment.


### <a name="when-should-i-use-a-second-storage-account"></a>Quand dois-je utiliser un deuxième compte de stockage ?

Vous devez utiliser un deuxième compte de stockage pour la persistance d’UNEDE lorsque vous pensez que vous avez le plus élevé que les opérations de jeu attendu sur le cache de hello.  La configuration de compte de stockage secondaire hello garantit que votre cache n’atteint pas les limites de bande passante de stockage.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>La persistance AOF affecte-t-elle le débit, la latence ou les performances de mon cache ?

Persistance d’UNEDE affecte le débit en environ 15 à 20 % lorsque le cache de hello est sous charge maximale (UC et charge du serveur à la fois sous 90 %). Il doit être pas les problèmes de latence lorsque le cache de hello est dans ces limites. Toutefois, le cache de hello atteint ces limites plus tôt avec UNEDE activée.

### <a name="how-can-i-remove-hello-second-storage-account"></a>Comment puis-je supprimer le compte de stockage deuxième hello ?

Vous pouvez supprimer le compte de stockage secondaire hello UNEDE persistance en définissant le deuxième compte de stockage hello toobe même hello en tant que premier compte de stockage hello. Pour obtenir des instructions, consultez la page [Configuration de la persistance AOF](#configure-aof-persistence).

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>Qu’est-ce qu’une réécriture et comment affecte-t-elle mon cache ?

Lorsque le fichier UNEDE de hello est suffisante, une réécriture est automatiquement mise en attente sur le cache de hello. fichier d’UNEDE hello Hello réécriture est redimensionné avec hello nombre minimal de jeu de données en cours d’opérations nécessaires toocreate hello. Au cours de réécritures, attendre tooreach des limites de performances plus tôt en particulier lors du traitement de grands jeux de données. Réécritures inférieur produisent souvent comme fichier d’UNEDE hello devient supérieure, mais prendra beaucoup de temps quand il se produit.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>À quoi dois-je attendre lors de la mise à l’échelle d’un cache avec la persistance AOF activée ?

Si le fichier d’UNEDE hello au moment de hello de mise à l’échelle est suffisamment importante, puis attendez hello échelle opération tootake plus longtemps que prévu, car il sera recharger les fichiers hello après mise à l’échelle.

Pour plus d’informations sur la mise à l’échelle, consultez [que se passe-t-il si j’ai mis à l’échelle tooa une taille différente et la restauration d’une sauvegarde effectuée avant l’opération de mise à l’échelle de hello ?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>Comment sont organisées mes données AOF dans le stockage ?

Les données stockées dans des fichiers UNEDE sont divisées en plusieurs objets BLOB de pages par des performances de l’enregistrement de hello données toostorage tooincrease du nœud. Hello tableau suivant affiche les objets BLOB de pages combien est utilisés pour chaque niveau de tarification :

| Niveau Premium | Objets blob |
|--------------|-------|
| P1           | 4 par partition    |
| P2           | 8 par partition    |
| P3           | 16 par partition   |
| P4           | 20 par partition   |

Lorsque le clustering est activé, chaque partition dans le cache de hello possède son propre ensemble d’objets BLOB de page, comme indiqué dans le tableau précédent de hello. Par exemple, un cache P2 avec trois partitions distribue son fichier AOF entre 24 objets blob de pages (8 objets blob par partition, avec 3 partitions).

Après une réécriture, deux jeux de fichiers AOF se trouvent dans le stockage. Réécritures se produisent en arrière-plan de hello et ajoutez toohello premier jeu de fichiers, alors que le jeu qui sont envoyés du cache de toohello au cours de réécriture de hello ajoutent toohello deuxième jeu. Une sauvegarde est temporairement stockée pendant les réécritures en cas d’échec, mais elle est immédiatement supprimée à la fin de la réécriture.


## <a name="next-steps"></a>Étapes suivantes
Découvrez comment mettre en cache des fonctionnalités par toouse plus premium.

* [Couche de présentation toohello Azure Redis Cache Premium](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
