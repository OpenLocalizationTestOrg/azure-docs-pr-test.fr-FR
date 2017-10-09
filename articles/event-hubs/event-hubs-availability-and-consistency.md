---
title: "aaaAvailability et la cohérence dans Azure Event Hubs | Documents Microsoft"
description: "Comment tooprovide hello maximum de disponibilité et la cohérence avec les concentrateurs d’événements Azure à l’aide de partitions."
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
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="1e262-103">Disponibilité et cohérence dans Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1e262-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="1e262-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1e262-104">Overview</span></span>
<span data-ttu-id="1e262-105">Azure Event Hubs utilise un [modèle de partitionnement](event-hubs-features.md#partitions) tooimprove disponibilité et la parallélisation au sein d’un concentrateur d’événements unique.</span><span class="sxs-lookup"><span data-stu-id="1e262-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="1e262-106">Par exemple, si un concentrateur d’événements a quatre partitions, et l’une de ces partitions est déplacée à partir de tooanother d’un serveur dans une opération d’équilibrage de charge, vous pouvez toujours envoyer et recevoir des trois autres partitions.</span><span class="sxs-lookup"><span data-stu-id="1e262-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="1e262-107">En outre, avoir davantage de partitions permet toohave lecteurs simultanés plus le traitement de vos données, améliorer le débit d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="1e262-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="1e262-108">Comprendre les implications en matière de hello de partitionnement et l’ordre dans un système distribué est un aspect essentiel de la conception de la solution.</span><span class="sxs-lookup"><span data-stu-id="1e262-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="1e262-109">toohelp expliquent les compromis de hello entre la commande et la disponibilité, consultez hello [théorème de CAP](https://en.wikipedia.org/wiki/CAP_theorem), également connue sous le théorème de Brewer.</span><span class="sxs-lookup"><span data-stu-id="1e262-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="1e262-110">Cette théorème de traite des choix hello entre la cohérence, la disponibilité et la tolérance de partition.</span><span class="sxs-lookup"><span data-stu-id="1e262-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="1e262-111">Le théorème de Brewer définit la cohérence et la disponibilité de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="1e262-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="1e262-112">La tolérance de panne de partition : hello la capacité d’un toocontinue de système de traitement des données du traitement des données même en cas d’une défaillance de la partition.</span><span class="sxs-lookup"><span data-stu-id="1e262-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="1e262-113">Disponibilité : un nœud sans échec renvoie une réponse raisonnable dans un délai raisonnable (sans erreurs ou expirations de délai).</span><span class="sxs-lookup"><span data-stu-id="1e262-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="1e262-114">Cohérence : une lecture est garantie tooreturn hello dernière inscription pour un client donné.</span><span class="sxs-lookup"><span data-stu-id="1e262-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="1e262-115">Tolérance de la partition</span><span class="sxs-lookup"><span data-stu-id="1e262-115">Partition tolerance</span></span>
<span data-ttu-id="1e262-116">Event Hubs repose sur un modèle de données partitionné.</span><span class="sxs-lookup"><span data-stu-id="1e262-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="1e262-117">Vous pouvez configurer le nombre hello de partitions dans votre concentrateur d’événements pendant l’installation, mais vous ne pouvez pas modifier cette valeur ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1e262-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="1e262-118">Étant donné que vous devez utiliser des partitions avec des concentrateurs d’événements, vous devez toomake une décision sur la disponibilité et la cohérence de votre application.</span><span class="sxs-lookup"><span data-stu-id="1e262-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="1e262-119">Disponibilité</span><span class="sxs-lookup"><span data-stu-id="1e262-119">Availability</span></span>
<span data-ttu-id="1e262-120">Hello tooget de façon la plus simple en main de concentrateurs d’événements est le comportement par défaut de hello toouse.</span><span class="sxs-lookup"><span data-stu-id="1e262-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="1e262-121">Si vous créez un nouveau `EventHubClient` de l’objet et utilisez hello `Send` (méthode), les événements sont automatiquement distribués entre des partitions dans votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="1e262-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="1e262-122">Ce comportement permet hello plus grande partie du temps d’activité.</span><span class="sxs-lookup"><span data-stu-id="1e262-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="1e262-123">Pour les cas d’usage qui nécessitent maximum hello le temps, ce modèle est préféré.</span><span class="sxs-lookup"><span data-stu-id="1e262-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="1e262-124">Cohérence</span><span class="sxs-lookup"><span data-stu-id="1e262-124">Consistency</span></span>
<span data-ttu-id="1e262-125">Dans certains scénarios, hello classement d’événements peut être important.</span><span class="sxs-lookup"><span data-stu-id="1e262-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="1e262-126">Par exemple, vous souhaiterez peut-être votre tooprocess système back-end une commande de mise à jour avant qu’une commande delete.</span><span class="sxs-lookup"><span data-stu-id="1e262-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="1e262-127">Dans ce cas, vous pouvez définir la clé de partition hello sur un événement, ou utiliser un `PartitionSender` objet tooonly envoyer les événements tooa certaine partition.</span><span class="sxs-lookup"><span data-stu-id="1e262-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="1e262-128">Cela garantit que lorsque ces événements sont lus à partir de la partition de hello, ils sont lus dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="1e262-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="1e262-129">Avec cette configuration, gardez à l’esprit que si toowhich de partition particulière hello que vous envoyez n’est pas disponible, vous recevrez une réponse d’erreur.</span><span class="sxs-lookup"><span data-stu-id="1e262-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="1e262-130">En tant que point de comparaison, si vous ne disposez pas d’une partition unique tooa d’affinité, hello service Event Hubs envoie votre partition disponible suivante événement toohello.</span><span class="sxs-lookup"><span data-stu-id="1e262-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="1e262-131">Une solution possible tooensure classement, tout en optimisant également le temps, serait tooaggregate événements dans le cadre de votre application de traitement des événements.</span><span class="sxs-lookup"><span data-stu-id="1e262-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="1e262-132">Hello tooaccomplish de façon plus simple de cela est toostamp votre événement avec une propriété de numéro de séquence personnalisée.</span><span class="sxs-lookup"><span data-stu-id="1e262-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="1e262-133">Hello suivant de code illustre un exemple :</span><span class="sxs-lookup"><span data-stu-id="1e262-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="1e262-134">Cet exemple envoie votre tooone d’événement des partitions disponibles de hello dans votre concentrateur d’événements et définit le numéro de séquence hello correspondant à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="1e262-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="1e262-135">Cette solution requiert toobe état conservé par votre application de traitement, mais il donne à votre expéditeurs un point de terminaison qui est plus probable toobe disponible.</span><span class="sxs-lookup"><span data-stu-id="1e262-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e262-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e262-136">Next steps</span></span>
<span data-ttu-id="1e262-137">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="1e262-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="1e262-138">Présentation du service Event Hubs</span><span class="sxs-lookup"><span data-stu-id="1e262-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="1e262-139">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="1e262-139">Create an event hub</span></span>](event-hubs-create.md)
