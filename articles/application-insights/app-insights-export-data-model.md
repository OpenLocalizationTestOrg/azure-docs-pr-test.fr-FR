---
title: "aaaAzure modèle de données d’Application Insights | Documents Microsoft"
description: "Décrit les propriétés exportées à partir de l’exportation continue dans JSON et utilisées comme filtres."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a>Modèle d’exportation de données Application Insights
Ce tableau répertorie les propriétés hello de télémétrie envoyé à partir de hello [Application Insights](app-insights-overview.md) portal toohello de kits de développement logiciel.
Vous verrez ces propriétés dans les données issues d’une [exportation continue](app-insights-export-telemetry.md).
Elles apparaissent également dans les filtres de propriétés, dans [Metrics Explorer](app-insights-metrics-explorer.md) et dans [Recherche de diagnostic](app-insights-diagnostic-search.md).

Points toonote :

* `[0]`dans ces tables désigne un point dans le chemin d’accès de hello où vous avez tooinsert un index ; mais il n’est pas toujours 0.
* Les durées sont énoncées en dixièmes de microsecondes, donc 10000000 = 1 seconde.
* Dates et heures sont UTC et figurent dans le format ISO hello`yyyy-MM-DDThh:mm:ss.sssZ`


## <a name="example"></a>Exemple
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  }

## <a name="context"></a>Context
Tous les types de données de télémétrie sont accompagnés d’une section de contexte. Tous ces champs ne sont pas transmis avec tous les points de données.

| Chemin | Type | Remarques |
| --- | --- | --- |
| context.custom.dimensions [0] |objet [ ] |Paires clé-valeur définies par le paramètre des propriétés personnalisées. Longueur maximale de clé 100, longueur maximale de valeur 1024. Plus de 100 valeurs uniques, hello propriété pouvant être recherchée, mais ne peut pas être utilisée pour la segmentation. 200 clés maximum par ikey. |
| context.custom.metrics [0] |objet [ ] |Paires clé-valeur définies par le paramètre des mesures personnalisées et par TrackMetrics. Longueur maximale de clé 100, les valeurs peuvent être numériques. |
| context.data.eventTime |string |UTC |
| context.data.isSynthetic |booléenne |Demande apparaît toocome à partir d’un test web ou le robot. |
| context.data.samplingRate |number |Pourcentage de télémétrie généré par hello SDK qui est envoyé à tooportal. Plage 0.0-100.0. |
| context.device |objet |Appareil client |
| context.device.browser |string |IE, Chrome, ... |
| context.device.browserVersion |string |Chrome 48.0, ... |
| context.device.deviceModel |string | |
| context.device.deviceName |string | |
| context.device.id |string | |
| context.device.locale |string |en-GB, de-DE, ... |
| context.device.network |string | |
| context.device.oemName |string | |
| context.device.osVersion |string |Système d’exploitation hôte |
| context.device.roleInstance |string |ID de l’hôte du serveur |
| context.device.roleName |string | |
| context.device.type |string |PC, navigateur... |
| context.location |objet |Dérivé de clientip. |
| context.location.city |string |Dérivé de clientip, si connu |
| context.location.clientip |string |Dernière octogone est too0 rendues anonymes. |
| context.location.continent |string | |
| context.location.country |string | |
| context.location.province |string |État ou province |
| context.operation.id |string |Éléments qui ont le même id d’opération sont affichés en tant qu’éléments associés dans le portail de hello de hello. Généralement les id de demande hello. |
| context.operation.name |string |nom d’URL ou de requête |
| context.operation.parentId |string |Autorise les éléments liés imbriqués. |
| context.session.id |string |ID d’un groupe d’opérations à partir de hello même source. Une période de 30 minutes sans opération signale la fin hello d’une session. |
| context.session.isFirst |booléenne | |
| context.user.accountAcquisitionDate |string | |
| context.user.anonAcquisitionDate |string | |
| context.user.anonId |string | |
| context.user.authAcquisitionDate |string |[Utilisateur authentifié](app-insights-api-custom-events-metrics.md#authenticated-users) |
| context.user.isAuthenticated |booléenne | |
| internal.data.documentVersion |string | |
| internal.data.id |string | |

## <a name="events"></a>Événements
Événements personnalisés générés par [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).

| Chemin | Type | Remarques |
| --- | --- | --- |
| event [0] count |integer |100 / (taux d’[échantillonnage](app-insights-sampling.md) ). Par exemple, 4 =&gt; 25 %. |
| event [0] name |string |Nom de l’événement.  Longueur maximale 250. |
| event [0] url |string | |
| event [0] urlData.base |string | |
| event [0] urlData.host |string | |

## <a name="exceptions"></a>Exceptions
Rapports [exceptions](app-insights-asp-net-exceptions.md) dans hello server et navigateur de hello.

| Chemin | Type | Remarques |
| --- | --- | --- |
| basicException [0] assembly |string | |
| basicException [0] count |integer |100 / (taux d’[échantillonnage](app-insights-sampling.md) ). Par exemple, 4 =&gt; 25 %. |
| basicException [0] exceptionGroup |string | |
| basicException [0] exceptionType |string | |
| basicException [0] failedUserCodeMethod |string | |
| basicException [0] failedUserCodeAssembly |string | |
| basicException [0] handledAt |string | |
| basicException [0] hasFullStack |booléenne | |
| basicException [0] id |string | |
| basicException [0] method |string | |
| basicException [0] message |string |Message d’exception. Longueur maximale 10 000. |
| basicException [0] outerExceptionMessage |string | |
| basicException [0] outerExceptionThrownAtAssembly |string | |
| basicException [0] outerExceptionThrownAtMethod |string | |
| basicException [0] outerExceptionType |string | |
| basicException [0] outerId |string | |
| basicException [0] parsedStack [0] assembly |string | |
| basicException [0] parsedStack [0] fileName |string | |
| basicException [0] parsedStack [0] level |integer | |
| basicException [0] parsedStack [0] line |integer | |
| basicException [0] parsedStack [0] method |string | |
| basicException [0] stack |string |Longueur maximale 10 000 |
| basicException [0] typeName |string | |

## <a name="trace-messages"></a>Messages de suivi
Envoyé par [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)et par hello [adaptateurs de journalisation](app-insights-asp-net-trace-logs.md).

| Chemin | Type | Remarques |
| --- | --- | --- |
| message [0] loggerName |string | |
| message [0] parameters |string | |
| message [0] raw |string |message de journal Hello, longueur max 10k. |
| message [0] severityLevel |string | |

## <a name="remote-dependency"></a>Dépendance distante
Envoyé par TrackDependency. Utilisé tooreport performances et l’utilisation de [appelle toodependencies](app-insights-asp-net-dependencies.md) dans hello server et les appels AJAX dans le navigateur de hello.

| Chemin | Type | Remarques |
| --- | --- | --- |
| remoteDependency [0] async |booléenne | |
| remoteDependency [0] baseName |string | |
| remoteDependency [0] commandName |string |Par exemple, « home/index » |
| remoteDependency [0] count |integer |100 / (taux d’[échantillonnage](app-insights-sampling.md) ). Par exemple, 4 =&gt; 25 %. |
| remoteDependency [0] dependencyTypeName |string |HTTP, SQL, ... |
| remoteDependency [0] durationMetric.value |number |Temps de toocompletion d’appel de réponse par une dépendance |
| remoteDependency [0] id |string | |
| remoteDependency [0] name |string |Url. Longueur maximale 250. |
| remoteDependency [0] resultCode |string |à partir de la dépendance HTTP |
| remoteDependency [0] success |booléenne | |
| remoteDependency [0] type |string |HTTP, SQL, ... |
| remoteDependency [0] url |string |Longueur maximale 2 000 |
| remoteDependency [0] urlData.base |string |Longueur maximale 2 000 |
| remoteDependency [0] urlData.hashTag |string | |
| remoteDependency [0] urlData.host |string |Longueur maximale 200 |

## <a name="requests"></a>Demandes
Envoyées par [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest). les modules standard Hello utilisent ce temps de réponse du serveur tooreports, mesuré sur le serveur de hello.

| Chemin | Type | Remarques |
| --- | --- | --- |
| request [0] count |integer |100 / (taux d’[échantillonnage](app-insights-sampling.md) ). Par exemple, 4 =&gt; 25 %. |
| request [0] durationMetric.value |number |Heure à partir de tooresponse qui arrivent en retard de demande. 1e7 = 1s |
| request [0] id |string |ID d’opération |
| request [0] name |string |GET/POST + base d’URL  Longueur maximale 250 |
| request [0] responseCode |integer |Tooclient d’envoi de réponse HTTP |
| request [0] success |booléenne |Par défaut == (responseCode &lt; 400) |
| request [0] url |string |Sans hôte |
| request [0] urlData.base |string | |
| request [0] urlData.hashTag |string | |
| request [0] urlData.host |string | |

## <a name="page-view-performance"></a>Performances d’affichage de la page
Envoyé par le navigateur de hello. Mesures hello temps tooprocess une page, à partir de l’utilisateur initiateur hello demande toodisplay complète (sauf les appels AJAX asynchrones).

Les valeurs de contexte représentent la version de système d’exploitation et de navigateur du client.

| Chemin | Type | Remarques |
| --- | --- | --- |
| clientPerformance [0] clientProcess.value |integer |Heure de fin de la réception de la page de hello toodisplaying hello HTML. |
| clientPerformance [0] name |string | |
| clientPerformance [0] networkConnection.value |integer |Temps écoulé tooestablish une connexion réseau. |
| clientPerformance [0] receiveRequest.value |integer |Heure de fin de l’envoi de hello tooreceiving de demande hello HTML dans la réponse. |
| clientPerformance [0] sendRequest.value |integer |Heure de la demande de hello HTTP toosend prises. |
| clientPerformance [0] total.value |integer |Heure à partir de la page de hello toodisplaying toosend hello demande de démarrage. |
| clientPerformance [0] url |string |URL de cette requête. |
| clientPerformance [0] urlData.base |string | |
| clientPerformance [0] urlData.hashTag |string | |
| clientPerformance [0] urlData.host |string | |
| clientPerformance [0] urlData.protocol |string | |

## <a name="page-views"></a>Affichages de pages
Envoyé par trackPageView() ou [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)

| Chemin | Type | Remarques |
| --- | --- | --- |
| view [0] count |integer |100 / (taux d’[échantillonnage](app-insights-sampling.md) ). Par exemple, 4 =&gt; 25 %. |
| view [0] durationMetric.value |integer |Valeur éventuellement définie dans trackPageView() ou par startTrackPage() - stopTrackPage(). Bonjour pas même en tant que valeurs de clientPerformance. |
| view [0] name |string |Titre de la page.  Longueur maximale 250 |
| view [0] url |string | |
| view [0] urlData.base |string | |
| view [0] urlData.hashTag |string | |
| view [0] urlData.host |string | |

## <a name="availability"></a>Availability
Consigne les [tests web de disponibilité](app-insights-monitor-web-app-availability.md).

| Chemin | Type | Remarques |
| --- | --- | --- |
| availability [0] availabilityMetric.name |string |Availability |
| availability [0] availabilityMetric.value |number |1.0 ou 0.0 |
| availability [0] count |integer |100 / (taux d’[échantillonnage](app-insights-sampling.md) ). Par exemple, 4 =&gt; 25 %. |
| availability [0] dataSizeMetric.name |string | |
| availability [0] dataSizeMetric.value |integer | |
| availability [0] durationMetric.name |string | |
| availability [0] durationMetric.value |number |Durée du test. 1e7 = 1s |
| availability [0] message |string |Diagnostic de défaillance |
| availability [0] result |string |Réussite/Échec |
| availability [0] runLocation |string |Source géographique de la requête HTTP |
| availability [0] testName |string | |
| availability [0] testRunId |string | |
| availability [0] testTimestamp |string | |

## <a name="metrics"></a>Mesures
Généré par TrackMetric().

valeur de métrique Hello se trouve dans context.custom.metrics[0]

Par exemple :

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a>À propos des valeurs de mesure
Les valeurs de mesure, dans les rapports de mesure et ailleurs, sont consignées avec une structure d’objet standard. Par exemple :

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

Actuellement - bien que cela peut modifier Bonjour futures - toutes les valeurs signalées par les modules du Kit de développement logiciel standard hello, `count==1` et uniquement hello `name` et `value` sont utiles. Hello seul cas où ils seraient différents serait si vous écrivez votre propre appels TrackMetric dans laquelle vous avez défini hello autres paramètres.

Hello objectif hello autres champs est tooallow toobe de métriques agrégée Bonjour SDK, le portail de toohello tooreduce le trafic. Par exemple, vous pouvez décider d’accumuler un nombre défini de valeurs successives avant d’envoyer chaque rapport de mesure. Cliquez ensuite calculer hello min, max, écart type et valeur d’agrégation (somme ou moyenne) et définissez le toohello au nombre de lectures représenté par les rapports hello.

Dans les tables de hello ci-dessus, nous avons omis hello rarement des champs count, min, max, stdDev et sampledValue.

Au lieu de l’agrégation des mesures, vous pouvez utiliser [échantillonnage](app-insights-sampling.md) si vous avez besoin de volume de hello tooreduce de télémétrie.

### <a name="durations"></a>Durées
Sauf mention contraire, les durées sont indiquées en dixièmes de microseconde. Ainsi, 10000000.0 représente 1s.

## <a name="see-also"></a>Voir aussi
* [Application Insights](app-insights-overview.md)
* [Exportation continue](app-insights-export-telemetry.md)
* [Exemples de code](app-insights-export-telemetry.md#code-samples)
