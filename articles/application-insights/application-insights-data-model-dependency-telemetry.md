---
title: "aaaAzure modèle de données d’Application Insights télémétrie - télémétrie des dépendances | Documents Microsoft"
description: "Modèle de données Application Insights pour la télémétrie des dépendances"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a>Télémétrie des dépendances : modèle de données Application Insights

Télémétrie des dépendances (dans [Application Insights](app-insights-overview.md)) représente une interaction de composant hello analysé avec un composant distant tel que SQL ou un point de terminaison HTTP.

## <a name="name"></a>Nom

Nom de la commande hello démarrée avec cet appel de dépendance. Valeur de faible cardinalité. Exemples : nom de procédure stockée et modèle de chemin d’accès d’URL.

## <a name="id"></a>ID

Identificateur d’une instance d’appel de dépendance. Utilisé pour la corrélation par élément de données de télémétrie hello demande correspondant toothis dépendance appel. Pour plus d’informations, consultez la page relative à la [corrélation](application-insights-correlation.md).

## <a name="data"></a>Données

Commande lancée par cet appel de dépendance. Exemples : instruction SQL et URL HTTP avec tous les paramètres de requête.

## <a name="type"></a>Type

Nom du type de dépendance. Valeur de faible cardinalité pour le regroupement logique de dépendances et l’interprétation d’autres champs comme commandName et resultCode. Exemples : SQL, table Azure et HTTP.

## <a name="target"></a>Cible

Site cible d’un appel de dépendance. Exemples : nom de serveur, adresse d’hôte. Pour plus d’informations, consultez la page relative à la [corrélation](application-insights-correlation.md).

## <a name="duration"></a>Durée

Durée de la demande au format : `DD.HH:MM:SS.MMMMMM`. Doit être inférieure à `1000` jours.

## <a name="result-code"></a>Code de résultat

Code de résultat d’un appel de dépendance. Exemples : code d’erreur SQL et code d’état HTTP.

## <a name="success"></a>Succès

Indication de la réussite ou non d’un appel.

## <a name="custom-properties"></a>Propriétés personnalisées

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Mesures personnalisées

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a>Étapes suivantes

- Configurez le suivi des dépendances pour [.NET](app-insights-asp-net-dependencies.md).
- Configurez le suivi des dépendances pour [Java](app-insights-java-agent.md).
- [Écrire des données de télémétrie des dépendances personnalisées](app-insights-api-custom-events-metrics.md#trackdependency)
- Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).
- Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.
