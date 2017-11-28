---
title: "nouvelle tentative et la remise de grille d’événement aaaAzure"
description: "Décrit comment Azure Event Grid distribue des événements et gère les messages qui n’ont pas été distribués."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="05942-103">Distribution et nouvelle tentative de distribution de messages avec Azure Grid</span><span class="sxs-lookup"><span data-stu-id="05942-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="05942-104">Cet article décrit comment Azure Event Grid gère les événements en l’absence d’accusé de réception d’une distribution.</span><span class="sxs-lookup"><span data-stu-id="05942-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="05942-105">Event Grid assure une distribution fiable.</span><span class="sxs-lookup"><span data-stu-id="05942-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="05942-106">Il distribue chaque message au moins une fois pour chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="05942-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="05942-107">Les événements sont immédiatement envoyés webhook toohello inscrit de chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="05942-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="05942-108">Si un webhook ne confirme pas la réception d’un événement pendant 60 secondes de la remise hello première tentative, grille d’événement tentatives de remise d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="05942-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="05942-109">État de distribution du message</span><span class="sxs-lookup"><span data-stu-id="05942-109">Message delivery status</span></span>

<span data-ttu-id="05942-110">Grille d’événement utilise la réception de tooacknowledge de codes de réponse HTTP d’événements.</span><span class="sxs-lookup"><span data-stu-id="05942-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="05942-111">Codes de réussite</span><span class="sxs-lookup"><span data-stu-id="05942-111">Success codes</span></span>

<span data-ttu-id="05942-112">Hello des codes de réponse HTTP suivants indiquent qu’un événement a été remis tooyour webhook.</span><span class="sxs-lookup"><span data-stu-id="05942-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="05942-113">Event Grid considère que la distribution est effectuée.</span><span class="sxs-lookup"><span data-stu-id="05942-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="05942-114">200 OK</span><span class="sxs-lookup"><span data-stu-id="05942-114">200 OK</span></span>
- <span data-ttu-id="05942-115">202 Accepté</span><span class="sxs-lookup"><span data-stu-id="05942-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="05942-116">Codes d’échec</span><span class="sxs-lookup"><span data-stu-id="05942-116">Failure codes</span></span>

<span data-ttu-id="05942-117">Hello suivant des codes de réponse HTTP indique l’échec de la tentative de remise d’un événement.</span><span class="sxs-lookup"><span data-stu-id="05942-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="05942-118">Grille d’événement événements de hello toosend recommence.</span><span class="sxs-lookup"><span data-stu-id="05942-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="05942-119">400 Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="05942-119">400 Bad Request</span></span>
- <span data-ttu-id="05942-120">401 Non autorisé</span><span class="sxs-lookup"><span data-stu-id="05942-120">401 Unauthorized</span></span>
- <span data-ttu-id="05942-121">404 Introuvable</span><span class="sxs-lookup"><span data-stu-id="05942-121">404 Not Found</span></span>
- <span data-ttu-id="05942-122">408 Délai d’expiration de la demande</span><span class="sxs-lookup"><span data-stu-id="05942-122">408 Request timeout</span></span>
- <span data-ttu-id="05942-123">414 URI trop long</span><span class="sxs-lookup"><span data-stu-id="05942-123">414 URI Too Long</span></span>
- <span data-ttu-id="05942-124">500 Erreur interne du serveur</span><span class="sxs-lookup"><span data-stu-id="05942-124">500 Internal Server Error</span></span>
- <span data-ttu-id="05942-125">503 Service indisponible</span><span class="sxs-lookup"><span data-stu-id="05942-125">503 Service Unavailable</span></span>
- <span data-ttu-id="05942-126">504 Dépassement du délai de la passerelle</span><span class="sxs-lookup"><span data-stu-id="05942-126">504 Gateway Timeout</span></span>

<span data-ttu-id="05942-127">Tout autre code de réponse ou manque de réponse indique un échec.</span><span class="sxs-lookup"><span data-stu-id="05942-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="05942-128">Event Grid effectue une nouvelle tentative de distribution.</span><span class="sxs-lookup"><span data-stu-id="05942-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="05942-129">Intervalles avant nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="05942-129">Retry intervals</span></span>

<span data-ttu-id="05942-130">Event Grid utilise une stratégie de nouvelle tentative d’interruption exponentielle pour la distribution des événements.</span><span class="sxs-lookup"><span data-stu-id="05942-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="05942-131">Si votre webhook ne répond pas, ou retourne un code d’échec, grille d’événement tentatives de remise sur hello suivant planification :</span><span class="sxs-lookup"><span data-stu-id="05942-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="05942-132">10 secondes</span><span class="sxs-lookup"><span data-stu-id="05942-132">10 seconds</span></span>
2. <span data-ttu-id="05942-133">30 secondes</span><span class="sxs-lookup"><span data-stu-id="05942-133">30 seconds</span></span>
3. <span data-ttu-id="05942-134">1 minute</span><span class="sxs-lookup"><span data-stu-id="05942-134">1 minute</span></span>
4. <span data-ttu-id="05942-135">5 minutes</span><span class="sxs-lookup"><span data-stu-id="05942-135">5 minutes</span></span>
5. <span data-ttu-id="05942-136">10 minutes</span><span class="sxs-lookup"><span data-stu-id="05942-136">10 minutes</span></span>
6. <span data-ttu-id="05942-137">30 minutes</span><span class="sxs-lookup"><span data-stu-id="05942-137">30 minutes</span></span>
7. <span data-ttu-id="05942-138">1 heure</span><span class="sxs-lookup"><span data-stu-id="05942-138">1 hour</span></span>

<span data-ttu-id="05942-139">Grille d’événement ajoute une intervalles tooall randomisation petit.</span><span class="sxs-lookup"><span data-stu-id="05942-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="05942-140">Durée des nouvelles tentatives</span><span class="sxs-lookup"><span data-stu-id="05942-140">Retry duration</span></span>

<span data-ttu-id="05942-141">Version d’évaluation hello grille d’événement Azure expire tous les événements qui ne sont pas remis dans les deux heures.</span><span class="sxs-lookup"><span data-stu-id="05942-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="05942-142">Avant la disponibilité générale, cette heure sera accrue too24 heures.</span><span class="sxs-lookup"><span data-stu-id="05942-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="05942-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05942-143">Next steps</span></span>

* <span data-ttu-id="05942-144">Pour une introduction tooEvent grille, consultez [sur la grille d’événement](overview.md).</span><span class="sxs-lookup"><span data-stu-id="05942-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="05942-145">tooquickly mise en route à l’aide de la grille d’événement, consultez [créer et itinéraire des événements personnalisés avec la grille d’événement Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="05942-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
