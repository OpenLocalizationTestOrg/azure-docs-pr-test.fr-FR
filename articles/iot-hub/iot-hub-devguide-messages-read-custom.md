---
title: "points de terminaison personnalisés aaaUnderstand Azure IoT Hub | Documents Microsoft"
description: "Guide du développeur - utilisant le routage règles des points de terminaison toocustom tooroute messages appareil-à-cloud."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Utiliser des itinéraires de messages et des points de terminaison personnalisés pour les messages appareil-à-cloud

IoT Hub vous permet de tooroute [messages appareil-à-cloud] [ lnk-device-to-cloud] tooIoT concentrateur de points de terminaison côté service en fonction des propriétés de message. Routage permettent de règles vous hello flexibilité toosend messages où ils ont besoin toogo sans hello besoin pour les messages tooprocess des services supplémentaires ou de code supplémentaire de toowrite. Chaque règle de routage que vous configurez a hello propriétés suivantes :

| Propriété      | Description |
| ------------- | ----------- |
| **Name**      | Hello nom unique qui identifie la règle de hello. |
| **Source**    | origine Hello de données de hello flux toobe réactions. Par exemple, télémétrie des appareils. |
| **Condition** | expression de requête Hello pour la règle de routage hello qui est exécuté sur les en-têtes et le corps du message de type hello et utilisé toodetermine s’il s’agit d’une correspondance pour le point de terminaison hello. Pour plus d’informations sur la construction d’une condition de routage, consultez hello [- référence de langage de requête pour jumeaux de périphérique et les travaux][lnk-devguide-query-language]. |
| **Point de terminaison**  | nom Hello du point de terminaison hello où IoT Hub envoie des messages qui correspondent à la condition de hello. Points de terminaison doivent être Bonjour même région comme concentrateur de IoT hello, sinon vous pouvez être facturé pour entre régions écrit. |

Un seul message peut correspondre à condition de hello sur plusieurs règles de routage, dans lequel cas IoT Hub fournit le point de terminaison toohello de message hello associé à chaque règle de mise en correspondance. IoT Hub deduplicates également automatiquement remise des messages, donc si un message correspond à plusieurs règles ayant hello même destination, il est uniquement écrit toothat destination qu’une seule fois.

Un hub IoT a par défaut un [point de terminaison intégré][lnk-built-in]. Vous pouvez créer des points de terminaison personnalisés tooroute messages tooby liaison d’autres services dans votre concentrateur de toohello d’abonnement. IoT Hub prend actuellement en charge les points de terminaison personnalisés Event Hubs, les files d’attente Service Bus et les rubriques Service Bus.

> [!WARNING]
> Les files d’attente et rubriques Service Bus dont les options **Sessions** ou **Détection des doublons** sont activées ne sont pas prises en charge comme points de terminaison personnalisés.

Pour plus d’informations sur la création de points de terminaison personnalisés dans IoT Hub, consultez la page [Points de terminaison IoT Hub][lnk-devguide-endpoints].

Pour plus d’informations sur la lecture à partir de points de terminaison personnalisés, consultez :

* Lecture à partir [d’Event Hubs][lnk-getstarted-eh].
* Lecture à partir de [files d’attente Service Bus][lnk-getstarted-queue].
* Lecture à partir de [rubriques Service Bus][lnk-getstarted-topic].

### <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les points de terminaison IoT Hub, consultez [Points de terminaison IoT Hub][lnk-devguide-endpoints].

Pour plus d’informations sur le langage de requête hello vous toodefine les règles de routage, consultez [langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages][lnk-devguide-query-language].

Hello [messages appareil-à-cloud de processus IoT Hub à l’aide d’itinéraires] [ lnk-d2c-tutorial] didacticiel vous montre de fonctionnement des règles de routage de toouse et points de terminaison personnalisés.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
