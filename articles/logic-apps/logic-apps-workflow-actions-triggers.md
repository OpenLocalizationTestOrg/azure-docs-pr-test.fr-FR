---
title: "aaaWorkflow actions et les déclencheurs - Azure Logic Apps | Documents Microsoft"
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
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="45f1c-102">Actions et déclencheurs de workflow pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="45f1c-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="45f1c-103">Les applications logiques se composent de déclencheurs et d’actions.</span><span class="sxs-lookup"><span data-stu-id="45f1c-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="45f1c-104">Il existe six types de déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="45f1c-104">There are six types of triggers.</span></span> <span data-ttu-id="45f1c-105">Chaque type présente une interface et un comportement différents.</span><span class="sxs-lookup"><span data-stu-id="45f1c-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="45f1c-106">Vous pouvez également découvrir les autres détails en examinant les détails de hello Hello [langage de définition de flux de travail](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="45f1c-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="45f1c-107">Lisez la suite toolearn en savoir plus sur les déclencheurs et les actions et comment vous pouvez utiliser les toobuild logique applications tooimprove votre processus d’entreprise et le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="45f1c-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="45f1c-108">Déclencheurs</span><span class="sxs-lookup"><span data-stu-id="45f1c-108">Triggers</span></span>  

<span data-ttu-id="45f1c-109">Un déclencheur spécifie les appels hello autorisés à initier une exécution de votre flux de travail application logique.</span><span class="sxs-lookup"><span data-stu-id="45f1c-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="45f1c-110">Voici deux façons différentes de hello tooinitiate une exécution de votre flux de travail :</span><span class="sxs-lookup"><span data-stu-id="45f1c-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="45f1c-111">Un déclencheur d’interrogation</span><span class="sxs-lookup"><span data-stu-id="45f1c-111">A polling trigger</span></span>  

-   <span data-ttu-id="45f1c-112">Un déclencheur d’émission - en appelant hello [API REST de Service de flux de travail](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="45f1c-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="45f1c-113">Tous les déclencheurs contiennent ces éléments de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="45f1c-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="45f1c-114">Types de déclencheurs et entrées associées</span><span class="sxs-lookup"><span data-stu-id="45f1c-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="45f1c-115">Vous pouvez utiliser les types de déclencheurs suivants :</span><span class="sxs-lookup"><span data-stu-id="45f1c-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="45f1c-116">**Demande** \- rend application logique de hello un point de terminaison pour vous toocall</span><span class="sxs-lookup"><span data-stu-id="45f1c-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="45f1c-117">**Recurrence** \- Se déclenche selon une planification définie.</span><span class="sxs-lookup"><span data-stu-id="45f1c-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="45f1c-118">**HTTP**\- Interroge un point de terminaison web HTTP.</span><span class="sxs-lookup"><span data-stu-id="45f1c-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="45f1c-119">point de terminaison Hello HTTP doit respecter le contrat de déclenchement spécifique tooa \- à l’aide d’un message 202\-un modèle asynchrone, ou en retournant un tableau</span><span class="sxs-lookup"><span data-stu-id="45f1c-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="45f1c-120">**ApiConnection** \- interroge comme hello HTTP déclenche, toutefois, elle tire parti de hello [gérée par Microsoft des API](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="45f1c-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="45f1c-121">**HTTPWebhook** \- ouvre un point de terminaison, similaire toohello déclencheur manuel, toutefois, il appelle également out tooa spécifié URL tooregister et annuler l’inscription</span><span class="sxs-lookup"><span data-stu-id="45f1c-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="45f1c-122">**ApiConnectionWebhook** \- fonctionne comme hello HTTPWebhook déclencheur en tirant parti de hello gérée par Microsoft des API</span><span class="sxs-lookup"><span data-stu-id="45f1c-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="45f1c-123">Chaque type de déclencheur présente un ensemble différent d’**entrées** qui définissent son comportement.</span><span class="sxs-lookup"><span data-stu-id="45f1c-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="45f1c-124">Déclencheur de requête</span><span class="sxs-lookup"><span data-stu-id="45f1c-124">Request trigger</span></span>  

<span data-ttu-id="45f1c-125">Ce déclencheur sert un point de terminaison que vous appelez votre application logique via un tooinvoke de requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="45f1c-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="45f1c-126">Un déclencheur request se présente comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-126">A request trigger looks like this example:</span></span>  
  
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

<span data-ttu-id="45f1c-127">Il existe également une propriété facultative appelée **schema** :</span><span class="sxs-lookup"><span data-stu-id="45f1c-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="45f1c-128">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-128">Element name</span></span>|<span data-ttu-id="45f1c-129">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-129">Required</span></span>|<span data-ttu-id="45f1c-130">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="45f1c-131">schema</span><span class="sxs-lookup"><span data-stu-id="45f1c-131">schema</span></span>|<span data-ttu-id="45f1c-132">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-132">No</span></span>|<span data-ttu-id="45f1c-133">Un schéma JSON qui valide la demande entrante de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="45f1c-134">Utile pour aider les étapes du flux de travail suivant savoir quels tooreference de propriétés.</span><span class="sxs-lookup"><span data-stu-id="45f1c-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="45f1c-135">tooinvoke ce point de terminaison, vous devez toocall hello *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="45f1c-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="45f1c-136">Consultez [API REST du service de workflow](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="45f1c-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="45f1c-137">Déclencheur recurrence</span><span class="sxs-lookup"><span data-stu-id="45f1c-137">Recurrence trigger</span></span>  

<span data-ttu-id="45f1c-138">Un déclencheur recurrence s’exécute selon une planification définie.</span><span class="sxs-lookup"><span data-stu-id="45f1c-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="45f1c-139">Ce type de déclencheur peut se présenter comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="45f1c-140">Comme vous pouvez le voir, il s’agit d’un moyen simple de toorun un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="45f1c-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="45f1c-141">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-141">Element name</span></span>|<span data-ttu-id="45f1c-142">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-142">Required</span></span>|<span data-ttu-id="45f1c-143">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="45f1c-144">frequency</span><span class="sxs-lookup"><span data-stu-id="45f1c-144">frequency</span></span>|<span data-ttu-id="45f1c-145">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-145">Yes</span></span>|<span data-ttu-id="45f1c-146">La fréquence à laquelle hello déclencheur s’exécute.</span><span class="sxs-lookup"><span data-stu-id="45f1c-146">How often hello trigger executes.</span></span> <span data-ttu-id="45f1c-147">Utilisez une seule de ces valeurs possibles : second (seconde), minute, hour (heure), day (jour), week (semaine), month (mois) ou year (année).</span><span class="sxs-lookup"><span data-stu-id="45f1c-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="45f1c-148">interval</span><span class="sxs-lookup"><span data-stu-id="45f1c-148">interval</span></span>|<span data-ttu-id="45f1c-149">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-149">Yes</span></span>|<span data-ttu-id="45f1c-150">Intervalle de hello attribué à la fréquence de récurrence de hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="45f1c-151">startTime</span><span class="sxs-lookup"><span data-stu-id="45f1c-151">startTime</span></span>|<span data-ttu-id="45f1c-152">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-152">No</span></span>|<span data-ttu-id="45f1c-153">Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire (timeZone) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="45f1c-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="45f1c-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="45f1c-154">timeZone</span></span>|<span data-ttu-id="45f1c-155">no</span><span class="sxs-lookup"><span data-stu-id="45f1c-155">no</span></span>|<span data-ttu-id="45f1c-156">Si une heure de début (startTime) est spécifiée sans décalage UTC, ce fuseau horaire (timeZone) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="45f1c-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="45f1c-157">Vous pouvez également programmer le déclencheur toostart l’exécution à un moment donné dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="45f1c-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="45f1c-158">Par exemple, si vous souhaitez toostart hebdomadaire signaler tous les lundis vous pouvez planifier hello logique application toostart tous les lundis en créant hello suivant déclencheur :</span><span class="sxs-lookup"><span data-stu-id="45f1c-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

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

## <a name="http-trigger"></a><span data-ttu-id="45f1c-159">Déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="45f1c-159">HTTP trigger</span></span>  

<span data-ttu-id="45f1c-160">Les déclencheurs HTTP interrogent un point de terminaison spécifié et vérifiez hello réponse toodetermine si le flux de travail hello doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="45f1c-161">objet d’entrées Hello prend ensemble hello de tooconstruct de paramètres requis un appel HTTP :</span><span class="sxs-lookup"><span data-stu-id="45f1c-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="45f1c-162">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-162">Element name</span></span>|<span data-ttu-id="45f1c-163">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-163">Required</span></span>|<span data-ttu-id="45f1c-164">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-164">Description</span></span>|<span data-ttu-id="45f1c-165">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="45f1c-166">method</span><span class="sxs-lookup"><span data-stu-id="45f1c-166">method</span></span>|<span data-ttu-id="45f1c-167">yes</span><span class="sxs-lookup"><span data-stu-id="45f1c-167">yes</span></span>|<span data-ttu-id="45f1c-168">Peut s’agir de hello suivant les méthodes HTTP : GET, POST, PUT, HEAD, PATCH ou DELETE</span><span class="sxs-lookup"><span data-stu-id="45f1c-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="45f1c-169">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-169">String</span></span>|  
|<span data-ttu-id="45f1c-170">URI</span><span class="sxs-lookup"><span data-stu-id="45f1c-170">uri</span></span>|<span data-ttu-id="45f1c-171">yes</span><span class="sxs-lookup"><span data-stu-id="45f1c-171">yes</span></span>|<span data-ttu-id="45f1c-172">Bonjour le point de terminaison http ou https est appelé.</span><span class="sxs-lookup"><span data-stu-id="45f1c-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="45f1c-173">La longueur maximale est de 2 Ko.</span><span class="sxs-lookup"><span data-stu-id="45f1c-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="45f1c-174">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-174">String</span></span>|  
|<span data-ttu-id="45f1c-175">queries</span><span class="sxs-lookup"><span data-stu-id="45f1c-175">queries</span></span>|<span data-ttu-id="45f1c-176">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-176">No</span></span>|<span data-ttu-id="45f1c-177">Objet représentant l’URL toohello tooadd de paramètres de requête hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="45f1c-178">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="45f1c-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="45f1c-179">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-179">Object</span></span>|  
|<span data-ttu-id="45f1c-180">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-180">headers</span></span>|<span data-ttu-id="45f1c-181">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-181">No</span></span>|<span data-ttu-id="45f1c-182">Objet représentant chacun des en-tête de hello toohello demande est envoyée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="45f1c-183">Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="45f1c-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="45f1c-184">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-184">Object</span></span>|  
|<span data-ttu-id="45f1c-185">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-185">body</span></span>|<span data-ttu-id="45f1c-186">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-186">No</span></span>|<span data-ttu-id="45f1c-187">Objet représentant la charge utile hello envoyé toohello le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="45f1c-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="45f1c-188">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-188">Object</span></span>|  
|<span data-ttu-id="45f1c-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="45f1c-189">retryPolicy</span></span>|<span data-ttu-id="45f1c-190">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-190">No</span></span>|<span data-ttu-id="45f1c-191">Objet qui vous permet de personnaliser le comportement des nouvelles tentatives hello pour les erreurs 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="45f1c-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="45f1c-192">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-192">Object</span></span>|  
|<span data-ttu-id="45f1c-193">authentication</span><span class="sxs-lookup"><span data-stu-id="45f1c-193">authentication</span></span>|<span data-ttu-id="45f1c-194">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-194">No</span></span>|<span data-ttu-id="45f1c-195">Méthode hello représente hello demande doit être authentifié.</span><span class="sxs-lookup"><span data-stu-id="45f1c-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="45f1c-196">Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="45f1c-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="45f1c-197">En plus de Scheduler, une autre propriété est prise en charge : `authority`. Par défaut, cette propriété est définie sur `https://login.windows.net` lorsqu’aucune valeur n’est spécifiée, mais vous pouvez utiliser une autre audience comme `https://login.windows\-ppe.net`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="45f1c-198">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-198">Object</span></span>|  
  
<span data-ttu-id="45f1c-199">déclencheur HTTP Hello nécessite tooconform d’API HTTP hello avec un toowork de modèle spécifique avec votre application logique.</span><span class="sxs-lookup"><span data-stu-id="45f1c-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="45f1c-200">Il requiert hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="45f1c-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="45f1c-201">Réponse</span><span class="sxs-lookup"><span data-stu-id="45f1c-201">Response</span></span>|<span data-ttu-id="45f1c-202">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="45f1c-203">Code d’état</span><span class="sxs-lookup"><span data-stu-id="45f1c-203">Status code</span></span>|<span data-ttu-id="45f1c-204">Code d’état 200 \(OK\) toocause une série de tests.</span><span class="sxs-lookup"><span data-stu-id="45f1c-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="45f1c-205">Les autres codes d’état ne déclenchent pas d’exécution.</span><span class="sxs-lookup"><span data-stu-id="45f1c-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="45f1c-206">En-tête Retry\-After</span><span class="sxs-lookup"><span data-stu-id="45f1c-206">Retry\-after header</span></span>|<span data-ttu-id="45f1c-207">Nombre de secondes jusqu'à ce que l’application logique de hello interroge le point de terminaison hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="45f1c-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="45f1c-208">En-tête Location</span><span class="sxs-lookup"><span data-stu-id="45f1c-208">Location header</span></span>|<span data-ttu-id="45f1c-209">Bonjour toocall d’URL sur le prochain intervalle d’interrogation de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="45f1c-210">Si non spécifié, l’URL d’origine de hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="45f1c-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="45f1c-211">Voici quelques exemples de comportements différents pour les différents types de requêtes :</span><span class="sxs-lookup"><span data-stu-id="45f1c-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="45f1c-212">Response code</span><span class="sxs-lookup"><span data-stu-id="45f1c-212">Response code</span></span>|<span data-ttu-id="45f1c-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="45f1c-213">Retry\-After</span></span>|<span data-ttu-id="45f1c-214">Comportement</span><span class="sxs-lookup"><span data-stu-id="45f1c-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="45f1c-215">200</span><span class="sxs-lookup"><span data-stu-id="45f1c-215">200</span></span>|<span data-ttu-id="45f1c-216">\(Aucune\)</span><span class="sxs-lookup"><span data-stu-id="45f1c-216">\(none\)</span></span>|<span data-ttu-id="45f1c-217">N’est pas un déclencheur valid, nouvelle tentative\-After est moteur de hello requis, ou bien jamais interroge la prochaine demande de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="45f1c-218">202</span><span class="sxs-lookup"><span data-stu-id="45f1c-218">202</span></span>|<span data-ttu-id="45f1c-219">60</span><span class="sxs-lookup"><span data-stu-id="45f1c-219">60</span></span>|<span data-ttu-id="45f1c-220">Ne déclenchent pas de flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="45f1c-221">tentative de Hello suivante se produit dans une minute.</span><span class="sxs-lookup"><span data-stu-id="45f1c-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="45f1c-222">200</span><span class="sxs-lookup"><span data-stu-id="45f1c-222">200</span></span>|<span data-ttu-id="45f1c-223">10</span><span class="sxs-lookup"><span data-stu-id="45f1c-223">10</span></span>|<span data-ttu-id="45f1c-224">Exécuter les flux de travail hello et vérifiez de nouveau pour le contenu de plus de 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="45f1c-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="45f1c-225">400</span><span class="sxs-lookup"><span data-stu-id="45f1c-225">400</span></span>|<span data-ttu-id="45f1c-226">\(Aucune\)</span><span class="sxs-lookup"><span data-stu-id="45f1c-226">\(none\)</span></span>|<span data-ttu-id="45f1c-227">Demande incorrecte, ne pas exécuter les flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="45f1c-228">S’il existe aucune **stratégie de nouvelle tentative** défini, la stratégie par défaut de hello est utilisée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="45f1c-229">Une fois le nombre de hello de tentatives a été atteint, le déclencheur de hello n’est plus valide.</span><span class="sxs-lookup"><span data-stu-id="45f1c-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="45f1c-230">500</span><span class="sxs-lookup"><span data-stu-id="45f1c-230">500</span></span>|<span data-ttu-id="45f1c-231">\(Aucune\)</span><span class="sxs-lookup"><span data-stu-id="45f1c-231">\(none\)</span></span>|<span data-ttu-id="45f1c-232">Erreur de serveur, n’exécutez ne pas le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="45f1c-233">S’il existe aucune **stratégie de nouvelle tentative** défini, la stratégie par défaut de hello est utilisée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="45f1c-234">Une fois le nombre de hello de tentatives a été atteint, le déclencheur de hello n’est plus valide.</span><span class="sxs-lookup"><span data-stu-id="45f1c-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="45f1c-235">sorties Hello d’un déclencheur HTTP ressemblent à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="45f1c-236">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-236">Element name</span></span>|<span data-ttu-id="45f1c-237">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-237">Description</span></span>|<span data-ttu-id="45f1c-238">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="45f1c-239">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-239">headers</span></span>|<span data-ttu-id="45f1c-240">en-têtes de réponse http de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-240">hello headers of hello http response.</span></span>|<span data-ttu-id="45f1c-241">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-241">Object</span></span>|  
|<span data-ttu-id="45f1c-242">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-242">body</span></span>|<span data-ttu-id="45f1c-243">corps de réponse http de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-243">hello body of hello http response.</span></span>|<span data-ttu-id="45f1c-244">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="45f1c-245">Déclencheur ApiConnection</span><span class="sxs-lookup"><span data-stu-id="45f1c-245">API Connection trigger</span></span>  

<span data-ttu-id="45f1c-246">déclencheur de connexion API Hello est similaire HTTP défini toohello dans ses fonctionnalités de base.</span><span class="sxs-lookup"><span data-stu-id="45f1c-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="45f1c-247">Toutefois, les paramètres hello pour identifier l’action de hello sont différents.</span><span class="sxs-lookup"><span data-stu-id="45f1c-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="45f1c-248">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-248">Here is an example:</span></span>  
  
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

|<span data-ttu-id="45f1c-249">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-249">Element name</span></span>|<span data-ttu-id="45f1c-250">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-250">Required</span></span>|<span data-ttu-id="45f1c-251">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-251">Type</span></span>|<span data-ttu-id="45f1c-252">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-253">host</span><span class="sxs-lookup"><span data-stu-id="45f1c-253">host</span></span>|<span data-ttu-id="45f1c-254">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-254">Yes</span></span>||<span data-ttu-id="45f1c-255">Hello ApiApp hébergé passerelle et l’id.</span><span class="sxs-lookup"><span data-stu-id="45f1c-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="45f1c-256">method</span><span class="sxs-lookup"><span data-stu-id="45f1c-256">method</span></span>|<span data-ttu-id="45f1c-257">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-257">Yes</span></span>|<span data-ttu-id="45f1c-258">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-258">String</span></span>|<span data-ttu-id="45f1c-259">Peut s’agir de hello suivant les méthodes HTTP : **obtenir**, **POST**, **PUT**, **supprimer**, **correctif**, ou  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="45f1c-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="45f1c-260">queries</span><span class="sxs-lookup"><span data-stu-id="45f1c-260">queries</span></span>|<span data-ttu-id="45f1c-261">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-261">No</span></span>|<span data-ttu-id="45f1c-262">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-262">Object</span></span>|<span data-ttu-id="45f1c-263">Toobe de paramètres de requête de hello représente ajouté toohello URL.</span><span class="sxs-lookup"><span data-stu-id="45f1c-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="45f1c-264">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="45f1c-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="45f1c-265">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-265">headers</span></span>|<span data-ttu-id="45f1c-266">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-266">No</span></span>|<span data-ttu-id="45f1c-267">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-267">Object</span></span>|<span data-ttu-id="45f1c-268">Représente chacun des en-tête de hello toohello demande est envoyée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="45f1c-269">Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="45f1c-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="45f1c-270">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-270">body</span></span>|<span data-ttu-id="45f1c-271">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-271">No</span></span>|<span data-ttu-id="45f1c-272">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-272">Object</span></span>|<span data-ttu-id="45f1c-273">Représente la charge utile hello envoyé toohello le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="45f1c-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="45f1c-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="45f1c-274">retryPolicy</span></span>|<span data-ttu-id="45f1c-275">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-275">No</span></span>|<span data-ttu-id="45f1c-276">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-276">Object</span></span>|<span data-ttu-id="45f1c-277">Vous permet de comportement des nouvelles tentatives toocustomize hello pour les erreurs 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="45f1c-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="45f1c-278">authentication</span><span class="sxs-lookup"><span data-stu-id="45f1c-278">authentication</span></span>|<span data-ttu-id="45f1c-279">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-279">No</span></span>|<span data-ttu-id="45f1c-280">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-280">Object</span></span>|<span data-ttu-id="45f1c-281">Méthode hello représente hello demande doit être authentifié.</span><span class="sxs-lookup"><span data-stu-id="45f1c-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="45f1c-282">Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="45f1c-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="45f1c-283">propriétés Hello pour l’hôte sont :</span><span class="sxs-lookup"><span data-stu-id="45f1c-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="45f1c-284">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-284">Element name</span></span>|<span data-ttu-id="45f1c-285">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-285">Required</span></span>|<span data-ttu-id="45f1c-286">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="45f1c-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="45f1c-287">api runtimeUrl</span></span>|<span data-ttu-id="45f1c-288">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-288">Yes</span></span>|<span data-ttu-id="45f1c-289">point de terminaison Hello Hello les API managée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="45f1c-290">connection name</span><span class="sxs-lookup"><span data-stu-id="45f1c-290">connection name</span></span>||<span data-ttu-id="45f1c-291">Un paramètre de tooa de référence doit être appelé `$connection` et nom hello de connexion hello géré API hello utilise des flux de travail.</span><span class="sxs-lookup"><span data-stu-id="45f1c-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="45f1c-292">Hello les sorties d’un déclencheur de connexion d’API sont :</span><span class="sxs-lookup"><span data-stu-id="45f1c-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="45f1c-293">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-293">Element name</span></span>|<span data-ttu-id="45f1c-294">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-294">Type</span></span>|<span data-ttu-id="45f1c-295">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="45f1c-296">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-296">headers</span></span>|<span data-ttu-id="45f1c-297">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-297">Object</span></span>|<span data-ttu-id="45f1c-298">en-têtes de réponse http de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="45f1c-299">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-299">body</span></span>|<span data-ttu-id="45f1c-300">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-300">Object</span></span>|<span data-ttu-id="45f1c-301">corps de réponse http de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="45f1c-302">Déclencheur HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="45f1c-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="45f1c-303">s’ouvre déclencheur Hello HTTPWebhook un point de terminaison, déclencheur manuel des toohello similaire, mais hello HTTPWebhook déclencheur appelle également tooa spécifié URL tooregister et annuler l’inscription.</span><span class="sxs-lookup"><span data-stu-id="45f1c-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="45f1c-304">Un déclencheur HTTPWebhook peut se présenter comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

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

<span data-ttu-id="45f1c-305">La plupart de ces sections sont facultatifs et comportement de hello Hello Webhook varie selon les sections fournies ou omises.</span><span class="sxs-lookup"><span data-stu-id="45f1c-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="45f1c-306">propriétés de Hello d’un Webhook sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="45f1c-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="45f1c-307">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-307">Element name</span></span>|<span data-ttu-id="45f1c-308">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-308">Required</span></span>|<span data-ttu-id="45f1c-309">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="45f1c-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="45f1c-310">subscribe</span></span>|<span data-ttu-id="45f1c-311">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-311">No</span></span>|<span data-ttu-id="45f1c-312">Hello sortant demande qui est appelée lorsque le déclencheur de hello est créé et effectue l’inscription initiale de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="45f1c-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="45f1c-313">unsubscribe</span></span>|<span data-ttu-id="45f1c-314">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-314">No</span></span>|<span data-ttu-id="45f1c-315">Hello sortant demande lorsque hello déclencheur est supprimé.</span><span class="sxs-lookup"><span data-stu-id="45f1c-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="45f1c-316">**S’abonner** hello sortant appel qui a effectué les tooevents écoute toostart.</span><span class="sxs-lookup"><span data-stu-id="45f1c-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="45f1c-317">Cet appel commence par hello faire de même jeu de paramètres qui hello normales actions HTTP.</span><span class="sxs-lookup"><span data-stu-id="45f1c-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="45f1c-318">Cet appel sortant est effectué hello de n’importe quel moment les modifications de workflow en aucune façon, par exemple, chaque fois que les informations d’identification de hello sont annulées ou modification des paramètres d’entrée de déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="45f1c-319">toosupport cet appel, il existe une nouvelle fonction : `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="45f1c-320">Cette fonction renvoie une URL unique pour ce déclencheur spécifique dans ce workflow.</span><span class="sxs-lookup"><span data-stu-id="45f1c-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="45f1c-321">Il représente identificateur unique de hello pour les points de terminaison hello utilisant hello Service REST.</span><span class="sxs-lookup"><span data-stu-id="45f1c-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="45f1c-322">**unsubscribe** est appelé lorsqu’une opération rend ce déclencheur non valide, notamment dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="45f1c-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="45f1c-323">Supprimer ou désactiver le déclencheur de hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="45f1c-324">Supprimez ou désactivez le flux de travail hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="45f1c-325">Supprimez ou désactivez les abonnement hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="45f1c-326">application de la logique de Hello appelle automatiquement hello vous désabonner d’action.</span><span class="sxs-lookup"><span data-stu-id="45f1c-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="45f1c-327">paramètres Hello toothis fonction sont même hello en tant que déclencheur HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="45f1c-328">Hello sorties du déclencheur de HTTPWebhook hello sont contenu hello de demande entrante de hello :</span><span class="sxs-lookup"><span data-stu-id="45f1c-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="45f1c-329">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-329">Element name</span></span>|<span data-ttu-id="45f1c-330">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-330">Type</span></span>|<span data-ttu-id="45f1c-331">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="45f1c-332">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-332">headers</span></span>|<span data-ttu-id="45f1c-333">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-333">Object</span></span>|<span data-ttu-id="45f1c-334">en-têtes de requête http de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="45f1c-335">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-335">body</span></span>|<span data-ttu-id="45f1c-336">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-336">Object</span></span>|<span data-ttu-id="45f1c-337">corps Hello de requête http de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="45f1c-338">Limites lors d’une action de webhook peuvent être spécifiés dans hello comme [limites asynchrone HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="45f1c-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="45f1c-339">Conditions</span><span class="sxs-lookup"><span data-stu-id="45f1c-339">Conditions</span></span>  

<span data-ttu-id="45f1c-340">Pour n’importe quel déclencheur, vous pouvez utiliser un ou plusieurs toodetermine de conditions si le flux de travail hello doit s’exécuter ou non.</span><span class="sxs-lookup"><span data-stu-id="45f1c-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="45f1c-341">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-341">For example:</span></span>  

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

<span data-ttu-id="45f1c-342">Dans ce cas, hello seuls les déclencheurs rapport lors du flux de travail hello `sendReports` paramètre a la valeur tootrue.</span><span class="sxs-lookup"><span data-stu-id="45f1c-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="45f1c-343">Enfin, conditions peuvent faire référence de code d’état hello du déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="45f1c-344">Par exemple, vous pouvez lancer un workflow uniquement lorsque votre site web renvoie un code d’état 500, comme suit :</span><span class="sxs-lookup"><span data-stu-id="45f1c-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="45f1c-345">Lorsque n’importe quelle expression fait référence au code d’état hello du déclencheur de hello \(en aucune façon\), hello le comportement par défaut \(déclencheur uniquement sur 200 \(OK\) \) est remplacé.</span><span class="sxs-lookup"><span data-stu-id="45f1c-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="45f1c-346">Par exemple, si vous souhaitez tootrigger sur le code d’état 200 et code d’état 201, vous avez tooinclude : `@or(equals(triggers().code, 200),equals(triggers().code,201))` comme condition.</span><span class="sxs-lookup"><span data-stu-id="45f1c-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="45f1c-347">Démarrer plusieurs exécutions pour une requête</span><span class="sxs-lookup"><span data-stu-id="45f1c-347">Start multiple runs for a request</span></span>

<span data-ttu-id="45f1c-348">tookick off pour une demande unique, plusieurs séries de `splitOn` est utile, par exemple, lorsque vous souhaitez toopoll un point de terminaison qui peut avoir plusieurs nouveaux éléments entre les intervalles d’interrogation.</span><span class="sxs-lookup"><span data-stu-id="45f1c-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="45f1c-349">Avec `splitOn`, vous spécifiez la propriété hello au sein de la charge utile de réponse hello qui contient le tableau hello d’éléments, chacun d’eux toouse toostart une exécution du déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="45f1c-350">Par exemple, imaginez qu'une API qui renvoie hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="45f1c-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
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
  
<span data-ttu-id="45f1c-351">Votre application logique doit uniquement le contenu de lignes hello, donc vous pouvez construire votre déclencheur à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="45f1c-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
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
  
<span data-ttu-id="45f1c-352">Ensuite, dans la définition de flux de travail hello `@triggerBody().name` retourne `mycoolrow` pour hello première exécution, et `another row` pour la deuxième exécution de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="45f1c-353">Hello déclencheur sorties ressemble cet exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="45f1c-354">Par conséquent, si vous utilisez `SplitOn`, vous ne pouvez pas obtenir les propriétés de hello situés en dehors de tableau de hello, dans ce cas, hello `Status` champ.</span><span class="sxs-lookup"><span data-stu-id="45f1c-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="45f1c-355">Dans cet exemple, nous utilisons hello `?` tooavoid en mesure d’opérateur toobe un échec si hello `Rows` propriété n’est pas présente.</span><span class="sxs-lookup"><span data-stu-id="45f1c-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="45f1c-356">Instance d’exécution unique</span><span class="sxs-lookup"><span data-stu-id="45f1c-356">Single run instance</span></span>

<span data-ttu-id="45f1c-357">Vous pouvez configurer les déclencheurs qui ont un incendie tooonly de propriété périodicité si toutes les exécutions actives s’est terminé.</span><span class="sxs-lookup"><span data-stu-id="45f1c-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="45f1c-358">Si une périodicité planifiée se produit alors qu’il est en cours d’exécution, déclencheur de hello ignore et attend jusqu'à hello suivant périodicité planifiée intervalle toocheck à nouveau.</span><span class="sxs-lookup"><span data-stu-id="45f1c-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="45f1c-359">Vous pouvez configurer ce paramètre via les options d’opération hello :</span><span class="sxs-lookup"><span data-stu-id="45f1c-359">You can configure this setting through hello operation options:</span></span>

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

## <a name="types-and-inputs"></a><span data-ttu-id="45f1c-360">Types et entrées</span><span class="sxs-lookup"><span data-stu-id="45f1c-360">Types and inputs</span></span>  

<span data-ttu-id="45f1c-361">Il existe de nombreux types d’actions, chacune présentant un comportement unique.</span><span class="sxs-lookup"><span data-stu-id="45f1c-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="45f1c-362">Les actions de collection peuvent contenir de nombreuses autres actions.</span><span class="sxs-lookup"><span data-stu-id="45f1c-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="45f1c-363">Actions standard</span><span class="sxs-lookup"><span data-stu-id="45f1c-363">Standard actions</span></span>  

-   <span data-ttu-id="45f1c-364">**HTTP** - Cette action appelle un point de terminaison web HTTP.</span><span class="sxs-lookup"><span data-stu-id="45f1c-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="45f1c-365">**ApiConnection** \- cette action se comporte comme hello action HTTP, mais il utilise hello gérée par Microsoft des API.</span><span class="sxs-lookup"><span data-stu-id="45f1c-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="45f1c-366">**ApiConnectionWebhook** \- comme HTTPWebhook, mais utilise hello gérée par Microsoft des API.</span><span class="sxs-lookup"><span data-stu-id="45f1c-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="45f1c-367">**Response** \- Cette action définit une réponse pour un appel entrant.</span><span class="sxs-lookup"><span data-stu-id="45f1c-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="45f1c-368">**Wait** \- Cette action simple déclenche une attente pendant une durée définie ou jusqu’à un moment spécifique.</span><span class="sxs-lookup"><span data-stu-id="45f1c-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="45f1c-369">**Workflow** \- Cette action représente un workflow imbriqué.</span><span class="sxs-lookup"><span data-stu-id="45f1c-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="45f1c-370">**Function**\- Cette action représente une fonction d’Azure.</span><span class="sxs-lookup"><span data-stu-id="45f1c-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="45f1c-371">Actions de collection</span><span class="sxs-lookup"><span data-stu-id="45f1c-371">Collection actions</span></span>

-   <span data-ttu-id="45f1c-372">**Scope** \- Cette action est un regroupement logique d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="45f1c-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="45f1c-373">**Condition** \- cette action évalue une expression et exécute la branche de résultat hello correspondante.</span><span class="sxs-lookup"><span data-stu-id="45f1c-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="45f1c-374">**ForEach** \- Cette action en boucle effectue une itération dans un tableau et exécute des actions internes pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="45f1c-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="45f1c-375">**Jusqu'à ce que** \- cette action en boucle exécute les actions internes jusqu'à ce qu’une condition entraîne tootrue.</span><span class="sxs-lookup"><span data-stu-id="45f1c-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="45f1c-376">Chaque type d’action présente un ensemble différent d’**entrées** qui définissent le comportement d’une action.</span><span class="sxs-lookup"><span data-stu-id="45f1c-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="45f1c-377">Action HTTP</span><span class="sxs-lookup"><span data-stu-id="45f1c-377">HTTP action</span></span>  

<span data-ttu-id="45f1c-378">Actions HTTP appellent un point de terminaison spécifié et vérifiez hello réponse toodetermine si le flux de travail hello doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="45f1c-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="45f1c-379">Hello **entrées** objet prend ensemble hello de paramètres requis tooconstruct hello HTTP appel :</span><span class="sxs-lookup"><span data-stu-id="45f1c-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="45f1c-380">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-380">Element name</span></span>|<span data-ttu-id="45f1c-381">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-381">Required</span></span>|<span data-ttu-id="45f1c-382">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-382">Type</span></span>|<span data-ttu-id="45f1c-383">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-384">method</span><span class="sxs-lookup"><span data-stu-id="45f1c-384">method</span></span>|<span data-ttu-id="45f1c-385">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-385">Yes</span></span>|<span data-ttu-id="45f1c-386">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-386">String</span></span>|<span data-ttu-id="45f1c-387">Peut s’agir de hello suivant les méthodes HTTP : **obtenir**, **POST**, **PUT**, **supprimer**, **correctif**, ou  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="45f1c-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="45f1c-388">URI</span><span class="sxs-lookup"><span data-stu-id="45f1c-388">uri</span></span>|<span data-ttu-id="45f1c-389">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-389">Yes</span></span>|<span data-ttu-id="45f1c-390">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-390">String</span></span>|<span data-ttu-id="45f1c-391">Bonjour le point de terminaison http ou https est appelé.</span><span class="sxs-lookup"><span data-stu-id="45f1c-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="45f1c-392">La longueur maximale est de 2 Ko.</span><span class="sxs-lookup"><span data-stu-id="45f1c-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="45f1c-393">queries</span><span class="sxs-lookup"><span data-stu-id="45f1c-393">queries</span></span>|<span data-ttu-id="45f1c-394">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-394">No</span></span>|<span data-ttu-id="45f1c-395">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-395">Object</span></span>|<span data-ttu-id="45f1c-396">Représente l’URL toohello tooadd de paramètres de requête hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="45f1c-397">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="45f1c-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="45f1c-398">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-398">headers</span></span>|<span data-ttu-id="45f1c-399">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-399">No</span></span>|<span data-ttu-id="45f1c-400">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-400">Object</span></span>|<span data-ttu-id="45f1c-401">Représente chacun des en-tête de hello toohello demande est envoyée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="45f1c-402">Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="45f1c-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="45f1c-403">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-403">body</span></span>|<span data-ttu-id="45f1c-404">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-404">No</span></span>|<span data-ttu-id="45f1c-405">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-405">Object</span></span>|<span data-ttu-id="45f1c-406">Représente la charge utile hello envoyé toohello le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="45f1c-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="45f1c-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="45f1c-407">retryPolicy</span></span>|<span data-ttu-id="45f1c-408">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-408">No</span></span>|<span data-ttu-id="45f1c-409">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-409">Object</span></span>|<span data-ttu-id="45f1c-410">Vous permet de personnaliser le comportement des nouvelles tentatives hello pour les erreurs 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="45f1c-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="45f1c-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="45f1c-411">operationsOptions</span></span>|<span data-ttu-id="45f1c-412">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-412">No</span></span>|<span data-ttu-id="45f1c-413">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-413">String</span></span>|<span data-ttu-id="45f1c-414">Définit un jeu hello de comportements spéciaux toooverride.</span><span class="sxs-lookup"><span data-stu-id="45f1c-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="45f1c-415">authentication</span><span class="sxs-lookup"><span data-stu-id="45f1c-415">authentication</span></span>|<span data-ttu-id="45f1c-416">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-416">No</span></span>|<span data-ttu-id="45f1c-417">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-417">Object</span></span>|<span data-ttu-id="45f1c-418">Méthode hello représente hello demande doit être authentifié.</span><span class="sxs-lookup"><span data-stu-id="45f1c-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="45f1c-419">Pour plus d’informations sur cet objet, consultez [Authentification sortante de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="45f1c-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="45f1c-420">En plus de Scheduler, une autre propriété est prise en charge : `authority`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="45f1c-421">Par défaut, cette propriété est définie sur `https://login.windows.net` lorsqu’aucune valeur n’est spécifiée, mais vous pouvez utiliser une autre audience comme `https://login.windows\-ppe.net`</span><span class="sxs-lookup"><span data-stu-id="45f1c-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="45f1c-422">Les actions HTTP \(et ApiConnection\) prennent en charge les stratégies de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="45f1c-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="45f1c-423">Stratégie de nouvelle tentative s’applique à des échecs de toointermittent, caractérisées en tant que l’état HTTP 408 429 et 5xx, exceptions de connectivité tooany Ajout des codes.</span><span class="sxs-lookup"><span data-stu-id="45f1c-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="45f1c-424">Cette stratégie est décrit à l’aide de hello *retryPolicy* objet défini comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="45f1c-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="45f1c-425">intervalle avant nouvelle tentative de Hello est spécifié au format de hello ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="45f1c-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="45f1c-426">Cet intervalle a une valeur par défaut et la valeur minimale de 20 secondes, alors que la valeur maximale de hello est d’une heure.</span><span class="sxs-lookup"><span data-stu-id="45f1c-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="45f1c-427">nombre de tentatives par défaut et maximale Hello correspond à quatre heures.</span><span class="sxs-lookup"><span data-stu-id="45f1c-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="45f1c-428">Si la définition de stratégie de nouvelle tentative hello n’est pas spécifiée, un `fixed` stratégie est utilisée avec les valeurs de compteur et d’intervalle de nouvelle tentative par défaut.</span><span class="sxs-lookup"><span data-stu-id="45f1c-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="45f1c-429">stratégie de nouvelle tentative toodisable hello, définissez son type trop`None`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="45f1c-430">Par exemple, hello action suivante effectue une nouvelle tentative extraction actualité hello deux fois, s’il existe des défaillances intermittentes, pour un total de trois exécutions, avec un délai de 30 secondes entre chaque tentative :</span><span class="sxs-lookup"><span data-stu-id="45f1c-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
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
### <a name="asynchronous-patterns"></a><span data-ttu-id="45f1c-431">Modèles asynchrones</span><span class="sxs-lookup"><span data-stu-id="45f1c-431">Asynchronous patterns</span></span>

<span data-ttu-id="45f1c-432">Par défaut, toutes les actions basées sur HTTP prend en charge le modèle d’opération asynchrone standard hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="45f1c-433">Donc si le serveur distant de hello indique cette demande hello est accepté pour traitement avec un message 202 \(accepté\) réponse, moteur de Logic Apps hello conserve l’interrogation des URL de hello spécifiée dans l’en-tête d’emplacement de la réponse hello jusqu'à atteindre un terminal état \(pas\-réponse 202\).</span><span class="sxs-lookup"><span data-stu-id="45f1c-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="45f1c-434">comportement asynchrone de hello toodisable précédemment décrit, définie un `DisableAsyncPattern` option dans les entrées d’action hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="45f1c-435">Dans ce cas, sortie hello d’action de hello est basée sur hello initiale 202 réponse hello serveur.</span><span class="sxs-lookup"><span data-stu-id="45f1c-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
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

#### <a name="asynchronous-limits"></a><span data-ttu-id="45f1c-436">Limites asynchrones</span><span class="sxs-lookup"><span data-stu-id="45f1c-436">Asynchronous Limits</span></span>

<span data-ttu-id="45f1c-437">Un modèle asynchrone peut être limité dans son intervalle de temps spécifique tooa durée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="45f1c-438">Si l’intervalle de temps hello s’écoule sans atteindre un état terminal, état hello d’action de hello est marquée `Cancelled` avec un code `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="45f1c-439">délai d’expiration de la limite Hello est spécifié au format ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="45f1c-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="45f1c-440">Les limites peuvent être spécifiées avec la syntaxe de hello :</span><span class="sxs-lookup"><span data-stu-id="45f1c-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="45f1c-441">ApiConnection</span><span class="sxs-lookup"><span data-stu-id="45f1c-441">API Connection</span></span>  

<span data-ttu-id="45f1c-442">ApiConnection est une action qui fait référence à un connecteur géré par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="45f1c-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="45f1c-443">Cette action nécessite une connexion valide au tooa de référence et des informations sur hello API et les paramètres requis.</span><span class="sxs-lookup"><span data-stu-id="45f1c-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="45f1c-444">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="45f1c-444">Element name</span></span>|<span data-ttu-id="45f1c-445">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-445">Required</span></span>|<span data-ttu-id="45f1c-446">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-446">Type</span></span>|<span data-ttu-id="45f1c-447">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-448">host</span><span class="sxs-lookup"><span data-stu-id="45f1c-448">host</span></span>|<span data-ttu-id="45f1c-449">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-449">Yes</span></span>|<span data-ttu-id="45f1c-450">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-450">Object</span></span>|<span data-ttu-id="45f1c-451">Représente les informations de connecteur hello comme objet de connexion toohello runtimeUrl et référence des hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="45f1c-452">method</span><span class="sxs-lookup"><span data-stu-id="45f1c-452">method</span></span>|<span data-ttu-id="45f1c-453">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-453">Yes</span></span>|<span data-ttu-id="45f1c-454">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-454">String</span></span>|<span data-ttu-id="45f1c-455">Peut s’agir de hello suivant les méthodes HTTP : **obtenir**, **POST**, **PUT**, **supprimer**, **correctif**, ou  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="45f1c-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="45f1c-456">path</span><span class="sxs-lookup"><span data-stu-id="45f1c-456">path</span></span>|<span data-ttu-id="45f1c-457">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-457">Yes</span></span>|<span data-ttu-id="45f1c-458">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-458">String</span></span>|<span data-ttu-id="45f1c-459">chemin d’accès de Hello d’opération de hello API.</span><span class="sxs-lookup"><span data-stu-id="45f1c-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="45f1c-460">queries</span><span class="sxs-lookup"><span data-stu-id="45f1c-460">queries</span></span>|<span data-ttu-id="45f1c-461">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-461">No</span></span>|<span data-ttu-id="45f1c-462">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-462">Object</span></span>|<span data-ttu-id="45f1c-463">Représente l’URL toohello tooadd de paramètres de requête hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="45f1c-464">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="45f1c-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="45f1c-465">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-465">headers</span></span>|<span data-ttu-id="45f1c-466">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-466">No</span></span>|<span data-ttu-id="45f1c-467">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-467">Object</span></span>|<span data-ttu-id="45f1c-468">Représente chacun des en-tête de hello toohello demande est envoyée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="45f1c-469">Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="45f1c-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="45f1c-470">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-470">body</span></span>|<span data-ttu-id="45f1c-471">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-471">No</span></span>|<span data-ttu-id="45f1c-472">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-472">Object</span></span>|<span data-ttu-id="45f1c-473">Représente la charge utile hello envoyé toohello le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="45f1c-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="45f1c-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="45f1c-474">retryPolicy</span></span>|<span data-ttu-id="45f1c-475">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-475">No</span></span>|<span data-ttu-id="45f1c-476">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-476">Object</span></span>|<span data-ttu-id="45f1c-477">Vous permet de personnaliser le comportement des nouvelles tentatives hello pour les erreurs 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="45f1c-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="45f1c-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="45f1c-478">operationsOptions</span></span>|<span data-ttu-id="45f1c-479">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-479">No</span></span>|<span data-ttu-id="45f1c-480">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-480">String</span></span>|<span data-ttu-id="45f1c-481">Définit un jeu hello de comportements spéciaux toooverride.</span><span class="sxs-lookup"><span data-stu-id="45f1c-481">Defines hello set of special behaviors toooverride.</span></span>|  

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

## <a name="api-connection-webhook-action"></a><span data-ttu-id="45f1c-482">Action ApiConnectionWebhook</span><span class="sxs-lookup"><span data-stu-id="45f1c-482">API Connection webhook action</span></span>

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

<span data-ttu-id="45f1c-483">Limites lors d’une action de webhook peuvent être spécifiés dans hello comme [limites asynchrone HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="45f1c-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="45f1c-484">Action de réponse</span><span class="sxs-lookup"><span data-stu-id="45f1c-484">Response action</span></span>  

<span data-ttu-id="45f1c-485">Ce type d’action contient hello charge utile de réponse entière à partir d’une requête HTTP et inclut un statusCode, corps et en-têtes :</span><span class="sxs-lookup"><span data-stu-id="45f1c-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
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
  
<span data-ttu-id="45f1c-486">action de réponse Hello présente des restrictions spéciales qui ne s’appliquent pas tooother actions.</span><span class="sxs-lookup"><span data-stu-id="45f1c-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="45f1c-487">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="45f1c-487">Specifically:</span></span>  
  
-   <span data-ttu-id="45f1c-488">Actions de réponse ne peut pas être parallèles dans une définition, car une demande entrante de réponse déterministe toohello est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="45f1c-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="45f1c-489">Si une action de réponse est atteinte après la demande entrante de hello a reçu une réponse, action de hello est considéré comme défectueux \(conflit\), et par conséquent, hello exécuter `Failed`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="45f1c-490">Un workflow comportant des actions response ne peut pas avoir `splitOn` dans son déclencheur, car un seul appel entraîne de nombreuses exécutions.</span><span class="sxs-lookup"><span data-stu-id="45f1c-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="45f1c-491">Par conséquent, il doit être validé lorsque le flux de hello est PUT et cause une erreur demande incorrecte.</span><span class="sxs-lookup"><span data-stu-id="45f1c-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="45f1c-492">Action wait</span><span class="sxs-lookup"><span data-stu-id="45f1c-492">Wait action</span></span>  

<span data-ttu-id="45f1c-493">Hello `wait` action interrompt l’exécution de flux de travail pour l’intervalle de salutation spécifié.</span><span class="sxs-lookup"><span data-stu-id="45f1c-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="45f1c-494">Par exemple, toowait 15 minutes, vous pouvez utiliser cet extrait de code :</span><span class="sxs-lookup"><span data-stu-id="45f1c-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
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
  
<span data-ttu-id="45f1c-495">Vous pouvez également toowait jusqu'à un moment précis, vous pouvez utiliser cet exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
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
> <span data-ttu-id="45f1c-496">durée d’attente Hello peut soit être spécifiée à l’aide de hello **intervalle** objet ou hello **jusqu'à ce que** objet, mais pas les deux.</span><span class="sxs-lookup"><span data-stu-id="45f1c-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="45f1c-497">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-497">Name</span></span>|<span data-ttu-id="45f1c-498">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-498">Required</span></span>|<span data-ttu-id="45f1c-499">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-499">Type</span></span>|<span data-ttu-id="45f1c-500">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-501">interval</span><span class="sxs-lookup"><span data-stu-id="45f1c-501">interval</span></span>|<span data-ttu-id="45f1c-502">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-502">No</span></span>|<span data-ttu-id="45f1c-503">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-503">Object</span></span>|<span data-ttu-id="45f1c-504">durée, en fonction de la quantité de temps d’attente de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="45f1c-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="45f1c-505">interval unit</span></span>|<span data-ttu-id="45f1c-506">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-506">Yes</span></span>|<span data-ttu-id="45f1c-507">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-507">String</span></span>|<span data-ttu-id="45f1c-508">Un de ces intervalles : second (seconde), minute (minute), hour (heure), day (jour), week (semaine), month (mois), year (année).</span><span class="sxs-lookup"><span data-stu-id="45f1c-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="45f1c-509">interval count</span><span class="sxs-lookup"><span data-stu-id="45f1c-509">interval count</span></span>|<span data-ttu-id="45f1c-510">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-510">Yes</span></span>|<span data-ttu-id="45f1c-511">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-511">String</span></span>|<span data-ttu-id="45f1c-512">Durée en fonction des hello donné d’unité interne.</span><span class="sxs-lookup"><span data-stu-id="45f1c-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="45f1c-513">until</span><span class="sxs-lookup"><span data-stu-id="45f1c-513">until</span></span>|<span data-ttu-id="45f1c-514">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-514">No</span></span>|<span data-ttu-id="45f1c-515">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-515">Object</span></span>|<span data-ttu-id="45f1c-516">durée basée sur un point dans le temps d’attente de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="45f1c-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="45f1c-517">until timestamp</span></span>|<span data-ttu-id="45f1c-518">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-518">Yes</span></span>|<span data-ttu-id="45f1c-519">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-519">String</span></span>|<span data-ttu-id="45f1c-520">Chaîne &#124; hello un point dans le temps au format UTC lorsque hello attente arrive à expiration.</span><span class="sxs-lookup"><span data-stu-id="45f1c-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="45f1c-521">Action de requête</span><span class="sxs-lookup"><span data-stu-id="45f1c-521">Query action</span></span>

<span data-ttu-id="45f1c-522">Hello `query` action vous permet de filtrer un tableau en fonction d’une condition.</span><span class="sxs-lookup"><span data-stu-id="45f1c-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="45f1c-523">Par exemple, les numéros de tooselect supérieures à 2, vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="45f1c-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="45f1c-524">Hello sortie de hello `query` action est un tableau qui contient des éléments qui satisfont la condition de hello hello tableau d’entrée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="45f1c-525">Si aucune valeur ne satisfaire hello `where` de condition, hello résultat est un tableau vide.</span><span class="sxs-lookup"><span data-stu-id="45f1c-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="45f1c-526">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-526">Name</span></span>|<span data-ttu-id="45f1c-527">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-527">Required</span></span>|<span data-ttu-id="45f1c-528">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-528">Type</span></span>|<span data-ttu-id="45f1c-529">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="45f1c-530">from</span><span class="sxs-lookup"><span data-stu-id="45f1c-530">from</span></span>|<span data-ttu-id="45f1c-531">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-531">Yes</span></span>|<span data-ttu-id="45f1c-532">Tableau</span><span class="sxs-lookup"><span data-stu-id="45f1c-532">Array</span></span>|<span data-ttu-id="45f1c-533">tableau de source de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-533">hello source array.</span></span>|
|<span data-ttu-id="45f1c-534">où</span><span class="sxs-lookup"><span data-stu-id="45f1c-534">where</span></span>|<span data-ttu-id="45f1c-535">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-535">Yes</span></span>|<span data-ttu-id="45f1c-536">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-536">String</span></span>|<span data-ttu-id="45f1c-537">Hello condition tooapply tooeach élément du tableau source de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="45f1c-538">Action select</span><span class="sxs-lookup"><span data-stu-id="45f1c-538">Select action</span></span>

<span data-ttu-id="45f1c-539">Hello `select` action vous permet de projeter de chaque élément d’un tableau dans une nouvelle valeur.</span><span class="sxs-lookup"><span data-stu-id="45f1c-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="45f1c-540">Par exemple, tooconvert un tableau de nombres dans un tableau d’objets, vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="45f1c-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="45f1c-541">Hello sortie Hello `select` action est un tableau ayant hello même cardinalité comme hello du tableau d’entrée, chaque élément transformé comme définie par hello `select` propriété.</span><span class="sxs-lookup"><span data-stu-id="45f1c-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="45f1c-542">Si l’entrée de hello est un tableau vide, hello sortie est également un tableau vide.</span><span class="sxs-lookup"><span data-stu-id="45f1c-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="45f1c-543">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-543">Name</span></span>|<span data-ttu-id="45f1c-544">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-544">Required</span></span>|<span data-ttu-id="45f1c-545">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-545">Type</span></span>|<span data-ttu-id="45f1c-546">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="45f1c-547">from</span><span class="sxs-lookup"><span data-stu-id="45f1c-547">from</span></span>|<span data-ttu-id="45f1c-548">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-548">Yes</span></span>|<span data-ttu-id="45f1c-549">Tableau</span><span class="sxs-lookup"><span data-stu-id="45f1c-549">Array</span></span>|<span data-ttu-id="45f1c-550">tableau de source de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-550">hello source array.</span></span>|
|<span data-ttu-id="45f1c-551">select</span><span class="sxs-lookup"><span data-stu-id="45f1c-551">select</span></span>|<span data-ttu-id="45f1c-552">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-552">Yes</span></span>|<span data-ttu-id="45f1c-553">Quelconque</span><span class="sxs-lookup"><span data-stu-id="45f1c-553">Any</span></span>|<span data-ttu-id="45f1c-554">Hello projection tooapply tooeach élément du tableau source de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="45f1c-555">Action terminate</span><span class="sxs-lookup"><span data-stu-id="45f1c-555">Terminate action</span></span>

<span data-ttu-id="45f1c-556">Hello Terminate action arrête l’exécution du workflow hello exécuter, abandon de toutes les actions en cours et en ignorant les actions restantes.</span><span class="sxs-lookup"><span data-stu-id="45f1c-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="45f1c-557">Par exemple, tooterminate une exécution avec l’état **n’a pas pu**, vous pouvez utiliser hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="45f1c-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

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
> <span data-ttu-id="45f1c-558">Déjà effectuées des actions ne sont pas affectées par hello terminer l’action.</span><span class="sxs-lookup"><span data-stu-id="45f1c-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="45f1c-559">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-559">Name</span></span>|<span data-ttu-id="45f1c-560">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-560">Required</span></span>|<span data-ttu-id="45f1c-561">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-561">Type</span></span>|<span data-ttu-id="45f1c-562">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="45f1c-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="45f1c-563">runStatus</span></span>|<span data-ttu-id="45f1c-564">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-564">Yes</span></span>|<span data-ttu-id="45f1c-565">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-565">String</span></span>|<span data-ttu-id="45f1c-566">cible de Hello statut d’exécution.</span><span class="sxs-lookup"><span data-stu-id="45f1c-566">hello target run status.</span></span> <span data-ttu-id="45f1c-567">Peut être défini sur **Failed** (Échec) ou **Cancelled** (Annulée).</span><span class="sxs-lookup"><span data-stu-id="45f1c-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="45f1c-568">runError</span><span class="sxs-lookup"><span data-stu-id="45f1c-568">runError</span></span>|<span data-ttu-id="45f1c-569">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-569">No</span></span>|<span data-ttu-id="45f1c-570">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-570">Object</span></span>|<span data-ttu-id="45f1c-571">Détails de l’erreur Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-571">hello error details.</span></span> <span data-ttu-id="45f1c-572">Uniquement pris en charge lorsque **runStatus** est défini trop**n’a pas pu**.</span><span class="sxs-lookup"><span data-stu-id="45f1c-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="45f1c-573">runError code</span><span class="sxs-lookup"><span data-stu-id="45f1c-573">runError code</span></span>|<span data-ttu-id="45f1c-574">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-574">No</span></span>|<span data-ttu-id="45f1c-575">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-575">String</span></span>|<span data-ttu-id="45f1c-576">Hello d’exécuter le code d’erreur.</span><span class="sxs-lookup"><span data-stu-id="45f1c-576">hello run error code.</span></span>|
|<span data-ttu-id="45f1c-577">runError message</span><span class="sxs-lookup"><span data-stu-id="45f1c-577">runError message</span></span>|<span data-ttu-id="45f1c-578">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-578">No</span></span>|<span data-ttu-id="45f1c-579">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-579">String</span></span>|<span data-ttu-id="45f1c-580">Hello exécuter le message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="45f1c-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="45f1c-581">Action compose</span><span class="sxs-lookup"><span data-stu-id="45f1c-581">Compose action</span></span>

<span data-ttu-id="45f1c-582">Hello message action vous permet de construire un objet arbitraire.</span><span class="sxs-lookup"><span data-stu-id="45f1c-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="45f1c-583">sortie Hello Hello composer action hello ne résulte de l’évaluation de ses entrées.</span><span class="sxs-lookup"><span data-stu-id="45f1c-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="45f1c-584">Par exemple, vous pouvez utiliser hello composer des sorties de toomerge d’action de plusieurs actions :</span><span class="sxs-lookup"><span data-stu-id="45f1c-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

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
> <span data-ttu-id="45f1c-585">Hello **composition** action peut être utilisé tooconstruct de sortie, y compris les objets, tableaux et tout autre type de prise en charge par la logique des applications telles que XML et binaire.</span><span class="sxs-lookup"><span data-stu-id="45f1c-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="45f1c-586">Action table</span><span class="sxs-lookup"><span data-stu-id="45f1c-586">Table action</span></span>

<span data-ttu-id="45f1c-587">Hello `table` vous permet de tooconvert un tableau d’éléments dans un **CSV** ou **HTML** table.</span><span class="sxs-lookup"><span data-stu-id="45f1c-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="45f1c-588">Supposons que @triggerBody() est</span><span class="sxs-lookup"><span data-stu-id="45f1c-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="45f1c-589">Et vous permettent d’être défini en tant qu’action de hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="45f1c-590">Hello ci-dessus se produirait</span><span class="sxs-lookup"><span data-stu-id="45f1c-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="45f1c-591">id</span><span class="sxs-lookup"><span data-stu-id="45f1c-591">id</span></span></th><th><span data-ttu-id="45f1c-592">name</span><span class="sxs-lookup"><span data-stu-id="45f1c-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="45f1c-593">0</span><span class="sxs-lookup"><span data-stu-id="45f1c-593">0</span></span></td><td><span data-ttu-id="45f1c-594">pommes</span><span class="sxs-lookup"><span data-stu-id="45f1c-594">apples</span></span></td></tr><tr><td><span data-ttu-id="45f1c-595">1</span><span class="sxs-lookup"><span data-stu-id="45f1c-595">1</span></span></td><td><span data-ttu-id="45f1c-596">oranges</span><span class="sxs-lookup"><span data-stu-id="45f1c-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="45f1c-597">"</span><span class="sxs-lookup"><span data-stu-id="45f1c-597">"</span></span>

<span data-ttu-id="45f1c-598">Dans la table de commande toocustomize hello, vous pouvez spécifier explicitement les colonnes de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="45f1c-599">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="45f1c-599">For example:</span></span>

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

<span data-ttu-id="45f1c-600">Hello ci-dessus se produirait</span><span class="sxs-lookup"><span data-stu-id="45f1c-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="45f1c-601">produce id</span><span class="sxs-lookup"><span data-stu-id="45f1c-601">produce id</span></span></th><th><span data-ttu-id="45f1c-602">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="45f1c-603">0</span><span class="sxs-lookup"><span data-stu-id="45f1c-603">0</span></span></td><td><span data-ttu-id="45f1c-604">pommes fraîches</span><span class="sxs-lookup"><span data-stu-id="45f1c-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="45f1c-605">1</span><span class="sxs-lookup"><span data-stu-id="45f1c-605">1</span></span></td><td><span data-ttu-id="45f1c-606">oranges fraîches</span><span class="sxs-lookup"><span data-stu-id="45f1c-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="45f1c-607">"</span><span class="sxs-lookup"><span data-stu-id="45f1c-607">"</span></span>

<span data-ttu-id="45f1c-608">Si hello `from` valeur de propriété est un tableau vide, la sortie de hello est une table vide.</span><span class="sxs-lookup"><span data-stu-id="45f1c-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="45f1c-609">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-609">Name</span></span>|<span data-ttu-id="45f1c-610">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-610">Required</span></span>|<span data-ttu-id="45f1c-611">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-611">Type</span></span>|<span data-ttu-id="45f1c-612">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="45f1c-613">from</span><span class="sxs-lookup"><span data-stu-id="45f1c-613">from</span></span>|<span data-ttu-id="45f1c-614">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-614">Yes</span></span>|<span data-ttu-id="45f1c-615">Tableau</span><span class="sxs-lookup"><span data-stu-id="45f1c-615">Array</span></span>|<span data-ttu-id="45f1c-616">tableau de source de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-616">hello source array.</span></span>|
|<span data-ttu-id="45f1c-617">format</span><span class="sxs-lookup"><span data-stu-id="45f1c-617">format</span></span>|<span data-ttu-id="45f1c-618">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-618">Yes</span></span>|<span data-ttu-id="45f1c-619">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-619">String</span></span>|<span data-ttu-id="45f1c-620">Hello format, soit **CSV** ou **HTML**.</span><span class="sxs-lookup"><span data-stu-id="45f1c-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="45f1c-621">colonnes</span><span class="sxs-lookup"><span data-stu-id="45f1c-621">columns</span></span>|<span data-ttu-id="45f1c-622">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-622">No</span></span>|<span data-ttu-id="45f1c-623">Tableau</span><span class="sxs-lookup"><span data-stu-id="45f1c-623">Array</span></span>|<span data-ttu-id="45f1c-624">colonnes de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-624">hello columns.</span></span> <span data-ttu-id="45f1c-625">Permet la forme de valeur par défaut toooverride hello de table de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="45f1c-626">column header</span><span class="sxs-lookup"><span data-stu-id="45f1c-626">column header</span></span>|<span data-ttu-id="45f1c-627">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-627">No</span></span>|<span data-ttu-id="45f1c-628">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-628">String</span></span>|<span data-ttu-id="45f1c-629">en-tête de colonne de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-629">hello header of hello column.</span></span>|
|<span data-ttu-id="45f1c-630">column value</span><span class="sxs-lookup"><span data-stu-id="45f1c-630">column value</span></span>|<span data-ttu-id="45f1c-631">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-631">Yes</span></span>|<span data-ttu-id="45f1c-632">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-632">String</span></span>|<span data-ttu-id="45f1c-633">valeur de Hello de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="45f1c-634">Action workflow</span><span class="sxs-lookup"><span data-stu-id="45f1c-634">Workflow action</span></span>   

|<span data-ttu-id="45f1c-635">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-635">Name</span></span>|<span data-ttu-id="45f1c-636">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-636">Required</span></span>|<span data-ttu-id="45f1c-637">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-637">Type</span></span>|<span data-ttu-id="45f1c-638">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-639">host id</span><span class="sxs-lookup"><span data-stu-id="45f1c-639">host id</span></span>|<span data-ttu-id="45f1c-640">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-640">Yes</span></span>|<span data-ttu-id="45f1c-641">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-641">String</span></span>|<span data-ttu-id="45f1c-642">ID de ressource Hello du flux de travail hello que vous souhaitez toocall.</span><span class="sxs-lookup"><span data-stu-id="45f1c-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="45f1c-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="45f1c-643">host triggerName</span></span>|<span data-ttu-id="45f1c-644">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-644">Yes</span></span>|<span data-ttu-id="45f1c-645">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-645">String</span></span>|<span data-ttu-id="45f1c-646">nom de Hello du déclencheur hello que vous souhaitez tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="45f1c-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="45f1c-647">queries</span><span class="sxs-lookup"><span data-stu-id="45f1c-647">queries</span></span>|<span data-ttu-id="45f1c-648">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-648">No</span></span>|<span data-ttu-id="45f1c-649">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-649">Object</span></span>|<span data-ttu-id="45f1c-650">Représente l’URL toohello tooadd de paramètres de requête hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="45f1c-651">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="45f1c-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="45f1c-652">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-652">headers</span></span>|<span data-ttu-id="45f1c-653">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-653">No</span></span>|<span data-ttu-id="45f1c-654">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-654">Object</span></span>|<span data-ttu-id="45f1c-655">Représente chacun des en-tête de hello toohello demande est envoyée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="45f1c-656">Par exemple, langage de hello tooset et type sur une demande :`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="45f1c-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="45f1c-657">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-657">body</span></span>|<span data-ttu-id="45f1c-658">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-658">No</span></span>|<span data-ttu-id="45f1c-659">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-659">Object</span></span>|<span data-ttu-id="45f1c-660">Représente la charge utile hello toohello le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="45f1c-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
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
  
<span data-ttu-id="45f1c-661">Une vérification d’accès est effectuée sur le flux de travail hello \(plus spécifiquement, les déclencheurs hello\), ce qui signifie que vous devez accéder toohello le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="45f1c-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="45f1c-662">Hello sorties de hello `workflow` action sont basées sur ce que vous avez définies dans hello `response` action dans le flux de travail enfant hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="45f1c-663">Si vous n’avez pas défini un `response` action, puis hello sorties sont vides.</span><span class="sxs-lookup"><span data-stu-id="45f1c-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="45f1c-664">Action function</span><span class="sxs-lookup"><span data-stu-id="45f1c-664">Function action</span></span>   

|<span data-ttu-id="45f1c-665">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-665">Name</span></span>|<span data-ttu-id="45f1c-666">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-666">Required</span></span>|<span data-ttu-id="45f1c-667">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-667">Type</span></span>|<span data-ttu-id="45f1c-668">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-669">function id</span><span class="sxs-lookup"><span data-stu-id="45f1c-669">function id</span></span>|<span data-ttu-id="45f1c-670">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-670">Yes</span></span>|<span data-ttu-id="45f1c-671">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-671">String</span></span>|<span data-ttu-id="45f1c-672">ID de la fonction hello que vous souhaitez tooinvoke Hello ressources.</span><span class="sxs-lookup"><span data-stu-id="45f1c-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="45f1c-673">method</span><span class="sxs-lookup"><span data-stu-id="45f1c-673">method</span></span>|<span data-ttu-id="45f1c-674">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-674">No</span></span>|<span data-ttu-id="45f1c-675">String</span><span class="sxs-lookup"><span data-stu-id="45f1c-675">String</span></span>|<span data-ttu-id="45f1c-676">Hello méthode HTTP utilisée (fonction) hello tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="45f1c-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="45f1c-677">Par défaut, a la valeur `POST` lorsqu’elle n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="45f1c-678">queries</span><span class="sxs-lookup"><span data-stu-id="45f1c-678">queries</span></span>|<span data-ttu-id="45f1c-679">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-679">No</span></span>|<span data-ttu-id="45f1c-680">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-680">Object</span></span>|<span data-ttu-id="45f1c-681">Représente l’URL toohello tooadd de paramètres de requête hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="45f1c-682">Par exemple, `"queries" : { "api-version": "2015-02-01" }` ajoute `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="45f1c-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="45f1c-683">headers</span><span class="sxs-lookup"><span data-stu-id="45f1c-683">headers</span></span>|<span data-ttu-id="45f1c-684">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-684">No</span></span>|<span data-ttu-id="45f1c-685">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-685">Object</span></span>|<span data-ttu-id="45f1c-686">Représente chacun des en-tête de hello toohello demande est envoyée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="45f1c-687">Par exemple, langage de hello tooset et le type dans une demande : `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="45f1c-688">body</span><span class="sxs-lookup"><span data-stu-id="45f1c-688">body</span></span>|<span data-ttu-id="45f1c-689">Non</span><span class="sxs-lookup"><span data-stu-id="45f1c-689">No</span></span>|<span data-ttu-id="45f1c-690">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-690">Object</span></span>|<span data-ttu-id="45f1c-691">Représente la charge utile hello toohello le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="45f1c-691">Represents hello payload sent toohello endpoint.</span></span>|  

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

<span data-ttu-id="45f1c-692">Lorsque vous enregistrez application logique de hello, nous effectuer des vérifications de la fonction hello référencé :</span><span class="sxs-lookup"><span data-stu-id="45f1c-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="45f1c-693">Vous devez toohave toohello access (fonction).</span><span class="sxs-lookup"><span data-stu-id="45f1c-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="45f1c-694">Seuls le déclencheur HTTP standard ou un déclencheur webhook JSON générique sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="45f1c-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="45f1c-695">Aucune route ne doit être définie.</span><span class="sxs-lookup"><span data-stu-id="45f1c-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="45f1c-696">Seuls les niveaux d’autorisation « fonction » et « anonyme » sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="45f1c-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="45f1c-697">URL du déclencheur Hello est récupéré, mis en cache et utilisé lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="45f1c-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="45f1c-698">Par conséquent, si une opération invalide les URL hello mis en cache, action de hello échoue lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="45f1c-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="45f1c-699">toowork résoudre ce problème, enregistrez hello application logique, ce qui entraîne la logique application tooretrieve et mettre en cache des URL du déclencheur hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="45f1c-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="45f1c-700">Actions de collection (étendues et boucles)</span><span class="sxs-lookup"><span data-stu-id="45f1c-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="45f1c-701">Certains types d’actions peuvent contenir d’autres actions.</span><span class="sxs-lookup"><span data-stu-id="45f1c-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="45f1c-702">Actions de référence dans une collection peuvent être référencées directement en dehors de la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="45f1c-703">Si vous avez défini `http` dans une étendue (scope), `@body('http')` est toujours valide n’importe où dans un workflow.</span><span class="sxs-lookup"><span data-stu-id="45f1c-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="45f1c-704">Les actions au sein d’une collection peuvent `runAfter` uniquement d’autres actions dans hello même collection.</span><span class="sxs-lookup"><span data-stu-id="45f1c-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="45f1c-705">Action scope</span><span class="sxs-lookup"><span data-stu-id="45f1c-705">Scope action</span></span>

<span data-ttu-id="45f1c-706">Hello `scope` action vous permet de logiquement regrouper les actions d’un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="45f1c-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="45f1c-707">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-707">Name</span></span>|<span data-ttu-id="45f1c-708">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-708">Required</span></span>|<span data-ttu-id="45f1c-709">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-709">Type</span></span>|<span data-ttu-id="45f1c-710">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-711">actions</span><span class="sxs-lookup"><span data-stu-id="45f1c-711">actions</span></span>|<span data-ttu-id="45f1c-712">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-712">Yes</span></span>|<span data-ttu-id="45f1c-713">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-713">Object</span></span>|<span data-ttu-id="45f1c-714">Tooexecute actions interne étendue hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-714">Inner actions tooexecute within hello scope</span></span>|

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

## <a name="foreach-action"></a><span data-ttu-id="45f1c-715">Action foreach</span><span class="sxs-lookup"><span data-stu-id="45f1c-715">ForEach action</span></span>

<span data-ttu-id="45f1c-716">Cette action en boucle effectue une itération dans un tableau et exécute des actions internes pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="45f1c-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="45f1c-717">Par défaut, la boucle foreach de hello exécutée en parallèle (20 exécutions en parallèle à la fois).</span><span class="sxs-lookup"><span data-stu-id="45f1c-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="45f1c-718">Vous pouvez définir des règles de l’exécution à l’aide de hello `operationOptions` paramètre.</span><span class="sxs-lookup"><span data-stu-id="45f1c-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="45f1c-719">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-719">Name</span></span>|<span data-ttu-id="45f1c-720">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-720">Required</span></span>|<span data-ttu-id="45f1c-721">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-721">Type</span></span>|<span data-ttu-id="45f1c-722">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-723">actions</span><span class="sxs-lookup"><span data-stu-id="45f1c-723">actions</span></span>|<span data-ttu-id="45f1c-724">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-724">Yes</span></span>|<span data-ttu-id="45f1c-725">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-725">Object</span></span>|<span data-ttu-id="45f1c-726">Tooexecute actions interne au sein de la boucle de hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="45f1c-727">foreach</span><span class="sxs-lookup"><span data-stu-id="45f1c-727">foreach</span></span>|<span data-ttu-id="45f1c-728">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-728">Yes</span></span>|<span data-ttu-id="45f1c-729">string</span><span class="sxs-lookup"><span data-stu-id="45f1c-729">string</span></span>|<span data-ttu-id="45f1c-730">tooiterate de tableau Hello sur</span><span class="sxs-lookup"><span data-stu-id="45f1c-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="45f1c-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="45f1c-731">operationOptions</span></span>|<span data-ttu-id="45f1c-732">no</span><span class="sxs-lookup"><span data-stu-id="45f1c-732">no</span></span>|<span data-ttu-id="45f1c-733">string</span><span class="sxs-lookup"><span data-stu-id="45f1c-733">string</span></span>|<span data-ttu-id="45f1c-734">Toutes les options d’opération pour le comportement.</span><span class="sxs-lookup"><span data-stu-id="45f1c-734">Any operation options for behavior.</span></span> <span data-ttu-id="45f1c-735">Actuellement prend uniquement en charge `sequential` tooexecute itérations séquentiellement (comportement par défaut est parallèle)</span><span class="sxs-lookup"><span data-stu-id="45f1c-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

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

## <a name="until-action"></a><span data-ttu-id="45f1c-736">Action until</span><span class="sxs-lookup"><span data-stu-id="45f1c-736">Until action</span></span>

<span data-ttu-id="45f1c-737">Cette action en boucle exécute les actions internes jusqu'à ce qu’une condition entraîne tootrue.</span><span class="sxs-lookup"><span data-stu-id="45f1c-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="45f1c-738">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-738">Name</span></span>|<span data-ttu-id="45f1c-739">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-739">Required</span></span>|<span data-ttu-id="45f1c-740">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-740">Type</span></span>|<span data-ttu-id="45f1c-741">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-742">actions</span><span class="sxs-lookup"><span data-stu-id="45f1c-742">actions</span></span>|<span data-ttu-id="45f1c-743">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-743">Yes</span></span>|<span data-ttu-id="45f1c-744">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-744">Object</span></span>|<span data-ttu-id="45f1c-745">Tooexecute actions interne au sein de la boucle de hello</span><span class="sxs-lookup"><span data-stu-id="45f1c-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="45f1c-746">expression</span><span class="sxs-lookup"><span data-stu-id="45f1c-746">expression</span></span>|<span data-ttu-id="45f1c-747">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-747">Yes</span></span>|<span data-ttu-id="45f1c-748">string</span><span class="sxs-lookup"><span data-stu-id="45f1c-748">string</span></span>|<span data-ttu-id="45f1c-749">Hello expression tooevaluate après chaque itération</span><span class="sxs-lookup"><span data-stu-id="45f1c-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="45f1c-750">limit</span><span class="sxs-lookup"><span data-stu-id="45f1c-750">limit</span></span>|<span data-ttu-id="45f1c-751">yes</span><span class="sxs-lookup"><span data-stu-id="45f1c-751">yes</span></span>|<span data-ttu-id="45f1c-752">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-752">Object</span></span>|<span data-ttu-id="45f1c-753">limites de Hello pour boucle hello - au moins une limite doivent être définis.</span><span class="sxs-lookup"><span data-stu-id="45f1c-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="45f1c-754">count</span><span class="sxs-lookup"><span data-stu-id="45f1c-754">count</span></span>|<span data-ttu-id="45f1c-755">no</span><span class="sxs-lookup"><span data-stu-id="45f1c-755">no</span></span>|<span data-ttu-id="45f1c-756">int</span><span class="sxs-lookup"><span data-stu-id="45f1c-756">int</span></span>|<span data-ttu-id="45f1c-757">Hello limiter toohello le nombre d’itérations qui peuvent être effectuées.</span><span class="sxs-lookup"><span data-stu-id="45f1c-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="45f1c-758">timeout</span><span class="sxs-lookup"><span data-stu-id="45f1c-758">timeout</span></span>|<span data-ttu-id="45f1c-759">no</span><span class="sxs-lookup"><span data-stu-id="45f1c-759">no</span></span>|<span data-ttu-id="45f1c-760">string</span><span class="sxs-lookup"><span data-stu-id="45f1c-760">string</span></span>|<span data-ttu-id="45f1c-761">Bonjour délai d’expiration de la durée pendant laquelle il doit effectuer une boucle.</span><span class="sxs-lookup"><span data-stu-id="45f1c-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="45f1c-762">Format ISO 8601</span><span class="sxs-lookup"><span data-stu-id="45f1c-762">ISO 8601 format</span></span>|


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

## <a name="conditions---if-action"></a><span data-ttu-id="45f1c-763">Conditions : action If</span><span class="sxs-lookup"><span data-stu-id="45f1c-763">Conditions - If Action</span></span>

<span data-ttu-id="45f1c-764">Hello `If` action vous permet d’évaluer une condition et d’exécuter une branche en fonction de si hello expression prend la valeur trop`true`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="45f1c-765">Nom</span><span class="sxs-lookup"><span data-stu-id="45f1c-765">Name</span></span>|<span data-ttu-id="45f1c-766">Requis</span><span class="sxs-lookup"><span data-stu-id="45f1c-766">Required</span></span>|<span data-ttu-id="45f1c-767">Type</span><span class="sxs-lookup"><span data-stu-id="45f1c-767">Type</span></span>|<span data-ttu-id="45f1c-768">Description</span><span class="sxs-lookup"><span data-stu-id="45f1c-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="45f1c-769">actions</span><span class="sxs-lookup"><span data-stu-id="45f1c-769">actions</span></span>|<span data-ttu-id="45f1c-770">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-770">Yes</span></span>|<span data-ttu-id="45f1c-771">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-771">Object</span></span>|<span data-ttu-id="45f1c-772">Actions interne tooexecute lorsque l’expression renvoie la valeur trop`true`</span><span class="sxs-lookup"><span data-stu-id="45f1c-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="45f1c-773">expression</span><span class="sxs-lookup"><span data-stu-id="45f1c-773">expression</span></span>|<span data-ttu-id="45f1c-774">Oui</span><span class="sxs-lookup"><span data-stu-id="45f1c-774">Yes</span></span>|<span data-ttu-id="45f1c-775">string</span><span class="sxs-lookup"><span data-stu-id="45f1c-775">string</span></span>|<span data-ttu-id="45f1c-776">Hello expression tooevaluate</span><span class="sxs-lookup"><span data-stu-id="45f1c-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="45f1c-777">else</span><span class="sxs-lookup"><span data-stu-id="45f1c-777">else</span></span>|<span data-ttu-id="45f1c-778">no</span><span class="sxs-lookup"><span data-stu-id="45f1c-778">no</span></span>|<span data-ttu-id="45f1c-779">Object</span><span class="sxs-lookup"><span data-stu-id="45f1c-779">Object</span></span>|<span data-ttu-id="45f1c-780">Actions interne tooexecute lorsque l’expression renvoie la valeur trop`false`</span><span class="sxs-lookup"><span data-stu-id="45f1c-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
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
  
<span data-ttu-id="45f1c-781">Hello tableau suivant présente des exemples de conditions d’utilisation des expressions dans une action :</span><span class="sxs-lookup"><span data-stu-id="45f1c-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="45f1c-782">Valeur JSON</span><span class="sxs-lookup"><span data-stu-id="45f1c-782">JSON value</span></span>|<span data-ttu-id="45f1c-783">Résultat</span><span class="sxs-lookup"><span data-stu-id="45f1c-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="45f1c-784">Toute valeur qui est évalué tootrue entraîne toopass de cette condition.</span><span class="sxs-lookup"><span data-stu-id="45f1c-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="45f1c-785">Seules les expressions booléennes sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="45f1c-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="45f1c-786">tooconvert autres types tooBoolean, utiliser des fonctions `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="45f1c-787">Les fonctions de comparaison sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="45f1c-787">Comparison functions are supported.</span></span> <span data-ttu-id="45f1c-788">Par exemple hello ici, action de hello s’exécute uniquement lors de la sortie de hello d’act1 est supérieure au seuil de hello.</span><span class="sxs-lookup"><span data-stu-id="45f1c-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="45f1c-789">Fonctions logiques sont également pris en charge toocreate imbriqués expressions booléennes.</span><span class="sxs-lookup"><span data-stu-id="45f1c-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="45f1c-790">Dans ce cas, hello action est exécutée lors de la sortie de hello d’act1 est au-dessus du seuil de hello ou inférieure à 100.</span><span class="sxs-lookup"><span data-stu-id="45f1c-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="45f1c-791">Vous pouvez utiliser toocheck des fonctions de tableau si un tableau possède des éléments.</span><span class="sxs-lookup"><span data-stu-id="45f1c-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="45f1c-792">Dans ce cas, hello action est exécutée lorsque hello erreurs tableau est vide.</span><span class="sxs-lookup"><span data-stu-id="45f1c-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="45f1c-793">Erreur : cette condition n’est pas valide, car @ est requis pour les conditions.</span><span class="sxs-lookup"><span data-stu-id="45f1c-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="45f1c-794">Si une condition a la valeur avec succès, la condition de hello est marquée comme `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="45f1c-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="45f1c-795">Actions dans soit hello `actions` ou `else` objets évaluent trop`Succeeded` lors de l’exécution et a réussi, `Failed` lorsque exécutée et a échoué, ou `Skipped` lorsque cette branche n’est pas exécutée.</span><span class="sxs-lookup"><span data-stu-id="45f1c-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45f1c-796">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45f1c-796">Next steps</span></span>

[<span data-ttu-id="45f1c-797">API REST du service de workflow</span><span class="sxs-lookup"><span data-stu-id="45f1c-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
