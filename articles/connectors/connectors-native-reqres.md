---
title: "actions de demande et de réponse aaaUse | Documents Microsoft"
description: "Vue d’ensemble de déclencheur de demande et de réponse hello et d’action dans une application Azure logique"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="ab0f2-103">Prise en main des composants de demande et de réponse hello</span><span class="sxs-lookup"><span data-stu-id="ab0f2-103">Get started with hello request and response components</span></span>
<span data-ttu-id="ab0f2-104">À hello demande et réponse des composants d’une application logique, vous pouvez répondre en temps réel tooevents.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="ab0f2-105">Vous pouvez par exemple afficher :</span><span class="sxs-lookup"><span data-stu-id="ab0f2-105">For example, you can:</span></span>

* <span data-ttu-id="ab0f2-106">Répondre demande HTTP de tooan avec des données à partir d’une base de données locale via une application logique.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="ab0f2-107">déclencher une application logique à partir d’un événement webhook externe ;</span><span class="sxs-lookup"><span data-stu-id="ab0f2-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="ab0f2-108">appeler une application logique avec une action de requête et de réponse depuis une autre application logique.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="ab0f2-109">tooget démarré à l’aide des actions de demande et de réponse hello dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ab0f2-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="ab0f2-110">Utilisez hello déclencheur de la requête HTTP</span><span class="sxs-lookup"><span data-stu-id="ab0f2-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="ab0f2-111">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail qui est défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="ab0f2-112">[En savoir plus sur les déclencheurs](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab0f2-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="ab0f2-113">Voici un exemple de séquence de la demande de tooset un HTTP Bonjour Concepteur de logique d’application.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="ab0f2-114">Ajouter le déclencheur de hello **demande - HTTP lors de la demande est reçue** dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="ab0f2-115">Vous pouvez éventuellement fournir un schéma JSON (à l’aide d’un outil tel que [JSONSchema.net](http://jsonschema.net)) pour le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="ab0f2-116">Cela permet des jetons de concepteur toogenerate hello pour les propriétés dans la demande HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="ab0f2-117">Ajouter une autre action afin que vous puissiez enregistrer application logique de hello.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="ab0f2-118">Après avoir enregistré l’application logique de hello, vous pouvez obtenir des URL de demande hello HTTP à partir de la carte de demande hello.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="ab0f2-119">Une requête HTTP POST (vous pouvez utiliser un outil tel que [Postman](https://www.getpostman.com/)) déclencheurs d’URL toohello hello application logique.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="ab0f2-120">Si vous ne définissez pas une action de réponse, une `202 ACCEPTED` réponse est retournée immédiatement toohello appelant.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="ab0f2-121">Vous pouvez utiliser hello réponse action toocustomize une réponse.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![Déclencheur de réponse](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="ab0f2-123">Utilisez hello action de réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="ab0f2-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="ab0f2-124">Hello action de réponse HTTP est valide uniquement lorsque vous l’utilisez dans un workflow qui est déclenché par une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="ab0f2-125">Si vous ne définissez pas une action de réponse, une `202 ACCEPTED` réponse est retournée immédiatement toohello appelant.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="ab0f2-126">Vous pouvez ajouter une action de réponse à une étape dans le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="ab0f2-127">Hello logique application conserve uniquement les demande entrante hello ouvert pendant une minute pour une réponse.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="ab0f2-128">Après une minute, si aucune réponse n’a été envoyé à partir de flux de travail hello (et une action de réponse existe dans la définition de hello), un `504 GATEWAY TIMEOUT` est retourné à l’appelant de toohello.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="ab0f2-129">Voici comment tooadd une action de réponse HTTP :</span><span class="sxs-lookup"><span data-stu-id="ab0f2-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="ab0f2-130">Sélectionnez hello **nouvelle étape** bouton.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="ab0f2-131">Choisissez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="ab0f2-132">Dans la zone de recherche action hello, tapez **réponse** hello de toolist action de réponse.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Sélectionnez l’action de réponse hello](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="ab0f2-134">Ajoutez tous les paramètres qui sont requis pour le message de réponse HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![Action de réponse hello terminée](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="ab0f2-136">Cliquez sur le coin supérieur gauche de hello de toosave de barre d’outils hello et votre logique application est à la fois enregistrer et publier (activer).</span><span class="sxs-lookup"><span data-stu-id="ab0f2-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="ab0f2-137">Déclencheur de requête</span><span class="sxs-lookup"><span data-stu-id="ab0f2-137">Request trigger</span></span>
<span data-ttu-id="ab0f2-138">Voici les détails de hello pour déclencheur hello qui prend en charge par ce connecteur.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="ab0f2-139">Il existe un seul déclencheur de requête.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-139">There is a single request trigger.</span></span>

| <span data-ttu-id="ab0f2-140">Déclencheur</span><span class="sxs-lookup"><span data-stu-id="ab0f2-140">Trigger</span></span> | <span data-ttu-id="ab0f2-141">Description</span><span class="sxs-lookup"><span data-stu-id="ab0f2-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab0f2-142">Demande</span><span class="sxs-lookup"><span data-stu-id="ab0f2-142">Request</span></span> |<span data-ttu-id="ab0f2-143">Se produit quand une requête HTTP est reçue</span><span class="sxs-lookup"><span data-stu-id="ab0f2-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="ab0f2-144">Action de réponse</span><span class="sxs-lookup"><span data-stu-id="ab0f2-144">Response action</span></span>
<span data-ttu-id="ab0f2-145">Voici les détails de hello pour action hello qui prend en charge par ce connecteur.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="ab0f2-146">Il existe une action de réponse unique qui est utilisable uniquement lorsqu’elle est accompagnée d’un déclencheur de requête.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="ab0f2-147">Action</span><span class="sxs-lookup"><span data-stu-id="ab0f2-147">Action</span></span> | <span data-ttu-id="ab0f2-148">Description</span><span class="sxs-lookup"><span data-stu-id="ab0f2-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab0f2-149">Réponse</span><span class="sxs-lookup"><span data-stu-id="ab0f2-149">Response</span></span> |<span data-ttu-id="ab0f2-150">Retourne qu'une réponse toohello mis en corrélation de demande HTTP</span><span class="sxs-lookup"><span data-stu-id="ab0f2-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="ab0f2-151">Détail des déclencheurs et des actions</span><span class="sxs-lookup"><span data-stu-id="ab0f2-151">Trigger and action details</span></span>
<span data-ttu-id="ab0f2-152">Hello tableaux suivants décrire les champs d’entrée de hello pour hello trigger et action et hello détails de sortie correspondants.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="ab0f2-153">Déclencheur de requête</span><span class="sxs-lookup"><span data-stu-id="ab0f2-153">Request trigger</span></span>
<span data-ttu-id="ab0f2-154">Hello Voici un champ d’entrée pour le déclencheur hello à partir d’une demande HTTP entrante.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="ab0f2-155">Nom complet</span><span class="sxs-lookup"><span data-stu-id="ab0f2-155">Display name</span></span> | <span data-ttu-id="ab0f2-156">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="ab0f2-156">Property name</span></span> | <span data-ttu-id="ab0f2-157">Description</span><span class="sxs-lookup"><span data-stu-id="ab0f2-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab0f2-158">JSON Schema (Schéma JSON)</span><span class="sxs-lookup"><span data-stu-id="ab0f2-158">JSON Schema</span></span> |<span data-ttu-id="ab0f2-159">schema</span><span class="sxs-lookup"><span data-stu-id="ab0f2-159">schema</span></span> |<span data-ttu-id="ab0f2-160">schéma JSON Hello hello HTTP du corps de demande</span><span class="sxs-lookup"><span data-stu-id="ab0f2-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="ab0f2-161">**Détails des résultats**</span><span class="sxs-lookup"><span data-stu-id="ab0f2-161">**Output details**</span></span>

<span data-ttu-id="ab0f2-162">Hello Voici les détails de sortie pour la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="ab0f2-163">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="ab0f2-163">Property name</span></span> | <span data-ttu-id="ab0f2-164">Type de données</span><span class="sxs-lookup"><span data-stu-id="ab0f2-164">Data type</span></span> | <span data-ttu-id="ab0f2-165">Description</span><span class="sxs-lookup"><span data-stu-id="ab0f2-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab0f2-166">headers</span><span class="sxs-lookup"><span data-stu-id="ab0f2-166">Headers</span></span> |<span data-ttu-id="ab0f2-167">objet</span><span class="sxs-lookup"><span data-stu-id="ab0f2-167">object</span></span> |<span data-ttu-id="ab0f2-168">En-têtes de requête</span><span class="sxs-lookup"><span data-stu-id="ab0f2-168">Request headers</span></span> |
| <span data-ttu-id="ab0f2-169">Corps</span><span class="sxs-lookup"><span data-stu-id="ab0f2-169">Body</span></span> |<span data-ttu-id="ab0f2-170">objet</span><span class="sxs-lookup"><span data-stu-id="ab0f2-170">object</span></span> |<span data-ttu-id="ab0f2-171">Objet Requête</span><span class="sxs-lookup"><span data-stu-id="ab0f2-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="ab0f2-172">Action de réponse</span><span class="sxs-lookup"><span data-stu-id="ab0f2-172">Response action</span></span>
<span data-ttu-id="ab0f2-173">Hello Voici les champs d’entrée de hello action de réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="ab0f2-174">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="ab0f2-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="ab0f2-175">Nom complet</span><span class="sxs-lookup"><span data-stu-id="ab0f2-175">Display name</span></span> | <span data-ttu-id="ab0f2-176">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="ab0f2-176">Property name</span></span> | <span data-ttu-id="ab0f2-177">Description</span><span class="sxs-lookup"><span data-stu-id="ab0f2-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab0f2-178">Status Code (Code d’état)*</span><span class="sxs-lookup"><span data-stu-id="ab0f2-178">Status Code*</span></span> |<span data-ttu-id="ab0f2-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="ab0f2-179">statusCode</span></span> |<span data-ttu-id="ab0f2-180">Hello, code d’état HTTP</span><span class="sxs-lookup"><span data-stu-id="ab0f2-180">hello HTTP status code</span></span> |
| <span data-ttu-id="ab0f2-181">headers</span><span class="sxs-lookup"><span data-stu-id="ab0f2-181">Headers</span></span> |<span data-ttu-id="ab0f2-182">headers</span><span class="sxs-lookup"><span data-stu-id="ab0f2-182">headers</span></span> |<span data-ttu-id="ab0f2-183">Un objet JSON de n’importe quel tooinclude d’en-têtes de réponse</span><span class="sxs-lookup"><span data-stu-id="ab0f2-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="ab0f2-184">Corps</span><span class="sxs-lookup"><span data-stu-id="ab0f2-184">Body</span></span> |<span data-ttu-id="ab0f2-185">body</span><span class="sxs-lookup"><span data-stu-id="ab0f2-185">body</span></span> |<span data-ttu-id="ab0f2-186">corps de réponse Hello</span><span class="sxs-lookup"><span data-stu-id="ab0f2-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ab0f2-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab0f2-187">Next steps</span></span>
<span data-ttu-id="ab0f2-188">Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ab0f2-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ab0f2-189">Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ab0f2-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

