---
title: "AAA « événement de début de tâche de traitement par lots Azure | Documents Microsoft »"
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="36780-103">Événement de début de tâche</span><span class="sxs-lookup"><span data-stu-id="36780-103">Task start event</span></span>

 <span data-ttu-id="36780-104">Cet événement est émis une fois qu’une tâche a été planifiée toostart sur un nœud de calcul par le Planificateur de hello.</span><span class="sxs-lookup"><span data-stu-id="36780-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="36780-105">Notez que si la tâche hello est retentée ou remis cet événement sera émis à nouveau pour hello même tâche, mais hello nombre de tentatives et la version de la tâche sera mis à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="36780-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="36780-106">Hello suivant montre les corps hello d’un événement de début de tâche.</span><span class="sxs-lookup"><span data-stu-id="36780-106">hello following example shows hello body of a task start event.</span></span>

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

|<span data-ttu-id="36780-107">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="36780-107">Element name</span></span>|<span data-ttu-id="36780-108">Type</span><span class="sxs-lookup"><span data-stu-id="36780-108">Type</span></span>|<span data-ttu-id="36780-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="36780-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="36780-110">jobId</span><span class="sxs-lookup"><span data-stu-id="36780-110">jobId</span></span>|<span data-ttu-id="36780-111">String</span><span class="sxs-lookup"><span data-stu-id="36780-111">String</span></span>|<span data-ttu-id="36780-112">id de Hello du travail hello contenant la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="36780-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="36780-113">id</span><span class="sxs-lookup"><span data-stu-id="36780-113">id</span></span>|<span data-ttu-id="36780-114">String</span><span class="sxs-lookup"><span data-stu-id="36780-114">String</span></span>|<span data-ttu-id="36780-115">id de Hello de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="36780-115">hello id of hello task.</span></span>|
|<span data-ttu-id="36780-116">taskType</span><span class="sxs-lookup"><span data-stu-id="36780-116">taskType</span></span>|<span data-ttu-id="36780-117">String</span><span class="sxs-lookup"><span data-stu-id="36780-117">String</span></span>|<span data-ttu-id="36780-118">type de Hello de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="36780-118">hello type of hello task.</span></span> <span data-ttu-id="36780-119">Ce peut être « JobManager », indiquant qu’il s’agit une tâche du gestionnaire, ou « User », indiquant qu’il ne s’agit pas d’une tâche du gestionnaire.</span><span class="sxs-lookup"><span data-stu-id="36780-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="36780-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="36780-120">systemTaskVersion</span></span>|<span data-ttu-id="36780-121">Int32</span><span class="sxs-lookup"><span data-stu-id="36780-121">Int32</span></span>|<span data-ttu-id="36780-122">Il s’agit de compteur de nouvelles tentatives internes hello sur une tâche.</span><span class="sxs-lookup"><span data-stu-id="36780-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="36780-123">En interne, service de traitement par lots hello peut réessayer un tooaccount de tâche pour les problèmes temporaires.</span><span class="sxs-lookup"><span data-stu-id="36780-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="36780-124">Ces problèmes peuvent inclure interne toorecover erreurs ou des tentatives de planification à partir des nœuds de calcul dans un état incorrect.</span><span class="sxs-lookup"><span data-stu-id="36780-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="36780-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="36780-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="36780-126">Type complexe</span><span class="sxs-lookup"><span data-stu-id="36780-126">Complex Type</span></span>|<span data-ttu-id="36780-127">Contient des informations sur le nœud de calcul hello sur quel hello tâche s’est exécutée.</span><span class="sxs-lookup"><span data-stu-id="36780-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="36780-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="36780-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="36780-129">Type complexe</span><span class="sxs-lookup"><span data-stu-id="36780-129">Complex Type</span></span>|<span data-ttu-id="36780-130">Spécifie que cette tâche hello est multi-instance nécessitant plusieurs nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="36780-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="36780-131">Pour plus d’informations, voir [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).</span><span class="sxs-lookup"><span data-stu-id="36780-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="36780-132">constraints</span><span class="sxs-lookup"><span data-stu-id="36780-132">constraints</span></span>](#constraints)|<span data-ttu-id="36780-133">Type complexe</span><span class="sxs-lookup"><span data-stu-id="36780-133">Complex Type</span></span>|<span data-ttu-id="36780-134">contraintes de l’exécution de Hello qui s’appliquent toothis tâche.</span><span class="sxs-lookup"><span data-stu-id="36780-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="36780-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="36780-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="36780-136">Type complexe</span><span class="sxs-lookup"><span data-stu-id="36780-136">Complex Type</span></span>|<span data-ttu-id="36780-137">Contient des informations sur l’exécution de hello de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="36780-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="36780-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="36780-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="36780-139">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="36780-139">Element name</span></span>|<span data-ttu-id="36780-140">Type</span><span class="sxs-lookup"><span data-stu-id="36780-140">Type</span></span>|<span data-ttu-id="36780-141">Remarques</span><span class="sxs-lookup"><span data-stu-id="36780-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="36780-142">poolId</span><span class="sxs-lookup"><span data-stu-id="36780-142">poolId</span></span>|<span data-ttu-id="36780-143">String</span><span class="sxs-lookup"><span data-stu-id="36780-143">String</span></span>|<span data-ttu-id="36780-144">id de Hello de pool hello sur quel hello tâche s’est exécutée.</span><span class="sxs-lookup"><span data-stu-id="36780-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="36780-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="36780-145">nodeId</span></span>|<span data-ttu-id="36780-146">String</span><span class="sxs-lookup"><span data-stu-id="36780-146">String</span></span>|<span data-ttu-id="36780-147">Hello l’id du nœud hello sur quel hello tâche s’est exécutée.</span><span class="sxs-lookup"><span data-stu-id="36780-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="36780-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="36780-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="36780-149">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="36780-149">Element name</span></span>|<span data-ttu-id="36780-150">Type</span><span class="sxs-lookup"><span data-stu-id="36780-150">Type</span></span>|<span data-ttu-id="36780-151">Remarques</span><span class="sxs-lookup"><span data-stu-id="36780-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="36780-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="36780-152">numberOfInstances</span></span>|<span data-ttu-id="36780-153">Int</span><span class="sxs-lookup"><span data-stu-id="36780-153">Int</span></span>|<span data-ttu-id="36780-154">nombre de Hello de nœuds de calcul requis par la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="36780-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="36780-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="36780-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="36780-156">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="36780-156">Element name</span></span>|<span data-ttu-id="36780-157">Type</span><span class="sxs-lookup"><span data-stu-id="36780-157">Type</span></span>|<span data-ttu-id="36780-158">Remarques</span><span class="sxs-lookup"><span data-stu-id="36780-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="36780-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="36780-159">maxTaskRetryCount</span></span>|<span data-ttu-id="36780-160">Int32</span><span class="sxs-lookup"><span data-stu-id="36780-160">Int32</span></span>|<span data-ttu-id="36780-161">Bonjour le nombre maximal de tentatives de tâche hello peut être.</span><span class="sxs-lookup"><span data-stu-id="36780-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="36780-162">Hello service Batch tente de renvoyer une tâche si son code de sortie est différent de zéro.</span><span class="sxs-lookup"><span data-stu-id="36780-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="36780-163">Notez que cette valeur contrôle spécifiquement nombre hello de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="36780-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="36780-164">service de traitement par lots Hello va tenter de tâche hello qu’une seule fois et peut être relancé puis des toothis limite.</span><span class="sxs-lookup"><span data-stu-id="36780-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="36780-165">Par exemple, si le nombre maximal de tentatives de hello est 3, lot tente une tâche too4 fois (une fois initiale et 3 tentatives).</span><span class="sxs-lookup"><span data-stu-id="36780-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="36780-166">Si le nombre maximal de tentatives de hello est 0, hello service Batch ne réessaie pas de tâches.</span><span class="sxs-lookup"><span data-stu-id="36780-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="36780-167">Si le nombre maximal de tentatives de hello est -1, service de traitement par lots hello réessaie tâches sans limite.</span><span class="sxs-lookup"><span data-stu-id="36780-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="36780-168">Hello par défaut est 0 (aucune nouvelle tentative).</span><span class="sxs-lookup"><span data-stu-id="36780-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="36780-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="36780-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="36780-170">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="36780-170">Element name</span></span>|<span data-ttu-id="36780-171">Type</span><span class="sxs-lookup"><span data-stu-id="36780-171">Type</span></span>|<span data-ttu-id="36780-172">Remarques</span><span class="sxs-lookup"><span data-stu-id="36780-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="36780-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="36780-173">retryCount</span></span>|<span data-ttu-id="36780-174">Int32</span><span class="sxs-lookup"><span data-stu-id="36780-174">Int32</span></span>|<span data-ttu-id="36780-175">Bonjour le nombre de tentatives de tâche hello par le service de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="36780-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="36780-176">tâche Hello est retentée si elle se termine avec un code de sortie différent de zéro, les toohello spécifié MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="36780-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
