---
title: messagerie de Azure IoT Hub aaaUnderstand | Documents Microsoft
description: "Guide du développeur - Messagerie d’appareil-à-cloud et de cloud-à-appareil avec IoT Hub. Comprend des informations sur les formats de message et les protocoles de communication pris en charge."
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
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Messagerie d’appareil-à-cloud et de cloud-à-appareil avec IoT Hub

Utiliser l’IoT Hub toocommunicate de messagerie avec vos appareils par :

* Envoi de [appareil-à-cloud] [ lnk-d2c] messages à partir de votre solution de tooyour périphériques back-end.
* Envoi de [cloud-à-appareil] [ lnk-c2d] tooyour périphériques de fin de messages à partir de la solution hello précédent.

Propriétés principales de la fonctionnalité de messagerie IoT Hub sont hello et des messages. Ces propriétés activent la connectivité de toointermittent de résilience côté hello d’appareil, et tooload des pics se produisent dans l’événement de traitement sur le côté du cloud hello. IoT Hub implémente *au moins une fois* des garanties de remise pour l’envoi de messages appareil-à-cloud et cloud-à-appareil.

Pour une fonctionnalités toohello introduction d’IoT Hub, consultez les articles de hello [Azure et Internet of Things] [ lnk-azure-iot] et [vue d’ensemble de hello Azure IoT Hub service] [lnk-iot-hub-overview].

## <a name="when-toouse-iot-hub-messaging"></a>Lors de la messagerie de toouse IoT Hub

Utiliser les messages appareil-à-cloud pour l’envoi de télémétrie de série de temps et des alertes à partir de votre application et des messages cloud-à-appareil pour l’application de périphérique tooyour notifications unidirectionnel.

* Consultez trop[des conseils de communication de périphérique dans le cloud] [ lnk-d2c-guidance] en cas de doute entre l’utilisation de messages appareil-à-cloud, les propriétés déclarées ou téléchargement du fichier.
* Consultez trop[des conseils de communication Cloud-à-appareil] [ lnk-c2d-guidance] en cas de doute entre l’utilisation des messages cloud-à-appareil, propriétés ou méthodes directes.

## <a name="next-steps"></a>Étapes suivantes

* Découvrez la [messagerie appareil-à-cloud][lnk-d2c] IoT Hub.
* Découvrez la [messagerie cloud-à-appareil][lnk-c2d] IoT Hub.

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md