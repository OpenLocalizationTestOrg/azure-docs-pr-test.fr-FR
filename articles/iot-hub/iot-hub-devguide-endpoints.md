---
title: points de terminaison Azure IoT Hub aaaUnderstand | Documents Microsoft
description: "Guide du développeur – informations de référence sur les points de terminaison côté appareil et côté service IoT Hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 57ba52ae-19c6-43e4-bc6c-d8a5c2476e95
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 8647f15d2f2a050ad5799ea82f4d2d46db0dbec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-endpoints"></a>Référence - Points de terminaison IoT Hub

## <a name="iot-hub-names"></a>Noms IoT Hub

Vous pouvez trouver le nom hello du hub IoT hello qui héberge vos points de terminaison dans le portail hello sur hello **vue d’ensemble** panneau. Par défaut, le nom DNS de hello d’un hub IoT ressemble : `{your iot hub name}.azure-devices.net`.

Vous pouvez utiliser Azure DNS toocreate un nom DNS personnalisé pour votre hub IoT. Pour plus d’informations, consultez [paramètres de domaine personnalisé tooprovide utiliser Azure DNS pour un service Azure](../dns/dns-custom-domain.md#azure-iot).

## <a name="list-of-built-in-iot-hub-endpoints"></a>Liste de points de terminaison IoT Hub intégrés

IoT Hub Azure est un service de plusieurs locataire qui expose ses acteurs toovarious de fonctionnalité. Hello diagramme suivant montre hello différents points de terminaison qui expose de IoT Hub.

![Points de terminaison IoT Hub][img-endpoints]

Hello suivant liste décrit les points de terminaison hello :

* **Fournisseur de ressources**. Hello fournisseur de ressources IoT Hub expose un [Azure Resource Manager] [ lnk-arm] interface. Cette interface permet toocreate de propriétaires d’abonnement Azure et supprimer des IoT hubs et des propriétés de hub IoT tooupdate. Propriétés de IoT Hub régissent [des stratégies de sécurité au niveau du concentrateur][lnk-accesscontrol], et non le contrôle d’accès toodevice et options fonctionnelles pour la messagerie cloud sur l’appareil et de périphérique dans le cloud. Hello fournisseur de ressources IoT Hub vous permet également de trop[exporter les identités d’appareil][lnk-importexport].
* **Gestion d’identité de l’appareil**. Chaque hub IoT expose un ensemble d’identités de périphérique de toomanage de points de terminaison HTTP REST (créer, récupérer, mettre à jour et supprimer). Les [identités des appareils][lnk-device-identities] sont utilisées pour l’authentification des appareils et le contrôle d’accès.
* **Gestion des représentations d’appareils**. Chaque hub IoT expose un ensemble de service côté tooquery de point de terminaison HTTP REST et mise à jour [jumeaux de périphérique] [ lnk-twins] (mettre à jour les étiquettes et les propriétés).
* **Gestion des travaux**. Expose un ensemble de tooquery de point de terminaison HTTP REST côté service et de gérer chaque hub IoT [travaux][lnk-jobs].
* **Points de terminaison des appareils**. Pour chaque périphérique dans le Registre des identités hello, IoT Hub expose un ensemble de points de terminaison :

  * *Envoyer des messages appareil-à-cloud*. Un appareil utilise ce point de terminaison trop[envoyer des messages de l’appareil-à-cloud][lnk-d2c].
  * *Recevoir des messages cloud-à-appareil*. Un appareil utilise ce tooreceive de point de terminaison ciblé [messages cloud-à-appareil][lnk-c2d].
  * *Initier des téléchargements de fichiers*. Un appareil utilise ce point de terminaison de tooreceive un URI de SAS du stockage Azure à partir de IoT Hub trop[télécharger un fichier][lnk-upload].
  * *Récupérer et mettre à jour les propriétés d’une représentation d’appareil*. Un appareil utilise ce point de terminaison tooaccess son [double de l’appareil][lnk-twins]de propriétés.
  * *Recevoir des requêtes de méthodes directes*. Un appareil utilise ce toolisten de point de terminaison pour [méthode directe][lnk-methods]de demandes.

    Ces points de terminaison sont exposés à l’aide des protocoles [MQTT v3.1.1][lnk-mqtt], HTTP 1.1 et [AMQP 1.0][lnk-amqp]. Le protocole AMQP est également disponible sur [WebSockets][lnk-websockets], sur le port 443.

    Hello appareil jumeaux et méthodes de points de terminaison sont disponibles uniquement lorsque vous utilisez hello [MQTT v3.1.1] [ lnk-mqtt] protocole.

* **Points de terminaison de service**. Chaque hub IoT expose un ensemble de points de terminaison pour votre toocommunicate back-end de solution avec vos appareils. Une exception, ces points de terminaison ne sont exposés à l’aide de hello [AMQP] [ lnk-amqp] protocole. point de terminaison appel de méthode Hello est exposé sur hello le protocole HTTP.
  
  * *Recevoir des messages Appareil vers cloud*. Ce point de terminaison est compatible avec [Azure Event Hubs][lnk-event-hubs]. Un service principal peut utiliser tooread hello [messages appareil-à-cloud] [ lnk-d2c] envoyé par vos périphériques. Vous pouvez créer des points de terminaison personnalisés sur votre hub IoT dans point de terminaison addition toothis intégrés.
  * *Envoyer des messages Cloud vers appareil et recevoir des accusés de remise*. Ces points de terminaison activer votre toosend de back-end solution fiable [messages cloud-à-appareil][lnk-c2d], et tooreceive hello correspondants accusés de réception de remise ou d’expiration.
  * *Recevoir les notifications de fichier*. Permet de ce point de terminaison de messagerie vous tooreceive des notifications de vos appareils téléchargement correctement un fichier. 
  * *Invocation de méthode directe*. Ce point de terminaison permet à un service principal de tooinvoke un [méthode directe] [ lnk-methods] sur un appareil.
  * *Recevoir les événements de surveillance des opérations*. Ce point de terminaison vous permet de surveillance des événements si votre IoT hub a été configuré tooemit des opérations de tooreceive les. Pour plus d’informations, consultez [Surveillance des opérations IoT Hub][lnk-operations-mon].

Hello [kits de développement logiciel Azure IoT] [ lnk-sdks] décrit hello différentes façons tooaccess ces points de terminaison.

Tous les points de terminaison IoT Hub utilisent hello [TLS] [ lnk-tls] protocole et aucun point de terminaison est jamais exposé sur les canaux de déchiffrés/non sécurisés.

## <a name="custom-endpoints"></a>Points de terminaison personnalisés

Vous pouvez lier des services Azure existants dans votre tooact de hub IoT abonnement tooyour en tant que points de terminaison pour le routage des messages. Ces points de terminaison de service jouent le rôle de points de terminaison de service et sont utilisés pour les routages de message. Les périphériques ne peut pas écrire directement toohello points de terminaison supplémentaires. toolearn savoir plus sur les itinéraires de message, consultez l’entrée de guide de développement de hello sur [envoyer et recevoir des messages avec IoT hub][lnk-devguide-messaging].

IoT Hub prend actuellement en charge hello suivant des services Azure en tant que points de terminaison supplémentaires :

* Event Hubs
* Files d'attente Service Bus
* Rubriques de Service Bus

IoT Hub a besoin de points de terminaison de service un accès en écriture toothese pour toowork de routage de message. Si vous configurez vos points de terminaison via hello portail Azure, les autorisations nécessaires hello sont ajoutées pour vous. Assurez-vous de que configurer vos services toosupport hello attendu de débit. Lorsque vous configurez tout d’abord votre solution IoT, vous pouvez peut-être toomonitor vos points de terminaison supplémentaires et effectuer les ajustements nécessaires pour la charge réelle hello.

Si un message correspond à plusieurs itinéraires que tous les point de toohello même point de terminaison IoT Hub fournit le point de terminaison de message toothat qu’une seule fois. C’est donc pas besoin de déduplication de tooconfigure sur votre file d’attente du Bus de Service ou une rubrique. Dans les files d’attente partitionnées, l’affinité de la partition assure le classement des messages.

> [!NOTE]
> Les options **Sessions** ou **Détection des doublons** ne doivent pas être activées pour les files d’attente et rubriques Service Bus utilisées comme points de terminaison IoT Hub. Si une de ces options sont activée, le point de terminaison hello s’affiche en tant que **inaccessible** Bonjour portail Azure.

Pour hello limites hello nombre de points de terminaison que vous pouvez ajouter, consultez [Quotas et la limitation][lnk-devguide-quotas].

## <a name="field-gateways"></a>Passerelles de champ

Dans une solution IoT, une *passerelle de champ* se situe entre vos appareils et vos points de terminaison IoT Hub. Il est généralement situé tooyour fermer pour les appareils. Vos appareils communiquent directement avec la passerelle de champ hello en utilisant un protocole pris en charge par les appareils hello. passerelle de champ Hello connecte tooan point de terminaison IoT Hub à l’aide d’un protocole pris en charge par IoT Hub. Une passerelle de champ peut être un matériel dédié ou un ordinateur à faible puissance exécutant un logiciel de passerelle personnalisé.

Vous pouvez utiliser [Azure IoT bord] [ lnk-iot-edge] tooimplement une passerelle de champ. IoT bord offre des fonctionnalités telles que les communications à partir de plusieurs périphériques sur hello de multiplexage même connexion IoT Hub.

## <a name="next-steps"></a>Étapes suivantes

Les autres rubriques de référence dans le Guide du développeur IoT Hub comprennent :

* [Langage de requête IoT Hub pour les jumeaux d’appareils, les travaux et le routage des messages][lnk-devguide-query]
* [Quotas et limitation][lnk-devguide-quotas]
* [Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt]

[lnk-iot-edge]: https://github.com/Azure/iot-edge

[img-endpoints]: ./media/iot-hub-devguide-endpoints/endpoints.png
[lnk-amqp]: https://www.amqp.org/
[lnk-mqtt]: http://mqtt.org/
[lnk-websockets]: https://tools.ietf.org/html/rfc6455
[lnk-arm]: ../azure-resource-manager/resource-group-overview.md
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/

[lnk-tls]: https://tools.ietf.org/html/rfc5246


[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-accesscontrol]: iot-hub-devguide-security.md#access-control-and-permissions
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-device-identities]: iot-hub-devguide-identity-registry.md
[lnk-upload]: iot-hub-devguide-file-upload.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md

[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[lnk-operations-mon]: iot-hub-operations-monitoring.md
