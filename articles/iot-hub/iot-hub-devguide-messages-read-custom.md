---
title: "points de terminaison personnalisés aaaUnderstand Azure IoT Hub | Documents Microsoft"
description: "Guide du développeur - utilisant le routage règles des points de terminaison toocustom tooroute messages appareil-à-cloud."
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="a9963-103">Utiliser des itinéraires de messages et des points de terminaison personnalisés pour les messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="a9963-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="a9963-104">IoT Hub vous permet de tooroute [messages appareil-à-cloud] [ lnk-device-to-cloud] tooIoT concentrateur de points de terminaison côté service en fonction des propriétés de message.</span><span class="sxs-lookup"><span data-stu-id="a9963-104">IoT Hub enables you tooroute [device-to-cloud messages][lnk-device-to-cloud] tooIoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="a9963-105">Routage permettent de règles vous hello flexibilité toosend messages où ils ont besoin toogo sans hello besoin pour les messages tooprocess des services supplémentaires ou de code supplémentaire de toowrite.</span><span class="sxs-lookup"><span data-stu-id="a9963-105">Routing rules give you hello flexibility toosend messages where they need toogo without hello need for additional services tooprocess messages or toowrite additional code.</span></span> <span data-ttu-id="a9963-106">Chaque règle de routage que vous configurez a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a9963-106">Each routing rule you configure has hello following properties:</span></span>

| <span data-ttu-id="a9963-107">Propriété</span><span class="sxs-lookup"><span data-stu-id="a9963-107">Property</span></span>      | <span data-ttu-id="a9963-108">Description</span><span class="sxs-lookup"><span data-stu-id="a9963-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="a9963-109">**Name**</span><span class="sxs-lookup"><span data-stu-id="a9963-109">**Name**</span></span>      | <span data-ttu-id="a9963-110">Hello nom unique qui identifie la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="a9963-110">hello unique name that identifies hello rule.</span></span> |
| <span data-ttu-id="a9963-111">**Source**</span><span class="sxs-lookup"><span data-stu-id="a9963-111">**Source**</span></span>    | <span data-ttu-id="a9963-112">origine Hello de données de hello flux toobe réactions.</span><span class="sxs-lookup"><span data-stu-id="a9963-112">hello origin of hello data stream toobe acted upon.</span></span> <span data-ttu-id="a9963-113">Par exemple, télémétrie des appareils.</span><span class="sxs-lookup"><span data-stu-id="a9963-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="a9963-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="a9963-114">**Condition**</span></span> | <span data-ttu-id="a9963-115">expression de requête Hello pour la règle de routage hello qui est exécuté sur les en-têtes et le corps du message de type hello et utilisé toodetermine s’il s’agit d’une correspondance pour le point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="a9963-115">hello query expression for hello routing rule that is run against hello message's headers and body and used toodetermine whether it is a match for hello endpoint.</span></span> <span data-ttu-id="a9963-116">Pour plus d’informations sur la construction d’une condition de routage, consultez hello [- référence de langage de requête pour jumeaux de périphérique et les travaux][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="a9963-116">For more information about constructing a route condition, see hello [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="a9963-117">**Point de terminaison**</span><span class="sxs-lookup"><span data-stu-id="a9963-117">**Endpoint**</span></span>  | <span data-ttu-id="a9963-118">nom Hello du point de terminaison hello où IoT Hub envoie des messages qui correspondent à la condition de hello.</span><span class="sxs-lookup"><span data-stu-id="a9963-118">hello name of hello endpoint where IoT Hub sends messages that match hello condition.</span></span> <span data-ttu-id="a9963-119">Points de terminaison doivent être Bonjour même région comme concentrateur de IoT hello, sinon vous pouvez être facturé pour entre régions écrit.</span><span class="sxs-lookup"><span data-stu-id="a9963-119">Endpoints should be in hello same region as hello IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="a9963-120">Un seul message peut correspondre à condition de hello sur plusieurs règles de routage, dans lequel cas IoT Hub fournit le point de terminaison toohello de message hello associé à chaque règle de mise en correspondance.</span><span class="sxs-lookup"><span data-stu-id="a9963-120">A single message may match hello condition on multiple routing rules, in which case IoT Hub delivers hello message toohello endpoint associated with each matched rule.</span></span> <span data-ttu-id="a9963-121">IoT Hub deduplicates également automatiquement remise des messages, donc si un message correspond à plusieurs règles ayant hello même destination, il est uniquement écrit toothat destination qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="a9963-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have hello same destination, it is only written toothat destination once.</span></span>

<span data-ttu-id="a9963-122">Un hub IoT a par défaut un [point de terminaison intégré][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="a9963-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="a9963-123">Vous pouvez créer des points de terminaison personnalisés tooroute messages tooby liaison d’autres services dans votre concentrateur de toohello d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a9963-123">You can create custom endpoints tooroute messages tooby linking other services in your subscription toohello hub.</span></span> <span data-ttu-id="a9963-124">IoT Hub prend actuellement en charge les points de terminaison personnalisés Event Hubs, les files d’attente Service Bus et les rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a9963-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="a9963-125">Les files d’attente et rubriques Service Bus dont les options **Sessions** ou **Détection des doublons** sont activées ne sont pas prises en charge comme points de terminaison personnalisés.</span><span class="sxs-lookup"><span data-stu-id="a9963-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="a9963-126">Pour plus d’informations sur la création de points de terminaison personnalisés dans IoT Hub, consultez la page [Points de terminaison IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="a9963-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="a9963-127">Pour plus d’informations sur la lecture à partir de points de terminaison personnalisés, consultez :</span><span class="sxs-lookup"><span data-stu-id="a9963-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="a9963-128">Lecture à partir [d’Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="a9963-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="a9963-129">Lecture à partir de [files d’attente Service Bus][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="a9963-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="a9963-130">Lecture à partir de [rubriques Service Bus][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="a9963-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="a9963-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9963-131">Next steps</span></span>

<span data-ttu-id="a9963-132">Pour plus d’informations sur les points de terminaison IoT Hub, consultez [Points de terminaison IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="a9963-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="a9963-133">Pour plus d’informations sur le langage de requête hello vous toodefine les règles de routage, consultez [langage de requête IoT Hub jumeaux d’appareil, les tâches et le routage des messages][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="a9963-133">For more information about hello query language you use toodefine routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="a9963-134">Hello [messages appareil-à-cloud de processus IoT Hub à l’aide d’itinéraires] [ lnk-d2c-tutorial] didacticiel vous montre de fonctionnement des règles de routage de toouse et points de terminaison personnalisés.</span><span class="sxs-lookup"><span data-stu-id="a9963-134">hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how toouse routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
