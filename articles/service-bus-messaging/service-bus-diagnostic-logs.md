---
title: les journaux de diagnostic de Service Bus aaaAzure | Documents Microsoft
description: "Découvrez comment tooset des journaux de diagnostic pour Service Bus dans Azure."
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
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a><span data-ttu-id="f4364-103">Journaux de diagnostic Service Bus</span><span class="sxs-lookup"><span data-stu-id="f4364-103">Service Bus diagnostic logs</span></span>

<span data-ttu-id="f4364-104">Vous pouvez afficher deux types de journaux pour Azure Service Bus :</span><span class="sxs-lookup"><span data-stu-id="f4364-104">You can view two types of logs for Azure Service Bus:</span></span>
* <span data-ttu-id="f4364-105">**[Journaux d’activité](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="f4364-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="f4364-106">Ces journaux contiennent des informations sur les opérations effectuées sur un travail.</span><span class="sxs-lookup"><span data-stu-id="f4364-106">These logs contain information about operations performed on a job.</span></span> <span data-ttu-id="f4364-107">Hello journaux sont toujours activés.</span><span class="sxs-lookup"><span data-stu-id="f4364-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="f4364-108">**[Journaux de diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="f4364-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="f4364-109">Vous pouvez configurer les journaux de diagnostic pour obtenir des informations plus détaillés sur tous les événements associés à un travail.</span><span class="sxs-lookup"><span data-stu-id="f4364-109">You can configure diagnostic logs for richer information about everything that happens within a job.</span></span> <span data-ttu-id="f4364-110">Activités de couverture de journaux de diagnostic de hello création des travaux de hello jusqu'à ce que le travail de hello est supprimé, y compris les mises à jour et les activités qui se produisent pendant l’exécution du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="f4364-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="f4364-111">Activer les journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="f4364-111">Turn on diagnostic logs</span></span>

<span data-ttu-id="f4364-112">Les journaux de diagnostic sont désactivés par défaut.</span><span class="sxs-lookup"><span data-stu-id="f4364-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="f4364-113">journaux de diagnostic tooenable, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f4364-113">tooenable diagnostic logs, perform hello following steps:</span></span>

1.  <span data-ttu-id="f4364-114">Bonjour [portail Azure](https://portal.azure.com), sous **analyse + gestion**, cliquez sur **les journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="f4364-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Panneau navigation toodiagnostic journaux](./media/service-bus-diagnostic-logs/image1.png)

2. <span data-ttu-id="f4364-116">Cliquez sur ressource hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="f4364-116">Click hello resource you want toomonitor.</span></span>  

3.  <span data-ttu-id="f4364-117">Cliquez sur **Activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="f4364-117">Click **Turn on diagnostics**.</span></span>

    ![activer les journaux de diagnostic](./media/service-bus-diagnostic-logs/image2.png)

4.  <span data-ttu-id="f4364-119">Pour l’**état**, cliquez sur **ACTIVÉ**.</span><span class="sxs-lookup"><span data-stu-id="f4364-119">For **Status**, click **On**.</span></span>

    ![modifier l’état des journaux de diagnostic](./media/service-bus-diagnostic-logs/image3.png)

5.  <span data-ttu-id="f4364-121">Ensemble hello archive cible que vous le souhaitez. par exemple, un compte de stockage, un Hub d’événements ou Analytique des journaux Azure.</span><span class="sxs-lookup"><span data-stu-id="f4364-121">Set hello archive target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="f4364-122">Enregistrer les nouveaux paramètres de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="f4364-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="f4364-123">Les nouveaux paramètres prennent effet au bout de 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="f4364-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="f4364-124">Après cela, des journaux apparaissent dans la cible d’archivage hello configuré, sur hello **les journaux de diagnostic** panneau.</span><span class="sxs-lookup"><span data-stu-id="f4364-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="f4364-125">Pour plus d’informations sur la configuration des diagnostics, consultez hello [vue d’ensemble des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="f4364-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="f4364-126">Schéma des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="f4364-126">Diagnostic logs schema</span></span>

<span data-ttu-id="f4364-127">Tous les journaux sont stockés au format JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="f4364-127">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="f4364-128">Chaque entrée comporte des champs de chaîne qui utilisent le format hello décrit Bonjour suivant la section.</span><span class="sxs-lookup"><span data-stu-id="f4364-128">Each entry has string fields that use hello format described in hello following section.</span></span>

## <a name="operational-logs-schema"></a><span data-ttu-id="f4364-129">Schéma des journaux des opérations</span><span class="sxs-lookup"><span data-stu-id="f4364-129">Operational logs schema</span></span>

<span data-ttu-id="f4364-130">Se connecte hello **OperationalLogs** catégorie capturer que se passe-t-il lors des opérations de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f4364-130">Logs in hello **OperationalLogs** category capture what happens during Service Bus operations.</span></span> <span data-ttu-id="f4364-131">Plus précisément, ces journaux capturer le type d’opération hello, y compris la création de file d’attente, les ressources utilisées et hello l’état de fonctionnement de hello.</span><span class="sxs-lookup"><span data-stu-id="f4364-131">Specifically, these logs capture hello operation type, including queue creation, resources used, and hello status of hello operation.</span></span>

<span data-ttu-id="f4364-132">Chaînes JSON de journal des opérations incluent les éléments répertoriés dans hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="f4364-132">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="f4364-133">Nom</span><span class="sxs-lookup"><span data-stu-id="f4364-133">Name</span></span> | <span data-ttu-id="f4364-134">Description</span><span class="sxs-lookup"><span data-stu-id="f4364-134">Description</span></span>
------- | -------
<span data-ttu-id="f4364-135">ActivityId</span><span class="sxs-lookup"><span data-stu-id="f4364-135">ActivityId</span></span> | <span data-ttu-id="f4364-136">ID interne, utilisé à des fins de suivi</span><span class="sxs-lookup"><span data-stu-id="f4364-136">Internal ID, used for tracking</span></span>
<span data-ttu-id="f4364-137">EventName</span><span class="sxs-lookup"><span data-stu-id="f4364-137">EventName</span></span> | <span data-ttu-id="f4364-138">Nom d’opération</span><span class="sxs-lookup"><span data-stu-id="f4364-138">Operation name</span></span>           
<span data-ttu-id="f4364-139">resourceId</span><span class="sxs-lookup"><span data-stu-id="f4364-139">resourceId</span></span> | <span data-ttu-id="f4364-140">ID de ressource Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f4364-140">Azure Resource Manager resource ID</span></span>
<span data-ttu-id="f4364-141">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="f4364-141">SubscriptionId</span></span> | <span data-ttu-id="f4364-142">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="f4364-142">Subscription ID</span></span>
<span data-ttu-id="f4364-143">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="f4364-143">EventTimeString</span></span> | <span data-ttu-id="f4364-144">Durée de l’opération</span><span class="sxs-lookup"><span data-stu-id="f4364-144">Operation time</span></span>
<span data-ttu-id="f4364-145">EventProperties</span><span class="sxs-lookup"><span data-stu-id="f4364-145">EventProperties</span></span> | <span data-ttu-id="f4364-146">Propriétés de l’opération</span><span class="sxs-lookup"><span data-stu-id="f4364-146">Operation properties</span></span>
<span data-ttu-id="f4364-147">État</span><span class="sxs-lookup"><span data-stu-id="f4364-147">Status</span></span> | <span data-ttu-id="f4364-148">État de l’opération</span><span class="sxs-lookup"><span data-stu-id="f4364-148">Operation status</span></span>
<span data-ttu-id="f4364-149">Appelant</span><span class="sxs-lookup"><span data-stu-id="f4364-149">Caller</span></span> | <span data-ttu-id="f4364-150">Appelant de l’opération (portail Azure ou client de gestion)</span><span class="sxs-lookup"><span data-stu-id="f4364-150">Caller of operation (Azure portal or management client)</span></span>
<span data-ttu-id="f4364-151">category</span><span class="sxs-lookup"><span data-stu-id="f4364-151">category</span></span> | <span data-ttu-id="f4364-152">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="f4364-152">OperationalLogs</span></span>

<span data-ttu-id="f4364-153">Voici un exemple de chaîne JSON du journal des opérations :</span><span class="sxs-lookup"><span data-stu-id="f4364-153">Here's an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f4364-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4364-154">Next steps</span></span>

<span data-ttu-id="f4364-155">Visitez hello suivant les liens toolearn plus sur le Bus de Service :</span><span class="sxs-lookup"><span data-stu-id="f4364-155">Visit hello following links toolearn more about Service Bus:</span></span>

* [<span data-ttu-id="f4364-156">Introduction tooService Bus</span><span class="sxs-lookup"><span data-stu-id="f4364-156">Introduction tooService Bus</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="f4364-157">Bien démarrer avec Service Bus</span><span class="sxs-lookup"><span data-stu-id="f4364-157">Get started with Service Bus</span></span>](service-bus-dotnet-get-started-with-queues.md)
