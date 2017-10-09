---
title: aaaAzure communication de IoT Hub protocoles et ports | Documents Microsoft
description: "Guide du développeur - décrit hello pris en charge les protocoles de communication pour les communications de périphérique dans le cloud et le cloud sur l’appareil et de numéros de port hello doit être ouvert."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Référence - Choisir un protocole de communication

IoT Hub permet de périphériques toouse [MQTT][lnk-mqtt], MQTT sur WebSockets, [AMQP][lnk-amqp], AMQP via HTTP, WebSockets et protocoles du côté de l’appareil communications. Pour plus d’informations sur la façon dont ces protocoles prennent en charge les fonctionnalités spécifiques d’IoT Hub, consultez [Recommandations sur les communications appareil-à-cloud][lnk-d2c-guidance] et [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].

Hello tableau suivant fournit des recommandations de haut niveau hello de votre choix du protocole :

| Protocole | Quand choisir ce protocole |
| --- | --- |
| MQTT <br> MQTT sur WebSocket |Utilisez plusieurs unités (chacun avec ses propres informations d’identification par périphérique) sur tous les appareils qui ne nécessitent pas de tooconnect sur hello même connexion TLS. |
| AMQP <br> AMQP sur WebSocket |Utilisez parti de tootake passerelles cloud et le champ de connexion multiplexage pour les appareils. |
| HTTP |Utiliser pour les appareils qui ne peuvent pas prendre en charge les autres protocoles. |

Tenez compte des hello lorsque vous choisissez votre protocole pour les communications côté appareil les points suivants :

* **Modèle Cloud vers appareil**. HTTP n’a pas d’un push de serveur de tooimplement de manière efficace. Par conséquent, lorsque vous utilisez HTTP, les appareils interrogent IoT Hub pour rechercher les messages cloud-à-appareil. Cette approche est inefficace pour appareil de hello et IoT Hub. Conformément aux recommandations actuelles concernant HTTP, chaque appareil doit interroger la présence de messages toutes les 25 minutes ou plus. Sur hello autre part, MQTT et AMQP prennent en charge par émission de données serveur lors de la réception des messages cloud-à-appareil. Elles permettent de push immédiate de messages à partir de l’appareil de toohello IoT Hub. Si la latence de livraison est un critère important, MQTT ou AMQP sont toouse de protocoles meilleures hello. Pour les appareils rarement connectés, HTTP fonctionne aussi bien.
* **Passerelles de champ**. Lorsque vous utilisez MQTT et HTTP, plusieurs périphériques (chacun avec ses propres informations d’identification par périphérique) Impossible de se connecter à l’aide de hello même connexion TLS. Par conséquent, pour [champ scénarios de passerelle][lnk-azure-gateway-guidance], ces protocoles sont non optimaux, car elles nécessitent une connexion TLS entre la passerelle de champ hello et IoT Hub pour chaque passerelle de champ appareil toohello connecté.
* **Appareils faibles en ressources**. Hello MQTT et les bibliothèques HTTP ont un plus petit encombrement que les bibliothèques AMQP hello. Par conséquent, si hello périphérique a limité les ressources (par exemple, moins de 1 Mo de RAM), ces protocoles peuvent être hello seule implémentation de protocole disponible.
* **Traversée réseau**. protocole AMQP standard de Hello utilise le port 5671, alors que MQTT est à l’écoute sur le port 8883, ce qui peut provoquer des problèmes dans des réseaux qui sont des protocoles HTTP toonon fermé. MQTT sur WebSockets, AMQP via HTTP et les WebSockets sont toobe disponible utilisé dans ce scénario.
* **Taille de charge utile**. MQTT et AMQP sont des protocoles binaires qui génèrent des charges utiles plus compactes que HTTP.

> [!WARNING]
> Lorsque vous utilisez HTTP, chaque appareil doit envoyer des interrogations pour les messages cloud-à-appareil toutes les 25 minutes, voire plus. Toutefois, pendant le développement, il est acceptable toopoll plus souvent que toutes les 25 minutes.

## Numéros de ports

Les appareils peuvent communiquer avec IoT Hub dans Azure à l’aide de divers protocoles. En règle générale, les choix hello du protocole est piloté par aux exigences de la solution de hello hello. Hello tableau suivant répertorie les ports sortants hello qui doivent être ouverts pour un toouse en mesure de périphérique toobe un protocole spécifique :

| Protocole | Port |
| --- | --- |
| MQTT |8883 |
| MQTT sur WebSockets |443 |
| AMQP |5671 |
| AMQP sur WebSockets |443 |
| HTTP |443 |

Une fois que vous avez créé un hub IoT dans une région Azure, hello conserve de hub IoT hello même adresse IP pour la durée de vie hello de ce hub IoT. Toutefois, toomaintain la qualité de service, si Microsoft déplace l’unité de l’échelle différents tooa hello IoT hub, puis il reçoit une nouvelle adresse IP.


## Étapes suivantes

toolearn en savoir plus sur comment IoT Hub implémente le protocole MQTT hello, consultez [communiquer avec votre IoT hub à l’aide du protocole MQTT hello][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
