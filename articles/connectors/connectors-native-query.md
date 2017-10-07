---
title: "action de requête aaaAdd hello dans les applications logique | Documents Microsoft"
description: "Vue d’ensemble de l’action de requête hello pour effectuer des actions comme tableau de filtre."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="f564e-103">Prise en main avec l’action de requête hello</span><span class="sxs-lookup"><span data-stu-id="f564e-103">Get started with hello query action</span></span>
<span data-ttu-id="f564e-104">En utilisant l’action de requête de hello, vous pouvez utiliser des flux de travail de lots et de tableaux tooaccomplish à :</span><span class="sxs-lookup"><span data-stu-id="f564e-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="f564e-105">Créer une tâche pour tous les enregistrements à priorité élevée à partir d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="f564e-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="f564e-106">Enregistrer toutes les pièces jointes PDF pour les messages électroniques dans l’objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f564e-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="f564e-107">tooget démarré à l’aide d’action de requête hello dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f564e-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="f564e-108">Utilisez l’action de requête hello</span><span class="sxs-lookup"><span data-stu-id="f564e-108">Use hello query action</span></span>
<span data-ttu-id="f564e-109">Une action est une opération est effectuée par le flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="f564e-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="f564e-110">[En savoir plus sur les actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f564e-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="f564e-111">action de requête Hello a actuellement une opération appelée tableau de filtre hello, qui est exposé dans le Concepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="f564e-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="f564e-112">Cela vous permet de tooquery un tableau et retourner un jeu de résultats filtrés.</span><span class="sxs-lookup"><span data-stu-id="f564e-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="f564e-113">Voici comment vous pouvez l’ajouter dans une application logique :</span><span class="sxs-lookup"><span data-stu-id="f564e-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="f564e-114">Sélectionnez hello **nouvelle étape** bouton.</span><span class="sxs-lookup"><span data-stu-id="f564e-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="f564e-115">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="f564e-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="f564e-116">Dans la zone de recherche action hello, tapez **filtre** hello de toolist **tableau de filtre** action.</span><span class="sxs-lookup"><span data-stu-id="f564e-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Sélectionnez l’action de requête hello](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="f564e-118">Sélectionnez un tableau toofilter.</span><span class="sxs-lookup"><span data-stu-id="f564e-118">Select an array toofilter.</span></span> <span data-ttu-id="f564e-119">(hello capture d’écran suivante montre hello tableau de résultats de la recherche Twitter.)</span><span class="sxs-lookup"><span data-stu-id="f564e-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="f564e-120">Créer une condition tooevaluate sur chaque élément.</span><span class="sxs-lookup"><span data-stu-id="f564e-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="f564e-121">(hello suivant capture d’écran de filtres tweet d’utilisateurs disposant de plus de 100 barreaux.)</span><span class="sxs-lookup"><span data-stu-id="f564e-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Action de requête hello terminée](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="f564e-123">action de Hello produira un nouveau tableau qui contient uniquement les résultats répondant aux exigences de filtre hello.</span><span class="sxs-lookup"><span data-stu-id="f564e-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="f564e-124">Cliquez sur le coin supérieur gauche de hello de toosave de barre d’outils hello et votre logique application est à la fois enregistrer et publier (activer).</span><span class="sxs-lookup"><span data-stu-id="f564e-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="f564e-125">Action de requête</span><span class="sxs-lookup"><span data-stu-id="f564e-125">Query action</span></span>
<span data-ttu-id="f564e-126">Voici les détails de hello pour action hello qui prend en charge par ce connecteur.</span><span class="sxs-lookup"><span data-stu-id="f564e-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="f564e-127">connecteur de Hello possède une seule action possible.</span><span class="sxs-lookup"><span data-stu-id="f564e-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="f564e-128">Action</span><span class="sxs-lookup"><span data-stu-id="f564e-128">Action</span></span> | <span data-ttu-id="f564e-129">Description</span><span class="sxs-lookup"><span data-stu-id="f564e-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f564e-130">Filtrer le tableau</span><span class="sxs-lookup"><span data-stu-id="f564e-130">Filter array</span></span> |<span data-ttu-id="f564e-131">Évalue une condition pour chaque élément dans un tableau et retourne les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="f564e-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="f564e-132">Détails de l’action</span><span class="sxs-lookup"><span data-stu-id="f564e-132">Action details</span></span>
<span data-ttu-id="f564e-133">action de requête Hello est fourni avec une seule action possible.</span><span class="sxs-lookup"><span data-stu-id="f564e-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="f564e-134">Hello tableaux suivants décrivent hello requis et les champs d’entrée facultatifs pour action de hello et détails sortie correspondants hello qui sont associés à l’aide d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="f564e-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="f564e-135">Filtrer le tableau</span><span class="sxs-lookup"><span data-stu-id="f564e-135">Filter array</span></span>
<span data-ttu-id="f564e-136">Hello Voici les champs d’entrée pour l’action hello, qui effectue une requête de sortie HTTP.</span><span class="sxs-lookup"><span data-stu-id="f564e-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="f564e-137">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="f564e-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="f564e-138">Nom complet</span><span class="sxs-lookup"><span data-stu-id="f564e-138">Display name</span></span> | <span data-ttu-id="f564e-139">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="f564e-139">Property name</span></span> | <span data-ttu-id="f564e-140">Description</span><span class="sxs-lookup"><span data-stu-id="f564e-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f564e-141">De*</span><span class="sxs-lookup"><span data-stu-id="f564e-141">From*</span></span> |<span data-ttu-id="f564e-142">from</span><span class="sxs-lookup"><span data-stu-id="f564e-142">from</span></span> |<span data-ttu-id="f564e-143">Hello tableau toofilter</span><span class="sxs-lookup"><span data-stu-id="f564e-143">hello array toofilter</span></span> |
| <span data-ttu-id="f564e-144">Condition*</span><span class="sxs-lookup"><span data-stu-id="f564e-144">Condition*</span></span> |<span data-ttu-id="f564e-145">où</span><span class="sxs-lookup"><span data-stu-id="f564e-145">where</span></span> |<span data-ttu-id="f564e-146">Hello tooevaluate condition pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="f564e-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="f564e-147">Détails des résultats</span><span class="sxs-lookup"><span data-stu-id="f564e-147">Output details</span></span>
<span data-ttu-id="f564e-148">Hello Voici les détails de sortie de réponse HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="f564e-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="f564e-149">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="f564e-149">Property name</span></span> | <span data-ttu-id="f564e-150">Type de données</span><span class="sxs-lookup"><span data-stu-id="f564e-150">Data type</span></span> | <span data-ttu-id="f564e-151">Description</span><span class="sxs-lookup"><span data-stu-id="f564e-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f564e-152">Tableau filtré</span><span class="sxs-lookup"><span data-stu-id="f564e-152">Filtered array</span></span> |<span data-ttu-id="f564e-153">array</span><span class="sxs-lookup"><span data-stu-id="f564e-153">array</span></span> |<span data-ttu-id="f564e-154">Tableau contenant un objet pour chaque résultat filtré</span><span class="sxs-lookup"><span data-stu-id="f564e-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f564e-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f564e-155">Next steps</span></span>
<span data-ttu-id="f564e-156">Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f564e-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="f564e-157">Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f564e-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

