---
title: Ports et protocoles de communication IoT Hub | Microsoft Docs
description: "Guide du développeur : décrit les protocoles de communication pris en charge pour les communications appareil-à-cloud et cloud-à-appareil et les numéros de port qui doivent être ouverts."
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
ms.openlocfilehash: 98004a48734e33f85eebf8f6213d9f0751dea843
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# Référence - Choisir un protocole de communication

IoT Hub permet aux appareils d’utiliser les protocoles [MQTT][lnk-mqtt], MQTT sur WebSockets, [AMQP][lnk-amqp], AMQP via WebSockets et HTTP utilisés pour les communications côté appareil. Pour plus d’informations sur la façon dont ces protocoles prennent en charge les fonctionnalités spécifiques d’IoT Hub, consultez [Recommandations sur les communications appareil-à-cloud][lnk-d2c-guidance] et [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].

Le tableau suivant fournit des recommandations de haut niveau pour votre choix de protocole :

| Protocole | Quand choisir ce protocole |
| --- | --- |
| MQTT <br> MQTT sur WebSocket |Utilisez sur tous les appareils ne nécessitant pas de connecter plusieurs appareils (chacun avec ses propres informations d’identification par appareil) à l’aide de la même connexion TLS. |
| AMQP <br> AMQP sur WebSocket |Utiliser sur les passerelles de champ et de cloud pour tirer parti du multiplexage de connexion sur les appareils. |
| HTTP |Utiliser pour les appareils qui ne peuvent pas prendre en charge les autres protocoles. |

Prenez en compte les points suivants lorsque vous choisissez votre protocole pour les communications côté appareil :

* **Modèle cloud-à-appareil**. HTTP ne dispose pas d’un moyen efficace de mettre en œuvre la transmission des messages par le serveur. Par conséquent, lorsque vous utilisez HTTP, les appareils interrogent IoT Hub pour rechercher les messages cloud-à-appareil. Cette approche est inefficace pour l’appareil et pour IoT Hub. Conformément aux recommandations actuelles concernant HTTP, chaque appareil doit interroger la présence de messages toutes les 25 minutes ou plus. En revanche, AMQP et MQTT prennent en charge les notifications Push sur le serveur lors de la réception de messages cloud-à-appareil. Ils permettent d’obtenir des notifications Push immédiates pour les messages IoT Hub-à-appareil. Si la latence de remise pose problème, MQTT ou AMQP sont les meilleurs protocoles à utiliser. Pour les appareils rarement connectés, HTTP fonctionne aussi bien.
* **Passerelles de champ**. Lorsque vous utilisez MQTT et HTTP, il est impossible de connecter plusieurs appareils (chacun avec ses propres informations d’identification par appareil) à l’aide de la même connexion TLS. Ces protocoles ne représentent donc pas la solution optimale pour les [scénarios de passerelle de champ][lnk-azure-gateway-guidance], car ils nécessitent une connexion TLS entre la passerelle de champ et IoT Hub pour chaque appareil connecté à la passerelle de champ.
* **Appareils faibles en ressources**. Les bibliothèques MQTT et HTTP sont moins encombrantes que les bibliothèques AMQP. Donc, si l’appareil dispose de ressources limitées (par exemple, moins de 1 Mo de mémoire RAM), ces protocoles sont peut-être les seuls protocoles d’implémentation disponibles.
* **Traversée réseau**. Le protocole standard AMQP utilise le port 5671, alors que MQTT écoute sur le port 8883, ce qui peut entraîner des problèmes dans les réseaux fermés aux protocoles autres que HTTP. MQTT sur WebSockets, AMQP sur WebSockets et HTTP sont disponibles pour être utilisés dans ce scénario.
* **Taille de charge utile**. MQTT et AMQP sont des protocoles binaires qui génèrent des charges utiles plus compactes que HTTP.

> [!WARNING]
> Lorsque vous utilisez HTTP, chaque appareil doit envoyer des interrogations pour les messages cloud-à-appareil toutes les 25 minutes, voire plus. Toutefois, au cours du développement, il est clairement acceptable d’avoir des fréquences d’interrogation plus régulières que toutes les 25 minutes.

## Numéros de ports

Les appareils peuvent communiquer avec IoT Hub dans Azure à l’aide de divers protocoles. En règle générale, le choix du protocole dépend des exigences spécifiques de la solution. Le tableau suivant répertorie les ports de sortie qui doivent être ouverts pour qu’un appareil puisse utiliser un protocole spécifique :

| Protocole | Port |
| --- | --- |
| MQTT |8883 |
| MQTT sur WebSockets |443 |
| AMQP |5671 |
| AMQP sur WebSockets |443 |
| HTTP |443 |

Lorsque vous avez créé un hub IoT dans une région Azure, ce hub conserve la même adresse IP pendant sa durée de vie. Toutefois, pour maintenir la qualité du service, si Microsoft le fait passer à une autre unité d’échelle, il reçoit une nouvelle adresse IP.


## Étapes suivantes

Pour plus d’informations sur la façon dont IoT Hub implémente le protocole MQTT, consultez [Communication avec votre hub IoT à l’aide du protocole MQTT][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
