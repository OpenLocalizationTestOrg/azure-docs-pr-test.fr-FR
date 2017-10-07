---
title: "aaaAzure modèle de données d’Application Insights télémétrie - événement de télémétrie | Documents Microsoft"
description: "Modèle de données Application Insights pour la télémétrie des événements"
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a>Télémétrie des événements : modèle de données Application Insights

Vous pouvez créer des éléments de télémétrie (dans [Application Insights](app-insights-overview.md)) toorepresent un événement qui s’est produite dans votre application. En général, il s’agit d’une interaction utilisateur comme un clic sur un bouton ou une validation de commande. Il peut aussi s’agir d’un événement lié au cycle de vie de l’application, comme une initialisation ou une mise à jour de configuration. 

Sémantiquement, les événements peuvent ou ne peuvent pas être corrélés toorequests. Toutefois, si la télémétrie des événements est utilisée correctement, elle est plus importante que les requêtes ou les traces. Événements représentent la télémétrie d’entreprise et doit être un objet tooseparate, moins agressive [échantillonnage](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Nom

Nom de l’événement. regroupement approprié de tooallow et mesures utiles, limiter votre application afin qu’il génère un petit nombre de noms d’événements distincts. Par exemple, n’utilisez pas un nom distinct pour chaque instance générée d’un événement.

Longueur maximale : 512 caractères

## <a name="custom-properties"></a>Propriétés personnalisées

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Mesures personnalisées

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Étapes suivantes

- Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).
- [Écrire des données de télémétrie d’événement personnalisées](app-insights-api-custom-events-metrics.md#trackevent)
- Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.
