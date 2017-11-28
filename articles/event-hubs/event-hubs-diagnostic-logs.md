---
title: "les journaux de diagnostic de concentrateurs d’événements aaaAzure | Documents Microsoft"
description: "Découvrez comment tooset des journaux de diagnostic pour les concentrateurs d’événements dans Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="db9c8-103">Journaux de diagnostic d’Event Hubs</span><span class="sxs-lookup"><span data-stu-id="db9c8-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="db9c8-104">Vous pouvez afficher deux types de journaux pour Azure Event Hubs :</span><span class="sxs-lookup"><span data-stu-id="db9c8-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="db9c8-105">**[Journaux d’activité](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="db9c8-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="db9c8-106">Ces journaux comportent des informations sur les opérations effectuées sur un travail.</span><span class="sxs-lookup"><span data-stu-id="db9c8-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="db9c8-107">Hello journaux sont toujours activés.</span><span class="sxs-lookup"><span data-stu-id="db9c8-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="db9c8-108">**[Journaux de diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="db9c8-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="db9c8-109">Vous pouvez configurer les journaux de diagnostic pour obtenir des informations plus détaillées sur tous les événements associés à un travail.</span><span class="sxs-lookup"><span data-stu-id="db9c8-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="db9c8-110">Activités de couverture de journaux de diagnostic de hello création des travaux de hello jusqu'à ce que le travail de hello est supprimé, y compris les mises à jour et les activités qui se produisent pendant l’exécution du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="db9c8-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="db9c8-111">Activer les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="db9c8-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="db9c8-112">Les journaux de diagnostic sont désactivés par défaut.</span><span class="sxs-lookup"><span data-stu-id="db9c8-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="db9c8-113">journaux de diagnostic tooenable :</span><span class="sxs-lookup"><span data-stu-id="db9c8-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="db9c8-114">Bonjour [portail Azure](https://portal.azure.com), sous **analyse + gestion**, cliquez sur **les journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="db9c8-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Panneau navigation toodiagnostic journaux](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="db9c8-116">Cliquez sur ressource hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="db9c8-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="db9c8-117">Cliquez sur **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="db9c8-117">Click **Turn on diagnostics**.</span></span>

    ![Activer les journaux de diagnostic](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="db9c8-119">Pour l’**état**, cliquez sur **ACTIVÉ**.</span><span class="sxs-lookup"><span data-stu-id="db9c8-119">For **Status**, click **On**.</span></span>

    ![Modifier le statut de hello de journaux de diagnostic](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="db9c8-121">Ensemble hello archive cible que vous le souhaitez. par exemple, un compte de stockage, un concentrateur d’événements ou Analytique de journal Azure.</span><span class="sxs-lookup"><span data-stu-id="db9c8-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="db9c8-122">Enregistrer les nouveaux paramètres de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="db9c8-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="db9c8-123">Les nouveaux paramètres prennent effet au bout de 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="db9c8-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="db9c8-124">Après cela, des journaux apparaissent dans la cible d’archivage hello configuré, sur hello **les journaux de diagnostic** panneau.</span><span class="sxs-lookup"><span data-stu-id="db9c8-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="db9c8-125">Pour plus d’informations sur la configuration des diagnostics, consultez hello [vue d’ensemble des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="db9c8-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="db9c8-126">Catégories de journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="db9c8-126">Diagnostic logs categories</span></span>
<span data-ttu-id="db9c8-127">Event Hubs capture les journaux de diagnostic pour deux catégories :</span><span class="sxs-lookup"><span data-stu-id="db9c8-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="db9c8-128">**ArchiveLogs**: journaux liés tooEvent concentrateurs archives, plus précisément, consigne que les erreurs de tooarchive connexes.</span><span class="sxs-lookup"><span data-stu-id="db9c8-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="db9c8-129">**OperationalLogs**: plus d’informations sur ce qui se passe lors des opérations de concentrateurs d’événements, en particulier, hello du type d’opération, y compris la création du concentrateur d’événements, les ressources utilisées et hello l’état de fonctionnement de hello.</span><span class="sxs-lookup"><span data-stu-id="db9c8-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="db9c8-130">Schéma des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="db9c8-130">Diagnostic logs schema</span></span>
<span data-ttu-id="db9c8-131">Tous les journaux sont stockés au format JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="db9c8-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="db9c8-132">Chaque entrée comporte des champs de chaîne qui utilisent le format hello décrit dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="db9c8-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="db9c8-133">Schéma des journaux d’archivage</span><span class="sxs-lookup"><span data-stu-id="db9c8-133">Archive logs schema</span></span>

<span data-ttu-id="db9c8-134">Chaînes JSON de journal archive incluent les éléments répertoriés dans hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="db9c8-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="db9c8-135">Nom</span><span class="sxs-lookup"><span data-stu-id="db9c8-135">Name</span></span> | <span data-ttu-id="db9c8-136">Description</span><span class="sxs-lookup"><span data-stu-id="db9c8-136">Description</span></span>
------- | -------
<span data-ttu-id="db9c8-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="db9c8-137">TaskName</span></span> | <span data-ttu-id="db9c8-138">Description de la tâche hello qui a échoué.</span><span class="sxs-lookup"><span data-stu-id="db9c8-138">Description of hello task that failed.</span></span>
<span data-ttu-id="db9c8-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="db9c8-139">ActivityId</span></span> | <span data-ttu-id="db9c8-140">ID interne, utilisé à des fins de suivi.</span><span class="sxs-lookup"><span data-stu-id="db9c8-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="db9c8-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="db9c8-141">trackingId</span></span> | <span data-ttu-id="db9c8-142">ID interne, utilisé à des fins de suivi.</span><span class="sxs-lookup"><span data-stu-id="db9c8-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="db9c8-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="db9c8-143">resourceId</span></span> | <span data-ttu-id="db9c8-144">ID de ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="db9c8-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="db9c8-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="db9c8-145">eventHub</span></span> | <span data-ttu-id="db9c8-146">Nom complet de l’Event Hub (nom d’espace de noms inclus).</span><span class="sxs-lookup"><span data-stu-id="db9c8-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="db9c8-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="db9c8-147">partitionId</span></span> | <span data-ttu-id="db9c8-148">Partition Event Hub sur laquelle s’effectue l’opération en écriture.</span><span class="sxs-lookup"><span data-stu-id="db9c8-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="db9c8-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="db9c8-149">archiveStep</span></span> | <span data-ttu-id="db9c8-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="db9c8-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="db9c8-151">startTime</span><span class="sxs-lookup"><span data-stu-id="db9c8-151">startTime</span></span> | <span data-ttu-id="db9c8-152">Heure de début de la défaillance.</span><span class="sxs-lookup"><span data-stu-id="db9c8-152">Failure start time.</span></span>
<span data-ttu-id="db9c8-153">failures</span><span class="sxs-lookup"><span data-stu-id="db9c8-153">failures</span></span> | <span data-ttu-id="db9c8-154">Nombre d’occurrences d’une défaillance.</span><span class="sxs-lookup"><span data-stu-id="db9c8-154">Number of times failure occurred.</span></span>
<span data-ttu-id="db9c8-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="db9c8-155">durationInSeconds</span></span> | <span data-ttu-id="db9c8-156">Durée de la défaillance.</span><span class="sxs-lookup"><span data-stu-id="db9c8-156">Duration of failure.</span></span>
<span data-ttu-id="db9c8-157">Message</span><span class="sxs-lookup"><span data-stu-id="db9c8-157">message</span></span> | <span data-ttu-id="db9c8-158">Message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="db9c8-158">Error message.</span></span>
<span data-ttu-id="db9c8-159">category</span><span class="sxs-lookup"><span data-stu-id="db9c8-159">category</span></span> | <span data-ttu-id="db9c8-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="db9c8-160">ArchiveLogs</span></span>

<span data-ttu-id="db9c8-161">Hello de code suivant est un exemple d’un journal d’archive chaîne JSON :</span><span class="sxs-lookup"><span data-stu-id="db9c8-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="db9c8-162">Schéma des journaux des opérations</span><span class="sxs-lookup"><span data-stu-id="db9c8-162">Operational logs schema</span></span>

<span data-ttu-id="db9c8-163">Chaînes JSON de journal des opérations incluent les éléments répertoriés dans hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="db9c8-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="db9c8-164">Nom</span><span class="sxs-lookup"><span data-stu-id="db9c8-164">Name</span></span> | <span data-ttu-id="db9c8-165">Description</span><span class="sxs-lookup"><span data-stu-id="db9c8-165">Description</span></span>
------- | -------
<span data-ttu-id="db9c8-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="db9c8-166">ActivityId</span></span> | <span data-ttu-id="db9c8-167">ID interne utilisé tootrack objectif.</span><span class="sxs-lookup"><span data-stu-id="db9c8-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="db9c8-168">EventName</span><span class="sxs-lookup"><span data-stu-id="db9c8-168">EventName</span></span> | <span data-ttu-id="db9c8-169">Nom d’opération.</span><span class="sxs-lookup"><span data-stu-id="db9c8-169">Operation name.</span></span>  
<span data-ttu-id="db9c8-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="db9c8-170">resourceId</span></span> | <span data-ttu-id="db9c8-171">ID de ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="db9c8-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="db9c8-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="db9c8-172">SubscriptionId</span></span> | <span data-ttu-id="db9c8-173">l'ID d'abonnement.</span><span class="sxs-lookup"><span data-stu-id="db9c8-173">Subscription ID.</span></span>
<span data-ttu-id="db9c8-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="db9c8-174">EventTimeString</span></span> | <span data-ttu-id="db9c8-175">Durée de l’opération.</span><span class="sxs-lookup"><span data-stu-id="db9c8-175">Operation time.</span></span>
<span data-ttu-id="db9c8-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="db9c8-176">EventProperties</span></span> | <span data-ttu-id="db9c8-177">Propriétés de l’opération.</span><span class="sxs-lookup"><span data-stu-id="db9c8-177">Operation properties.</span></span>
<span data-ttu-id="db9c8-178">Statut</span><span class="sxs-lookup"><span data-stu-id="db9c8-178">Status</span></span> | <span data-ttu-id="db9c8-179">État de l’opération.</span><span class="sxs-lookup"><span data-stu-id="db9c8-179">Operation status.</span></span>
<span data-ttu-id="db9c8-180">Appelant</span><span class="sxs-lookup"><span data-stu-id="db9c8-180">Caller</span></span> | <span data-ttu-id="db9c8-181">Appelant de l’opération (portail Azure ou client de gestion).</span><span class="sxs-lookup"><span data-stu-id="db9c8-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="db9c8-182">category</span><span class="sxs-lookup"><span data-stu-id="db9c8-182">category</span></span> | <span data-ttu-id="db9c8-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="db9c8-183">OperationalLogs</span></span>

<span data-ttu-id="db9c8-184">Hello de code suivant est un exemple d’une chaîne JSON de journal des opérations :</span><span class="sxs-lookup"><span data-stu-id="db9c8-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="db9c8-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db9c8-185">Next steps</span></span>
* [<span data-ttu-id="db9c8-186">Introduction tooEvent concentrateurs</span><span class="sxs-lookup"><span data-stu-id="db9c8-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="db9c8-187">Vue d’ensemble de l'API Event Hubs</span><span class="sxs-lookup"><span data-stu-id="db9c8-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="db9c8-188">Prise en main des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="db9c8-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
