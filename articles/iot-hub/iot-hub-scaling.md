---
title: "Mise à l’échelle Azure IoT Hub | Microsoft Docs"
description: "Mise à l’échelle de votre IoT hub pour prendre en charge votre débit de messages prévu. Inclut un résumé du débit pris en charge pour chaque niveau et des options pour le partitionnement."
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
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="89281-104">Mettre à l’échelle votre solution IoT Hub</span><span class="sxs-lookup"><span data-stu-id="89281-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="89281-105">Azure IoT Hub peut prendre en charge jusqu’à un million d’appareils connectés simultanément.</span><span class="sxs-lookup"><span data-stu-id="89281-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="89281-106">Pour plus d’informations, consultez la [tarification IoT Hub][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="89281-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="89281-107">Chaque unité IoT Hub autorise un certain nombre de messages quotidiens.</span><span class="sxs-lookup"><span data-stu-id="89281-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="89281-108">Pour mettre correctement à l’échelle votre solution, étudiez votre utilisation particulière d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="89281-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="89281-109">Prenez plus particulièrement en compte le débit maximal requis pour les catégories d’opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="89281-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="89281-110">Messages Appareil vers cloud</span><span class="sxs-lookup"><span data-stu-id="89281-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="89281-111">Messages Cloud vers appareil</span><span class="sxs-lookup"><span data-stu-id="89281-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="89281-112">Opérations du registre d’identité</span><span class="sxs-lookup"><span data-stu-id="89281-112">Identity registry operations</span></span>

<span data-ttu-id="89281-113">Outre ces informations sur le débit, consultez les [quotas et limitations IoT Hub][IoT Hub quotas and throttles] et concevez votre solution en conséquence.</span><span class="sxs-lookup"><span data-stu-id="89281-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="89281-114">Débit de message Appareil vers cloud et Cloud vers appareil.</span><span class="sxs-lookup"><span data-stu-id="89281-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="89281-115">La meilleure façon de dimensionner une solution IoT Hub consiste à évaluer le trafic sur une base par unité.</span><span class="sxs-lookup"><span data-stu-id="89281-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="89281-116">Les messages Appareil vers cloud respectent les recommandations de débit soutenu.</span><span class="sxs-lookup"><span data-stu-id="89281-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="89281-117">Niveau</span><span class="sxs-lookup"><span data-stu-id="89281-117">Tier</span></span> | <span data-ttu-id="89281-118">Débit soutenu</span><span class="sxs-lookup"><span data-stu-id="89281-118">Sustained throughput</span></span> | <span data-ttu-id="89281-119">Vitesse de transmission soutenue</span><span class="sxs-lookup"><span data-stu-id="89281-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89281-120">S1</span><span class="sxs-lookup"><span data-stu-id="89281-120">S1</span></span> |<span data-ttu-id="89281-121">Jusqu’à 1 111 Ko/minute par unité</span><span class="sxs-lookup"><span data-stu-id="89281-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="89281-122">(1,5 Go/jour/unité)</span><span class="sxs-lookup"><span data-stu-id="89281-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="89281-123">Moyenne de 278 messages/minute par unité</span><span class="sxs-lookup"><span data-stu-id="89281-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="89281-124">(400 000 messages/jour par unité)</span><span class="sxs-lookup"><span data-stu-id="89281-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="89281-125">S2</span><span class="sxs-lookup"><span data-stu-id="89281-125">S2</span></span> |<span data-ttu-id="89281-126">Jusqu’à 16 Mo/minute par unité</span><span class="sxs-lookup"><span data-stu-id="89281-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="89281-127">(22,8 Go/jour/unité)</span><span class="sxs-lookup"><span data-stu-id="89281-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="89281-128">Moyenne de 4167 messages/minute par unité</span><span class="sxs-lookup"><span data-stu-id="89281-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="89281-129">(6 millions de messages/jour par unité)</span><span class="sxs-lookup"><span data-stu-id="89281-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="89281-130">S3</span><span class="sxs-lookup"><span data-stu-id="89281-130">S3</span></span> |<span data-ttu-id="89281-131">Jusqu’à 814 Mo/minute par unité</span><span class="sxs-lookup"><span data-stu-id="89281-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="89281-132">(1144,4 Go/jour/unité)</span><span class="sxs-lookup"><span data-stu-id="89281-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="89281-133">Moyenne de 208 333 messages/minute par unité</span><span class="sxs-lookup"><span data-stu-id="89281-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="89281-134">(300 millions de messages/jour par unité)</span><span class="sxs-lookup"><span data-stu-id="89281-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="89281-135">Débit des opérations de registre d’identité</span><span class="sxs-lookup"><span data-stu-id="89281-135">Identity registry operation throughput</span></span>
<span data-ttu-id="89281-136">Les opérations de registre d’identité IoT Hub ne sont pas censées être des opérations d’exécution, car elles sont principalement liées à l’approvisionnement d’appareils.</span><span class="sxs-lookup"><span data-stu-id="89281-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="89281-137">Pour obtenir les pics de performances spécifiques, consultez [Quotas et limitations IoT Hub][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="89281-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="89281-138">Partitionnement</span><span class="sxs-lookup"><span data-stu-id="89281-138">Sharding</span></span>
<span data-ttu-id="89281-139">Un hub IoT unique peut recevoir des millions d’appareils, mais votre solution nécessite parfois des caractéristiques de performances spécifiques qu’un seul hub IoT ne peut pas assurer.</span><span class="sxs-lookup"><span data-stu-id="89281-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="89281-140">Dans ce cas, il est recommandé de partitionner vos appareils en plusieurs IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="89281-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="89281-141">L’utilisation de plusieurs IoT Hubs permet de simplifier les pics de trafic et d’obtenir le débit requis ou les taux d’opération requis.</span><span class="sxs-lookup"><span data-stu-id="89281-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89281-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89281-142">Next steps</span></span>
<span data-ttu-id="89281-143">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="89281-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="89281-144">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="89281-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="89281-145">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="89281-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
