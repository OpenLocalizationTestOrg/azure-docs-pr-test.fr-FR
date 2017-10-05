---
title: "Utilisation de l’API REST d’alerte Log Analytics OMS"
description: "L’API REST d’alerte Log Analytics vous permet de créer et de gérer des alertes dans Log Analytics, qui fait partie d’Operations Management Suite (OMS).  Cet article fournit des détails sur l’API et plusieurs exemples pour effectuer différentes opérations."
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
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="4275d-104">Créer et gérer des règles d’alerte dans Log Analytics avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="4275d-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="4275d-105">L’API REST d’alerte Log Analytics vous permet de créer et de gérer des alertes dans Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="4275d-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="4275d-106">Cet article fournit des détails sur l’API et plusieurs exemples pour effectuer différentes opérations.</span><span class="sxs-lookup"><span data-stu-id="4275d-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="4275d-107">L’API REST de recherche Log Analytics est un service RESTful qui est accessible par le biais de l’API REST Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4275d-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="4275d-108">Ce document présente des exemples montrant comment accéder à l’API à partir d’une ligne de commande PowerShell en utilisant [ARMClient](https://github.com/projectkudu/ARMClient), outil en ligne de commande open source qui simplifie l’appel de l’API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4275d-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="4275d-109">L'utilisation d’ARMClient et de PowerShell est une des nombreuses options vous permettant d’accéder à l'API de recherche Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4275d-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="4275d-110">Grâce à ces outils, vous pouvez utiliser l'API RESTful Azure Resource Manager pour effectuer des appels vers les espaces de travail OMS et exécuter en leur sein des commandes de recherche.</span><span class="sxs-lookup"><span data-stu-id="4275d-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="4275d-111">L'API produira pour vous des résultats de recherche au format JSON, qui vous permet d'utiliser ces résultats, par programme, de différentes manières.</span><span class="sxs-lookup"><span data-stu-id="4275d-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4275d-112">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="4275d-112">Prerequisites</span></span>
<span data-ttu-id="4275d-113">Actuellement, les alertes peuvent être créées uniquement avec une recherche enregistrée dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4275d-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="4275d-114">Vous pouvez consulter l’ [API REST de recherche de journal](log-analytics-log-search-api.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4275d-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="4275d-115">Planifications</span><span class="sxs-lookup"><span data-stu-id="4275d-115">Schedules</span></span>
<span data-ttu-id="4275d-116">Une recherche enregistrée peut avoir une ou plusieurs planifications.</span><span class="sxs-lookup"><span data-stu-id="4275d-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="4275d-117">La planification définit la fréquence à laquelle la recherche est exécutée et l’intervalle de temps pendant lequel les critères sont identifiés.</span><span class="sxs-lookup"><span data-stu-id="4275d-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="4275d-118">Les propriétés des planifications sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="4275d-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="4275d-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="4275d-119">Property</span></span> | <span data-ttu-id="4275d-120">Description</span><span class="sxs-lookup"><span data-stu-id="4275d-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4275d-121">Intervalle</span><span class="sxs-lookup"><span data-stu-id="4275d-121">Interval</span></span> |<span data-ttu-id="4275d-122">Fréquence à laquelle la recherche est exécutée.</span><span class="sxs-lookup"><span data-stu-id="4275d-122">How often the search is run.</span></span> <span data-ttu-id="4275d-123">Exprimée en minutes.</span><span class="sxs-lookup"><span data-stu-id="4275d-123">Measured in minutes.</span></span> |
| <span data-ttu-id="4275d-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="4275d-124">QueryTimeSpan</span></span> |<span data-ttu-id="4275d-125">Intervalle de temps pendant lequel les critères sont évalués.</span><span class="sxs-lookup"><span data-stu-id="4275d-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="4275d-126">Doit être égal ou supérieur à Interval.</span><span class="sxs-lookup"><span data-stu-id="4275d-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="4275d-127">Exprimée en minutes.</span><span class="sxs-lookup"><span data-stu-id="4275d-127">Measured in minutes.</span></span> |
| <span data-ttu-id="4275d-128">Version</span><span class="sxs-lookup"><span data-stu-id="4275d-128">Version</span></span> |<span data-ttu-id="4275d-129">Version de l’API utilisée.</span><span class="sxs-lookup"><span data-stu-id="4275d-129">The API version being used.</span></span>  <span data-ttu-id="4275d-130">Actuellement, cette propriété doit toujours être définie sur 1.</span><span class="sxs-lookup"><span data-stu-id="4275d-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="4275d-131">Par exemple, considérez une requête d’événement avec Interval défini sur 15 minutes et QueryTimeSpan sur 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="4275d-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="4275d-132">Dans ce cas, la requête est exécutée toutes les 15 minutes et une alerte se déclenche si les critères sont satisfaits pendant un intervalle de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="4275d-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="4275d-133">Récupération des planifications</span><span class="sxs-lookup"><span data-stu-id="4275d-133">Retrieving schedules</span></span>
<span data-ttu-id="4275d-134">Utilisez la méthode Get pour extraire toutes les planifications d’une recherche enregistrée.</span><span class="sxs-lookup"><span data-stu-id="4275d-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="4275d-135">Utilisez la méthode Get avec un ID de planification pour extraire une planification particulière pour une recherche enregistrée.</span><span class="sxs-lookup"><span data-stu-id="4275d-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="4275d-136">Voici un exemple de réponse pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="4275d-137">Création d'une planification</span><span class="sxs-lookup"><span data-stu-id="4275d-137">Creating a schedule</span></span>
<span data-ttu-id="4275d-138">Utilisez la méthode Put avec un ID de planification unique pour créer une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="4275d-139">Notez que deux planifications ne peuvent pas avoir le même ID, même si elles sont associées à d’autres recherches enregistrées.</span><span class="sxs-lookup"><span data-stu-id="4275d-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="4275d-140">Quand vous créez une planification dans la console OMS, un GUID est créé pour l’ID de la planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="4275d-141">Le nom de l’ensemble des recherches enregistrées, des planifications et des actions créées avec l’API Log Analytics doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="4275d-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="4275d-142">Modification d’une planification</span><span class="sxs-lookup"><span data-stu-id="4275d-142">Editing a schedule</span></span>
<span data-ttu-id="4275d-143">Utilisez la méthode Put avec un ID de planification existant pour la même recherche enregistrée afin de modifier cette planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="4275d-144">Le corps de la demande doit inclure l’ETag de la planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="4275d-145">Suppression de planifications</span><span class="sxs-lookup"><span data-stu-id="4275d-145">Deleting schedules</span></span>
<span data-ttu-id="4275d-146">Pour supprimer une planification, utilisez la méthode Delete avec un ID de planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="4275d-147">Actions</span><span class="sxs-lookup"><span data-stu-id="4275d-147">Actions</span></span>
<span data-ttu-id="4275d-148">Une planification peut avoir plusieurs actions.</span><span class="sxs-lookup"><span data-stu-id="4275d-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="4275d-149">Une action peut définir un ou plusieurs processus à effectuer, tels que l’envoi d’un courrier électronique ou le démarrage d’un runbook, ou elle peut définir un seuil qui détermine si les résultats d’une recherche satisfont à certains critères.</span><span class="sxs-lookup"><span data-stu-id="4275d-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="4275d-150">Certaines actions définissent ces deux aspects afin que les processus soient exécutés quand le seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="4275d-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="4275d-151">Toutes les actions des planifications sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="4275d-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="4275d-152">Différents types d’alertes ont différentes propriétés supplémentaires qui sont décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4275d-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="4275d-153">Propriété</span><span class="sxs-lookup"><span data-stu-id="4275d-153">Property</span></span> | <span data-ttu-id="4275d-154">Description</span><span class="sxs-lookup"><span data-stu-id="4275d-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4275d-155">Type</span><span class="sxs-lookup"><span data-stu-id="4275d-155">Type</span></span> |<span data-ttu-id="4275d-156">Type de l’action.</span><span class="sxs-lookup"><span data-stu-id="4275d-156">Type of the action.</span></span>  <span data-ttu-id="4275d-157">Actuellement, les valeurs possibles sont Alert et Webhook.</span><span class="sxs-lookup"><span data-stu-id="4275d-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="4275d-158">Nom</span><span class="sxs-lookup"><span data-stu-id="4275d-158">Name</span></span> |<span data-ttu-id="4275d-159">Nom d’affichage de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="4275d-159">Display name for the alert.</span></span> |
| <span data-ttu-id="4275d-160">Version</span><span class="sxs-lookup"><span data-stu-id="4275d-160">Version</span></span> |<span data-ttu-id="4275d-161">Version de l’API utilisée.</span><span class="sxs-lookup"><span data-stu-id="4275d-161">The API version being used.</span></span>  <span data-ttu-id="4275d-162">Actuellement, cette propriété doit toujours être définie sur 1.</span><span class="sxs-lookup"><span data-stu-id="4275d-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="4275d-163">Récupération des actions</span><span class="sxs-lookup"><span data-stu-id="4275d-163">Retrieving actions</span></span>
<span data-ttu-id="4275d-164">Utilisez la méthode Get pour récupérer toutes les actions d’une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-164">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="4275d-165">Utilisez la méthode Get avec l’ID d’action pour récupérer une action particulière d’une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-165">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="4275d-166">Création ou modification des actions</span><span class="sxs-lookup"><span data-stu-id="4275d-166">Creating or editing actions</span></span>
<span data-ttu-id="4275d-167">Utilisez la méthode Put avec un ID d’action propre à la planification pour créer une activité.</span><span class="sxs-lookup"><span data-stu-id="4275d-167">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="4275d-168">Quand vous créez une action dans la console OMS, un GUID est défini pour l’ID d’action.</span><span class="sxs-lookup"><span data-stu-id="4275d-168">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="4275d-169">Le nom de l’ensemble des recherches enregistrées, des planifications et des actions créées avec l’API Log Analytics doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="4275d-169">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="4275d-170">Utilisez la méthode Put avec un ID d’action existant pour la même recherche enregistrée afin de modifier cette planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-170">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="4275d-171">Le corps de la demande doit inclure l’ETag de la planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-171">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="4275d-172">Le format de demande pour la création d’une action variant selon le type d’action, des exemples sont fournis dans les sections ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4275d-172">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="4275d-173">Suppression des actions</span><span class="sxs-lookup"><span data-stu-id="4275d-173">Deleting actions</span></span>
<span data-ttu-id="4275d-174">Utilisez la méthode Delete avec l’ID d’action pour supprimer une action.</span><span class="sxs-lookup"><span data-stu-id="4275d-174">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="4275d-175">Actions d’alerte</span><span class="sxs-lookup"><span data-stu-id="4275d-175">Alert Actions</span></span>
<span data-ttu-id="4275d-176">Une planification doit avoir une, et une seule, action d’alerte.</span><span class="sxs-lookup"><span data-stu-id="4275d-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="4275d-177">Les actions d’alerte ont une ou plusieurs des sections indiquées dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="4275d-177">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="4275d-178">Chacune est décrite plus en détail ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4275d-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="4275d-179">Section</span><span class="sxs-lookup"><span data-stu-id="4275d-179">Section</span></span> | <span data-ttu-id="4275d-180">Description</span><span class="sxs-lookup"><span data-stu-id="4275d-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4275d-181">Seuil</span><span class="sxs-lookup"><span data-stu-id="4275d-181">Threshold</span></span> |<span data-ttu-id="4275d-182">Critères d’exécution de l’action.</span><span class="sxs-lookup"><span data-stu-id="4275d-182">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="4275d-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="4275d-183">EmailNotification</span></span> |<span data-ttu-id="4275d-184">Envoyer des messages à plusieurs destinataires.</span><span class="sxs-lookup"><span data-stu-id="4275d-184">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="4275d-185">Correction</span><span class="sxs-lookup"><span data-stu-id="4275d-185">Remediation</span></span> |<span data-ttu-id="4275d-186">Démarrer un runbook dans Azure Automation pour tenter de résoudre le problème identifié.</span><span class="sxs-lookup"><span data-stu-id="4275d-186">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="4275d-187">Seuils</span><span class="sxs-lookup"><span data-stu-id="4275d-187">Thresholds</span></span>
<span data-ttu-id="4275d-188">Une action d’alerte ne doit avoir qu’un seul seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="4275d-189">Quand les résultats d’une recherche enregistrée correspondent au seuil dans une action associée à cette recherche, tous les autres processus dans cette action sont exécutés.</span><span class="sxs-lookup"><span data-stu-id="4275d-189">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="4275d-190">En outre, une action peut ne contenir qu’un seuil et être ainsi utilisable avec d’autres types d’actions ne comportant pas de seuils.</span><span class="sxs-lookup"><span data-stu-id="4275d-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="4275d-191">Les propriétés des seuils sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="4275d-191">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="4275d-192">Propriété</span><span class="sxs-lookup"><span data-stu-id="4275d-192">Property</span></span> | <span data-ttu-id="4275d-193">Description</span><span class="sxs-lookup"><span data-stu-id="4275d-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4275d-194">Opérateur </span><span class="sxs-lookup"><span data-stu-id="4275d-194">Operator</span></span> |<span data-ttu-id="4275d-195">Opérateur de comparaison de seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-195">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="4275d-196">gt = supérieur à</span><span class="sxs-lookup"><span data-stu-id="4275d-196">gt = Greater Than</span></span> <br> <span data-ttu-id="4275d-197">lt = inférieur à</span><span class="sxs-lookup"><span data-stu-id="4275d-197">lt = Less Than</span></span> |
| <span data-ttu-id="4275d-198">Valeur</span><span class="sxs-lookup"><span data-stu-id="4275d-198">Value</span></span> |<span data-ttu-id="4275d-199">Valeur du seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-199">Value for the threshold.</span></span> |

<span data-ttu-id="4275d-200">Par exemple, considérez une requête d’événement avec Interval défini sur 15 minutes, QueryTimeSpan sur 30 minutes et Threshold sur une valeur supérieure à 10.</span><span class="sxs-lookup"><span data-stu-id="4275d-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="4275d-201">Dans ce cas, la requête est exécutée toutes les 15 minutes et une alerte se déclenche si la requête retourne 10 événements créés en l’espace de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="4275d-201">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="4275d-202">Voici un exemple de réponse pour une action comportant uniquement un seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="4275d-203">Utilisez la méthode Put avec un ID d’action unique pour créer une action de seuil pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-203">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="4275d-204">Utilisez la méthode Put avec un ID d’action existant pour modifier une action de seuil pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-204">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="4275d-205">Le corps de la demande doit inclure l’ETag de l’action.</span><span class="sxs-lookup"><span data-stu-id="4275d-205">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="4275d-206">Notification par courrier électronique</span><span class="sxs-lookup"><span data-stu-id="4275d-206">Email Notification</span></span>
<span data-ttu-id="4275d-207">Les notifications par courrier électronique envoient un e-mail à un ou plusieurs destinataires.</span><span class="sxs-lookup"><span data-stu-id="4275d-207">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="4275d-208">Leurs propriétés sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="4275d-208">They include the properties in the following table.</span></span>

| <span data-ttu-id="4275d-209">Propriété</span><span class="sxs-lookup"><span data-stu-id="4275d-209">Property</span></span> | <span data-ttu-id="4275d-210">Description</span><span class="sxs-lookup"><span data-stu-id="4275d-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4275d-211">Recipients</span><span class="sxs-lookup"><span data-stu-id="4275d-211">Recipients</span></span> |<span data-ttu-id="4275d-212">Liste d’adresses de messagerie.</span><span class="sxs-lookup"><span data-stu-id="4275d-212">List of mail addresses.</span></span> |
| <span data-ttu-id="4275d-213">Objet</span><span class="sxs-lookup"><span data-stu-id="4275d-213">Subject</span></span> |<span data-ttu-id="4275d-214">Objet de l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="4275d-214">The subject of the mail.</span></span> |
| <span data-ttu-id="4275d-215">Pièce jointe</span><span class="sxs-lookup"><span data-stu-id="4275d-215">Attachment</span></span> |<span data-ttu-id="4275d-216">Les pièces jointes n’étant pas actuellement prises en charge, cette propriété est toujours définie sur « None ».</span><span class="sxs-lookup"><span data-stu-id="4275d-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="4275d-217">Voici un exemple de réponse pour une action de notification par courrier électronique comportant un seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="4275d-218">Utilisez la méthode Put avec un ID d’action unique pour créer une action de messagerie pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-218">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="4275d-219">L’exemple suivant crée une notification par courrier électronique avec un seuil afin que l’e-mail soit envoyé quand les résultats de la recherche enregistrée dépassent le seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-219">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="4275d-220">Utilisez la méthode Put avec un ID d’action existant pour modifier une action de messagerie pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-220">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="4275d-221">Le corps de la demande doit inclure l’ETag de l’action.</span><span class="sxs-lookup"><span data-stu-id="4275d-221">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="4275d-222">Actions de correction</span><span class="sxs-lookup"><span data-stu-id="4275d-222">Remediation actions</span></span>
<span data-ttu-id="4275d-223">Les corrections démarrent un runbook dans Azure Automation qui essaie de corriger le problème identifié par l’alerte.</span><span class="sxs-lookup"><span data-stu-id="4275d-223">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="4275d-224">Vous devez créer un webhook pour le runbook utilisé dans une action de correction, puis spécifier l’URI dans la propriété WebhookUri.</span><span class="sxs-lookup"><span data-stu-id="4275d-224">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="4275d-225">Quand vous créez cette action à l’aide de la console OMS, un webhook est automatiquement créé pour le runbook.</span><span class="sxs-lookup"><span data-stu-id="4275d-225">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="4275d-226">Les propriétés des corrections sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="4275d-226">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="4275d-227">Propriété</span><span class="sxs-lookup"><span data-stu-id="4275d-227">Property</span></span> | <span data-ttu-id="4275d-228">Description</span><span class="sxs-lookup"><span data-stu-id="4275d-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4275d-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="4275d-229">RunbookName</span></span> |<span data-ttu-id="4275d-230">Nom du runbook.</span><span class="sxs-lookup"><span data-stu-id="4275d-230">Name of the runbook.</span></span> <span data-ttu-id="4275d-231">Il doit correspondre à un runbook publié dans le compte automation configuré dans la solution Automation au sein de votre espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="4275d-231">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="4275d-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="4275d-232">WebhookUri</span></span> |<span data-ttu-id="4275d-233">URI du webhook.</span><span class="sxs-lookup"><span data-stu-id="4275d-233">URI of the webhook.</span></span> |
| <span data-ttu-id="4275d-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="4275d-234">Expiry</span></span> |<span data-ttu-id="4275d-235">Date et heure d’expiration du webhook.</span><span class="sxs-lookup"><span data-stu-id="4275d-235">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="4275d-236">Si le webhook n’a pas d’expiration, il peut s’agir de n’importe quelle date future valide.</span><span class="sxs-lookup"><span data-stu-id="4275d-236">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="4275d-237">Voici un exemple de réponse pour une action de correction comportant un seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="4275d-238">Utilisez la méthode Put avec un ID d’action unique pour créer une action corrective pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-238">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="4275d-239">L’exemple suivant crée une correction avec un seuil afin que le runbook démarre quand les résultats de la recherche enregistrée dépassent le seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-239">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="4275d-240">Utilisez la méthode Put avec un ID d’action existant pour modifier une action corrective pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-240">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="4275d-241">Le corps de la demande doit inclure l’ETag de l’action.</span><span class="sxs-lookup"><span data-stu-id="4275d-241">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="4275d-242">Exemple</span><span class="sxs-lookup"><span data-stu-id="4275d-242">Example</span></span>
<span data-ttu-id="4275d-243">Voici un exemple complet pour créer une alerte par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="4275d-243">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="4275d-244">Cet exemple crée une planification avec une action qui contient un seuil et un e-mail.</span><span class="sxs-lookup"><span data-stu-id="4275d-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="4275d-245">Actions de webhook</span><span class="sxs-lookup"><span data-stu-id="4275d-245">Webhook actions</span></span>
<span data-ttu-id="4275d-246">Les actions de webhook démarrent un processus en appelant une URL et, éventuellement, en fournissant une charge utile à envoyer.</span><span class="sxs-lookup"><span data-stu-id="4275d-246">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="4275d-247">Elles sont similaires aux actions correctives, à la différence qu’elles sont destinées à des webhooks qui peuvent appeler des processus autres que des runbooks Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4275d-247">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="4275d-248">En outre, elles permettent de fournir une charge utile à remettre au processus distant.</span><span class="sxs-lookup"><span data-stu-id="4275d-248">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="4275d-249">Les actions de webhook n’ont pas de seuil ; en revanche, elles doivent être ajoutées à une planification qui a une action d’alerte comportant un seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-249">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="4275d-250">Vous pouvez ajouter plusieurs actions webhook, qui sont toutes exécutées si le seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="4275d-250">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="4275d-251">Les propriétés des actions de webhook sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="4275d-251">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="4275d-252">Propriété</span><span class="sxs-lookup"><span data-stu-id="4275d-252">Property</span></span> | <span data-ttu-id="4275d-253">Description</span><span class="sxs-lookup"><span data-stu-id="4275d-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4275d-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="4275d-254">WebhookUri</span></span> |<span data-ttu-id="4275d-255">Objet de l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="4275d-255">The subject of the mail.</span></span> |
| <span data-ttu-id="4275d-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="4275d-256">CustomPayload</span></span> |<span data-ttu-id="4275d-257">Charge utile personnalisée à envoyer au webhook.</span><span class="sxs-lookup"><span data-stu-id="4275d-257">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="4275d-258">Le format dépend de ce que le webhook attend.</span><span class="sxs-lookup"><span data-stu-id="4275d-258">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="4275d-259">Voici un exemple de réponse pour l’action webhook et une action d’alerte associée comportant un seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="4275d-260">Créer ou modifier une action de webhook</span><span class="sxs-lookup"><span data-stu-id="4275d-260">Create or edit a webhook action</span></span>
<span data-ttu-id="4275d-261">Utilisez la méthode Put avec un ID d’action unique pour créer une action webhook pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-261">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="4275d-262">L’exemple suivant crée une action de webhook et une action d’alerte avec un seuil pour que le webhook soit déclenché quand les résultats de la recherche enregistrée dépassent le seuil.</span><span class="sxs-lookup"><span data-stu-id="4275d-262">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="4275d-263">Utilisez la méthode Put avec un ID d’action existant pour modifier une action webhook pour une planification.</span><span class="sxs-lookup"><span data-stu-id="4275d-263">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="4275d-264">Le corps de la demande doit inclure l’ETag de l’action.</span><span class="sxs-lookup"><span data-stu-id="4275d-264">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="4275d-265">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4275d-265">Next steps</span></span>
* <span data-ttu-id="4275d-266">Utilisez l’ [API REST pour effectuer des recherches de journaux](log-analytics-log-search-api.md) dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4275d-266">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

