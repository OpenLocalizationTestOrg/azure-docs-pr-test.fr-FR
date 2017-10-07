---
title: aaaAzure Analytique de traitement par lots | Documents Microsoft
description: "Référence pour Azure Batch Analytics."
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
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a>Analyse en mode batch
les rubriques de Hello de traitement Analytique contiennent des informations de référence pour les événements de hello et alertes disponibles pour les ressources de service de traitement par lots.

Pour plus d’informations sur l’activation et l’utilisation des journaux de diagnostic de Batch, voir [Journalisation des diagnostics Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/).

## <a name="diagnostic-logs"></a>Journaux de diagnostic

Hello service Azure Batch émet hello suivant des événements du journal de diagnostic pendant la durée de vie hello de certaines ressources de traitement par lots.

**Événements du journal de service**
* [Création de pool](batch-pool-create-event.md)
* [Début de suppression de pool](batch-pool-delete-start-event.md)
* [Fin de suppression de pool](batch-pool-delete-complete-event.md)
* [Début de redimensionnement de pool](batch-pool-resize-start-event.md)
* [Fin de redimensionnement de pool](batch-pool-resize-complete-event.md)
* [Début de tâche](batch-task-start-event.md)
* [Fin de tâche](batch-task-complete-event.md)
* [Échec de tâche](batch-task-fail-event.md)