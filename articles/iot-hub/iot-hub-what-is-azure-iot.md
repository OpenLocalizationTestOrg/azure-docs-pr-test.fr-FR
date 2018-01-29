---
title: "Solutions Azure pour l’Internet des objets (IoT) | Microsoft Docs"
description: "Découvrez une vue d’ensemble d’un exemple d’architecture de solution IoT et sa relation avec les appareils, le service Azure IoT Hub, les kits de développement logiciel (SDK) d’appareils Azure IoT, les kits de développement logiciel de services Azure IoT et autres services Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/15/2017
ms.author: dobett
ms.openlocfilehash: 417ca4b6ecc39cbdafd8e12b5360b370d0ce79fa
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a>Étapes suivantes

Azure IoT Hub est un service Azure qui autorise des communications bidirectionnelles sécurisées et fiables entre votre serveur principal de solution et des millions d’appareils. Grâce à ce service, le serveur de solution principal peut :

* Recevoir des données de télémétrie à grande échelle en provenance de vos appareils
* Acheminer les données vers un processeur d’événements de flux
* Recevoir des fichiers chargés par les appareils
* Envoyez des messages cloud-à-appareil à des appareils spécifiques.

Vous pouvez utiliser IoT Hub pour implémenter votre propre serveur principal de solution. IoT Hub offre aussi un registre d’identités qui permet de configurer des appareils, leurs informations d’identification et leurs droits de connexion à l’IoT Hub. Pour en savoir plus sur IoT Hub, consultez l’article [Qu’est-ce qu’IoT Hub ?][lnk-iot-hub].

Pour découvrir comment Azure IoT Hub permet une gestion des appareils basée sur des normes pour administrer vos appareils à distance, voir [Vue d’ensemble de la gestion des appareils avec IoT Hub][lnk-device-management].

Pour implémenter des applications clientes sur un large éventail de plateformes matérielles et de systèmes d’exploitation d’appareils, vous pouvez utiliser les Kits de développement logiciel (SDK) d’appareils Azure IoT. Le kit de développement logiciel (SDK) contient des bibliothèques qui facilitent l’envoi de télémétrie à un IoT Hub et la réception de messages cloud-vers-appareil. Avec les Kits de développement logiciel (SDK) d’appareils, vous avez le choix parmi plusieurs protocoles réseau pour communiquer avec IoT Hub. Pour plus d’informations, consultez la rubrique [Plus d’informations sur les kits de développement logiciel (SDK) d’appareils][lnk-device-sdks].

Pour commencer à écrire du code et à exécuter certains exemples, consultez le didacticiel [Prise en main d’IoT Hub][lnk-getstarted].

[Azure IoT Suite][lnk-iot-suite] est un ensemble de solutions préconfigurées qui peut vous intéresser. IoT Suite vous permet de démarrer rapidement et de mettre à l’échelle des projets IoT pour résoudre des scénarios IoT courants tels que la surveillance à distance, la gestion des éléments multimédias et la maintenance prédictive.

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
