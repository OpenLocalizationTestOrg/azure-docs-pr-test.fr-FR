---
title: "Événement de fin de suppression de pool Azure Batch | Microsoft Docs"
description: "Référence pour l’événement de fin de suppression de pool Batch."
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
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="03f3d-103">Événement de fin de suppression de pool</span><span class="sxs-lookup"><span data-stu-id="03f3d-103">Pool delete complete event</span></span>

 <span data-ttu-id="03f3d-104">Cet événement est émis quand une opération de suppression de pool est terminée.</span><span class="sxs-lookup"><span data-stu-id="03f3d-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="03f3d-105">L’exemple suivant montre le corps d’un événement de fin de suppression de pool.</span><span class="sxs-lookup"><span data-stu-id="03f3d-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="03f3d-106">Élément</span><span class="sxs-lookup"><span data-stu-id="03f3d-106">Element</span></span>|<span data-ttu-id="03f3d-107">Type</span><span class="sxs-lookup"><span data-stu-id="03f3d-107">Type</span></span>|<span data-ttu-id="03f3d-108">Remarques</span><span class="sxs-lookup"><span data-stu-id="03f3d-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="03f3d-109">id</span><span class="sxs-lookup"><span data-stu-id="03f3d-109">id</span></span>|<span data-ttu-id="03f3d-110">String</span><span class="sxs-lookup"><span data-stu-id="03f3d-110">String</span></span>|<span data-ttu-id="03f3d-111">ID du pool.</span><span class="sxs-lookup"><span data-stu-id="03f3d-111">The id of the pool.</span></span>|
|<span data-ttu-id="03f3d-112">startTime</span><span class="sxs-lookup"><span data-stu-id="03f3d-112">startTime</span></span>|<span data-ttu-id="03f3d-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="03f3d-113">DateTime</span></span>|<span data-ttu-id="03f3d-114">Heure de début de la suppression du pool.</span><span class="sxs-lookup"><span data-stu-id="03f3d-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="03f3d-115">endTime</span><span class="sxs-lookup"><span data-stu-id="03f3d-115">endTime</span></span>|<span data-ttu-id="03f3d-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="03f3d-116">DateTime</span></span>|<span data-ttu-id="03f3d-117">Heure de fin de la suppression du pool.</span><span class="sxs-lookup"><span data-stu-id="03f3d-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="03f3d-118">Remarques</span><span class="sxs-lookup"><span data-stu-id="03f3d-118">Remarks</span></span>
<span data-ttu-id="03f3d-119">Pour plus d’informations sur les états et les codes d’erreur pour l’opération de redimensionnement de pool, voir [Supprimer un pool d’un compte](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="03f3d-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>