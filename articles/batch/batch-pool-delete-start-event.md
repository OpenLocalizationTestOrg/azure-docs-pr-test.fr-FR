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
# <a name="pool-delete-start-event"></a><span data-ttu-id="557ab-103">Événement de début de suppression de pool</span><span class="sxs-lookup"><span data-stu-id="557ab-103">Pool delete start event</span></span>

 <span data-ttu-id="557ab-104">Cet événement est émis quand une opération de suppression du pool a commencé.</span><span class="sxs-lookup"><span data-stu-id="557ab-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="557ab-105">Suppression de pools de hello étant un événement asynchrone, vous pouvez vous attendre un toobe complète des événements de suppression de pool émis une fois l’opération de suppression hello se termine.</span><span class="sxs-lookup"><span data-stu-id="557ab-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="557ab-106">Hello suivant montre les corps de hello d’un événement de début de suppression de pool.</span><span class="sxs-lookup"><span data-stu-id="557ab-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="557ab-107">Élément</span><span class="sxs-lookup"><span data-stu-id="557ab-107">Element</span></span>|<span data-ttu-id="557ab-108">Type</span><span class="sxs-lookup"><span data-stu-id="557ab-108">Type</span></span>|<span data-ttu-id="557ab-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="557ab-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="557ab-110">id</span><span class="sxs-lookup"><span data-stu-id="557ab-110">id</span></span>|<span data-ttu-id="557ab-111">String</span><span class="sxs-lookup"><span data-stu-id="557ab-111">String</span></span>|<span data-ttu-id="557ab-112">id de Hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="557ab-112">hello id of hello pool.</span></span>|
