---
title: "un retard dans les applications de la logique d’aaaAdd | Documents Microsoft"
description: "Vue d’ensemble de hello délai et le délai-jusqu'à ce que les actions et comment toouse avec une application Azure logique."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="276bc-103">Prise en main hello délai et le délai-jusqu'à ce que les actions</span><span class="sxs-lookup"><span data-stu-id="276bc-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="276bc-104">À l’aide du délai de hello et « délai-jusqu'à ce que « actions, vous pouvez effectuer les scénarios de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="276bc-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="276bc-105">Vous pouvez par exemple afficher :</span><span class="sxs-lookup"><span data-stu-id="276bc-105">For example, you can:</span></span>

* <span data-ttu-id="276bc-106">Attendez un toosend jour ouvrable un état de mise à jour par e-mail.</span><span class="sxs-lookup"><span data-stu-id="276bc-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="276bc-107">Workflow de hello délai jusqu'à ce qu’un appel HTTP a toofinish de temps avant la reprise et de récupérer les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="276bc-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="276bc-108">tooget démarré à l’aide de retarder l’action hello dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="276bc-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="276bc-109">Utiliser des actions de retard hello</span><span class="sxs-lookup"><span data-stu-id="276bc-109">Use hello delay actions</span></span>
<span data-ttu-id="276bc-110">Une action est une opération est effectuée par le flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="276bc-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="276bc-111">[En savoir plus sur les actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="276bc-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="276bc-112">Voici un exemple de séquence de comment toouse un délai étape dans une application de logique :</span><span class="sxs-lookup"><span data-stu-id="276bc-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="276bc-113">Après l’ajout d’un déclencheur, cliquez sur **nouvelle étape** tooadd une action.</span><span class="sxs-lookup"><span data-stu-id="276bc-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="276bc-114">Recherchez **délai** toobring des actions de retard hello.</span><span class="sxs-lookup"><span data-stu-id="276bc-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="276bc-115">Dans cet exemple, nous sélectionnons **Retarder**.</span><span class="sxs-lookup"><span data-stu-id="276bc-115">In this example, we will select **Delay**.</span></span>
   
    ![Action Retarder](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="276bc-117">Effectuez l’une de retard de hello action propriétés tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="276bc-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![Configuration du retard](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="276bc-119">Cliquez sur **enregistrer** toopublish et activer l’application de la logique de hello.</span><span class="sxs-lookup"><span data-stu-id="276bc-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="276bc-120">Détails de l’action</span><span class="sxs-lookup"><span data-stu-id="276bc-120">Action details</span></span>
<span data-ttu-id="276bc-121">déclencheur de périodicité Hello a hello suivant des propriétés qui peuvent être configurées.</span><span class="sxs-lookup"><span data-stu-id="276bc-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="276bc-122">Action Retarder</span><span class="sxs-lookup"><span data-stu-id="276bc-122">Delay action</span></span>
<span data-ttu-id="276bc-123">Cette hello de retards action exécutée pour un intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="276bc-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="276bc-124">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="276bc-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="276bc-125">Nom complet</span><span class="sxs-lookup"><span data-stu-id="276bc-125">Display name</span></span> | <span data-ttu-id="276bc-126">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="276bc-126">Property name</span></span> | <span data-ttu-id="276bc-127">Description</span><span class="sxs-lookup"><span data-stu-id="276bc-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="276bc-128">Count*</span><span class="sxs-lookup"><span data-stu-id="276bc-128">Count*</span></span> |<span data-ttu-id="276bc-129">count</span><span class="sxs-lookup"><span data-stu-id="276bc-129">count</span></span> |<span data-ttu-id="276bc-130">nombre de Hello de toodelay d’unités de temps</span><span class="sxs-lookup"><span data-stu-id="276bc-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="276bc-131">Unit*</span><span class="sxs-lookup"><span data-stu-id="276bc-131">Unit*</span></span> |<span data-ttu-id="276bc-132">unité</span><span class="sxs-lookup"><span data-stu-id="276bc-132">unit</span></span> |<span data-ttu-id="276bc-133">unité de Hello de temps : `Second`, `Minute`, `Hour`, ou`Day`</span><span class="sxs-lookup"><span data-stu-id="276bc-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="276bc-134">Action Retarder jusqu'à</span><span class="sxs-lookup"><span data-stu-id="276bc-134">Delay-until action</span></span>
<span data-ttu-id="276bc-135">Cette action retarde hello exécuter jusqu'à une date/heure spécifiée.</span><span class="sxs-lookup"><span data-stu-id="276bc-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="276bc-136">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="276bc-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="276bc-137">Nom complet</span><span class="sxs-lookup"><span data-stu-id="276bc-137">Display name</span></span> | <span data-ttu-id="276bc-138">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="276bc-138">Property name</span></span> | <span data-ttu-id="276bc-139">Description</span><span class="sxs-lookup"><span data-stu-id="276bc-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="276bc-140">Year*</span><span class="sxs-lookup"><span data-stu-id="276bc-140">Year*</span></span> |<span data-ttu-id="276bc-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="276bc-141">timestamp</span></span> |<span data-ttu-id="276bc-142">Hello année toodelay jusqu'à (GMT)</span><span class="sxs-lookup"><span data-stu-id="276bc-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="276bc-143">Month*</span><span class="sxs-lookup"><span data-stu-id="276bc-143">Month*</span></span> |<span data-ttu-id="276bc-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="276bc-144">timestamp</span></span> |<span data-ttu-id="276bc-145">Hello mois toodelay jusqu'à (GMT)</span><span class="sxs-lookup"><span data-stu-id="276bc-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="276bc-146">Day*</span><span class="sxs-lookup"><span data-stu-id="276bc-146">Day*</span></span> |<span data-ttu-id="276bc-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="276bc-147">timestamp</span></span> |<span data-ttu-id="276bc-148">Hello jour toodelay jusqu'à (GMT)</span><span class="sxs-lookup"><span data-stu-id="276bc-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="276bc-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="276bc-149">Next steps</span></span>
<span data-ttu-id="276bc-150">Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="276bc-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="276bc-151">Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="276bc-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

