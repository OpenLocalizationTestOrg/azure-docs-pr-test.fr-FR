---
title: messagerie de Azure IoT Hub aaaUnderstand | Documents Microsoft
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
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="9ca65-104">Messagerie d’appareil-à-cloud et de cloud-à-appareil avec IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9ca65-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="9ca65-105">Utiliser l’IoT Hub toocommunicate de messagerie avec vos appareils par :</span><span class="sxs-lookup"><span data-stu-id="9ca65-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="9ca65-106">Envoi de [appareil-à-cloud] [ lnk-d2c] messages à partir de votre solution de tooyour périphériques back-end.</span><span class="sxs-lookup"><span data-stu-id="9ca65-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="9ca65-107">Envoi de [cloud-à-appareil] [ lnk-c2d] tooyour périphériques de fin de messages à partir de la solution hello précédent.</span><span class="sxs-lookup"><span data-stu-id="9ca65-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="9ca65-108">Propriétés principales de la fonctionnalité de messagerie IoT Hub sont hello et des messages.</span><span class="sxs-lookup"><span data-stu-id="9ca65-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="9ca65-109">Ces propriétés activent la connectivité de toointermittent de résilience côté hello d’appareil, et tooload des pics se produisent dans l’événement de traitement sur le côté du cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9ca65-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="9ca65-110">IoT Hub implémente *au moins une fois* des garanties de remise pour l’envoi de messages appareil-à-cloud et cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="9ca65-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="9ca65-111">Pour une fonctionnalités toohello introduction d’IoT Hub, consultez les articles de hello [Azure et Internet of Things] [ lnk-azure-iot] et [vue d’ensemble de hello Azure IoT Hub service] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="9ca65-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="9ca65-112">Lors de la messagerie de toouse IoT Hub</span><span class="sxs-lookup"><span data-stu-id="9ca65-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="9ca65-113">Utiliser les messages appareil-à-cloud pour l’envoi de télémétrie de série de temps et des alertes à partir de votre application et des messages cloud-à-appareil pour l’application de périphérique tooyour notifications unidirectionnel.</span><span class="sxs-lookup"><span data-stu-id="9ca65-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="9ca65-114">Consultez trop[des conseils de communication de périphérique dans le cloud] [ lnk-d2c-guidance] en cas de doute entre l’utilisation de messages appareil-à-cloud, les propriétés déclarées ou téléchargement du fichier.</span><span class="sxs-lookup"><span data-stu-id="9ca65-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="9ca65-115">Consultez trop[des conseils de communication Cloud-à-appareil] [ lnk-c2d-guidance] en cas de doute entre l’utilisation des messages cloud-à-appareil, propriétés ou méthodes directes.</span><span class="sxs-lookup"><span data-stu-id="9ca65-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ca65-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ca65-116">Next steps</span></span>

* <span data-ttu-id="9ca65-117">Découvrez la [messagerie appareil-à-cloud][lnk-d2c] IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9ca65-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="9ca65-118">Découvrez la [messagerie cloud-à-appareil][lnk-c2d] IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9ca65-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md