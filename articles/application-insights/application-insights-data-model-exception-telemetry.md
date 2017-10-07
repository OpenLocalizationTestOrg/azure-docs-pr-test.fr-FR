---
title: "aaaAzure modèle de données d’Application Insights télémétrie - télémétrie des exceptions | Documents Microsoft"
description: "Modèle de données Application Insights pour la télémétrie des exceptions"
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
ms.openlocfilehash: 4c2b7d1ac3816d5623db9a35819a48a68a13a9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exception-telemetry-application-insights-data-model"></a>Télémétrie des exceptions : modèle de données Application Insights

Dans [Application Insights](app-insights-overview.md), une instance d’Exception représente une exception gérée ou non gérée s’est produite lors de l’exécution de l’application hello analysé.

## <a name="problem-id"></a>ID du problème

Identificateur d’où l’exception de hello a été levée dans le code. Utilisé pour le regroupement des exceptions. En règle générale, une combinaison de type d’exception et une fonction à partir de la pile des appels hello.

Longueur maximale : 1024 caractères

## <a name="severity-level"></a>Niveau de gravité

Niveau de gravité de trace. La valeur peut être `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="exception-details"></a>Détails de l’exception

(toobe étendu)

## <a name="custom-properties"></a>Propriétés personnalisées

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Mesures personnalisées

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Étapes suivantes

- Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).
- Découvrez comment trop[diagnostiquer des exceptions dans vos applications web avec Application Insights](app-insights-asp-net-exceptions.md).
- Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.
