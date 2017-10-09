---
title: "tâches parallèle toouse aaaRun ressources de calcul Azure Batch efficacement - | Documents Microsoft"
description: "Améliorer l’efficacité et réduire les coûts en utilisant moins de nœuds de calcul et en exécutant des tâches simultanées sur chaque nœud dans un pool Azure Batch"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="ef7b6-103">Exécuter des tâches simultanément l’utilisation de toomaximize lot de nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="ef7b6-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="ef7b6-104">En exécutant plusieurs tâches simultanément sur chaque nœud de calcul dans le pool de traitement par lots Azure, vous pouvez optimiser l’utilisation des ressources sur un plus petit nombre de nœuds dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="ef7b6-105">Pour certaines charges de travail, vous obtiendrez ainsi des durées de travail réduites et un coût inférieur.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="ef7b6-106">Alors que certains scénarios de tirer parti de dédier la totalité de la seule tâche d’un nœud ressources tooa, plusieurs situations bénéficient de ce qui permet à plusieurs tâches tooshare ces ressources :</span><span class="sxs-lookup"><span data-stu-id="ef7b6-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="ef7b6-107">**Réduire le transfert de données** lorsque les tâches sont en mesure de tooshare données.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="ef7b6-108">Dans ce scénario, vous pouvez réduire les frais de transfert de données en copiant les données partagées tooa plus petit nombre de nœuds et de l’exécution de tâches en parallèle sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="ef7b6-109">Cela s’applique en particulier si le nœud de hello données toobe tooeach copiées doit être transféré entre les régions géographiques.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="ef7b6-110">**Optimisation de l’utilisation de la mémoire** lorsque les tâches nécessitent une grande quantité de mémoire, mais seulement pendant de courtes périodes et à des moments variables au cours de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="ef7b6-111">Vous pouvez employer moins, mais la plus grande, de calcul des nœuds avec tooefficiently de mémoire plus gérer ces pics.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="ef7b6-112">Ces nœuds devrait avoir plusieurs tâches en cours d’exécution en parallèle sur chaque nœud, mais chaque tâche bénéficie de mémoire abondante de nœuds hello à des moments différents.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="ef7b6-113">**Atténuation des limites au nombre de nœuds** lorsque la communication entre les nœuds est requise au sein d’un pool.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="ef7b6-114">Actuellement, les pools configurés pour la communication entre les nœuds sont des nœuds de calcul too50 limité.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="ef7b6-115">Si chaque nœud dans un pool de ce type est en mesure de tooexecute les tâches en parallèle, un plus grand nombre de tâches pouvant être exécuté simultanément.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="ef7b6-116">**Réplication d’un cluster de calcul local**, par exemple lorsque vous commencez par déplacer un tooAzure d’environnement de calcul.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="ef7b6-117">Si votre solution sur site en cours s’exécute plusieurs tâches par nœud de calcul, vous pouvez augmenter le nombre maximal de hello des tâches de nœuds toomore reflètent précisément que la configuration.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="ef7b6-118">Exemple de scénario</span><span class="sxs-lookup"><span data-stu-id="ef7b6-118">Example scenario</span></span>
<span data-ttu-id="ef7b6-119">Comme un tooillustrate exemple hello les avantages de l’exécution de tâches parallèles, supposons que votre application de la tâche a processeur et de mémoire que [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nœuds sont suffisantes.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="ef7b6-120">Toutefois, dans le travail de hello ordre toofinish dans le temps de hello requis, 1 000 de ces nœuds sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="ef7b6-121">Au lieu d’utiliser les nœuds Standard\_D1 avec 1 cœur de processeur, vous pouvez utiliser des nœuds [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) avec 16 cœurs chacun, et activer l’exécution de tâches parallèles.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="ef7b6-122">Vous pouvez donc utiliser *16 fois moins de nœuds* : à la place des 1 000 nœuds, seuls 63 sont requis.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="ef7b6-123">En outre, si les fichiers d’application de grande taille ou des données de référence sont requises pour chaque nœud, l’efficacité et la durée du travail sont à nouveau améliorées hello les données étant copiées tooonly 16 nœuds.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="ef7b6-124">Activer l’exécution des tâches parallèles</span><span class="sxs-lookup"><span data-stu-id="ef7b6-124">Enable parallel task execution</span></span>
<span data-ttu-id="ef7b6-125">Vous configurez les nœuds de calcul pour l’exécution de la tâche parallèle au niveau du pool hello.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="ef7b6-126">Avec la bibliothèque de lot .NET hello, définissez hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propriété lorsque vous créez un pool.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="ef7b6-127">Si vous utilisez l’API REST de traitement par lots de hello, définissez hello [maxTasksPerNode] [ rest_addpool] élément dans le corps de la demande hello lors de la création du pool.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="ef7b6-128">Traitement par lots Azure vous permet de tooset nombre maximum de tâches par nœud de toofour fois (x 4) hello nombre de cœurs de nœud.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="ef7b6-129">Par exemple, si hello pool est configuré avec les nœuds de taille « Grande » (quatre cœurs), puis `maxTasksPerNode` peut avoir la valeur too16.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="ef7b6-130">Pour plus d’informations sur le nombre hello de cœurs pour chacun des tailles de nœud hello, consultez [tailles pour les Services de Cloud](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="ef7b6-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="ef7b6-131">Pour plus d’informations sur les limites de service, consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="ef7b6-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="ef7b6-132">Être vraiment tootake dans hello du compte `maxTasksPerNode` valeur lorsque vous construisez une [formule de mise à l’échelle] [ enable_autoscaling] pour votre pool.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="ef7b6-133">Par exemple, une formule qui évalue `$RunningTasks` pourrait être considérablement affectée par une augmentation des tâches par nœud.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="ef7b6-134">Consultez [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](batch-automatic-scaling.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="ef7b6-135">Répartition des tâches</span><span class="sxs-lookup"><span data-stu-id="ef7b6-135">Distribution of tasks</span></span>
<span data-ttu-id="ef7b6-136">Lorsque les nœuds de calcul hello dans un pool peuvent exécuter des tâches simultanément, il est important toospecify comment vous souhaitez que toobe de tâches hello répartis entre les nœuds hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="ef7b6-137">À l’aide de hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] propriété, vous pouvez spécifier que les tâches doivent être assignées uniformément entre tous les nœuds dans le pool hello (« propagation »).</span><span class="sxs-lookup"><span data-stu-id="ef7b6-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="ef7b6-138">Ou vous pouvez spécifier que les tâches autant que possible doivent être assignées tooeach nœud avant que les tâches sont assignées nœud tooanother pool hello (« compression »).</span><span class="sxs-lookup"><span data-stu-id="ef7b6-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="ef7b6-139">Prenons un exemple de comment cette fonctionnalité est utile, pool hello de [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nœuds (dans l’exemple hello ci-dessus) qui est configuré avec un [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] valeur 16.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="ef7b6-140">Si hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] est configuré avec un [ComputeNodeFillType] [ fill_type] de *Pack*, il optimiser l’utilisation de toutes les 16 noyaux de chaque nœud et autoriser une [échelle pool](batch-automatic-scaling.md) tooprune les nœuds inutilisés de pool de hello (nœuds sans toutes les tâches affectées).</span><span class="sxs-lookup"><span data-stu-id="ef7b6-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="ef7b6-141">Ceci limite l'utilisation des ressources et permet d'économiser de l'argent.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="ef7b6-142">Exemple .NET Batch</span><span class="sxs-lookup"><span data-stu-id="ef7b6-142">Batch .NET example</span></span>
<span data-ttu-id="ef7b6-143">Cela [Batch .NET] [ api_net] API de code montre une toocreate demande un pool qui contient les quatre nœuds de grande taille avec un maximum de quatre tâches par nœud.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="ef7b6-144">Elle spécifie une stratégie qui remplit chaque nœud tâches antérieures tooassigning tâches tooanother nœud du pool de hello de planification des tâches.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="ef7b6-145">Pour plus d’informations sur l’ajout de pools à l’aide de hello API .NET de traitement par lots, consultez [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="ef7b6-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a><span data-ttu-id="ef7b6-146">Exemple REST Batch</span><span class="sxs-lookup"><span data-stu-id="ef7b6-146">Batch REST example</span></span>
<span data-ttu-id="ef7b6-147">Cela [lot reste] [ api_rest] API montre un toocreate demande un pool qui contient deux nœuds de grande taille avec un maximum de quatre tâches par nœud.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="ef7b6-148">Pour plus d’informations sur l’ajout de pools à l’aide de hello API REST, consultez [ajouter un compte du pool de tooan][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="ef7b6-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> <span data-ttu-id="ef7b6-149">Vous pouvez définir hello `maxTasksPerNode` élément et [MaxTasksPerComputeNode] [ maxtasks_net] propriété uniquement au moment de la création du pool.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="ef7b6-150">Ils ne peuvent pas être modifiés après qu'un pool a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="ef7b6-151">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="ef7b6-151">Code sample</span></span>
<span data-ttu-id="ef7b6-152">Hello [ParallelNodeTasks] [ parallel_tasks_sample] projet sur GitHub illustre l’utilisation de hello de hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propriété.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="ef7b6-153">Cette application de console c# utilise hello [Batch .NET] [ api_net] toocreate de bibliothèque un pool avec un ou plusieurs nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="ef7b6-154">Il exécute un nombre configurable de tâches sur ces nœuds toosimulate la charge variable.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="ef7b6-155">Sortie de l’application hello spécifie les nœuds exécuté chaque tâche.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="ef7b6-156">application Hello fournit également un résumé des paramètres de la tâche hello et la durée.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="ef7b6-157">partie de résumé Hello de sortie hello de deux exécutions différentes de l’application d’exemple hello s’affiche ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="ef7b6-158">première exécution de Hello de l’exemple d’application hello montre que, avec un nœud unique dans le pool de hello et paramètre hello par défaut est une tâche par nœud, la durée du travail hello est plus de 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="ef7b6-159">Hello deuxième exécution de l’exemple hello montre une diminution considérable de la durée du travail.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="ef7b6-160">Il s’agit, car le pool de hello a été configurée avec quatre tâches par nœud, ce qui permet de travail de tâche parallèle d’exécution toocomplete hello dans près d’un quart de temps de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="ef7b6-161">durées de travail Hello dans des résumés d’hello ci-dessus n’incluent pas l’heure de création du pool.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="ef7b6-162">Chacune des tâches hello ci-dessus a été soumis toopreviously créé les pools dont les nœuds de calcul ont été Bonjour *inactif* état au moment de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ef7b6-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef7b6-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="ef7b6-164">Carte thermique Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="ef7b6-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="ef7b6-165">Hello [Azure Batch Explorer][batch_explorer], un des hello Azure Batch [exemples d’applications][github_samples], contient un *cartethermique* fonctionnalité qui fournit la visualisation de l’exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="ef7b6-166">Lorsque vous avez exécuté l’hello [ParallelTasks] [ parallel_tasks_sample] exemple d’application, vous pouvez utiliser hello thermique fonctionnalité tooeasily visualiser l’exécution de hello de tâches en parallèle sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="ef7b6-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Carte thermique Batch Explorer][1]

<span data-ttu-id="ef7b6-168">*Carte thermique Batch Explorer affichant un pool de quatre nœuds, chaque nœud exécutant quatre tâches*</span><span class="sxs-lookup"><span data-stu-id="ef7b6-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
