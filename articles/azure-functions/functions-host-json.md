---
title: "Informations de référence sur le fichier host.json pour Azure Functions"
description: "Documentation de référence pour le fichier host.json d’Azure Functions."
services: functions
author: tdykstra
manager: cfowler
editor: 
tags: 
keywords: 
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/09/2017
ms.author: tdykstra
ms.openlocfilehash: 522d0590595b0fc0fef503599f1677658f223bd8
ms.sourcegitcommit: cfd1ea99922329b3d5fab26b71ca2882df33f6c2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2017
---
# <a name="hostjson-reference-for-azure-functions"></a>Informations de référence sur le fichier host.json pour Azure Functions

Le fichier de métadonnées *host.json* contient les options de configuration globale qui affectent l’ensemble des fonctions d’une application de fonction. Cet article répertorie les paramètres qui sont disponibles. Le schéma JSON est indiqué sur la page http://json.schemastore.org/host.

Les [paramètres d’application](functions-app-settings.md) et le fichier [local.settings.json](functions-run-local.md#local-settings-file) contiennent d’autres options de configuration globale.

## <a name="sample-hostjson-file"></a>Exemple de fichier host.json

L’exemple de fichier *host.json* suivant contient toutes les options possibles spécifiées.

```json
{
    "aggregator": {
        "batchSize": 1000,
        "flushTimeout": "00:00:30"
    },
    "applicationInsights": {
        "sampling": {
          "isEnabled": true,
          "maxTelemetryItemsPerSecond" : 5
        }
    },
    "eventHub": {
      "maxBatchSize": 64,
      "prefetchCount": 256,
      "batchCheckpointFrequency": 1
    },
    "functions": [ "QueueProcessor", "GitHubWebHook" ],
    "functionTimeout": "00:05:00",
    "http": {
        "routePrefix": "api",
        "maxOutstandingRequests": 20,
        "maxConcurrentRequests": 10,
        "dynamicThrottlesEnabled": false
    },
    "id": "9f4ea53c5136457d883d685e57164f08",
    "logger": {
        "categoryFilter": {
            "defaultLevel": "Information",
            "categoryLevels": {
                "Host": "Error",
                "Function": "Error",
                "Host.Aggregator": "Information"
            }
        }
    },
    "queues": {
      "maxPollingInterval": 2000,
      "visibilityTimeout" : "00:00:30",
      "batchSize": 16,
      "maxDequeueCount": 5,
      "newBatchThreshold": 8
    },
    "serviceBus": {
      "maxConcurrentCalls": 16,
      "prefetchCount": 100,
      "autoRenewTimeout": "00:05:00"
    },
    "singleton": {
      "lockPeriod": "00:00:15",
      "listenerLockPeriod": "00:01:00",
      "listenerLockRecoveryPollingInterval": "00:01:00",
      "lockAcquisitionTimeout": "00:01:00",
      "lockAcquisitionPollingInterval": "00:00:03"
    },
    "tracing": {
      "consoleLevel": "verbose",
      "fileLoggingMode": "debugOnly"
    },
    "watchDirectories": [ "Shared" ],
}
```

Les sections suivantes de cet article expliquent chaque propriété de niveau supérieur. Toutes les autres propriétés sont facultatives sauf indication contraire.

## <a name="aggregator"></a>aggregator

Spécifie le nombre d’appels de fonction agrégés lorsque vous [calculez des métriques pour Application Insights](functions-monitoring.md#configure-the-aggregator). 

```json
{
    "aggregator": {
        "batchSize": 1000,
        "flushTimeout": "00:00:30"
    }
}
```

|Propriété  |Default | Description |
|---------|---------|---------| 
|batchSize|1 000|Nombre maximal de requêtes à agréger.| 
|flushTimeout|00:00:30|Période maximale d’agrégation.| 

Les appels de fonction sont agrégés lorsque la première des deux limites est atteinte.

## <a name="applicationinsights"></a>applicationInsights

Contrôle la [fonctionnalité d’échantillonnage dans Application Insights](functions-monitoring.md#configure-sampling).

```json
{
    "applicationInsights": {
        "sampling": {
          "isEnabled": true,
          "maxTelemetryItemsPerSecond" : 5
        }
    }
}
```

|Propriété  |Default | Description |
|---------|---------|---------| 
|isEnabled|false|Active ou désactive l’échantillonnage.| 
|maxTelemetryItemsPerSecond|5|Seuil à partir duquel l’échantillonnage débute.| 

## <a name="eventhub"></a>eventHub

Paramètres de configuration pour les [déclencheurs et liaisons Event Hub](functions-bindings-event-hubs.md).

[!INCLUDE [functions-host-json-event-hubs](../../includes/functions-host-json-event-hubs.md)]

## <a name="functions"></a>functions

Liste des fonctions que l’hôte de travail exécute.  Un tableau vide désigne l’exécution de toutes les fonctions.  Utilisée uniquement pour une [exécution locale](functions-run-local.md). Dans les applications de fonction, utilisez la propriété *function.json* `disabled` plutôt que cette propriété dans *host.json*.

```json
{
    "functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```

## <a name="functiontimeout"></a>functionTimeout

Indique la durée avant expiration du délai de toutes les fonctions. Dans les plans de consommation, la plage valide est comprise entre 1 seconde et 10 minutes, et la valeur par défaut est de 5 minutes. Dans les plans App Service, il n’existe aucune limite et la valeur par défaut est Null, ce qui indique qu’il n’y a pas de durée avant expiration du délai.

```json
{
    "functionTimeout": "00:05:00"
}
```

## <a name="http"></a>http

Paramètre de configuration pour les [déclencheurs et liaisons http](functions-bindings-http-webhook.md).

[!INCLUDE [functions-host-json-http](../../includes/functions-host-json-http.md)]

## <a name="id"></a>id

ID unique d’un hôte de travail. Il peut s’agir d’un GUID en minuscules dont les tirets ont été supprimés. Requis lors d’une exécution locale. Lors de l’exécution dans Azure Functions, un ID est généré automatiquement si `id` est omis.

```json
{
    "id": "9f4ea53c5136457d883d685e57164f08"
}
```

## <a name="logger"></a>logger

Contrôle le filtrage des journaux écrits par un [objet ILogger](functions-monitoring.md#write-logs-in-c-functions) ou par [context.log](functions-monitoring.md#write-logs-in-javascript-functions).

```json
{
    "logger": {
        "categoryFilter": {
            "defaultLevel": "Information",
            "categoryLevels": {
                "Host": "Error",
                "Function": "Error",
                "Host.Aggregator": "Information"
            }
        }
    }
}
```

|Propriété  |Default | Description |
|---------|---------|---------| 
|categoryFilter|n/a|Spécifie un filtrage par catégorie.| 
|defaultLevel|Information|Pour toutes les catégories non spécifiées dans le tableau `categoryLevels`, envoie les journaux de ce niveau et des niveaux supérieurs à Application Insights.| 
|categoryLevels|n/a|Tableau des catégories qui spécifie le niveau de journalisation minimal à envoyer à Application Insights pour chaque catégorie. La catégorie indiquée ici contrôle toutes les catégories qui commencent par la même valeur, et les valeurs plus longues sont prioritaires. Dans l’exemple de fichier *host.json* précédent, toutes les catégories qui commencent par « Host.Aggregator » journalisent au niveau `Information`. Toutes les autres catégories commençant par « Host », comme « Host.Executor », journalisent au niveau `Error`.| 

## <a name="queues"></a>queues

Paramètre de configuration pour les [déclencheurs et liaisons de file d’attente de stockage](functions-bindings-storage-queue.md).

```json
{
    "queues": {
      "maxPollingInterval": 2000,
      "visibilityTimeout" : "00:00:30",
      "batchSize": 16,
      "maxDequeueCount": 5,
      "newBatchThreshold": 8
    }
}
```

|Propriété  |Default | Description |
|---------|---------|---------| 
|maxPollingInterval|60000|Intervalle maximal (en millisecondes) entre les interrogations de la file d’attente.| 
|visibilityTimeout|0|Intervalle de temps entre les nouvelles tentatives en cas d’échec du traitement d’un message.| 
|batchSize|16|Nombre de messages en file d’attente à récupérer et à traiter en parallèle. La valeur maximale est de 32.| 
|maxDequeueCount|5|Nombre de tentatives de traitement d’un message avant de le placer dans la file d’attente de messages incohérents.| 
|newBatchThreshold|batchSize/2|Seuil auquel un nouveau lot de messages est extrait.| 

## <a name="servicebus"></a>serviceBus

Paramètre de configuration pour les [déclencheurs et liaisons Service Bus](functions-bindings-service-bus.md).

[!INCLUDE [functions-host-json-service-bus](../../includes/functions-host-json-service-bus.md)]

## <a name="singleton"></a>singleton

Paramètres de configuration du comportement de verrouillage Singleton. Pour plus d’informations, consultez l’article sur le [problème de GitHub relatif à la prise en charge de singleton](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```json
    "singleton": {
      "lockPeriod": "00:00:15",
      "listenerLockPeriod": "00:01:00",
      "listenerLockRecoveryPollingInterval": "00:01:00",
      "lockAcquisitionTimeout": "00:01:00",
      "lockAcquisitionPollingInterval": "00:00:03"
    }
}
```

|Propriété  |Default | Description |
|---------|---------|---------| 
|lockPeriod|00:00:15|Période pendant laquelle des verrous sont établis au niveau des fonctions. Les verrous se renouvellent automatiquement.| 
|listenerLockPeriod|00:01:00|Période pendant laquelle des verrous sont établis au niveau des écouteurs.| 
|listenerLockRecoveryPollingInterval|00:01:00|Intervalle de temps utilisé pour la récupération des verrous d’écouteurs si un verrou de ce type n’a pas pu être acquis au démarrage.| 
|lockAcquisitionTimeout|00:01:00|Période de temps maximale pendant laquelle le runtime essaie d’acquérir un verrou.| 
|lockAcquisitionPollingInterval|n/a|Intervalle écoulé entre les tentatives d’acquisition de verrou.| 

## <a name="tracing"></a>tracing

Paramètres de configuration des journaux que vous créez à l’aide d’un objet `TraceWriter`. Consultez les sections relatives à la [journalisation en C#](functions-reference-csharp.md#logging) et à la [journalisation Node.js](functions-reference-node.md#writing-trace-output-to-the-console). 

```json
{
    "tracing": {
      "consoleLevel": "verbose",
      "fileLoggingMode": "debugOnly"
    }
}
```

|Propriété  |Default | Description |
|---------|---------|---------| 
|consoleLevel|info|Niveau de suivi pour la journalisation de la console. Options : `off`, `error`, `warning`, `info` et `verbose`.|
|fileLoggingMode|debugOnly|Niveau de suivi pour la journalisation des fichiers. Options : `never`, `always`, `debugOnly`.| 

## <a name="watchdirectories"></a>watchDirectories

Ensemble de [répertoires de code partagé](functions-reference-csharp.md#watched-directories) dont les modifications doivent être surveillées.  Garantit que lorsque le code contenu dans ces répertoires est modifié, les changements sont récupérés par vos fonctions.

```json
{
    "watchDirectories": [ "Shared" ]
}
```

## <a name="durabletask"></a>durableTask

Nom du [hub de tâches](durable-functions-task-hubs.md) pour l’extension [Fonctions durables](durable-functions-overview.md).

```json
{
  "durableTask": {
    "HubName": "MyTaskHub"
  }
}
```

Les noms de hubs de tâches doivent commencer par une lettre et contenir uniquement des lettres et des chiffres. S’il n’est pas spécifié, le nom du hub de tâches par défaut d’une application de fonction est **DurableFunctionsHub**. Pour en savoir plus, consultez la section relative aux [hubs de tâches](durable-functions-task-hubs.md).


## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Découvrez comment mettre à jour le fichier host.json](functions-reference.md#fileupdate)

> [!div class="nextstepaction"]
> [Consultez les paramètres globaux des variables d’environnement](functions-app-settings.md)
