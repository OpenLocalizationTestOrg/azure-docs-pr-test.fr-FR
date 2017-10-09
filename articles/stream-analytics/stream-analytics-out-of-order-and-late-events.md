---
title: "aaaHandling ordre des événements et lateness avec Analytique de flux de données Azure | Documents Microsoft"
description: "Découvrez le fonctionnement de Stream Analytics avec des événements en retard ou en désordre dans les flux de données."
keywords: "Événements en désordre, en retard"
documentationcenter: 
services: stream-analytics
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Traitement de l’ordre des événements Azure Stream Analytics

Dans un flux de données temporelles des événements, chaque événement est enregistré avec le temps hello cet événement hello est reçu. Certaines conditions peuvent provoquer des flux d’événements toooccasionally recevoir certains événements dans un ordre différent, au-delà de laquelle ils ont été envoyés. Un simple TCP retransmettre, ou même un décalage horaire entre hello envoi hello réception concentrateur d’événements et des appareils susceptibles de provoquer cette toooccur. Les événements « Ponctuation » sont ajoutés les flux d’événements tooreceived, heure de hello tooadvance en absence de hello d’arrivée des événements. Ils sont nécessaires dans des scénarios tels que « M’informer lorsque aucune connexion ne se produit pendant 3 minutes ».

Les flux d’entrée qui ne sont pas dans l’ordre sont :
* Triés (et par conséquent **retardés**).
* Ajusté par système hello, selon la stratégie de tooa spécifié par l’utilisateur.


## <a name="lateness-tolerance"></a>Tolérance de retard
Stream Analytics tolère les types de scénarios suivants. Le service Stream Analytics dispose d’une gestion des événements « en désordre » et « en retard ». Il gère ces événements Bonjour suivant façons :

* Les événements qui arrivent dans le désordre, mais dans hello définir la tolérance de panne sont **réorganisées par horodatage**.
* Les événements qui arrivent plus tard que la tolérance sont **supprimés ou ajustés**.
    * **Ajustée**: tooappear ajustée toohave est arrivé à hello acceptable heure la plus récente.
    * **Supprimés** : ignorés.

![Traitement des événements Stream Analytics](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>Réduire la quantité, hello pour les événements non ordonnés

Comme Stream Analytics applique une transformation temporelle lorsqu’il traite les événements entrants (par exemple, pour les agrégats fenêtrés ou les jointures temporelles), Stream Analytics trie les événements entrants par ordre d’horodatage.

Lorsque le mot clé d’horodatage hello » par » est **pas** utilisé, heure de file d’attente d’événement hello Azure Event Hubs est utilisé par défaut. Concentrateurs d’événements garantit unitonicité de timestamp hello sur chaque partition du concentrateur d’événements hello. Il garantit également que les événements de toutes les partitions sont fusionnés dans l’ordre d’horodatage. Ces garanties Event Hubs permettent d’éviter les événement en désordre.

Parfois, il est important pour l’horodatage de vous toouse hello l’expéditeur. Dans ce cas, un horodatage à partir de la charge utile d’événement hello est choisi à l’aide de « timestamp par ». Dans ces scénarios, une ou plusieurs sources du désordre des événements peuvent être introduites :

* Les producteurs d’événements ont des décalages d’horloge. Cela est courant lorsque les producteurs proviennent de différents ordinateurs et qu’ils ont donc des horloges différentes.
* Il existe un délai de réseau à partir de la source hello du concentrateur d’événements hello événements toohello destination.
* Les décalages d’horloge existent entre les partitions du Event Hub. Stream Analytics trie tout d’abord les événements de toutes les partitions du Event Hub par heure de mise en file d’attente des événements. Ensuite, il examine les flux de données hello pour les événements dans un ordre incorrect.

Sur l’onglet de configuration hello, vous voyez hello suivant par défaut :

![Traitement des événements désordonnés dans Stream Analytics](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Si vous utilisez 0 seconde comme hello ordonnés plage de tolérance, vous déclarez que tous les événements sont dans l’ordre toutes les périodes de hello. Sources de hello trois d’événements de dans un ordre incorrect, il est peu probable que cela est vrai. 

toocorrect du flux de données Analytique tooallow un misorder d’événement, vous pouvez spécifier une plage de tolérance non nulle non ordonnés. Événements de mémoires tampons flux Analytique toothat fenêtre, puis les à l’aide de hello timestamp que vous avez choisi de nouvelles commandes. Il applique ensuite la transformation temporelle de hello. Vous pouvez commencer par une fenêtre de 3 secondes et ajuster hello valeur tooreduce hello nombre d’événements qui sont ajustées à la fois. 

Un effet secondaire de la mise en mémoire tampon hello est sortie de hello **retardé hello même durée**. Vous pouvez ajuster hello valeur tooreduce hello nombre d’événements de non ordonnés et limiter la latence du travail hello.

## <a name="get-help"></a>Obtenir de l’aide
Pour une assistance supplémentaire, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooStream Analytique](stream-analytics-introduction.md)
* [Prise en main de Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l’échelle des travaux Stream Analytics](stream-analytics-scale-jobs.md)
* [Informations de référence sur le langage de requête Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion de Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)