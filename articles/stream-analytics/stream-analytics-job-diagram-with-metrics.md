---
title: "AAA Analytique de flux de données Azure piloté par les données de débogage à l’aide du schéma de tâche hello | Documents Microsoft"
description: "Résoudre les problèmes de votre tâche de flux de données Analytique à l’aide de mesures et schéma de tâche hello."
keywords: 
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
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Débogage à l’aide du schéma de tâche hello piloté par les données

diagramme de travail Hello sur hello **analyse** panneau Bonjour portail Azure peut vous aider à visualiser le pipeline de votre travail. Il montre les entrées, les sorties et les étapes de requête. Vous pouvez utiliser des métriques de hello tooexamine hello travail diagramme pour chaque étape, toomore isoler rapidement source hello d’un problème pour résoudre des problèmes.

## <a name="using-hello-job-diagram"></a>À l’aide du schéma de tâche hello

Bonjour portail Azure, alors que dans une tâche de flux de données Analytique sous **prise en charge + dépannage**, sélectionnez **diagramme de travail**:

![Diagramme de travail avec des mesures - emplacement](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Sélectionnez chaque section requête étape toosee hello correspondant dans une volet de modification de la requête. Un graphique de métrique de l’étape hello est affiché dans un volet inférieur de la page de hello.

![Diagramme de travail avec des mesures - travail de base](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

partitions de hello toosee d’entrée de concentrateurs d’événements Azure hello, sélectionnez **...** Un menu contextuel s’affiche. Vous pouvez également voir fusion d’entrée de hello.

![Diagramme de travail avec des mesures - étendre une partition](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

graphique de métrique hello toosee pour une seule partition, nœud de partition hello select. métriques de Hello sont affichés en bas de hello de page de hello.

![Diagramme de travail avec des mesures - mesures supplémentaires](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

graphique des métriques toosee hello pour une fusion, le nœud de fusion hello select. Hello suivant le graphique indique qu’aucun événement ont été supprimés ou ajustée.

![Diagramme de travail avec des mesures - grille](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

Détails de hello toosee de valeur de métrique hello et l’heure, point toohello graphique.

![Diagramme de travail avec des mesures - pointer](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Résoudre les problèmes à l’aide de mesures

Hello **QueryLastProcessedTime** métrique indique quand une étape spécifique a reçu des données. En examinant la topologie de hello, vous pouvez travailler à partir de hello sortie processeur toosee étape qui ne reçoit pas de données. Si une étape ne reçoit pas de données, passez à étape de requête toohello juste avant qu’il. Vérifiez si une fenêtre de temps a hello précédente étape de requête, et si suffisamment longtemps pour qu’il toooutput données. (Notez que temporelles windows sont alignés toohello heure).
 
Si hello étape de requête précédente est un processeur d’entrée, les éléments suivants utilisez hello métriques d’entrée toohelp réponses hello ciblé questions. Elles peuvent vous aider à déterminer si un travail récupère des données à partir de ses sources d’entrée. Si la requête de hello est partitionnée, examinez chaque partition.
 
### <a name="how-much-data-is-being-read"></a>Quelle est la quantité de données lue ?

*   **InputEventsSourcesTotal** est le nombre de hello d’unités de données en lecture. Par exemple, hello nombre d’objets BLOB.
*   **InputEventsTotal** nombre de hello d’événements de lecture. Cette mesure est disponible par partition.
*   **InputEventsInBytesTotal** est le nombre de hello d’octets lus.
*   **InputEventsLastArrivalTime** est mis à jour avec chaque durée de file d’attente des événements reçus.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>La chronologie progresse-t-elle ? Si des événements réels sont lus, il est possible qu’aucune ponctuation ne soit émise.

*   **InputEventsLastPunctuationTime** indique quand un signe de ponctuation a été émis tookeep temps à transférer vers l’avant. Si la ponctuation n’est pas émise, le flux de données peut être bloqué.
 
### <a name="are-there-any-errors-in-hello-input"></a>Existe-t-il des erreurs dans l’entrée de hello ?

*   **InputEventsEventDataNullTotal** correspond au nombre d’événements présentant des données nulles.
*   **InputEventsSerializerErrorsTotal** correspond au nombre d’événements qui n’ont pas pu être désérialisés correctement.
*   **InputEventsDegradedTotal** correspond au nombre d’événements présentant un problème autre que la désérialisation.
 
### <a name="are-events-being-dropped-or-adjusted"></a>Les événements sont-ils supprimés ou modifiés ?

*   **InputEventsEarlyTotal** nombre de hello d’événements qui ont un horodateur de l’application avant la limite supérieure de hello.
*   **InputEventsLateTotal** est nombre hello d’événements qui ont un horodateur de l’application après la limite supérieure de hello.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** est le nombre d’événements hello supprimé avant l’heure de début du travail de hello.
 
### <a name="are-we-falling-behind-in-reading-data"></a>Sommes-nous en retard en matière de lecture des données ?

*   **InputEventsSourcesBackloggedTotal** vous indique de combien de messages plus besoin toobe lire pour les entrées de concentrateurs d’événements et Azure IoT Hub.


## <a name="get-help"></a>Obtenir de l’aide
Pour une assistance supplémentaire, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooStream Analytique](stream-analytics-introduction.md)
* [Prise en main de Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l’échelle des travaux Stream Analytics](stream-analytics-scale-jobs.md)
* [Informations de référence sur le langage de requête Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion de Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
