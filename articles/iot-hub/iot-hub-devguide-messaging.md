---
title: "Présentation des messages Azure IoT Hub | Microsoft Docs"
description: "Guide du développeur - Messagerie d’appareil-à-cloud et de cloud-à-appareil avec IoT Hub. Comprend des informations sur les formats de message et les protocoles de communication pris en charge."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="c7429-104">Messagerie d’appareil-à-cloud et de cloud-à-appareil avec IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c7429-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="c7429-105">Utilisez la messagerie IoT Hub pour communiquer avec vos appareils en :</span><span class="sxs-lookup"><span data-stu-id="c7429-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="c7429-106">envoyant des messages [appareil-à-cloud][lnk-d2c] depuis vos appareils vers le back-end de votre solution ;</span><span class="sxs-lookup"><span data-stu-id="c7429-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="c7429-107">envoyant des messages [cloud-à-appareil][lnk-c2d] depuis le back-end de la solution vers vos appareils.</span><span class="sxs-lookup"><span data-stu-id="c7429-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="c7429-108">Les principales propriétés de la fonctionnalité de messagerie IoT Hub sont la fiabilité et la durabilité des messages.</span><span class="sxs-lookup"><span data-stu-id="c7429-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="c7429-109">Ces propriétés activent la résilience de la connectivité intermittente côté appareils et des pics de chargement dans le traitement d’événements côté cloud.</span><span class="sxs-lookup"><span data-stu-id="c7429-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="c7429-110">IoT Hub implémente *au moins une fois* des garanties de remise pour l’envoi de messages appareil-à-cloud et cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="c7429-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="c7429-111">Pour obtenir une présentation des fonctionnalités IoT Hub, consultez les articles [Azure et IoT][lnk-azure-iot] et [Présentation du service Azure IoT Hub][lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="c7429-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="c7429-112">Quand utiliser la messagerie IoT Hub</span><span class="sxs-lookup"><span data-stu-id="c7429-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="c7429-113">Utilisez les messages appareil-à-cloud pour envoyer des alertes et des données de télémétrie de série chronologique à partir de votre application pour appareil, et des messages cloud-à-appareil pour envoyer des notifications unidirectionnelles à votre application pour appareil.</span><span class="sxs-lookup"><span data-stu-id="c7429-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="c7429-114">Reportez-vous à [l’aide sur la communication appareil-à-cloud][lnk-d2c-guidance] en cas de doute entre l’utilisation des messages appareil-à-cloud, des propriétés signalées ou du chargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="c7429-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="c7429-115">Reportez-vous à [l’aide sur la communication cloud-à-appareil][lnk-c2d-guidance] en cas de doute entre l’utilisation des messages cloud-à-appareil, des propriétés de votre choix ou des méthodes directes.</span><span class="sxs-lookup"><span data-stu-id="c7429-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7429-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7429-116">Next steps</span></span>

* <span data-ttu-id="c7429-117">Découvrez la [messagerie appareil-à-cloud][lnk-d2c] IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7429-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="c7429-118">Découvrez la [messagerie cloud-à-appareil][lnk-c2d] IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c7429-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md