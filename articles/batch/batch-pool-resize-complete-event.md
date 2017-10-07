---
title: "Événement de fin de redimensionnement de pool Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: 7072293d98526812cb42ce9c2f8e33bfcafaa149
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-complete-event"></a><span data-ttu-id="5b9d5-103">Événement de fin de redimensionnement de pool</span><span class="sxs-lookup"><span data-stu-id="5b9d5-103">Pool resize complete event</span></span>

 <span data-ttu-id="5b9d5-104">Cet événement est émis quand un redimensionnement de pool est terminé ou a échoué.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-104">This event is emitted when a pool resize has completed or failed.</span></span>

 <span data-ttu-id="5b9d5-105">L’exemple suivant montre le corps d’un événement de fin de redimensionnement de pool pour un pool dont l’augmentation de la taille s’est terminée correctement.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-105">The following example shows the body of a pool resize complete event for a pool that increased in size and completed successfully.</span></span>

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
    "resizeError": "The operation succeeded"
}
```

|<span data-ttu-id="5b9d5-106">Élément</span><span class="sxs-lookup"><span data-stu-id="5b9d5-106">Element</span></span>|<span data-ttu-id="5b9d5-107">Type</span><span class="sxs-lookup"><span data-stu-id="5b9d5-107">Type</span></span>|<span data-ttu-id="5b9d5-108">Remarques</span><span class="sxs-lookup"><span data-stu-id="5b9d5-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="5b9d5-109">id</span><span class="sxs-lookup"><span data-stu-id="5b9d5-109">id</span></span>|<span data-ttu-id="5b9d5-110">String</span><span class="sxs-lookup"><span data-stu-id="5b9d5-110">String</span></span>|<span data-ttu-id="5b9d5-111">ID du pool.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-111">The id of the pool.</span></span>|
|<span data-ttu-id="5b9d5-112">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="5b9d5-112">nodeDeallocationOption</span></span>|<span data-ttu-id="5b9d5-113">Chaîne</span><span class="sxs-lookup"><span data-stu-id="5b9d5-113">String</span></span>|<span data-ttu-id="5b9d5-114">Spécifie quand des nœuds peuvent être supprimés du pool en cas de diminution de la taille du pool.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-114">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="5b9d5-115">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b9d5-115">Possible values are:</span></span><br /><br /> <span data-ttu-id="5b9d5-116">**requeue** : arrêter les tâches en cours d’exécution et les replacer en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-116">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="5b9d5-117">Les tâches sont ré-exécutées lors de l’activation du travail.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-117">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="5b9d5-118">Supprimez les nœuds dès que les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-118">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="5b9d5-119">**terminate** : mettre fin aux tâches en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-119">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="5b9d5-120">Les tâches ne sont pas ré-exécutées.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-120">The tasks will not run again.</span></span> <span data-ttu-id="5b9d5-121">Supprimez les nœuds dès que les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-121">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="5b9d5-122">**taskcompletion** : autoriser l’achèvement des tâches en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-122">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="5b9d5-123">Ne planifiez aucune nouvelle tâche en attendant.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-123">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="5b9d5-124">Supprimer les nœuds quand toutes les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-124">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="5b9d5-125">**Retaineddata** : autoriser l’achèvement des tâches en cours d’exécution, puis attendre que toutes les périodes de rétention des données expirent.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-125">**Retaineddata** -  Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="5b9d5-126">Ne planifiez aucune nouvelle tâche en attendant.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-126">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="5b9d5-127">Supprimez les nœuds une fois que toutes les périodes de rétention ont expiré.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-127">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="5b9d5-128">La valeur par défaut est requeue.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-128">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="5b9d5-129">Si la taille du pool augmente, cela signifie que la valeur est définie **invalide**.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-129">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="5b9d5-130">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="5b9d5-130">currentDedicated</span></span>|<span data-ttu-id="5b9d5-131">Int32</span><span class="sxs-lookup"><span data-stu-id="5b9d5-131">Int32</span></span>|<span data-ttu-id="5b9d5-132">Nombre de nœuds de calcul actuellement affectés au pool.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-132">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="5b9d5-133">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="5b9d5-133">targetDedicated</span></span>|<span data-ttu-id="5b9d5-134">Int32</span><span class="sxs-lookup"><span data-stu-id="5b9d5-134">Int32</span></span>|<span data-ttu-id="5b9d5-135">Nombre de nœuds de calcul demandés pour le pool.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-135">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="5b9d5-136">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="5b9d5-136">enableAutoScale</span></span>|<span data-ttu-id="5b9d5-137">Bool</span><span class="sxs-lookup"><span data-stu-id="5b9d5-137">Bool</span></span>|<span data-ttu-id="5b9d5-138">Spécifie si la taille du pool s’ajuste automatiquement au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-138">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="5b9d5-139">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="5b9d5-139">isAutoPool</span></span>|<span data-ttu-id="5b9d5-140">Bool</span><span class="sxs-lookup"><span data-stu-id="5b9d5-140">Bool</span></span>|<span data-ttu-id="5b9d5-141">Spécifie si le pool a été créé via un mécanisme AutoPool du travail.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-141">Specifies whether the pool was created via a job's AutoPool mechanism.</span></span>|
|<span data-ttu-id="5b9d5-142">startTime</span><span class="sxs-lookup"><span data-stu-id="5b9d5-142">startTime</span></span>|<span data-ttu-id="5b9d5-143">DateTime</span><span class="sxs-lookup"><span data-stu-id="5b9d5-143">DateTime</span></span>|<span data-ttu-id="5b9d5-144">Heure de début du redimensionnement du pool.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-144">The time the pool resize started.</span></span>|
|<span data-ttu-id="5b9d5-145">endTime</span><span class="sxs-lookup"><span data-stu-id="5b9d5-145">endTime</span></span>|<span data-ttu-id="5b9d5-146">DateTime</span><span class="sxs-lookup"><span data-stu-id="5b9d5-146">DateTime</span></span>|<span data-ttu-id="5b9d5-147">Heure de fin du redimensionnement du pool.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-147">The time the pool resize completed.</span></span>|
|<span data-ttu-id="5b9d5-148">resultCode</span><span class="sxs-lookup"><span data-stu-id="5b9d5-148">resultCode</span></span>|<span data-ttu-id="5b9d5-149">String</span><span class="sxs-lookup"><span data-stu-id="5b9d5-149">String</span></span>|<span data-ttu-id="5b9d5-150">Résultat du redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-150">The result of the resize.</span></span>|
|<span data-ttu-id="5b9d5-151">resultMessage</span><span class="sxs-lookup"><span data-stu-id="5b9d5-151">resultMessage</span></span>|<span data-ttu-id="5b9d5-152">Chaîne</span><span class="sxs-lookup"><span data-stu-id="5b9d5-152">String</span></span>|<span data-ttu-id="5b9d5-153">L’erreur de redimensionnement inclut les détails du résultat.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-153">The resize error includes the details of the result.</span></span><br /><br /> <span data-ttu-id="5b9d5-154">Si le redimensionnement s’est terminé correctement, indique que l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="5b9d5-154">If the resize completed successfully it states that the operation succeeded.</span></span>|