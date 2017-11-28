---
title: "messagerie de l’appareil-à-cloud Azure IoT Hub d’aaaUnderstand | Documents Microsoft"
description: "Guide du développeur - comment toouse appareil-à-cloud avec IoT Hub de messagerie. Inclut des informations sur l’envoi de données de télémétrie et non-telemtry et à l’aide de routage des messages toodeliver."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="8d952-104">Envoyer des messages appareil-à-cloud tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="8d952-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="8d952-105">télémétrie de série chronologique toosend et des alertes de vos appareils tooyour solution serveur principal, envoyer des messages de l’appareil-à-cloud à partir de votre appareil tooyour IoT de supervision.</span><span class="sxs-lookup"><span data-stu-id="8d952-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="8d952-106">Pour une description des autres options appareil-à-cloud prises en charge par IoT Hub, consultez [Recommandations sur les communications appareil-à-cloud][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="8d952-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="8d952-107">Vous envoyez des messages appareil-à-cloud via un point de terminaison côté appareil (**/devices/{deviceId}/messages/events**).</span><span class="sxs-lookup"><span data-stu-id="8d952-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="8d952-108">Règles de routage, puis router votre tooone de messages de points de terminaison de service côté hello sur votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8d952-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="8d952-109">Règles de routage utilisent des en-têtes de hello et corps de messages appareil-à-cloud de hello transitant via votre toodetermine hub où tooroute les.</span><span class="sxs-lookup"><span data-stu-id="8d952-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="8d952-110">Par défaut, les messages sont routés toohello intégrés côté service point de terminaison (**messages/événements**), qui est compatible avec [concentrateurs d’événements][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="8d952-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="8d952-111">Par conséquent, vous pouvez utiliser la norme [intégration des concentrateurs d’événements et les kits de développement logiciel] [ lnk-compatible-endpoint] tooreceive les messages appareil-à-cloud dans votre solution back-end.</span><span class="sxs-lookup"><span data-stu-id="8d952-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="8d952-112">IoT Hub implémente les messages appareil-à-cloud à l’aide d’un modèle de messagerie en streaming.</span><span class="sxs-lookup"><span data-stu-id="8d952-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="8d952-113">Les messages appareil-à-cloud du IoT Hub sont apparentent [concentrateurs d’événements] [ lnk-event-hubs] *événements* à [Service Bus] [ lnk-servicebus] *messages* dans la mesure où il existe un grand nombre d’événements passent par le service hello qui peut être lu par plusieurs lecteurs.</span><span class="sxs-lookup"><span data-stu-id="8d952-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="8d952-114">Appareil-à-cloud avec IoT Hub de messagerie a hello suivant caractéristiques :</span><span class="sxs-lookup"><span data-stu-id="8d952-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="8d952-115">Les messages appareil-à-cloud sont durables et conservée dans la valeur par défaut d’un hub IoT **messages/événements** pour un point de terminaison tooseven jours.</span><span class="sxs-lookup"><span data-stu-id="8d952-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="8d952-116">Les messages appareil-à-cloud peuvent contenir au plus 256 Ko et peuvent être regroupés par lots toooptimize envoie.</span><span class="sxs-lookup"><span data-stu-id="8d952-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="8d952-117">Les lots ne peuvent pas dépasser 256 Ko.</span><span class="sxs-lookup"><span data-stu-id="8d952-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="8d952-118">Comme expliqué dans hello [tooIoT d’accès contrôle Hub] [ lnk-devguide-security] section, IoT Hub active par périphérique d’authentification et contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="8d952-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="8d952-119">IoT Hub vous permet de toocreate des points de terminaison personnalisés too10.</span><span class="sxs-lookup"><span data-stu-id="8d952-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="8d952-120">Les messages sont remis toohello les points de terminaison selon les itinéraires configurés sur votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8d952-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="8d952-121">Pour plus d’informations, consultez [Règles de routage](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="8d952-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="8d952-122">IoT Hub autorise des millions d’appareils connectés simultanément (voir [Quotas et la limitation][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="8d952-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="8d952-123">IoT Hub n’autorise pas le partitionnement arbitraire.</span><span class="sxs-lookup"><span data-stu-id="8d952-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="8d952-124">Les messages appareil-à-cloud sont partitionnés selon leur **deviceId**d’origine.</span><span class="sxs-lookup"><span data-stu-id="8d952-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="8d952-125">Pour plus d’informations sur les différences de hello entre hello IoT Hub et les services de concentrateurs d’événements, consultez [comparaison d’Azure IoT Hub et Azure Event Hubs][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="8d952-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="8d952-126">Envoyer du trafic autre que la télémétrie</span><span class="sxs-lookup"><span data-stu-id="8d952-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="8d952-127">Souvent, les appareils en plus des points de données de tootelemetry, envoient des messages et des demandes qui nécessitent d’exécution distinct et la gestion dans hello solution back-end.</span><span class="sxs-lookup"><span data-stu-id="8d952-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="8d952-128">Par exemple, les alertes critiques qui doivent déclencher une action spécifique Bonjour back-end.</span><span class="sxs-lookup"><span data-stu-id="8d952-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="8d952-129">Vous pouvez écrire facilement un [règle de routage] [ lnk-devguide-custom] toosend ces types de point de terminaison de messages tooan dédié traitement tootheir selon soit un en-tête de message de type hello ou une valeur dans le corps du message hello.</span><span class="sxs-lookup"><span data-stu-id="8d952-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="8d952-130">Pour plus d’informations sur tooprocess moyen hello meilleures ce type de message, consultez hello [didacticiel : comment tooprocess les messages appareil-à-cloud IoT Hub] [ lnk-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8d952-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="8d952-131">Acheminer des messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="8d952-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="8d952-132">Vous avez deux options pour les applications de serveur principal de routage messages appareil-à-cloud tooyour :</span><span class="sxs-lookup"><span data-stu-id="8d952-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="8d952-133">Utiliser hello intégrée [point de terminaison de Hub d’événements compatibles] [ lnk-compatible-endpoint] tooenable principal applications tooread hello appareil-à-cloud les messages reçus par le concentrateur de hello.</span><span class="sxs-lookup"><span data-stu-id="8d952-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="8d952-134">toolearn sur hello intégré concentrateur d’événements compatibles point de terminaison, consultez [lire les messages de l’appareil-à-cloud à partir du point de terminaison intégrés hello][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="8d952-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="8d952-135">Utilisez routage règles toosend messages toocustom points de terminaison de votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8d952-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="8d952-136">Points de terminaison personnalisés activer vos messages appareil-à-cloud de tooread des applications de serveur principal à l’aide de concentrateurs d’événements, files d’attente Service Bus ou rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8d952-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="8d952-137">toolearn sur les points de terminaison de routage et personnalisées, consultez [utiliser des points de terminaison personnalisés et les règles de routage pour les messages de l’appareil-à-cloud][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="8d952-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="8d952-138">Propriétés de détection d’usurpation d’identité</span><span class="sxs-lookup"><span data-stu-id="8d952-138">Anti-spoofing properties</span></span>

<span data-ttu-id="8d952-139">APPAREIL tooavoid l’usurpation d’identité dans les messages appareil-à-cloud, IoT Hub tampons tous les messages avec hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d952-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="8d952-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="8d952-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="8d952-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="8d952-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="8d952-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="8d952-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="8d952-143">Hello tout d’abord deux contient hello **deviceId** et **generationId** Hello provenant d’appareils, comme par [propriétés d’identité de périphérique][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="8d952-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="8d952-144">Hello **ConnectionAuthMethod** propriété contient un objet sérialisé au format JSON, avec hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d952-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="8d952-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d952-145">Next steps</span></span>

<span data-ttu-id="8d952-146">Pour plus d’informations sur les kits de développement logiciel hello, vous pouvez utiliser les messages appareil-à-cloud toosend, consultez [kits de développement logiciel Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="8d952-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="8d952-147">Hello [prise en main] [ lnk-get-started] didacticiels vous montrent comment les messages toosend appareil-à-cloud à partir d’appareils simulés et physiques.</span><span class="sxs-lookup"><span data-stu-id="8d952-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="8d952-148">Pour plus d’informations, consultez hello [messages appareil-à-cloud de processus IoT Hub à l’aide d’itinéraires] [ lnk-d2c-tutorial] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8d952-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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
