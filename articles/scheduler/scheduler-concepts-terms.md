---
title: "aaaScheduler concepts, les termes du contrat et les entités | Documents Microsoft"
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
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="8efc9-104">Concepts, terminologie et hiérarchie d’entités de Scheduler</span><span class="sxs-lookup"><span data-stu-id="8efc9-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="8efc9-105">Hiérarchie d’entités de Scheduler</span><span class="sxs-lookup"><span data-stu-id="8efc9-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="8efc9-106">Hello tableau suivant décrit hello les ressources principales exposées ou utilisées par l’API du Planificateur de hello :</span><span class="sxs-lookup"><span data-stu-id="8efc9-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="8efc9-107">Ressource</span><span class="sxs-lookup"><span data-stu-id="8efc9-107">Resource</span></span> | <span data-ttu-id="8efc9-108">Description</span><span class="sxs-lookup"><span data-stu-id="8efc9-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8efc9-109">**Collection de travaux**</span><span class="sxs-lookup"><span data-stu-id="8efc9-109">**Job collection**</span></span> |<span data-ttu-id="8efc9-110">Une collection de travaux contient un groupe de tâches et conserve les paramètres, les quotas et limitations qui sont partagés par les travaux dans la collection de hello.</span><span class="sxs-lookup"><span data-stu-id="8efc9-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="8efc9-111">Une collection de travaux est créée par le propriétaire d’un abonnement et regroupe des travaux en fonction des limites de l’utilisation ou de l’application.</span><span class="sxs-lookup"><span data-stu-id="8efc9-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="8efc9-112">Il est contraint tooone région.</span><span class="sxs-lookup"><span data-stu-id="8efc9-112">It’s constrained tooone region.</span></span> <span data-ttu-id="8efc9-113">Il permet également application hello de quotas d’utilisation de hello tooconstrain de tous les travaux de la collection.</span><span class="sxs-lookup"><span data-stu-id="8efc9-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="8efc9-114">les quotas Hello incluent MaxJobs et MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="8efc9-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="8efc9-115">**Travail**</span><span class="sxs-lookup"><span data-stu-id="8efc9-115">**Job**</span></span> |<span data-ttu-id="8efc9-116">Un travail définit une seule action récurrente, avec des stratégies d'exécution simples ou complexes.</span><span class="sxs-lookup"><span data-stu-id="8efc9-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="8efc9-117">Les actions peuvent inclure des demandes HTTP, de file d’attente de stockage, de file d’attente Service Bus ou de rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8efc9-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="8efc9-118">**Historique des travaux**</span><span class="sxs-lookup"><span data-stu-id="8efc9-118">**Job history**</span></span> |<span data-ttu-id="8efc9-119">Un historique des travaux représente les détails de l'exécution d'un travail.</span><span class="sxs-lookup"><span data-stu-id="8efc9-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="8efc9-120">Il contient le succès ou l'échec, ainsi que les détails de la réponse.</span><span class="sxs-lookup"><span data-stu-id="8efc9-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="8efc9-121">Gestion des entités de Scheduler</span><span class="sxs-lookup"><span data-stu-id="8efc9-121">Scheduler entity management</span></span>
<span data-ttu-id="8efc9-122">À un niveau élevé, le planificateur hello et API de gestion de service hello exposent hello suivant des opérations sur les ressources de hello :</span><span class="sxs-lookup"><span data-stu-id="8efc9-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="8efc9-123">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="8efc9-123">Capability</span></span> | <span data-ttu-id="8efc9-124">Description et adresse URI</span><span class="sxs-lookup"><span data-stu-id="8efc9-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="8efc9-125">**Gestion de la collection de travaux**</span><span class="sxs-lookup"><span data-stu-id="8efc9-125">**Job collection management**</span></span> |<span data-ttu-id="8efc9-126">GET, PUT et supprimer la prise en charge pour créer et modifier des collections de travaux et des travaux hello qu’elles contiennent.</span><span class="sxs-lookup"><span data-stu-id="8efc9-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="8efc9-127">Une collection de travaux est un conteneur pour les travaux et mappe tooquotas et paramètres partagés.</span><span class="sxs-lookup"><span data-stu-id="8efc9-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="8efc9-128">Les exemples de quotas présentés ultérieurement, sont le nombre maximal de travaux et le plus petit intervalle de périodicité.</span><span class="sxs-lookup"><span data-stu-id="8efc9-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="8efc9-129">PUT et DELETE : `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="8efc9-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="8efc9-130">GET : `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="8efc9-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="8efc9-131">**Gestion des travaux**</span><span class="sxs-lookup"><span data-stu-id="8efc9-131">**Job management**</span></span> |<span data-ttu-id="8efc9-132">Prise en charge de GET, PUT, POST, PATCH et DELETE pour la création et la modification des travaux.</span><span class="sxs-lookup"><span data-stu-id="8efc9-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="8efc9-133">Tous les travaux doivent appartenir collection de tâches tooa qui existe déjà, il n’existe pas de création implicite.</span><span class="sxs-lookup"><span data-stu-id="8efc9-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="8efc9-134">**Gestion de l'historique des travaux**</span><span class="sxs-lookup"><span data-stu-id="8efc9-134">**Job history management**</span></span> |<span data-ttu-id="8efc9-135">Prise en charge de GET pour l'extraction de 60 jours d'historique d'exécution, comme le temps de travail écoulé et les résultats d'exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="8efc9-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="8efc9-136">Ajoute la prise en charge du paramètre de chaîne de requête pour le filtrage basé sur l’état et le statut.</span><span class="sxs-lookup"><span data-stu-id="8efc9-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="8efc9-137">Types de travaux</span><span class="sxs-lookup"><span data-stu-id="8efc9-137">Job types</span></span>
<span data-ttu-id="8efc9-138">Il existe plusieurs types de travaux : les travaux HTTP (notamment les travaux HTTPS prenant en charge SSL), les travaux de file d’attente de stockage et les travaux de file d’attente ou de rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8efc9-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="8efc9-139">Les travaux HTTP sont idéaux si vous disposez d'un point de terminaison d'une charge de travail ou d'un service existant.</span><span class="sxs-lookup"><span data-stu-id="8efc9-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="8efc9-140">Vous pouvez utiliser le stockage travaux toopost messages toostorage d’attente, donc ces travaux sont idéales pour les charges de travail qui utilisent des files d’attente de stockage.</span><span class="sxs-lookup"><span data-stu-id="8efc9-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="8efc9-141">De même, les travaux Service Bus conviennent aux charges de travail utilisant les files d’attente et rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8efc9-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="8efc9-142">entité de « job » Hello en détail</span><span class="sxs-lookup"><span data-stu-id="8efc9-142">hello "job" entity in detail</span></span>
<span data-ttu-id="8efc9-143">À un niveau de base, un travail planifié comporte plusieurs éléments :</span><span class="sxs-lookup"><span data-stu-id="8efc9-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="8efc9-144">Hello action tooperform lors du déclenche du minuteur de travail hello</span><span class="sxs-lookup"><span data-stu-id="8efc9-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="8efc9-145">(Facultatif) hello temps toorun hello tâche</span><span class="sxs-lookup"><span data-stu-id="8efc9-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="8efc9-146">(Facultatif) Fréquence et quand le travail de hello toorepeat</span><span class="sxs-lookup"><span data-stu-id="8efc9-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="8efc9-147">(Facultatif) Un toofire action si l’action principale hello échoue</span><span class="sxs-lookup"><span data-stu-id="8efc9-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="8efc9-148">En interne, un travail planifié contient également des données fournies par le système comme hello prochaine heure d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8efc9-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="8efc9-149">Hello suivant code fournit un exemple complet d’une tâche planifiée.</span><span class="sxs-lookup"><span data-stu-id="8efc9-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="8efc9-150">Les détails sont fournis dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="8efc9-150">Details are provided in subsequent sections.</span></span>

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
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
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

<span data-ttu-id="8efc9-151">Comme indiqué dans hello exemple tâche planifiée ci-dessus, une définition de travail comporte plusieurs éléments :</span><span class="sxs-lookup"><span data-stu-id="8efc9-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="8efc9-152">Heure de début (« startTime »)</span><span class="sxs-lookup"><span data-stu-id="8efc9-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="8efc9-153">Action (« action »), qui inclut l'action d'erreur (« errorAction »)</span><span class="sxs-lookup"><span data-stu-id="8efc9-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="8efc9-154">Récurrence (« recurrence »)</span><span class="sxs-lookup"><span data-stu-id="8efc9-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="8efc9-155">État (« state »)</span><span class="sxs-lookup"><span data-stu-id="8efc9-155">State (“state”)</span></span>  
* <span data-ttu-id="8efc9-156">Statut (« status »)</span><span class="sxs-lookup"><span data-stu-id="8efc9-156">Status (“status”)</span></span>  
* <span data-ttu-id="8efc9-157">Stratégie de nouvelle tentative (« retryPolicy »)</span><span class="sxs-lookup"><span data-stu-id="8efc9-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="8efc9-158">Examinons chacun en détail :</span><span class="sxs-lookup"><span data-stu-id="8efc9-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="8efc9-159">startTime</span><span class="sxs-lookup"><span data-stu-id="8efc9-159">startTime</span></span>
<span data-ttu-id="8efc9-160">Hello « startTime » est l’heure de début hello et permet à un fuseau horaire d’une compensation sur le câble hello dans hello appelant toospecify [format ISO-8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="8efc9-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="8efc9-161">action et errorAction</span><span class="sxs-lookup"><span data-stu-id="8efc9-161">action and errorAction</span></span>
<span data-ttu-id="8efc9-162">Hello « action » est l’action hello appelée sur chaque occurrence et décrit un type d’appel de service.</span><span class="sxs-lookup"><span data-stu-id="8efc9-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="8efc9-163">action de Hello est qui sera exécutée sur hello fourni la planification.</span><span class="sxs-lookup"><span data-stu-id="8efc9-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="8efc9-164">Scheduler prend en charge des actions HTTP, de file d’attente de stockage, de rubrique Service Bus ou de file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8efc9-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="8efc9-165">Hello dans l’exemple hello ci-dessus est une action HTTP.</span><span class="sxs-lookup"><span data-stu-id="8efc9-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="8efc9-166">Voici un exemple d'action de file d'attente de stockage :</span><span class="sxs-lookup"><span data-stu-id="8efc9-166">Below is an example of a storage queue action:</span></span>

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

<span data-ttu-id="8efc9-167">Voici un exemple d’action de rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8efc9-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="8efc9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="8efc9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="8efc9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="8efc9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="8efc9-170">Voici un exemple d’action de file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8efc9-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="8efc9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="8efc9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="8efc9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="8efc9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="8efc9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="8efc9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="8efc9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="8efc9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="8efc9-175">Hello « errorAction » est un gestionnaire d’erreurs hello, action hello appelée en cas d’échec de l’action principale de hello.</span><span class="sxs-lookup"><span data-stu-id="8efc9-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="8efc9-176">Vous pouvez utiliser cette variable toocall un point de terminaison de gestion des erreurs ou envoyer une notification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8efc9-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="8efc9-177">Cela peut être utilisé pour atteindre un point de terminaison secondaire en cas de hello que hello principal n’est pas disponible (par exemple, en cas de hello d’un incident site du point de terminaison hello) ou peut être utilisé pour notifier une erreur de traitement du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8efc9-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="8efc9-178">Comme action principale de hello, action d’erreur hello peut être simple ou composite logique basée sur les autres actions.</span><span class="sxs-lookup"><span data-stu-id="8efc9-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="8efc9-179">toolearn comment toocreate un jeton SAS, consultez trop[créer et utiliser une Signature d’accès partagé](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="8efc9-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="8efc9-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="8efc9-180">recurrence</span></span>
<span data-ttu-id="8efc9-181">La récurrence comporte plusieurs parties :</span><span class="sxs-lookup"><span data-stu-id="8efc9-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="8efc9-182">La fréquence (frequency) : minute, heure, jour, semaine, mois, année</span><span class="sxs-lookup"><span data-stu-id="8efc9-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="8efc9-183">Interval : Intervalle à hello attribué à la fréquence de récurrence de hello</span><span class="sxs-lookup"><span data-stu-id="8efc9-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="8efc9-184">Planification prescrite : spécifiez les minutes, heures, jours de la semaine, mois et jour du mois de périodicité de hello</span><span class="sxs-lookup"><span data-stu-id="8efc9-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="8efc9-185">Le nombre (count) : nombre d'occurrences</span><span class="sxs-lookup"><span data-stu-id="8efc9-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="8efc9-186">Heure de fin : aucun travail ne s’exécutera après hello spécifié l’heure de fin</span><span class="sxs-lookup"><span data-stu-id="8efc9-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="8efc9-187">Un travail est récurrent s'il comporte un objet récurrent spécifié dans sa définition JSON.</span><span class="sxs-lookup"><span data-stu-id="8efc9-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="8efc9-188">Si count et endTime sont spécifiés, la règle d’achèvement hello qui apparaît en premier est honorée.</span><span class="sxs-lookup"><span data-stu-id="8efc9-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="8efc9-189">state</span><span class="sxs-lookup"><span data-stu-id="8efc9-189">state</span></span>
<span data-ttu-id="8efc9-190">état Hello du travail de hello est un des quatre valeurs : activé, désactivé, terminé ou a généré une erreur.</span><span class="sxs-lookup"><span data-stu-id="8efc9-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="8efc9-191">Vous pouvez placer ou le correctif logiciel des travaux, en tant que tooupdate les toohello activé ou l’état désactivé.</span><span class="sxs-lookup"><span data-stu-id="8efc9-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="8efc9-192">Si une tâche a été terminée ou a généré une erreur, qui est un état final ne peut pas être mis à jour (même si le travail de hello peut encore être supprimé).</span><span class="sxs-lookup"><span data-stu-id="8efc9-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="8efc9-193">Un exemple de propriété d’état hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="8efc9-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="8efc9-194">Les travaux terminés et ayant généré une erreur sont supprimés après 60 jours.</span><span class="sxs-lookup"><span data-stu-id="8efc9-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="8efc9-195">status</span><span class="sxs-lookup"><span data-stu-id="8efc9-195">status</span></span>
<span data-ttu-id="8efc9-196">Lorsqu’une tâche du planificateur a démarré, informations sur l’état actuel de hello du travail de hello être renvoyées.</span><span class="sxs-lookup"><span data-stu-id="8efc9-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="8efc9-197">Cet objet n’est pas définissable par l’utilisateur de hello, elle est définie par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="8efc9-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="8efc9-198">Toutefois, il est inclus dans les hello objet travail (plutôt qu’une ressource liée distincte) afin qu’il puisse obtenir facilement état hello d’un travail.</span><span class="sxs-lookup"><span data-stu-id="8efc9-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="8efc9-199">État de la tâche comprend le temps de hello de hello l’exécution précédente (le cas échéant), hello heure de la prochaine exécution planifiée hello (pour les travaux en cours) et le nombre d’exécutions du travail de hello hello.</span><span class="sxs-lookup"><span data-stu-id="8efc9-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="8efc9-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="8efc9-200">retryPolicy</span></span>
<span data-ttu-id="8efc9-201">Si une tâche du planificateur échoue, il est possible de toospecify un toodetermine de stratégie de nouvelle tentative si et comment l’action de hello est retentée.</span><span class="sxs-lookup"><span data-stu-id="8efc9-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="8efc9-202">Cela est déterminé par hello **retryType** objet, il est défini trop**aucun** s’il n’existe aucune stratégie de nouvelle tentative, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8efc9-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="8efc9-203">Définissez-le trop**fixe** s’il existe une stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="8efc9-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="8efc9-204">tooset une stratégie de nouvelle tentative, vous peuvent spécifier deux paramètres supplémentaires : un intervalle avant nouvelle tentative (**retryInterval**) et nombre hello de nouvelles tentatives (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="8efc9-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="8efc9-205">intervalle avant nouvelle tentative de Hello, spécifié par hello **retryInterval** d’objet, est l’intervalle de salutation entre les nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="8efc9-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="8efc9-206">Sa valeur par défaut est de 30 secondes. Elle peut varier de 15 secondes à 18 mois.</span><span class="sxs-lookup"><span data-stu-id="8efc9-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="8efc9-207">Les travaux des collections de tâches gratuites ont une valeur minimale configurable de 1 heure.</span><span class="sxs-lookup"><span data-stu-id="8efc9-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="8efc9-208">Il est défini dans le format de hello ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="8efc9-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="8efc9-209">De même, la valeur hello nombre hello de nouvelles tentatives est affectée par hello **retryCount** de l’objet ; il s’agit hello les nombre de fois où une nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="8efc9-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="8efc9-210">Sa valeur par défaut est 4, et sa valeur maximale est 20\.</span><span class="sxs-lookup"><span data-stu-id="8efc9-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="8efc9-211">Les deux **retryInterval** et **retryCount** sont facultatifs.</span><span class="sxs-lookup"><span data-stu-id="8efc9-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="8efc9-212">Ils reçoivent leurs valeurs par défaut si **retryType** est défini trop**fixe** et aucune est spécifiée explicitement.</span><span class="sxs-lookup"><span data-stu-id="8efc9-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="8efc9-213">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8efc9-213">See also</span></span>
 [<span data-ttu-id="8efc9-214">Présentation d'Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="8efc9-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="8efc9-215">Prise en main du planificateur Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="8efc9-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="8efc9-216">Plans et facturation dans Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="8efc9-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="8efc9-217">Comment toobuild complexe planifie et périodicité avancée avec Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="8efc9-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="8efc9-218">Informations de référence sur l’API REST d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="8efc9-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="8efc9-219">Informations de référence sur les applets de commande PowerShell d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="8efc9-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="8efc9-220">Haute disponibilité et fiabilité d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="8efc9-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="8efc9-221">Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="8efc9-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="8efc9-222">Authentification sortante d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="8efc9-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

