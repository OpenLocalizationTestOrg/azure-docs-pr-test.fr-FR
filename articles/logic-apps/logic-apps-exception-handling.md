---
title: aaaError & exceptions - Azure Logic Apps | Documents Microsoft
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
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="affb6-103">Gérer les erreurs et les exceptions dans Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="affb6-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="affb6-104">Azure Logic Apps fournit des outils et modèles toohelp vous vérifiez que votre intégrations sont solide et fiable contre les défaillances.</span><span class="sxs-lookup"><span data-stu-id="affb6-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="affb6-105">Architecture d’intégration pose problème hello de fabrication des temps d’arrêt tooappropriately que handle ou des problèmes à partir de systèmes dépendants.</span><span class="sxs-lookup"><span data-stu-id="affb6-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="affb6-106">Logique d’applications facilite la gestion des erreurs une expérience de première classe, ce qui vous donne hello outils tooact sur les erreurs et exceptions dans vos workflows.</span><span class="sxs-lookup"><span data-stu-id="affb6-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="affb6-107">Stratégies de nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="affb6-107">Retry policies</span></span>

<span data-ttu-id="affb6-108">Stratégie de nouvelle tentative est de type de base de hello d’exception et la gestion des erreurs.</span><span class="sxs-lookup"><span data-stu-id="affb6-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="affb6-109">Si une demande initiale a expiré ou a échoué (toute demande qui entraîne un 429 ou réponse 5xx), cette stratégie définit si l’action de hello doit réessayer.</span><span class="sxs-lookup"><span data-stu-id="affb6-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="affb6-110">Par défaut, toutes les actions font l’objet de 4 tentatives supplémentaires sur des intervalles de 20 secondes.</span><span class="sxs-lookup"><span data-stu-id="affb6-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="affb6-111">Par conséquent, si la première demande de hello reçoit un `500 Internal Server Error` réponse, le moteur de flux de travail hello s’interrompt pendant 20 secondes et tentatives hello demande à nouveau.</span><span class="sxs-lookup"><span data-stu-id="affb6-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="affb6-112">Si après toutes les nouvelles tentatives, hello réponse est toujours une exception ou une défaillance, le flux de travail de hello continue et marques hello l’état de l’action en tant que `Failed`.</span><span class="sxs-lookup"><span data-stu-id="affb6-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="affb6-113">Vous pouvez configurer des stratégies de nouvelle tentative dans hello **entrées** pour une action particulière.</span><span class="sxs-lookup"><span data-stu-id="affb6-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="affb6-114">Par exemple, vous pouvez configurer un tootry de stratégie de nouvelle tentative jusqu'à 4 fois sur des intervalles de 1 heure.</span><span class="sxs-lookup"><span data-stu-id="affb6-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="affb6-115">Pour plus d’informations sur les propriétés d’entrée, voir [Actions et déclencheurs de flux de travail][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="affb6-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="affb6-116">Si vous souhaitiez votre tooretry d’action HTTP 4 fois et que vous attendez 10 minutes entre chaque tentative, vous utiliseriez hello définition :</span><span class="sxs-lookup"><span data-stu-id="affb6-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

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

<span data-ttu-id="affb6-117">Pour plus d’informations sur la syntaxe prise en charge, consultez hello [section stratégie de nouvelle tentative dans les Actions de flux de travail et les déclencheurs][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="affb6-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="affb6-118">Intercepter des échecs avec hello RunAfter propriété</span><span class="sxs-lookup"><span data-stu-id="affb6-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="affb6-119">Chaque action d’application logique déclare les actions que doivent se terminer avant le début d’action hello, telles que l’ordre des étapes de hello dans votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="affb6-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="affb6-120">Dans la définition d’action hello, ce classement est connu comme hello `runAfter` propriété.</span><span class="sxs-lookup"><span data-stu-id="affb6-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="affb6-121">Cette propriété est un objet qui décrit les actions et les États de l’action exécutent l’action de hello.</span><span class="sxs-lookup"><span data-stu-id="affb6-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="affb6-122">Par défaut, toutes les actions sont ajoutées via hello Concepteur de logique d’application sont définies trop`runAfter` hello précédemment si hello étape précédente `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="affb6-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="affb6-123">Toutefois, vous pouvez personnaliser cette actions toofire la valeur lorsque les actions précédentes ont `Failed`, `Skipped`, ou un ensemble possible de ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="affb6-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="affb6-124">Si vous souhaitiez tooadd un tooa élément désigné rubrique Service Bus après une action spécifique `Insert_Row` échoue, vous pouvez utiliser hello suivant `runAfter` configuration :</span><span class="sxs-lookup"><span data-stu-id="affb6-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

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

<span data-ttu-id="affb6-125">Hello d’avis `runAfter` propriété a la valeur toofire si hello `Insert_Row` action est `Failed`.</span><span class="sxs-lookup"><span data-stu-id="affb6-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="affb6-126">action de hello toorun si l’état de l’action hello est `Succeeded`, `Failed`, ou `Skipped`, utilisez la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="affb6-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="affb6-127">Les actions qui s’exécutent suite à l’échec d’une action précédente et qui sont correctement exécutées seront marquées comme `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="affb6-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="affb6-128">Cela signifie que si vous avec succès toutes les défaillances dans un flux de travail, hello exécuter lui-même est marqué comme `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="affb6-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="affb6-129">Actions de tooevaluate étendues et les résultats</span><span class="sxs-lookup"><span data-stu-id="affb6-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="affb6-130">Toohow similaires que vous pouvez exécuter après des actions individuelles, vous pouvez également regrouper actions à l’intérieur d’un [étendue](../logic-apps/logic-apps-loops-and-scopes.md), qui agissent comme un regroupement logique des actions.</span><span class="sxs-lookup"><span data-stu-id="affb6-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="affb6-131">Les étendues sont utiles pour organiser des actions de votre logique d’application et pour effectuer des évaluations d’agrégation sur état hello d’une étendue.</span><span class="sxs-lookup"><span data-stu-id="affb6-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="affb6-132">étendue Hello lui-même reçoit un état une fois toutes les actions dans une portée ont terminé.</span><span class="sxs-lookup"><span data-stu-id="affb6-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="affb6-133">état de l’étendue Hello est déterminé par hello mêmes critères comme une série de tests.</span><span class="sxs-lookup"><span data-stu-id="affb6-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="affb6-134">Si la dernière action de hello dans une branche de l’exécution est `Failed` ou `Aborted`, l’état hello est `Failed`.</span><span class="sxs-lookup"><span data-stu-id="affb6-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="affb6-135">toofire des actions spécifiques pour les erreurs qui se sont produits au sein de la portée de hello, vous pouvez utiliser `runAfter` avec une étendue qui est marqué comme `Failed`.</span><span class="sxs-lookup"><span data-stu-id="affb6-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="affb6-136">Si *tout* actions dans la portée de hello échouent, en cours d’exécution après l’échec d’une étendue vous permet de vous créer un toocatch action unique échecs.</span><span class="sxs-lookup"><span data-stu-id="affb6-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="affb6-137">Lors de l’obtention de contexte hello d’échecs de résultats</span><span class="sxs-lookup"><span data-stu-id="affb6-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="affb6-138">Bien qu’il est utile d’intercepter les défaillances d’une étendue, vous pouvez également vous toohelp de contexte que vous comprenez exactement quelles actions a échoué, et les erreurs ou les codes d’état retournés.</span><span class="sxs-lookup"><span data-stu-id="affb6-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="affb6-139">Hello `@result()` fonction de workflow fournit le contexte relatif résultat hello de toutes les actions dans une étendue.</span><span class="sxs-lookup"><span data-stu-id="affb6-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="affb6-140">`@result()`prend un seul paramètre, le nom de l’étendue et retourne un tableau de tous les résultats d’action hello à partir de cette étendue.</span><span class="sxs-lookup"><span data-stu-id="affb6-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="affb6-141">Ces objets action incluent hello même attributs sous la forme d’hello `@actions()` sort de l’objet, y compris l’heure de début d’action, heure de fin d’action, état de l’action, entrées d’action, ID de corrélation action et action.</span><span class="sxs-lookup"><span data-stu-id="affb6-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="affb6-142">contexte toosend de toutes les actions qui ont échoué dans une étendue, vous pouvez facilement associer un `@result()` fonctionne avec un `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="affb6-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="affb6-143">tooexecute une action *pour chaque* action dans une étendue qui `Failed`, tableau de hello de filtre de tooactions de résultats qui ont échoué, vous pouvez également associer des `@result()` avec un  **[filtre tableau](../connectors/connectors-native-query.md)**  action et un  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  boucle.</span><span class="sxs-lookup"><span data-stu-id="affb6-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="affb6-144">Vous pouvez prendre le tableau de résultats filtré hello et effectuer une action pour chaque défaillance à l’aide de hello **ForEach** boucle.</span><span class="sxs-lookup"><span data-stu-id="affb6-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="affb6-145">Voici un exemple, suivi d’une explication détaillée, qui envoie une demande HTTP POST avec un corps de la réponse de toutes les actions qui ont échoué hello étendue hello `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="affb6-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

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

<span data-ttu-id="affb6-146">Voici un toodescribe de procédure pas à pas détaillées que se passe-t-il :</span><span class="sxs-lookup"><span data-stu-id="affb6-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="affb6-147">résultat de hello tooget de toutes les actions dans `My_Scope`, hello **filtre tableau** filtres d’action `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="affb6-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="affb6-148">Hello condition pour **filtre tableau** toute `@result()` élément ayant l’état égal trop`Failed`.</span><span class="sxs-lookup"><span data-stu-id="affb6-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="affb6-149">Cette condition de filtre de tableau hello avec tous les résultats d’action à partir de `My_Scope` tableau tooan avec uniquement échec des résultats d’action.</span><span class="sxs-lookup"><span data-stu-id="affb6-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="affb6-150">Effectuer un **pour chaque** action sur hello **filtrée de tableau** génère.</span><span class="sxs-lookup"><span data-stu-id="affb6-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="affb6-151">Cette étape exécute une action *pour chaque* résultat d’action ayant échoué filtré précédemment.</span><span class="sxs-lookup"><span data-stu-id="affb6-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="affb6-152">En cas d’échec d’une action unique dans la portée de hello, hello actions Bonjour `foreach` n'exécuter qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="affb6-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="affb6-153">De nombreuses actions ayant échoué peuvent provoquer une action par échec.</span><span class="sxs-lookup"><span data-stu-id="affb6-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="affb6-154">Envoyer une requête HTTP POST sur hello `foreach` élément corps de réponse, ou `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="affb6-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="affb6-155">Hello `@result()` forme d’élément est de même hello comme hello `@actions()` mettre en forme et peut être analysé hello même façon.</span><span class="sxs-lookup"><span data-stu-id="affb6-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="affb6-156">Inclure les deux en-têtes personnalisés avec le nom de l’action ayant échoué hello `@item()['name']` et Échec de l’exécution de client ID de suivi hello `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="affb6-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="affb6-157">Pour référence, Voici un exemple d’un seul `@result()` élément, montrant hello `name`, `body`, et `clientTrackingId` les propriétés qui sont analysées dans l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="affb6-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="affb6-158">En dehors de `foreach`, `@result()` retourne un tableau de ces objets.</span><span class="sxs-lookup"><span data-stu-id="affb6-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="affb6-159">tooperform la gestion des exceptions de différents modèles, vous pouvez utiliser des expressions hello indiquées précédemment.</span><span class="sxs-lookup"><span data-stu-id="affb6-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="affb6-160">Vous pouvez choisir tooexecute une action en dehors de la portée hello qui accepte hello ensemble tableau filtré d’échecs d’exceptions unique et supprimer hello `foreach`.</span><span class="sxs-lookup"><span data-stu-id="affb6-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="affb6-161">Vous pouvez également inclure d’autres propriétés utiles à partir de hello `@result()` réponse illustré précédemment.</span><span class="sxs-lookup"><span data-stu-id="affb6-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="affb6-162">Azure Diagnostics et télémétrie</span><span class="sxs-lookup"><span data-stu-id="affb6-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="affb6-163">Hello modèles précédents sont aisément toohandle et exceptions lors d’une exécution, mais vous pouvez également identifier et répondre tooerrors indépendant de hello exécuter lui-même.</span><span class="sxs-lookup"><span data-stu-id="affb6-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="affb6-164">[Diagnostics Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) fournit un moyen simple de toosend compte de stockage Azure tooan tous les flux de travail (y compris tous les États d’exécution et action) ou un concentrateur d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="affb6-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="affb6-165">tooevaluate exécuter des États, vous pouvez surveiller les métriques et les journaux de hello, ou les publier dans n’importe quel outil de surveillance que vous préférez.</span><span class="sxs-lookup"><span data-stu-id="affb6-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="affb6-166">Une option potentielle est toostream tous les événements hello via un concentrateur d’événements Azure dans [flux Analytique](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="affb6-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="affb6-167">Dans le flux de données Analytique, vous pouvez écrire des requêtes actives hors des anomalies, moyennes ou des défaillances de hello des journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="affb6-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="affb6-168">Analytique de flux de sortie peut facilement tooother des sources de données, les files d’attente, rubriques, SQL, base de données Azure Cosmos et Power BI.</span><span class="sxs-lookup"><span data-stu-id="affb6-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="affb6-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="affb6-169">Next Steps</span></span>

* [<span data-ttu-id="affb6-170">Voir comment un client conçoit la gestion des erreurs avec Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="affb6-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="affb6-171">Consultez d’autres exemples et scénarios Logic Apps</span><span class="sxs-lookup"><span data-stu-id="affb6-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="affb6-172">Découvrez comment toocreate automatisé des déploiements pour logic apps</span><span class="sxs-lookup"><span data-stu-id="affb6-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="affb6-173">Créer et déployer des applications logiques avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="affb6-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
