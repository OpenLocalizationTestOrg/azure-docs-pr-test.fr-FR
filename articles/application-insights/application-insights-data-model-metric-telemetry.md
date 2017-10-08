---
title: "aaaAzure modèle de données d’Application Insights télémétrie - métrique de télémétrie | Documents Microsoft"
description: "Modèle de données Application Insights pour la télémétrie des mesures"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 005e218a8451007458185f1e457a20cee93fa630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="metric-telemetry-application-insights-data-model"></a>Télémétrie des mesure : modèle de données Application Insights

Deux types de télémétrie des mesures sont prises en charge par [Application Insights](app-insights-overview.md) : la mesure unique et la mesure pré-agrégée. La mesure unique consiste simplement dans un nom et une valeur. Métrique agrégée au préalable spécifie la valeur minimale et maximale de la métrique de hello dans l’intervalle d’agrégation de hello et écart de celui-ci.

La télémétrie des mesures pré-agrégées suppose que cette période d’agrégation est d’une minute.

Plusieurs noms de mesure connus sont pris en charge par Application Insights. 

Système de représentation des mesures et compteurs de processus :

| **Nom .NET**             | **Nom sans plateforme spécifiée** | **Nom d’API REST** | **Description**
| ------------------------- | -------------------------- | ----------------- | ---------------- 
| `\Processor(_Total)\% Processor Time` | Travail en cours... | [processorCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessorCpuPercentage) | nombre total de processeurs de l’ordinateur
| `\Memory\Available Bytes`                 | Travail en cours... | [memoryAvailableBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FmemoryAvailableBytes) | mémoire disponible sur le disque
| `\Process(??APP_WIN32_PROC??)\% Processor Time` | Travail en cours... | [processCpuPercentage](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessCpuPercentage) | UC du processus hello hébergeant l’application hello
| `\Process(??APP_WIN32_PROC??)\Private Bytes`      | Travail en cours... | [processPrivateBytes](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessPrivateBytes) | mémoire utilisée par les processus hello hébergeant l’application hello
| `\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec` | Travail en cours... | [processIOBytesPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FprocessIOBytesPerSecond) | taux d’opérations d’e/s s’exécute par processus hébergeant l’application hello
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec`             | Travail en cours... | [requestsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsPerSecond) | fréquence des requêtes traitées par application 
| `\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec`    | Travail en cours... | [exceptionsPerSecond](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FexceptionsPerSecond) | fréquence des exceptions levées par application
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time`   | Travail en cours... | [requestExecutionTime](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestExecutionTime) | durée d’exécution moyenne des requêtes
| `\ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue` | Travail en cours... | [requestsInQueue](https://dev.applicationinsights.io/apiexplorer/metrics?appId=DEMO_APP&apiKey=DEMO_KEY&metricId=performanceCounters%2FrequestsInQueue) | nombre de demandes en attente de hello dans une file d’attente de traitement

## <a name="name"></a>Nom

Nom de mesure de hello vous aimeriez toosee dans le portail Application Insights et l’interface utilisateur. 

## <a name="value"></a>Valeur

Valeur unique pour la mesure. Somme des mesures individuelles pour l’agrégation de hello.

## <a name="count"></a>Nombre

Poids de la métrique de hello agrégées métrique. Ne doit pas être défini pour une mesure.

## <a name="min"></a>Min

Valeur minimale de la métrique de hello agrégée. Ne doit pas être défini pour une mesure.

## <a name="max"></a>max

Valeur maximale de la métrique de hello agrégée. Ne doit pas être défini pour une mesure.

## <a name="standard-deviation"></a>Écart standard

Écart type de mesure de hello agrégée. Ne doit pas être défini pour une mesure.

## <a name="custom-properties"></a>Propriétés personnalisées

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment toouse [API Application Insights pour les événements personnalisés et les métriques](app-insights-api-custom-events-metrics.md#trackmetric).
- Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).
- Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.
