---
title: "Concepts, termes et entités Scheduler | Microsoft Docs"
description: "Concepts, terminologie et hiérarchie des entités d’Azure Scheduler, notamment les travaux et les collections de travaux.  Fournit un exemple complet d’un exemple de tâche planifiée."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="cc13b-104">Concepts, terminologie et hiérarchie d’entités de Scheduler</span><span class="sxs-lookup"><span data-stu-id="cc13b-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="cc13b-105">Hiérarchie d’entités de Scheduler</span><span class="sxs-lookup"><span data-stu-id="cc13b-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="cc13b-106">Le tableau suivant décrit les ressources principales exposées ou utilisées par l'API de Scheduler :</span><span class="sxs-lookup"><span data-stu-id="cc13b-106">The following table describes the main resources exposed or used by the Scheduler API:</span></span>

| <span data-ttu-id="cc13b-107">Ressource</span><span class="sxs-lookup"><span data-stu-id="cc13b-107">Resource</span></span> | <span data-ttu-id="cc13b-108">Description</span><span class="sxs-lookup"><span data-stu-id="cc13b-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc13b-109">**Collection de travaux**</span><span class="sxs-lookup"><span data-stu-id="cc13b-109">**Job collection**</span></span> |<span data-ttu-id="cc13b-110">Une collection de travaux contient un groupe de travaux et conserve les paramètres, les quotas et les limitations qui sont partagés par les travaux au sein de la collection.</span><span class="sxs-lookup"><span data-stu-id="cc13b-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span></span> <span data-ttu-id="cc13b-111">Une collection de travaux est créée par le propriétaire d’un abonnement et regroupe des travaux en fonction des limites de l’utilisation ou de l’application.</span><span class="sxs-lookup"><span data-stu-id="cc13b-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="cc13b-112">Une collection est limitée à une région.</span><span class="sxs-lookup"><span data-stu-id="cc13b-112">It’s constrained to one region.</span></span> <span data-ttu-id="cc13b-113">Elle permet également la mise en œuvre de quotas pour limiter l’utilisation de tous les travaux de la collection.</span><span class="sxs-lookup"><span data-stu-id="cc13b-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span></span> <span data-ttu-id="cc13b-114">Les quotas incluent MaxJobs et MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="cc13b-114">The quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="cc13b-115">**Travail**</span><span class="sxs-lookup"><span data-stu-id="cc13b-115">**Job**</span></span> |<span data-ttu-id="cc13b-116">Un travail définit une seule action récurrente, avec des stratégies d'exécution simples ou complexes.</span><span class="sxs-lookup"><span data-stu-id="cc13b-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="cc13b-117">Les actions peuvent inclure des demandes HTTP, de file d’attente de stockage, de file d’attente Service Bus ou de rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cc13b-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="cc13b-118">**Historique des travaux**</span><span class="sxs-lookup"><span data-stu-id="cc13b-118">**Job history**</span></span> |<span data-ttu-id="cc13b-119">Un historique des travaux représente les détails de l'exécution d'un travail.</span><span class="sxs-lookup"><span data-stu-id="cc13b-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="cc13b-120">Il contient le succès ou l'échec, ainsi que les détails de la réponse.</span><span class="sxs-lookup"><span data-stu-id="cc13b-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="cc13b-121">Gestion des entités de Scheduler</span><span class="sxs-lookup"><span data-stu-id="cc13b-121">Scheduler entity management</span></span>
<span data-ttu-id="cc13b-122">Globalement, le planificateur et l'API de gestion de service exposent les opérations suivantes sur les ressources :</span><span class="sxs-lookup"><span data-stu-id="cc13b-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span></span>

| <span data-ttu-id="cc13b-123">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="cc13b-123">Capability</span></span> | <span data-ttu-id="cc13b-124">Description et adresse URI</span><span class="sxs-lookup"><span data-stu-id="cc13b-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="cc13b-125">**Gestion de la collection de travaux**</span><span class="sxs-lookup"><span data-stu-id="cc13b-125">**Job collection management**</span></span> |<span data-ttu-id="cc13b-126">Prise en charge de GET, PUT et DELETE pour la création et la modification des collections de travaux et des travaux qu'elles contiennent.</span><span class="sxs-lookup"><span data-stu-id="cc13b-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span></span> <span data-ttu-id="cc13b-127">Une collection de travaux sert de conteneur pour les travaux et mappe ceux-ci aux quotas et paramètres partagés.</span><span class="sxs-lookup"><span data-stu-id="cc13b-127">A job collection is a container for jobs and maps to quotas and shared settings.</span></span> <span data-ttu-id="cc13b-128">Les exemples de quotas présentés ultérieurement, sont le nombre maximal de travaux et le plus petit intervalle de périodicité.</span><span class="sxs-lookup"><span data-stu-id="cc13b-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="cc13b-129">PUT et DELETE : `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="cc13b-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="cc13b-130">GET : `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="cc13b-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="cc13b-131">**Gestion des travaux**</span><span class="sxs-lookup"><span data-stu-id="cc13b-131">**Job management**</span></span> |<span data-ttu-id="cc13b-132">Prise en charge de GET, PUT, POST, PATCH et DELETE pour la création et la modification des travaux.</span><span class="sxs-lookup"><span data-stu-id="cc13b-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="cc13b-133">Tous les travaux doivent appartenir à une collection de travaux qui existe déjà, afin qu’il n’y ait pas de création implicite.</span><span class="sxs-lookup"><span data-stu-id="cc13b-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="cc13b-134">**Gestion de l'historique des travaux**</span><span class="sxs-lookup"><span data-stu-id="cc13b-134">**Job history management**</span></span> |<span data-ttu-id="cc13b-135">Prise en charge de GET pour l'extraction de 60 jours d'historique d'exécution, comme le temps de travail écoulé et les résultats d'exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="cc13b-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="cc13b-136">Ajoute la prise en charge du paramètre de chaîne de requête pour le filtrage basé sur l’état et le statut.</span><span class="sxs-lookup"><span data-stu-id="cc13b-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="cc13b-137">Types de travaux</span><span class="sxs-lookup"><span data-stu-id="cc13b-137">Job types</span></span>
<span data-ttu-id="cc13b-138">Il existe plusieurs types de travaux : les travaux HTTP (notamment les travaux HTTPS prenant en charge SSL), les travaux de file d’attente de stockage et les travaux de file d’attente ou de rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cc13b-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="cc13b-139">Les travaux HTTP sont idéaux si vous disposez d'un point de terminaison d'une charge de travail ou d'un service existant.</span><span class="sxs-lookup"><span data-stu-id="cc13b-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="cc13b-140">Vous pouvez utiliser les travaux de file d’attente de stockage pour publier des messages aux files d’attente de stockage et donc, ces travaux sont idéaux pour les charges de travail qui utilisent des files d’attente de stockage.</span><span class="sxs-lookup"><span data-stu-id="cc13b-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="cc13b-141">De même, les travaux Service Bus conviennent aux charges de travail utilisant les files d’attente et rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cc13b-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="the-job-entity-in-detail"></a><span data-ttu-id="cc13b-142">L’entité « travail » en détail</span><span class="sxs-lookup"><span data-stu-id="cc13b-142">The "job" entity in detail</span></span>
<span data-ttu-id="cc13b-143">À un niveau de base, un travail planifié comporte plusieurs éléments :</span><span class="sxs-lookup"><span data-stu-id="cc13b-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="cc13b-144">L'action à effectuer lorsque le travail se déclenche</span><span class="sxs-lookup"><span data-stu-id="cc13b-144">The action to perform when the job timer fires</span></span>  
* <span data-ttu-id="cc13b-145">(Facultatif) L'heure d'exécution du travail</span><span class="sxs-lookup"><span data-stu-id="cc13b-145">(Optional) The time to run the job</span></span>  
* <span data-ttu-id="cc13b-146">(Facultatif) Quand et à quelle fréquence répéter le travail</span><span class="sxs-lookup"><span data-stu-id="cc13b-146">(Optional) When and how often to repeat the job</span></span>  
* <span data-ttu-id="cc13b-147">(Facultatif) Une action à déclencher en cas d'échec de l'action principale</span><span class="sxs-lookup"><span data-stu-id="cc13b-147">(Optional) An action to fire if the primary action fails</span></span>  

<span data-ttu-id="cc13b-148">En interne, un travail planifié contient également des données fournies par le système, comme l'heure d'exécution planifiée suivante.</span><span class="sxs-lookup"><span data-stu-id="cc13b-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span></span>

<span data-ttu-id="cc13b-149">Le code suivant fournit un exemple complet d’un exemple de tâche planifiée.</span><span class="sxs-lookup"><span data-stu-id="cc13b-149">The following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="cc13b-150">Les détails sont fournis dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="cc13b-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="cc13b-151">Comme indiqué dans l’exemple de travail de Scheduler ci-dessus, une définition de travail comporte plusieurs éléments :</span><span class="sxs-lookup"><span data-stu-id="cc13b-151">As seen in the sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="cc13b-152">Heure de début (« startTime »)</span><span class="sxs-lookup"><span data-stu-id="cc13b-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="cc13b-153">Action (« action »), qui inclut l'action d'erreur (« errorAction »)</span><span class="sxs-lookup"><span data-stu-id="cc13b-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="cc13b-154">Récurrence (« recurrence »)</span><span class="sxs-lookup"><span data-stu-id="cc13b-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="cc13b-155">État (« state »)</span><span class="sxs-lookup"><span data-stu-id="cc13b-155">State (“state”)</span></span>  
* <span data-ttu-id="cc13b-156">Statut (« status »)</span><span class="sxs-lookup"><span data-stu-id="cc13b-156">Status (“status”)</span></span>  
* <span data-ttu-id="cc13b-157">Stratégie de nouvelle tentative (« retryPolicy »)</span><span class="sxs-lookup"><span data-stu-id="cc13b-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="cc13b-158">Examinons chacun en détail :</span><span class="sxs-lookup"><span data-stu-id="cc13b-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="cc13b-159">startTime</span><span class="sxs-lookup"><span data-stu-id="cc13b-159">startTime</span></span>
<span data-ttu-id="cc13b-160">« startTime » correspond à l’heure de début et permet à l’appelant de spécifier un décalage de fuseau horaire sur le câble au [format ISO-8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="cc13b-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="cc13b-161">action et errorAction</span><span class="sxs-lookup"><span data-stu-id="cc13b-161">action and errorAction</span></span>
<span data-ttu-id="cc13b-162">« action » est l’action appelée sur chaque occurrence et décrit un type d’appel de service.</span><span class="sxs-lookup"><span data-stu-id="cc13b-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="cc13b-163">L’action correspond à l’opération qui sera exécutée, en fonction de la planification spécifiée.</span><span class="sxs-lookup"><span data-stu-id="cc13b-163">The action is what will be executed on the provided schedule.</span></span> <span data-ttu-id="cc13b-164">Scheduler prend en charge des actions HTTP, de file d’attente de stockage, de rubrique Service Bus ou de file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cc13b-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="cc13b-165">L’action dans l’exemple ci-dessus est une action http.</span><span class="sxs-lookup"><span data-stu-id="cc13b-165">The action in the example above is an HTTP action.</span></span> <span data-ttu-id="cc13b-166">Voici un exemple d'action de file d'attente de stockage :</span><span class="sxs-lookup"><span data-stu-id="cc13b-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="cc13b-167">Voici un exemple d’action de rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cc13b-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="cc13b-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="cc13b-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="cc13b-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="cc13b-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="cc13b-170">Voici un exemple d’action de file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="cc13b-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="cc13b-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="cc13b-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="cc13b-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="cc13b-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="cc13b-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="cc13b-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="cc13b-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="cc13b-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="cc13b-175">« errorAction » est le gestionnaire d'erreurs, l'action appelée lorsque l'action principale échoue.</span><span class="sxs-lookup"><span data-stu-id="cc13b-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span></span> <span data-ttu-id="cc13b-176">Vous pouvez utiliser cette variable pour appeler un point de terminaison de gestion d’erreur ou envoyer une notification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc13b-176">You can use this variable to call an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="cc13b-177">L’opération peut servir à atteindre un point de terminaison secondaire au cas où le premier ne serait pas disponible (par exemple, en cas de sinistre sur le site du point de terminaison) ou pour notifier un point de terminaison de traitement d’erreur.</span><span class="sxs-lookup"><span data-stu-id="cc13b-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="cc13b-178">Comme l'action principale, l'action d'erreur peut être une logique simple ou composite basée sur d'autres actions.</span><span class="sxs-lookup"><span data-stu-id="cc13b-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="cc13b-179">Pour savoir comment créer un jeton SAS, consultez [Créer et utiliser une signature d'accès partagé](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc13b-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="cc13b-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="cc13b-180">recurrence</span></span>
<span data-ttu-id="cc13b-181">La récurrence comporte plusieurs parties :</span><span class="sxs-lookup"><span data-stu-id="cc13b-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="cc13b-182">La fréquence (frequency) : minute, heure, jour, semaine, mois, année</span><span class="sxs-lookup"><span data-stu-id="cc13b-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="cc13b-183">L'intervalle (interval) : intervalle à la fréquence donnée pour la récurrence</span><span class="sxs-lookup"><span data-stu-id="cc13b-183">Interval: Interval at the given frequency for the recurrence</span></span>  
* <span data-ttu-id="cc13b-184">La planification prescrite (prescribed schedule) : spécifiez les minutes, heures, jours de la semaine, mois et jours du mois de la récurrence</span><span class="sxs-lookup"><span data-stu-id="cc13b-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span></span>  
* <span data-ttu-id="cc13b-185">Le nombre (count) : nombre d'occurrences</span><span class="sxs-lookup"><span data-stu-id="cc13b-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="cc13b-186">L'heure de fin (end time) : aucun travail ne s'exécutera après l'heure de fin spécifiée</span><span class="sxs-lookup"><span data-stu-id="cc13b-186">End time: No jobs will execute after the specified end time</span></span>  

<span data-ttu-id="cc13b-187">Un travail est récurrent s'il comporte un objet récurrent spécifié dans sa définition JSON.</span><span class="sxs-lookup"><span data-stu-id="cc13b-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="cc13b-188">Si les valeurs count et endTime sont toutes deux spécifiées, la règle d'achèvement qui se produit en premier est honorée.</span><span class="sxs-lookup"><span data-stu-id="cc13b-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="cc13b-189">state</span><span class="sxs-lookup"><span data-stu-id="cc13b-189">state</span></span>
<span data-ttu-id="cc13b-190">L'état du travail a l'une de quatre valeurs : activé, désactivé, terminé ou a généré une erreur.</span><span class="sxs-lookup"><span data-stu-id="cc13b-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="cc13b-191">Vous pouvez exécuter PUT ou PATCH sur les travaux afin de les mettre à jour sur l'état activé ou désactivé.</span><span class="sxs-lookup"><span data-stu-id="cc13b-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span></span> <span data-ttu-id="cc13b-192">Si un travail a été terminé ou a généré une erreur, cet état final ne peut pas être mis à jour (bien que le travail puisse encore être supprimé).</span><span class="sxs-lookup"><span data-stu-id="cc13b-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span></span> <span data-ttu-id="cc13b-193">Vous trouverez ci-dessous un exemple de la propriété state :</span><span class="sxs-lookup"><span data-stu-id="cc13b-193">An example of the state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="cc13b-194">Les travaux terminés et ayant généré une erreur sont supprimés après 60 jours.</span><span class="sxs-lookup"><span data-stu-id="cc13b-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="cc13b-195">status</span><span class="sxs-lookup"><span data-stu-id="cc13b-195">status</span></span>
<span data-ttu-id="cc13b-196">Lorsqu'un travail de Scheduler a démarré, des informations sur l'état actuel du travail sont renvoyées.</span><span class="sxs-lookup"><span data-stu-id="cc13b-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span></span> <span data-ttu-id="cc13b-197">Cet objet n’est pas définissable par l’utilisateur ; il est défini par le système.</span><span class="sxs-lookup"><span data-stu-id="cc13b-197">This object is not settable by the user—it’s set by the system.</span></span> <span data-ttu-id="cc13b-198">Toutefois, il est inclus dans l'objet du travail (plutôt qu'en tant que ressource liée distincte) afin que l'utilisateur puisse obtenir l'état d'un travail facilement.</span><span class="sxs-lookup"><span data-stu-id="cc13b-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span></span>

<span data-ttu-id="cc13b-199">L'état du travail inclut l'heure de l'exécution précédente (le cas échéant), l'heure de la prochaine exécution planifiée (pour les travaux en cours) et le nombre d'exécutions du travail.</span><span class="sxs-lookup"><span data-stu-id="cc13b-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="cc13b-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="cc13b-200">retryPolicy</span></span>
<span data-ttu-id="cc13b-201">En cas d'échec d'un travail de Scheduler, il est possible de spécifier une stratégie de nouvelle tentative pour déterminer si et comment l'action est retentée.</span><span class="sxs-lookup"><span data-stu-id="cc13b-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span></span> <span data-ttu-id="cc13b-202">Ceci est déterminé par l’objet **retryType**. Il est défini sur **none** s’il n’existe aucune stratégie de nouvelle tentative, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="cc13b-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="cc13b-203">Définissez-le sur **fixed** s’il existe une stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="cc13b-203">Set it to **fixed** if there is a retry policy.</span></span>

<span data-ttu-id="cc13b-204">Pour définir une stratégie de nouvelle tentative, deux paramètres supplémentaires peuvent être spécifiés : un intervalle de nouvelle tentative (**retryInterval**) et le nombre de nouvelles tentatives (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="cc13b-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span></span>

<span data-ttu-id="cc13b-205">L’intervalle de nouvelle tentative, spécifié avec l’objet **retryInterval**, est l’intervalle entre les nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="cc13b-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span></span> <span data-ttu-id="cc13b-206">Sa valeur par défaut est de 30 secondes. Elle peut varier de 15 secondes à 18 mois.</span><span class="sxs-lookup"><span data-stu-id="cc13b-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="cc13b-207">Les travaux des collections de tâches gratuites ont une valeur minimale configurable de 1 heure.</span><span class="sxs-lookup"><span data-stu-id="cc13b-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="cc13b-208">Il est défini dans le format ISO-8601.</span><span class="sxs-lookup"><span data-stu-id="cc13b-208">It is defined in the ISO 8601 format.</span></span> <span data-ttu-id="cc13b-209">De même, la valeur du nombre de nouvelles tentatives est spécifiée avec l’objet **retryCount**. Il s’agit du nombre de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="cc13b-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span></span> <span data-ttu-id="cc13b-210">Sa valeur par défaut est 4, et sa valeur maximale est 20\.</span><span class="sxs-lookup"><span data-stu-id="cc13b-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="cc13b-211">Les deux **retryInterval** et **retryCount** sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="cc13b-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="cc13b-212">Ils reçoivent leur valeur par défaut si **retryType** est défini sur **fixed** et si aucune valeur n’est spécifiée explicitement.</span><span class="sxs-lookup"><span data-stu-id="cc13b-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="cc13b-213">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cc13b-213">See also</span></span>
 [<span data-ttu-id="cc13b-214">Présentation d'Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="cc13b-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="cc13b-215">Prise en main de Scheduler dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="cc13b-215">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="cc13b-216">Plans et facturation dans Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="cc13b-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="cc13b-217">Comment créer des planifications complexes et une périodicité avancée avec Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="cc13b-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="cc13b-218">Informations de référence sur l’API REST d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="cc13b-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="cc13b-219">Informations de référence sur les applets de commande PowerShell d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="cc13b-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="cc13b-220">Haute disponibilité et fiabilité d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="cc13b-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="cc13b-221">Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="cc13b-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="cc13b-222">Authentification sortante d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="cc13b-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

