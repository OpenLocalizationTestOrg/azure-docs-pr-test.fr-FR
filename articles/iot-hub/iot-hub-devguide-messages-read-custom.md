---
title: "Présentation des points de terminaison Azure IoT Hub personnalisés | Microsoft Docs"
description: "Guide du développeur : utilisation de règles de routage pour router les messages appareil-à-cloud vers des points de terminaison."
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
ms.openlocfilehash: a21f1c61f344f96e2e03422e41fd8c5f7f841a0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a><span data-ttu-id="ef729-103">Utiliser des itinéraires de messages et des points de terminaison personnalisés pour les messages appareil-à-cloud</span><span class="sxs-lookup"><span data-stu-id="ef729-103">Use message routes and custom endpoints for device-to-cloud messages</span></span>

<span data-ttu-id="ef729-104">IoT Hub vous permet d’acheminer les [messages appareil-à-cloud][lnk-device-to-cloud] vers des points de terminaison exposés au service IoT Hub en fonction de leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="ef729-104">IoT Hub enables you to route [device-to-cloud messages][lnk-device-to-cloud] to IoT Hub service-facing endpoints based on message properties.</span></span> <span data-ttu-id="ef729-105">Les règles d’acheminement vous offrent la souplesse nécessaire pour envoyer des messages au bon endroit sans avoir besoin de services supplémentaires pour les traiter ou pour écrire du code supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="ef729-105">Routing rules give you the flexibility to send messages where they need to go without the need for additional services to process messages or to write additional code.</span></span> <span data-ttu-id="ef729-106">Chaque règle d’acheminement que vous configurez a les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="ef729-106">Each routing rule you configure has the following properties:</span></span>

| <span data-ttu-id="ef729-107">Propriété</span><span class="sxs-lookup"><span data-stu-id="ef729-107">Property</span></span>      | <span data-ttu-id="ef729-108">Description</span><span class="sxs-lookup"><span data-stu-id="ef729-108">Description</span></span> |
| ------------- | ----------- |
| <span data-ttu-id="ef729-109">**Nom**</span><span class="sxs-lookup"><span data-stu-id="ef729-109">**Name**</span></span>      | <span data-ttu-id="ef729-110">Nom unique qui identifie la règle.</span><span class="sxs-lookup"><span data-stu-id="ef729-110">The unique name that identifies the rule.</span></span> |
| <span data-ttu-id="ef729-111">**Source**</span><span class="sxs-lookup"><span data-stu-id="ef729-111">**Source**</span></span>    | <span data-ttu-id="ef729-112">Origine du flux de données qui fait l’objet du traitement.</span><span class="sxs-lookup"><span data-stu-id="ef729-112">The origin of the data stream to be acted upon.</span></span> <span data-ttu-id="ef729-113">Par exemple, télémétrie des appareils.</span><span class="sxs-lookup"><span data-stu-id="ef729-113">For example, device telemetry.</span></span> |
| <span data-ttu-id="ef729-114">**Condition**</span><span class="sxs-lookup"><span data-stu-id="ef729-114">**Condition**</span></span> | <span data-ttu-id="ef729-115">Expression de requête de la règle d’acheminement exécutée sur les en-têtes et le corps du message et utilisée pour déterminer s’il existe une correspondance pour le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="ef729-115">The query expression for the routing rule that is run against the message's headers and body and used to determine whether it is a match for the endpoint.</span></span> <span data-ttu-id="ef729-116">Pour plus d’informations sur la construction d’une condition d’acheminement, consultez la [Référence : langage de requête pour jumeaux d’appareils et travaux][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="ef729-116">For more information about constructing a route condition, see the [Reference - query language for device twins and jobs][lnk-devguide-query-language].</span></span> |
| <span data-ttu-id="ef729-117">**Point de terminaison**</span><span class="sxs-lookup"><span data-stu-id="ef729-117">**Endpoint**</span></span>  | <span data-ttu-id="ef729-118">Nom du point de terminaison auquel IoT Hub envoie des messages qui correspondent à la condition.</span><span class="sxs-lookup"><span data-stu-id="ef729-118">The name of the endpoint where IoT Hub sends messages that match the condition.</span></span> <span data-ttu-id="ef729-119">Les points de terminaison doivent être dans la même région que l’IoT Hub, sinon des écritures inter-régions peuvent vous être facturées.</span><span class="sxs-lookup"><span data-stu-id="ef729-119">Endpoints should be in the same region as the IoT hub, otherwise you may be charged for cross-region writes.</span></span> |

<span data-ttu-id="ef729-120">Un seul message peut correspondre à la condition de plusieurs règles d’acheminement, auquel cas IoT Hub remet le message au point de terminaison associé à chaque règle ayant affiché une correspondance.</span><span class="sxs-lookup"><span data-stu-id="ef729-120">A single message may match the condition on multiple routing rules, in which case IoT Hub delivers the message to the endpoint associated with each matched rule.</span></span> <span data-ttu-id="ef729-121">Par ailleurs, IoT Hub déduplique automatiquement la remise des messages ; par conséquent, si un message correspond à plusieurs règles qui ont toutes la même destination, il n’est écrit qu’une seule fois dans cette destination.</span><span class="sxs-lookup"><span data-stu-id="ef729-121">IoT Hub also automatically deduplicates message delivery, so if a message matches multiple rules that all have the same destination, it is only written to that destination once.</span></span>

<span data-ttu-id="ef729-122">Un hub IoT a par défaut un [point de terminaison intégré][lnk-built-in].</span><span class="sxs-lookup"><span data-stu-id="ef729-122">An IoT hub has a default [built-in endpoint][lnk-built-in].</span></span> <span data-ttu-id="ef729-123">Vous pouvez créer des points de terminaison personnalisés pour y acheminer les messages en liant d’autres services de votre abonnement au hub.</span><span class="sxs-lookup"><span data-stu-id="ef729-123">You can create custom endpoints to route messages to by linking other services in your subscription to the hub.</span></span> <span data-ttu-id="ef729-124">IoT Hub prend actuellement en charge les points de terminaison personnalisés Event Hubs, les files d’attente Service Bus et les rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ef729-124">IoT Hub currently supports Event Hubs, Service Bus queues, and Service Bus topics as custom endpoints.</span></span>

> [!WARNING]
> <span data-ttu-id="ef729-125">Les files d’attente et rubriques Service Bus dont les options **Sessions** ou **Détection des doublons** sont activées ne sont pas prises en charge comme points de terminaison personnalisés.</span><span class="sxs-lookup"><span data-stu-id="ef729-125">Service Bus queues and topics with **Sessions** or **Duplicate Detection** enabled are not supported as custom endpoints.</span></span>

<span data-ttu-id="ef729-126">Pour plus d’informations sur la création de points de terminaison personnalisés dans IoT Hub, consultez la page [Points de terminaison IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="ef729-126">For more information about creating custom endpoints in IoT Hub, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="ef729-127">Pour plus d’informations sur la lecture à partir de points de terminaison personnalisés, consultez :</span><span class="sxs-lookup"><span data-stu-id="ef729-127">For more information about reading from custom endpoints, see:</span></span>

* <span data-ttu-id="ef729-128">Lecture à partir [d’Event Hubs][lnk-getstarted-eh].</span><span class="sxs-lookup"><span data-stu-id="ef729-128">Reading from [Event Hubs][lnk-getstarted-eh].</span></span>
* <span data-ttu-id="ef729-129">Lecture à partir de [files d’attente Service Bus][lnk-getstarted-queue].</span><span class="sxs-lookup"><span data-stu-id="ef729-129">Reading from [Service Bus queues][lnk-getstarted-queue].</span></span>
* <span data-ttu-id="ef729-130">Lecture à partir de [rubriques Service Bus][lnk-getstarted-topic].</span><span class="sxs-lookup"><span data-stu-id="ef729-130">Reading from [Service Bus topics][lnk-getstarted-topic].</span></span>

### <a name="next-steps"></a><span data-ttu-id="ef729-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef729-131">Next steps</span></span>

<span data-ttu-id="ef729-132">Pour plus d’informations sur les points de terminaison IoT Hub, consultez [Points de terminaison IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="ef729-132">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-devguide-endpoints].</span></span>

<span data-ttu-id="ef729-133">Pour plus d’informations sur le langage de requête que vous utilisez pour définir des règles de routage, consultez [Langage de requête d’IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-devguide-query-language].</span><span class="sxs-lookup"><span data-stu-id="ef729-133">For more information about the query language you use to define routing rules, see [IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query-language].</span></span>

<span data-ttu-id="ef729-134">Le didacticiel [Traiter les messages appareil-à-cloud IoT Hub en utilisant les itinéraires][lnk-d2c-tutorial] vous montre comment utiliser des règles de routage et des points de terminaison personnalisés.</span><span class="sxs-lookup"><span data-stu-id="ef729-134">The [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial shows you how to use routing rules and custom endpoints.</span></span>

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
