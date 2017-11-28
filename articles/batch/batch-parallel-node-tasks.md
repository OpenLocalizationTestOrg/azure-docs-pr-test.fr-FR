---
title: "Exécuter des tâches en parallèle pour utiliser les ressources de calcul de manière efficace - Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="96bbb-103">Exécuter des tâches simultanément pour optimiser l’utilisation des nœuds de calcul Batch</span><span class="sxs-lookup"><span data-stu-id="96bbb-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="96bbb-104">En exécutant simultanément plusieurs tâches sur chaque nœud de calcul dans votre pool Azure Batch, vous pouvez optimiser l’utilisation des ressources sur un plus petit nombre de nœuds du pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="96bbb-105">Pour certaines charges de travail, vous obtiendrez ainsi des durées de travail réduites et un coût inférieur.</span><span class="sxs-lookup"><span data-stu-id="96bbb-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="96bbb-106">Alors que certains scénarios tirent parti du fait de dédier toutes les ressources d’un nœud disponibles à une seule tâche, certaines situations profitent de l’autorisation accordée à plusieurs tâches de partager ces ressources :</span><span class="sxs-lookup"><span data-stu-id="96bbb-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="96bbb-107">**Réduction du transfert de données** lorsque les tâches sont en mesure de partager des données.</span><span class="sxs-lookup"><span data-stu-id="96bbb-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="96bbb-108">Dans ce scénario, vous pouvez considérablement réduire les frais de transfert de données en copiant les données partagées vers un plus petit nombre de nœuds et en exécutant les tâches en parallèle sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="96bbb-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="96bbb-109">Cela s'applique surtout si les données à copier sur chaque nœud doivent être transférées entre des régions géographiques.</span><span class="sxs-lookup"><span data-stu-id="96bbb-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="96bbb-110">**Optimisation de l’utilisation de la mémoire** lorsque les tâches nécessitent une grande quantité de mémoire, mais seulement pendant de courtes périodes et à des moments variables au cours de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="96bbb-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="96bbb-111">Vous pouvez employer des nœuds de calcul moins nombreux mais de plus grande taille, avec plus de mémoire pour gérer efficacement ces pics.</span><span class="sxs-lookup"><span data-stu-id="96bbb-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="96bbb-112">De cette façon, ces nœuds ont plusieurs tâches exécutées en parallèle sur chaque nœud, mais chaque tâche bénéficie de la mémoire abondante des nœuds à des moments différents.</span><span class="sxs-lookup"><span data-stu-id="96bbb-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="96bbb-113">**Atténuation des limites au nombre de nœuds** lorsque la communication entre les nœuds est requise au sein d’un pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="96bbb-114">Actuellement, les pools configurés pour la communication entre les nœuds sont limités à 50 nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="96bbb-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="96bbb-115">Si chaque nœud dans un pool de ce type est capable d’exécuter des tâches en parallèle, un plus grand nombre de tâches peuvent être exécutées simultanément.</span><span class="sxs-lookup"><span data-stu-id="96bbb-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="96bbb-116">**Réplication d'un cluster de calcul local**, comme lorsque vous déplacez un environnement de calcul vers Azure pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="96bbb-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="96bbb-117">Si cette configuration exécute actuellement plusieurs tâches par nœud de calcul, vous pouvez augmenter le nombre maximal de tâches de nœud pour refléter plus précisément cette configuration.</span><span class="sxs-lookup"><span data-stu-id="96bbb-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="96bbb-118">Exemple de scénario</span><span class="sxs-lookup"><span data-stu-id="96bbb-118">Example scenario</span></span>
<span data-ttu-id="96bbb-119">Comme exemple d’illustration des avantages de l’exécution de tâches parallèles, supposons que votre application de tâche soit dotée de critères de processeur et de mémoire tels que des nœuds [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) sont suffisants.</span><span class="sxs-lookup"><span data-stu-id="96bbb-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="96bbb-120">Cependant, pour terminer le travail dans le délai imparti, 1 000 nœuds de ce type sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="96bbb-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="96bbb-121">Au lieu d’utiliser les nœuds Standard\_D1 avec 1 cœur de processeur, vous pouvez utiliser des nœuds [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) avec 16 cœurs chacun, et activer l’exécution de tâches parallèles.</span><span class="sxs-lookup"><span data-stu-id="96bbb-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="96bbb-122">Vous pouvez donc utiliser *16 fois moins de nœuds* : à la place des 1 000 nœuds, seuls 63 sont requis.</span><span class="sxs-lookup"><span data-stu-id="96bbb-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="96bbb-123">En outre, si des fichiers d’application volumineux ou des données de référence sont requis pour chaque nœud, l’efficacité et la durée du travail sont encore améliorées, car les données ne sont copiées que sur 16 nœuds.</span><span class="sxs-lookup"><span data-stu-id="96bbb-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="96bbb-124">Activer l’exécution des tâches parallèles</span><span class="sxs-lookup"><span data-stu-id="96bbb-124">Enable parallel task execution</span></span>
<span data-ttu-id="96bbb-125">Vous configurez les nœuds de calcul pour l’exécution des tâches parallèles au niveau du pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="96bbb-126">Avec la bibliothèque Batch .NET, définissez la propriété [CloudPool.MaxTasksPerComputeNode][maxtasks_net] lorsque vous créez un pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="96bbb-127">Si vous utilisez l’API REST Batch, définissez l’élément [maxTasksPerNode][rest_addpool] dans le corps de la requête lors de la création du pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="96bbb-128">Azure Batch vous permet de définir un nombre maximum de tâches par nœud allant jusqu'à quatre fois (4x) le nombre de cœurs de nœud.</span><span class="sxs-lookup"><span data-stu-id="96bbb-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="96bbb-129">Par exemple, si le pool est configuré avec des nœuds de grande taille (quatre cœurs), alors la valeur `maxTasksPerNode` peut être définie sur 16.</span><span class="sxs-lookup"><span data-stu-id="96bbb-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="96bbb-130">Pour plus d’informations sur le nombre de cœurs pour chacune des tailles de nœud, consultez [Tailles de services Cloud](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="96bbb-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="96bbb-131">Pour plus d’informations sur les limites du service, consultez [Quotas et les limites pour le service Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="96bbb-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="96bbb-132">Veillez à prendre en compte la valeur `maxTasksPerNode` lors de la construction d’une [formule de mise à l’échelle automatique][enable_autoscaling] pour votre pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="96bbb-133">Par exemple, une formule qui évalue `$RunningTasks` pourrait être considérablement affectée par une augmentation des tâches par nœud.</span><span class="sxs-lookup"><span data-stu-id="96bbb-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="96bbb-134">Consultez [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](batch-automatic-scaling.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="96bbb-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="96bbb-135">Répartition des tâches</span><span class="sxs-lookup"><span data-stu-id="96bbb-135">Distribution of tasks</span></span>
<span data-ttu-id="96bbb-136">Lorsque les nœuds de calcul d’un pool peuvent exécuter des tâches simultanément, il est important de spécifier comment vous souhaitez que les tâches soient réparties entre les nœuds du pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="96bbb-137">La propriété [CloudPool.TaskSchedulingPolicy][task_schedule] vous permet de spécifier que les tâches doivent être affectées uniformément entre tous les nœuds du pool (« propagation »).</span><span class="sxs-lookup"><span data-stu-id="96bbb-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="96bbb-138">Vous pouvez également spécifier qu'autant de tâches que possible doivent être attribuées à chaque nœud avant que les tâches ne soient attribuées à un autre nœud du pool (« compression »).</span><span class="sxs-lookup"><span data-stu-id="96bbb-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="96bbb-139">Pour illustrer l’importance de cette fonctionnalité, examinons le pool de nœuds [Standard_Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) (dans l’exemple ci-dessus) configuré avec une propriété [CloudPool.MaxTasksPerComputeNode][maxtasks_net] d’une valeur de 16.</span><span class="sxs-lookup"><span data-stu-id="96bbb-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="96bbb-140">Si la propriété [CloudPool.TaskSchedulingPolicy][task_schedule] est configurée avec une propriété [ComputeNodeFillType][fill_type] de type *Pack*, l’utilisation des 16 cœurs de chaque nœud est optimisée et un [pool de mise à l’échelle automatique](batch-automatic-scaling.md) est autorisé pour nettoyer les nœuds inutilisés du pool (nœuds sans aucune tâche affectée).</span><span class="sxs-lookup"><span data-stu-id="96bbb-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="96bbb-141">Ceci limite l'utilisation des ressources et permet d'économiser de l'argent.</span><span class="sxs-lookup"><span data-stu-id="96bbb-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="96bbb-142">Exemple .NET Batch</span><span class="sxs-lookup"><span data-stu-id="96bbb-142">Batch .NET example</span></span>
<span data-ttu-id="96bbb-143">Cet extrait de code de l’API [Batch .NET][api_net] illustre une demande de création d’un pool contenant quatre grands nœuds avec un maximum de quatre tâches par nœud.</span><span class="sxs-lookup"><span data-stu-id="96bbb-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="96bbb-144">Une stratégie de planification de tâche est également spécifiée ; elle remplira chaque nœud de tâches avant d'attribuer des tâches à un autre nœud du pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="96bbb-145">Pour plus d’informations sur l’ajout de pools à l’aide de l’API Batch .NET, consultez [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="96bbb-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="96bbb-146">Exemple REST Batch</span><span class="sxs-lookup"><span data-stu-id="96bbb-146">Batch REST example</span></span>
<span data-ttu-id="96bbb-147">Cet extrait de code de l’API [REST Batch][api_rest] illustre une demande de création d’un pool contenant deux grands nœuds avec un maximum de quatre tâches par nœud.</span><span class="sxs-lookup"><span data-stu-id="96bbb-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="96bbb-148">Pour plus d’informations sur l’ajout de pools à l’aide de l’API REST, consultez la page [Ajout d’un pool à un compte][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="96bbb-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

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
> <span data-ttu-id="96bbb-149">Vous ne pouvez définir l’élément `maxTasksPerNode` et la propriété [MaxTasksPerComputeNode][maxtasks_net] qu’au moment de la création du pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="96bbb-150">Ils ne peuvent pas être modifiés après qu'un pool a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="96bbb-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="96bbb-151">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="96bbb-151">Code sample</span></span>
<span data-ttu-id="96bbb-152">Le projet [ParallelNodeTasks][parallel_tasks_sample] sur GitHub illustre l’utilisation de la propriété [CloudPool.MaxTasksPerComputeNode][maxtasks_net].</span><span class="sxs-lookup"><span data-stu-id="96bbb-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="96bbb-153">Cette application de console en C# utilise la bibliothèque [Batch .NET][api_net] pour créer un pool avec un ou plusieurs nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="96bbb-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="96bbb-154">Elle exécute un nombre configurable de tâches sur ces nœuds pour simuler la charge variable.</span><span class="sxs-lookup"><span data-stu-id="96bbb-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="96bbb-155">La sortie de l'application spécifie quels nœuds ont exécuté chaque tâche.</span><span class="sxs-lookup"><span data-stu-id="96bbb-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="96bbb-156">L'application fournit également un résumé des paramètres du travail et sa durée.</span><span class="sxs-lookup"><span data-stu-id="96bbb-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="96bbb-157">La partie Résumé de la sortie de deux exécutions différentes de l’exemple d’application apparaît ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="96bbb-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="96bbb-158">La première exécution de l'exemple d'application montre qu'avec un nœud unique dans le pool et le paramètre par défaut d'une tâche par nœud, la durée du travail dépasse 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="96bbb-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="96bbb-159">La deuxième exécution de l'exemple montre une diminution significative de la durée du travail.</span><span class="sxs-lookup"><span data-stu-id="96bbb-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="96bbb-160">Cela est dû au fait que le pool a été configuré avec quatre tâches par nœud, ce qui permet l'exécution de tâches parallèles pour terminer le travail en un quart du temps, environ.</span><span class="sxs-lookup"><span data-stu-id="96bbb-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="96bbb-161">Les durées des tâches dans les résumés ci-dessus n’incluent pas le temps de création du pool.</span><span class="sxs-lookup"><span data-stu-id="96bbb-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="96bbb-162">Chacune des tâches ci-dessus a été envoyée à des pools créés précédemment dont les nœuds de calcul étaient à l’état *Inactif* au moment de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="96bbb-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="96bbb-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="96bbb-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="96bbb-164">Carte thermique Batch Explorer</span><span class="sxs-lookup"><span data-stu-id="96bbb-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="96bbb-165">[Azure Batch Explorer][batch_explorer], l’un des [exemples d’applications][github_samples] Azure Batch, contient une fonctionnalité *Carte thermique* qui permet de visualiser l’exécution des tâches.</span><span class="sxs-lookup"><span data-stu-id="96bbb-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="96bbb-166">Lorsque vous exécutez l’exemple d’application [ParallelTasks][parallel_tasks_sample], utilisez la fonctionnalité Carte thermique pour visualiser l’exécution de tâches parallèles sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="96bbb-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Carte thermique Batch Explorer][1]

<span data-ttu-id="96bbb-168">*Carte thermique Batch Explorer affichant un pool de quatre nœuds, chaque nœud exécutant quatre tâches*</span><span class="sxs-lookup"><span data-stu-id="96bbb-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
