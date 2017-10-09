---
title: "aaaUnderstand hello kits de développement logiciel Azure IoT | Documents Microsoft"
description: "Guide du développeur - informations et liens toohello différents SDK de périphérique et le service Azure IoT que vous pouvez utiliser les applications de périphérique toobuild et principal."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a>Comprendre et utiliser les kits Azure IoT SDK

Il existe trois catégories de kit SDK à utiliser avec IoT Hub :

* **Kits de développement logiciel appareil** permettent de toobuild les applications qui s’exécutent sur vos appareils IoT. Ces applications IoT hub tooyour de télémétrie d’envoi et éventuellement recevoir des messages à partir de votre hub IoT.

* **Kits de développement logiciel service** activer vous toomanage votre IoT hub et éventuellement envoyer des messages tooyour des appareils IoT.

* **Azure IoT bord** vous permet des appareils toobuild passerelles tooenable qui n’utilisez pas un des protocoles de hello pris en charge, ou lorsque vous devez tooprocess des messages sur les bords de hello.

Kits de développement logiciel sont fournis toosupport plusieurs langages de programmation.

## <a name="azure-iot-device-sdks"></a>Kits Azure IoT device SDK

Hello kits de développement logiciel de Microsoft Azure IoT appareil contenir du code qui facilite la construction des appareils et applications qui se connectent tooand sont gérées par les services Azure IoT Hub.

Hello des kits de développement Azure IoT périphérique suivantes sont toodownload disponible à partir de GitHub :

* [Azure IoT device SDK pour C][lnk-c-device-sdk] : écrit en C ANSI (C99) pour la portabilité et la compatibilité de nombreuses plateformes. Il existe deux bibliothèques de client de périphérique pour C, hello bas niveau **iothub_client** et hello **sérialiseur**.
* [Azure IoT device SDK pour .NET][lnk-dotnet-device-sdk]
* [Azure IoT device SDK pour Java][lnk-java-device-sdk]
* [Azure IoT device SDK pour Node.js][lnk-node-device-sdk]
* [Azure IoT device SDK pour Python][lnk-python-device-sdk]

> [!NOTE]
> Consultez les fichiers readme dans hello dans des référentiels GitHub hello pour plus d’informations sur l’utilisation de langage et les binaires de tooinstall spécifique à la plateforme package gestionnaires et les dépendances sur votre ordinateur de développement.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>Compatibilité des plateformes de système d’exploitation et du matériel

Pour plus d’informations sur la compatibilité du Kit de développement logiciel avec des périphériques matériels spécifiques, consultez hello [Azure certifié pour le catalogue de périphérique IoT][lnk-certified].

## <a name="azure-iot-service-sdks"></a>Kits Azure IoT service SDK

service de Azure IoT Hello kits de développement logiciel contiennent toofacilitate code création d’applications qui interagissent directement avec la sécurité et les appareils toomanage IoT Hub.

Hello SDK de service Azure IoT suivantes est toodownload disponible à partir de GitHub :

* [Azure IoT service SDK pour .NET][lnk-dotnet-service-sdk]
* [Azure IoT service SDK pour Node.js][lnk-node-service-sdk]
* [Azure IoT service SDK pour Java][lnk-java-service-sdk]
* [Azure IoT service SDK pour Java][lnk-python-service-sdk]
* [Azure IoT service SDK pour C][lnk-c-service-sdk]

> [!NOTE]
> Consultez les fichiers readme dans hello dans des référentiels GitHub hello pour plus d’informations sur l’utilisation de langage et les binaires de tooinstall spécifique à la plateforme package gestionnaires et les dépendances sur votre ordinateur de développement.

## <a name="azure-iot-edge"></a>Azure IoT Edge

Azure IoT bord contient hello infrastructure et les modules toocreate IoT solutions de passerelle. Vous pouvez étendre le scénario de bout en bout IoT bord toocreate passerelles tooany adaptés.

[Azure IoT Edge][lnk-iot-edge] est téléchargeable à partir de GitHub.

## <a name="online-api-reference-documentation"></a>Documentation de référence sur les API en ligne

Hello liste suivante contient des liens tooonline API documentation de référence sur Azure IoT DISPOSITIF, service et les bibliothèques de passerelle :

* [Internet des objets (IoT) .NET][lnk-dotnet-ref]
* [IoT Hub REST][lnk-rest-ref]
* [Azure IoT device SDK pour C][lnk-c-ref]
* [Azure IoT device SDK pour Java][lnk-java-ref]
* [Azure IoT service SDK pour Java][lnk-java-service-ref]
* [Azure IoT device SDK pour Node.js][lnk-node-ref]
* [Azure IoT service SDK pour Node.js][lnk-node-service-ref]
* [Azure IoT Edge][lnk-gateway-ref]

## <a name="next-steps"></a>Étapes suivantes

Les autres rubriques de référence de ce Guide du développeur IoT Hub comprennent :

* [Points de terminaison IoT Hub][lnk-devguide-endpoints]
* [Langage de requête IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-devguide-query]
* [Quotas et limitation][lnk-devguide-quotas]
* [Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt]

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
