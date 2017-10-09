---
title: "AAA « événement de début de tâche de traitement par lots Azure | Documents Microsoft »"
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>Événement de début de tâche

 Cet événement est émis une fois qu’une tâche a été planifiée toostart sur un nœud de calcul par le Planificateur de hello. Notez que si la tâche hello est retentée ou remis cet événement sera émis à nouveau pour hello même tâche, mais hello nombre de tentatives et la version de la tâche sera mis à jour en conséquence.


 Hello suivant montre les corps hello d’un événement de début de tâche.

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
|jobId|String|id de Hello du travail hello contenant la tâche hello.|
|id|String|id de Hello de tâche hello.|
|taskType|String|type de Hello de tâche hello. Ce peut être « JobManager », indiquant qu’il s’agit une tâche du gestionnaire, ou « User », indiquant qu’il ne s’agit pas d’une tâche du gestionnaire.|
|systemTaskVersion|Int32|Il s’agit de compteur de nouvelles tentatives internes hello sur une tâche. En interne, service de traitement par lots hello peut réessayer un tooaccount de tâche pour les problèmes temporaires. Ces problèmes peuvent inclure interne toorecover erreurs ou des tentatives de planification à partir des nœuds de calcul dans un état incorrect.|
|[nodeInfo](#nodeInfo)|Type complexe|Contient des informations sur le nœud de calcul hello sur quel hello tâche s’est exécutée.|
|[multiInstanceSettings](#multiInstanceSettings)|Type complexe|Spécifie que cette tâche hello est multi-instance nécessitant plusieurs nœuds de calcul.  Pour plus d’informations, voir [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).|
|[constraints](#constraints)|Type complexe|contraintes de l’exécution de Hello qui s’appliquent toothis tâche.|
|[executionInfo](#executionInfo)|Type complexe|Contient des informations sur l’exécution de hello de tâche hello.|

###  <a name="nodeInfo"></a> nodeInfo

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|poolId|String|id de Hello de pool hello sur quel hello tâche s’est exécutée.|
|nodeId|String|Hello l’id du nœud hello sur quel hello tâche s’est exécutée.|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|numberOfInstances|Int|nombre de Hello de nœuds de calcul requis par la tâche hello.|

###  <a name="constraints"></a> constraints

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Bonjour le nombre maximal de tentatives de tâche hello peut être. Hello service Batch tente de renvoyer une tâche si son code de sortie est différent de zéro.<br /><br /> Notez que cette valeur contrôle spécifiquement nombre hello de nouvelles tentatives. service de traitement par lots Hello va tenter de tâche hello qu’une seule fois et peut être relancé puis des toothis limite. Par exemple, si le nombre maximal de tentatives de hello est 3, lot tente une tâche too4 fois (une fois initiale et 3 tentatives).<br /><br /> Si le nombre maximal de tentatives de hello est 0, hello service Batch ne réessaie pas de tâches.<br /><br /> Si le nombre maximal de tentatives de hello est -1, service de traitement par lots hello réessaie tâches sans limite.<br /><br /> Hello par défaut est 0 (aucune nouvelle tentative).|

###  <a name="executionInfo"></a> executionInfo

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|retryCount|Int32|Bonjour le nombre de tentatives de tâche hello par le service de traitement par lots hello. tâche Hello est retentée si elle se termine avec un code de sortie différent de zéro, les toohello spécifié MaxTaskRetryCount|
