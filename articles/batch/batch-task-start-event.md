---
title: "Événement de début de tâche Azure Batch | Microsoft Docs"
description: "Référence pour l’événement de début de tâche Batch."
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="eef65-103">Événement de début de tâche</span><span class="sxs-lookup"><span data-stu-id="eef65-103">Task start event</span></span>

 <span data-ttu-id="eef65-104">Cet événement est émis quand une tâche est planifiée pour démarrer sur un nœud de calcul par le Scheduler.</span><span class="sxs-lookup"><span data-stu-id="eef65-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="eef65-105">Notez que, si la tâche est retentée ou replacée en file d’attente, cet événement est ré-émis pour la même tâche, mais que le nombre de nouvelles tentatives et la version de la tâche système sont mis à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="eef65-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="eef65-106">L’exemple suivant montre le corps d’un événement de début de tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-106">The following example shows the body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="eef65-107">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="eef65-107">Element name</span></span>|<span data-ttu-id="eef65-108">Type</span><span class="sxs-lookup"><span data-stu-id="eef65-108">Type</span></span>|<span data-ttu-id="eef65-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="eef65-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="eef65-110">jobId</span><span class="sxs-lookup"><span data-stu-id="eef65-110">jobId</span></span>|<span data-ttu-id="eef65-111">String</span><span class="sxs-lookup"><span data-stu-id="eef65-111">String</span></span>|<span data-ttu-id="eef65-112">ID du travail contenant la tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="eef65-113">id</span><span class="sxs-lookup"><span data-stu-id="eef65-113">id</span></span>|<span data-ttu-id="eef65-114">String</span><span class="sxs-lookup"><span data-stu-id="eef65-114">String</span></span>|<span data-ttu-id="eef65-115">ID de la tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-115">The id of the task.</span></span>|
|<span data-ttu-id="eef65-116">taskType</span><span class="sxs-lookup"><span data-stu-id="eef65-116">taskType</span></span>|<span data-ttu-id="eef65-117">String</span><span class="sxs-lookup"><span data-stu-id="eef65-117">String</span></span>|<span data-ttu-id="eef65-118">Type de la tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-118">The type of the task.</span></span> <span data-ttu-id="eef65-119">Ce peut être « JobManager », indiquant qu’il s’agit une tâche du gestionnaire, ou « User », indiquant qu’il ne s’agit pas d’une tâche du gestionnaire.</span><span class="sxs-lookup"><span data-stu-id="eef65-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="eef65-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="eef65-120">systemTaskVersion</span></span>|<span data-ttu-id="eef65-121">Int32</span><span class="sxs-lookup"><span data-stu-id="eef65-121">Int32</span></span>|<span data-ttu-id="eef65-122">Compteur de tentatives internes d’exécution d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="eef65-123">En interne, le service Batch peut recommencer une tâche pour prendre en compte des problèmes temporaires.</span><span class="sxs-lookup"><span data-stu-id="eef65-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="eef65-124">Ces problèmes peuvent être des erreurs de planification internes ou des tentatives de récupération à partir de nœuds de calcul en mauvais état.</span><span class="sxs-lookup"><span data-stu-id="eef65-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="eef65-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="eef65-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="eef65-126">Type complexe</span><span class="sxs-lookup"><span data-stu-id="eef65-126">Complex Type</span></span>|<span data-ttu-id="eef65-127">Contient des informations sur le nœud de calcul sur lequel la tâche a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="eef65-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="eef65-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="eef65-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="eef65-129">Type complexe</span><span class="sxs-lookup"><span data-stu-id="eef65-129">Complex Type</span></span>|<span data-ttu-id="eef65-130">Spécifie que la tâche est une tâche multi-instance nécessitant plusieurs nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="eef65-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="eef65-131">Pour plus d’informations, voir [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).</span><span class="sxs-lookup"><span data-stu-id="eef65-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="eef65-132">constraints</span><span class="sxs-lookup"><span data-stu-id="eef65-132">constraints</span></span>](#constraints)|<span data-ttu-id="eef65-133">Type complexe</span><span class="sxs-lookup"><span data-stu-id="eef65-133">Complex Type</span></span>|<span data-ttu-id="eef65-134">Contraintes d’exécution qui s’appliquent à cette tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="eef65-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="eef65-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="eef65-136">Type complexe</span><span class="sxs-lookup"><span data-stu-id="eef65-136">Complex Type</span></span>|<span data-ttu-id="eef65-137">Contient des informations sur l’exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="eef65-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="eef65-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="eef65-139">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="eef65-139">Element name</span></span>|<span data-ttu-id="eef65-140">Type</span><span class="sxs-lookup"><span data-stu-id="eef65-140">Type</span></span>|<span data-ttu-id="eef65-141">Remarques</span><span class="sxs-lookup"><span data-stu-id="eef65-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="eef65-142">poolId</span><span class="sxs-lookup"><span data-stu-id="eef65-142">poolId</span></span>|<span data-ttu-id="eef65-143">Chaîne</span><span class="sxs-lookup"><span data-stu-id="eef65-143">String</span></span>|<span data-ttu-id="eef65-144">ID u pool sur lequel la tâche a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="eef65-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="eef65-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="eef65-145">nodeId</span></span>|<span data-ttu-id="eef65-146">String</span><span class="sxs-lookup"><span data-stu-id="eef65-146">String</span></span>|<span data-ttu-id="eef65-147">ID du nœud sur lequel la tâche a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="eef65-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="eef65-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="eef65-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="eef65-149">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="eef65-149">Element name</span></span>|<span data-ttu-id="eef65-150">Type</span><span class="sxs-lookup"><span data-stu-id="eef65-150">Type</span></span>|<span data-ttu-id="eef65-151">Remarques</span><span class="sxs-lookup"><span data-stu-id="eef65-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="eef65-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="eef65-152">numberOfInstances</span></span>|<span data-ttu-id="eef65-153">int</span><span class="sxs-lookup"><span data-stu-id="eef65-153">Int</span></span>|<span data-ttu-id="eef65-154">Nombre de nœuds de calcul requis pour la tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="eef65-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="eef65-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="eef65-156">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="eef65-156">Element name</span></span>|<span data-ttu-id="eef65-157">Type</span><span class="sxs-lookup"><span data-stu-id="eef65-157">Type</span></span>|<span data-ttu-id="eef65-158">Remarques</span><span class="sxs-lookup"><span data-stu-id="eef65-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="eef65-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="eef65-159">maxTaskRetryCount</span></span>|<span data-ttu-id="eef65-160">Int32</span><span class="sxs-lookup"><span data-stu-id="eef65-160">Int32</span></span>|<span data-ttu-id="eef65-161">Nombre maximal de fois que la tâche peut être retentée.</span><span class="sxs-lookup"><span data-stu-id="eef65-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="eef65-162">Le service Batch retente une tâche si le code de sortie de celle-ci diffère de zéro.</span><span class="sxs-lookup"><span data-stu-id="eef65-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="eef65-163">Notez que cette valeur contrôle spécifiquement le nombre de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="eef65-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="eef65-164">Le service Batch tente la tâche une fois et peut réessayer jusqu’à cette limite.</span><span class="sxs-lookup"><span data-stu-id="eef65-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="eef65-165">Par exemple, si le nombre maximal de nouvelles tentatives est 3, le service Batch peut tenter d’exécuter la tâche jusqu’à 4 fois (tentative initiale + 3 tentatives supplémentaires).</span><span class="sxs-lookup"><span data-stu-id="eef65-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="eef65-166">Si le nombre maximal de tentatives est 0, le service Batch ne réessaye pas d’exécuter des tâches.</span><span class="sxs-lookup"><span data-stu-id="eef65-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="eef65-167">Si le nombre maximal de nouvelles tentatives est -1, le service Batch réessaie d’exécuter les tâches sans limite.</span><span class="sxs-lookup"><span data-stu-id="eef65-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="eef65-168">La valeur par défaut est 0 (aucune nouvelle tentative).</span><span class="sxs-lookup"><span data-stu-id="eef65-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="eef65-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="eef65-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="eef65-170">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="eef65-170">Element name</span></span>|<span data-ttu-id="eef65-171">Type</span><span class="sxs-lookup"><span data-stu-id="eef65-171">Type</span></span>|<span data-ttu-id="eef65-172">Remarques</span><span class="sxs-lookup"><span data-stu-id="eef65-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="eef65-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="eef65-173">retryCount</span></span>|<span data-ttu-id="eef65-174">Int32</span><span class="sxs-lookup"><span data-stu-id="eef65-174">Int32</span></span>|<span data-ttu-id="eef65-175">Nombre de fois que le service Batch a réessayé d’exécuter la tâche.</span><span class="sxs-lookup"><span data-stu-id="eef65-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="eef65-176">Si la tâche se termine avec un code de sortie autre que zéro, elle est retentée le nombre de fois spécifié par la valeur MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="eef65-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
