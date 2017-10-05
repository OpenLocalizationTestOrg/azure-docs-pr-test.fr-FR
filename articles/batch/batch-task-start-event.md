---
title: "Événement de début de tâche Azure Batch | Microsoft Docs"
description: "Référence pour l’événement de début de tâche Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a>Événement de début de tâche

 Cet événement est émis quand une tâche est planifiée pour démarrer sur un nœud de calcul par le Scheduler. Notez que, si la tâche est retentée ou replacée en file d’attente, cet événement est ré-émis pour la même tâche, mais que le nombre de nouvelles tentatives et la version de la tâche système sont mis à jour en conséquence.


 L’exemple suivant montre le corps d’un événement de début de tâche.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|jobId|String|ID du travail contenant la tâche.|
|id|String|ID de la tâche.|
|taskType|String|Type de la tâche. Ce peut être « JobManager », indiquant qu’il s’agit une tâche du gestionnaire, ou « User », indiquant qu’il ne s’agit pas d’une tâche du gestionnaire.|
|systemTaskVersion|Int32|Compteur de tentatives internes d’exécution d’une tâche. En interne, le service Batch peut recommencer une tâche pour prendre en compte des problèmes temporaires. Ces problèmes peuvent être des erreurs de planification internes ou des tentatives de récupération à partir de nœuds de calcul en mauvais état.|
|[nodeInfo](#nodeInfo)|Type complexe|Contient des informations sur le nœud de calcul sur lequel la tâche a été exécutée.|
|[multiInstanceSettings](#multiInstanceSettings)|Type complexe|Spécifie que la tâche est une tâche multi-instance nécessitant plusieurs nœuds de calcul.  Pour plus d’informations, voir [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).|
|[constraints](#constraints)|Type complexe|Contraintes d’exécution qui s’appliquent à cette tâche.|
|[executionInfo](#executionInfo)|Type complexe|Contient des informations sur l’exécution de la tâche.|

###  <a name="nodeInfo"></a> nodeInfo

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|poolId|Chaîne|ID u pool sur lequel la tâche a été exécutée.|
|nodeId|String|ID du nœud sur lequel la tâche a été exécutée.|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|numberOfInstances|int|Nombre de nœuds de calcul requis pour la tâche.|

###  <a name="constraints"></a> constraints

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Nombre maximal de fois que la tâche peut être retentée. Le service Batch retente une tâche si le code de sortie de celle-ci diffère de zéro.<br /><br /> Notez que cette valeur contrôle spécifiquement le nombre de nouvelles tentatives. Le service Batch tente la tâche une fois et peut réessayer jusqu’à cette limite. Par exemple, si le nombre maximal de nouvelles tentatives est 3, le service Batch peut tenter d’exécuter la tâche jusqu’à 4 fois (tentative initiale + 3 tentatives supplémentaires).<br /><br /> Si le nombre maximal de tentatives est 0, le service Batch ne réessaye pas d’exécuter des tâches.<br /><br /> Si le nombre maximal de nouvelles tentatives est -1, le service Batch réessaie d’exécuter les tâches sans limite.<br /><br /> La valeur par défaut est 0 (aucune nouvelle tentative).|

###  <a name="executionInfo"></a> executionInfo

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|retryCount|Int32|Nombre de fois que le service Batch a réessayé d’exécuter la tâche. Si la tâche se termine avec un code de sortie autre que zéro, elle est retentée le nombre de fois spécifié par la valeur MaxTaskRetryCount|
