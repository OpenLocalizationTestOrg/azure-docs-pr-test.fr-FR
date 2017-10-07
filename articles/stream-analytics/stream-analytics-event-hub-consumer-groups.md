---
title: "aaaDebug Analytique de flux de données Azure avec les récepteurs du hub d’événements | Documents Microsoft"
description: "Meilleures pratiques pour considérer les groupes de consommateurs Event Hubs dans Stream Analytics."
keywords: "limite de hub d’événement, groupe de consommateurs"
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Déboguer Azure Stream Analytics avec des destinataires de hub d’événement

Vous pouvez utiliser Azure Event Hubs Azure flux Analytique tooingest ou sortie des données à partir d’un travail. Il est recommandé pour l’utilisation des concentrateurs d’événements toouse plusieurs groupes de consommateurs, l’extensibilité de projet tooensure. L’une des raisons sont que nombre hello de lecteurs dans la tâche de flux de données Analytique hello pour une entrée spécifique affecte un nombre hello de lecteurs dans un groupe de consommateurs unique. nombre précis de Hello de récepteurs est basé sur les détails d’implémentation interne pour la logique de topologie de montée en puissance parallèle hello. nombre de Hello de récepteurs n’est pas exposé en externe. nombre de Hello de lecteurs peut changer à l’heure de début de tâche hello ou mises à niveau de la tâche.

> [!NOTE]
> Quand un nombre de lecteurs hello change pendant une mise à niveau de la tâche, avertissements temporaires sont écrits tooaudit journaux. Les travaux Stream Analytics récupèrent automatiquement de ces problèmes temporaires.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Le nombre de lecteurs par partition dépasse la limite de 5 définie dans Event Hubs.

Les scénarios dans le hello nombre de lecteurs par partition dépasse la limite de concentrateurs d’événements hello de cinq hello suivants :

* Plusieurs instructions SELECT : Si vous utilisez plusieurs instructions SELECT qui font référence trop**même** concentrateur d’événements d’entrée, chaque instruction SELECT entraîne une nouvelle toobe de récepteur créé.
* UNION : Lorsque vous utilisez une UNION, il est possible de toohave plusieurs entrées qui font référence toohello **même** groupe hub et consommateur d’événements.
* Une jointure RÉFLEXIVE : Lorsque vous utilisez une opération de jointure de libre-service, il est possible de toorefer toohello **même** concentrateur d’événements plusieurs fois.

## <a name="solution"></a>Solution

Hello meilleures pratiques suivantes peuvent aider à atténuer les Bonjour nombre de lecteurs par partition dépasse la limite de concentrateurs d’événements hello de cinq des scénarios.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>Fractionner votre requête en plusieurs étapes à l’aide d’une clause WITH

clause WITH de Hello spécifie un jeu de résultats nommé temporaire qui peut être référencé par une clause FROM de la requête de hello. Vous définissez la clause WITH de hello dans la portée de l’exécution de hello d’une instruction SELECT unique.

Par exemple, au lieu de cette requête :

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Utilisez cette requête :

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Assurez-vous que les entrées lient des groupes de consommateurs toodifferent

Pour les requêtes dans laquelle au moins trois entrées sont connecté toohello même consommateur de concentrateurs d’événements, créer des groupes de consommateurs distincts. Cela requiert la création d’entrées de flux de données Analytique supplémentaires hello.


## <a name="get-help"></a>Obtenir de l’aide
Pour une assistance supplémentaire, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooStream Analytique](stream-analytics-introduction.md)
* [Prise en main de Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l’échelle des travaux Stream Analytics](stream-analytics-scale-jobs.md)
* [Informations de référence sur le langage de requête Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion de Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
