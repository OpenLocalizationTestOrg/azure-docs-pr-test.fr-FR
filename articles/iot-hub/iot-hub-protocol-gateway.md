---
title: passerelle de protocole IoT aaaAzure | Documents Microsoft
description: "Comment toouse un Azure IoT protocole protocole prise en charge tooenable périphériques tooconnect tooyour concentrateur à l’aide des protocoles non pris en charge par IoT Hub en mode natif et des fonctionnalités de passerelle tooextend IoT Hub."
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Prise en charge de protocoles supplémentaires pour IoT Hub
IoT Hub Azure en mode natif prend en charge la communication via des protocoles HTTP, AMQP et MQTT hello. Dans certains cas, les appareils ou des passerelles du champ peut ne pas être en mesure de toouse un de ces protocoles standards et nécessiteront une adaptation de protocole. Dans ce cas, vous pouvez utiliser une passerelle personnalisée. Une passerelle personnalisée peut activer adaptation de protocole pour les points de terminaison IoT Hub par pontage tooand de trafic hello de IoT Hub. Vous pouvez utiliser hello [passerelle de protocole Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) comme une adaptation de protocole personnalisé passerelle tooenable pour IoT Hub.

## passerelle de protocole Azure IoT
passerelle de protocole Azure IoT Hello est une infrastructure pour l’adaptation de protocole qui est destinée à grande échelle, la communication bidirectionnelle appareil avec IoT Hub. passerelle de protocole Hello est un composant direct qui accepte les connexions des périphériques via un protocole spécifique. Elle établit un pont entre hello trafic tooIoT Hub via AMQP 1.0. passerelle de protocole Azure IoT Hello est disponible en tant qu’une flexibilité de tooprovide logiciels open source project pour ajouter la prise en charge de différents protocoles et les versions de protocole.

Vous pouvez déployer la passerelle de protocole hello dans Azure de manière hautement évolutive en utilisant Azure Service Fabric, les rôles de travail Azure Cloud Services ou les Machines virtuelles Windows. En outre, la passerelle de protocole hello peut être déployée dans les environnements sur site, telles que des passerelles de champ.

passerelle de protocole Hello Azure IoT inclut un adaptateur de protocole MQTT qui permet de vous toocustomize hello comportement du protocole MQTT si nécessaire. Étant donné que IoT Hub fournit la prise en charge intégrée pour le protocole de v3.1.1 MQTT hello, uniquement tenez à l’aide de la carte du protocole MQTT hello si les personnalisations de protocole ou des exigences spécifiques pour des fonctionnalités supplémentaires sont nécessaires.

l’adaptateur MQTT Hello illustre également le modèle de programmation hello pour la création d’adaptateurs de protocole pour les autres protocoles. En outre, modèle de programmation hello Azure IoT protocole passerelle permet vous tooplug dans les composants personnalisés pour spécialisé traitement telles que l’authentification personnalisée, les transformations de message, compression/décompression ou chiffrement/déchiffrement du trafic entre les appareils hello et IoT Hub.

Pour une flexibilité, la passerelle de protocole hello et l’implémentation de MQTT sont fournis dans un projet de logiciels open source. Cela vous permet de mise en œuvre hello toocustomize en fonction des besoins.

## Étapes suivantes
toolearn plus sur la passerelle de protocole Azure IoT hello et comment toouse et le déployer en tant que partie de votre solution IoT, consultez :

* [Référentiel sur la passerelle de protocole Azure IoT sur GitHub](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Guide du développeur de passerelle de protocole Azure IoT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

toolearn savoir plus sur la planification de votre déploiement IoT Hub, consultez :

* [Comparer à Event Hubs][lnk-compare]
* [Mise à l’échelle, HA et DR][lnk-scaling]
* [Guide du développeur IoT Hub][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
