---
title: "Guide Azure IoT Hub | Microsoft Docs"
description: "En tant que développeur, comment utiliser les différentes fonctionnalités IoT Hub ?"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/13/2017
ms.author: dobett
ms.openlocfilehash: b451ea2d42f0ff2f64746bcb296fb9128472fea8
ms.sourcegitcommit: e6029b2994fa5ba82d0ac72b264879c3484e3dd0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-use-azure-iot-hub"></a>Utilisation d’Azure IoT Hub

Vous disposez de plusieurs options pour vous former au développement pour le service IoT Hub :

* Lisez les articles conceptuels qui décrivent les fonctionnalités de IoT Hub en détail.
* Suivez l’un des didacticiels qui couvrent les différentes fonctionnalités de IoT Hub.

## <a name="developer-guide"></a>Guide du développeur

En tant que développeur, vous trouverez des recommandations détaillées sur l’IoT Hub dans le [Guide du développeur][lnk-devguide]. Ce guide comprend les éléments suivants :

* Description détaillée de toutes les fonctionnalités de IoT Hub pour vous aider à les utiliser.
* Conseils pour choisir entre plusieurs options disponibles.

## <a name="tutorials"></a>Didacticiels

Si vous souhaitez découvrir les fonctionnalités spécifiques de IoT Hub par le biais d’exercices pratiques, vous disposez à cet effet de plusieurs didacticiels. La plupart de ces didacticiels sont disponibles dans plusieurs langages de programmation. Voici les didacticiels disponibles :

- [Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires][lnk-routes-tutorial]. Ce didacticiel explique comment utiliser les règles de routage de IoT Hub pour distribuer facilement les messages appareil-à-cloud.

- [Envoi de messages cloud-à-appareil avec IoT Hub][lnk-c2d-tutorial]. Ce didacticiel explique comment envoyer des messages cloud-à-appareil via IoT Hub et comment recevoir des messages cloud-à-appareil sur un appareil.

- [Télécharger des fichiers à partir d’appareils vers le cloud avec IoT Hub][lnk-upload-tutorial]. Ce didacticiel vous montre comment utiliser les fonctions de téléchargement de fichiers de IoT Hub.

- [Prise en main des représentations d’appareils][lnk-twin-tutorial]. Ce didacticiel décrit les jumeaux d’appareils, les propriétés déclarées, les propriétés souhaitées et les balises. Vous pouvez utiliser des jumeaux d’appareils pour synchroniser les valeurs de vos appareils.

- [Utilisation des méthodes directes][lnk-methods-tutorial]. Ce didacticiel explique comment utiliser des méthodes directes. Vous ajoutez un gestionnaire pour une méthode directe dans votre appareil simulé et appelez la méthode directe depuis IoT Hub.

- [Prise en main de la gestion d’appareils][lnk-dm-tutorial]. Ce didacticiel vous montre comment utiliser les principales fonctionnalités de gestion d’appareils, notamment les jumeaux et les méthodes directes. Ces fonctionnalités vous permettent de redémarrer à distance votre appareil simulé.

- [Utilisation des propriétés souhaitées pour configurer des appareils][lnk-properties-tutorial]. Ce didacticiel explique comment combiner les propriétés souhaitées des jumeaux d’appareils aux propriétés signalées afin de configurer votre appareil à distance.

- [Utilisation de la gestion des appareils pour lancer une mise à jour du microprogramme d’un appareil][lnk-jobs-tutorial]. Ce didacticiel vous montre comment utiliser les principales fonctionnalités de gestion d’appareils, notamment les jumeaux et les méthodes directes. Vous apprenez à utiliser ces fonctionnalités pour mettre à jour à distance le microprogramme de votre appareil.

- [Planifier et diffuser des travaux][lnk-schedule-tutorial]. Ce didacticiel vous montre comment utiliser les propriétés souhaitées et les méthodes directes pour interagir avec plusieurs appareils à une heure planifiée.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur le service IoT Hub, consultez le [Guide du développeur][lnk-devguide].

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md