---
title: "options d’aaaAzure IoT Hub cloud-à-appareil | Documents Microsoft"
description: "Guide du développeur - obtenir des conseils sur lorsque toouse diriger les méthodes, du double de l’appareil souhaitées des propriétés ou messages cloud-à-appareil pour les communications du cloud sur l’appareil."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Conseils pour les communications cloud-à-appareil
IoT Hub fournit trois options pour les applications de périphérique applications tooexpose fonctionnalité tooa principal :

* [Diriger les méthodes] [ lnk-methods] pour les communications qui nécessitent une confirmation immédiate du résultat de hello. Les méthodes directes sont souvent utilisées pour un contrôle interactif d’appareil, tel que la mise en marche d’un ventilateur.
* [Double souhaité par propriétés] [ lnk-twins] pour les commandes longues destiné état souhaité de périphérique de hello tooput dans une certaine. Par exemple, définissez too30 d’intervalle hello télémétrie envoi.
* [Messages cloud-à-appareil] [ lnk-c2d] pour l’application de périphérique toohello notifications unidirectionnel.

Voici une comparaison détaillée de hello diverses options de communication du cloud sur l’appareil.

|  | Méthodes directes | Propriétés souhaitées des représentations | Messages Cloud vers appareil |
| ---- | ------- | ---------- | ---- |
| Scénario | Commandes qui nécessitent une confirmation immédiate, par exemple, activer un ventilateur. | Les commandes longues destiné appareil de hello tooput à l’état de votre choix. Par exemple, définissez too30 d’intervalle hello télémétrie envoi. | Application de périphérique toohello notifications unidirectionnel. |
| Flux de données | Bidirectionnel. application d’appareil Hello peut répondre toohello méthode immédiatement. Hello solution back-end reçoit le résultat de hello intelligentes toohello demande. | Unidirectionnel. application d’appareil Hello reçoit une notification de modification de la propriété hello. | Unidirectionnel. application d’appareil Hello reçoit le message de type hello
| Durabilité | Les appareils déconnectés ne sont pas contactés. Hello solution back-end est averti de que cet appareil hello n’est pas connecté. | Les valeurs de propriété sont conservés dans le double de périphérique hello. L’appareil les lira lors de la reconnexion suivante. Les valeurs de propriété sont récupérables par hello [langage de requête IoT Hub][lnk-query]. | Les messages peuvent être conservées par IoT Hub pour les heures de too48. |
| Cibles | Appareil unique utilisant le paramètre **deviceId** ou appareils multiples utilisant le paramètre [jobs][lnk-jobs]. | Appareil unique utilisant le paramètre **deviceId** ou appareils multiples utilisant le paramètre [jobs][lnk-jobs]. | Appareil unique par **deviceId**. |
| Taille | Too8KB demandes et réponses de 8 Ko. | La taille maximum des propriétés souhaitées est de 8 Ko. | Les messages de too64KB. |
| Fréquence | Élevée. Pour plus d’informations, consultez les [limites d’IoT Hub][lnk-quotas]. | Moyenne. Pour plus d’informations, consultez les [limites d’IoT Hub][lnk-quotas]. | Faible. Pour plus d’informations, consultez les [limites d’IoT Hub][lnk-quotas]. |
| Protocole | Disponible actuellement uniquement lorsque vous utilisez MQTT. | Disponible actuellement uniquement lorsque vous utilisez MQTT. | Disponible sur tous les protocoles. L’appareil doit interroger lors de l’utilisation de HTTP. |

Découvrez comment toouse directe des méthodes, les propriétés souhaitées et les messages cloud-à-appareil Bonjour suivant didacticiels :

* [Utiliser les méthodes directes][lnk-methods-tutorial], pour les méthodes directes ;
* [Utiliser les propriétés souhaitées tooconfigure périphériques][lnk-twin-properties], pour les propriétés ; souhaité par le double de l’appareil 
* [Envoyer des messages cloud-à-appareil][lnk-c2d-tutorial], pour les messages cloud-à-appareil.

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
