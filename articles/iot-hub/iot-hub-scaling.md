---
title: "mise à l’échelle du Hub IoT aaaAzure | Documents Microsoft"
description: "Comment tooscale votre toosupport de hub IoT votre débit de message anticipées. Inclut un résumé des options pour le partitionnement et de débit hello pris en charge pour chaque niveau."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>Mettre à l’échelle votre solution IoT Hub
IoT Hub Azure peut prendre en charge les périphériques connectés simultanément millions de tooa. Pour plus d’informations, consultez la [tarification IoT Hub][lnk-pricing]. Chaque unité IoT Hub autorise un certain nombre de messages quotidiens.

tooproperly l’échelle de votre solution, envisagez d’utiliser votre particulier IoT Hub. En particulier, considérez le débit de pointe hello requis pour hello suivant des catégories d’opérations :

* Messages appareil-à-cloud
* Messages Cloud vers appareil
* Opérations du registre d’identité

Dans Ajout toothis débit d’informations, consultez [IoT Hub quotas et les accélérateurs] [ IoT Hub quotas and throttles] et concevoir votre solution en conséquence.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>Débit de message Appareil vers cloud et Cloud vers appareil.
Hello meilleure manière toosize une solution IoT Hub est le trafic de hello tooevaluate sur une base par unité.

Les messages Appareil vers cloud respectent les recommandations de débit soutenu.

| Niveau | Débit soutenu | Vitesse de transmission soutenue |
| --- | --- | --- |
| S1 |Des too1111 Ko par minute par unité<br/>(1,5 Go/jour/unité) |Moyenne de 278 messages/minute par unité<br/>(400 000 messages/jour par unité) |
| S2 |Des too16 Mo/minute par unité<br/>(22,8 Go/jour/unité) |Moyenne de 4167 messages/minute par unité<br/>(6 millions de messages/jour par unité) |
| S3 |Des too814 Mo/minute par unité<br/>(1144,4 Go/jour/unité) |Moyenne de 208 333 messages/minute par unité<br/>(300 millions de messages/jour par unité) |

## <a name="identity-registry-operation-throughput"></a>Débit des opérations de registre d’identité
Opérations de Registre identité IoT Hub ne sont pas supposées toobe opérations d’exécution, car ils sont principalement associée toodevice de configuration.

Pour obtenir les pics de performances spécifiques, consultez [Quotas et limitations IoT Hub][IoT Hub quotas and throttles].

## <a name="sharding"></a>Partitionnement
Pendant un hub IoT unique peut évoluer toomillions des périphériques, votre solution nécessite parfois des caractéristiques de performances spécifiques qui ne garantit pas un hub IoT unique. Dans ce cas, il est recommandé de partitionner vos appareils en plusieurs IoT hubs. Les hubs IoT plusieurs lisser les pics de trafic et obtenir un débit requis hello ou taux d’opération qui sont requises.

## <a name="next-steps"></a>Étapes suivantes
toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
