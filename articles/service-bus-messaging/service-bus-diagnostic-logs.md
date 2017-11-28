---
title: "Journaux de diagnostic Azure Service Bus | Microsoft Docs"
description: "Découvrez comment configurer les journaux de diagnostic pour Service Bus dans Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: 72e18444c83b84c5191a0aab3dc6983517167dd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="a9693-103">Journaux de diagnostic Service Bus</span><span class="sxs-lookup"><span data-stu-id="a9693-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="a9693-104">Vous pouvez afficher deux types de journaux pour Azure Service Bus :</span><span class="sxs-lookup"><span data-stu-id="a9693-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="a9693-105">**[Journaux d’activité](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="a9693-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="a9693-106">Ces journaux contiennent des informations sur les opérations effectuées sur un travail.</span><span class="sxs-lookup"><span data-stu-id="a9693-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="a9693-107">Les journaux sont toujours activés.</span><span class="sxs-lookup"><span data-stu-id="a9693-107">The logs are always enabled.</span></span>
* <span data-ttu-id="a9693-108">**[Journaux de diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="a9693-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="a9693-109">Vous pouvez configurer les journaux de diagnostic pour obtenir des informations plus détaillés sur tous les événements associés à un travail.</span><span class="sxs-lookup"><span data-stu-id="a9693-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="a9693-110">Les journaux de diagnostic couvrent les activités qui se déroulent entre la création du travail et sa suppression, notamment les mises à jour et les activités durant l’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="a9693-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="a9693-111">Activer les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="a9693-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="a9693-112">Les journaux de diagnostic sont désactivés par défaut.</span><span class="sxs-lookup"><span data-stu-id="a9693-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="a9693-113">Pour activer les journaux de diagnostic, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a9693-113">To enable diagnostic logs, perform the following steps:</span></span>

1.  <span data-ttu-id="a9693-114">Dans le [portail Azure](https://portal.azure.com), sous **Surveillance + gestion**, cliquez sur **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="a9693-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![navigation dans le panneau jusqu’aux journaux de diagnostic](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="a9693-116">Cliquez sur la ressource que vous souhaitez surveiller.</span><span class="sxs-lookup"><span data-stu-id="a9693-116">Click the resource you want to monitor.</span></span>  

3.  <span data-ttu-id="a9693-117">Cliquez sur **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="a9693-117">Click **Turn on diagnostics**.</span></span>

    ![activer les journaux de diagnostic](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="a9693-119">Pour l’**état**, cliquez sur **ACTIVÉ**.</span><span class="sxs-lookup"><span data-stu-id="a9693-119">For **Status**, click **On**.</span></span>

    ![modifier l’état des journaux de diagnostic](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="a9693-121">Définissez la cible d’archivage de votre choix, par exemple un compte de stockage, un Event Hub ou Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a9693-121">Set the archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="a9693-122">Enregistrez les nouveaux paramètres de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="a9693-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="a9693-123">Les nouveaux paramètres prennent effet au bout de 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="a9693-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="a9693-124">Après cela, les journaux apparaissent dans la cible d’archivage configurée, dans le panneau **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="a9693-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="a9693-125">Pour plus d’informations sur la configuration des diagnostics, consultez la [vue d’ensemble des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a9693-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="a9693-126">Schéma des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="a9693-126">Diagnostic logs schema</span></span>

<span data-ttu-id="a9693-127">Tous les journaux sont stockés au format JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="a9693-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="a9693-128">Chaque entrée comporte des champs de type chaîne au format décrit dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="a9693-128">Each entry has string fields that use the format described in the following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="a9693-129">Schéma des journaux des opérations</span><span class="sxs-lookup"><span data-stu-id="a9693-129">Operational logs schema</span></span>

<span data-ttu-id="a9693-130">Les journaux de la catégorie **OperationalLogs** capturent ce qui se passe durant l’opération Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a9693-130">Logs in the **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="a9693-131">Plus précisément, ces journaux capturent le type d’opération, notamment la création de la file d’attente, les ressources utilisées et l’état de l’opération.</span><span class="sxs-lookup"><span data-stu-id="a9693-131">Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.</span></span>

<span data-ttu-id="a9693-132">Les chaînes JSON du journal des opérations incluent les éléments répertoriés dans le tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="a9693-132">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="a9693-133">Nom</span><span class="sxs-lookup"><span data-stu-id="a9693-133">Name</span></span> | <span data-ttu-id="a9693-134">Description</span><span class="sxs-lookup"><span data-stu-id="a9693-134">Description</span></span>
------- | -------
<span data-ttu-id="a9693-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="a9693-135">ActivityId</span></span> | <span data-ttu-id="a9693-136">ID interne, utilisé à des fins de suivi</span><span class="sxs-lookup"><span data-stu-id="a9693-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="a9693-137">EventName</span><span class="sxs-lookup"><span data-stu-id="a9693-137">EventName</span></span> | <span data-ttu-id="a9693-138">Nom d’opération</span><span class="sxs-lookup"><span data-stu-id="a9693-138">Operation name</span></span>           
<span data-ttu-id="a9693-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="a9693-139">resourceId</span></span> | <span data-ttu-id="a9693-140">ID de ressource Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a9693-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="a9693-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="a9693-141">SubscriptionId</span></span> | <span data-ttu-id="a9693-142">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="a9693-142">Subscription ID</span></span>
<span data-ttu-id="a9693-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="a9693-143">EventTimeString</span></span> | <span data-ttu-id="a9693-144">Durée de l’opération</span><span class="sxs-lookup"><span data-stu-id="a9693-144">Operation time</span></span>
<span data-ttu-id="a9693-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="a9693-145">EventProperties</span></span> | <span data-ttu-id="a9693-146">Propriétés de l’opération</span><span class="sxs-lookup"><span data-stu-id="a9693-146">Operation properties</span></span>
<span data-ttu-id="a9693-147">État</span><span class="sxs-lookup"><span data-stu-id="a9693-147">Status</span></span> | <span data-ttu-id="a9693-148">État de l’opération</span><span class="sxs-lookup"><span data-stu-id="a9693-148">Operation status</span></span>
<span data-ttu-id="a9693-149">Appelant</span><span class="sxs-lookup"><span data-stu-id="a9693-149">Caller</span></span> | <span data-ttu-id="a9693-150">Appelant de l’opération (portail Azure ou client de gestion)</span><span class="sxs-lookup"><span data-stu-id="a9693-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="a9693-151">category</span><span class="sxs-lookup"><span data-stu-id="a9693-151">category</span></span> | <span data-ttu-id="a9693-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="a9693-152">OperationalLogs</span></span>

<span data-ttu-id="a9693-153">Voici un exemple de chaîne JSON du journal des opérations :</span><span class="sxs-lookup"><span data-stu-id="a9693-153">Here's an example of an operational log JSON string:</span></span>

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="a9693-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9693-154">Next steps</span></span>

<span data-ttu-id="a9693-155">Pour en savoir plus sur Service Bus, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="a9693-155">Visit the following links to learn more about Service Bus:</span></span>

* [<span data-ttu-id="a9693-156">Introduction à Service Bus</span><span class="sxs-lookup"><span data-stu-id="a9693-156">Introduction to Service Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="a9693-157">Bien démarrer avec Service Bus</span><span class="sxs-lookup"><span data-stu-id="a9693-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
