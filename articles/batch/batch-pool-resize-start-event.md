---
title: "Événement de début de redimensionnement de pool Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="e6663-103">Événement de début de redimensionnement de pool</span><span class="sxs-lookup"><span data-stu-id="e6663-103">Pool resize start event</span></span>

 <span data-ttu-id="e6663-104">Cet événement est émis quand un redimensionnement de pool a commencé.</span><span class="sxs-lookup"><span data-stu-id="e6663-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="e6663-105">Étant donné que le redimensionnement de pool est un événement asynchrone, vous pouvez vous attendre à ce qu’un événement de fin de redimensionnement de pool soit émis au terme de l’opération de redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="e6663-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="e6663-106">L’exemple suivant montre le corps d’un événement de début de redimensionnement de pool pour redimensionnement de pool de 0 à 2 en mode manuel.</span><span class="sxs-lookup"><span data-stu-id="e6663-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="e6663-107">Élément</span><span class="sxs-lookup"><span data-stu-id="e6663-107">Element</span></span>|<span data-ttu-id="e6663-108">Type</span><span class="sxs-lookup"><span data-stu-id="e6663-108">Type</span></span>|<span data-ttu-id="e6663-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="e6663-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="e6663-110">poolId</span><span class="sxs-lookup"><span data-stu-id="e6663-110">poolId</span></span>|<span data-ttu-id="e6663-111">String</span><span class="sxs-lookup"><span data-stu-id="e6663-111">String</span></span>|<span data-ttu-id="e6663-112">ID du pool.</span><span class="sxs-lookup"><span data-stu-id="e6663-112">The id of the pool.</span></span>|
|<span data-ttu-id="e6663-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="e6663-113">nodeDeallocationOption</span></span>|<span data-ttu-id="e6663-114">Chaîne</span><span class="sxs-lookup"><span data-stu-id="e6663-114">String</span></span>|<span data-ttu-id="e6663-115">Spécifie quand des nœuds peuvent être supprimés du pool en cas de diminution de la taille du pool.</span><span class="sxs-lookup"><span data-stu-id="e6663-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="e6663-116">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6663-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="e6663-117">**requeue** : arrêter les tâches en cours d’exécution et les replacer en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="e6663-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="e6663-118">Les tâches sont ré-exécutées lors de l’activation du travail.</span><span class="sxs-lookup"><span data-stu-id="e6663-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="e6663-119">Supprimez les nœuds dès que les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="e6663-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="e6663-120">**terminate** : mettre fin aux tâches en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e6663-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="e6663-121">Les tâches ne sont pas ré-exécutées.</span><span class="sxs-lookup"><span data-stu-id="e6663-121">The tasks will not run again.</span></span> <span data-ttu-id="e6663-122">Supprimez les nœuds dès que les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="e6663-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="e6663-123">**taskcompletion** : autoriser l’achèvement des tâches en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e6663-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="e6663-124">Ne planifiez aucune nouvelle tâche en attendant.</span><span class="sxs-lookup"><span data-stu-id="e6663-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="e6663-125">Supprimer les nœuds quand toutes les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="e6663-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="e6663-126">**Retaineddata** : autoriser l’achèvement des tâches en cours d’exécution, puis attendre que toutes les périodes de rétention des données expirent.</span><span class="sxs-lookup"><span data-stu-id="e6663-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="e6663-127">Ne planifiez aucune nouvelle tâche en attendant.</span><span class="sxs-lookup"><span data-stu-id="e6663-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="e6663-128">Supprimez les nœuds une fois que toutes les périodes de rétention ont expiré.</span><span class="sxs-lookup"><span data-stu-id="e6663-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="e6663-129">La valeur par défaut est requeue.</span><span class="sxs-lookup"><span data-stu-id="e6663-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="e6663-130">Si la taille du pool augmente, cela signifie que la valeur est définie **invalide**.</span><span class="sxs-lookup"><span data-stu-id="e6663-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="e6663-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="e6663-131">currentDedicated</span></span>|<span data-ttu-id="e6663-132">Int32</span><span class="sxs-lookup"><span data-stu-id="e6663-132">Int32</span></span>|<span data-ttu-id="e6663-133">Nombre de nœuds de calcul actuellement affectés au pool.</span><span class="sxs-lookup"><span data-stu-id="e6663-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="e6663-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="e6663-134">targetDedicated</span></span>|<span data-ttu-id="e6663-135">Int32</span><span class="sxs-lookup"><span data-stu-id="e6663-135">Int32</span></span>|<span data-ttu-id="e6663-136">Nombre de nœuds de calcul demandés pour le pool.</span><span class="sxs-lookup"><span data-stu-id="e6663-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="e6663-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="e6663-137">enableAutoScale</span></span>|<span data-ttu-id="e6663-138">Bool</span><span class="sxs-lookup"><span data-stu-id="e6663-138">Bool</span></span>|<span data-ttu-id="e6663-139">Spécifie si la taille du pool s’ajuste automatiquement au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="e6663-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="e6663-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="e6663-140">isAutoPool</span></span>|<span data-ttu-id="e6663-141">Bool</span><span class="sxs-lookup"><span data-stu-id="e6663-141">Bool</span></span>|<span data-ttu-id="e6663-142">Spécifie si le pool a été créé via un mécanisme AutoPool du travail.</span><span class="sxs-lookup"><span data-stu-id="e6663-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
