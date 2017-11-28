---
title: Comprendre les kits IoT Azure SDK | Microsoft Docs
description: "Guide du développeur - informations et liens vers divers kits Azure IoT device et service SDK que vous pouvez utiliser pour créer des applications d’appareil et des applications principales."
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
ms.openlocfilehash: bcbf4b9633f58293edb19aeb33dec6602ac4ec8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="4746c-103">Comprendre et utiliser les kits Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="4746c-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="4746c-104">Il existe trois catégories de kit SDK à utiliser avec IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="4746c-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="4746c-105">Les kits **device SDK** vous permettent de créer des applications qui s’exécuteront sur vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="4746c-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="4746c-106">Ces applications envoient des données de télémétrie à votre hub IoT et reçoivent éventuellement des messages provenant de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4746c-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="4746c-107">Les kits **service SDK** vous permettent de gérer votre hub IoT et éventuellement d’envoyer des messages à vos appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="4746c-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="4746c-108">**Azure IoT Edge** permet de créer des passerelles pour activer les appareils qui n’utilisent pas l’un des protocoles pris en charge, ou lorsque vous devez traiter des messages en périphérie.</span><span class="sxs-lookup"><span data-stu-id="4746c-108">**Azure IoT Edge** enables you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="4746c-109">Les kits SDK prennent en charge plusieurs langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="4746c-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="4746c-110">Kits Azure IoT device SDK</span><span class="sxs-lookup"><span data-stu-id="4746c-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="4746c-111">Les kits Microsoft Azure IoT device SDK contiennent du code qui facilite la création d’appareils et d’applications qui se connectent aux services Azure IoT Hub et sont gérés par eux.</span><span class="sxs-lookup"><span data-stu-id="4746c-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="4746c-112">Vous pouvez télécharger les kits Azure IoT device SDK suivants à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="4746c-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="4746c-113">[Azure IoT device SDK pour C][lnk-c-device-sdk] : écrit en C ANSI (C99) pour la portabilité et la compatibilité de nombreuses plateformes.</span><span class="sxs-lookup"><span data-stu-id="4746c-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="4746c-114">Il existe deux bibliothèques clientes d’appareil pour C, **iothub_client** de bas niveau et **serializer**.</span><span class="sxs-lookup"><span data-stu-id="4746c-114">There are two device client libraries for C, the low-level **iothub_client** and the **serializer**.</span></span>
* <span data-ttu-id="4746c-115">[Azure IoT device SDK pour .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="4746c-116">[Azure IoT device SDK pour Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="4746c-117">[Azure IoT device SDK pour Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="4746c-118">[Azure IoT device SDK pour Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="4746c-119">Consultez les fichiers lisez-moi dans les dépôts GitHub pour plus d’informations sur l’utilisation du langage et des gestionnaires de packages spécifiques à la plateforme pour installer les fichiers binaires et dépendances sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="4746c-119">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="4746c-120">Compatibilité des plateformes de système d’exploitation et du matériel</span><span class="sxs-lookup"><span data-stu-id="4746c-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="4746c-121">Pour plus d’informations sur la compatibilité des kits SDK avec des appareils physiques spécifiques, consultez le [catalogue d’appareils Azure Certified pour IoT][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="4746c-121">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="4746c-122">Kits Azure IoT service SDK</span><span class="sxs-lookup"><span data-stu-id="4746c-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="4746c-123">Les kits Azure IoT service SDK contiennent du code pour faciliter la création d’applications qui interagissent directement avec IoT Hub pour gérer les appareils et la sécurité.</span><span class="sxs-lookup"><span data-stu-id="4746c-123">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="4746c-124">Vous pouvez télécharger les kits Azure IoT service SDK suivants à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="4746c-124">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="4746c-125">[Azure IoT service SDK pour .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="4746c-126">[Azure IoT service SDK pour Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="4746c-127">[Azure IoT service SDK pour Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="4746c-128">[Azure IoT service SDK pour Java][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="4746c-129">[Azure IoT service SDK pour C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="4746c-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="4746c-130">Consultez les fichiers lisez-moi dans les dépôts GitHub pour plus d’informations sur l’utilisation du langage et des gestionnaires de packages spécifiques à la plateforme pour installer les fichiers binaires et dépendances sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="4746c-130">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="4746c-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="4746c-131">Azure IoT Edge</span></span>

<span data-ttu-id="4746c-132">Azure IoT Edge contient l’infrastructure et les modules nécessaires pour créer des solutions de passerelle IoT.</span><span class="sxs-lookup"><span data-stu-id="4746c-132">Azure IoT Edge contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="4746c-133">Vous pouvez étendre IoT Edge pour créer des passerelles adaptées à n’importe quel scénario de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="4746c-133">You can extend IoT Edge to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="4746c-134">[Azure IoT Edge][lnk-iot-edge] est téléchargeable à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="4746c-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="4746c-135">Documentation de référence sur les API en ligne</span><span class="sxs-lookup"><span data-stu-id="4746c-135">Online API reference documentation</span></span>

<span data-ttu-id="4746c-136">La liste suivant contient des liens vers la documentation de référence sur les API en ligne pour les bibliothèques d’appareils, de services et de passerelles Azure IoT :</span><span class="sxs-lookup"><span data-stu-id="4746c-136">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="4746c-137">[Internet des objets (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="4746c-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="4746c-138">[IoT Hub REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="4746c-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="4746c-139">[Azure IoT device SDK pour C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="4746c-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="4746c-140">[Azure IoT device SDK pour Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="4746c-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="4746c-141">[Azure IoT service SDK pour Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="4746c-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="4746c-142">[Azure IoT device SDK pour Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="4746c-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="4746c-143">[Azure IoT service SDK pour Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="4746c-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="4746c-144">[Azure IoT Edge][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="4746c-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="4746c-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4746c-145">Next steps</span></span>

<span data-ttu-id="4746c-146">Les autres rubriques de référence de ce Guide du développeur IoT Hub comprennent :</span><span class="sxs-lookup"><span data-stu-id="4746c-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4746c-147">[Points de terminaison IoT Hub][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="4746c-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="4746c-148">[Langage de requête IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="4746c-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="4746c-149">[Quotas et limitation][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="4746c-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="4746c-150">[Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="4746c-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
