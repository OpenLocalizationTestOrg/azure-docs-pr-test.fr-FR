---
title: "Présentation de la messagerie d’appareil-à-cloud Azure IoT Hub | Microsoft Docs"
description: "Guide du développeur : comment utiliser la messagerie d’appareil-à-cloud avec IoT Hub. Inclut des informations sur l’envoi de données de télémétrie et autres, ainsi que sur l’utilisation du routage pour remettre les messages."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="a38b4-104">Envoyer des messages appareil-à-cloud sur IoT Hub</span><span class="sxs-lookup"><span data-stu-id="a38b4-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="a38b4-105">Pour envoyer des alertes et des données de télémétrie de série chronologique à partir de vos appareils vers le back-end de votre solution, envoyez des messages appareil-à-cloud depuis votre appareil vers votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a38b4-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="a38b4-106">Pour une description des autres options appareil-à-cloud prises en charge par IoT Hub, consultez [Recommandations sur les communications appareil-à-cloud][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="a38b4-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="a38b4-107">Vous envoyez des messages appareil-à-cloud via un point de terminaison côté appareil (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="a38b4-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="a38b4-108">Les règles d’acheminement acheminent ensuite vos messages vers l’un des points de terminaison côté service sur votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a38b4-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="a38b4-109">Les règles de routage utilisent les en-têtes et corps des messages appareil-à-cloud qui transitent par votre hub pour déterminer où les acheminer.</span><span class="sxs-lookup"><span data-stu-id="a38b4-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="a38b4-110">Par défaut, les messages sont acheminés vers le point de terminaison côté service prédéfini (**messages/events**) compatible avec [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="a38b4-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="a38b4-111">Ainsi, vous pouvez utiliser [l’intégration et les SDK standard Event Hubs][lnk-compatible-endpoint] pour recevoir des messages appareil-à-cloud dans le back-end de votre solution.</span><span class="sxs-lookup"><span data-stu-id="a38b4-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="a38b4-112">IoT Hub implémente les messages appareil-à-cloud à l’aide d’un modèle de messagerie en streaming.</span><span class="sxs-lookup"><span data-stu-id="a38b4-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="a38b4-113">Les messages appareil-à-cloud d’IoT Hub s’apparentent plus à des *événements* [Event Hubs][lnk-event-hubs] qu’à des *messages* [Service Bus][lnk-servicebus] dans la mesure où de nombreux événements transmis par le service peuvent être lus par plusieurs lecteurs.</span><span class="sxs-lookup"><span data-stu-id="a38b4-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="a38b4-114">La messagerie appareil-à-cloud avec IoT Hub présente les caractéristiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="a38b4-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="a38b4-115">Les messages appareil-à-cloud sont durables et sont conservés dans le point de terminaison **messages/events** par défaut d’un hub IoT jusqu’à sept jours.</span><span class="sxs-lookup"><span data-stu-id="a38b4-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="a38b4-116">Les messages appareil-à-cloud ne doivent pas dépasser 256 Ko et peuvent être groupés en lots pour optimiser les envois.</span><span class="sxs-lookup"><span data-stu-id="a38b4-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="a38b4-117">Les lots ne peuvent pas dépasser 256 Ko.</span><span class="sxs-lookup"><span data-stu-id="a38b4-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="a38b4-118">Comme l’explique la section [Contrôler l’accès à IoT Hub][lnk-devguide-security], IoT Hub permet l’authentification et le contrôle d’accès par appareil.</span><span class="sxs-lookup"><span data-stu-id="a38b4-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="a38b4-119">IoT Hub vous permet de créer jusqu'à 10 points de terminaison personnalisés.</span><span class="sxs-lookup"><span data-stu-id="a38b4-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="a38b4-120">Les messages sont remis aux points de terminaison selon les itinéraires configurés sur votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a38b4-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="a38b4-121">Pour plus d’informations, consultez [Règles de routage](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="a38b4-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="a38b4-122">IoT Hub autorise des millions d’appareils connectés simultanément (voir [Quotas et la limitation][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="a38b4-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="a38b4-123">IoT Hub n’autorise pas le partitionnement arbitraire.</span><span class="sxs-lookup"><span data-stu-id="a38b4-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="a38b4-124">Les messages appareil-à-cloud sont partitionnés selon leur **deviceId**d’origine.</span><span class="sxs-lookup"><span data-stu-id="a38b4-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="a38b4-125">Pour plus d’informations sur les différences entre les services IoT Hub et Event Hubs, consultez [Comparaison entre Azure IoT Hub et Azure Event Hub][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="a38b4-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="a38b4-126">Envoyer du trafic autre que la télémétrie</span><span class="sxs-lookup"><span data-stu-id="a38b4-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="a38b4-127">Souvent, outre les points de données de télémétrie, les appareils envoient des messages et demandes qui nécessitent une exécution et une gestion séparées dans le back-end de la solution.</span><span class="sxs-lookup"><span data-stu-id="a38b4-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="a38b4-128">Par exemple, les alertes critiques qui doivent déclencher une action spécifique dans le service principal.</span><span class="sxs-lookup"><span data-stu-id="a38b4-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="a38b4-129">Vous pouvez facilement écrire une [règle de routage][lnk-devguide-custom] qui envoie ces types de messages à un point de terminaison dédié à leur traitement en fonction d’un en-tête sur le message ou d’une valeur dans le corps de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="a38b4-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="a38b4-130">Pour plus d’informations sur la meilleure façon de traiter ce genre de messages, consultez [Didacticiel : traiter les messages appareil-à-cloud IoT Hub][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="a38b4-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="a38b4-131">Acheminer des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="a38b4-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="a38b4-132">Vous avez deux options pour acheminer des messages appareil-à-cloud vers vos applications principales :</span><span class="sxs-lookup"><span data-stu-id="a38b4-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="a38b4-133">Utiliser le [Point de terminaison compatible avec Event Hub][lnk-compatible-endpoint] prédéfini pour permettre aux applications principales de lire les messages appareil-à-cloud que le hub reçoit.</span><span class="sxs-lookup"><span data-stu-id="a38b4-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="a38b4-134">Pour obtenir des informations sur le point de terminaison compatible avec Event Hub prédéfini, consultez [Lire des messages appareil-à-cloud à partir du point de terminaison intégré][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="a38b4-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="a38b4-135">Utiliser des règles de routage pour envoyer des messages à des points de terminaison personnalisés dans votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a38b4-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="a38b4-136">Les points de terminaison personnalisés permettent à vos applications principales de lire les messages appareil-à-cloud à l’aide d’Event Hubs, de files d’attente Service Bus ou de rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a38b4-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="a38b4-137">Pour en savoir plus sur les points de terminaison de routage et personnalisés, consultez [Utiliser des points de terminaison et des règles de routage personnalisés pour les messages appareil-à-cloud][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="a38b4-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="a38b4-138">Propriétés de détection d’usurpation d’identité</span><span class="sxs-lookup"><span data-stu-id="a38b4-138">Anti-spoofing properties</span></span>

<span data-ttu-id="a38b4-139">Pour éviter l’usurpation d’appareil dans les messages appareil-à-cloud, IoT Hub marque tous les messages avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a38b4-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="a38b4-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="a38b4-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="a38b4-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="a38b4-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="a38b4-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="a38b4-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="a38b4-143">Les deux premières propriétés contiennent le **deviceId** et le **generationId** de l’appareil d’origine, conformément aux [Propriétés d’identité des appareils][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="a38b4-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="a38b4-144">La propriété **ConnectionAuthMethod** contient un objet sérialisé JSON avec les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a38b4-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="a38b4-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a38b4-145">Next steps</span></span>

<span data-ttu-id="a38b4-146">Pour plus d’informations sur les SDK que vous pouvez utiliser pour envoyer des messages appareil-à-cloud, consultez [Kits de développement logiciel (SDK) Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="a38b4-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="a38b4-147">Les didacticiels de [prise en main][lnk-get-started] vous montrent comment envoyer des messages appareil-à-cloud à partir d’appareils physiques et d’appareils simulés.</span><span class="sxs-lookup"><span data-stu-id="a38b4-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="a38b4-148">Pour plus de détails, consultez le didacticiel [Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="a38b4-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
