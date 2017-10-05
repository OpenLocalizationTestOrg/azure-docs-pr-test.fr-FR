---
title: "Ajout du déclencheur de périodicité dans des applications logiques | Microsoft Docs"
description: "Vue d’ensemble du déclencheur de périodicité et de son utilisation avec une application logique Azure."
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
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="455d6-103">Prise en main du déclencheur de périodicité</span><span class="sxs-lookup"><span data-stu-id="455d6-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="455d6-104">En utilisant le déclencheur de périodicité, vous pouvez créer des workflows puissants dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="455d6-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="455d6-105">Vous pouvez par exemple afficher :</span><span class="sxs-lookup"><span data-stu-id="455d6-105">For example, you can:</span></span>

* <span data-ttu-id="455d6-106">Planifier un workflow pour l’exécution quotidienne d’une procédure SQL stockée.</span><span class="sxs-lookup"><span data-stu-id="455d6-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="455d6-107">Envoyer par e-mail un résumé de tous les tweets de la semaine écoulée sur la base d’un hashtag spécifique.</span><span class="sxs-lookup"><span data-stu-id="455d6-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="455d6-108">Pour commencer à utiliser le déclencheur de périodicité dans une application logique, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="455d6-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="455d6-109">Utilisation d’un déclencheur de périodicité</span><span class="sxs-lookup"><span data-stu-id="455d6-109">Use a recurrence trigger</span></span>
<span data-ttu-id="455d6-110">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="455d6-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="455d6-111">[En savoir plus sur les déclencheurs](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="455d6-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="455d6-112">Voici un exemple de séquence de configuration d’un déclencheur de périodicité dans une application logique :</span><span class="sxs-lookup"><span data-stu-id="455d6-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="455d6-113">Ajoutez le déclencheur **Périodicité** en tant que première étape dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="455d6-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="455d6-114">Renseignez les paramètres pour l’intervalle de périodicité.</span><span class="sxs-lookup"><span data-stu-id="455d6-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="455d6-115">L’application logique est exécutée après l’écoulement de chaque intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="455d6-115">The logic app now starts a run after each interval of time.</span></span>

![Déclencheur HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="455d6-117">Détails du déclencheur</span><span class="sxs-lookup"><span data-stu-id="455d6-117">Trigger details</span></span>
<span data-ttu-id="455d6-118">Le déclencheur de périodicité a les propriétés suivantes qui peuvent être configurées.</span><span class="sxs-lookup"><span data-stu-id="455d6-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="455d6-119">Il déclenche une application logique après un intervalle de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="455d6-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="455d6-120">A * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="455d6-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="455d6-121">Nom complet</span><span class="sxs-lookup"><span data-stu-id="455d6-121">Display name</span></span> | <span data-ttu-id="455d6-122">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="455d6-122">Property name</span></span> | <span data-ttu-id="455d6-123">Description</span><span class="sxs-lookup"><span data-stu-id="455d6-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="455d6-124">Frequency (Fréquence)*</span><span class="sxs-lookup"><span data-stu-id="455d6-124">Frequency*</span></span> |<span data-ttu-id="455d6-125">frequency</span><span class="sxs-lookup"><span data-stu-id="455d6-125">frequency</span></span> |<span data-ttu-id="455d6-126">L’unité de temps : `Second`, `Minute`, `Hour`, `Day` ou `Year`.</span><span class="sxs-lookup"><span data-stu-id="455d6-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="455d6-127">Interval (Intervalle)*</span><span class="sxs-lookup"><span data-stu-id="455d6-127">Interval*</span></span> |<span data-ttu-id="455d6-128">interval</span><span class="sxs-lookup"><span data-stu-id="455d6-128">interval</span></span> |<span data-ttu-id="455d6-129">L'intervalle de la fréquence donnée pour la récurrence.</span><span class="sxs-lookup"><span data-stu-id="455d6-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="455d6-130">Time Zone (Fuseau horaire)</span><span class="sxs-lookup"><span data-stu-id="455d6-130">Time Zone</span></span> |<span data-ttu-id="455d6-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="455d6-131">timeZone</span></span> |<span data-ttu-id="455d6-132">Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire est utilisé.</span><span class="sxs-lookup"><span data-stu-id="455d6-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="455d6-133">Heure de début</span><span class="sxs-lookup"><span data-stu-id="455d6-133">Start time</span></span> |<span data-ttu-id="455d6-134">startTime</span><span class="sxs-lookup"><span data-stu-id="455d6-134">startTime</span></span> |<span data-ttu-id="455d6-135">L'heure de début au [format ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="455d6-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="455d6-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="455d6-136">Next steps</span></span>
<span data-ttu-id="455d6-137">Essayez maintenant la plateforme et [créez une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="455d6-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="455d6-138">Vous pouvez explorer les autres connecteurs disponibles dans les applications logiques en examinant notre [liste d’API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="455d6-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

