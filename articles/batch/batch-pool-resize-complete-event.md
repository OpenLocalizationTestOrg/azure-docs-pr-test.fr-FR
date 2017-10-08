---
title: "AAA « pool Azure Batch redimensionner l’événement complete | Documents Microsoft »"
description: "Référence pour l’événement de fin de redimensionnement de pool Batch."
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>Événement de fin de redimensionnement de pool

 Cet événement est émis quand un redimensionnement de pool est terminé ou a échoué.

 Hello suivant montre les corps hello d’un événement de redimensionnement complète pool d’un pool a augmenté en taille et s’est terminée correctement.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|Élément|Type|Remarques|
|-------------|----------|-----------|
|id|String|id de Hello du pool de hello.|
|nodeDeallocationOption|String|Spécifie quand les nœuds peuvent être supprimées de pool de hello, si la taille du pool hello baisse.<br /><br /> Les valeurs possibles sont les suivantes :<br /><br /> **requeue** : arrêter les tâches en cours d’exécution et les replacer en file d’attente. Hello tâches seront réexécutées quand le travail hello est activé. Supprimez les nœuds dès que les tâches sont terminées.<br /><br /> **terminate** : mettre fin aux tâches en cours d’exécution. tâches de Hello ne s’exécutera pas à nouveau. Supprimez les nœuds dès que les tâches sont terminées.<br /><br /> **taskcompletion** – autoriser le toocomplete de tâches en cours d’exécution. Ne planifiez aucune nouvelle tâche en attendant. Supprimer les nœuds quand toutes les tâches sont terminées.<br /><br /> **Retaineddata** : toocomplete de tâches en cours d’exécution, puis attendre que toutes les tâches tooexpire de périodes de rétention de données. Ne planifiez aucune nouvelle tâche en attendant. Supprimez les nœuds une fois que toutes les périodes de rétention ont expiré.<br /><br /> valeur par défaut de Hello est remettre.<br /><br /> Si l’augmentation de taille du pool de hello, hello a la valeur trop**non valide**.|
|currentDedicated|Int32|nombre de Hello de nœuds de calcul actuellement attribués toohello pool.|
|targetDedicated|Int32|nombre de Hello de nœuds de calcul qui sont demandées pour le pool de hello.|
|enableAutoScale|Bool|Spécifie si taille du pool hello s’ajuste automatiquement au fil du temps.|
|isAutoPool|Bool|Spécifie si le pool de hello a été créé via le mécanisme de pool automatique d’un travail.|
|startTime|DateTime|Hello de redimensionnement du pool de hello début.|
|endTime|DateTime|Hello temps de redimensionnement du pool de hello s’est terminée.|
|resultCode|String|résultat de Hello Hello redimensionner.|
|resultMessage|String|Erreur de redimensionnement Hello comprend des détails de hello du résultat de hello.<br /><br /> Si hello redimensionner terminée il États hello la réussite de l’opération.|
