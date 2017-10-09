---
title: "mise à l’échelle du Hub IoT aaaAzure | Documents Microsoft"
description: "Comment tooscale votre toosupport de hub IoT votre débit de message anticipées. Inclut un résumé des options pour le partitionnement et de débit hello pris en charge pour chaque niveau."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="58cda-104">Mettre à l’échelle votre solution IoT Hub</span><span class="sxs-lookup"><span data-stu-id="58cda-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="58cda-105">IoT Hub Azure peut prendre en charge les périphériques connectés simultanément millions de tooa.</span><span class="sxs-lookup"><span data-stu-id="58cda-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="58cda-106">Pour plus d’informations, consultez la [tarification IoT Hub][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="58cda-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="58cda-107">Chaque unité IoT Hub autorise un certain nombre de messages quotidiens.</span><span class="sxs-lookup"><span data-stu-id="58cda-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="58cda-108">tooproperly l’échelle de votre solution, envisagez d’utiliser votre particulier IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="58cda-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="58cda-109">En particulier, considérez le débit de pointe hello requis pour hello suivant des catégories d’opérations :</span><span class="sxs-lookup"><span data-stu-id="58cda-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="58cda-110">Messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="58cda-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="58cda-111">Messages Cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="58cda-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="58cda-112">Opérations du registre d’identité</span><span class="sxs-lookup"><span data-stu-id="58cda-112">Identity registry operations</span></span>

<span data-ttu-id="58cda-113">Dans Ajout toothis débit d’informations, consultez [IoT Hub quotas et les accélérateurs] [ IoT Hub quotas and throttles] et concevoir votre solution en conséquence.</span><span class="sxs-lookup"><span data-stu-id="58cda-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="58cda-114">Débit de message Appareil vers cloud et Cloud vers appareil.</span><span class="sxs-lookup"><span data-stu-id="58cda-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="58cda-115">Hello meilleure manière toosize une solution IoT Hub est le trafic de hello tooevaluate sur une base par unité.</span><span class="sxs-lookup"><span data-stu-id="58cda-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="58cda-116">Les messages Appareil vers cloud respectent les recommandations de débit soutenu.</span><span class="sxs-lookup"><span data-stu-id="58cda-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="58cda-117">Niveau</span><span class="sxs-lookup"><span data-stu-id="58cda-117">Tier</span></span> | <span data-ttu-id="58cda-118">Débit soutenu</span><span class="sxs-lookup"><span data-stu-id="58cda-118">Sustained throughput</span></span> | <span data-ttu-id="58cda-119">Vitesse de transmission soutenue</span><span class="sxs-lookup"><span data-stu-id="58cda-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58cda-120">S1</span><span class="sxs-lookup"><span data-stu-id="58cda-120">S1</span></span> |<span data-ttu-id="58cda-121">Des too1111 Ko par minute par unité</span><span class="sxs-lookup"><span data-stu-id="58cda-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="58cda-122">(1,5 Go/jour/unité)</span><span class="sxs-lookup"><span data-stu-id="58cda-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="58cda-123">Moyenne de 278 messages/minute par unité</span><span class="sxs-lookup"><span data-stu-id="58cda-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="58cda-124">(400 000 messages/jour par unité)</span><span class="sxs-lookup"><span data-stu-id="58cda-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="58cda-125">S2</span><span class="sxs-lookup"><span data-stu-id="58cda-125">S2</span></span> |<span data-ttu-id="58cda-126">Des too16 Mo/minute par unité</span><span class="sxs-lookup"><span data-stu-id="58cda-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="58cda-127">(22,8 Go/jour/unité)</span><span class="sxs-lookup"><span data-stu-id="58cda-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="58cda-128">Moyenne de 4167 messages/minute par unité</span><span class="sxs-lookup"><span data-stu-id="58cda-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="58cda-129">(6 millions de messages/jour par unité)</span><span class="sxs-lookup"><span data-stu-id="58cda-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="58cda-130">S3</span><span class="sxs-lookup"><span data-stu-id="58cda-130">S3</span></span> |<span data-ttu-id="58cda-131">Des too814 Mo/minute par unité</span><span class="sxs-lookup"><span data-stu-id="58cda-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="58cda-132">(1144,4 Go/jour/unité)</span><span class="sxs-lookup"><span data-stu-id="58cda-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="58cda-133">Moyenne de 208 333 messages/minute par unité</span><span class="sxs-lookup"><span data-stu-id="58cda-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="58cda-134">(300 millions de messages/jour par unité)</span><span class="sxs-lookup"><span data-stu-id="58cda-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="58cda-135">Débit des opérations de registre d’identité</span><span class="sxs-lookup"><span data-stu-id="58cda-135">Identity registry operation throughput</span></span>
<span data-ttu-id="58cda-136">Opérations de Registre identité IoT Hub ne sont pas supposées toobe opérations d’exécution, car ils sont principalement associée toodevice de configuration.</span><span class="sxs-lookup"><span data-stu-id="58cda-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="58cda-137">Pour obtenir les pics de performances spécifiques, consultez [Quotas et limitations IoT Hub][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="58cda-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="58cda-138">Partitionnement</span><span class="sxs-lookup"><span data-stu-id="58cda-138">Sharding</span></span>
<span data-ttu-id="58cda-139">Pendant un hub IoT unique peut évoluer toomillions des périphériques, votre solution nécessite parfois des caractéristiques de performances spécifiques qui ne garantit pas un hub IoT unique.</span><span class="sxs-lookup"><span data-stu-id="58cda-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="58cda-140">Dans ce cas, il est recommandé de partitionner vos appareils en plusieurs IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="58cda-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="58cda-141">Les hubs IoT plusieurs lisser les pics de trafic et obtenir un débit requis hello ou taux d’opération qui sont requises.</span><span class="sxs-lookup"><span data-stu-id="58cda-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58cda-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58cda-142">Next steps</span></span>
<span data-ttu-id="58cda-143">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="58cda-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="58cda-144">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="58cda-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="58cda-145">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="58cda-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
