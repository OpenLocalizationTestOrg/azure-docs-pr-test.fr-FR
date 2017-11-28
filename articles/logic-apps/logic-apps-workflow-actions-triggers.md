---
title: "Actions et déclencheurs de workflow - Azure Logic Apps | Microsoft Docs"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="48788-102">Actions et déclencheurs de workflow pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="48788-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="48788-103">Les applications logiques se composent de déclencheurs et d’actions.</span><span class="sxs-lookup"><span data-stu-id="48788-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="48788-104">Il existe six types de déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="48788-104">There are six types of triggers.</span></span> <span data-ttu-id="48788-105">Chaque type présente une interface et un comportement différents.</span><span class="sxs-lookup"><span data-stu-id="48788-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="48788-106">Pour plus d’informations, vous pouvez également examiner le [langage de définition de flux de travail](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="48788-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="48788-107">Poursuivez la lecture de cet article pour en savoir plus sur les déclencheurs et les actions, et la manière dont vous pouvez les utiliser pour créer des applications logiques et améliorer vos processus et workflows d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="48788-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="48788-108">Déclencheurs</span><span class="sxs-lookup"><span data-stu-id="48788-108">Triggers</span></span>  

<span data-ttu-id="48788-109">Un déclencheur spécifie les appels qui peuvent initialiser l’exécution de votre workflow d’application logique.</span><span class="sxs-lookup"><span data-stu-id="48788-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="48788-110">Voici deux moyens différents d’initialiser l’exécution de votre workflow :</span><span class="sxs-lookup"><span data-stu-id="48788-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="48788-111">Un déclencheur d’interrogation</span><span class="sxs-lookup"><span data-stu-id="48788-111">A polling trigger</span></span>  

-   <span data-ttu-id="48788-112">Un déclencheur d’émission (en appelant l’[API REST du service de workflow](https://docs.microsoft.com/rest/api/logic/workflows))</span><span class="sxs-lookup"><span data-stu-id="48788-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="48788-113">Tous les déclencheurs contiennent ces éléments de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="48788-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="48788-114">Types de déclencheurs et entrées associées</span><span class="sxs-lookup"><span data-stu-id="48788-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="48788-115">Vous pouvez utiliser les types de déclencheurs suivants :</span><span class="sxs-lookup"><span data-stu-id="48788-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="48788-116">**Request** \- Fait de l’application logique un point de terminaison que vous pouvez appeler.</span><span class="sxs-lookup"><span data-stu-id="48788-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="48788-117">**Recurrence** \- Se déclenche selon une planification définie.</span><span class="sxs-lookup"><span data-stu-id="48788-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="48788-118">**HTTP**\- Interroge un point de terminaison web HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="48788-119">Le point de terminaison HTTP doit être conforme à un contrat de déclenchement spécifique, soit en utilisant un modèle asynchrone 202, soit en renvoyant un tableau.</span><span class="sxs-lookup"><span data-stu-id="48788-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="48788-120">**ApiConnection** \- Effectue une interrogation comme le déclencheur HTTP, mais en tirant parti des [API gérées par Microsoft](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="48788-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="48788-121">**HTTPWebhook** \- Ouvre un point de terminaison de la même manière que le déclencheur manuel, mais en appelant également une URL spécifique à des fins d’inscription et de désinscription.</span><span class="sxs-lookup"><span data-stu-id="48788-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="48788-122">**ApiConnectionWebhook**\- Fonctionne de la même manière que le déclencheur HTTPWebhook, mais en tirant parti des API gérées par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48788-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="48788-123">Chaque type de déclencheur présente un ensemble différent d’**entrées** qui définissent son comportement.</span><span class="sxs-lookup"><span data-stu-id="48788-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="48788-124">Déclencheur de requête</span><span class="sxs-lookup"><span data-stu-id="48788-124">Request trigger</span></span>  

<span data-ttu-id="48788-125">Ce déclencheur joue un rôle de point de terminaison que vous appelez via une requête HTTP pour appeler votre application logique.</span><span class="sxs-lookup"><span data-stu-id="48788-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="48788-126">Un déclencheur request se présente comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="48788-127">Il existe également une propriété facultative appelée **schema** :</span><span class="sxs-lookup"><span data-stu-id="48788-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="48788-128">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-128">Element name</span></span>|<span data-ttu-id="48788-129">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-129">Required</span></span>|<span data-ttu-id="48788-130">Description</span><span class="sxs-lookup"><span data-stu-id="48788-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="48788-131">schema</span><span class="sxs-lookup"><span data-stu-id="48788-131">schema</span></span>|<span data-ttu-id="48788-132">Non</span><span class="sxs-lookup"><span data-stu-id="48788-132">No</span></span>|<span data-ttu-id="48788-133">Schéma JSON qui valide la requête entrante.</span><span class="sxs-lookup"><span data-stu-id="48788-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="48788-134">Utile pour aider les étapes de workflow suivantes à déterminer les propriétés auxquelles faire référence.</span><span class="sxs-lookup"><span data-stu-id="48788-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="48788-135">Pour appeler ce point de terminaison, vous devez appeler l’API *listCallbackUrl*.</span><span class="sxs-lookup"><span data-stu-id="48788-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="48788-136">Consultez [API REST du service de workflow](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="48788-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="48788-137">Déclencheur recurrence</span><span class="sxs-lookup"><span data-stu-id="48788-137">Recurrence trigger</span></span>  

<span data-ttu-id="48788-138">Un déclencheur recurrence s’exécute selon une planification définie.</span><span class="sxs-lookup"><span data-stu-id="48788-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="48788-139">Ce type de déclencheur peut se présenter comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="48788-140">Comme vous pouvez le constater, il offre un moyen simple d’exécuter un workflow.</span><span class="sxs-lookup"><span data-stu-id="48788-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="48788-141">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-141">Element name</span></span>|<span data-ttu-id="48788-142">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-142">Required</span></span>|<span data-ttu-id="48788-143">Description</span><span class="sxs-lookup"><span data-stu-id="48788-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="48788-144">frequency</span><span class="sxs-lookup"><span data-stu-id="48788-144">frequency</span></span>|<span data-ttu-id="48788-145">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-145">Yes</span></span>|<span data-ttu-id="48788-146">Fréquence à laquelle le déclencheur s’exécute.</span><span class="sxs-lookup"><span data-stu-id="48788-146">How often the trigger executes.</span></span> <span data-ttu-id="48788-147">Utilisez une seule de ces valeurs possibles : second (seconde), minute, hour (heure), day (jour), week (semaine), month (mois) ou year (année).</span><span class="sxs-lookup"><span data-stu-id="48788-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="48788-148">interval</span><span class="sxs-lookup"><span data-stu-id="48788-148">interval</span></span>|<span data-ttu-id="48788-149">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-149">Yes</span></span>|<span data-ttu-id="48788-150">Intervalle de la fréquence donnée pour la récurrence</span><span class="sxs-lookup"><span data-stu-id="48788-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="48788-151">startTime</span><span class="sxs-lookup"><span data-stu-id="48788-151">startTime</span></span>|<span data-ttu-id="48788-152">Non</span><span class="sxs-lookup"><span data-stu-id="48788-152">No</span></span>|<span data-ttu-id="48788-153">Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire (timeZone) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="48788-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="48788-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="48788-154">timeZone</span></span>|<span data-ttu-id="48788-155">no</span><span class="sxs-lookup"><span data-stu-id="48788-155">no</span></span>|<span data-ttu-id="48788-156">Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire (timeZone) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="48788-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="48788-157">Vous pouvez également planifier le démarrage de l’exécution d’un déclencheur à un moment ultérieur.</span><span class="sxs-lookup"><span data-stu-id="48788-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="48788-158">Par exemple, si vous souhaitez démarrer un rapport hebdomadaire tous les lundis, vous pouvez planifier le démarrage de l’application logique tous les lundis en créant le déclencheur suivant :</span><span class="sxs-lookup"><span data-stu-id="48788-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="48788-159">Déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="48788-159">HTTP trigger</span></span>  

<span data-ttu-id="48788-160">Les déclencheurs HTTP interrogent un point de terminaison spécifique et vérifient la réponse pour déterminer si le workflow doit être exécuté.</span><span class="sxs-lookup"><span data-stu-id="48788-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="48788-161">L’objet d’entrée prend l’ensemble des paramètres requis pour construire un appel HTTP :</span><span class="sxs-lookup"><span data-stu-id="48788-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="48788-162">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-162">Element name</span></span>|<span data-ttu-id="48788-163">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-163">Required</span></span>|<span data-ttu-id="48788-164">Description</span><span class="sxs-lookup"><span data-stu-id="48788-164">Description</span></span>|<span data-ttu-id="48788-165">Type</span><span class="sxs-lookup"><span data-stu-id="48788-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="48788-166">method</span><span class="sxs-lookup"><span data-stu-id="48788-166">method</span></span>|<span data-ttu-id="48788-167">yes</span><span class="sxs-lookup"><span data-stu-id="48788-167">yes</span></span>|<span data-ttu-id="48788-168">Peut être l’une des méthodes HTTP suivantes : GET, POST, PUT, DELETE, PATCH ou HEAD.</span><span class="sxs-lookup"><span data-stu-id="48788-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="48788-169">String</span><span class="sxs-lookup"><span data-stu-id="48788-169">String</span></span>|  
|<span data-ttu-id="48788-170">URI</span><span class="sxs-lookup"><span data-stu-id="48788-170">uri</span></span>|<span data-ttu-id="48788-171">yes</span><span class="sxs-lookup"><span data-stu-id="48788-171">yes</span></span>|<span data-ttu-id="48788-172">Point de terminaison HTTP ou HTTPS qui est appelé.</span><span class="sxs-lookup"><span data-stu-id="48788-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="48788-173">La longueur maximale est de 2 Ko.</span><span class="sxs-lookup"><span data-stu-id="48788-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="48788-174">String</span><span class="sxs-lookup"><span data-stu-id="48788-174">String</span></span>|  
|<span data-ttu-id="48788-175">queries</span><span class="sxs-lookup"><span data-stu-id="48788-175">queries</span></span>|<span data-ttu-id="48788-176">Non</span><span class="sxs-lookup"><span data-stu-id="48788-176">No</span></span>|<span data-ttu-id="48788-177">Objet représentant les paramètres de requête à ajouter à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="48788-178">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="48788-179">Object</span><span class="sxs-lookup"><span data-stu-id="48788-179">Object</span></span>|  
|<span data-ttu-id="48788-180">headers</span><span class="sxs-lookup"><span data-stu-id="48788-180">headers</span></span>|<span data-ttu-id="48788-181">Non</span><span class="sxs-lookup"><span data-stu-id="48788-181">No</span></span>|<span data-ttu-id="48788-182">Objet représentant chacun des en-têtes envoyés à la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="48788-183">Par exemple, pour définir la langue et le type sur une requête :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48788-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="48788-184">Object</span><span class="sxs-lookup"><span data-stu-id="48788-184">Object</span></span>|  
|<span data-ttu-id="48788-185">body</span><span class="sxs-lookup"><span data-stu-id="48788-185">body</span></span>|<span data-ttu-id="48788-186">Non</span><span class="sxs-lookup"><span data-stu-id="48788-186">No</span></span>|<span data-ttu-id="48788-187">Objet représentant la charge utile envoyée au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48788-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="48788-188">Object</span><span class="sxs-lookup"><span data-stu-id="48788-188">Object</span></span>|  
|<span data-ttu-id="48788-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="48788-189">retryPolicy</span></span>|<span data-ttu-id="48788-190">Non</span><span class="sxs-lookup"><span data-stu-id="48788-190">No</span></span>|<span data-ttu-id="48788-191">Objet permettant de personnaliser le comportement de nouvelle tentative pour les erreurs 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="48788-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="48788-192">Object</span><span class="sxs-lookup"><span data-stu-id="48788-192">Object</span></span>|  
|<span data-ttu-id="48788-193">authentication</span><span class="sxs-lookup"><span data-stu-id="48788-193">authentication</span></span>|<span data-ttu-id="48788-194">Non</span><span class="sxs-lookup"><span data-stu-id="48788-194">No</span></span>|<span data-ttu-id="48788-195">Représente la méthode à utiliser pour authentifier la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="48788-196">Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="48788-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="48788-197">En plus de Scheduler, une autre propriété est prise en charge : `authority`. Par défaut, cette propriété est définie sur `https://login.windows.net` lorsqu’aucune valeur n’est spécifiée, mais vous pouvez utiliser une autre audience comme `https://login.windows\-ppe.net`.</span><span class="sxs-lookup"><span data-stu-id="48788-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="48788-198">Object</span><span class="sxs-lookup"><span data-stu-id="48788-198">Object</span></span>|  
  
<span data-ttu-id="48788-199">Le déclencheur HTTP nécessite que l’API HTTP se conforme à un modèle spécifique pour fonctionner correctement avec votre application logique.</span><span class="sxs-lookup"><span data-stu-id="48788-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="48788-200">Il requiert les champs suivants :</span><span class="sxs-lookup"><span data-stu-id="48788-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="48788-201">Réponse</span><span class="sxs-lookup"><span data-stu-id="48788-201">Response</span></span>|<span data-ttu-id="48788-202">Description</span><span class="sxs-lookup"><span data-stu-id="48788-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="48788-203">Code d’état</span><span class="sxs-lookup"><span data-stu-id="48788-203">Status code</span></span>|<span data-ttu-id="48788-204">Code d’état 200 \(OK\) pour déclencher une exécution.</span><span class="sxs-lookup"><span data-stu-id="48788-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="48788-205">Les autres codes d’état ne déclenchent pas d’exécution.</span><span class="sxs-lookup"><span data-stu-id="48788-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="48788-206">En-tête Retry\-After</span><span class="sxs-lookup"><span data-stu-id="48788-206">Retry\-after header</span></span>|<span data-ttu-id="48788-207">Nombre de secondes au bout duquel l’application logique interroge à nouveau le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48788-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="48788-208">En-tête Location</span><span class="sxs-lookup"><span data-stu-id="48788-208">Location header</span></span>|<span data-ttu-id="48788-209">URL à appeler lors du prochain intervalle d’interrogation.</span><span class="sxs-lookup"><span data-stu-id="48788-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="48788-210">Si aucune valeur n’est spécifiée, l’URL d’origine est utilisée.</span><span class="sxs-lookup"><span data-stu-id="48788-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="48788-211">Voici quelques exemples de comportements différents pour les différents types de requêtes :</span><span class="sxs-lookup"><span data-stu-id="48788-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="48788-212">Response code</span><span class="sxs-lookup"><span data-stu-id="48788-212">Response code</span></span>|<span data-ttu-id="48788-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="48788-213">Retry\-After</span></span>|<span data-ttu-id="48788-214">Comportement</span><span class="sxs-lookup"><span data-stu-id="48788-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="48788-215">200</span><span class="sxs-lookup"><span data-stu-id="48788-215">200</span></span>|<span data-ttu-id="48788-216">\(Aucune\)</span><span class="sxs-lookup"><span data-stu-id="48788-216">\(none\)</span></span>|<span data-ttu-id="48788-217">Déclencheur non valide, Retry\-After est requis, sinon le moteur n’interrogera jamais la requête suivante.</span><span class="sxs-lookup"><span data-stu-id="48788-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="48788-218">202</span><span class="sxs-lookup"><span data-stu-id="48788-218">202</span></span>|<span data-ttu-id="48788-219">60</span><span class="sxs-lookup"><span data-stu-id="48788-219">60</span></span>|<span data-ttu-id="48788-220">Ne pas déclencher le workflow.</span><span class="sxs-lookup"><span data-stu-id="48788-220">Do not trigger the workflow.</span></span> <span data-ttu-id="48788-221">La tentative suivante aura lieu une minute après.</span><span class="sxs-lookup"><span data-stu-id="48788-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="48788-222">200</span><span class="sxs-lookup"><span data-stu-id="48788-222">200</span></span>|<span data-ttu-id="48788-223">10</span><span class="sxs-lookup"><span data-stu-id="48788-223">10</span></span>|<span data-ttu-id="48788-224">Exécuter le workflow, et vérifier si du contenu supplémentaire est disponible 10 secondes après.</span><span class="sxs-lookup"><span data-stu-id="48788-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="48788-225">400</span><span class="sxs-lookup"><span data-stu-id="48788-225">400</span></span>|<span data-ttu-id="48788-226">\(Aucune\)</span><span class="sxs-lookup"><span data-stu-id="48788-226">\(none\)</span></span>|<span data-ttu-id="48788-227">Requête incorrecte, ne pas exécuter le workflow.</span><span class="sxs-lookup"><span data-stu-id="48788-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="48788-228">Si aucune **stratégie de nouvelle tentative** n’est définie, la stratégie par défaut est utilisée.</span><span class="sxs-lookup"><span data-stu-id="48788-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="48788-229">Une fois que le nombre de nouvelles tentatives a été atteint, le déclencheur n’est plus valide.</span><span class="sxs-lookup"><span data-stu-id="48788-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="48788-230">500</span><span class="sxs-lookup"><span data-stu-id="48788-230">500</span></span>|<span data-ttu-id="48788-231">\(Aucune\)</span><span class="sxs-lookup"><span data-stu-id="48788-231">\(none\)</span></span>|<span data-ttu-id="48788-232">Erreur de serveur, ne pas exécuter le workflow.</span><span class="sxs-lookup"><span data-stu-id="48788-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="48788-233">Si aucune **stratégie de nouvelle tentative** n’est définie, la stratégie par défaut est utilisée.</span><span class="sxs-lookup"><span data-stu-id="48788-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="48788-234">Une fois que le nombre de nouvelles tentatives a été atteint, le déclencheur n’est plus valide.</span><span class="sxs-lookup"><span data-stu-id="48788-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="48788-235">Les sorties d’un déclencheur HTTP se présentent comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="48788-236">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-236">Element name</span></span>|<span data-ttu-id="48788-237">Description</span><span class="sxs-lookup"><span data-stu-id="48788-237">Description</span></span>|<span data-ttu-id="48788-238">Type</span><span class="sxs-lookup"><span data-stu-id="48788-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="48788-239">headers</span><span class="sxs-lookup"><span data-stu-id="48788-239">headers</span></span>|<span data-ttu-id="48788-240">En-têtes de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-240">The headers of the http response.</span></span>|<span data-ttu-id="48788-241">Object</span><span class="sxs-lookup"><span data-stu-id="48788-241">Object</span></span>|  
|<span data-ttu-id="48788-242">body</span><span class="sxs-lookup"><span data-stu-id="48788-242">body</span></span>|<span data-ttu-id="48788-243">Corps de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-243">The body of the http response.</span></span>|<span data-ttu-id="48788-244">Object</span><span class="sxs-lookup"><span data-stu-id="48788-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="48788-245">Déclencheur ApiConnection</span><span class="sxs-lookup"><span data-stu-id="48788-245">API Connection trigger</span></span>  

<span data-ttu-id="48788-246">Le déclencheur ApiConnection présente des fonctionnalités de base similaires à celles du déclencheur HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="48788-247">Cependant, les paramètres d’identification de l’action sont différents.</span><span class="sxs-lookup"><span data-stu-id="48788-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="48788-248">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="48788-249">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-249">Element name</span></span>|<span data-ttu-id="48788-250">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-250">Required</span></span>|<span data-ttu-id="48788-251">Type</span><span class="sxs-lookup"><span data-stu-id="48788-251">Type</span></span>|<span data-ttu-id="48788-252">Description</span><span class="sxs-lookup"><span data-stu-id="48788-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="48788-253">host</span><span class="sxs-lookup"><span data-stu-id="48788-253">host</span></span>|<span data-ttu-id="48788-254">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-254">Yes</span></span>||<span data-ttu-id="48788-255">Passerelle et ID d’hôte de l’application d’API.</span><span class="sxs-lookup"><span data-stu-id="48788-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="48788-256">method</span><span class="sxs-lookup"><span data-stu-id="48788-256">method</span></span>|<span data-ttu-id="48788-257">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-257">Yes</span></span>|<span data-ttu-id="48788-258">String</span><span class="sxs-lookup"><span data-stu-id="48788-258">String</span></span>|<span data-ttu-id="48788-259">Peut être l’une des méthodes HTTP suivantes : **GET**, **POST**, **PUT**, **DELETE**, **PATCH** ou **HEAD**.</span><span class="sxs-lookup"><span data-stu-id="48788-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="48788-260">queries</span><span class="sxs-lookup"><span data-stu-id="48788-260">queries</span></span>|<span data-ttu-id="48788-261">Non</span><span class="sxs-lookup"><span data-stu-id="48788-261">No</span></span>|<span data-ttu-id="48788-262">Object</span><span class="sxs-lookup"><span data-stu-id="48788-262">Object</span></span>|<span data-ttu-id="48788-263">Représente les paramètres de requête à ajouter à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="48788-264">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48788-265">headers</span><span class="sxs-lookup"><span data-stu-id="48788-265">headers</span></span>|<span data-ttu-id="48788-266">Non</span><span class="sxs-lookup"><span data-stu-id="48788-266">No</span></span>|<span data-ttu-id="48788-267">Object</span><span class="sxs-lookup"><span data-stu-id="48788-267">Object</span></span>|<span data-ttu-id="48788-268">Représente chacun des en-têtes envoyés à la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48788-269">Par exemple, pour définir la langue et le type sur une requête :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48788-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="48788-270">body</span><span class="sxs-lookup"><span data-stu-id="48788-270">body</span></span>|<span data-ttu-id="48788-271">Non</span><span class="sxs-lookup"><span data-stu-id="48788-271">No</span></span>|<span data-ttu-id="48788-272">Object</span><span class="sxs-lookup"><span data-stu-id="48788-272">Object</span></span>|<span data-ttu-id="48788-273">Représente la charge utile envoyée au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48788-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="48788-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="48788-274">retryPolicy</span></span>|<span data-ttu-id="48788-275">Non</span><span class="sxs-lookup"><span data-stu-id="48788-275">No</span></span>|<span data-ttu-id="48788-276">Object</span><span class="sxs-lookup"><span data-stu-id="48788-276">Object</span></span>|<span data-ttu-id="48788-277">Permet de personnaliser le comportement de nouvelle tentative pour les erreurs 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="48788-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="48788-278">authentication</span><span class="sxs-lookup"><span data-stu-id="48788-278">authentication</span></span>|<span data-ttu-id="48788-279">Non</span><span class="sxs-lookup"><span data-stu-id="48788-279">No</span></span>|<span data-ttu-id="48788-280">Object</span><span class="sxs-lookup"><span data-stu-id="48788-280">Object</span></span>|<span data-ttu-id="48788-281">Représente la méthode à utiliser pour authentifier la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="48788-282">Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="48788-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="48788-283">Les propriétés de l’élément host sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="48788-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="48788-284">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-284">Element name</span></span>|<span data-ttu-id="48788-285">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-285">Required</span></span>|<span data-ttu-id="48788-286">Description</span><span class="sxs-lookup"><span data-stu-id="48788-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="48788-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="48788-287">api runtimeUrl</span></span>|<span data-ttu-id="48788-288">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-288">Yes</span></span>|<span data-ttu-id="48788-289">Le point de terminaison de l’API gérée.</span><span class="sxs-lookup"><span data-stu-id="48788-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="48788-290">connection name</span><span class="sxs-lookup"><span data-stu-id="48788-290">connection name</span></span>||<span data-ttu-id="48788-291">Doit être une référence à un paramètre appelé `$connection` et correspond au nom de la connexion d’API gérée que le workflow utilise.</span><span class="sxs-lookup"><span data-stu-id="48788-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="48788-292">Les sorties du déclencheur ApiConnection sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="48788-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="48788-293">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-293">Element name</span></span>|<span data-ttu-id="48788-294">Type</span><span class="sxs-lookup"><span data-stu-id="48788-294">Type</span></span>|<span data-ttu-id="48788-295">Description</span><span class="sxs-lookup"><span data-stu-id="48788-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="48788-296">headers</span><span class="sxs-lookup"><span data-stu-id="48788-296">headers</span></span>|<span data-ttu-id="48788-297">Object</span><span class="sxs-lookup"><span data-stu-id="48788-297">Object</span></span>|<span data-ttu-id="48788-298">En-têtes de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="48788-299">body</span><span class="sxs-lookup"><span data-stu-id="48788-299">body</span></span>|<span data-ttu-id="48788-300">Object</span><span class="sxs-lookup"><span data-stu-id="48788-300">Object</span></span>|<span data-ttu-id="48788-301">Corps de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="48788-302">Déclencheur HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="48788-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="48788-303">Le déclencheur HTTPWebhook ouvre un point de terminaison de la même manière que le déclencheur manuel, mais il appelle également une URL spécifique à des fins d’inscription et de désinscription.</span><span class="sxs-lookup"><span data-stu-id="48788-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="48788-304">Un déclencheur HTTPWebhook peut se présenter comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="48788-305">Un grand nombre de ces sections sont facultatives, et le comportement du webhook varie selon les sections fournies ou omises.</span><span class="sxs-lookup"><span data-stu-id="48788-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="48788-306">Les propriétés d’un webhook sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="48788-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="48788-307">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-307">Element name</span></span>|<span data-ttu-id="48788-308">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-308">Required</span></span>|<span data-ttu-id="48788-309">Description</span><span class="sxs-lookup"><span data-stu-id="48788-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="48788-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="48788-310">subscribe</span></span>|<span data-ttu-id="48788-311">Non</span><span class="sxs-lookup"><span data-stu-id="48788-311">No</span></span>|<span data-ttu-id="48788-312">Demande sortante appelée lorsque le déclencheur est créé et effectue l’inscription initiale.</span><span class="sxs-lookup"><span data-stu-id="48788-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="48788-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="48788-313">unsubscribe</span></span>|<span data-ttu-id="48788-314">Non</span><span class="sxs-lookup"><span data-stu-id="48788-314">No</span></span>|<span data-ttu-id="48788-315">Demande sortante lorsque le déclencheur est supprimé.</span><span class="sxs-lookup"><span data-stu-id="48788-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="48788-316">**subscribe** est l’appel sortant effectué pour commencer à écouter des événements.</span><span class="sxs-lookup"><span data-stu-id="48788-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="48788-317">Cet appel commence par le même ensemble de paramètres que les actions HTTP normales.</span><span class="sxs-lookup"><span data-stu-id="48788-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="48788-318">Cet appel sortant est effectué à chaque fois que le workflow change de quelque façon, par exemple lorsque les informations d’identification sont remplacées ou les paramètres d’entrée du déclencheur modifiés.</span><span class="sxs-lookup"><span data-stu-id="48788-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="48788-319">En complément de cet appel, il existe une nouvelle fonction : `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="48788-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="48788-320">Cette fonction renvoie une URL unique pour ce déclencheur spécifique dans ce workflow.</span><span class="sxs-lookup"><span data-stu-id="48788-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="48788-321">Elle constitue l’identificateur unique des points de terminaison qui utilisent l’API REST du service.</span><span class="sxs-lookup"><span data-stu-id="48788-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="48788-322">**unsubscribe** est appelé lorsqu’une opération rend ce déclencheur non valide, notamment dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="48788-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="48788-323">Suppression ou désactivation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="48788-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="48788-324">Suppression ou désactivation du workflow</span><span class="sxs-lookup"><span data-stu-id="48788-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="48788-325">Suppression ou désactivation de l’inscription</span><span class="sxs-lookup"><span data-stu-id="48788-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="48788-326">L’application logique appelle automatiquement l’action unsubscribe.</span><span class="sxs-lookup"><span data-stu-id="48788-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="48788-327">Les paramètres de cette fonction sont les mêmes que ceux du déclencheur HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="48788-328">Les sorties du déclencheur HTTPWebhook correspondent au contenu de la demande entrante :</span><span class="sxs-lookup"><span data-stu-id="48788-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="48788-329">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-329">Element name</span></span>|<span data-ttu-id="48788-330">Type</span><span class="sxs-lookup"><span data-stu-id="48788-330">Type</span></span>|<span data-ttu-id="48788-331">Description</span><span class="sxs-lookup"><span data-stu-id="48788-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="48788-332">headers</span><span class="sxs-lookup"><span data-stu-id="48788-332">headers</span></span>|<span data-ttu-id="48788-333">Object</span><span class="sxs-lookup"><span data-stu-id="48788-333">Object</span></span>|<span data-ttu-id="48788-334">En-têtes de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="48788-335">body</span><span class="sxs-lookup"><span data-stu-id="48788-335">body</span></span>|<span data-ttu-id="48788-336">Object</span><span class="sxs-lookup"><span data-stu-id="48788-336">Object</span></span>|<span data-ttu-id="48788-337">Corps de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-337">The body of the http request.</span></span>|  

<span data-ttu-id="48788-338">Les limites d’une action webhook peuvent être spécifiées de la même manière que les [limites asynchrones HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="48788-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="48788-339">Conditions</span><span class="sxs-lookup"><span data-stu-id="48788-339">Conditions</span></span>  

<span data-ttu-id="48788-340">Pour n’importe quel déclencheur, vous pouvez utiliser une ou plusieurs conditions pour déterminer si le workflow doit s’exécuter ou non.</span><span class="sxs-lookup"><span data-stu-id="48788-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="48788-341">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="48788-342">Dans ce cas, le rapport se déclenche uniquement lorsque le paramètre `sendReports` du workflow est défini sur true.</span><span class="sxs-lookup"><span data-stu-id="48788-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="48788-343">Enfin, les conditions peuvent faire référence au code d’état du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="48788-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="48788-344">Par exemple, vous pouvez lancer un workflow uniquement lorsque votre site web renvoie un code d’état 500, comme suit :</span><span class="sxs-lookup"><span data-stu-id="48788-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="48788-345">Lorsqu’une expression fait référence au code d’état du déclencheur \(de quelque façon\), le comportement par défaut \(trigger only on 200 \(OK\) \) est remplacé.</span><span class="sxs-lookup"><span data-stu-id="48788-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="48788-346">Par exemple, si vous souhaitez que le déclenchement soit effectué avec le code d’état 200 et le code d’état 201, vous devez inclure la condition `@or(equals(triggers().code, 200),equals(triggers().code,201))`.</span><span class="sxs-lookup"><span data-stu-id="48788-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="48788-347">Démarrer plusieurs exécutions pour une requête</span><span class="sxs-lookup"><span data-stu-id="48788-347">Start multiple runs for a request</span></span>

<span data-ttu-id="48788-348">Pour lancer plusieurs exécutions pour une requête unique, par exemple lorsque vous souhaitez interroger un point de terminaison qui peut présenter plusieurs nouveaux éléments entre les intervalles d’interrogation, vous pouvez utiliser `splitOn`.</span><span class="sxs-lookup"><span data-stu-id="48788-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="48788-349">Avec `splitOn`, vous spécifiez la propriété à l’intérieur de la charge utile de réponse qui contient le tableau de tous les éléments que vous souhaitez utiliser pour démarrer l’exécution du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="48788-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="48788-350">Par exemple, supposons que vous ayez une API qui renvoie la réponse suivante :</span><span class="sxs-lookup"><span data-stu-id="48788-350">For example, imagine you have an API that returns the following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="48788-351">Comme votre application logique a uniquement besoin du contenu de Rows, vous pouvez construire votre déclencheur comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="48788-352">Ensuite, dans la définition du workflow, `@triggerBody().name` renvoie `mycoolrow` pour la première exécution, et `another row` pour la deuxième exécution.</span><span class="sxs-lookup"><span data-stu-id="48788-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="48788-353">Les sorties du déclencheur se présentent comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="48788-354">Par conséquent, si vous utilisez `SplitOn`, vous ne pouvez pas obtenir les propriétés qui ne se trouvent pas dans le tableau (dans le cas présent, le champ `Status`).</span><span class="sxs-lookup"><span data-stu-id="48788-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="48788-355">Dans cet exemple, nous utilisons l’opérateur `?` afin d’éviter un échec en cas d’absence de la propriété `Rows`.</span><span class="sxs-lookup"><span data-stu-id="48788-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="48788-356">Instance d’exécution unique</span><span class="sxs-lookup"><span data-stu-id="48788-356">Single run instance</span></span>

<span data-ttu-id="48788-357">Vous pouvez configurer les déclencheurs présentant une propriété recurrence de telle sorte qu’ils ne se déclenchent que lorsque toutes les exécutions actives sont terminées.</span><span class="sxs-lookup"><span data-stu-id="48788-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="48788-358">Si une répétition planifiée a lieu alors qu’une exécution est encore en cours, le déclencheur attend l’intervalle de périodicité planifié suivant pour effectuer une nouvelle vérification.</span><span class="sxs-lookup"><span data-stu-id="48788-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="48788-359">Vous pouvez configurer ce paramètre via les options d’opération :</span><span class="sxs-lookup"><span data-stu-id="48788-359">You can configure this setting through the operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="48788-360">Types et entrées</span><span class="sxs-lookup"><span data-stu-id="48788-360">Types and inputs</span></span>  

<span data-ttu-id="48788-361">Il existe de nombreux types d’actions, chacune présentant un comportement unique.</span><span class="sxs-lookup"><span data-stu-id="48788-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="48788-362">Les actions de collection peuvent contenir de nombreuses autres actions.</span><span class="sxs-lookup"><span data-stu-id="48788-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="48788-363">Actions standard</span><span class="sxs-lookup"><span data-stu-id="48788-363">Standard actions</span></span>  

-   <span data-ttu-id="48788-364">**HTTP** - Cette action appelle un point de terminaison web HTTP.</span><span class="sxs-lookup"><span data-stu-id="48788-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="48788-365">**ApiConnection** \- Cette action se comporte comme l’action HTTP, mais utilise les API gérées par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48788-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="48788-366">**ApiConnectionWebhook** \- Similaire à HTTPWebhook, mais utilise les API gérées par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48788-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="48788-367">**Response** \- Cette action définit une réponse pour un appel entrant.</span><span class="sxs-lookup"><span data-stu-id="48788-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="48788-368">**Wait** \- Cette action simple déclenche une attente pendant une durée définie ou jusqu’à un moment spécifique.</span><span class="sxs-lookup"><span data-stu-id="48788-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="48788-369">**Workflow** \- Cette action représente un workflow imbriqué.</span><span class="sxs-lookup"><span data-stu-id="48788-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="48788-370">**Function** \- Cette action représente une fonction d’Azure.</span><span class="sxs-lookup"><span data-stu-id="48788-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="48788-371">Actions de collection</span><span class="sxs-lookup"><span data-stu-id="48788-371">Collection actions</span></span>

-   <span data-ttu-id="48788-372">**Scope** \- Cette action est un regroupement logique d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="48788-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="48788-373">**Condition** \- Cette action évalue une expression et exécute la branche de résultat correspondante.</span><span class="sxs-lookup"><span data-stu-id="48788-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="48788-374">**ForEach** \- Cette action en boucle effectue une itération dans un tableau et exécute des actions internes pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="48788-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="48788-375">**Until** \- Cette action en boucle exécute des actions internes jusqu’à ce qu’une condition soit vérifiée.</span><span class="sxs-lookup"><span data-stu-id="48788-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="48788-376">Chaque type d’action présente un ensemble différent d’**entrées** qui définissent le comportement d’une action.</span><span class="sxs-lookup"><span data-stu-id="48788-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="48788-377">Action HTTP</span><span class="sxs-lookup"><span data-stu-id="48788-377">HTTP action</span></span>  

<span data-ttu-id="48788-378">Les actions HTTP appellent un point de terminaison spécifique et vérifient la réponse pour déterminer si le workflow doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="48788-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="48788-379">L’objet d’**entrée** prend l’ensemble des paramètres requis pour construire l’appel HTTP :</span><span class="sxs-lookup"><span data-stu-id="48788-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="48788-380">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-380">Element name</span></span>|<span data-ttu-id="48788-381">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-381">Required</span></span>|<span data-ttu-id="48788-382">Type</span><span class="sxs-lookup"><span data-stu-id="48788-382">Type</span></span>|<span data-ttu-id="48788-383">Description</span><span class="sxs-lookup"><span data-stu-id="48788-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="48788-384">method</span><span class="sxs-lookup"><span data-stu-id="48788-384">method</span></span>|<span data-ttu-id="48788-385">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-385">Yes</span></span>|<span data-ttu-id="48788-386">String</span><span class="sxs-lookup"><span data-stu-id="48788-386">String</span></span>|<span data-ttu-id="48788-387">Peut être l’une des méthodes HTTP suivantes : **GET**, **POST**, **PUT**, **DELETE**, **PATCH** ou **HEAD**.</span><span class="sxs-lookup"><span data-stu-id="48788-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="48788-388">URI</span><span class="sxs-lookup"><span data-stu-id="48788-388">uri</span></span>|<span data-ttu-id="48788-389">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-389">Yes</span></span>|<span data-ttu-id="48788-390">String</span><span class="sxs-lookup"><span data-stu-id="48788-390">String</span></span>|<span data-ttu-id="48788-391">Point de terminaison HTTP ou HTTPS qui est appelé.</span><span class="sxs-lookup"><span data-stu-id="48788-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="48788-392">La longueur maximale est de 2 Ko.</span><span class="sxs-lookup"><span data-stu-id="48788-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="48788-393">queries</span><span class="sxs-lookup"><span data-stu-id="48788-393">queries</span></span>|<span data-ttu-id="48788-394">Non</span><span class="sxs-lookup"><span data-stu-id="48788-394">No</span></span>|<span data-ttu-id="48788-395">Object</span><span class="sxs-lookup"><span data-stu-id="48788-395">Object</span></span>|<span data-ttu-id="48788-396">Représente les paramètres de requête à ajouter à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="48788-397">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48788-398">headers</span><span class="sxs-lookup"><span data-stu-id="48788-398">headers</span></span>|<span data-ttu-id="48788-399">Non</span><span class="sxs-lookup"><span data-stu-id="48788-399">No</span></span>|<span data-ttu-id="48788-400">Object</span><span class="sxs-lookup"><span data-stu-id="48788-400">Object</span></span>|<span data-ttu-id="48788-401">Représente chacun des en-têtes envoyés à la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48788-402">Par exemple, pour définir la langue et le type sur une requête :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48788-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="48788-403">body</span><span class="sxs-lookup"><span data-stu-id="48788-403">body</span></span>|<span data-ttu-id="48788-404">Non</span><span class="sxs-lookup"><span data-stu-id="48788-404">No</span></span>|<span data-ttu-id="48788-405">Object</span><span class="sxs-lookup"><span data-stu-id="48788-405">Object</span></span>|<span data-ttu-id="48788-406">Représente la charge utile envoyée au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48788-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="48788-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="48788-407">retryPolicy</span></span>|<span data-ttu-id="48788-408">Non</span><span class="sxs-lookup"><span data-stu-id="48788-408">No</span></span>|<span data-ttu-id="48788-409">Object</span><span class="sxs-lookup"><span data-stu-id="48788-409">Object</span></span>|<span data-ttu-id="48788-410">Permet de personnaliser le comportement de nouvelle tentative pour les erreurs 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="48788-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="48788-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="48788-411">operationsOptions</span></span>|<span data-ttu-id="48788-412">Non</span><span class="sxs-lookup"><span data-stu-id="48788-412">No</span></span>|<span data-ttu-id="48788-413">String</span><span class="sxs-lookup"><span data-stu-id="48788-413">String</span></span>|<span data-ttu-id="48788-414">Définit l’ensemble de comportements spéciaux à substituer.</span><span class="sxs-lookup"><span data-stu-id="48788-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="48788-415">authentication</span><span class="sxs-lookup"><span data-stu-id="48788-415">authentication</span></span>|<span data-ttu-id="48788-416">Non</span><span class="sxs-lookup"><span data-stu-id="48788-416">No</span></span>|<span data-ttu-id="48788-417">Object</span><span class="sxs-lookup"><span data-stu-id="48788-417">Object</span></span>|<span data-ttu-id="48788-418">Représente la méthode à utiliser pour authentifier la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="48788-419">Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="48788-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="48788-420">En plus de Scheduler, une autre propriété est prise en charge : `authority`.</span><span class="sxs-lookup"><span data-stu-id="48788-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="48788-421">Par défaut, cette propriété est définie sur `https://login.windows.net` lorsqu’aucune valeur n’est spécifiée, mais vous pouvez utiliser une autre audience comme `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="48788-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="48788-422">Les actions HTTP \(et ApiConnection\) prennent en charge les stratégies de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="48788-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="48788-423">Une stratégie de nouvelle tentative s’applique aux échecs temporaires, caractérisés par les codes d’état HTTP 408, 429 et 5xx, en plus de toutes les exceptions de connectivité.</span><span class="sxs-lookup"><span data-stu-id="48788-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="48788-424">Cette stratégie est décrite à l’aide de l’objet *retryPolicy* défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="48788-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="48788-425">L’intervalle avant nouvelle tentative est spécifié dans le format ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="48788-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="48788-426">L’intervalle présente une valeur par défaut (et minimale) de 20 secondes, tandis que la valeur maximale est d’une heure.</span><span class="sxs-lookup"><span data-stu-id="48788-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="48788-427">Le nombre de nouvelles tentatives par défaut (et maximal) est de 4.</span><span class="sxs-lookup"><span data-stu-id="48788-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="48788-428">Si la définition de stratégie de nouvelle tentative n’est pas spécifiée, une stratégie `fixed` est utilisée avec les valeurs d’intervalle et de nombre de nouvelles tentatives par défaut.</span><span class="sxs-lookup"><span data-stu-id="48788-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="48788-429">Pour désactiver la stratégie de nouvelle tentative, définissez son type sur `None`.</span><span class="sxs-lookup"><span data-stu-id="48788-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="48788-430">Par exemple, en cas d’échec temporaire, l’action suivante tente à nouveau de récupérer les dernières actualités deux fois, pour un total de 3 exécutions, avec un délai de 30 secondes entre chaque tentative :</span><span class="sxs-lookup"><span data-stu-id="48788-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="48788-431">Modèles asynchrones</span><span class="sxs-lookup"><span data-stu-id="48788-431">Asynchronous patterns</span></span>

<span data-ttu-id="48788-432">Par défaut, toutes les actions basées sur HTTP prennent en charge le modèle d’opération asynchrone standard.</span><span class="sxs-lookup"><span data-stu-id="48788-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="48788-433">Par conséquent, si le serveur distant indique que la requête est acceptée pour traitement avec une réponse 202 \(Accepted\) (Acceptée), le moteur Logic Apps continue à interroger l’URL spécifiée dans l’en-tête Location de la réponse jusqu’à atteindre un état terminal \(c’est-à-dire une réponse autre que 202\).</span><span class="sxs-lookup"><span data-stu-id="48788-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="48788-434">Pour désactiver le comportement asynchrone décrit précédemment, définissez une option `DisableAsyncPattern` dans les entrées de l’action.</span><span class="sxs-lookup"><span data-stu-id="48788-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="48788-435">Dans ce cas, la sortie de l’action est basée sur la réponse 202 initiale du serveur.</span><span class="sxs-lookup"><span data-stu-id="48788-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="48788-436">Limites asynchrones</span><span class="sxs-lookup"><span data-stu-id="48788-436">Asynchronous Limits</span></span>

<span data-ttu-id="48788-437">Un modèle asynchrone peut être limité dans sa durée à un intervalle de temps spécifique.</span><span class="sxs-lookup"><span data-stu-id="48788-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="48788-438">Si l’intervalle de temps s’écoule sans qu’un état terminal ait été atteint, l’état de l’action sera marqué comme `Cancelled` avec un code `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="48788-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="48788-439">Le délai d’expiration de la limite est spécifié au format ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="48788-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="48788-440">Les limites peuvent être spécifiées avec la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="48788-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="48788-441">ApiConnection</span><span class="sxs-lookup"><span data-stu-id="48788-441">API Connection</span></span>  

<span data-ttu-id="48788-442">ApiConnection est une action qui fait référence à un connecteur géré par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48788-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="48788-443">Cette action requiert une référence à une connexion valide, ainsi que des informations sur l’API et les paramètres requis.</span><span class="sxs-lookup"><span data-stu-id="48788-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="48788-444">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="48788-444">Element name</span></span>|<span data-ttu-id="48788-445">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-445">Required</span></span>|<span data-ttu-id="48788-446">Type</span><span class="sxs-lookup"><span data-stu-id="48788-446">Type</span></span>|<span data-ttu-id="48788-447">Description</span><span class="sxs-lookup"><span data-stu-id="48788-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="48788-448">host</span><span class="sxs-lookup"><span data-stu-id="48788-448">host</span></span>|<span data-ttu-id="48788-449">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-449">Yes</span></span>|<span data-ttu-id="48788-450">Object</span><span class="sxs-lookup"><span data-stu-id="48788-450">Object</span></span>|<span data-ttu-id="48788-451">Représente les informations sur le connecteur, telles que la propriété runtimeUrl et la référence à l’objet de connexion.</span><span class="sxs-lookup"><span data-stu-id="48788-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="48788-452">method</span><span class="sxs-lookup"><span data-stu-id="48788-452">method</span></span>|<span data-ttu-id="48788-453">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-453">Yes</span></span>|<span data-ttu-id="48788-454">String</span><span class="sxs-lookup"><span data-stu-id="48788-454">String</span></span>|<span data-ttu-id="48788-455">Peut être l’une des méthodes HTTP suivantes : **GET**, **POST**, **PUT**, **DELETE**, **PATCH** ou **HEAD**.</span><span class="sxs-lookup"><span data-stu-id="48788-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="48788-456">path</span><span class="sxs-lookup"><span data-stu-id="48788-456">path</span></span>|<span data-ttu-id="48788-457">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-457">Yes</span></span>|<span data-ttu-id="48788-458">String</span><span class="sxs-lookup"><span data-stu-id="48788-458">String</span></span>|<span data-ttu-id="48788-459">Chemin de l’opération d’API.</span><span class="sxs-lookup"><span data-stu-id="48788-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="48788-460">queries</span><span class="sxs-lookup"><span data-stu-id="48788-460">queries</span></span>|<span data-ttu-id="48788-461">Non</span><span class="sxs-lookup"><span data-stu-id="48788-461">No</span></span>|<span data-ttu-id="48788-462">Object</span><span class="sxs-lookup"><span data-stu-id="48788-462">Object</span></span>|<span data-ttu-id="48788-463">Représente les paramètres de requête à ajouter à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="48788-464">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48788-465">headers</span><span class="sxs-lookup"><span data-stu-id="48788-465">headers</span></span>|<span data-ttu-id="48788-466">Non</span><span class="sxs-lookup"><span data-stu-id="48788-466">No</span></span>|<span data-ttu-id="48788-467">Object</span><span class="sxs-lookup"><span data-stu-id="48788-467">Object</span></span>|<span data-ttu-id="48788-468">Représente chacun des en-têtes envoyés à la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48788-469">Par exemple, pour définir la langue et le type sur une requête :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48788-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="48788-470">body</span><span class="sxs-lookup"><span data-stu-id="48788-470">body</span></span>|<span data-ttu-id="48788-471">Non</span><span class="sxs-lookup"><span data-stu-id="48788-471">No</span></span>|<span data-ttu-id="48788-472">Object</span><span class="sxs-lookup"><span data-stu-id="48788-472">Object</span></span>|<span data-ttu-id="48788-473">Représente la charge utile envoyée au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48788-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="48788-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="48788-474">retryPolicy</span></span>|<span data-ttu-id="48788-475">Non</span><span class="sxs-lookup"><span data-stu-id="48788-475">No</span></span>|<span data-ttu-id="48788-476">Object</span><span class="sxs-lookup"><span data-stu-id="48788-476">Object</span></span>|<span data-ttu-id="48788-477">Permet de personnaliser le comportement de nouvelle tentative pour les erreurs 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="48788-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="48788-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="48788-478">operationsOptions</span></span>|<span data-ttu-id="48788-479">Non</span><span class="sxs-lookup"><span data-stu-id="48788-479">No</span></span>|<span data-ttu-id="48788-480">String</span><span class="sxs-lookup"><span data-stu-id="48788-480">String</span></span>|<span data-ttu-id="48788-481">Définit l’ensemble de comportements spéciaux à substituer.</span><span class="sxs-lookup"><span data-stu-id="48788-481">Defines the set of special behaviors to override.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="48788-482">Action ApiConnectionWebhook</span><span class="sxs-lookup"><span data-stu-id="48788-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="48788-483">Les limites d’une action webhook peuvent être spécifiées de la même manière que les [limites asynchrones HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="48788-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="48788-484">Action de réponse</span><span class="sxs-lookup"><span data-stu-id="48788-484">Response action</span></span>  

<span data-ttu-id="48788-485">Ce type d’action contient la charge utile de réponse entière d’une requête HTTP et inclut des entrées statusCode, body et headers :</span><span class="sxs-lookup"><span data-stu-id="48788-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="48788-486">L’action response présente des restrictions spéciales qui ne s’appliquent pas aux autres actions.</span><span class="sxs-lookup"><span data-stu-id="48788-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="48788-487">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="48788-487">Specifically:</span></span>  
  
-   <span data-ttu-id="48788-488">Les actions response ne peuvent pas être parallèles dans une définition, car une réponse déterministe à la requête entrante est requise.</span><span class="sxs-lookup"><span data-stu-id="48788-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="48788-489">Si une action response est atteinte après que la requête entrante a reçu une réponse, l’action est considérée comme ayant échoué \(conflict\) (conflit), et par conséquent, l’exécution est définie sur `Failed` (Échec).</span><span class="sxs-lookup"><span data-stu-id="48788-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="48788-490">Un workflow comportant des actions response ne peut pas avoir `splitOn` dans son déclencheur, car un seul appel entraîne de nombreuses exécutions.</span><span class="sxs-lookup"><span data-stu-id="48788-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="48788-491">Par conséquent, une validation est requise lorsque le flux est PUT et cause une requête incorrecte.</span><span class="sxs-lookup"><span data-stu-id="48788-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="48788-492">Action wait</span><span class="sxs-lookup"><span data-stu-id="48788-492">Wait action</span></span>  

<span data-ttu-id="48788-493">L’action `wait` interrompt l’exécution du workflow pendant l’intervalle spécifié.</span><span class="sxs-lookup"><span data-stu-id="48788-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="48788-494">Par exemple, pour définir une attente de 15 minutes, vous pouvez utiliser cet extrait de code :</span><span class="sxs-lookup"><span data-stu-id="48788-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="48788-495">Pour attendre jusqu’à un moment spécifique, vous pouvez utiliser cet exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="48788-496">La durée d’attente peut être spécifiée soit à l’aide de l’objet **interval**, soit à l’aide de l’objet **until**.</span><span class="sxs-lookup"><span data-stu-id="48788-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="48788-497">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-497">Name</span></span>|<span data-ttu-id="48788-498">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-498">Required</span></span>|<span data-ttu-id="48788-499">Type</span><span class="sxs-lookup"><span data-stu-id="48788-499">Type</span></span>|<span data-ttu-id="48788-500">Description</span><span class="sxs-lookup"><span data-stu-id="48788-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48788-501">interval</span><span class="sxs-lookup"><span data-stu-id="48788-501">interval</span></span>|<span data-ttu-id="48788-502">Non</span><span class="sxs-lookup"><span data-stu-id="48788-502">No</span></span>|<span data-ttu-id="48788-503">Object</span><span class="sxs-lookup"><span data-stu-id="48788-503">Object</span></span>|<span data-ttu-id="48788-504">Temps d’attente basé sur une durée.</span><span class="sxs-lookup"><span data-stu-id="48788-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="48788-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="48788-505">interval unit</span></span>|<span data-ttu-id="48788-506">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-506">Yes</span></span>|<span data-ttu-id="48788-507">String</span><span class="sxs-lookup"><span data-stu-id="48788-507">String</span></span>|<span data-ttu-id="48788-508">Un de ces intervalles : second (seconde), minute (minute), hour (heure), day (jour), week (semaine), month (mois), year (année).</span><span class="sxs-lookup"><span data-stu-id="48788-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="48788-509">interval count</span><span class="sxs-lookup"><span data-stu-id="48788-509">interval count</span></span>|<span data-ttu-id="48788-510">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-510">Yes</span></span>|<span data-ttu-id="48788-511">String</span><span class="sxs-lookup"><span data-stu-id="48788-511">String</span></span>|<span data-ttu-id="48788-512">Temps d’attente basé sur l’unité interne donnée.</span><span class="sxs-lookup"><span data-stu-id="48788-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="48788-513">until</span><span class="sxs-lookup"><span data-stu-id="48788-513">until</span></span>|<span data-ttu-id="48788-514">Non</span><span class="sxs-lookup"><span data-stu-id="48788-514">No</span></span>|<span data-ttu-id="48788-515">Object</span><span class="sxs-lookup"><span data-stu-id="48788-515">Object</span></span>|<span data-ttu-id="48788-516">Temps d’attente basé sur un moment spécifique.</span><span class="sxs-lookup"><span data-stu-id="48788-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="48788-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="48788-517">until timestamp</span></span>|<span data-ttu-id="48788-518">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-518">Yes</span></span>|<span data-ttu-id="48788-519">String</span><span class="sxs-lookup"><span data-stu-id="48788-519">String</span></span>|<span data-ttu-id="48788-520">Moment auquel l’attente expirera (exprimé en heure UTC).</span><span class="sxs-lookup"><span data-stu-id="48788-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="48788-521">Action de requête</span><span class="sxs-lookup"><span data-stu-id="48788-521">Query action</span></span>

<span data-ttu-id="48788-522">L’action `query` vous permet de filtrer un tableau en fonction d’une condition.</span><span class="sxs-lookup"><span data-stu-id="48788-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="48788-523">Par exemple, pour sélectionner des nombres supérieurs à 2, vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="48788-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="48788-524">La sortie de l’action `query` est un tableau qui contient les éléments du tableau d’entrée qui remplissent la condition.</span><span class="sxs-lookup"><span data-stu-id="48788-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="48788-525">Si aucune valeur ne remplit la condition `where`, le résultat est un tableau vide.</span><span class="sxs-lookup"><span data-stu-id="48788-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="48788-526">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-526">Name</span></span>|<span data-ttu-id="48788-527">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-527">Required</span></span>|<span data-ttu-id="48788-528">Type</span><span class="sxs-lookup"><span data-stu-id="48788-528">Type</span></span>|<span data-ttu-id="48788-529">Description</span><span class="sxs-lookup"><span data-stu-id="48788-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="48788-530">from</span><span class="sxs-lookup"><span data-stu-id="48788-530">from</span></span>|<span data-ttu-id="48788-531">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-531">Yes</span></span>|<span data-ttu-id="48788-532">Tableau</span><span class="sxs-lookup"><span data-stu-id="48788-532">Array</span></span>|<span data-ttu-id="48788-533">Tableau source.</span><span class="sxs-lookup"><span data-stu-id="48788-533">The source array.</span></span>|
|<span data-ttu-id="48788-534">where</span><span class="sxs-lookup"><span data-stu-id="48788-534">where</span></span>|<span data-ttu-id="48788-535">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-535">Yes</span></span>|<span data-ttu-id="48788-536">String</span><span class="sxs-lookup"><span data-stu-id="48788-536">String</span></span>|<span data-ttu-id="48788-537">Condition à appliquer à chaque élément du tableau source.</span><span class="sxs-lookup"><span data-stu-id="48788-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="48788-538">Action select</span><span class="sxs-lookup"><span data-stu-id="48788-538">Select action</span></span>

<span data-ttu-id="48788-539">L’action `select` permet de projeter chaque élément d’un tableau dans une nouvelle valeur.</span><span class="sxs-lookup"><span data-stu-id="48788-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="48788-540">Par exemple, pour convertir un tableau de nombres en tableau d’objets, vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="48788-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="48788-541">La sortie de l’action `select` est un tableau présentant la même cardinalité que le tableau d’entrée, chaque élément étant transformé comme défini par la propriété `select`.</span><span class="sxs-lookup"><span data-stu-id="48788-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="48788-542">Si l’entrée est un tableau vide, la sortie est également un tableau vide.</span><span class="sxs-lookup"><span data-stu-id="48788-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="48788-543">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-543">Name</span></span>|<span data-ttu-id="48788-544">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-544">Required</span></span>|<span data-ttu-id="48788-545">Type</span><span class="sxs-lookup"><span data-stu-id="48788-545">Type</span></span>|<span data-ttu-id="48788-546">Description</span><span class="sxs-lookup"><span data-stu-id="48788-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="48788-547">from</span><span class="sxs-lookup"><span data-stu-id="48788-547">from</span></span>|<span data-ttu-id="48788-548">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-548">Yes</span></span>|<span data-ttu-id="48788-549">Tableau</span><span class="sxs-lookup"><span data-stu-id="48788-549">Array</span></span>|<span data-ttu-id="48788-550">Tableau source.</span><span class="sxs-lookup"><span data-stu-id="48788-550">The source array.</span></span>|
|<span data-ttu-id="48788-551">select</span><span class="sxs-lookup"><span data-stu-id="48788-551">select</span></span>|<span data-ttu-id="48788-552">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-552">Yes</span></span>|<span data-ttu-id="48788-553">Quelconque</span><span class="sxs-lookup"><span data-stu-id="48788-553">Any</span></span>|<span data-ttu-id="48788-554">Projection à appliquer à chaque élément du tableau source.</span><span class="sxs-lookup"><span data-stu-id="48788-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="48788-555">Action terminate</span><span class="sxs-lookup"><span data-stu-id="48788-555">Terminate action</span></span>

<span data-ttu-id="48788-556">L’action terminate met fin à l’exécution de l’exécution du workflow, abandonnant les actions en cours et ignorant les actions restantes.</span><span class="sxs-lookup"><span data-stu-id="48788-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="48788-557">Par exemple, pour mettre fin à une exécution qui présente l’état **Failed** (Échec), vous pouvez utiliser l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="48788-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="48788-558">Les actions déjà terminées ne sont pas affectées par l’action terminate.</span><span class="sxs-lookup"><span data-stu-id="48788-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="48788-559">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-559">Name</span></span>|<span data-ttu-id="48788-560">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-560">Required</span></span>|<span data-ttu-id="48788-561">Type</span><span class="sxs-lookup"><span data-stu-id="48788-561">Type</span></span>|<span data-ttu-id="48788-562">Description</span><span class="sxs-lookup"><span data-stu-id="48788-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="48788-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="48788-563">runStatus</span></span>|<span data-ttu-id="48788-564">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-564">Yes</span></span>|<span data-ttu-id="48788-565">String</span><span class="sxs-lookup"><span data-stu-id="48788-565">String</span></span>|<span data-ttu-id="48788-566">État d’exécution cible.</span><span class="sxs-lookup"><span data-stu-id="48788-566">The target run status.</span></span> <span data-ttu-id="48788-567">Peut être défini sur **Failed** (Échec) ou **Cancelled** (Annulée).</span><span class="sxs-lookup"><span data-stu-id="48788-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="48788-568">runError</span><span class="sxs-lookup"><span data-stu-id="48788-568">runError</span></span>|<span data-ttu-id="48788-569">Non</span><span class="sxs-lookup"><span data-stu-id="48788-569">No</span></span>|<span data-ttu-id="48788-570">Object</span><span class="sxs-lookup"><span data-stu-id="48788-570">Object</span></span>|<span data-ttu-id="48788-571">Détails de l’erreur.</span><span class="sxs-lookup"><span data-stu-id="48788-571">The error details.</span></span> <span data-ttu-id="48788-572">Uniquement pris en charge lorsque **runStatus** est défini sur **Failed** (Échec).</span><span class="sxs-lookup"><span data-stu-id="48788-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="48788-573">runError code</span><span class="sxs-lookup"><span data-stu-id="48788-573">runError code</span></span>|<span data-ttu-id="48788-574">Non</span><span class="sxs-lookup"><span data-stu-id="48788-574">No</span></span>|<span data-ttu-id="48788-575">String</span><span class="sxs-lookup"><span data-stu-id="48788-575">String</span></span>|<span data-ttu-id="48788-576">Code d’erreur de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="48788-576">The run error code.</span></span>|
|<span data-ttu-id="48788-577">runError message</span><span class="sxs-lookup"><span data-stu-id="48788-577">runError message</span></span>|<span data-ttu-id="48788-578">Non</span><span class="sxs-lookup"><span data-stu-id="48788-578">No</span></span>|<span data-ttu-id="48788-579">String</span><span class="sxs-lookup"><span data-stu-id="48788-579">String</span></span>|<span data-ttu-id="48788-580">Message d’erreur de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="48788-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="48788-581">Action compose</span><span class="sxs-lookup"><span data-stu-id="48788-581">Compose action</span></span>

<span data-ttu-id="48788-582">L’action compose vous permet de construire un objet arbitraire.</span><span class="sxs-lookup"><span data-stu-id="48788-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="48788-583">La sortie de l’action compose est le résultat de l’évaluation de ses entrées.</span><span class="sxs-lookup"><span data-stu-id="48788-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="48788-584">Par exemple, vous pouvez utiliser l’action compose pour fusionner les sorties de plusieurs actions :</span><span class="sxs-lookup"><span data-stu-id="48788-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="48788-585">L’action **compose** peut être utilisée pour construire n’importe quelle sortie, y compris des objets, des tableaux et tout autre type pris en charge de façon native par les applications logiques, tel que XML et binaire.</span><span class="sxs-lookup"><span data-stu-id="48788-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="48788-586">Action table</span><span class="sxs-lookup"><span data-stu-id="48788-586">Table action</span></span>

<span data-ttu-id="48788-587">L’action `table` permet de convertir un tableau d’éléments en table **CSV** ou **HTML**.</span><span class="sxs-lookup"><span data-stu-id="48788-587">The `table` allows you to convert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="48788-588">Supposons que @triggerBody() est</span><span class="sxs-lookup"><span data-stu-id="48788-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="48788-589">Et que l’action est définie comme étant</span><span class="sxs-lookup"><span data-stu-id="48788-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="48788-590">Les éléments ci-dessus produisent le résultat</span><span class="sxs-lookup"><span data-stu-id="48788-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="48788-591">id</span><span class="sxs-lookup"><span data-stu-id="48788-591">id</span></span></th><th><span data-ttu-id="48788-592">name</span><span class="sxs-lookup"><span data-stu-id="48788-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="48788-593">0</span><span class="sxs-lookup"><span data-stu-id="48788-593">0</span></span></td><td><span data-ttu-id="48788-594">pommes</span><span class="sxs-lookup"><span data-stu-id="48788-594">apples</span></span></td></tr><tr><td><span data-ttu-id="48788-595">1</span><span class="sxs-lookup"><span data-stu-id="48788-595">1</span></span></td><td><span data-ttu-id="48788-596">oranges</span><span class="sxs-lookup"><span data-stu-id="48788-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="48788-597">"</span><span class="sxs-lookup"><span data-stu-id="48788-597">"</span></span>

<span data-ttu-id="48788-598">Afin de personnaliser le tableau, vous pouvez spécifier explicitement les colonnes.</span><span class="sxs-lookup"><span data-stu-id="48788-598">In order to customize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="48788-599">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="48788-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="48788-600">Les éléments ci-dessus produisent le résultat</span><span class="sxs-lookup"><span data-stu-id="48788-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="48788-601">produce id</span><span class="sxs-lookup"><span data-stu-id="48788-601">produce id</span></span></th><th><span data-ttu-id="48788-602">Description</span><span class="sxs-lookup"><span data-stu-id="48788-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="48788-603">0</span><span class="sxs-lookup"><span data-stu-id="48788-603">0</span></span></td><td><span data-ttu-id="48788-604">pommes fraîches</span><span class="sxs-lookup"><span data-stu-id="48788-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="48788-605">1</span><span class="sxs-lookup"><span data-stu-id="48788-605">1</span></span></td><td><span data-ttu-id="48788-606">oranges fraîches</span><span class="sxs-lookup"><span data-stu-id="48788-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="48788-607">"</span><span class="sxs-lookup"><span data-stu-id="48788-607">"</span></span>

<span data-ttu-id="48788-608">Si la valeur de propriété `from` est un tableau vide, la sortie est un tableau vide.</span><span class="sxs-lookup"><span data-stu-id="48788-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="48788-609">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-609">Name</span></span>|<span data-ttu-id="48788-610">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-610">Required</span></span>|<span data-ttu-id="48788-611">Type</span><span class="sxs-lookup"><span data-stu-id="48788-611">Type</span></span>|<span data-ttu-id="48788-612">Description</span><span class="sxs-lookup"><span data-stu-id="48788-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="48788-613">from</span><span class="sxs-lookup"><span data-stu-id="48788-613">from</span></span>|<span data-ttu-id="48788-614">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-614">Yes</span></span>|<span data-ttu-id="48788-615">Tableau</span><span class="sxs-lookup"><span data-stu-id="48788-615">Array</span></span>|<span data-ttu-id="48788-616">Tableau source.</span><span class="sxs-lookup"><span data-stu-id="48788-616">The source array.</span></span>|
|<span data-ttu-id="48788-617">format</span><span class="sxs-lookup"><span data-stu-id="48788-617">format</span></span>|<span data-ttu-id="48788-618">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-618">Yes</span></span>|<span data-ttu-id="48788-619">String</span><span class="sxs-lookup"><span data-stu-id="48788-619">String</span></span>|<span data-ttu-id="48788-620">Le format, soit **CSV** ou **HTML**.</span><span class="sxs-lookup"><span data-stu-id="48788-620">The format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="48788-621">colonnes</span><span class="sxs-lookup"><span data-stu-id="48788-621">columns</span></span>|<span data-ttu-id="48788-622">Non</span><span class="sxs-lookup"><span data-stu-id="48788-622">No</span></span>|<span data-ttu-id="48788-623">Tableau</span><span class="sxs-lookup"><span data-stu-id="48788-623">Array</span></span>|<span data-ttu-id="48788-624">Les colonnes.</span><span class="sxs-lookup"><span data-stu-id="48788-624">The columns.</span></span> <span data-ttu-id="48788-625">Permet de remplacer la forme par défaut de la table.</span><span class="sxs-lookup"><span data-stu-id="48788-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="48788-626">column header</span><span class="sxs-lookup"><span data-stu-id="48788-626">column header</span></span>|<span data-ttu-id="48788-627">Non</span><span class="sxs-lookup"><span data-stu-id="48788-627">No</span></span>|<span data-ttu-id="48788-628">String</span><span class="sxs-lookup"><span data-stu-id="48788-628">String</span></span>|<span data-ttu-id="48788-629">En-tête de la colonne.</span><span class="sxs-lookup"><span data-stu-id="48788-629">The header of the column.</span></span>|
|<span data-ttu-id="48788-630">column value</span><span class="sxs-lookup"><span data-stu-id="48788-630">column value</span></span>|<span data-ttu-id="48788-631">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-631">Yes</span></span>|<span data-ttu-id="48788-632">Chaîne</span><span class="sxs-lookup"><span data-stu-id="48788-632">String</span></span>|<span data-ttu-id="48788-633">Valeur de la colonne.</span><span class="sxs-lookup"><span data-stu-id="48788-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="48788-634">Action workflow</span><span class="sxs-lookup"><span data-stu-id="48788-634">Workflow action</span></span>   

|<span data-ttu-id="48788-635">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-635">Name</span></span>|<span data-ttu-id="48788-636">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-636">Required</span></span>|<span data-ttu-id="48788-637">Type</span><span class="sxs-lookup"><span data-stu-id="48788-637">Type</span></span>|<span data-ttu-id="48788-638">Description</span><span class="sxs-lookup"><span data-stu-id="48788-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48788-639">host id</span><span class="sxs-lookup"><span data-stu-id="48788-639">host id</span></span>|<span data-ttu-id="48788-640">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-640">Yes</span></span>|<span data-ttu-id="48788-641">String</span><span class="sxs-lookup"><span data-stu-id="48788-641">String</span></span>|<span data-ttu-id="48788-642">ID de ressource du workflow que vous souhaitez appeler.</span><span class="sxs-lookup"><span data-stu-id="48788-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="48788-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="48788-643">host triggerName</span></span>|<span data-ttu-id="48788-644">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-644">Yes</span></span>|<span data-ttu-id="48788-645">String</span><span class="sxs-lookup"><span data-stu-id="48788-645">String</span></span>|<span data-ttu-id="48788-646">Nom du déclencheur que vous souhaitez appeler.</span><span class="sxs-lookup"><span data-stu-id="48788-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="48788-647">queries</span><span class="sxs-lookup"><span data-stu-id="48788-647">queries</span></span>|<span data-ttu-id="48788-648">Non</span><span class="sxs-lookup"><span data-stu-id="48788-648">No</span></span>|<span data-ttu-id="48788-649">Object</span><span class="sxs-lookup"><span data-stu-id="48788-649">Object</span></span>|<span data-ttu-id="48788-650">Représente les paramètres de requête à ajouter à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="48788-651">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48788-652">headers</span><span class="sxs-lookup"><span data-stu-id="48788-652">headers</span></span>|<span data-ttu-id="48788-653">Non</span><span class="sxs-lookup"><span data-stu-id="48788-653">No</span></span>|<span data-ttu-id="48788-654">Object</span><span class="sxs-lookup"><span data-stu-id="48788-654">Object</span></span>|<span data-ttu-id="48788-655">Représente chacun des en-têtes envoyés à la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48788-656">Par exemple, pour définir la langue et le type sur une requête :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="48788-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="48788-657">body</span><span class="sxs-lookup"><span data-stu-id="48788-657">body</span></span>|<span data-ttu-id="48788-658">Non</span><span class="sxs-lookup"><span data-stu-id="48788-658">No</span></span>|<span data-ttu-id="48788-659">Object</span><span class="sxs-lookup"><span data-stu-id="48788-659">Object</span></span>|<span data-ttu-id="48788-660">Représente la charge utile envoyée au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48788-660">Represents the payload sent to the endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="48788-661">Un contrôle d’accès est effectué sur le workflow \(plus précisément, sur le déclencheur\), ce qui signifie que vous avez besoin d’un accès au workflow.</span><span class="sxs-lookup"><span data-stu-id="48788-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="48788-662">Les sorties de l’action `workflow` sont basées sur ce que vous avez défini pour l’action `response` dans le workflow enfant.</span><span class="sxs-lookup"><span data-stu-id="48788-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="48788-663">Si vous n’avez pas défini d’action `response`, les sorties sont vides.</span><span class="sxs-lookup"><span data-stu-id="48788-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="48788-664">Action function</span><span class="sxs-lookup"><span data-stu-id="48788-664">Function action</span></span>   

|<span data-ttu-id="48788-665">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-665">Name</span></span>|<span data-ttu-id="48788-666">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-666">Required</span></span>|<span data-ttu-id="48788-667">Type</span><span class="sxs-lookup"><span data-stu-id="48788-667">Type</span></span>|<span data-ttu-id="48788-668">Description</span><span class="sxs-lookup"><span data-stu-id="48788-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48788-669">function id</span><span class="sxs-lookup"><span data-stu-id="48788-669">function id</span></span>|<span data-ttu-id="48788-670">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-670">Yes</span></span>|<span data-ttu-id="48788-671">String</span><span class="sxs-lookup"><span data-stu-id="48788-671">String</span></span>|<span data-ttu-id="48788-672">ID de ressource de la fonction que vous souhaitez appeler.</span><span class="sxs-lookup"><span data-stu-id="48788-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="48788-673">method</span><span class="sxs-lookup"><span data-stu-id="48788-673">method</span></span>|<span data-ttu-id="48788-674">Non</span><span class="sxs-lookup"><span data-stu-id="48788-674">No</span></span>|<span data-ttu-id="48788-675">String</span><span class="sxs-lookup"><span data-stu-id="48788-675">String</span></span>|<span data-ttu-id="48788-676">Méthode HTTP utilisée pour appeler la fonction.</span><span class="sxs-lookup"><span data-stu-id="48788-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="48788-677">Par défaut, a la valeur `POST` lorsqu’elle n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="48788-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="48788-678">queries</span><span class="sxs-lookup"><span data-stu-id="48788-678">queries</span></span>|<span data-ttu-id="48788-679">Non</span><span class="sxs-lookup"><span data-stu-id="48788-679">No</span></span>|<span data-ttu-id="48788-680">Object</span><span class="sxs-lookup"><span data-stu-id="48788-680">Object</span></span>|<span data-ttu-id="48788-681">Représente les paramètres de requête à ajouter à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="48788-682">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` à l’URL.</span><span class="sxs-lookup"><span data-stu-id="48788-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="48788-683">headers</span><span class="sxs-lookup"><span data-stu-id="48788-683">headers</span></span>|<span data-ttu-id="48788-684">Non</span><span class="sxs-lookup"><span data-stu-id="48788-684">No</span></span>|<span data-ttu-id="48788-685">Object</span><span class="sxs-lookup"><span data-stu-id="48788-685">Object</span></span>|<span data-ttu-id="48788-686">Représente chacun des en-têtes envoyés à la requête.</span><span class="sxs-lookup"><span data-stu-id="48788-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="48788-687">Par exemple, pour définir la langue et le type sur une requête : `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="48788-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="48788-688">body</span><span class="sxs-lookup"><span data-stu-id="48788-688">body</span></span>|<span data-ttu-id="48788-689">Non</span><span class="sxs-lookup"><span data-stu-id="48788-689">No</span></span>|<span data-ttu-id="48788-690">Object</span><span class="sxs-lookup"><span data-stu-id="48788-690">Object</span></span>|<span data-ttu-id="48788-691">Représente la charge utile envoyée au point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48788-691">Represents the payload sent to the endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="48788-692">Lorsque vous enregistrez l’application logique, certaines vérifications sont effectuées sur la fonction référencée :</span><span class="sxs-lookup"><span data-stu-id="48788-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="48788-693">Vous devez avoir accès à la fonction.</span><span class="sxs-lookup"><span data-stu-id="48788-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="48788-694">Seuls le déclencheur HTTP standard ou un déclencheur webhook JSON générique sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="48788-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="48788-695">Aucune route ne doit être définie.</span><span class="sxs-lookup"><span data-stu-id="48788-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="48788-696">Seuls les niveaux d’autorisation « fonction » et « anonyme » sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="48788-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="48788-697">L’URL du déclencheur est récupéré, mis en cache et utilisé au runtime.</span><span class="sxs-lookup"><span data-stu-id="48788-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="48788-698">Par conséquent, si une opération invalide l’URL en cache, l’action échoue au runtime.</span><span class="sxs-lookup"><span data-stu-id="48788-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="48788-699">Pour contourner ce problème, enregistrez de nouveau l’application logique pour que l’application logique puisse de nouveau récupérer et mettre en cache l’URL du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="48788-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="48788-700">Actions de collection (étendues et boucles)</span><span class="sxs-lookup"><span data-stu-id="48788-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="48788-701">Certains types d’actions peuvent contenir d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="48788-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="48788-702">Il est possible de faire référence aux actions d’une collection directement en dehors de la collection.</span><span class="sxs-lookup"><span data-stu-id="48788-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="48788-703">Si vous avez défini `http` dans une étendue (scope), `@body('http')` est toujours valide n’importe où dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="48788-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="48788-704">Les actions d’une collection peuvent uniquement être exécutées après (avec la propriété `runAfter`) les actions de la même collection.</span><span class="sxs-lookup"><span data-stu-id="48788-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="48788-705">Action scope</span><span class="sxs-lookup"><span data-stu-id="48788-705">Scope action</span></span>

<span data-ttu-id="48788-706">L’action `scope` vous permet de logiquement regrouper les actions d’un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="48788-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="48788-707">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-707">Name</span></span>|<span data-ttu-id="48788-708">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-708">Required</span></span>|<span data-ttu-id="48788-709">Type</span><span class="sxs-lookup"><span data-stu-id="48788-709">Type</span></span>|<span data-ttu-id="48788-710">Description</span><span class="sxs-lookup"><span data-stu-id="48788-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48788-711">actions</span><span class="sxs-lookup"><span data-stu-id="48788-711">actions</span></span>|<span data-ttu-id="48788-712">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-712">Yes</span></span>|<span data-ttu-id="48788-713">Object</span><span class="sxs-lookup"><span data-stu-id="48788-713">Object</span></span>|<span data-ttu-id="48788-714">Actions internes à exécuter dans l’étendue.</span><span class="sxs-lookup"><span data-stu-id="48788-714">Inner actions to execute within the scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="48788-715">Action foreach</span><span class="sxs-lookup"><span data-stu-id="48788-715">ForEach action</span></span>

<span data-ttu-id="48788-716">Cette action en boucle effectue une itération dans un tableau et exécute des actions internes pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="48788-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="48788-717">Par défaut, la boucle foreach exécute les itérations en parallèle (20 exécutions en parallèle à la fois).</span><span class="sxs-lookup"><span data-stu-id="48788-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="48788-718">Vous pouvez définir les règles d’exécution à l’aide du paramètre `operationOptions`.</span><span class="sxs-lookup"><span data-stu-id="48788-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="48788-719">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-719">Name</span></span>|<span data-ttu-id="48788-720">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-720">Required</span></span>|<span data-ttu-id="48788-721">Type</span><span class="sxs-lookup"><span data-stu-id="48788-721">Type</span></span>|<span data-ttu-id="48788-722">Description</span><span class="sxs-lookup"><span data-stu-id="48788-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48788-723">actions</span><span class="sxs-lookup"><span data-stu-id="48788-723">actions</span></span>|<span data-ttu-id="48788-724">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-724">Yes</span></span>|<span data-ttu-id="48788-725">Object</span><span class="sxs-lookup"><span data-stu-id="48788-725">Object</span></span>|<span data-ttu-id="48788-726">Actions internes à exécuter dans la boucle.</span><span class="sxs-lookup"><span data-stu-id="48788-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="48788-727">foreach</span><span class="sxs-lookup"><span data-stu-id="48788-727">foreach</span></span>|<span data-ttu-id="48788-728">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-728">Yes</span></span>|<span data-ttu-id="48788-729">string</span><span class="sxs-lookup"><span data-stu-id="48788-729">string</span></span>|<span data-ttu-id="48788-730">Tableau dans lequel effectuer l’itération.</span><span class="sxs-lookup"><span data-stu-id="48788-730">The array to iterate over</span></span>|
|<span data-ttu-id="48788-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="48788-731">operationOptions</span></span>|<span data-ttu-id="48788-732">no</span><span class="sxs-lookup"><span data-stu-id="48788-732">no</span></span>|<span data-ttu-id="48788-733">string</span><span class="sxs-lookup"><span data-stu-id="48788-733">string</span></span>|<span data-ttu-id="48788-734">Toutes les options d’opération pour le comportement.</span><span class="sxs-lookup"><span data-stu-id="48788-734">Any operation options for behavior.</span></span> <span data-ttu-id="48788-735">Pour le moment, prend uniquement en charge `sequential` pour exécuter les itérations de manière séquentielle (le comportement par défaut est parallèle)</span><span class="sxs-lookup"><span data-stu-id="48788-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="48788-736">Action until</span><span class="sxs-lookup"><span data-stu-id="48788-736">Until action</span></span>

<span data-ttu-id="48788-737">Cette action en boucle exécute des actions internes jusqu’à ce qu’une condition soit vérifiée.</span><span class="sxs-lookup"><span data-stu-id="48788-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="48788-738">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-738">Name</span></span>|<span data-ttu-id="48788-739">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-739">Required</span></span>|<span data-ttu-id="48788-740">Type</span><span class="sxs-lookup"><span data-stu-id="48788-740">Type</span></span>|<span data-ttu-id="48788-741">Description</span><span class="sxs-lookup"><span data-stu-id="48788-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48788-742">actions</span><span class="sxs-lookup"><span data-stu-id="48788-742">actions</span></span>|<span data-ttu-id="48788-743">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-743">Yes</span></span>|<span data-ttu-id="48788-744">Object</span><span class="sxs-lookup"><span data-stu-id="48788-744">Object</span></span>|<span data-ttu-id="48788-745">Actions internes à exécuter dans la boucle.</span><span class="sxs-lookup"><span data-stu-id="48788-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="48788-746">expression</span><span class="sxs-lookup"><span data-stu-id="48788-746">expression</span></span>|<span data-ttu-id="48788-747">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-747">Yes</span></span>|<span data-ttu-id="48788-748">string</span><span class="sxs-lookup"><span data-stu-id="48788-748">string</span></span>|<span data-ttu-id="48788-749">Expression à évaluer après chaque itération.</span><span class="sxs-lookup"><span data-stu-id="48788-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="48788-750">limit</span><span class="sxs-lookup"><span data-stu-id="48788-750">limit</span></span>|<span data-ttu-id="48788-751">yes</span><span class="sxs-lookup"><span data-stu-id="48788-751">yes</span></span>|<span data-ttu-id="48788-752">Object</span><span class="sxs-lookup"><span data-stu-id="48788-752">Object</span></span>|<span data-ttu-id="48788-753">Limites de la boucle (au moins une limite doit être définie).</span><span class="sxs-lookup"><span data-stu-id="48788-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="48788-754">count</span><span class="sxs-lookup"><span data-stu-id="48788-754">count</span></span>|<span data-ttu-id="48788-755">no</span><span class="sxs-lookup"><span data-stu-id="48788-755">no</span></span>|<span data-ttu-id="48788-756">int</span><span class="sxs-lookup"><span data-stu-id="48788-756">int</span></span>|<span data-ttu-id="48788-757">Nombre maximal d’itérations pouvant être exécutées.</span><span class="sxs-lookup"><span data-stu-id="48788-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="48788-758">timeout</span><span class="sxs-lookup"><span data-stu-id="48788-758">timeout</span></span>|<span data-ttu-id="48788-759">no</span><span class="sxs-lookup"><span data-stu-id="48788-759">no</span></span>|<span data-ttu-id="48788-760">string</span><span class="sxs-lookup"><span data-stu-id="48788-760">string</span></span>|<span data-ttu-id="48788-761">Délai d’expiration de la boucle.</span><span class="sxs-lookup"><span data-stu-id="48788-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="48788-762">Format ISO 8601</span><span class="sxs-lookup"><span data-stu-id="48788-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="48788-763">Conditions : action If</span><span class="sxs-lookup"><span data-stu-id="48788-763">Conditions - If Action</span></span>

<span data-ttu-id="48788-764">L’action `If` vous permet d’évaluer une condition et d’exécuter une branche spécifique si l’expression évaluée présente la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="48788-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="48788-765">Nom</span><span class="sxs-lookup"><span data-stu-id="48788-765">Name</span></span>|<span data-ttu-id="48788-766">Requis</span><span class="sxs-lookup"><span data-stu-id="48788-766">Required</span></span>|<span data-ttu-id="48788-767">Type</span><span class="sxs-lookup"><span data-stu-id="48788-767">Type</span></span>|<span data-ttu-id="48788-768">Description</span><span class="sxs-lookup"><span data-stu-id="48788-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="48788-769">actions</span><span class="sxs-lookup"><span data-stu-id="48788-769">actions</span></span>|<span data-ttu-id="48788-770">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-770">Yes</span></span>|<span data-ttu-id="48788-771">Object</span><span class="sxs-lookup"><span data-stu-id="48788-771">Object</span></span>|<span data-ttu-id="48788-772">Actions internes à exécuter lorsque l’expression évaluée présente la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="48788-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="48788-773">expression</span><span class="sxs-lookup"><span data-stu-id="48788-773">expression</span></span>|<span data-ttu-id="48788-774">Oui</span><span class="sxs-lookup"><span data-stu-id="48788-774">Yes</span></span>|<span data-ttu-id="48788-775">string</span><span class="sxs-lookup"><span data-stu-id="48788-775">string</span></span>|<span data-ttu-id="48788-776">Expression à évaluer.</span><span class="sxs-lookup"><span data-stu-id="48788-776">The expression to evaluate</span></span>|
|<span data-ttu-id="48788-777">else</span><span class="sxs-lookup"><span data-stu-id="48788-777">else</span></span>|<span data-ttu-id="48788-778">no</span><span class="sxs-lookup"><span data-stu-id="48788-778">no</span></span>|<span data-ttu-id="48788-779">Object</span><span class="sxs-lookup"><span data-stu-id="48788-779">Object</span></span>|<span data-ttu-id="48788-780">Actions internes à exécuter lorsque l’expression évaluée présente la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="48788-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="48788-781">Le tableau suivant montre comment les conditions peuvent utiliser des expressions dans une action à travers plusieurs exemples :</span><span class="sxs-lookup"><span data-stu-id="48788-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="48788-782">Valeur JSON</span><span class="sxs-lookup"><span data-stu-id="48788-782">JSON value</span></span>|<span data-ttu-id="48788-783">Résultat</span><span class="sxs-lookup"><span data-stu-id="48788-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="48788-784">Cette condition est remplie dès lors que l’expression évaluée présente la valeur true.</span><span class="sxs-lookup"><span data-stu-id="48788-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="48788-785">Seules les expressions booléennes sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="48788-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="48788-786">Pour convertir d’autres types en valeurs booléennes, utilisez les fonctions `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="48788-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="48788-787">Les fonctions de comparaison sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="48788-787">Comparison functions are supported.</span></span> <span data-ttu-id="48788-788">Pour cet exemple, l’action s’exécute uniquement lorsque la sortie d’act1 est supérieure au seuil.</span><span class="sxs-lookup"><span data-stu-id="48788-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="48788-789">Les fonctions logiques sont également prises en charge pour créer des expressions booléennes imbriquées.</span><span class="sxs-lookup"><span data-stu-id="48788-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="48788-790">Dans le cas présent, l’action s’exécute lorsque la sortie d’act1 est supérieure au seuil ou inférieure à 100.</span><span class="sxs-lookup"><span data-stu-id="48788-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="48788-791">Vous pouvez utiliser les fonctions de tableau pour vérifier si un tableau contient des éléments.</span><span class="sxs-lookup"><span data-stu-id="48788-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="48788-792">Dans le cas présent, l’action s’exécute lorsque le tableau d’erreurs est vide.</span><span class="sxs-lookup"><span data-stu-id="48788-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="48788-793">Erreur : cette condition n’est pas valide, car @ est requis pour les conditions.</span><span class="sxs-lookup"><span data-stu-id="48788-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="48788-794">Si une condition est évaluée avec succès, elle est marquée comme `Succeeded` (Réussite).</span><span class="sxs-lookup"><span data-stu-id="48788-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="48788-795">Les actions évaluées au sein des objets `actions` ou `else` présentent la valeur `Succeeded` (Réussite) lorsque leur exécution réussit, `Failed` (Échec) lorsque leur exécution échoue ou `Skipped` (Ignorée) lorsque cette branche n’est pas exécutée.</span><span class="sxs-lookup"><span data-stu-id="48788-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48788-796">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48788-796">Next steps</span></span>

[<span data-ttu-id="48788-797">API REST du service de workflow</span><span class="sxs-lookup"><span data-stu-id="48788-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
