---
title: aaaUsing OMS journal Analytique alerte REST API
description: "Hello journal Analytique alerte REST API vous permet de toocreate et gérer les alertes dans Analytique de journal qui fait partie d’Operations Management Suite (OMS).  Cet article fournit des détails de hello API et plusieurs exemples pour effectuer différentes opérations."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="480e4-104">Créer et gérer des règles d’alerte dans Log Analytics avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="480e4-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="480e4-105">Hello journal Analytique alerte REST API vous permet de toocreate et gérer les alertes Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="480e4-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="480e4-106">Cet article fournit des détails de hello API et plusieurs exemples pour effectuer différentes opérations.</span><span class="sxs-lookup"><span data-stu-id="480e4-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="480e4-107">Hello API REST de journal Analytique Search est RESTful et sont accessibles via les REST API Azure Resource Manager de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="480e4-108">Dans ce document vous trouverez des exemples où hello API est accessible à partir d’une ligne de commande PowerShell à l’aide [ARMClient](https://github.com/projectkudu/ARMClient), un outil de ligne de commande open source qui simplifie l’appel hello API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="480e4-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="480e4-109">utilisation de Hello d’ARMClient et de PowerShell est une des nombreuses options de tooaccess hello API de recherche Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="480e4-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="480e4-110">Grâce à ces outils, vous pouvez utiliser des espaces de travail hello API RESTful Azure Resource Manager toomake appelle tooOMS et exécuter des commandes de recherche de.</span><span class="sxs-lookup"><span data-stu-id="480e4-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="480e4-111">Hello API produira tooyou de résultats de recherche au format JSON, ce qui vous toouse résultats de la recherche hello de différentes façons par programme.</span><span class="sxs-lookup"><span data-stu-id="480e4-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="480e4-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="480e4-112">Prerequisites</span></span>
<span data-ttu-id="480e4-113">Actuellement, les alertes peuvent être créées uniquement avec une recherche enregistrée dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="480e4-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="480e4-114">Vous pouvez faire référence toohello [API REST de recherche journal](log-analytics-log-search-api.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="480e4-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="480e4-115">Planifications</span><span class="sxs-lookup"><span data-stu-id="480e4-115">Schedules</span></span>
<span data-ttu-id="480e4-116">Une recherche enregistrée peut avoir une ou plusieurs planifications.</span><span class="sxs-lookup"><span data-stu-id="480e4-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="480e4-117">Hello planification définit la fréquence à laquelle hello recherche est exécutée et intervalle de temps hello sur les critères de hello est identifiée.</span><span class="sxs-lookup"><span data-stu-id="480e4-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="480e4-118">Planifications ont des propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="480e4-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="480e4-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="480e4-119">Property</span></span> | <span data-ttu-id="480e4-120">Description</span><span class="sxs-lookup"><span data-stu-id="480e4-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="480e4-121">Intervalle</span><span class="sxs-lookup"><span data-stu-id="480e4-121">Interval</span></span> |<span data-ttu-id="480e4-122">La fréquence à laquelle hello recherche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="480e4-122">How often hello search is run.</span></span> <span data-ttu-id="480e4-123">Exprimée en minutes.</span><span class="sxs-lookup"><span data-stu-id="480e4-123">Measured in minutes.</span></span> |
| <span data-ttu-id="480e4-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="480e4-124">QueryTimeSpan</span></span> |<span data-ttu-id="480e4-125">intervalle de temps Hello sur quel hello critères est évaluée.</span><span class="sxs-lookup"><span data-stu-id="480e4-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="480e4-126">Doit être supérieure à intervalle égal tooor.</span><span class="sxs-lookup"><span data-stu-id="480e4-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="480e4-127">Exprimée en minutes.</span><span class="sxs-lookup"><span data-stu-id="480e4-127">Measured in minutes.</span></span> |
| <span data-ttu-id="480e4-128">Version</span><span class="sxs-lookup"><span data-stu-id="480e4-128">Version</span></span> |<span data-ttu-id="480e4-129">Hello version API utilisée.</span><span class="sxs-lookup"><span data-stu-id="480e4-129">hello API version being used.</span></span>  <span data-ttu-id="480e4-130">Actuellement, il doit toujours être défini too1.</span><span class="sxs-lookup"><span data-stu-id="480e4-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="480e4-131">Par exemple, considérez une requête d’événement avec Interval défini sur 15 minutes et QueryTimeSpan sur 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="480e4-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="480e4-132">Dans ce cas, les requêtes hello sont exécuté toutes les 15 minutes, et se déclenchera une alerte si les critères de hello suite tooresolve tootrue sur un intervalle de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="480e4-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="480e4-133">Récupération des planifications</span><span class="sxs-lookup"><span data-stu-id="480e4-133">Retrieving schedules</span></span>
<span data-ttu-id="480e4-134">Méthode tooretrieve d’obtenir hello d’utiliser toutes les planifications d’une recherche enregistrée.</span><span class="sxs-lookup"><span data-stu-id="480e4-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="480e4-135">Hello d’utilisation Get (méthode) avec un tooretrieve ID de planification une planification particulière d’une recherche enregistrée.</span><span class="sxs-lookup"><span data-stu-id="480e4-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="480e4-136">Voici un exemple de réponse pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="480e4-137">Création d'une planification</span><span class="sxs-lookup"><span data-stu-id="480e4-137">Creating a schedule</span></span>
<span data-ttu-id="480e4-138">Utilisez la méthode de Put de hello avec un toocreate ID de planification unique une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="480e4-139">Notez que deux planifications ne peut pas avoir hello même ID même s’ils sont associés avec différentes recherches enregistrées.</span><span class="sxs-lookup"><span data-stu-id="480e4-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="480e4-140">Lorsque vous créez une planification dans la console OMS hello, un GUID est créé pour l’ID de planification hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="480e4-141">nom de Hello pour toutes les recherches enregistrées, planifications et créées par hello API Analytique de journal des actions doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="480e4-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="480e4-142">Modification d’une planification</span><span class="sxs-lookup"><span data-stu-id="480e4-142">Editing a schedule</span></span>
<span data-ttu-id="480e4-143">Utilisez la méthode de Put de hello avec une planification existante ID pour hello même enregistrée rechercher toomodify planifier.</span><span class="sxs-lookup"><span data-stu-id="480e4-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="480e4-144">corps de Hello de demande de hello doit inclure etag hello de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="480e4-145">Suppression de planifications</span><span class="sxs-lookup"><span data-stu-id="480e4-145">Deleting schedules</span></span>
<span data-ttu-id="480e4-146">Utilisez la méthode de suppression de hello avec un toodelete ID de planification une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="480e4-147">Actions</span><span class="sxs-lookup"><span data-stu-id="480e4-147">Actions</span></span>
<span data-ttu-id="480e4-148">Une planification peut avoir plusieurs actions.</span><span class="sxs-lookup"><span data-stu-id="480e4-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="480e4-149">Une action peut définir un ou plusieurs tooperform de processus tels que l’envoi d’un message électronique ou le démarrage d’un runbook, ou elle peut définir un seuil qui détermine quand des résultats d’une recherche hello correspondent à certains critères.</span><span class="sxs-lookup"><span data-stu-id="480e4-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="480e4-150">Certaines actions à la fois définirez afin que le processus de hello sont effectuées lorsque hello seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="480e4-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="480e4-151">Toutes les actions ont des propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="480e4-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="480e4-152">Différents types d’alertes ont différentes propriétés supplémentaires qui sont décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="480e4-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="480e4-153">Propriété</span><span class="sxs-lookup"><span data-stu-id="480e4-153">Property</span></span> | <span data-ttu-id="480e4-154">Description</span><span class="sxs-lookup"><span data-stu-id="480e4-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="480e4-155">Type</span><span class="sxs-lookup"><span data-stu-id="480e4-155">Type</span></span> |<span data-ttu-id="480e4-156">Type d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-156">Type of hello action.</span></span>  <span data-ttu-id="480e4-157">Actuellement, les valeurs possibles de hello sont alerte et Webhook.</span><span class="sxs-lookup"><span data-stu-id="480e4-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="480e4-158">Nom</span><span class="sxs-lookup"><span data-stu-id="480e4-158">Name</span></span> |<span data-ttu-id="480e4-159">Nom complet de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="480e4-160">Version</span><span class="sxs-lookup"><span data-stu-id="480e4-160">Version</span></span> |<span data-ttu-id="480e4-161">Hello version API utilisée.</span><span class="sxs-lookup"><span data-stu-id="480e4-161">hello API version being used.</span></span>  <span data-ttu-id="480e4-162">Actuellement, il doit toujours être défini too1.</span><span class="sxs-lookup"><span data-stu-id="480e4-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="480e4-163">Récupération des actions</span><span class="sxs-lookup"><span data-stu-id="480e4-163">Retrieving actions</span></span>
<span data-ttu-id="480e4-164">Méthode tooretrieve d’obtenir hello d’utiliser toutes les actions pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="480e4-165">Hello d’utilisation Get (méthode) avec hello action ID tooretrieve une action particulière pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="480e4-166">Création ou modification des actions</span><span class="sxs-lookup"><span data-stu-id="480e4-166">Creating or editing actions</span></span>
<span data-ttu-id="480e4-167">Utilisez la méthode de Put de hello avec un ID d’action qui est unique toohello planification toocreate une nouvelle action.</span><span class="sxs-lookup"><span data-stu-id="480e4-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="480e4-168">Lorsque vous créez une action dans la console OMS hello, un GUID est pour le code d’action hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="480e4-169">nom de Hello pour toutes les recherches enregistrées, planifications et créées par hello API Analytique de journal des actions doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="480e4-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="480e4-170">Utiliser la méthode Put de hello avec un ID pour hello même enregistrée rechercher toomodify planifier des actions existant.</span><span class="sxs-lookup"><span data-stu-id="480e4-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="480e4-171">corps de Hello de demande de hello doit inclure etag hello de planification de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="480e4-172">format de demande Hello pour la création d’une nouvelle action varie selon le type d’action pour ces exemples sont fournis dans les sections hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="480e4-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="480e4-173">Suppression des actions</span><span class="sxs-lookup"><span data-stu-id="480e4-173">Deleting actions</span></span>
<span data-ttu-id="480e4-174">Utilisez la méthode de suppression de hello avec hello action ID toodelete une action.</span><span class="sxs-lookup"><span data-stu-id="480e4-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="480e4-175">Actions d’alerte</span><span class="sxs-lookup"><span data-stu-id="480e4-175">Alert Actions</span></span>
<span data-ttu-id="480e4-176">Une planification doit avoir une, et une seule, action d’alerte.</span><span class="sxs-lookup"><span data-stu-id="480e4-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="480e4-177">Actions d’alerte ont un ou plusieurs des sections hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="480e4-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="480e4-178">Chacune est décrite plus en détail ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="480e4-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="480e4-179">Section</span><span class="sxs-lookup"><span data-stu-id="480e4-179">Section</span></span> | <span data-ttu-id="480e4-180">Description</span><span class="sxs-lookup"><span data-stu-id="480e4-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="480e4-181">Seuil</span><span class="sxs-lookup"><span data-stu-id="480e4-181">Threshold</span></span> |<span data-ttu-id="480e4-182">Critères quand l’action de hello est exécuté.</span><span class="sxs-lookup"><span data-stu-id="480e4-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="480e4-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="480e4-183">EmailNotification</span></span> |<span data-ttu-id="480e4-184">Envoyer des messages toomultiple destinataires.</span><span class="sxs-lookup"><span data-stu-id="480e4-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="480e4-185">Correction</span><span class="sxs-lookup"><span data-stu-id="480e4-185">Remediation</span></span> |<span data-ttu-id="480e4-186">Démarrer un runbook dans Azure Automation tooattempt toocorrect identifié le problème.</span><span class="sxs-lookup"><span data-stu-id="480e4-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="480e4-187">Seuils</span><span class="sxs-lookup"><span data-stu-id="480e4-187">Thresholds</span></span>
<span data-ttu-id="480e4-188">Une action d’alerte ne doit avoir qu’un seul seuil.</span><span class="sxs-lookup"><span data-stu-id="480e4-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="480e4-189">Lorsque des résultats d’une recherche enregistrée hello correspondent seuil hello dans une action associée à cette recherche, tous les autres processus dans cette action sont exécutés.</span><span class="sxs-lookup"><span data-stu-id="480e4-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="480e4-190">En outre, une action peut ne contenir qu’un seuil et être ainsi utilisable avec d’autres types d’actions ne comportant pas de seuils.</span><span class="sxs-lookup"><span data-stu-id="480e4-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="480e4-191">Seuils ont des propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="480e4-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="480e4-192">Propriété</span><span class="sxs-lookup"><span data-stu-id="480e4-192">Property</span></span> | <span data-ttu-id="480e4-193">Description</span><span class="sxs-lookup"><span data-stu-id="480e4-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="480e4-194">Operator</span><span class="sxs-lookup"><span data-stu-id="480e4-194">Operator</span></span> |<span data-ttu-id="480e4-195">Opérateur de comparaison des seuils hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="480e4-196">gt = supérieur à</span><span class="sxs-lookup"><span data-stu-id="480e4-196">gt = Greater Than</span></span> <br> <span data-ttu-id="480e4-197">lt = inférieur à</span><span class="sxs-lookup"><span data-stu-id="480e4-197">lt = Less Than</span></span> |
| <span data-ttu-id="480e4-198">Valeur</span><span class="sxs-lookup"><span data-stu-id="480e4-198">Value</span></span> |<span data-ttu-id="480e4-199">Valeur de seuil de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-199">Value for hello threshold.</span></span> |

<span data-ttu-id="480e4-200">Par exemple, considérez une requête d’événement avec Interval défini sur 15 minutes, QueryTimeSpan sur 30 minutes et Threshold sur une valeur supérieure à 10.</span><span class="sxs-lookup"><span data-stu-id="480e4-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="480e4-201">Dans ce cas, les requêtes hello sont exécuté toutes les 15 minutes, et se déclenchera une alerte si elle a retourné les 10 événements qui ont été créés sur un intervalle de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="480e4-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="480e4-202">Voici un exemple de réponse pour une action comportant uniquement un seuil.</span><span class="sxs-lookup"><span data-stu-id="480e4-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="480e4-203">Utilisez hello Put méthode avec un toocreate d’ID unique d’action une nouvelle action de seuil pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="480e4-204">Utilisez hello Put méthode avec une toomodify d’ID action existante une action de seuil pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="480e4-205">corps de Hello de demande de hello doit inclure etag hello d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="480e4-206">Notification par courrier électronique</span><span class="sxs-lookup"><span data-stu-id="480e4-206">Email Notification</span></span>
<span data-ttu-id="480e4-207">Envoient des Notifications par courrier électronique tooone de messagerie ou d’autres destinataires.</span><span class="sxs-lookup"><span data-stu-id="480e4-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="480e4-208">Elles incluent des propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="480e4-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="480e4-209">Propriété</span><span class="sxs-lookup"><span data-stu-id="480e4-209">Property</span></span> | <span data-ttu-id="480e4-210">Description</span><span class="sxs-lookup"><span data-stu-id="480e4-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="480e4-211">Recipients</span><span class="sxs-lookup"><span data-stu-id="480e4-211">Recipients</span></span> |<span data-ttu-id="480e4-212">Liste d’adresses de messagerie.</span><span class="sxs-lookup"><span data-stu-id="480e4-212">List of mail addresses.</span></span> |
| <span data-ttu-id="480e4-213">Objet</span><span class="sxs-lookup"><span data-stu-id="480e4-213">Subject</span></span> |<span data-ttu-id="480e4-214">objet de Hello de message de salutation.</span><span class="sxs-lookup"><span data-stu-id="480e4-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="480e4-215">Pièce jointe</span><span class="sxs-lookup"><span data-stu-id="480e4-215">Attachment</span></span> |<span data-ttu-id="480e4-216">Les pièces jointes n’étant pas actuellement prises en charge, cette propriété est toujours définie sur « None ».</span><span class="sxs-lookup"><span data-stu-id="480e4-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="480e4-217">Voici un exemple de réponse pour une action de notification par courrier électronique comportant un seuil.</span><span class="sxs-lookup"><span data-stu-id="480e4-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="480e4-218">Utilisez hello Put méthode avec un toocreate d’ID unique d’action une nouvelle action de courrier électronique pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="480e4-219">Hello exemple suivant crée une notification par courrier électronique avec un seuil pour les messages hello sont envoyé lorsque les résultats de hello Hello recherche enregistrée dépassent le seuil de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="480e4-220">Utilisez hello Put méthode avec une toomodify d’ID action existante une action de courrier électronique pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="480e4-221">corps de Hello de demande de hello doit inclure etag hello d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="480e4-222">Actions de correction</span><span class="sxs-lookup"><span data-stu-id="480e4-222">Remediation actions</span></span>
<span data-ttu-id="480e4-223">Corrections de démarrer un runbook dans Azure Automation qui tente de problème de hello toocorrect identifié par l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="480e4-224">Vous devez créer un webhook pour runbook hello utilisé dans une action de mise à jour, puis spécifiez hello URI Bonjour WebhookUri propriété.</span><span class="sxs-lookup"><span data-stu-id="480e4-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="480e4-225">Lorsque vous créez cette action à l’aide de la console OMS de hello, un nouveau webhook est automatiquement créé pour hello runbook.</span><span class="sxs-lookup"><span data-stu-id="480e4-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="480e4-226">Des corrections incluent les propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="480e4-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="480e4-227">Propriété</span><span class="sxs-lookup"><span data-stu-id="480e4-227">Property</span></span> | <span data-ttu-id="480e4-228">Description</span><span class="sxs-lookup"><span data-stu-id="480e4-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="480e4-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="480e4-229">RunbookName</span></span> |<span data-ttu-id="480e4-230">Nom du runbook de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-230">Name of hello runbook.</span></span> <span data-ttu-id="480e4-231">Cela doit correspondre à un runbook publié dans le compte d’automatisation hello configuré Bonjour Solution Automation dans votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="480e4-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="480e4-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="480e4-232">WebhookUri</span></span> |<span data-ttu-id="480e4-233">URI de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="480e4-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="480e4-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="480e4-234">Expiry</span></span> |<span data-ttu-id="480e4-235">date d’expiration de Hello et l’heure de hello webhook.</span><span class="sxs-lookup"><span data-stu-id="480e4-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="480e4-236">Si hello webhook n’a pas un délai d’expiration, cela peut être une date future valide.</span><span class="sxs-lookup"><span data-stu-id="480e4-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="480e4-237">Voici un exemple de réponse pour une action de correction comportant un seuil.</span><span class="sxs-lookup"><span data-stu-id="480e4-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="480e4-238">Utilisez hello Put méthode avec un toocreate d’ID unique d’action une nouvelle action de mise à jour pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="480e4-239">Hello exemple suivant crée une mise à jour avec un seuil hello runbook est démarré lorsque les résultats de hello Hello recherche enregistrée dépassent le seuil de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="480e4-240">Utilisez hello Put méthode avec une toomodify d’ID action existante une action de mise à jour pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="480e4-241">corps de Hello de demande de hello doit inclure etag hello d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="480e4-242">Exemple</span><span class="sxs-lookup"><span data-stu-id="480e4-242">Example</span></span>
<span data-ttu-id="480e4-243">Voici un exemple complet de toocreate une alerte par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="480e4-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="480e4-244">Cet exemple crée une planification avec une action qui contient un seuil et un e-mail.</span><span class="sxs-lookup"><span data-stu-id="480e4-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="480e4-245">Actions de webhook</span><span class="sxs-lookup"><span data-stu-id="480e4-245">Webhook actions</span></span>
<span data-ttu-id="480e4-246">Les actions Webhook démarrer un processus en appelant une URL et éventuellement en fournissant un toobe de charge utile envoyée.</span><span class="sxs-lookup"><span data-stu-id="480e4-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="480e4-247">Ils sont des actions tooRemediation similaires à ceci près qu’ils sont destinés à webhooks qui peut appeler des processus autres que les runbooks Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="480e4-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="480e4-248">Elles fournissent également hello option supplémentaire permettant de fournir un processus à distance de charge utile toobe remis toohello.</span><span class="sxs-lookup"><span data-stu-id="480e4-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="480e4-249">Les actions Webhook n’ont pas d’un seuil, mais au lieu de cela doivent être ajoutées planification tooa qui a une action avec un seuil d’alerte.</span><span class="sxs-lookup"><span data-stu-id="480e4-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="480e4-250">Vous pouvez ajouter plusieurs actions Webhook qui seront toutes exécutées lorsque hello seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="480e4-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="480e4-251">Les actions Webhook incluent les propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="480e4-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="480e4-252">Propriété</span><span class="sxs-lookup"><span data-stu-id="480e4-252">Property</span></span> | <span data-ttu-id="480e4-253">Description</span><span class="sxs-lookup"><span data-stu-id="480e4-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="480e4-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="480e4-254">WebhookUri</span></span> |<span data-ttu-id="480e4-255">objet de Hello de message de salutation.</span><span class="sxs-lookup"><span data-stu-id="480e4-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="480e4-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="480e4-256">CustomPayload</span></span> |<span data-ttu-id="480e4-257">Charge utile personnalisée toobe envoyé toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="480e4-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="480e4-258">format de Hello dépend de quelles webhook hello est attendu.</span><span class="sxs-lookup"><span data-stu-id="480e4-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="480e4-259">Voici un exemple de réponse pour l’action webhook et une action d’alerte associée comportant un seuil.</span><span class="sxs-lookup"><span data-stu-id="480e4-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="480e4-260">Créer ou modifier une action de webhook</span><span class="sxs-lookup"><span data-stu-id="480e4-260">Create or edit a webhook action</span></span>
<span data-ttu-id="480e4-261">Utilisez hello Put méthode avec un toocreate d’ID unique d’action une nouvelle action de webhook pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="480e4-262">Hello exemple suivant crée une action de Webhook et une action d’alerte avec un seuil afin que hello webhook est déclenchée lorsque les résultats de hello Hello recherche enregistrée dépassent le seuil de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="480e4-263">Utilisez hello Put méthode avec une toomodify d’ID action existante une action de webhook pour une planification.</span><span class="sxs-lookup"><span data-stu-id="480e4-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="480e4-264">corps de Hello de demande de hello doit inclure etag hello d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="480e4-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="480e4-265">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="480e4-265">Next steps</span></span>
* <span data-ttu-id="480e4-266">Hello d’utilisation [API REST des recherches de journaux tooperform](log-analytics-log-search-api.md) dans le journal Analytique.</span><span class="sxs-lookup"><span data-stu-id="480e4-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

