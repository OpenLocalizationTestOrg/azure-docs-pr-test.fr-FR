---
title: "aaaAzure modèle de données de télémétrie Application Insights | Documents Microsoft"
description: "Présentation du modèle de données Application Insights"
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
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Modèle de données de télémétrie d’Application Insights

[Azure Application Insights](app-insights-overview.md) envoie les données de télémétrie à partir de votre toohello d’application web portail Azure, afin que vous pouvez analyser les performances de hello et d’utilisation de votre application. modèle de données de télémétrie Hello est normalisé afin qu’il soit possible toocreate plateforme et indépendant du langage d’analyse. 

Les données collectées par Application Insights modélisent ce schéma standard d’exécution d’application :

![Modèle d’application Application Insights](./media/application-insights-data-model/application-insights-data-model.png)

Hello des types suivants de télémétrie sont l’exécution de hello toomonitor utilisés de votre application. Hello trois types suivants sont en général automatiquement collectées par hello Application Insights SDK à partir de l’infrastructure d’application web hello :

* [**Demande** ](application-insights-data-model-request-telemetry.md) -généré toolog une demande reçue par votre application. Par exemple, hello web Application Insights que SDK génère automatiquement un élément de données de télémétrie de demande pour chaque demande HTTP qui reçoit de votre application web. 

    Un **opération** est hello des threads d’exécution qui traite une requête. Vous pouvez également [écrire du code](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor autres types d’opérations, comme un « sort » d’un site web de la tâche ou périodiquement de fonction qui traite les données.  Chaque opération a un ID. Cet ID peut être utilisé too[group]((application-insights-correlation.md) toutes les données de télémétrie générée lors du traitement de demande de hello votre application. Chaque opération réussit ou échoue et a une certaine durée.
* [**Exception** ](application-insights-data-model-exception-telemetry.md) -représente généralement une exception qui provoque un toofail de l’opération.
* [**Dépendance** ](application-insights-data-model-dependency-telemetry.md) -représente un appel de votre service d’applications externes de tooan ou de stockage tel qu’une API REST ou de SQL. Dans ASP.NET, tooSQL des appels de dépendance sont définis par `System.Data`. Points de terminaison tooHTTP appels sont définis par `System.Net`. 

Application Insights fournit trois types de données supplémentaires pour la télémétrie personnalisée :

* [Trace](application-insights-data-model-trace-telemetry.md) - utilisées directement ou via un enregistrement des diagnostics tooimplement adaptateur à l’aide d’une infrastructure d’instrumentation est tooyou familier, tels que `Log4Net` ou `System.Diagnostics`.
* [Événement](application-insights-data-model-event-telemetry.md) -généralement utilisé interaction avec votre service, les modèles d’utilisation de tooanalyze toocapture de l’utilisateur.
* [Métrique](application-insights-data-model-metric-telemetry.md) -utilisé tooreport des mesures scalaires périodiques.

Chaque élément de données de télémétrie peut définir hello [les informations de contexte](application-insights-data-model-context.md) comme id session utilisateur ou de la version d’application. Le contexte est un ensemble de champs fortement typés qui débloque certains scénarios. Quand la version de l’application est correctement initialisée, Application Insights peut détecter les nouveaux modèles de comportement de l’application en corrélation avec un redéploiement. Id de session peut être utilisé toocalculate hello panne ou un impact sur les utilisateurs sur le problème. Calculer des nombres distincts de valeurs d’ID de session pour certaines dépendances en échec, suivis d’erreur ou exceptions critique vous donne une bonne compréhension d’un impact.

Modèle de données de télémétrie définit un moyen de application Insights trop[mettre en corrélation](application-insights-correlation.md) opération toohello de télémétrie dont il fait partie. Par exemple, une requête peut appeler une base de données SQL et enregistrer les informations de diagnostic. Vous pouvez définir le contexte de corrélation hello pour les éléments de télémétrie relier la télémétrie des requêtes toohello précédent.

## <a name="schema-improvements"></a>Améliorations du schéma

Modèle de données d’application Insights est un toomodel de façon simple et de base et puissant de télémétrie de votre application. Nous s’efforcent de scénarios essentiels de tookeep hello modèle toosupport simple et compacte et autoriser le schéma de hello tooextend pour une utilisation avancée.

Affiche des suggestions et des problèmes de schéma ou de modèle de données tooreport utilisent GitHub [ApplicationInsights-accueil](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) référentiel.

## <a name="next-steps"></a>Étapes suivantes

- [Écrire des données de télémétrie personnalisées](app-insights-api-custom-events-metrics.md)
- Découvrez comment trop[étendre et de filtrer les données de télémétrie](app-insights-api-filtering-sampling.md).
- Utilisez [échantillonnage](app-insights-sampling.md) quantité toominimize de télémétrie basée sur le modèle de données.
- Découvrez quelles [plateformes](app-insights-platforms.md) sont prises en charge par Application Insights.
