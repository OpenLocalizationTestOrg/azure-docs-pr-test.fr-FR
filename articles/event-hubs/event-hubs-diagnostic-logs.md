---
title: "les journaux de diagnostic de concentrateurs d’événements aaaAzure | Documents Microsoft"
description: "Découvrez comment tooset des journaux de diagnostic pour les concentrateurs d’événements dans Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a>Journaux de diagnostic d’Event Hubs

Vous pouvez afficher deux types de journaux pour Azure Event Hubs :
* **[Journaux d’activité](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Ces journaux comportent des informations sur les opérations effectuées sur un travail. Hello journaux sont toujours activés.
* **[Journaux de diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. Vous pouvez configurer les journaux de diagnostic pour obtenir des informations plus détaillées sur tous les événements associés à un travail. Activités de couverture de journaux de diagnostic de hello création des travaux de hello jusqu'à ce que le travail de hello est supprimé, y compris les mises à jour et les activités qui se produisent pendant l’exécution du travail de hello.

## <a name="turn-on-diagnostic-logs"></a>Activer les journaux de diagnostic
Les journaux de diagnostic sont désactivés par défaut. journaux de diagnostic tooenable :

1.  Bonjour [portail Azure](https://portal.azure.com), sous **analyse + gestion**, cliquez sur **les journaux de diagnostic**.

    ![Panneau navigation toodiagnostic journaux](./media/event-hubs-diagnostic-logs/image1.png)

2.  Cliquez sur ressource hello toomonitor.

3.  Cliquez sur **Activer les diagnostics**.

    ![Activer les journaux de diagnostic](./media/event-hubs-diagnostic-logs/image2.png)

4.  Pour l’**état**, cliquez sur **ACTIVÉ**.

    ![Modifier le statut de hello de journaux de diagnostic](./media/event-hubs-diagnostic-logs/image3.png)

5.  Ensemble hello archive cible que vous le souhaitez. par exemple, un compte de stockage, un concentrateur d’événements ou Analytique de journal Azure.

6.  Enregistrer les nouveaux paramètres de diagnostics hello.

Les nouveaux paramètres prennent effet au bout de 10 minutes environ. Après cela, des journaux apparaissent dans la cible d’archivage hello configuré, sur hello **les journaux de diagnostic** panneau.

Pour plus d’informations sur la configuration des diagnostics, consultez hello [vue d’ensemble des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-categories"></a>Catégories de journaux de diagnostic
Event Hubs capture les journaux de diagnostic pour deux catégories :

* **ArchiveLogs**: journaux liés tooEvent concentrateurs archives, plus précisément, consigne que les erreurs de tooarchive connexes.
* **OperationalLogs**: plus d’informations sur ce qui se passe lors des opérations de concentrateurs d’événements, en particulier, hello du type d’opération, y compris la création du concentrateur d’événements, les ressources utilisées et hello l’état de fonctionnement de hello.

## <a name="diagnostic-logs-schema"></a>Schéma des journaux de diagnostic
Tous les journaux sont stockés au format JSON (JavaScript Object Notation). Chaque entrée comporte des champs de chaîne qui utilisent le format hello décrit dans les sections suivantes de hello.

### <a name="archive-logs-schema"></a>Schéma des journaux d’archivage

Chaînes JSON de journal archive incluent les éléments répertoriés dans hello tableau suivant :

Nom | Description
------- | -------
TaskName | Description de la tâche hello qui a échoué.
ActivityId | ID interne, utilisé à des fins de suivi.
trackingId | ID interne, utilisé à des fins de suivi.
resourceId | ID de ressource Azure Resource Manager.
eventHub | Nom complet de l’Event Hub (nom d’espace de noms inclus).
partitionId | Partition Event Hub sur laquelle s’effectue l’opération en écriture.
archiveStep | ArchiveFlushWriter
startTime | Heure de début de la défaillance.
failures | Nombre d’occurrences d’une défaillance.
durationInSeconds | Durée de la défaillance.
Message | Message d’erreur.
category | ArchiveLogs

Hello de code suivant est un exemple d’un journal d’archive chaîne JSON :

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a>Schéma des journaux des opérations

Chaînes JSON de journal des opérations incluent les éléments répertoriés dans hello tableau suivant :

Nom | Description
------- | -------
ActivityId | ID interne utilisé tootrack objectif.
EventName | Nom d’opération.  
resourceId | ID de ressource Azure Resource Manager.
SubscriptionId | l'ID d'abonnement.
EventTimeString | Durée de l’opération.
EventProperties | Propriétés de l’opération.
Statut | État de l’opération.
Appelant | Appelant de l’opération (portail Azure ou client de gestion).
category | OperationalLogs

Hello de code suivant est un exemple d’une chaîne JSON de journal des opérations :

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooEvent concentrateurs](event-hubs-what-is-event-hubs.md)
* [Vue d’ensemble de l'API Event Hubs](event-hubs-api-overview.md)
* [Prise en main des hubs d’événements](event-hubs-csharp-ephcs-getstarted.md)
