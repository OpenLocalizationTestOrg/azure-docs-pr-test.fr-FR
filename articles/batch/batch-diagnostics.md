---
title: "aaaEnable journalisation des diagnostics pour les événements de traitement par lots - Azure | Documents Microsoft"
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
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="505fd-103">Consigner des événements pour l’analyse et l’évaluation de diagnostic des solutions Batch</span><span class="sxs-lookup"><span data-stu-id="505fd-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="505fd-104">Comme avec nombreux services Azure, hello service Batch émet des événements de journal pour certaines ressources pendant hello durée de vie de la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="505fd-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="505fd-105">Vous pouvez activer des événements de toorecord de journaux de diagnostic Azure Batch pour les ressources, telles que les pools et les tâches et ensuite utiliser les journaux de hello pour l’évaluation de diagnostic et de suivi.</span><span class="sxs-lookup"><span data-stu-id="505fd-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="505fd-106">Des événements tels qu’une création de pool, une suppression de pool, un démarrage de tâche ou un achèvement de tâche sont consignés dans les journaux de diagnostic de Batch.</span><span class="sxs-lookup"><span data-stu-id="505fd-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="505fd-107">Cet article décrit la journalisation d’événements pour les ressources de compte Batch, pas les données de sortie de travail et de tâche.</span><span class="sxs-lookup"><span data-stu-id="505fd-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="505fd-108">Pour plus d’informations sur le stockage des données de sortie hello des travaux et des tâches, consultez [sortie de projet et la tâche de rendre persistantes Azure Batch](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="505fd-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="505fd-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="505fd-109">Prerequisites</span></span>
* [<span data-ttu-id="505fd-110">Compte Azure Batch</span><span class="sxs-lookup"><span data-stu-id="505fd-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="505fd-111">compte Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="505fd-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="505fd-112">journaux de diagnostic de lot toopersist, vous devez créer un compte Azure Storage où Azure stocke les journaux hello.</span><span class="sxs-lookup"><span data-stu-id="505fd-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="505fd-113">Vous spécifiez ce compte de stockage lorsque vous [activez la journalisation des diagnostics](#enable-diagnostic-logging) pour votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="505fd-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="505fd-114">Hello compte de stockage que vous spécifiez lorsque vous activez la collecte de journaux est même hello pas comme un hello tooin référencé du compte stockage [les packages d’applications](batch-application-packages.md) et [sortie de la tâche persistance](batch-task-output.md) articles.</span><span class="sxs-lookup"><span data-stu-id="505fd-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="505fd-115">Vous êtes **facturé** pour les données de hello stockées dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="505fd-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="505fd-116">Cela inclut les journaux de diagnostic hello abordés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="505fd-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="505fd-117">Gardez cela à l’esprit lorsque vous élaborez votre [stratégie de rétention des journaux](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="505fd-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="505fd-118">Activer la journalisation des diagnostics</span><span class="sxs-lookup"><span data-stu-id="505fd-118">Enable diagnostic logging</span></span>
<span data-ttu-id="505fd-119">La journalisation des diagnostics n’est pas activée par défaut pour votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="505fd-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="505fd-120">Vous devez explicitement activer la journalisation des diagnostics pour chaque compte de traitement par lots toomonitor :</span><span class="sxs-lookup"><span data-stu-id="505fd-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="505fd-121">La collection tooenable de journaux de Diagnostic</span><span class="sxs-lookup"><span data-stu-id="505fd-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="505fd-122">Nous vous recommandons de lire hello complète [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain comprendre non seulement comment tooenable journalisation mais hello du journal catégories pris en charge par hello divers services Azure.</span><span class="sxs-lookup"><span data-stu-id="505fd-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="505fd-123">Par exemple, Azure Batch prend actuellement en charge une seule catégorie de journal, celle des **journaux de service**.</span><span class="sxs-lookup"><span data-stu-id="505fd-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="505fd-124">Journaux de service</span><span class="sxs-lookup"><span data-stu-id="505fd-124">Service Logs</span></span>
<span data-ttu-id="505fd-125">Journaux de Service de traitement par lots Azure contiennent des événements émis par le service de traitement par lots Azure hello lors de la durée de vie hello d’une ressource de lot comme une tâche ou un pool.</span><span class="sxs-lookup"><span data-stu-id="505fd-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="505fd-126">Chaque événement émis par lot est stocké dans hello spécifié compte de stockage au format JSON.</span><span class="sxs-lookup"><span data-stu-id="505fd-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="505fd-127">Par exemple, il s’agit d’un exemple de corps de la hello **créer un pool événement**:</span><span class="sxs-lookup"><span data-stu-id="505fd-127">For example, this is hello body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="505fd-128">Chaque corps de l’événement réside dans un .json fichier Bonjour spécifié de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="505fd-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="505fd-129">Si vous souhaitez tooaccess hello directement les journaux, vous pouvez de tooreview hello [schéma des journaux de Diagnostic dans le compte de stockage hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="505fd-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="505fd-130">Événements du journal de service</span><span class="sxs-lookup"><span data-stu-id="505fd-130">Service Log events</span></span>
<span data-ttu-id="505fd-131">Hello service Batch émet actuellement hello après les événements du journal du Service.</span><span class="sxs-lookup"><span data-stu-id="505fd-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="505fd-132">Cette liste n’est peut-être pas exhaustive, car des événements supplémentaires peuvent avoir été ajoutés depuis la dernière mise à jour de cet article.</span><span class="sxs-lookup"><span data-stu-id="505fd-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="505fd-133">**Événements du journal de service**</span><span class="sxs-lookup"><span data-stu-id="505fd-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="505fd-134">[Création de pool][pool_create]</span><span class="sxs-lookup"><span data-stu-id="505fd-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="505fd-135">[Démarrage de suppression de pool][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="505fd-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="505fd-136">[Fin de suppression de pool][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="505fd-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="505fd-137">[Démarrage de redimensionnement de pool][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="505fd-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="505fd-138">[Fin de redimensionnement de pool][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="505fd-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="505fd-139">[Démarrage de tâche][task_start]</span><span class="sxs-lookup"><span data-stu-id="505fd-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="505fd-140">[Fin de tâche][task_complete]</span><span class="sxs-lookup"><span data-stu-id="505fd-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="505fd-141">[Échec de la tâche][task_fail]</span><span class="sxs-lookup"><span data-stu-id="505fd-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="505fd-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="505fd-142">Next steps</span></span>
<span data-ttu-id="505fd-143">Dans les événements de journal de diagnostics toostoring ajout dans un compte de stockage Azure, vous pouvez aussi diffuser tooan des événements de journal du Service Batch [concentrateur d’événements Azure](../event-hubs/event-hubs-what-is-event-hubs.md)et les envoyer de trop[Analytique de journal Azure](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="505fd-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="505fd-144">Flux de données des journaux de Diagnostic Azure tooEvent concentrateurs</span><span class="sxs-lookup"><span data-stu-id="505fd-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="505fd-145">Flux de service Batch des événements de diagnostic toohello données hautement évolutive en entrée, les concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="505fd-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="505fd-146">Le service Event Hubs peut traiter à chaque seconde des millions d’événements que vous pouvez transformer et stocker à l’aide de tout fournisseur d’analyses en temps réel.</span><span class="sxs-lookup"><span data-stu-id="505fd-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="505fd-147">Analyser les journaux de diagnostic Azure à l’aide de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="505fd-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="505fd-148">Envoyez votre tooLog de journaux de diagnostic Analytique où vous pouvez les analyser dans le portail Operations Management Suite (OMS) de hello, ou les exporter pour analyse dans Power BI ou Excel.</span><span class="sxs-lookup"><span data-stu-id="505fd-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
