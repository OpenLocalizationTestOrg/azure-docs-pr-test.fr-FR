---
title: "Disponibilité et cohérence dans Azure Event Hubs | Microsoft Docs"
description: "Découvrez comment obtenir la quantité maximale de disponibilité et de cohérence avec Azure Event Hubs à l’aide de partitions."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 681a9d1636d547492f6f827461c6b2494b918778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="7f52a-103">Disponibilité et cohérence dans Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7f52a-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="7f52a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7f52a-104">Overview</span></span>
<span data-ttu-id="7f52a-105">Azure Event Hubs utilise un [modèle de partitionnement](event-hubs-features.md#partitions) pour améliorer la disponibilité et la parallélisation dans un concentrateur d’événements unique.</span><span class="sxs-lookup"><span data-stu-id="7f52a-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) to improve availability and parallelization within a single event hub.</span></span> <span data-ttu-id="7f52a-106">Par exemple, si un concentrateur d’événements a quatre partitions et que l’une de ces partitions est déplacée d’un serveur à l’autre dans une opération d’équilibrage de charge, vous pouvez quand même envoyer et recevoir à partir des trois autres partitions.</span><span class="sxs-lookup"><span data-stu-id="7f52a-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server to another in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="7f52a-107">En outre, avoir davantage de partitions vous permet d’avoir plus lecteurs pour traiter vos données simultanément, ce qui améliore le débit global.</span><span class="sxs-lookup"><span data-stu-id="7f52a-107">Additionally, having more partitions enables you to have more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="7f52a-108">Comprendre les implications en matière de partitionnement et de classement dans un système distribué est un aspect essentiel de la conception de la solution.</span><span class="sxs-lookup"><span data-stu-id="7f52a-108">Understanding the implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="7f52a-109">Pour expliquer le compromis entre classement et disponibilité, reportez-vous au [théorème CAP](https://en.wikipedia.org/wiki/CAP_theorem), également connu sous le nom de théorème de Brewer.</span><span class="sxs-lookup"><span data-stu-id="7f52a-109">To help explain the trade-off between ordering and availability, see the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="7f52a-110">Ce théorème discute le choix entre la cohérence, la disponibilité et la tolérance de la partition.</span><span class="sxs-lookup"><span data-stu-id="7f52a-110">This theorem discusses the choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="7f52a-111">Le théorème de Brewer définit la cohérence et la disponibilité de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="7f52a-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="7f52a-112">Tolérance de la partition : la capacité d’un système de traitement de données à continuer le traitement des données même en cas de défaillance d’une partition.</span><span class="sxs-lookup"><span data-stu-id="7f52a-112">Partition tolerance: the ability of a data processing system to continue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="7f52a-113">Disponibilité : un nœud sans échec renvoie une réponse raisonnable dans un délai raisonnable (sans erreurs ou expirations de délai).</span><span class="sxs-lookup"><span data-stu-id="7f52a-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="7f52a-114">Cohérence : une lecture renvoie toujours la dernière écriture pour un client donné.</span><span class="sxs-lookup"><span data-stu-id="7f52a-114">Consistency: a read is guaranteed to return the most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="7f52a-115">Tolérance de la partition</span><span class="sxs-lookup"><span data-stu-id="7f52a-115">Partition tolerance</span></span>
<span data-ttu-id="7f52a-116">Event Hubs repose sur un modèle de données partitionné.</span><span class="sxs-lookup"><span data-stu-id="7f52a-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="7f52a-117">Vous pouvez configurer le nombre de partitions dans votre concentrateur d’événements pendant l’installation, mais vous ne pouvez pas modifier cette valeur par la suite.</span><span class="sxs-lookup"><span data-stu-id="7f52a-117">You can configure the number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="7f52a-118">Étant donné que vous devez utiliser des partitions avec Event Hubs, vous devez prendre une décision concernant la disponibilité et la cohérence de votre application.</span><span class="sxs-lookup"><span data-stu-id="7f52a-118">Since you must use partitions with Event Hubs, you have to make a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="7f52a-119">Availability</span><span class="sxs-lookup"><span data-stu-id="7f52a-119">Availability</span></span>
<span data-ttu-id="7f52a-120">La méthode la plus simple pour se familiariser avec Event Hubs est d’utiliser le comportement par défaut.</span><span class="sxs-lookup"><span data-stu-id="7f52a-120">The simplest way to get started with Event Hubs is to use the default behavior.</span></span> <span data-ttu-id="7f52a-121">Si vous créez un `EventHubClient` et que vous utilisez la méthode `Send`, les événements sont automatiquement distribués entre les partitions de votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="7f52a-121">If you create a new `EventHubClient` object and use the `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="7f52a-122">Ce comportement offre le meilleur temps d’activité.</span><span class="sxs-lookup"><span data-stu-id="7f52a-122">This behavior allows for the greatest amount of up time.</span></span>

<span data-ttu-id="7f52a-123">Pour les cas d’utilisation qui exigent un temps d’activité maximum, ce modèle est conseillé.</span><span class="sxs-lookup"><span data-stu-id="7f52a-123">For use cases that require the maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="7f52a-124">Cohérence</span><span class="sxs-lookup"><span data-stu-id="7f52a-124">Consistency</span></span>
<span data-ttu-id="7f52a-125">Dans certains scénarios, l’ordre des événements peut être important.</span><span class="sxs-lookup"><span data-stu-id="7f52a-125">In some scenarios, the ordering of events can be important.</span></span> <span data-ttu-id="7f52a-126">Par exemple, vous souhaiterez peut-être que votre système principal traite une commande de mise à jour avant une commande de suppression.</span><span class="sxs-lookup"><span data-stu-id="7f52a-126">For example, you may want your back-end system to process an update command before a delete command.</span></span> <span data-ttu-id="7f52a-127">Dans ce cas, vous pouvez définir la clé de partition sur un événement, ou utiliser un objet `PartitionSender` pour envoyer uniquement les événements à une certaine partition.</span><span class="sxs-lookup"><span data-stu-id="7f52a-127">In this instance, you can either set the partition key on an event, or use a `PartitionSender` object to only send events to a certain partition.</span></span> <span data-ttu-id="7f52a-128">Cela garantit que ces événements sont lus dans l’ordre lorsqu’ils sont lus à partir de la partition.</span><span class="sxs-lookup"><span data-stu-id="7f52a-128">Doing so ensures that when these events are read from the partition, they are read in order.</span></span>

<span data-ttu-id="7f52a-129">Avec cette configuration, gardez à l’esprit que si la partition particulière à laquelle vous envoyez les événements n’est pas disponible, vous recevrez une réponse d’erreur.</span><span class="sxs-lookup"><span data-stu-id="7f52a-129">With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="7f52a-130">À titre de comparaison, si vous n’avez pas d’affinité avec une partition unique, le service Event Hubs envoie votre événement à la prochaine partition disponible.</span><span class="sxs-lookup"><span data-stu-id="7f52a-130">As a point of comparison, if you do not have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.</span></span>

<span data-ttu-id="7f52a-131">Pour garantir le classement tout en optimisant aussi le temps d’activité, vous pouvez regrouper les événements dans le cadre de votre application de traitement des événements.</span><span class="sxs-lookup"><span data-stu-id="7f52a-131">One possible solution to ensure ordering, while also maximizing up time, would be to aggregate events as part of your event processing application.</span></span> <span data-ttu-id="7f52a-132">Pour cela, le moyen le plus simple consiste à marquer votre événement avec une propriété de numéro de séquence personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7f52a-132">The easiest way to accomplish this is to stamp your event with a custom sequence number property.</span></span> <span data-ttu-id="7f52a-133">Le code suivant montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="7f52a-133">The following code shows an example:</span></span>

```csharp
// Get the latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="7f52a-134">L’exemple envoie votre événement à l’une des partitions disponibles dans votre concentrateur d’événements et définit le numéro de séquence correspondant à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="7f52a-134">This example sends your event to one of the available partitions in your event hub, and sets the corresponding sequence number from your application.</span></span> <span data-ttu-id="7f52a-135">Cette solution nécessite que l’état soit conservé par votre application de traitement, mais offre à vos expéditeurs un point de terminaison plus susceptible d’être disponible.</span><span class="sxs-lookup"><span data-stu-id="7f52a-135">This solution requires state to be kept by your processing application, but gives your senders an endpoint that is more likely to be available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f52a-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f52a-136">Next steps</span></span>
<span data-ttu-id="7f52a-137">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="7f52a-137">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="7f52a-138">Présentation du service Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7f52a-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="7f52a-139">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="7f52a-139">Create an event hub</span></span>](event-hubs-create.md)
