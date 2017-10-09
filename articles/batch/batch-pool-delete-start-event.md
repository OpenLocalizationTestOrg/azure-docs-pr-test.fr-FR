---
title: "AAA « événement de début de suppression de pool Azure Batch | Documents Microsoft »"
description: "Référence pour l’événement de début de suppression de pool Batch."
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a>Événement de début de suppression de pool

 Cet événement est émis quand une opération de suppression du pool a commencé. Suppression de pools de hello étant un événement asynchrone, vous pouvez vous attendre un toobe complète des événements de suppression de pool émis une fois l’opération de suppression hello se termine.

 Hello suivant montre les corps de hello d’un événement de début de suppression de pool.

```
{
    "id": "myPool1"
}
```

|Élément|Type|Remarques|
|-------------|----------|-----------|
|id|String|id de Hello du pool de hello.|
