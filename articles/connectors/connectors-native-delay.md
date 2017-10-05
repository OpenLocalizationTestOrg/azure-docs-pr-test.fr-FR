---
title: "Ajout d’un retard dans des applications logiques | Microsoft Docs"
description: "Vue d’ensemble des actions Retarder et Retarder jusqu’à et de leur utilisation avec une application Azure logique."
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
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="49325-103">Prise en main des actions Retarder et Retarder jusqu’à</span><span class="sxs-lookup"><span data-stu-id="49325-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="49325-104">Les actions Retarder et Retarder jusqu’à vous permettent d’exécuter des scénarios de workflow.</span><span class="sxs-lookup"><span data-stu-id="49325-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="49325-105">Vous pouvez par exemple afficher :</span><span class="sxs-lookup"><span data-stu-id="49325-105">For example, you can:</span></span>

* <span data-ttu-id="49325-106">Attendre un jour de semaine pour envoyer une mise à jour d’état par e-mail.</span><span class="sxs-lookup"><span data-stu-id="49325-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="49325-107">Retarder le workflow jusqu’à ce qu’un appel HTTP dispose d’assez de temps avant la reprise et la récupération du résultat.</span><span class="sxs-lookup"><span data-stu-id="49325-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="49325-108">Pour commencer à utiliser l’action Retarder dans une application logique, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="49325-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="49325-109">Utilisation d’actions Retarder</span><span class="sxs-lookup"><span data-stu-id="49325-109">Use the delay actions</span></span>
<span data-ttu-id="49325-110">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="49325-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="49325-111">[En savoir plus sur les actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49325-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="49325-112">Voici un exemple de séquence d’utilisation d’une étape de retard dans une application logique :</span><span class="sxs-lookup"><span data-stu-id="49325-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="49325-113">Après avoir ajouté un déclencheur, cliquez sur **Nouvelle étape** pour ajouter une action.</span><span class="sxs-lookup"><span data-stu-id="49325-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="49325-114">Recherchez **Retarder** pour afficher les actions Retarder.</span><span class="sxs-lookup"><span data-stu-id="49325-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="49325-115">Dans cet exemple, nous sélectionnons **Retarder**.</span><span class="sxs-lookup"><span data-stu-id="49325-115">In this example, we will select **Delay**.</span></span>
   
    ![Action Retarder](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="49325-117">Exécutez toutes les propriétés de l’action pour configurer le retard.</span><span class="sxs-lookup"><span data-stu-id="49325-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![Configuration du retard](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="49325-119">Cliquez sur **Enregistrer** pour publier et activer l’application logique.</span><span class="sxs-lookup"><span data-stu-id="49325-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="49325-120">Détails de l’action</span><span class="sxs-lookup"><span data-stu-id="49325-120">Action details</span></span>
<span data-ttu-id="49325-121">Le déclencheur de périodicité a les propriétés suivantes qui peuvent être configurées.</span><span class="sxs-lookup"><span data-stu-id="49325-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="49325-122">Action Retarder</span><span class="sxs-lookup"><span data-stu-id="49325-122">Delay action</span></span>
<span data-ttu-id="49325-123">Cette action retarde l’exécution pour un intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="49325-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="49325-124">A * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="49325-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="49325-125">Nom complet</span><span class="sxs-lookup"><span data-stu-id="49325-125">Display name</span></span> | <span data-ttu-id="49325-126">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="49325-126">Property name</span></span> | <span data-ttu-id="49325-127">Description</span><span class="sxs-lookup"><span data-stu-id="49325-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49325-128">Count*</span><span class="sxs-lookup"><span data-stu-id="49325-128">Count*</span></span> |<span data-ttu-id="49325-129">count</span><span class="sxs-lookup"><span data-stu-id="49325-129">count</span></span> |<span data-ttu-id="49325-130">Le nombre d’unités à retarder</span><span class="sxs-lookup"><span data-stu-id="49325-130">The number of time units to delay</span></span> |
| <span data-ttu-id="49325-131">Unit*</span><span class="sxs-lookup"><span data-stu-id="49325-131">Unit*</span></span> |<span data-ttu-id="49325-132">unité</span><span class="sxs-lookup"><span data-stu-id="49325-132">unit</span></span> |<span data-ttu-id="49325-133">L’unité de temps : `Second`, `Minute`, `Hour` ou `Day`</span><span class="sxs-lookup"><span data-stu-id="49325-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="49325-134">Action Retarder jusqu'à</span><span class="sxs-lookup"><span data-stu-id="49325-134">Delay-until action</span></span>
<span data-ttu-id="49325-135">Cette action retarde l’exécution jusqu’à une date/heure spécifique.</span><span class="sxs-lookup"><span data-stu-id="49325-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="49325-136">A * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="49325-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="49325-137">Nom complet</span><span class="sxs-lookup"><span data-stu-id="49325-137">Display name</span></span> | <span data-ttu-id="49325-138">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="49325-138">Property name</span></span> | <span data-ttu-id="49325-139">Description</span><span class="sxs-lookup"><span data-stu-id="49325-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49325-140">Year*</span><span class="sxs-lookup"><span data-stu-id="49325-140">Year*</span></span> |<span data-ttu-id="49325-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="49325-141">timestamp</span></span> |<span data-ttu-id="49325-142">L’année jusqu’à laquelle le retard doit être défini (GMT)</span><span class="sxs-lookup"><span data-stu-id="49325-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="49325-143">Month*</span><span class="sxs-lookup"><span data-stu-id="49325-143">Month*</span></span> |<span data-ttu-id="49325-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="49325-144">timestamp</span></span> |<span data-ttu-id="49325-145">Le mois jusqu’auquel le retard doit être défini (GMT)</span><span class="sxs-lookup"><span data-stu-id="49325-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="49325-146">Day*</span><span class="sxs-lookup"><span data-stu-id="49325-146">Day*</span></span> |<span data-ttu-id="49325-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="49325-147">timestamp</span></span> |<span data-ttu-id="49325-148">Le jour jusqu’auquel le retard doit être défini (GMT)</span><span class="sxs-lookup"><span data-stu-id="49325-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="49325-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49325-149">Next steps</span></span>
<span data-ttu-id="49325-150">Essayez maintenant la plateforme et [créez une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="49325-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="49325-151">Vous pouvez explorer les autres connecteurs disponibles dans les applications logiques en examinant notre [liste d’API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="49325-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

