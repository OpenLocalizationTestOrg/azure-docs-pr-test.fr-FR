---
title: "aaaCompare Azure IoT Hub tooAzure concentrateurs d’événements | Documents Microsoft"
description: "Comparaison de hello IoT Hub et les services Azure de concentrateurs d’événements mettant en surbrillance les différences fonctionnelles et cas d’usage. comparaison de Hello inclut les protocoles pris en charge, la gestion des périphériques, surveillance, et les téléchargements de fichiers."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Comparaison entre Azure IoT Hub et Azure Event Hub
Un des cas d’usage principaux hello pour IoT Hub est télémétrie toogather à partir d’appareils. Pour cette raison, IoT Hub est souvent comparé trop[Azure Event Hubs][Azure Event Hubs]. IoT Hub, comme les concentrateurs d’événements est un service qui permet l’entrée d’événements et les données de télémétrie de traitement des événements cloud toohello à très grande échelle, avec une latence faible et une haute fiabilité.

Toutefois, les services de hello ont beaucoup de différences qui est décrites en détail dans hello tableau suivant :

| Domaine | IoT Hub | Event Hubs |
| --- | --- | --- |
| Modèles de communication | Active [device-to-cloud communications][lnk-d2c-guidance] (messagerie, chargements de fichiers et propriétés signalées) et [cloud-to-device communications][lnk-c2d-guidance] (méthodes directes, propriétés désirées). |Permet uniquement une entrée d’événement (en général utilisé pour les scénarios appareil-à-cloud). |
| Informations d’état de l’appareil | Des [jumeaux d’appareils][lnk-twins] peuvent stocker et interroger les informations d’état de l’appareil. | Aucune information d’état de l’appareil ne peut être stockée. |
| Prise en charge du protocole d’appareil |Prend en charge MQTT, MQTT sur WebSockets, AMQP, AMQP sur WebSocket et HTTP. En outre, IoT Hub fonctionne avec hello [passerelle de protocole Azure IoT][lnk-azure-protocol-gateway], un protocole personnalisable implémentation toosupport personnalisé les protocoles de passerelle. |Prend en charge AMQP, AMQP sur WebSocket et HTTP. |
| Sécurité |Fournit une identité par appareil et le contrôle d’accès révocable. Consultez hello [section sécurité de hello guide du développeur IoT Hub]. |Fournit des [stratégies d’accès partagé][Event Hubs - security] à l’échelle d’Event Hubs, avec une prise en charge de révocation limitée par le biais de [stratégies de l’éditeur][Event Hubs publisher policies]. IoT solutions sont souvent des informations d’identification requises tooimplement une solution personnalisée toosupport par périphérique et les mesures de détection d’usurpation. |
| Surveillance des opérations |Propose IoT solutions toosubscribe tooa nombreux événements de périphériques identity management et connectivité telles que des erreurs d’authentification de chaque périphérique, la limitation et les exceptions de format incorrect. Ces événements permettent tooquickly identifient les problèmes de connectivité au niveau de chaque périphérique hello. |Expose uniquement les mesures d’agrégation. |
| Mettre à l'échelle |Est optimisé toosupport des millions d’appareils connectés simultanément. |Compteurs hello connexions en tant que par [les quotas Azure Event Hubs][Azure Event Hubs quotas]. Sur hello autre part, les concentrateurs d’événements vous permet de partition de hello toospecify pour chaque message envoyé. |
| Kits de développement logiciel (SDK) d’appareil |Fournit des [appareil kits de développement logiciel] [ Azure IoT SDKs] pour de nombreuses plateformes et les langues, plus toodirect MQTT et AMQP APIs HTTP. |Prend en charge sur .NET, Java et C, ajout tooAMQP et les interfaces d’envoi HTTP. |
| Chargement de fichiers |Permet que IoT solutions tooupload fichiers du cloud toohello de périphériques. Comprend un point de terminaison de notification de fichier pour l’intégration du workflow et une catégorie de surveillance des opérations pour le débogage de la prise en charge. | Non pris en charge. |
| Itinéraire des messages toomultiple de points de terminaison | Jusqu'à too10 points de terminaison personnalisés sont pris en charge. Les règles déterminent comment les messages sont routés toocustom de points de terminaison. Pour plus d’informations, consultez [Envoyer et recevoir des messages avec IoT Hub][lnk-devguide-messaging]. | Nécessite un code supplémentaire toobe écrit et hébergés pour la distribution des messages. |

En résumé, même si les cas d’usage uniquement hello est entrée de télémétrie de l’appareil-à-cloud, IoT Hub fournit un service qui est conçu pour la connectivité d’appareils IoT. Il continue des propositions de valeur tooexpand hello pour ces scénarios avec des fonctionnalités spécifiques à IoT. Concentrateurs d’événements est conçu pour l’entrée d’événement à une très grande échelle, à la fois dans le contexte de hello de scénarios de centres de données entre réseaux virtuels et intra-centre de données.

Il n’est pas rare toouse IoT Hub et concentrateurs d’événements dans hello même solution. IoT Hub gère la communication de périphérique dans le cloud de hello et concentrateurs d’événements gère l’entrée d’événement d’étape ultérieure dans les moteurs de traitement en temps réel.

### <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur la planification de votre déploiement IoT Hub, consultez [mise à l’échelle, la haute disponibilité et récupération d’urgence][lnk-scaling].

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec IoT Edge][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[section sécurité de hello guide du développeur IoT Hub]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
