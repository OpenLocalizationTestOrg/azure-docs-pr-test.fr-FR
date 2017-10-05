---
title: "Utiliser des dépendances de tâches pour exécuter des tâches basées sur l’achèvement d’autres tâches - Azure Batch | Microsoft Docs"
description: "Créez des tâches qui dépendent de l’achèvement d’autres tâches pour le traitement de charges de travail de type MapReduce ou Big Data dans Azure Batch."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="6526c-103">Créer des dépendances de tâches pour exécuter des tâches qui dépendent d’autres tâches</span><span class="sxs-lookup"><span data-stu-id="6526c-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="6526c-104">Vous pouvez définir des dépendances de tâche pour exécuter une tâche ou un ensemble de tâches uniquement après la fin d’une tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="6526c-105">Voici quelques scénarios dont les dépendances de tâche sont utiles :</span><span class="sxs-lookup"><span data-stu-id="6526c-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="6526c-106">des charges de travail MapReduce dans le cloud ;</span><span class="sxs-lookup"><span data-stu-id="6526c-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="6526c-107">des travaux dont les tâches de traitement des données peuvent être exprimées sous la forme d’un graphe orienté acyclique (DAG) ;</span><span class="sxs-lookup"><span data-stu-id="6526c-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="6526c-108">Processus de pré-rendu et de post-rendu dans lesquels chaque tâche doit s’achever avant que la tâche suivante puisse commencer.</span><span class="sxs-lookup"><span data-stu-id="6526c-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="6526c-109">tout autre travail dont les tâches en aval dépendent de la sortie des tâches en amont.</span><span class="sxs-lookup"><span data-stu-id="6526c-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="6526c-110">Avec les dépendances de tâches Batch, vous pouvez créer des tâches dont l’exécution est planifiée sur des nœuds de calcul à condition qu’une ou plusieurs tâches parentes aient été exécutées.</span><span class="sxs-lookup"><span data-stu-id="6526c-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="6526c-111">Par exemple, vous pouvez créer un travail qui restitue chaque image d’un film 3D avec des tâches parallèles distinctes.</span><span class="sxs-lookup"><span data-stu-id="6526c-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="6526c-112">La dernière tâche (dite de fusion) fusionne les images restituées dans la vidéo complète uniquement après restitution de toutes les images.</span><span class="sxs-lookup"><span data-stu-id="6526c-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="6526c-113">Par défaut, les tâches dépendantes sont planifiées pour que leur exécution ait lieu uniquement après la fin de l’exécution de la tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="6526c-114">Vous pouvez indiquer une action de dépendance afin de remplacer le comportement par défaut et exécuter des tâches en cas d’échec de la tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="6526c-115">Pour plus d’informations, consultez la section [Actions de dépendance](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="6526c-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="6526c-116">Vous pouvez créer des tâches qui dépendent d’autres tâches dans une relation un-à-un ou un-à-plusieurs.</span><span class="sxs-lookup"><span data-stu-id="6526c-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="6526c-117">Vous pouvez également créer une dépendance de plage dans laquelle une tâche dépend de l’exécution d’un groupe de tâches au sein d’une plage spécifiée d’ID de tâches.</span><span class="sxs-lookup"><span data-stu-id="6526c-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="6526c-118">Vous pouvez combiner ces trois scénarios de base pour créer des relations plusieurs-à-plusieurs.</span><span class="sxs-lookup"><span data-stu-id="6526c-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="6526c-119">Dépendances de tâches avec Batch.NET</span><span class="sxs-lookup"><span data-stu-id="6526c-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="6526c-120">Cet article explique comment configurer les dépendances de tâches à l’aide de la bibliothèque [Batch .NET][net_msdn].</span><span class="sxs-lookup"><span data-stu-id="6526c-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="6526c-121">Nous allons tout d’abord vous montrer comment [activer la dépendance de tâches](#enable-task-dependencies) dans vos travaux, puis vous expliquer comment [configurer une tâche avec des dépendances](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="6526c-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="6526c-122">Nous décrivons également comment spécifier une action de dépendance pour exécuter des tâches dépendantes en cas d’échec de la tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="6526c-123">Pour finir, nous passerons en revue les [scénarios de dépendance](#dependency-scenarios) pris en charge par Batch.</span><span class="sxs-lookup"><span data-stu-id="6526c-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="6526c-124">Activation des dépendances de tâches</span><span class="sxs-lookup"><span data-stu-id="6526c-124">Enable task dependencies</span></span>
<span data-ttu-id="6526c-125">Pour utiliser les dépendances de tâches dans votre application Batch, vous devez d’abord configurer la tâche afin d’utiliser des dépendances de tâches.</span><span class="sxs-lookup"><span data-stu-id="6526c-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="6526c-126">Dans Batch.NET, activez la dépendance de tâches sur votre [CloudJob][net_cloudjob] en définissant sa propriété [UsesTaskDependencies][net_usestaskdependencies] sur `true` :</span><span class="sxs-lookup"><span data-stu-id="6526c-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="6526c-127">Dans l’extrait de code précédent, « batchClient » est une instance de la classe [BatchClient][net_batchclient].</span><span class="sxs-lookup"><span data-stu-id="6526c-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="6526c-128">Création de tâches dépendantes</span><span class="sxs-lookup"><span data-stu-id="6526c-128">Create dependent tasks</span></span>
<span data-ttu-id="6526c-129">Pour créer une tâche qui dépend de l’exécution d’une ou plusieurs tâches parentes, vous devez indiquer que la tâche « dépend » des autres tâches.</span><span class="sxs-lookup"><span data-stu-id="6526c-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="6526c-130">Dans Batch.NET, configurez la propriété [CloudTask][net_cloudtask].[DependsOn][net_dependson] avec une instance de la classe [TaskDependencies][net_taskdependencies] :</span><span class="sxs-lookup"><span data-stu-id="6526c-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="6526c-131">Cet extrait de code crée une tâche dépendante avec l’ID de tâche « Flowers ».</span><span class="sxs-lookup"><span data-stu-id="6526c-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="6526c-132">La tâche « Flowers » dépend des tâches « Rain » et « Sun ».</span><span class="sxs-lookup"><span data-stu-id="6526c-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="6526c-133">La tâche « Flowers » est programmée pour s’exécuter sur un nœud de calcul uniquement après la réussite de l’exécution des tâches « Rain » et « Sun ».</span><span class="sxs-lookup"><span data-stu-id="6526c-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="6526c-134">Une tâche est considérée comme réussie lorsqu’elle se trouve à l’état **terminé** et que son **code de sortie** est `0`.</span><span class="sxs-lookup"><span data-stu-id="6526c-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="6526c-135">Dans Batch.NET, la valeur de propriété [CloudTask][net_cloudtask].[State][net_taskstate] doit être `Completed` et la valeur de propriété [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] de CloudTask doit être de `0`.</span><span class="sxs-lookup"><span data-stu-id="6526c-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="6526c-136">scénarios de dépendance</span><span class="sxs-lookup"><span data-stu-id="6526c-136">Dependency scenarios</span></span>
<span data-ttu-id="6526c-137">Vous pouvez utiliser trois scénarios de dépendance de tâches de base dans Azure Batch : un-à-un, un-à-plusieurs et dépendance de plage d’ID de tâche.</span><span class="sxs-lookup"><span data-stu-id="6526c-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="6526c-138">Ces scénarios peuvent être combinés pour créer un quatrième scénario : plusieurs-à-plusieurs.</span><span class="sxs-lookup"><span data-stu-id="6526c-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="6526c-139">Scénario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="6526c-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="6526c-140">Exemple</span><span class="sxs-lookup"><span data-stu-id="6526c-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="6526c-141">Un-à-un</span><span class="sxs-lookup"><span data-stu-id="6526c-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="6526c-142">*taskB* dépend de *taskA*</span><span class="sxs-lookup"><span data-stu-id="6526c-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="6526c-143">*taskB* n’est pas planifié pour s’exécuter tant que l’exécution de *taskA* n’est pas terminée</span><span class="sxs-lookup"><span data-stu-id="6526c-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="6526c-144">![Schéma : dépendance de tâches un-à-un][1]</span><span class="sxs-lookup"><span data-stu-id="6526c-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="6526c-145">Un-à-plusieurs</span><span class="sxs-lookup"><span data-stu-id="6526c-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="6526c-146">*taskC* dépend de *taskA* et de *taskB*</span><span class="sxs-lookup"><span data-stu-id="6526c-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="6526c-147">*taskC* n’est pas planifié pour s’exécuter tant que l’exécution de *taskA* et *taskB* n’est pas terminée</span><span class="sxs-lookup"><span data-stu-id="6526c-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="6526c-148">![Schéma : dépendance de tâches un-à-plusieurs][2]</span><span class="sxs-lookup"><span data-stu-id="6526c-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="6526c-149">Plage d’ID de tâche</span><span class="sxs-lookup"><span data-stu-id="6526c-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="6526c-150">*taskD* dépend d’une plage de tâches</span><span class="sxs-lookup"><span data-stu-id="6526c-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="6526c-151">*taskD* n’est pas planifié pour s’exécuter tant que l’exécution des tâches associées aux ID *1* à *10* n’est pas terminée</span><span class="sxs-lookup"><span data-stu-id="6526c-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="6526c-152">![Schéma : dépendance de plage d’ID de tâche][3]</span><span class="sxs-lookup"><span data-stu-id="6526c-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="6526c-153">Vous pouvez créer des relations **plusieurs-à-plusieurs** où, par exemple, les tâches C, D, E et F dépendent toutes des tâches A et B. Cela est utile, par exemple, dans les scénarios de prétraitement parallélisés où vos tâches en aval dépendent de la sortie de plusieurs tâches en amont.</span><span class="sxs-lookup"><span data-stu-id="6526c-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="6526c-154">Dans les exemples de cette section, une tâche dépendante s’exécute uniquement après l’achèvement des tâches parentes.</span><span class="sxs-lookup"><span data-stu-id="6526c-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="6526c-155">Ce comportement est le comportement par défaut d’une tâche dépendante.</span><span class="sxs-lookup"><span data-stu-id="6526c-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="6526c-156">Vous pouvez exécuter une tâche dépendante après l’échec d’une tâche parente en indiquant l’action de dépendance destinée à se substituer au comportement par défaut.</span><span class="sxs-lookup"><span data-stu-id="6526c-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="6526c-157">Pour plus d’informations, consultez la section [Actions de dépendance](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="6526c-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="6526c-158">Un-à-un</span><span class="sxs-lookup"><span data-stu-id="6526c-158">One-to-one</span></span>
<span data-ttu-id="6526c-159">Dans une relation un-à-un, une tâche dépend de la bonne exécution d’une tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="6526c-160">Pour créer la dépendance, fournissez un ID de tâche unique à la méthode statique [TaskDependencies][net_taskdependencies].[OnId][net_onid] lorsque vous renseignez la propriété [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="6526c-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="6526c-161">Un-à-plusieurs</span><span class="sxs-lookup"><span data-stu-id="6526c-161">One-to-many</span></span>
<span data-ttu-id="6526c-162">Dans une relation un-à-plusieurs, une tâche dépend de la bonne exécution de plusieurs tâches parentes.</span><span class="sxs-lookup"><span data-stu-id="6526c-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="6526c-163">Pour créer la dépendance, fournissez une collection d’ID de tâche à la méthode statique [TaskDependencies][net_taskdependencies].[OnId][net_onids] lorsque vous renseignez la propriété [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="6526c-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="6526c-164">Plage d’ID de tâche</span><span class="sxs-lookup"><span data-stu-id="6526c-164">Task ID range</span></span>
<span data-ttu-id="6526c-165">Vous pouvez même créer une dépendance de plage de tâches parentes, une tâche dépend de la bonne exécution des tâches dont les ID figurent dans une plage spécifique.</span><span class="sxs-lookup"><span data-stu-id="6526c-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="6526c-166">Pour créer la dépendance, fournissez le premier et le dernier ID de tâche dans la plage à la méthode statique [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] lorsque vous renseignez la propriété [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="6526c-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6526c-167">Lorsque vous utilisez des plages d’ID de tâche pour vos dépendances, les ID de tâche de la plage *doivent* être des représentations sous forme de chaîne de valeurs entières.</span><span class="sxs-lookup"><span data-stu-id="6526c-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="6526c-168">Chaque tâche de la plage doit satisfaire la dépendance soit en se terminant avec succès, soit en échouant avec une erreur associée à une action de dépendance définie sur **Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="6526c-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="6526c-169">Pour plus d’informations, consultez la section [Actions de dépendance](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="6526c-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="6526c-170">Actions de dépendance</span><span class="sxs-lookup"><span data-stu-id="6526c-170">Dependency actions</span></span>

<span data-ttu-id="6526c-171">Par défaut, une tâche dépendante ou un ensemble de tâches s’exécute uniquement après la fin d’une tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="6526c-172">Dans certains scénarios, vous pouvez exécuter des tâches dépendantes même si la tâche parente échoue.</span><span class="sxs-lookup"><span data-stu-id="6526c-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="6526c-173">Vous pouvez remplacer le comportement par défaut en spécifiant une action de dépendance.</span><span class="sxs-lookup"><span data-stu-id="6526c-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="6526c-174">Une action de dépendance spécifie si une tâche dépendante peut être exécutée en fonction de la réussite ou de l’échec de la tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="6526c-175">Par exemple, supposons qu’une tâche dépendante attend des données de l’achèvement de la tâche amont.</span><span class="sxs-lookup"><span data-stu-id="6526c-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="6526c-176">Si la tâche en amont échoue, la tâche dépendante peut toujours être en mesure de s’exécuter en utilisant des données plus anciennes.</span><span class="sxs-lookup"><span data-stu-id="6526c-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="6526c-177">Dans ce cas, une action de dépendance peut spécifier que la tâche dépendante peut être exécutée malgré l’échec de la tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="6526c-178">Une action de dépendance est basée sur une condition de sortie pour la tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="6526c-179">Vous pouvez indiquer une action de dépendance pour toutes les conditions de sortie suivantes ; pour un environnement .NET, consultez la classe [ExitConditions][net_exitconditions] :</span><span class="sxs-lookup"><span data-stu-id="6526c-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="6526c-180">Lorsqu’une erreur de prétraitement se produit.</span><span class="sxs-lookup"><span data-stu-id="6526c-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="6526c-181">Lorsqu’une erreur de chargement de fichier se produit.</span><span class="sxs-lookup"><span data-stu-id="6526c-181">When a file upload error occurs.</span></span> <span data-ttu-id="6526c-182">Si la tâche se termine avec un code de sortie qui a été spécifié via **exitCodes** ou **exitCodeRanges**, puis rencontre une erreur de chargement de fichier, l’action spécifiée par le code de sortie est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="6526c-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="6526c-183">Lorsque la tâche se termine avec un code de sortie défini par la propriété **ExitCodes**.</span><span class="sxs-lookup"><span data-stu-id="6526c-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="6526c-184">Lorsque la tâche se termine avec un code de sortie dans une plage définie par la propriété **ExitCodeRanges**.</span><span class="sxs-lookup"><span data-stu-id="6526c-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="6526c-185">Le cas par défaut : si la tâche se termine avec un code de sortie non défini par **ExitCodes** ou **ExitCodeRanges**, ou si la tâche se termine avec une erreur de prétraitement et si la propriété **PreProcessingError** n’est pas définie, ou si la tâche échoue avec une erreur de chargement de fichier et si la propriété **FileUploadError** n’est pas définie.</span><span class="sxs-lookup"><span data-stu-id="6526c-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="6526c-186">Pour spécifier une action de dépendance dans .NET, définissez la propriété [ExitOptions][net_exitoptions].[ DependencyAction][net_dependencyaction] pour la condition de sortie.</span><span class="sxs-lookup"><span data-stu-id="6526c-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="6526c-187">La propriété **DependencyAction** accepte l’une des deux valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="6526c-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="6526c-188">Définir la propriété **DependencyAction** sur **Satisfy** indique que les tâches dépendantes sont autorisées à s’exécuter si la tâche parente se termine avec une erreur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="6526c-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="6526c-189">Définir la propriété **DependencyAction** sur **Block** indique que les tâches dépendantes ne sont pas autorisées à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="6526c-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="6526c-190">Le paramètre par défaut de la propriété **DependencyAction** est **Satisfy** pour le code de sortie 0 et **Block** pour toutes les autres conditions de sortie.</span><span class="sxs-lookup"><span data-stu-id="6526c-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="6526c-191">L’extrait de code suivant définit la propriété **DependencyAction** d’une tâche parente.</span><span class="sxs-lookup"><span data-stu-id="6526c-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="6526c-192">Si la tâche parente se termine avec une erreur de prétraitement ou avec les codes d’erreur spécifiés, la tâche dépendante est bloquée.</span><span class="sxs-lookup"><span data-stu-id="6526c-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="6526c-193">Si la tâche parente se termine avec une autre erreur non nulle, la tâche dépendante peut être exécutée.</span><span class="sxs-lookup"><span data-stu-id="6526c-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="6526c-194">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="6526c-194">Code sample</span></span>
<span data-ttu-id="6526c-195">L’exemple de projet [TaskDependencies][github_taskdependencies] est l’un des [exemples de code Azure Batch][github_samples] disponibles sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="6526c-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="6526c-196">La solution Visual Studio montre :</span><span class="sxs-lookup"><span data-stu-id="6526c-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="6526c-197">Comment activer la dépendance d’une tâche</span><span class="sxs-lookup"><span data-stu-id="6526c-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="6526c-198">Comment créer des tâches qui dépendent d’autres tâches</span><span class="sxs-lookup"><span data-stu-id="6526c-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="6526c-199">Comment exécuter ces tâches sur un pool de nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="6526c-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6526c-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6526c-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="6526c-201">Déploiement des applications</span><span class="sxs-lookup"><span data-stu-id="6526c-201">Application deployment</span></span>
<span data-ttu-id="6526c-202">La fonctionnalité [packages d’application](batch-application-packages.md) de Batch est un moyen facile de déployer et contrôler les versions des applications exécutées par vos tâches sur des nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="6526c-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="6526c-203">Installation d’applications et de données intermédiaires</span><span class="sxs-lookup"><span data-stu-id="6526c-203">Installing applications and staging data</span></span>
<span data-ttu-id="6526c-204">Pour découvrir les méthodes de préparation des nœuds à l’exécution de tâches, consultez l’article [Installing applications and staging data on Batch compute nodes][forum_post] (Installation d’applications et de données intermédiaires sur les nœuds de calcul Batch) sur le forum Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="6526c-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="6526c-205">Rédigée par un membre de l’équipe Azure Batch, cette publication est une excellente introduction aux différentes façons de copier des applications, des données d’entrée de tâche et d’autres fichiers sur vos nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="6526c-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

<span data-ttu-id="6526c-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Schéma : dépendance un-à-un"</span><span class="sxs-lookup"><span data-stu-id="6526c-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="6526c-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Schéma : dépendance un-à-plusieurs"</span><span class="sxs-lookup"><span data-stu-id="6526c-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="6526c-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Schéma : dépendance de plage d’ID de tâche"</span><span class="sxs-lookup"><span data-stu-id="6526c-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>
