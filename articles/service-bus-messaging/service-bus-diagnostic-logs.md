---
title: les journaux de diagnostic de Service Bus aaaAzure | Documents Microsoft
description: "Découvrez comment tooset des journaux de diagnostic pour Service Bus dans Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a>Journaux de diagnostic Service Bus

Vous pouvez afficher deux types de journaux pour Azure Service Bus :
* **[Journaux d’activité](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Ces journaux contiennent des informations sur les opérations effectuées sur un travail. Hello journaux sont toujours activés.
* **[Journaux de diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. Vous pouvez configurer les journaux de diagnostic pour obtenir des informations plus détaillés sur tous les événements associés à un travail. Activités de couverture de journaux de diagnostic de hello création des travaux de hello jusqu'à ce que le travail de hello est supprimé, y compris les mises à jour et les activités qui se produisent pendant l’exécution du travail de hello.

## <a name="turn-on-diagnostic-logs"></a>Activer les journaux de diagnostic

Les journaux de diagnostic sont désactivés par défaut. journaux de diagnostic tooenable, effectuez hello comme suit :

1.  Bonjour [portail Azure](https://portal.azure.com), sous **analyse + gestion**, cliquez sur **les journaux de diagnostic**.

    ![Panneau navigation toodiagnostic journaux](./media/service-bus-diagnostic-logs/image1.png)

2. Cliquez sur ressource hello toomonitor.  

3.  Cliquez sur **Activer les diagnostics**.

    ![activer les journaux de diagnostic](./media/service-bus-diagnostic-logs/image2.png)

4.  Pour l’**état**, cliquez sur **ACTIVÉ**.

    ![modifier l’état des journaux de diagnostic](./media/service-bus-diagnostic-logs/image3.png)

5.  Ensemble hello archive cible que vous le souhaitez. par exemple, un compte de stockage, un Hub d’événements ou Analytique des journaux Azure.

6.  Enregistrer les nouveaux paramètres de diagnostics hello.

Les nouveaux paramètres prennent effet au bout de 10 minutes environ. Après cela, des journaux apparaissent dans la cible d’archivage hello configuré, sur hello **les journaux de diagnostic** panneau.

Pour plus d’informations sur la configuration des diagnostics, consultez hello [vue d’ensemble des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Schéma des journaux de diagnostic

Tous les journaux sont stockés au format JSON (JavaScript Object Notation). Chaque entrée comporte des champs de chaîne qui utilisent le format hello décrit Bonjour suivant la section.

## <a name="operational-logs-schema"></a>Schéma des journaux des opérations

Se connecte hello **OperationalLogs** catégorie capturer que se passe-t-il lors des opérations de Service Bus. Plus précisément, ces journaux capturer le type d’opération hello, y compris la création de file d’attente, les ressources utilisées et hello l’état de fonctionnement de hello.

Chaînes JSON de journal des opérations incluent les éléments répertoriés dans hello tableau suivant :

Nom | Description
------- | -------
ActivityId | ID interne, utilisé à des fins de suivi
EventName | Nom d’opération           
resourceId | ID de ressource Azure Resource Manager
SubscriptionId | Identifiant d’abonnement
EventTimeString | Durée de l’opération
EventProperties | Propriétés de l’opération
État | État de l’opération
Appelant | Appelant de l’opération (portail Azure ou client de gestion)
category | OperationalLogs

Voici un exemple de chaîne JSON du journal des opérations :

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Étapes suivantes

Visitez hello suivant les liens toolearn plus sur le Bus de Service :

* [Introduction tooService Bus](service-bus-messaging-overview.md)
* [Bien démarrer avec Service Bus](service-bus-dotnet-get-started-with-queues.md)
