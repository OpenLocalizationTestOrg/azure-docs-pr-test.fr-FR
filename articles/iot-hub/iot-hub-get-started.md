---
title: IoT Hub Azure - prise en main de la connexion de cloud de toohello appareils IoT | Documents Microsoft
description: "Découvrez comment tooconnect les starter kits tooAzure IoT Hub IoT cartes. Vos appareils peuvent envoyer la télémétrie tooIoT Hub IoT Hub peut surveiller et gérer vos appareils."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: Tutoriel Azure IoT Hub
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a>Tutoriels de prise en main d’Azure IoT Hub

Vous pouvez utiliser Azure IoT Hub et les solutions de hello Azure IoT appareils kits de développement logiciel toobuild Internet of Things (IoT) :

* IoT Hub Azure est un service entièrement géré dans le cloud hello qui se connecte en toute sécurité, surveille et gère vos appareils IoT. Utilisez hello kits de développement logiciel Azure IoT appareil tooimplement vos appareils IoT.
* Utilisez une passerelle IoT dans des scénarios IoT plus complexes. Par exemple, où vous devez tooconsider des facteurs tels que des périphériques hérités, les coûts de bande passante, les stratégies de sécurité et de confidentialité ou le traitement des données edge. Dans ces scénarios, vous utilisez Azure IoT bord tooimplement une passerelle qui se connecte IoT hub tooyour de périphériques.

## <a name="what-hello-tutorials-cover"></a>Éléments traitent dans les didacticiels hello

Ces didacticiels présentent tooAzure IoT Hub et l’appareil hello kits de développement logiciel. didacticiels de Hello couvrent les fonctionnalités courantes que IoT scénarios toodemonstrate hello de IoT Hub. Hello didacticiels illustrent également la façon dont toocombine IoT Hub avec autres Azure services et les outils toobuild plus puissantes solutions IoT. Dans les didacticiels hello, vous pouvez choisir toouse des appareils IoT simulées ou réelles. En outre, vous pouvez apprendre comment toouse un IoT hub passerelle tooenable périphériques tooconnect tooyour.

## <a name="set-up-your-device"></a>Configurer votre appareil

Connecter un tooAzure périphérique ou passerelle IoT IoT Hub. Vous pouvez choisir un tooget périphérique physique ou simulé démarré :

| Appareil IoT                       | Langage de programmation |
|----------------------------------|----------------------|
| Raspberry Pi                     | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| IoT DevKit                       | [Arduino dans VSCode][DevKit]     |
| Intel Edison                     | [Node.js][Ed_Nd], [C][Ed_C]    |
| Adafruit Feather HUZZAH ESP8266  | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 Thing Dev       | [Arduino][Th_Ard]              |
| Adafruit Feather M0              | [Arduino][M0_Ard]              |
| Appareil simulé sur PC           | [.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth] |
| Simulateur d’appareil en ligne         | [Raspberry Pi (Node.js)][Ol_Sim] |

En outre, vous pouvez utiliser un IoT hub IoT bord passerelle tooenable périphériques tooconnect tooyour :

| Appareil de passerelle               | Langage de programmation | Plateforme         |
|------------------------------|----------------------|------------------|
| Intel NUC (modèle DE3815TYKE) | C                    | [Wind River Linux][NUC_Lnx] |
| Passerelle simulée            | C                    | [Linux][Sim_Lnx], [Windows][Sim_Win] |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
