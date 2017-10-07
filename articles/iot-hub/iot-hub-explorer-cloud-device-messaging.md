---
title: Appareil de cloud Azure IoT Hub aaaManage messagerie avec iothub-explorer | Documents Microsoft
description: "Découvrez comment toouse hello messages toocloud (D2C) de l’appareil iothub-explorer CLI outil toomonitor et envoyer des messages de toodevice (C2D) de cloud dans Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "l’Explorateur d’iothub, appareil de cloud de messagerie, iot hub cloud toodevice, cloud toodevice de messagerie"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Utilisez l’Explorateur du iothub toosend et recevoir des messages entre votre appareil et un IoT Hub

![Diagramme de bout en bout](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[iothub-explorer](https://github.com/azure/iothub-explorer) dispose d’un certain nombre de commandes qui facilitent la gestion d’IoT Hub. Ce didacticiel se concentre sur la façon de toouse iothub-explorer toosend et recevoir des messages entre votre appareil et votre hub IoT.

## <a name="what-you-will-learn"></a>Contenu

Vous apprendrez comment toouse les messages appareil-à-cloud explorer d’iothub toomonitor et les messages de cloud-à-appareil toosend. Messages appareil-à-cloud peut être des données de capteur que votre appareil collecte et envoie ensuite tooyour IoT hub. Messages cloud-à-appareil peut être votre hub IoT envoie tooyour périphérique tooblink une DEL qui est connecté tooyour périphérique de commandes.

## <a name="what-you-will-do"></a>Procédure à suivre

- Utilisez les messages appareil-à-cloud explorer d’iothub toomonitor.
- Utiliser des messages de cloud-à-appareil toosend iothub-explorer.

## <a name="what-you-need"></a>Ce dont vous avez besoin

- Didacticiel [configurer votre appareil](iot-hub-raspberry-pi-kit-node-get-started.md) terminé qui couvre hello suivant les exigences :
  - Un abonnement Azure actif.
  - Une instance Azure IoT Hub associée à votre abonnement.
  - Une application cliente qui envoie le concentrateur de messages tooyour Azure IoT.
- iothub-explorer. ([Installer iothub-explorer](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>Analyse de messages appareil vers cloud

toomonitor les messages qui sont envoyés à partir de votre appareil tooyour IoT de supervision, procédez comme suit :

1. Ouvrez une fenêtre de console.
1. Exécutez hello de commande suivante :

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > Obtenez `<device-id>` et `<IoTHubConnectionString>` à partir de votre instance IoT Hub. Assurez-vous que vous avez terminé le didacticiel précédent de hello. Vous pouvez également essayer toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` si vous avez `HostName`, `SharedAccessKeyName` et `SharedAccessKey`.

## <a name="send-cloud-to-device-messages"></a>Envoi de messages cloud vers appareil

toosend un message à partir de votre appareil tooyour de hub IoT, procédez comme suit :

1. Ouvrez une fenêtre de console.
1. Démarrer une session sur votre IoT hub en exécutant hello de commande suivante :

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Envoyer un message de périphérique de tooyour en exécutant hello commande suivante :

   ```bash
   iothub-explorer send <device-id> <message>
   ```

commande Hello clignote hello DEL tooyour connecté appareil et envoie le dispositif de tooyour message hello.

> [!Note]
> Pas besoin de hello appareil toosend un accusé de réception distincts commande tooyour précédent IoT hub est lors de la réception du message de type hello.

## <a name="next-steps"></a>Étapes suivantes

Vous avez appris comment toomonitor appareil-à-cloud des messages et envoyer des messages cloud-à-appareil entre les appareils IoT Azure IoT Hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
