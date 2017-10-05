---
title: Gestion des erreurs et des exceptions - Azure Logic Apps | Microsoft Docs
description: "Modèles de gestion des erreurs et des exceptions dans Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="fbc7a-103">Gérer les erreurs et les exceptions dans Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="fbc7a-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="fbc7a-104">Azure Logic Apps propose un ensemble complet d’outils et de modèles afin de garantir la résistance et la fiabilité de vos intégrations contre les défaillances.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-104">Azure Logic Apps provides rich tools and patterns to help you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="fbc7a-105">Toute architecture d’intégration nécessite que les temps d’arrêt et les problèmes soient gérés de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-105">Any integration architecture poses the challenge of making sure to appropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="fbc7a-106">Logic Apps optimise la gestion des erreurs, en vous offrant les outils dont vous avez besoin pour gérer les exceptions et les erreurs qui se produisent dans vos flux de travail.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-106">Logic Apps makes handling errors a first-class experience, giving you the tools you need to act on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="fbc7a-107">Stratégies de nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="fbc7a-107">Retry policies</span></span>

<span data-ttu-id="fbc7a-108">Le type de gestion des erreurs et des exceptions le plus simple consiste à utiliser une stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-108">A retry policy is the most basic type of exception and error handling.</span></span> <span data-ttu-id="fbc7a-109">Cette stratégie définit si l’action doit faire l’objet d’une nouvelle tentative en cas d’expiration ou d’échec de la demande initiale (toute demande ayant entraîné une réponse 429 ou 5xx).</span><span class="sxs-lookup"><span data-stu-id="fbc7a-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether the action should retry.</span></span> <span data-ttu-id="fbc7a-110">Par défaut, toutes les actions font l’objet de 4 tentatives supplémentaires sur des intervalles de 20 secondes.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="fbc7a-111">Par conséquent, si la première demande reçoit une réponse `500 Internal Server Error`, le moteur de flux de travail s’interrompt pendant 20 secondes, puis tente à nouveau d’exécuter la demande.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-111">So if the first request receives a `500 Internal Server Error` response, the workflow engine pauses for 20 seconds, and attempts the request again.</span></span> <span data-ttu-id="fbc7a-112">Si à l’issue de toutes les tentatives, la réponse renvoie toujours une exception ou un échec, le flux de travail continue et marque l’état de l’action comme `Failed`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-112">If after all retries, the response is still an exception or failure, the workflow continues and marks the action status as `Failed`.</span></span>

<span data-ttu-id="fbc7a-113">Vous pouvez configurer des stratégies de nouvelle tentative dans les **entrées** d’une action en particulier.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-113">You can configure retry policies in the **inputs** for a particular action.</span></span> <span data-ttu-id="fbc7a-114">Une stratégie de nouvelle tentative peut par exemple être configurée pour effectuer jusqu’à 4 tentatives avec des intervalles d’1 heure.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-114">For example, you can configure a retry policy to try as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="fbc7a-115">Pour plus d’informations sur les propriétés d’entrée, voir [Actions et déclencheurs de flux de travail][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="fbc7a-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="fbc7a-116">Si vous voulez que votre action HTTP effectue 4 tentatives et attende 10 minutes entre chacune d’entre elles, vous devez utiliser la définition suivante :</span><span class="sxs-lookup"><span data-stu-id="fbc7a-116">If you wanted your HTTP action to retry 4 times and wait 10 minutes between each attempt, you would use the following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="fbc7a-117">Pour plus d’informations sur la syntaxe prise en charge, consultez la [section relative aux stratégies de nouvelle tentative sous Actions et déclencheurs de flux de travail][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="fbc7a-117">For more information on supported syntax, see the [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-the-runafter-property"></a><span data-ttu-id="fbc7a-118">Identification des échecs avec la propriété RunAfter</span><span class="sxs-lookup"><span data-stu-id="fbc7a-118">Catch failures with the RunAfter property</span></span>

<span data-ttu-id="fbc7a-119">Chaque action d’application logique déclare quelles actions doivent se terminer avant de démarrer une autre action, hiérarchisant ainsi les étapes de votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-119">Each logic app action declares which actions must finish before the action starts, like ordering the steps in your workflow.</span></span> <span data-ttu-id="fbc7a-120">Ce classement est connu sous le nom de propriété `runAfter` dans la définition de l’action.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-120">In the action definition, this ordering is known as the `runAfter` property.</span></span> <span data-ttu-id="fbc7a-121">Cette propriété est un objet qui décrit les actions et les états d’action qui exécutent l’action.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-121">This property is an object that describes which actions and action statuses execute the action.</span></span> <span data-ttu-id="fbc7a-122">Par défaut, toutes les actions ajoutées par le biais du Concepteur d’application logique sont définies avec la propriété `runAfter` par rapport à l’étape précédente, si celle-ci était `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-122">By default, all actions added through the Logic App Designer are set to `runAfter` the previous step if the previous step `Succeeded`.</span></span> <span data-ttu-id="fbc7a-123">Toutefois, vous pouvez personnaliser cette valeur pour déclencher des actions lorsque les actions précédentes sont `Failed`, `Skipped` ou un ensemble de valeurs possible.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-123">However, you can customize this value to fire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="fbc7a-124">Si vous souhaitez ajouter un élément à une rubrique Service Bus désignée suite à l’échec d’une action spécifique `Insert_Row`, vous pouvez utiliser la configuration `runAfter` suivante :</span><span class="sxs-lookup"><span data-stu-id="fbc7a-124">If you wanted to add an item to a designated Service Bus topic after a specific action `Insert_Row` fails, you could use the following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="fbc7a-125">Notez que la propriété `runAfter` est définie pour se déclencher si l’action `Insert_Row` est `Failed`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-125">Notice the `runAfter` property is set to fire if the `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="fbc7a-126">Pour exécuter l’action si l’état de l’action est `Succeeded`, `Failed` ou `Skipped`, utilisez cette syntaxe :</span><span class="sxs-lookup"><span data-stu-id="fbc7a-126">To run the action if the action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="fbc7a-127">Les actions qui s’exécutent suite à l’échec d’une action précédente et qui sont correctement exécutées seront marquées comme `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="fbc7a-128">Ce comportement signifie que si vous avez correctement intercepté tous les échecs dans un flux de travail, l’exécution elle-même est marquée comme `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-128">This behavior means that if you successfully catch all failures in a workflow, the run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-to-evaluate-actions"></a><span data-ttu-id="fbc7a-129">Étendues et résultats permettant d’évaluer les actions</span><span class="sxs-lookup"><span data-stu-id="fbc7a-129">Scopes and results to evaluate actions</span></span>

<span data-ttu-id="fbc7a-130">De la même manière que vous pouvez exécuter des actions individuelles, vous pouvez également regrouper des actions au sein d’une [étendue](../logic-apps/logic-apps-loops-and-scopes.md) qui agit comme un regroupement logique d’actions.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-130">Similar to how you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="fbc7a-131">Les étendues sont utiles pour organiser vos actions d’application logique et pour effectuer des évaluations d’agrégation sur l’état d’une étendue.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on the status of a scope.</span></span> <span data-ttu-id="fbc7a-132">L’étendue elle-même se voit attribuer un état une fois toutes les actions de l’étendue effectuées.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-132">The scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="fbc7a-133">L’état de l’étendue est déterminé avec les mêmes critères que pour une exécution.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-133">The scope status is determined with the same criteria as a run.</span></span> <span data-ttu-id="fbc7a-134">Si la dernière action dans une branche de l’exécution est `Failed` ou `Aborted`, l’état est `Failed`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-134">If the final action in an execution branch is `Failed` or `Aborted`, the status is `Failed`.</span></span>

<span data-ttu-id="fbc7a-135">Vous pouvez utiliser la propriété `runAfter` sur une étendue qui a été marquée comme `Failed` pour déclencher des actions spécifiques en raison d’échecs survenus dans l’étendue.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-135">To fire specific actions for any failures that happened within the scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="fbc7a-136">L’exécution suite à l’échec d’une étendue vous permet de créer une seule action pour intercepter des échecs, si *des* actions figurent dans l’étendue.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-136">If *any* actions in the scope fail, running after a scope fails lets you create a single action to catch failures.</span></span>

### <a name="getting-the-context-of-failures-with-results"></a><span data-ttu-id="fbc7a-137">Obtention du contexte des échecs avec les résultats</span><span class="sxs-lookup"><span data-stu-id="fbc7a-137">Getting the context of failures with results</span></span>

<span data-ttu-id="fbc7a-138">Bien que l’interception des échecs d’une étendue soit très utile, vous aurez peut-être également besoin du contexte pour identifier précisément les actions qui ont échoué, ainsi que les codes d’erreur ou d’état renvoyés.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-138">Although catching failures from a scope is useful, you might also want context to help you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="fbc7a-139">La fonction de flux de travail `@result()` fournit le contexte dans le résultat de toutes les actions au sein d’une étendue.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-139">The `@result()` workflow function provides context about the result of all actions in a scope.</span></span>

<span data-ttu-id="fbc7a-140">`@result()` prend un paramètre unique, le nom de l’étendue, et renvoie un tableau de tous les résultats d’action dans cette étendue.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-140">`@result()` takes a single parameter, scope name, and returns an array of all the action results from within that scope.</span></span> <span data-ttu-id="fbc7a-141">Ces objets d’action incluent les mêmes attributs que l’objet `@actions()` , y compris l’heure de début de l’action, l’heure de fin de l’action, l’état de l’action, les entrées de l’action, les ID de corrélation d’action, ainsi que ses résultats.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-141">These action objects include the same attributes as the `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="fbc7a-142">Vous pouvez facilement associer une fonction `@result()` avec une propriété `runAfter` pour envoyer le contexte de toutes les actions qui ont échoué dans une étendue.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-142">To send context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="fbc7a-143">Pour exécuter une action *pour chaque* action dans une étendue marquée comme `Failed`, filtrez les résultats sur les actions ayant échoué, et associez `@result()` avec une action **[Filtrer le tableau](../connectors/connectors-native-query.md)** et une boucle **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-143">To execute an action *for each* action in a scope that `Failed`, filter the array of results to actions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="fbc7a-144">Vous pouvez prendre le tableau des résultats filtrés et effectuer une action pour chaque échec à l’aide de la boucle **ForEach** .</span><span class="sxs-lookup"><span data-stu-id="fbc7a-144">You can take the filtered result array and perform an action for each failure using the **ForEach** loop.</span></span> <span data-ttu-id="fbc7a-145">Cet exemple, suivi d’une explication détaillée, envoie une demande HTTP POST avec le corps de réponse de toutes les actions qui ont échoué dans l’étendue `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with the response body of any actions that failed within the scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="fbc7a-146">Voici la procédure détaillée pour décrire ce qui se produit :</span><span class="sxs-lookup"><span data-stu-id="fbc7a-146">Here's a detailed walkthrough to describe what happens:</span></span>

1. <span data-ttu-id="fbc7a-147">Pour obtenir le résultat de toutes les actions au sein de `My_Scope`, l’action **Filtrer le tableau** permet de filtrer `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-147">To get the result of all actions within `My_Scope`, the **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="fbc7a-148">La condition de l’action **Filtrer le tableau** est tout élément `@result()` dont l’état est égal à `Failed`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-148">The condition for **Filter Array** is any `@result()` item that has status equal to `Failed`.</span></span> <span data-ttu-id="fbc7a-149">Cette condition filtre le tableau de tous les résultats d’action de `My_Scope` selon un tableau contenant uniquement les résultats d’action ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-149">This condition filters the array with all action results from `My_Scope` to an array with only failed action results.</span></span>

3. <span data-ttu-id="fbc7a-150">Exécution d’une action **For Each** sur les résultats du **tableau filtré**.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-150">Perform a **For Each** action on the **Filtered Array** outputs.</span></span> <span data-ttu-id="fbc7a-151">Cette étape exécute une action *pour chaque* résultat d’action ayant échoué filtré précédemment.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="fbc7a-152">Si une action unique dans l’étendue a échoué, les actions de `foreach` s’exécutent une seule fois.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-152">If a single action in the scope failed, the actions in the `foreach` run only once.</span></span> 
    <span data-ttu-id="fbc7a-153">De nombreuses actions ayant échoué peuvent provoquer une action par échec.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="fbc7a-154">Envoi d’une requête HTTP POST sur le corps de réponse de l’élément `foreach`, ou `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-154">Send an HTTP POST on the `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="fbc7a-155">La forme de l’élément `@result()` est identique à la forme `@actions()` et peut être analysée de la même façon.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-155">The `@result()` item shape is the same as the `@actions()` shape, and can be parsed the same way.</span></span>

5. <span data-ttu-id="fbc7a-156">Deux en-têtes personnalisés avec le nom de l’action qui a échoué `@item()['name']` sont également inclus, ainsi que l’ID de suivi du client d’exécution qui a échoué `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-156">Include two custom headers with the failed action name `@item()['name']` and the failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="fbc7a-157">Pour référence, voici un exemple d’un seul élément `@result()`, montrant le `name`, le `body`, et les propriétés `clientTrackingId` analysés dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-157">For reference, here's an example of a single `@result()` item, showing the `name`, `body`, and `clientTrackingId` properties that are parsed in the previous example.</span></span> <span data-ttu-id="fbc7a-158">En dehors de `foreach`, `@result()` retourne un tableau de ces objets.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="fbc7a-159">Vous pouvez utiliser les expressions ci-dessus pour exécuter différents modèles de gestion des exceptions.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-159">To perform different exception handling patterns, you can use the expressions shown previously.</span></span> <span data-ttu-id="fbc7a-160">Vous pouvez choisir d’exécuter une seule action de gestion en dehors de l’étendue qui accepte l’intégralité du tableau filtré d’échecs et de supprimer `foreach`.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-160">You might choose to execute a single exception handling action outside the scope that accepts the entire filtered array of failures, and remove the `foreach`.</span></span> <span data-ttu-id="fbc7a-161">Vous pouvez également inclure d’autres propriétés utiles à partir de la réponse `@result()` obtenue précédemment.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-161">You can also include other useful properties from the `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="fbc7a-162">Azure Diagnostics et télémétrie</span><span class="sxs-lookup"><span data-stu-id="fbc7a-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="fbc7a-163">Les précédents modèles sont très utiles pour gérer les erreurs et les exceptions d’une exécution, mais vous pouvez également identifier les erreurs et y répondre indépendamment de l’exécution elle-même.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-163">The previous patterns are great way to handle errors and exceptions within a run, but you can also identify and respond to errors independent of the run itself.</span></span> 
<span data-ttu-id="fbc7a-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) fournit un moyen simple d’envoyer tous les événements de flux de travail (y compris tous les états d’exécution et d’action) à un compte Azure Storage ou un concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way to send all workflow events (including all run and action statuses) to an Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="fbc7a-165">Vous pouvez surveiller les journaux et les mesures ou les publier dans n’importe quel outil de surveillance de votre choix pour évaluer les états d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-165">To evaluate run statuses, you can monitor the logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="fbc7a-166">Vous avez également la possibilité de transmettre tous les événements via le concentrateur d’événements Azure dans [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="fbc7a-166">One potential option is to stream all the events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="fbc7a-167">Dans Stream Analytics, vous pouvez écrire des requêtes actives sans aucune anomalie, des moyennes ou des échecs dans les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from the diagnostic logs.</span></span> <span data-ttu-id="fbc7a-168">Stream Analytics peut facilement exporter ses résultats vers d’autres sources de données, telles que les files d’attente, les rubriques, SQL, Azure Cosmos DB et Power BI.</span><span class="sxs-lookup"><span data-stu-id="fbc7a-168">Stream Analytics can easily output to other data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbc7a-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fbc7a-169">Next Steps</span></span>

* [<span data-ttu-id="fbc7a-170">Voir comment un client conçoit la gestion des erreurs avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="fbc7a-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="fbc7a-171">Consultez d’autres exemples et scénarios Logic Apps</span><span class="sxs-lookup"><span data-stu-id="fbc7a-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="fbc7a-172">Découvrez comment créer des déploiements automatisés pour des applications logiques</span><span class="sxs-lookup"><span data-stu-id="fbc7a-172">Learn how to create automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="fbc7a-173">Créer et déployer des applications logiques avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fbc7a-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
