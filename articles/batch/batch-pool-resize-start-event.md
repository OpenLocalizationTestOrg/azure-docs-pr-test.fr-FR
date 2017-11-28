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
# <a name="pool-resize-start-event"></a><span data-ttu-id="21dca-103">Événement de début de redimensionnement de pool</span><span class="sxs-lookup"><span data-stu-id="21dca-103">Pool resize start event</span></span>

 <span data-ttu-id="21dca-104">Cet événement est émis quand un redimensionnement de pool a commencé.</span><span class="sxs-lookup"><span data-stu-id="21dca-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="21dca-105">Redimensionnement du pool hello étant un événement asynchrone, vous pouvez vous attendre un toobe complète des événements de redimensionnement de pool émis une fois l’opération de redimensionnement hello se termine.</span><span class="sxs-lookup"><span data-stu-id="21dca-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="21dca-106">redimensionne les Hello affiche hello corps d’un événement de début de redimensionnement de pool pour le redimensionnement d’un pool à partir des nœuds too2 0 d’une opération manuelle de l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="21dca-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="21dca-107">Élément</span><span class="sxs-lookup"><span data-stu-id="21dca-107">Element</span></span>|<span data-ttu-id="21dca-108">Type</span><span class="sxs-lookup"><span data-stu-id="21dca-108">Type</span></span>|<span data-ttu-id="21dca-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="21dca-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="21dca-110">poolId</span><span class="sxs-lookup"><span data-stu-id="21dca-110">poolId</span></span>|<span data-ttu-id="21dca-111">String</span><span class="sxs-lookup"><span data-stu-id="21dca-111">String</span></span>|<span data-ttu-id="21dca-112">id de Hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="21dca-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="21dca-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="21dca-113">nodeDeallocationOption</span></span>|<span data-ttu-id="21dca-114">String</span><span class="sxs-lookup"><span data-stu-id="21dca-114">String</span></span>|<span data-ttu-id="21dca-115">Spécifie quand les nœuds peuvent être supprimées de pool de hello, si la taille du pool hello baisse.</span><span class="sxs-lookup"><span data-stu-id="21dca-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="21dca-116">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="21dca-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="21dca-117">**requeue** : arrêter les tâches en cours d’exécution et les replacer en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="21dca-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="21dca-118">Hello tâches seront réexécutées quand le travail hello est activé.</span><span class="sxs-lookup"><span data-stu-id="21dca-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="21dca-119">Supprimez les nœuds dès que les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="21dca-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="21dca-120">**terminate** : mettre fin aux tâches en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="21dca-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="21dca-121">tâches de Hello ne s’exécutera pas à nouveau.</span><span class="sxs-lookup"><span data-stu-id="21dca-121">hello tasks will not run again.</span></span> <span data-ttu-id="21dca-122">Supprimez les nœuds dès que les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="21dca-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="21dca-123">**taskcompletion** – autoriser le toocomplete de tâches en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="21dca-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="21dca-124">Ne planifiez aucune nouvelle tâche en attendant.</span><span class="sxs-lookup"><span data-stu-id="21dca-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="21dca-125">Supprimer les nœuds quand toutes les tâches sont terminées.</span><span class="sxs-lookup"><span data-stu-id="21dca-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="21dca-126">**Retaineddata** : toocomplete de tâches en cours d’exécution, puis attendre que toutes les tâches tooexpire de périodes de rétention de données.</span><span class="sxs-lookup"><span data-stu-id="21dca-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="21dca-127">Ne planifiez aucune nouvelle tâche en attendant.</span><span class="sxs-lookup"><span data-stu-id="21dca-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="21dca-128">Supprimez les nœuds une fois que toutes les périodes de rétention ont expiré.</span><span class="sxs-lookup"><span data-stu-id="21dca-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="21dca-129">valeur par défaut de Hello est remettre.</span><span class="sxs-lookup"><span data-stu-id="21dca-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="21dca-130">Si l’augmentation de taille du pool de hello, hello a la valeur trop**non valide**.</span><span class="sxs-lookup"><span data-stu-id="21dca-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="21dca-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="21dca-131">currentDedicated</span></span>|<span data-ttu-id="21dca-132">Int32</span><span class="sxs-lookup"><span data-stu-id="21dca-132">Int32</span></span>|<span data-ttu-id="21dca-133">nombre de Hello de nœuds de calcul actuellement attribués toohello pool.</span><span class="sxs-lookup"><span data-stu-id="21dca-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="21dca-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="21dca-134">targetDedicated</span></span>|<span data-ttu-id="21dca-135">Int32</span><span class="sxs-lookup"><span data-stu-id="21dca-135">Int32</span></span>|<span data-ttu-id="21dca-136">nombre de Hello de nœuds de calcul qui sont demandées pour le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="21dca-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="21dca-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="21dca-137">enableAutoScale</span></span>|<span data-ttu-id="21dca-138">Bool</span><span class="sxs-lookup"><span data-stu-id="21dca-138">Bool</span></span>|<span data-ttu-id="21dca-139">Spécifie si taille du pool hello s’ajuste automatiquement au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="21dca-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="21dca-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="21dca-140">isAutoPool</span></span>|<span data-ttu-id="21dca-141">Bool</span><span class="sxs-lookup"><span data-stu-id="21dca-141">Bool</span></span>|<span data-ttu-id="21dca-142">Spécifie si le pool de hello a été créé via le mécanisme de pool automatique d’un travail.</span><span class="sxs-lookup"><span data-stu-id="21dca-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
