---
title: "messagerie de l’appareil-à-cloud Azure IoT Hub d’aaaUnderstand | Documents Microsoft"
description: "Guide du développeur - comment toouse appareil-à-cloud avec IoT Hub de messagerie. Inclut des informations sur l’envoi de données de télémétrie et non-telemtry et à l’aide de routage des messages toodeliver."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>Envoyer des messages appareil-à-cloud tooIoT Hub

télémétrie de série chronologique toosend et des alertes de vos appareils tooyour solution serveur principal, envoyer des messages de l’appareil-à-cloud à partir de votre appareil tooyour IoT de supervision. Pour une description des autres options appareil-à-cloud prises en charge par IoT Hub, consultez [Recommandations sur les communications appareil-à-cloud][lnk-d2c-guidance].

Vous envoyez des messages appareil-à-cloud via un point de terminaison côté appareil (**/devices/{deviceId}/messages/events**). Règles de routage, puis router votre tooone de messages de points de terminaison de service côté hello sur votre hub IoT. Règles de routage utilisent des en-têtes de hello et corps de messages appareil-à-cloud de hello transitant via votre toodetermine hub où tooroute les. Par défaut, les messages sont routés toohello intégrés côté service point de terminaison (**messages/événements**), qui est compatible avec [concentrateurs d’événements][lnk-event-hubs]. Par conséquent, vous pouvez utiliser la norme [intégration des concentrateurs d’événements et les kits de développement logiciel] [ lnk-compatible-endpoint] tooreceive les messages appareil-à-cloud dans votre solution back-end.

IoT Hub implémente les messages appareil-à-cloud à l’aide d’un modèle de messagerie en streaming. Les messages appareil-à-cloud du IoT Hub sont apparentent [concentrateurs d’événements] [ lnk-event-hubs] *événements* à [Service Bus] [ lnk-servicebus] *messages* dans la mesure où il existe un grand nombre d’événements passent par le service hello qui peut être lu par plusieurs lecteurs.

Appareil-à-cloud avec IoT Hub de messagerie a hello suivant caractéristiques :

* Les messages appareil-à-cloud sont durables et conservée dans la valeur par défaut d’un hub IoT **messages/événements** pour un point de terminaison tooseven jours.
* Les messages appareil-à-cloud peuvent contenir au plus 256 Ko et peuvent être regroupés par lots toooptimize envoie. Les lots ne peuvent pas dépasser 256 Ko.
* Comme expliqué dans hello [tooIoT d’accès contrôle Hub] [ lnk-devguide-security] section, IoT Hub active par périphérique d’authentification et contrôle d’accès.
* IoT Hub vous permet de toocreate des points de terminaison personnalisés too10. Les messages sont remis toohello les points de terminaison selon les itinéraires configurés sur votre hub IoT. Pour plus d’informations, consultez [Règles de routage](#routing-rules).
* IoT Hub autorise des millions d’appareils connectés simultanément (voir [Quotas et la limitation][lnk-quotas]).
* IoT Hub n’autorise pas le partitionnement arbitraire. Les messages appareil-à-cloud sont partitionnés selon leur **deviceId**d’origine.

Pour plus d’informations sur les différences de hello entre hello IoT Hub et les services de concentrateurs d’événements, consultez [comparaison d’Azure IoT Hub et Azure Event Hubs][lnk-comparison].

## <a name="send-non-telemetry-traffic"></a>Envoyer du trafic autre que la télémétrie

Souvent, les appareils en plus des points de données de tootelemetry, envoient des messages et des demandes qui nécessitent d’exécution distinct et la gestion dans hello solution back-end. Par exemple, les alertes critiques qui doivent déclencher une action spécifique Bonjour back-end. Vous pouvez écrire facilement un [règle de routage] [ lnk-devguide-custom] toosend ces types de point de terminaison de messages tooan dédié traitement tootheir selon soit un en-tête de message de type hello ou une valeur dans le corps du message hello.

Pour plus d’informations sur tooprocess moyen hello meilleures ce type de message, consultez hello [didacticiel : comment tooprocess les messages appareil-à-cloud IoT Hub] [ lnk-d2c-tutorial] didacticiel.

## <a name="route-device-to-cloud-messages"></a>Acheminer des messages appareil-à-cloud

Vous avez deux options pour les applications de serveur principal de routage messages appareil-à-cloud tooyour :

* Utiliser hello intégrée [point de terminaison de Hub d’événements compatibles] [ lnk-compatible-endpoint] tooenable principal applications tooread hello appareil-à-cloud les messages reçus par le concentrateur de hello. toolearn sur hello intégré concentrateur d’événements compatibles point de terminaison, consultez [lire les messages de l’appareil-à-cloud à partir du point de terminaison intégrés hello][lnk-devguide-builtin].
* Utilisez routage règles toosend messages toocustom points de terminaison de votre hub IoT. Points de terminaison personnalisés activer vos messages appareil-à-cloud de tooread des applications de serveur principal à l’aide de concentrateurs d’événements, files d’attente Service Bus ou rubriques Service Bus. toolearn sur les points de terminaison de routage et personnalisées, consultez [utiliser des points de terminaison personnalisés et les règles de routage pour les messages de l’appareil-à-cloud][lnk-devguide-custom].

## <a name="anti-spoofing-properties"></a>Propriétés de détection d’usurpation d’identité

APPAREIL tooavoid l’usurpation d’identité dans les messages appareil-à-cloud, IoT Hub tampons tous les messages avec hello propriétés suivantes :

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

Hello tout d’abord deux contient hello **deviceId** et **generationId** Hello provenant d’appareils, comme par [propriétés d’identité de périphérique][lnk-device-properties].

Hello **ConnectionAuthMethod** propriété contient un objet sérialisé au format JSON, avec hello propriétés suivantes :

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les kits de développement logiciel hello, vous pouvez utiliser les messages appareil-à-cloud toosend, consultez [kits de développement logiciel Azure IoT][lnk-sdks].

Hello [prise en main] [ lnk-get-started] didacticiels vous montrent comment les messages toosend appareil-à-cloud à partir d’appareils simulés et physiques. Pour plus d’informations, consultez hello [messages appareil-à-cloud de processus IoT Hub à l’aide d’itinéraires] [ lnk-d2c-tutorial] didacticiel.

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
