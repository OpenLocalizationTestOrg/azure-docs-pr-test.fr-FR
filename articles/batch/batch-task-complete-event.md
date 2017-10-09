---
title: "AAA « événement complète de tâche de traitement par lots Azure | Documents Microsoft »"
description: "Référence pour l’événement de fin de tâche Batch."
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
ms.openlocfilehash: c126bf897071c008be3d24190cf77bba5878b807
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="task-complete-event"></a>Événement de fin de tâche

 Cet événement est émis une fois qu’une tâche est terminée, quel que soit le code de sortie hello. Cet événement peut être durée de hello toodetermine utilisé d’une tâche, où a exécuté la tâche hello et si elle a été tentée.


 Hello suivant montre les corps de hello d’un événement de tâche terminé.

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
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|jobId|String|id de Hello du travail hello contenant la tâche hello.|
|id|String|id de Hello de tâche hello.|
|taskType|String|type de Hello de tâche hello. Ce peut être « JobManager », indiquant qu’il s’agit une tâche du gestionnaire, ou « User », indiquant qu’il ne s’agit pas d’une tâche du gestionnaire. Cet événement n’est pas émis pour des tâches de préparation du travail, des tâches de fin de travail ou des tâches de démarrage.|
|systemTaskVersion|Int32|Il s’agit de compteur de nouvelles tentatives internes hello sur une tâche. En interne, service de traitement par lots hello peut réessayer un tooaccount de tâche pour les problèmes temporaires. Ces problèmes peuvent inclure interne toorecover erreurs ou des tentatives de planification à partir des nœuds de calcul dans un état incorrect.|
|[nodeInfo](#nodeInfo)|Type complexe|Contient des informations sur le nœud de calcul hello sur quel hello tâche s’est exécutée.|
|[multiInstanceSettings](#multiInstanceSettings)|Type complexe|Spécifie que cette tâche hello est une tâche de plusieurs instances nécessitant plusieurs nœuds de calcul.  Pour plus d’informations, voir [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).|
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
|numberOfInstances|Int32|nombre de Hello de nœuds de calcul requis par la tâche hello.|

###  <a name="constraints"></a> constraints

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Bonjour le nombre maximal de tentatives de tâche hello peut être. Hello service Batch tente de renvoyer une tâche si son code de sortie est différent de zéro.<br /><br /> Notez que cette valeur contrôle spécifiquement nombre hello de nouvelles tentatives. service de traitement par lots Hello va tenter de tâche hello qu’une seule fois et peut être relancé puis des toothis limite. Par exemple, si le nombre maximal de tentatives de hello est 3, lot tente une tâche too4 fois (une fois initiale et 3 tentatives).<br /><br /> Si le nombre maximal de tentatives de hello est 0, hello service Batch ne réessaie pas de tâches.<br /><br /> Si le nombre maximal de tentatives de hello est -1, service de traitement par lots hello réessaie tâches sans limite.<br /><br /> Hello par défaut est 0 (aucune nouvelle tentative).|

###  <a name="executionInfo"></a> executionInfo

|Nom de l'élément|Type|Remarques|
|------------------|----------|-----------|
|startTime|DateTime|heure de Hello à quelle tâche hello a démarré. « En cours d’exécution » correspond à toohello **en cours d’exécution** d’état, de sorte que si la tâche hello spécifie les fichiers de ressources ou des packages d’applications, l’heure de début hello reflète temps hello au démarrage du téléchargement ou déploiement de ces tâches hello.  Si la tâche hello a été redémarré ou renouvelée, il s’agit de hello heure la plus récente à la tâche hello a démarré.|
|endTime|DateTime|heure de Hello à quelle tâche hello s’est terminée.|
|exitCode|Int32|code de sortie Hello de tâche hello.|
|retryCount|Int32|Bonjour le nombre de tentatives de tâche hello par le service de traitement par lots hello. tâche Hello est retentée si elle se termine avec un code de sortie différent de zéro, les toohello spécifié MaxTaskRetryCount.|
|requeueCount|Int32|Bonjour le nombre de fois tâche hello a été remis en service de traitement par lots hello en tant que résultat de hello d’une demande de l’utilisateur.<br /><br /> Lorsque les supprime d’utilisateur hello nœuds à partir d’un pool (en les redimensionnant ou réduction hello pool) ou lorsque hello travail est désactivé, l’utilisateur de hello peuvent spécifier que les tâches en cours d’exécution sur les nœuds hello être remis pour l’exécution. Ce nombre reflète le nombre de fois où tâche hello a été remis pour ces raisons.|
