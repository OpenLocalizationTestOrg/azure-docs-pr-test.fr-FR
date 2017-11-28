---
title: "Activer la journalisation des événements de lot - Azure | Microsoft Docs"
description: "Enregistrez et analysez les événements du journal de diagnostic pour des ressources de compte Azure Batch telles que des pools et des tâches."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7bc6fd9921ab0f2374ace33ea5c1ab93a78f860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="33e68-103">Consigner des événements pour l’analyse et l’évaluation de diagnostic des solutions Batch</span><span class="sxs-lookup"><span data-stu-id="33e68-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="33e68-104">Comme de nombreux services Azure, le service Batch génère des événements de journal pour certaines ressources pendant la durée de vie de celles-ci.</span><span class="sxs-lookup"><span data-stu-id="33e68-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="33e68-105">Vous pouvez activer les journaux de diagnostic Azure Batch afin d’enregistrer des événements pour des ressources telles que des pools et des tâches, puis utiliser les journaux à des fins d’évaluation et d’analyse des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="33e68-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="33e68-106">Des événements tels qu’une création de pool, une suppression de pool, un démarrage de tâche ou un achèvement de tâche sont consignés dans les journaux de diagnostic de Batch.</span><span class="sxs-lookup"><span data-stu-id="33e68-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="33e68-107">Cet article décrit la journalisation d’événements pour les ressources de compte Batch, pas les données de sortie de travail et de tâche.</span><span class="sxs-lookup"><span data-stu-id="33e68-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="33e68-108">Pour plus d’informations sur le stockage des données de sortie des travaux et des tâches, voir [Conserver une sortie de tâche et de travail Azure Batch](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="33e68-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="33e68-109">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="33e68-109">Prerequisites</span></span>
* [<span data-ttu-id="33e68-110">Compte Azure Batch</span><span class="sxs-lookup"><span data-stu-id="33e68-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="33e68-111">Compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="33e68-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="33e68-112">Pour conserver les journaux de diagnostic de Batch, vous devez créer un compte Stockage Azure dans lequel Azure stocke les journaux.</span><span class="sxs-lookup"><span data-stu-id="33e68-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="33e68-113">Vous spécifiez ce compte de stockage lorsque vous [activez la journalisation des diagnostics](#enable-diagnostic-logging) pour votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="33e68-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="33e68-114">Le compte de stockage que vous spécifiez lorsque vous activez la collecte de journaux n’est pas identique à un compte de stockage lié tel que décrit dans les articles relatifs aux [packages d’application](batch-application-packages.md) et à la [persistance en sortie des tâches](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="33e68-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="33e68-115">Vous êtes **facturé** pour les données stockées dans votre compte de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="33e68-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="33e68-116">Cela inclut les journaux de diagnostic abordés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="33e68-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="33e68-117">Gardez cela à l’esprit lorsque vous élaborez votre [stratégie de rétention des journaux](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="33e68-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="33e68-118">Activer la journalisation des diagnostics</span><span class="sxs-lookup"><span data-stu-id="33e68-118">Enable diagnostic logging</span></span>
<span data-ttu-id="33e68-119">La journalisation des diagnostics n’est pas activée par défaut pour votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="33e68-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="33e68-120">Vous devez activer explicitement la journalisation des diagnostics pour chaque compte Batch à analyser :</span><span class="sxs-lookup"><span data-stu-id="33e68-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="33e68-121">Comment activer la collecte des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="33e68-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="33e68-122">Nous vous recommandons de lire entièrement l’article [Présentation des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) pour comprendre non seulement comment activer la journalisation, mais aussi les catégories de journal prises en charge par les divers services Azure.</span><span class="sxs-lookup"><span data-stu-id="33e68-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="33e68-123">Par exemple, Azure Batch prend actuellement en charge une seule catégorie de journal, celle des **journaux de service**.</span><span class="sxs-lookup"><span data-stu-id="33e68-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="33e68-124">Journaux de service</span><span class="sxs-lookup"><span data-stu-id="33e68-124">Service Logs</span></span>
<span data-ttu-id="33e68-125">Les journaux de service Azure Batch contiennent des événements signalés par le service Azure Batch pendant la durée de vie d’une ressource Batch telle qu’un pool ou une tâche.</span><span class="sxs-lookup"><span data-stu-id="33e68-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="33e68-126">Chaque événement émis par Batch est stocké dans le compte de stockage spécifié au format JSON.</span><span class="sxs-lookup"><span data-stu-id="33e68-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="33e68-127">Par exemple, ceci est le corps d’un exemple d’**événement de création de pool** :</span><span class="sxs-lookup"><span data-stu-id="33e68-127">For example, this is the body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="33e68-128">Chaque corps d’événement réside dans un fichier .json dans le compte de Stockage Azure spécifié.</span><span class="sxs-lookup"><span data-stu-id="33e68-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="33e68-129">Si vous souhaitez accéder directement aux journaux, vous pouvez consulter le [Schéma des journaux de diagnostic dans le compte de stockage](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="33e68-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="33e68-130">Événements du journal de service</span><span class="sxs-lookup"><span data-stu-id="33e68-130">Service Log events</span></span>
<span data-ttu-id="33e68-131">Actuellement, le service Batch émet les événements du journal de service suivants.</span><span class="sxs-lookup"><span data-stu-id="33e68-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="33e68-132">Cette liste n’est peut-être pas exhaustive, car des événements supplémentaires peuvent avoir été ajoutés depuis la dernière mise à jour de cet article.</span><span class="sxs-lookup"><span data-stu-id="33e68-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="33e68-133">**Événements du journal de service**</span><span class="sxs-lookup"><span data-stu-id="33e68-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="33e68-134">[Création de pool][pool_create]</span><span class="sxs-lookup"><span data-stu-id="33e68-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="33e68-135">[Démarrage de suppression de pool][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="33e68-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="33e68-136">[Fin de suppression de pool][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="33e68-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="33e68-137">[Démarrage de redimensionnement de pool][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="33e68-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="33e68-138">[Fin de redimensionnement de pool][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="33e68-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="33e68-139">[Démarrage de tâche][task_start]</span><span class="sxs-lookup"><span data-stu-id="33e68-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="33e68-140">[Fin de tâche][task_complete]</span><span class="sxs-lookup"><span data-stu-id="33e68-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="33e68-141">[Échec de la tâche][task_fail]</span><span class="sxs-lookup"><span data-stu-id="33e68-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="33e68-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="33e68-142">Next steps</span></span>
<span data-ttu-id="33e68-143">Outre le stockage d’événements du journal de diagnostic dans un compte de Stockage Azure, vous pouvez diffuser des événements de journal de service Batch sur un [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), puis les envoyer à [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33e68-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="33e68-144">Stream Azure Diagnostic Logs to Event Hubs (Diffuser en continu les journaux de diagnostic Azure vers Event Hubs)</span><span class="sxs-lookup"><span data-stu-id="33e68-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="33e68-145">Diffusez les événements de diagnostic de Batch vers le service d’entrée de données hautement extensible Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="33e68-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="33e68-146">Le service Event Hubs peut traiter à chaque seconde des millions d’événements que vous pouvez transformer et stocker à l’aide de tout fournisseur d’analyses en temps réel.</span><span class="sxs-lookup"><span data-stu-id="33e68-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="33e68-147">Analyser les journaux de diagnostic Azure à l’aide de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="33e68-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="33e68-148">Envoyez vos journaux de diagnostic à Log Analytics où vous pouvez les analyser via le portail Operations Management Suite (OMS), ou les exporter à des fins d’analyse vers Power BI ou Excel.</span><span class="sxs-lookup"><span data-stu-id="33e68-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
