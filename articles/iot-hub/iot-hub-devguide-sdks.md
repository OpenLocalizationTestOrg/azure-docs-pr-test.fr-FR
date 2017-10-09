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
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="3e8b6-103">Comprendre et utiliser les kits Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="3e8b6-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="3e8b6-104">Il existe trois catégories de kit SDK à utiliser avec IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="3e8b6-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="3e8b6-105">**Kits de développement logiciel appareil** permettent de toobuild les applications qui s’exécutent sur vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="3e8b6-106">Ces applications IoT hub tooyour de télémétrie d’envoi et éventuellement recevoir des messages à partir de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="3e8b6-107">**Kits de développement logiciel service** activer vous toomanage votre IoT hub et éventuellement envoyer des messages tooyour des appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="3e8b6-108">**Azure IoT bord** vous permet des appareils toobuild passerelles tooenable qui n’utilisez pas un des protocoles de hello pris en charge, ou lorsque vous devez tooprocess des messages sur les bords de hello.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="3e8b6-109">Kits de développement logiciel sont fournis toosupport plusieurs langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="3e8b6-110">Kits Azure IoT device SDK</span><span class="sxs-lookup"><span data-stu-id="3e8b6-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="3e8b6-111">Hello kits de développement logiciel de Microsoft Azure IoT appareil contenir du code qui facilite la construction des appareils et applications qui se connectent tooand sont gérées par les services Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="3e8b6-112">Hello des kits de développement Azure IoT périphérique suivantes sont toodownload disponible à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="3e8b6-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="3e8b6-113">[Azure IoT device SDK pour C][lnk-c-device-sdk] : écrit en C ANSI (C99) pour la portabilité et la compatibilité de nombreuses plateformes.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="3e8b6-114">Il existe deux bibliothèques de client de périphérique pour C, hello bas niveau **iothub_client** et hello **sérialiseur**.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="3e8b6-115">[Azure IoT device SDK pour .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="3e8b6-116">[Azure IoT device SDK pour Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="3e8b6-117">[Azure IoT device SDK pour Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="3e8b6-118">[Azure IoT device SDK pour Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="3e8b6-119">Consultez les fichiers readme dans hello dans des référentiels GitHub hello pour plus d’informations sur l’utilisation de langage et les binaires de tooinstall spécifique à la plateforme package gestionnaires et les dépendances sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="3e8b6-120">Compatibilité des plateformes de système d’exploitation et du matériel</span><span class="sxs-lookup"><span data-stu-id="3e8b6-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="3e8b6-121">Pour plus d’informations sur la compatibilité du Kit de développement logiciel avec des périphériques matériels spécifiques, consultez hello [Azure certifié pour le catalogue de périphérique IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="3e8b6-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="3e8b6-122">Kits Azure IoT service SDK</span><span class="sxs-lookup"><span data-stu-id="3e8b6-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="3e8b6-123">service de Azure IoT Hello kits de développement logiciel contiennent toofacilitate code création d’applications qui interagissent directement avec la sécurité et les appareils toomanage IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="3e8b6-124">Hello SDK de service Azure IoT suivantes est toodownload disponible à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="3e8b6-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="3e8b6-125">[Azure IoT service SDK pour .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="3e8b6-126">[Azure IoT service SDK pour Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="3e8b6-127">[Azure IoT service SDK pour Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="3e8b6-128">[Azure IoT service SDK pour Java][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="3e8b6-129">[Azure IoT service SDK pour C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="3e8b6-130">Consultez les fichiers readme dans hello dans des référentiels GitHub hello pour plus d’informations sur l’utilisation de langage et les binaires de tooinstall spécifique à la plateforme package gestionnaires et les dépendances sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="3e8b6-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="3e8b6-131">Azure IoT Edge</span></span>

<span data-ttu-id="3e8b6-132">Azure IoT bord contient hello infrastructure et les modules toocreate IoT solutions de passerelle.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="3e8b6-133">Vous pouvez étendre le scénario de bout en bout IoT bord toocreate passerelles tooany adaptés.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="3e8b6-134">[Azure IoT Edge][lnk-iot-edge] est téléchargeable à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3e8b6-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="3e8b6-135">Documentation de référence sur les API en ligne</span><span class="sxs-lookup"><span data-stu-id="3e8b6-135">Online API reference documentation</span></span>

<span data-ttu-id="3e8b6-136">Hello liste suivante contient des liens tooonline API documentation de référence sur Azure IoT DISPOSITIF, service et les bibliothèques de passerelle :</span><span class="sxs-lookup"><span data-stu-id="3e8b6-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="3e8b6-137">[Internet des objets (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="3e8b6-138">[IoT Hub REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="3e8b6-139">[Azure IoT device SDK pour C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="3e8b6-140">[Azure IoT device SDK pour Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="3e8b6-141">[Azure IoT service SDK pour Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="3e8b6-142">[Azure IoT device SDK pour Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="3e8b6-143">[Azure IoT service SDK pour Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="3e8b6-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e8b6-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e8b6-145">Next steps</span></span>

<span data-ttu-id="3e8b6-146">Les autres rubriques de référence de ce Guide du développeur IoT Hub comprennent :</span><span class="sxs-lookup"><span data-stu-id="3e8b6-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="3e8b6-147">[Points de terminaison IoT Hub][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="3e8b6-148">[Langage de requête IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="3e8b6-149">[Quotas et limitation][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="3e8b6-150">[Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="3e8b6-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
