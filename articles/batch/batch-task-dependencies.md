---
title: "aaaUse tâche dépendances toorun tâches basées sur la réalisation de hello d’autres tâches - Azure Batch | Documents Microsoft"
description: "Créez des tâches qui dépendent d’achèvement hello d’autres tâches de traitement de style MapReduce et données big similaires les charges de travail en traitement par lots Azure."
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
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="26860-103">Créer des interdépendances toorun les tâches qui dépendent d’autres tâches</span><span class="sxs-lookup"><span data-stu-id="26860-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="26860-104">Vous pouvez définir toorun des dépendances de tâche une tâche ou un ensemble de tâches uniquement après qu’une tâche parente est terminée.</span><span class="sxs-lookup"><span data-stu-id="26860-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="26860-105">Voici quelques scénarios dont les dépendances de tâche sont utiles :</span><span class="sxs-lookup"><span data-stu-id="26860-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="26860-106">Charges de travail MapReduce de style dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="26860-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="26860-107">des travaux dont les tâches de traitement des données peuvent être exprimées sous la forme d’un graphe orienté acyclique (DAG) ;</span><span class="sxs-lookup"><span data-stu-id="26860-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="26860-108">Processus de rendu avant et après le rendu, où chaque tâche doit se terminer avant le début de la tâche suivante hello.</span><span class="sxs-lookup"><span data-stu-id="26860-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="26860-109">N’importe quel travail dans lequel les tâches en aval dépendent de sortie hello de tâches en amont.</span><span class="sxs-lookup"><span data-stu-id="26860-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="26860-110">Avec les dépendances de tâche de traitement par lots, vous pouvez créer des tâches qui sont planifiées pour l’exécution sur les nœuds de calcul après l’achèvement de hello d’une ou plusieurs tâches parent.</span><span class="sxs-lookup"><span data-stu-id="26860-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="26860-111">Par exemple, vous pouvez créer un travail qui restitue chaque image d’un film 3D avec des tâches parallèles distinctes.</span><span class="sxs-lookup"><span data-stu-id="26860-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="26860-112">tâche finale de Hello--hello « tâche de fusion »--fusions hello images rendue dans la vidéo complète de hello uniquement une fois toutes les images ont été correctement rendus.</span><span class="sxs-lookup"><span data-stu-id="26860-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="26860-113">Par défaut, les tâches dépendantes sont planifiées pour l’exécution uniquement après hello parent est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="26860-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="26860-114">Vous pouvez spécifier un comportement par défaut de dépendance action toooverride hello et exécuter des tâches en cas d’échec de la tâche parente de hello.</span><span class="sxs-lookup"><span data-stu-id="26860-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="26860-115">Consultez hello [actions de dépendance](#dependency-actions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="26860-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="26860-116">Vous pouvez créer des tâches qui dépendent d’autres tâches dans une relation un-à-un ou un-à-plusieurs.</span><span class="sxs-lookup"><span data-stu-id="26860-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="26860-117">Vous pouvez également créer une dépendance de la plage où une tâche dépend d’achèvement hello d’un groupe de tâches au sein d’une plage d’ID de tâche spécifiée.</span><span class="sxs-lookup"><span data-stu-id="26860-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="26860-118">Vous pouvez combiner ces trois relations plusieurs-à-plusieurs de toocreate des scénarios de base.</span><span class="sxs-lookup"><span data-stu-id="26860-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="26860-119">Dépendances de tâches avec Batch.NET</span><span class="sxs-lookup"><span data-stu-id="26860-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="26860-120">Dans cet article, nous expliquons comment tooconfigure les dépendances de tâche à l’aide de hello [Batch .NET] [ net_msdn] bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="26860-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="26860-121">Nous avons tout d’abord montrent comment trop[activer interdépendance](#enable-task-dependencies) dans vos projets, puis d’illustrer comment trop[configurer une tâche avec des dépendances](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="26860-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="26860-122">Nous expliquons également comment toospecify une dépendance action toorun tâches dépendantes si le parent de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="26860-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="26860-123">Enfin, nous évoquerons hello [scénarios dépendance](#dependency-scenarios) qui prend en charge de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="26860-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="26860-124">Activation des dépendances de tâches</span><span class="sxs-lookup"><span data-stu-id="26860-124">Enable task dependencies</span></span>
<span data-ttu-id="26860-125">toouse les dépendances de tâches dans votre application de traitement par lots, vous devez d’abord configurer interdépendances toouse de travail hello.</span><span class="sxs-lookup"><span data-stu-id="26860-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="26860-126">Dans .NET de lot, l’activer sur votre [CloudJob] [ net_cloudjob] en définissant son [UsesTaskDependencies] [ net_usestaskdependencies] propriété trop`true`:</span><span class="sxs-lookup"><span data-stu-id="26860-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="26860-127">Bonjour précédant l’extrait de code, « batchClient » est une instance de hello [BatchClient] [ net_batchclient] classe.</span><span class="sxs-lookup"><span data-stu-id="26860-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="26860-128">Création de tâches dépendantes</span><span class="sxs-lookup"><span data-stu-id="26860-128">Create dependent tasks</span></span>
<span data-ttu-id="26860-129">toocreate une tâche qui dépend d’achèvement hello d’une ou plusieurs tâches parent, vous pouvez spécifier que hello hello de tâche « dépend » autres tâches.</span><span class="sxs-lookup"><span data-stu-id="26860-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="26860-130">Dans .NET de lot, configurer hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] propriété avec une instance de hello [TaskDependencies] [ net_taskdependencies] classe :</span><span class="sxs-lookup"><span data-stu-id="26860-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="26860-131">Cet extrait de code crée une tâche dépendante avec l’ID de tâche « Flowers ».</span><span class="sxs-lookup"><span data-stu-id="26860-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="26860-132">Hello « Fleurs » tâche dépend des tâches « Train » et « Sun ».</span><span class="sxs-lookup"><span data-stu-id="26860-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="26860-133">La tâche « Fleurs » sera toorun planifiée sur un nœud de calcul uniquement une fois les tâches « Train » et « Sun » sont terminés.</span><span class="sxs-lookup"><span data-stu-id="26860-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="26860-134">Une tâche est considérée comme toobe s’est terminée correctement quand il sera hello **terminé** état et son **code de sortie** est `0`.</span><span class="sxs-lookup"><span data-stu-id="26860-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="26860-135">Dans .NET de traitement par lots, cela signifie une [CloudTask][net_cloudtask].[ État] [ net_taskstate] valeur de propriété `Completed` et hello du CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] valeur de propriété est `0`.</span><span class="sxs-lookup"><span data-stu-id="26860-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="26860-136">scénarios de dépendance</span><span class="sxs-lookup"><span data-stu-id="26860-136">Dependency scenarios</span></span>
<span data-ttu-id="26860-137">Vous pouvez utiliser trois scénarios de dépendance de tâches de base dans Azure Batch : un-à-un, un-à-plusieurs et dépendance de plage d’ID de tâche.</span><span class="sxs-lookup"><span data-stu-id="26860-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="26860-138">Il peuvent être combiné tooprovide une quatrième scénario, plusieurs-à-plusieurs.</span><span class="sxs-lookup"><span data-stu-id="26860-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="26860-139">Scénario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="26860-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="26860-140">Exemple</span><span class="sxs-lookup"><span data-stu-id="26860-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="26860-141">Un-à-un</span><span class="sxs-lookup"><span data-stu-id="26860-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="26860-142">*taskB* dépend de *taskA*</span><span class="sxs-lookup"><span data-stu-id="26860-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="26860-143">*taskB* n’est pas planifié pour s’exécuter tant que l’exécution de *taskA* n’est pas terminée</span><span class="sxs-lookup"><span data-stu-id="26860-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="26860-144">![Schéma : dépendance de tâches un-à-un][1]</span><span class="sxs-lookup"><span data-stu-id="26860-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="26860-145">Un-à-plusieurs</span><span class="sxs-lookup"><span data-stu-id="26860-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="26860-146">*taskC* dépend de *taskA* et de *taskB*</span><span class="sxs-lookup"><span data-stu-id="26860-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="26860-147">*taskC* n’est pas planifié pour s’exécuter tant que l’exécution de *taskA* et *taskB* n’est pas terminée</span><span class="sxs-lookup"><span data-stu-id="26860-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="26860-148">![Schéma : dépendance de tâches un-à-plusieurs][2]</span><span class="sxs-lookup"><span data-stu-id="26860-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="26860-149">Plage d’ID de tâche</span><span class="sxs-lookup"><span data-stu-id="26860-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="26860-150">*taskD* dépend d’une plage de tâches</span><span class="sxs-lookup"><span data-stu-id="26860-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="26860-151">*taskD* ne sera pas planifié pour l’exécution jusqu'à ce que les tâches hello avec des ID *1* via *10* terminées avec succès</span><span class="sxs-lookup"><span data-stu-id="26860-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="26860-152">![Schéma : dépendance de plage d’ID de tâche][3]</span><span class="sxs-lookup"><span data-stu-id="26860-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="26860-153">Vous pouvez créer **plusieurs-à-plusieurs** relations, telles que les tâches C, D, E et F chaque où dépendent de tâches A et B. Cela est utile, par exemple, dans des scénarios de prétraitement parallélisées où vos tâches en aval dépendent de sortie hello de plusieurs tâches en amont.</span><span class="sxs-lookup"><span data-stu-id="26860-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="26860-154">Dans les exemples hello dans cette section, une tâche dépendante s’exécute uniquement une fois hello parent tâches terminées.</span><span class="sxs-lookup"><span data-stu-id="26860-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="26860-155">Ce comportement est le comportement par défaut de hello pour une tâche dépendante.</span><span class="sxs-lookup"><span data-stu-id="26860-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="26860-156">Vous pouvez exécuter une tâche dépendante après l’échec d’une tâche parent en spécifiant un comportement par défaut de dépendance action toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="26860-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="26860-157">Consultez hello [actions de dépendance](#dependency-actions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="26860-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="26860-158">Un-à-un</span><span class="sxs-lookup"><span data-stu-id="26860-158">One-to-one</span></span>
<span data-ttu-id="26860-159">Dans le type de relation, une tâche dépend hello tâche se termine correctement un seul parent.</span><span class="sxs-lookup"><span data-stu-id="26860-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="26860-160">toocreate hello dépendance, fournissez un toohello d’ID de tâche unique [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] une méthode statique lorsque vous remplissez hello [DependsOn] [ net_dependson] propriété du [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="26860-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="26860-161">Un-à-plusieurs</span><span class="sxs-lookup"><span data-stu-id="26860-161">One-to-many</span></span>
<span data-ttu-id="26860-162">Dans une relation un-à-plusieurs, une tâche dépend à la fin de hello de plusieurs tâches parent.</span><span class="sxs-lookup"><span data-stu-id="26860-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="26860-163">toocreate hello dépendance, fournissent une collection de tâches ID toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] une méthode statique lorsque vous remplissez hello [DependsOn] [ net_dependson] propriété du [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="26860-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="26860-164">Plage d’ID de tâche</span><span class="sxs-lookup"><span data-stu-id="26860-164">Task ID range</span></span>
<span data-ttu-id="26860-165">Une dépendance sur une plage de tâches parentes, une tâche dépend à la fin de hello hello de tâches dont les ID se situent dans une plage.</span><span class="sxs-lookup"><span data-stu-id="26860-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="26860-166">dépendance de hello toocreate, fournir tout d’abord les hello et dernier ID de tâches dans hello plage toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] une méthode statique lorsque vous remplissez hello [DependsOn] [ net_dependson] propriété du [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="26860-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26860-167">Lorsque vous utilisez des plages d’ID de tâche pour les dépendances, hello ID de tâche dans la plage de hello *doit* être représentations sous forme de chaîne de valeurs entières.</span><span class="sxs-lookup"><span data-stu-id="26860-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="26860-168">Chaque tâche dans la plage de hello doit satisfaire la dépendance de hello, terminé ou en procédant avec un échec est l’action de dépendance mappé tooa définie trop**satisfaction**.</span><span class="sxs-lookup"><span data-stu-id="26860-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="26860-169">Consultez hello [actions de dépendance](#dependency-actions) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="26860-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="26860-170">Actions de dépendance</span><span class="sxs-lookup"><span data-stu-id="26860-170">Dependency actions</span></span>

<span data-ttu-id="26860-171">Par défaut, une tâche dépendante ou un ensemble de tâches s’exécute uniquement après la fin d’une tâche parente.</span><span class="sxs-lookup"><span data-stu-id="26860-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="26860-172">Dans certains scénarios, vous pouvez vouloir toorun des tâches dépendantes même si la tâche parent hello échoue.</span><span class="sxs-lookup"><span data-stu-id="26860-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="26860-173">Vous pouvez remplacer le comportement par défaut de hello en spécifiant une action de dépendance.</span><span class="sxs-lookup"><span data-stu-id="26860-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="26860-174">Une action de dépendance Spécifie si une tâche dépendante est éligible toorun, en fonction de la réussite de hello ou l’échec de la tâche parente de hello.</span><span class="sxs-lookup"><span data-stu-id="26860-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="26860-175">Par exemple, supposons qu’une tâche dépendante est en attente de données à partir de la fin de hello de tâche en amont hello.</span><span class="sxs-lookup"><span data-stu-id="26860-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="26860-176">Si la tâche en amont hello échoue, tâche dépendante hello peut-être toujours en mesure de toorun à l’aide des données plus anciennes.</span><span class="sxs-lookup"><span data-stu-id="26860-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="26860-177">Dans ce cas, une action de dépendance peut spécifier que cette tâche de dépendants hello est éligible toorun en dépit de l’échec hello de la tâche parente de hello.</span><span class="sxs-lookup"><span data-stu-id="26860-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="26860-178">Une action de dépendance est basée sur une condition de sortie de la tâche parente de hello.</span><span class="sxs-lookup"><span data-stu-id="26860-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="26860-179">Vous pouvez spécifier une action de dépendance des hello suivant des conditions de sortie ; pour .NET, consultez hello [ExitConditions] [ net_exitconditions] classe pour plus d’informations :</span><span class="sxs-lookup"><span data-stu-id="26860-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="26860-180">Lorsqu’une erreur de prétraitement se produit.</span><span class="sxs-lookup"><span data-stu-id="26860-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="26860-181">Lorsqu’une erreur de chargement de fichier se produit.</span><span class="sxs-lookup"><span data-stu-id="26860-181">When a file upload error occurs.</span></span> <span data-ttu-id="26860-182">Si la tâche hello se termine avec un code de sortie qui a été spécifié via **exitCodes** ou **exitCodeRanges**, puis rencontre une erreur de chargement du fichier, l’action hello spécifié par hello exit code est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="26860-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="26860-183">Lorsque la tâche hello se termine avec un code de sortie défini par hello **ExitCodes** propriété.</span><span class="sxs-lookup"><span data-stu-id="26860-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="26860-184">Lorsque la tâche hello se termine avec un code de sortie qui se situe dans une plage spécifiée par hello **ExitCodeRanges** propriété.</span><span class="sxs-lookup"><span data-stu-id="26860-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="26860-185">Hello cas par défaut, si la tâche hello se termine avec un code de sortie non défini par **ExitCodes** ou **ExitCodeRanges**, ou si la tâche hello se termine avec une erreur de prétraitement et hello **PreProcessingError**  propriété n’est pas définie, ou si hello de tâches échoue avec un fichier télécharger erreur et hello **FileUploadError** propriété n’est pas définie.</span><span class="sxs-lookup"><span data-stu-id="26860-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="26860-186">toospecify une action de dépendance dans .NET, jeu hello [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] propriété de condition de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="26860-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="26860-187">Hello **DependencyAction** propriété prend l’une des deux valeurs :</span><span class="sxs-lookup"><span data-stu-id="26860-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="26860-188">Hello du paramètre **DependencyAction** propriété trop**satisfaction** indique que les tâches dépendantes sont éligible toorun si la tâche parente de hello se termine avec une erreur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="26860-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="26860-189">Hello du paramètre **DependencyAction** propriété trop**bloc** indique que les tâches dépendantes ne sont pas éligible toorun.</span><span class="sxs-lookup"><span data-stu-id="26860-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="26860-190">Hello du paramètre par défaut pour hello **DependencyAction** propriété **satisfaction** pour le code de sortie 0, et **bloc** pour toutes les autres conditions de sortie.</span><span class="sxs-lookup"><span data-stu-id="26860-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="26860-191">Hello extrait de code suivant définit hello **DependencyAction** propriété pour une tâche parente.</span><span class="sxs-lookup"><span data-stu-id="26860-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="26860-192">Si tâche parente de hello se termine avec une erreur de traitement préliminaire ou par hello les codes d’erreur spécifié, hello dépendants tâche est bloquée.</span><span class="sxs-lookup"><span data-stu-id="26860-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="26860-193">Si la tâche parente de hello se termine avec une autre erreur non nulle, les tâches dépendantes hello sont toorun éligible.</span><span class="sxs-lookup"><span data-stu-id="26860-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
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
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="26860-194">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="26860-194">Code sample</span></span>
<span data-ttu-id="26860-195">Hello [TaskDependencies] [ github_taskdependencies] exemple de projet est un des hello [exemples de code Azure Batch] [ github_samples] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="26860-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="26860-196">La solution Visual Studio montre :</span><span class="sxs-lookup"><span data-stu-id="26860-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="26860-197">Comment tooenable tâche dépendant d’un travail</span><span class="sxs-lookup"><span data-stu-id="26860-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="26860-198">Comment toocreate tâches qui dépendent d’autres tâches</span><span class="sxs-lookup"><span data-stu-id="26860-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="26860-199">Comment tooexecute ces tâches sur un pool de nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="26860-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26860-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26860-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="26860-201">Déploiement des applications</span><span class="sxs-lookup"><span data-stu-id="26860-201">Application deployment</span></span>
<span data-ttu-id="26860-202">Hello [des packages d’application](batch-application-packages.md) fonctionnalité du lot fournit une facilement tooboth déployer et une version applications hello vos tâches s’exécutent sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="26860-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="26860-203">Installation d’applications et de données intermédiaires</span><span class="sxs-lookup"><span data-stu-id="26860-203">Installing applications and staging data</span></span>
<span data-ttu-id="26860-204">Consultez [l’installation d’applications et de mise en attente de traitement par lots des nœuds de calcul] [ forum_post] dans le forum Azure Batch hello pour une vue d’ensemble des méthodes pour la préparation de vos nœuds toorun tâches.</span><span class="sxs-lookup"><span data-stu-id="26860-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="26860-205">Écrit par un des membres de l’équipe Azure Batch hello, que cette publication est une bonne introduction sur les applications de toocopy de différentes façons de hello, les données d’entrée de tâches et autres tooyour fichiers nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="26860-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

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

[1]: ./media/batch-task-dependency/01_one_to_one.png "Schéma : dépendance un-à-un"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Schéma : dépendance un-à-plusieurs"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Schéma : dépendance de plage d’ID de tâche"
