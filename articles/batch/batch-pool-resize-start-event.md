---
title: "AAA « événement de démarrage de redimensionnement de pool de traitement par lots Azure | Documents Microsoft »"
description: "Référence pour l’événement de début de redimensionnement de pool Batch."
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>Événement de début de redimensionnement de pool

 Cet événement est émis quand un redimensionnement de pool a commencé. Redimensionnement du pool hello étant un événement asynchrone, vous pouvez vous attendre un toobe complète des événements de redimensionnement de pool émis une fois l’opération de redimensionnement hello se termine.

 redimensionne les Hello affiche hello corps d’un événement de début de redimensionnement de pool pour le redimensionnement d’un pool à partir des nœuds too2 0 d’une opération manuelle de l’exemple suivant.

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|Élément|Type|Remarques|
|-------------|----------|-----------|
|poolId|String|id de Hello du pool de hello.|
|nodeDeallocationOption|String|Spécifie quand les nœuds peuvent être supprimées de pool de hello, si la taille du pool hello baisse.<br /><br /> Les valeurs possibles sont les suivantes :<br /><br /> **requeue** : arrêter les tâches en cours d’exécution et les replacer en file d’attente. Hello tâches seront réexécutées quand le travail hello est activé. Supprimez les nœuds dès que les tâches sont terminées.<br /><br /> **terminate** : mettre fin aux tâches en cours d’exécution. tâches de Hello ne s’exécutera pas à nouveau. Supprimez les nœuds dès que les tâches sont terminées.<br /><br /> **taskcompletion** – autoriser le toocomplete de tâches en cours d’exécution. Ne planifiez aucune nouvelle tâche en attendant. Supprimer les nœuds quand toutes les tâches sont terminées.<br /><br /> **Retaineddata** : toocomplete de tâches en cours d’exécution, puis attendre que toutes les tâches tooexpire de périodes de rétention de données. Ne planifiez aucune nouvelle tâche en attendant. Supprimez les nœuds une fois que toutes les périodes de rétention ont expiré.<br /><br /> valeur par défaut de Hello est remettre.<br /><br /> Si l’augmentation de taille du pool de hello, hello a la valeur trop**non valide**.|
|currentDedicated|Int32|nombre de Hello de nœuds de calcul actuellement attribués toohello pool.|
|targetDedicated|Int32|nombre de Hello de nœuds de calcul qui sont demandées pour le pool de hello.|
|enableAutoScale|Bool|Spécifie si taille du pool hello s’ajuste automatiquement au fil du temps.|
|isAutoPool|Bool|Spécifie si le pool de hello a été créé via le mécanisme de pool automatique d’un travail.|
