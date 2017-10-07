---
title: "options d’aaaAzure IoT Hub appareil-à-cloud | Documents Microsoft"
description: "Guide du développeur - obtenir des conseils sur lorsque les messages appareil-à-cloud toouse, les propriétés déclarées ou fichier Téléchargez pour les communications du cloud sur l’appareil."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Recommandations sur les communications appareil-à-cloud
Lors de l’envoi des informations à partir de hello appareil application toohello solution back-end, IoT Hub expose trois options :

* Les [messages appareil-à-cloud][lnk-d2c], pour la télémétrie et les alertes de série chronologique.
* [Signalé propriétés] [ lnk-twins] pour les rapports des informations d’état de périphérique tels que les fonctionnalités disponibles, conditions ou d’état hello de flux de travail de longue. Par exemple, les mises à jour de configuration et de logiciels.
* [Téléchargements de fichiers] [ lnk-fileupload] support de fichiers et les lots de télémétrie volumineux téléchargés par les appareils connectés par intermittence ou compressés toosave de bande passante.

Voici une comparaison détaillée de hello diverses options de communication de l’appareil-à-cloud.

|  | Messages appareil-à-cloud | Propriétés signalées | Chargements de fichiers |
| ---- | ------- | ---------- | ---- |
| Scénario | Télémétrie et alertes de série chronologique. Par exemple, les lots de données de capteur de 256 Ko envoyés toutes les 5 minutes. | Capacités et conditions disponibles. Par exemple, hello actuel appareil mode de connectivité telles que cellulaire ou Wi-Fi. Synchronisation des workflows de longue durée, comme les mises à jour logicielles et de la configuration. | Fichiers multimédias. Lots de télémétrie volumineux (généralement compressés). |
| Stockage et récupération | Temporairement stockées par IoT Hub, too7 jours. Lecture uniquement séquentielle. | Stockées par IoT Hub en double d’appareil hello. Récupérables à l’aide de hello [langage de requête IoT Hub][lnk-query]. | Stockées dans le compte de stockage Azure fourni par l’utilisateur. |
| Taille | Les messages de too256 Ko. | La taille maximale des propriétés signalées est de 8 Ko. | Taille maximale de fichier prise en charge par le stockage Blob Azure. |
| Fréquence | Élevée. Pour plus d’informations, consultez les [limites d’IoT Hub][lnk-quotas]. | Moyenne. Pour plus d’informations, consultez les [limites d’IoT Hub][lnk-quotas]. | Faible. Pour plus d’informations, consultez les [limites d’IoT Hub][lnk-quotas]. |
| Protocole | Disponible sur tous les protocoles. | Disponible actuellement uniquement lorsque vous utilisez MQTT. | Disponible lorsque vous utilisez n’importe quel protocole, mais nécessite HTTP sur le périphérique de hello. |

Il est possible qu’une application requiert des informations d’envoi de tooboth comme une série chronologique de télémétrie ou alerte et également toomake accessibles dans le double de périphérique hello. Dans ce scénario, vous pouvez choisir l’une des options suivantes de hello :

* application Hello envoie un message de l’appareil-à-cloud et signale une modification de propriété.
* Hello solution back-end peut stocker des informations de hello dans les balises du double hello appareil lorsqu’il reçoit le message de type hello.

Étant donné que les messages appareil-à-cloud activer un quantité débit plus élevé que les mises à jour de périphériques double, il est parfois souhaitable de tooavoid double périphérique hello mise à jour pour tous les messages appareil-à-cloud.


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
