---
title: "niveau d’Azure Redis Cache Premium aaaIntroduction toohello | Documents Microsoft"
description: "Découvrez comment toocreate et gérer la persistance de Redis, le clustering de Redis et prise en charge de réseau virtuel pour vos instances de Cache Redis Azure de niveau Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Couche de présentation toohello Azure Redis Cache Premium
Cache Redis Azure est un cache distribué géré qui vous permet de générer des applications hautement évolutives et réactives en fournissant un accès super rapide des données tooyour. 

Hello que nouvelle couche Premium est une couche de prêt Enterprise, qui inclut toutes les fonctionnalités de niveau Standard hello et plus d’informations, telles que les meilleures performances, les charges de travail plus grandes, la récupération d’urgence, importation/exportation et une sécurité renforcée. Continuer toolearn lecture plus d’informations sur les fonctionnalités de niveau de cache Premium hello hello.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Meilleures performances par rapport à tooStandard ou niveau de base
**Amélioration des performances par rapport au niveau Standard ou De base.** Les caches de niveau Premium de hello sont déployés sur le matériel qui possède des processeurs plus rapides et offre de meilleures performances que toohello, Basic ou niveau Standard. Les caches de niveau Premium ont un débit supérieur et des latences moindres. 

**Débit pour hello même Cache taille est plus élevée dans Premium en tant que couche de tooStandard comparés.** Par exemple, le débit hello un 53 Go P4 cache (Premium) est 250K des demandes par seconde en tant que too150K comparés pour C6 (Standard).

Pour plus d’informations sur la taille, le débit et la bande passante des caches Premium, voir le [Forum aux questions sur le Cache Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Persistance des données Redis
niveau Premium de Hello vous permet de données du cache de hello toopersist dans un compte de stockage Azure. Dans un cache de base/Standard toutes les données hello est stocké uniquement dans la mémoire. En cas de problème lié à l’infrastructure sous-jacente, il existe un risque de perte de données. Nous recommandons d’utiliser la fonctionnalité de persistance des données Redis hello dans la résilience hello Premium couche tooincrease contre la perte de données. Le Cache Redis Azure propose des options RDB et AOF (à venir) de [persistance Redis](http://redis.io/topics/persistence). 

Pour obtenir des instructions sur la configuration de la persistance, consultez [la persistance tooconfigure cache Redis Azure Premium](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Cluster Redis
Si vous souhaitez les caches toocreate supérieure à 53 Go ou tooshard données sur plusieurs nœuds de Redis, vous pouvez utiliser Redis clustering qui est disponible dans le niveau Premium de hello. Chaque nœud se compose d’une paire de caches principal/réplica géré par Azure pour la haute disponibilité. 

**Le clustering Redis permet un débit et une capacité d’évolutivité maximum.** Débit augmente de façon linéaire lorsque vous augmentez le nombre de hello de partitions (nœuds) dans un cluster de hello. par exemple Si vous créez un cluster P4 de 10 partitions, le débit disponible hello est 250K * 10 = 2,5 millions de requêtes par seconde. Consultez hello [Azure Redis Cache-FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) pour plus d’informations sur la taille, le débit et la bande passante avec des caches de niveau premium.

tooget a démarré avec le clustering, consultez [comment tooconfigure clustering Premium Azure Redis cache](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Amélioration de la sécurité et de l’isolation
Créé dans la couche de base ou Standard hello les caches sont accessibles sur hello internet public. Accès toohello de que cache est limité en fonction de la clé d’accès hello. Avec le niveau de hello Premium, vous pouvez davantage garantir que seuls les clients dans un réseau spécifié peuvent accéder à hello du Cache. Vous pouvez déployer le Cache Redis dans un [réseau virtuel Azure (VNet)](https://azure.microsoft.com/services/virtual-network/). Vous pouvez utiliser toutes les fonctionnalités de hello de réseau virtuel tels que les sous-réseaux, les stratégies de contrôle d’accès et les autres toofurther fonctionnalités restreignent l’accès tooRedis.

Pour plus d’informations, consultez [comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>Importation/Exportation
Importation/exportation est une opération de gestion de données de Cache Redis Azure qui vous permet de tooimport données dans le Cache Redis Azure ou exporter des données à partir du Cache Redis Azure par l’importation et exportation d’un instantané de base de données de Cache Redis (RDB) à partir de premium cache tooa objet blob de pages dans Azure Compte de stockage. Cela vous permet de toomigrate entre différentes instances de Cache Redis Azure ou remplir le cache de hello avec les données avant des utiliser.

Importation peut être utilisé toobring Redis les compatibles RDB fichier (s) à partir de n’importe quel serveur Redis en cours d’exécution dans n’importe quel cloud ou l’environnement, y compris Redis en cours d’exécution sur n’importe quel fournisseur de cloud comme Amazon Web Services et d’autres utilisateurs, Windows ou Linux. L’importation de données est un toocreate facilement un cache de données prédéfinis. Pendant le processus d’importation hello, le Cache Redis Azure charge les fichiers RDB hello depuis le stockage Azure en mémoire, puis insère les clés hello dans le cache de hello.

Exportation vous permet des données de hello tooexport stockées dans le Cache Redis Azure tooRedis compatible RDB ou les fichiers. Vous pouvez utiliser ces données toomove de fonctionnalité à partir d’un Cache Redis Azure instance tooanother ou tooanother Redis server. Au cours du processus d’exportation hello, un fichier temporaire est créé sur hello VM que hôtes hello l’instance de serveur de Cache Redis Azure et hello fichier téléchargé toohello désigné du compte de stockage. Lors de l’opération d’exportation hello se termine avec l’état de réussite ou l’échec, le fichier temporaire de hello est supprimé.

Pour plus d’informations, consultez [comment tooimport des données dans et exporter des données à partir du Cache Redis Azure](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Reboot
niveau de Hello premium vous permet de tooreboot un ou plusieurs nœuds de votre cache à la demande. Cela vous permet de tootest votre application pour assurer la résilience en cas de hello d’un échec. Vous pouvez redémarrer hello suivant de nœuds.

* Nœud master de votre cache
* Nœud subordonné de votre cache
* Nœuds master et subordonné de votre cache
* Lorsque vous utilisez un cache premium avec le clustering, vous pouvez redémarrer hello master, esclave ou les deux nœuds pour les partitions dans le cache de hello

Pour plus d’informations, consultez [Redémarrage](cache-administration.md#reboot) et le [Forum aux questions sur le redémarrage](cache-administration.md#reboot-faq).

>[!NOTE]
>La fonctionnalité de redémarrage est à présent activée pour tous les niveaux de Cache Redis Azure.
>
>

## <a name="schedule-updates"></a>Planifier les mises à jour
fonctionnalité de mises à jour planifiées Hello vous permet de toodesignate une fenêtre de maintenance pour votre cache. Lors de la fenêtre de maintenance hello est spécifié, les mises à jour du serveur Redis sont effectuées au cours de cette fenêtre. toodesignate une fenêtre de maintenance, sélectionnez les jours de hello souhaité et spécifiez l’heure de début de fenêtre de maintenance hello pour chaque jour. Notez que l’heure de la fenêtre maintenance hello est au format UTC. 

Pour plus d’informations, consultez [Planification de mises à jour](cache-administration.md#schedule-updates) et le [Forum aux questions de la planification des mises à jour](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Redis uniquement les mises à jour sont effectuées au cours de la fenêtre de maintenance planifiée hello de serveur. fenêtre de maintenance Hello ne s’applique pas les mises à jour tooAzure ou met à jour de système d’exploitation de l’ordinateur virtuel toohello.
> 
> 

## <a name="geo-replication"></a>Géoréplication

La **Géoréplication** fournit un mécanisme de lien de deux instances de Cache Redis Azure de niveau Premium. Un cache est désigné comme le cache de lié principal hello et hello autre en tant que cache de lié secondaire hello. cache lié de Hello secondaire devient en lecture seule, et les données toohello écrit le cache principal est répliquée toohello cache lié secondaire. Cette fonctionnalité peut être utilisé tooreplicate un cache entre les régions Azure.

Pour plus d’informations, consultez [comment tooconfigure géo-réplication Azure Redis cache](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>niveau de tooscale toohello premium
niveau premium toohello tooscale simplement choisir un des niveaux de premium hello Bonjour **modification tarification** panneau. Vous pouvez également faire évoluer votre niveau premium de toohello de cache à l’aide de PowerShell et l’interface CLI. Pour obtenir des instructions, consultez [comment tooScale Cache Redis Azure](cache-how-to-scale.md) et [comment tooautomate une opération de mise à l’échelle](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Étapes suivantes
Créer un cache et Explorer les nouvelles fonctionnalités de niveau premium hello.

* [La persistance tooconfigure Premium Azure Redis cache](cache-how-to-premium-persistence.md)
* [Comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache](cache-how-to-premium-vnet.md)
* [Comment tooconfigure clustering Premium Azure Redis cache](cache-how-to-premium-clustering.md)
* [Comment tooimport des données dans et exporter des données à partir du Cache Redis Azure](cache-how-to-import-export-data.md)
* [Comment tooadminister Cache Redis Azure](cache-administration.md)

