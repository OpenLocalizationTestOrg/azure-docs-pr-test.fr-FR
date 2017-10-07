---
title: aaaAzure gestion des appareils IoT avec iothub-explorer | Documents Microsoft
description: "Utilisez hello iothub-CLI outil Explorateur pour la gestion des appareils Azure IoT Hub, présentant les méthodes directes hello et options de gestion de propriétés souhaitées du double hello."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gestion des appareils iot azure, gestion des appareils azure iot hub, gestion des appareils iot, gestion des appareils iot hub
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Utilisation de iothub-explorer pour la gestion des appareils Azure IoT Hub

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[Explorateur d’iothub](https://github.com/azure/iothub-explorer) est un outil d’interface CLI que vous exécutez sur une identité d’appareil hôte ordinateur toomanage dans le Registre du hub IoT. Il est fourni avec les options de gestion que vous pouvez utiliser tooperform différentes tâches.

| Option de gestion          | Task                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Méthodes directes             | Rendre un périphérique agissent comme le démarrage ou l’arrêt d’envoi de messages ou le redémarrage du périphérique de hello.                                        |
| Propriétés souhaitées pour la représentation    | Mettre un appareil dans certains États, telles que la définition d’un toogreen LED ou définition de données de télémétrie hello too30 intervalle d’envoi.         |
| Propriétés signalées pour la représentation   | Obtenir hello a signalé l’état d’un périphérique. Par exemple, les appareils hello signale hello que LED clignote maintenant.                                    |
| Balises de représentation                  | Stocker les métadonnées spécifiques au périphérique dans le cloud de hello. Par exemple, hello emplacement de déploiement d’un distributeur automatique.                         |
| Messages Cloud vers appareil   | Envoyer les notifications de périphérique tooa. Par exemple, « il est très probable toorain aujourd'hui. N’oubliez pas toobring un parapluie. »              |
| Requêtes de jumeaux d’appareil        | Requête tooretrieve de jumeaux tous les appareils dotés de conditions arbitraires, telles que l’identification des unités hello qui sont disponibles pour une utilisation. |

Pour plus d’explications sur les différences de hello et des conseils sur l’utilisation de ces options, consultez [des conseils de communication de périphérique dans le cloud](iot-hub-devguide-d2c-guidance.md) et [des conseils de communication Cloud-à-appareil](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Les représentations d’appareil sont des documents JSON qui stockent des informations sur l’état des appareils (métadonnées, configurations et conditions). IoT Hub conserve un double du périphérique pour chaque périphérique qui se connecte tooit. Pour plus d’informations sur les représentations d’appareil, consultez [Prise en main des représentations d’appareils](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>Contenu

Vous allez apprendre à utiliser iothub-explorer avec diverses options de gestion sur votre ordinateur de développement.

## <a name="what-you-do"></a>Procédure

Exécutez iothub-diverses avec diverses options de gestion.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :
  - Un abonnement Azure actif.
  - Une instance Azure IoT Hub associée à votre abonnement.
  - Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.
- Assurez-vous que votre appareil est en cours d’exécution avec l’application cliente de hello au cours de ce didacticiel.
- iothub-explorer, [Installez iothub-explorer](https://github.com/azure/iothub-explorer) sur votre ordinateur de développement.

## <a name="connect-tooyour-iot-hub"></a>Se connecter tooyour IoT hub

Se connecter tooyour IoT hub en exécutant hello de commande suivante :

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Utilisation d’iothub-explorer avec des méthodes directes

Appeler hello `start` méthode hello appareil application toosend messages tooyour IoT hub en exécutant hello de commande suivante :

```bash
iothub-explorer device-method <your device Id> start
```

Appeler hello `stop` méthode hello périphérique application toostop envoie des messages tooyour IoT hub en exécutant hello de commande suivante :

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Utiliser iothub-explorer avec les propriétés de représentation souhaitées

Définir un intervalle de la propriété désirée = 3000 en exécutant hello de commande suivante :

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

Cette propriété peut être lue par votre appareil.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Utiliser iothub-explorer avec les propriétés signalées pour la représentation

Obtient hello signalé des propriétés du périphérique hello en exécutant hello commande suivante :

```bash
iothub-explorer get-twin <your device id>
```

Une des propriétés de hello est $metadata. $lastUpdated qui affiche hello dernière cet appareil envoie ou reçoit un message.

## <a name="use-iothub-explorer-with-twins-tags"></a>Utilisez iothub-explorer avec les balises de représentation

Afficher les étiquettes de hello et les propriétés de l’appareil de hello en exécutant hello de commande suivante :

```bash
iothub-explorer get-twin <your device id>
```

Ajouter un rôle de champ = température et humidité appareil de toohello en exécutant hello de commande suivante :

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Utiliser iothub-explorer avec les messages cloud vers appareil

Envoyer un périphérique toohello de message « Hello World » en exécutant hello de commande suivante :

```bash
iothub-explorer send <device-id> "Hello World"
```

Consultez [utiliser l’Explorateur du iothub toosend et recevoir des messages entre votre appareil et un IoT Hub](iot-hub-explorer-cloud-device-messaging.md) pour un scénario réel de l’utilisation de cette commande.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Utiliser iothub-explorer avec des requêtes de représentation d’appareil

Interroger des périphériques avec une balise de rôle = « température et humidité » en exécutant hello de commande suivante :

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Interroger tous les périphériques à l’exception de ceux dont la balise de rôle = « température et humidité » en exécutant hello de commande suivante :

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Étapes suivantes

Vous avez appris comment toouse iothub-Explorateur avec les différentes options de gestion.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
