---
title: "AAA « pool Azure Batch supprimer l’événement complete | Documents Microsoft »"
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="0022f-103">Événement de fin de suppression de pool</span><span class="sxs-lookup"><span data-stu-id="0022f-103">Pool delete complete event</span></span>

 <span data-ttu-id="0022f-104">Cet événement est émis quand une opération de suppression de pool est terminée.</span><span class="sxs-lookup"><span data-stu-id="0022f-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="0022f-105">Hello suivant montre les corps hello d’un événement complète de suppression de pool.</span><span class="sxs-lookup"><span data-stu-id="0022f-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="0022f-106">Élément</span><span class="sxs-lookup"><span data-stu-id="0022f-106">Element</span></span>|<span data-ttu-id="0022f-107">Type</span><span class="sxs-lookup"><span data-stu-id="0022f-107">Type</span></span>|<span data-ttu-id="0022f-108">Remarques</span><span class="sxs-lookup"><span data-stu-id="0022f-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="0022f-109">id</span><span class="sxs-lookup"><span data-stu-id="0022f-109">id</span></span>|<span data-ttu-id="0022f-110">String</span><span class="sxs-lookup"><span data-stu-id="0022f-110">String</span></span>|<span data-ttu-id="0022f-111">id de Hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="0022f-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="0022f-112">startTime</span><span class="sxs-lookup"><span data-stu-id="0022f-112">startTime</span></span>|<span data-ttu-id="0022f-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="0022f-113">DateTime</span></span>|<span data-ttu-id="0022f-114">Hello supprimer du pool de hello début.</span><span class="sxs-lookup"><span data-stu-id="0022f-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="0022f-115">endTime</span><span class="sxs-lookup"><span data-stu-id="0022f-115">endTime</span></span>|<span data-ttu-id="0022f-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="0022f-116">DateTime</span></span>|<span data-ttu-id="0022f-117">Hello temps supprimer du pool de hello s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="0022f-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="0022f-118">Remarques</span><span class="sxs-lookup"><span data-stu-id="0022f-118">Remarks</span></span>
<span data-ttu-id="0022f-119">Pour plus d’informations sur les états et les codes d’erreur pour l’opération de redimensionnement de pool, voir [Supprimer un pool d’un compte](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="0022f-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>