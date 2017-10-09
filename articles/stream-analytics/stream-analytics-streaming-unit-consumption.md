---
title: "Analytique de flux de données Azure : Optimiser vos unités de diffusion en continu de toouse travail efficacement | Documents Microsoft"
description: "Meilleures pratiques en matière de requêtes pour la mise à l’échelle et les performances dans Azure Stream Analytics."
keywords: "unité de streaming, performance des requêtes"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a>Optimiser vos unités de diffusion en continu de toouse travail efficacement

Analytique de flux de données Azure regroupe les performances de hello « weight » de l’exécution d’un travail en unités de diffusion en continu (SUs). SUs représentent les ressources informatiques hello qui sont consommé tooexecute un travail. SUs fournissent un événement relatif hello toodescribe moyen en fonction de la mesure du processeur, mémoire, la capacité de traitement et lire et écrire des taux. Cette capacité vous pouvez vous concentrer sur la logique de requête de hello et supprime vous d’avoir tooknow stockage niveau considérations sur les performances, allocation de mémoire pour votre travail manuellement et approximative hello UC core-nombre nécessaire toorun votre travail en temps voulu.

## <a name="how-many-sus-are-required-for-a-job"></a>Combien d’unités de streaming sont requises pour un travail ?

Nombre hello de SUs requis pour un travail particulier le choix dépend de la configuration de partitions hello pour les entrées de hello et une requête de hello est défini dans le travail de hello. Hello **échelle** panneau vous permet de tooset hello droite nombre de SUs. Il s’agit d’une meilleure pratique tooallocate SUs plus que nécessaire. moteur de traitement de flux de données Analytique Hello optimise les demandes de latence et débit au coût hello d’allocation de mémoire supplémentaire.

En règle générale, hello est préférable toostart avec 6 SUs pour les requêtes qui n’utilisent pas *PARTITION BY*. Puis déterminer hello idéale en utilisant une méthode d’évaluation et d’erreurs dans lequel vous modifiez le nombre de hello de SUs une fois que vous transmettez des quantités représentatives de données et examinez les métriques d’utilisation hello SU %.

Analytique de flux de données Azure conserve les événements dans une fenêtre appelée hello « réorganiser les mémoires tampons » avant de commencer tout traitement. Les événements sont triés dans la fenêtre de commande hello par heure et les opérations suivantes sont effectuées sur les événements de hello rapprochée triée. Réorganisation des événements par heure garantit cet opérateur hello a une visibilité dans tous les événements hello Bonjour stipulés laps de temps. Il permet également d’opérateur de hello effectuer le traitement requis de hello et produire une sortie. Un effet secondaire de ce mécanisme est que le traitement est retardé par durée hello de fenêtre de commande hello. encombrement de mémoire Hello du travail hello (qui affecte la consommation SU) est une fonction de la taille de hello de ce nombre réorganiser les fenêtres et hello d’événements qu’il contient.

> [!NOTE]
> Quand un nombre de lecteurs hello change pendant les mises à niveau de la tâche, avertissements temporaires sont écrits tooaudit journaux. Les travaux Stream Analytics récupèrent automatiquement de ces problèmes temporaires.

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a>Causes courantes d’une mémoire élevée pour une utilisation élevée des unités de streaming lors de l’exécution de travaux

### <a name="high-cardinality-for-group-by"></a>Cardinalité élevée pour GROUP BY

utilisation de la mémoire de travail de hello détermine la cardinalité Hello d’événements entrants.

Par exemple, dans `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello numéro associé **cluster** est cardinalité hello de requête de hello.

toomitigate problèmes provoqués par une cardinalité élevée, monter en charge les requêtes hello en augmentant les partitions à l’aide de **PARTITION BY**.

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

Hello nombre de *cluster* est cardinalité hello de GROUP BY ici.

Une fois la requête de hello est partitionnée, il est réparti sur plusieurs nœuds. Par conséquent, nombre de hello d’événements arrivant dans chaque nœud est réduit, ce qui réduit à son tour taille hello de mémoire tampon de commande hello. Vous devez également partitionner les Event Hubs par partitionid.

### <a name="high-unmatched-event-count-for-join"></a>Nombre élevée d’événements sans correspondance pour JOIN

nombre Hello d’événements sans correspondance dans une jointure affecte l’utilisation de la mémoire de requête de hello hello. Par exemple, effectuer une requête qui recherche nombre hello toofind d’impressions de publicités qui génère des clics :

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

Dans ce scénario, il se peut qu’il y ait de nombreuses annonces affichées et que peu de clics soient générés. Un de cet résultats nécessiterait hello travail tookeep tous les événements hello dans la fenêtre de temps hello. quantité Hello de mémoire consommée est le taux de taille et les événements de fenêtre toohello proportionnel. 

toomitigate cette situation, la montée en puissance parallèle requête hello en augmentant les partitions à l’aide de PARTITION BY. 

Une fois la requête de hello est partitionnée, il est réparti sur plusieurs nœuds de traitement. Par conséquent, nombre de hello d’événements arrivant dans chaque nœud est réduit, ce qui réduit à son tour taille hello de mémoire tampon de commande hello.

### <a name="large-number-of-out-of-order-events"></a>Nombre élevé d’événements en désordre 

Un grand nombre d’événements en désordre dans une fenêtre de temps de grande taille, taille de hello de hello « réorganiser les mémoires tampons » toobe supérieure. toomitigate ce cas, la requête de hello échelle en augmentant les partitions à l’aide de PARTITION BY. Une fois la requête de hello est partitionnée, il est réparti sur plusieurs nœuds. Par conséquent, nombre de hello d’événements arrivant dans chaque nœud est réduit, ce qui réduit à son tour taille hello de mémoire tampon de commande hello. 


## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
