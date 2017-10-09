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
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Consigner des événements pour l’analyse et l’évaluation de diagnostic des solutions Batch

Comme avec nombreux services Azure, hello service Batch émet des événements de journal pour certaines ressources pendant hello durée de vie de la ressource de hello. Vous pouvez activer des événements de toorecord de journaux de diagnostic Azure Batch pour les ressources, telles que les pools et les tâches et ensuite utiliser les journaux de hello pour l’évaluation de diagnostic et de suivi. Des événements tels qu’une création de pool, une suppression de pool, un démarrage de tâche ou un achèvement de tâche sont consignés dans les journaux de diagnostic de Batch.

> [!NOTE]
> Cet article décrit la journalisation d’événements pour les ressources de compte Batch, pas les données de sortie de travail et de tâche. Pour plus d’informations sur le stockage des données de sortie hello des travaux et des tâches, consultez [sortie de projet et la tâche de rendre persistantes Azure Batch](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Composants requis
* [Compte Azure Batch](batch-account-create-portal.md)
* [compte Stockage Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  journaux de diagnostic de lot toopersist, vous devez créer un compte Azure Storage où Azure stocke les journaux hello. Vous spécifiez ce compte de stockage lorsque vous [activez la journalisation des diagnostics](#enable-diagnostic-logging) pour votre compte Batch. Hello compte de stockage que vous spécifiez lorsque vous activez la collecte de journaux est même hello pas comme un hello tooin référencé du compte stockage [les packages d’applications](batch-application-packages.md) et [sortie de la tâche persistance](batch-task-output.md) articles.
  
  > [!WARNING]
  > Vous êtes **facturé** pour les données de hello stockées dans votre compte de stockage Azure. Cela inclut les journaux de diagnostic hello abordés dans cet article. Gardez cela à l’esprit lorsque vous élaborez votre [stratégie de rétention des journaux](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Activer la journalisation des diagnostics
La journalisation des diagnostics n’est pas activée par défaut pour votre compte Batch. Vous devez explicitement activer la journalisation des diagnostics pour chaque compte de traitement par lots toomonitor :

[La collection tooenable de journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

Nous vous recommandons de lire hello complète [vue d’ensemble de Azure des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain comprendre non seulement comment tooenable journalisation mais hello du journal catégories pris en charge par hello divers services Azure. Par exemple, Azure Batch prend actuellement en charge une seule catégorie de journal, celle des **journaux de service**.

## <a name="service-logs"></a>Journaux de service
Journaux de Service de traitement par lots Azure contiennent des événements émis par le service de traitement par lots Azure hello lors de la durée de vie hello d’une ressource de lot comme une tâche ou un pool. Chaque événement émis par lot est stocké dans hello spécifié compte de stockage au format JSON. Par exemple, il s’agit d’un exemple de corps de la hello **créer un pool événement**:

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

Chaque corps de l’événement réside dans un .json fichier Bonjour spécifié de compte de stockage Azure. Si vous souhaitez tooaccess hello directement les journaux, vous pouvez de tooreview hello [schéma des journaux de Diagnostic dans le compte de stockage hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>Événements du journal de service
Hello service Batch émet actuellement hello après les événements du journal du Service. Cette liste n’est peut-être pas exhaustive, car des événements supplémentaires peuvent avoir été ajoutés depuis la dernière mise à jour de cet article.

| **Événements du journal de service** |
| --- |
| [Création de pool][pool_create] |
| [Démarrage de suppression de pool][pool_delete_start] |
| [Fin de suppression de pool][pool_delete_complete] |
| [Démarrage de redimensionnement de pool][pool_resize_start] |
| [Fin de redimensionnement de pool][pool_resize_complete] |
| [Démarrage de tâche][task_start] |
| [Fin de tâche][task_complete] |
| [Échec de la tâche][task_fail] |

## <a name="next-steps"></a>Étapes suivantes
Dans les événements de journal de diagnostics toostoring ajout dans un compte de stockage Azure, vous pouvez aussi diffuser tooan des événements de journal du Service Batch [concentrateur d’événements Azure](../event-hubs/event-hubs-what-is-event-hubs.md)et les envoyer de trop[Analytique de journal Azure](../log-analytics/log-analytics-overview.md).

* [Flux de données des journaux de Diagnostic Azure tooEvent concentrateurs](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Flux de service Batch des événements de diagnostic toohello données hautement évolutive en entrée, les concentrateurs d’événements. Le service Event Hubs peut traiter à chaque seconde des millions d’événements que vous pouvez transformer et stocker à l’aide de tout fournisseur d’analyses en temps réel.
* [Analyser les journaux de diagnostic Azure à l’aide de Log Analytics](../log-analytics/log-analytics-azure-storage.md)
  
  Envoyez votre tooLog de journaux de diagnostic Analytique où vous pouvez les analyser dans le portail Operations Management Suite (OMS) de hello, ou les exporter pour analyse dans Power BI ou Excel.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
