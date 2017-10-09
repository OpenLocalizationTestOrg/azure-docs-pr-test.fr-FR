---
title: "déclencheur de périodicité aaaAdd hello dans les applications logique | Documents Microsoft"
description: "Vue d’ensemble du déclencheur de périodicité hello et comment toouse avec une application Azure logique."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="5b6db-103">Prise en main déclencheur de périodicité hello</span><span class="sxs-lookup"><span data-stu-id="5b6db-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="5b6db-104">À l’aide de déclencheur de périodicité hello, vous pouvez créer puissants flux de travail dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="5b6db-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="5b6db-105">Vous pouvez par exemple afficher :</span><span class="sxs-lookup"><span data-stu-id="5b6db-105">For example, you can:</span></span>

* <span data-ttu-id="5b6db-106">Planifier un toorun de flux de travail une procédure stockée SQL tous les jours.</span><span class="sxs-lookup"><span data-stu-id="5b6db-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="5b6db-107">Envoyer par courrier électronique un résumé de tous les tweet dans hello sur une certaine #sqlhelp la semaine dernière.</span><span class="sxs-lookup"><span data-stu-id="5b6db-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="5b6db-108">tooget démarré à l’aide de déclencheur de périodicité hello dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5b6db-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="5b6db-109">Utilisation d’un déclencheur de périodicité</span><span class="sxs-lookup"><span data-stu-id="5b6db-109">Use a recurrence trigger</span></span>
<span data-ttu-id="5b6db-110">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail qui est défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="5b6db-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="5b6db-111">[En savoir plus sur les déclencheurs](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b6db-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="5b6db-112">Voici un exemple de séquence de comment déclencher des tooset d’une périodicité dans une application de logique :</span><span class="sxs-lookup"><span data-stu-id="5b6db-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="5b6db-113">Ajouter hello **périodicité** déclencheur en tant que première étape de hello dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="5b6db-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="5b6db-114">Renseignez les paramètres hello hello intervalle de périodicité.</span><span class="sxs-lookup"><span data-stu-id="5b6db-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="5b6db-115">application de la logique de Hello commence désormais une exécution après chaque intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="5b6db-115">hello logic app now starts a run after each interval of time.</span></span>

![Déclencheur HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="5b6db-117">Détails du déclencheur</span><span class="sxs-lookup"><span data-stu-id="5b6db-117">Trigger details</span></span>
<span data-ttu-id="5b6db-118">déclencheur de périodicité Hello a hello propriétés que vous pouvez configurer suivantes.</span><span class="sxs-lookup"><span data-stu-id="5b6db-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="5b6db-119">Il déclenche une application logique après un intervalle de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="5b6db-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="5b6db-120">A * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="5b6db-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="5b6db-121">Nom complet</span><span class="sxs-lookup"><span data-stu-id="5b6db-121">Display name</span></span> | <span data-ttu-id="5b6db-122">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="5b6db-122">Property name</span></span> | <span data-ttu-id="5b6db-123">Description</span><span class="sxs-lookup"><span data-stu-id="5b6db-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b6db-124">Frequency (Fréquence)*</span><span class="sxs-lookup"><span data-stu-id="5b6db-124">Frequency*</span></span> |<span data-ttu-id="5b6db-125">frequency</span><span class="sxs-lookup"><span data-stu-id="5b6db-125">frequency</span></span> |<span data-ttu-id="5b6db-126">unité de Hello de temps : `Second`, `Minute`, `Hour`, `Day`, ou `Year`.</span><span class="sxs-lookup"><span data-stu-id="5b6db-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="5b6db-127">Interval (Intervalle)*</span><span class="sxs-lookup"><span data-stu-id="5b6db-127">Interval*</span></span> |<span data-ttu-id="5b6db-128">interval</span><span class="sxs-lookup"><span data-stu-id="5b6db-128">interval</span></span> |<span data-ttu-id="5b6db-129">intervalle de salutation Hello attribué à la fréquence de récurrence de hello.</span><span class="sxs-lookup"><span data-stu-id="5b6db-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="5b6db-130">Time Zone (Fuseau horaire)</span><span class="sxs-lookup"><span data-stu-id="5b6db-130">Time Zone</span></span> |<span data-ttu-id="5b6db-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="5b6db-131">timeZone</span></span> |<span data-ttu-id="5b6db-132">Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire est utilisé.</span><span class="sxs-lookup"><span data-stu-id="5b6db-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="5b6db-133">Heure de début</span><span class="sxs-lookup"><span data-stu-id="5b6db-133">Start time</span></span> |<span data-ttu-id="5b6db-134">startTime</span><span class="sxs-lookup"><span data-stu-id="5b6db-134">startTime</span></span> |<span data-ttu-id="5b6db-135">heure de début Hello [format ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="5b6db-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="5b6db-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b6db-136">Next steps</span></span>
<span data-ttu-id="5b6db-137">Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5b6db-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5b6db-138">Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5b6db-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

