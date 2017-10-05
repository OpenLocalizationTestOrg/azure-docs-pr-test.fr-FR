---
title: "Créer des tâches pour préparer et exécuter des travaux sur les nœuds de calcul - Azure Batch | Microsoft Docs"
description: "Utilisez des tâches de préparation au niveau du travail afin de minimiser le transfert de données vers les nœuds de calcul Azure Batch, et utilisez des tâches de validation pour le nettoyage des nœuds une fois le travail achevé."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="82015-103">Exécuter des tâches de préparation et de validation du travail sur les nœuds de calcul Batch</span><span class="sxs-lookup"><span data-stu-id="82015-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="82015-104">Un travail Azure Batch nécessite souvent une certaine forme de préparation avant l’exécution de ses tâches, ainsi qu’une maintenance ultérieure une fois les tâches terminées.</span><span class="sxs-lookup"><span data-stu-id="82015-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="82015-105">Vous pouvez avoir besoin de télécharger les données d’entrée de tâche communes dans vos nœuds de calcul, ou de charger les données de sortie de tâche dans le stockage Azure une fois le travail terminé.</span><span class="sxs-lookup"><span data-stu-id="82015-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="82015-106">Vous pouvez effectuer ces opérations à l’aide des tâches de **préparation du travail** et de **validation du travail**.</span><span class="sxs-lookup"><span data-stu-id="82015-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="82015-107">En quoi consistent les tâches de préparation et de validation du travail ?</span><span class="sxs-lookup"><span data-stu-id="82015-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="82015-108">Avant l’exécution des tâches d’un travail, la tâche de préparation du travail s’exécute sur tous les nœuds de calcul destinés à exécuter au moins l’une des tâches.</span><span class="sxs-lookup"><span data-stu-id="82015-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="82015-109">Lorsqu'un travail est terminé, la tâche de validation du travail s'exécute sur chaque nœud dans le pool ayant exécuté au moins une tâche.</span><span class="sxs-lookup"><span data-stu-id="82015-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="82015-110">Comme dans le cas des tâches Batch standard, vous pouvez spécifier une ligne de commande à appeler lors de l’exécution d’une tâche de préparation ou de validation du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="82015-111">Les tâches de préparation et de validation du travail offrent des fonctionnalités de tâche Batch courantes, telles que téléchargement de fichiers ([fichiers de ressources][net_job_prep_resourcefiles]), exécution avec élévation de privilèges, variables d’environnement personnalisées, durée d’exécution maximale, nombre de tentatives et période de rétention des fichiers.</span><span class="sxs-lookup"><span data-stu-id="82015-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="82015-112">Dans les sections ci-après, vous découvrirez comment utiliser les classes [JobPreparationTask][net_job_prep] et [JobReleaseTask][net_job_release] disponibles dans la bibliothèque [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="82015-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="82015-113">Les tâches de préparation et de validation du travail sont particulièrement utiles dans les environnements de « pool partagé », dans lesquels un pool de nœuds de calcul persiste entre les exécutions d’un travail et est utilisé par de nombreux travaux.</span><span class="sxs-lookup"><span data-stu-id="82015-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="82015-114">Utilisation des tâches de préparation et de validation du travail</span><span class="sxs-lookup"><span data-stu-id="82015-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="82015-115">Les tâches de préparation et de validation du travail sont parfaitement adaptées aux opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="82015-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="82015-116">**Télécharger les données de tâche communes**</span><span class="sxs-lookup"><span data-stu-id="82015-116">**Download common task data**</span></span>

<span data-ttu-id="82015-117">Les travaux Batch nécessitent souvent un ensemble commun de données comme entrée pour les tâches du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="82015-118">Par exemple, dans les calculs quotidiens de l’analyse des risques, les données de marché sont propres à un travail, mais communes à toutes les tâches de ce travail.</span><span class="sxs-lookup"><span data-stu-id="82015-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="82015-119">Ces données de marché, dont la taille atteint souvent plusieurs gigaoctets, ne doivent être téléchargées qu’une seule fois dans chaque nœud de calcul pour être utilisables par toutes les tâches qui s’exécutent sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="82015-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="82015-120">Utilisez une **tâche de préparation du travail** pour télécharger ces données sur chaque nœud avant l’exécution des autres tâches du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="82015-121">**Supprimer la sortie des travaux et des tâches**</span><span class="sxs-lookup"><span data-stu-id="82015-121">**Delete job and task output**</span></span>

<span data-ttu-id="82015-122">Dans un environnement de « pool partagé » dans lequel les nœuds de calcul d’un pool ne sont pas désactivés entre les travaux, il peut être nécessaire de supprimer les données du travail entre les exécutions</span><span class="sxs-lookup"><span data-stu-id="82015-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="82015-123">afin d’économiser de l’espace disque sur les nœuds ou de respecter les stratégies de sécurité de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="82015-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="82015-124">Utilisez une **tâche de validation du travail** pour supprimer les données téléchargées par une tâche de préparation du travail ou générées pendant l’exécution d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="82015-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="82015-125">**Rétention des journaux**</span><span class="sxs-lookup"><span data-stu-id="82015-125">**Log retention**</span></span>

<span data-ttu-id="82015-126">Vous voulez peut-être conserver une copie des fichiers journaux générés par les tâches ou peut-être les fichiers de vidage sur incident qui peuvent être générés par les applications ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="82015-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="82015-127">Dans ces cas, utilisez une **tâche de validation du travail** pour compresser et télécharger ces données vers un compte de [Stockage Azure][azure_storage].</span><span class="sxs-lookup"><span data-stu-id="82015-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="82015-128">Une autre façon de conserver les journaux et les autres données de sortie des travaux et des tâches consiste à utiliser la bibliothèque de [conventions de fichier Azure Batch](batch-task-output.md) .</span><span class="sxs-lookup"><span data-stu-id="82015-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="82015-129">tâche de préparation du travail</span><span class="sxs-lookup"><span data-stu-id="82015-129">Job preparation task</span></span>
<span data-ttu-id="82015-130">Avant l’exécution des tâches d’un travail, Batch exécute la tâche de préparation du travail sur chaque nœud de calcul sur lequel l’exécution d’une tâche est planifiée.</span><span class="sxs-lookup"><span data-stu-id="82015-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="82015-131">Par défaut, le service Batch attend la fin de la tâche de préparation du travail avant d’exécuter les tâches destinées à s’exécuter sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="82015-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="82015-132">Toutefois, vous pouvez configurer le service pour qu'il n'attende pas.</span><span class="sxs-lookup"><span data-stu-id="82015-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="82015-133">Si le nœud redémarre, la tâche de préparation du travail s’exécute de nouveau. Toutefois, vous pouvez également désactiver ce comportement.</span><span class="sxs-lookup"><span data-stu-id="82015-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="82015-134">La tâche de préparation du travail est uniquement exécutée sur les nœuds sur lesquels l’exécution d’une tâche est planifiée.</span><span class="sxs-lookup"><span data-stu-id="82015-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="82015-135">Ceci empêche l'exécution d'une tâche de préparation inutile dans le cas où une tâche n'est pas attribuée à un nœud.</span><span class="sxs-lookup"><span data-stu-id="82015-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="82015-136">Cette situation peut survenir lorsque le nombre de tâches pour un travail est inférieur au nombre de nœuds dans un pool.</span><span class="sxs-lookup"><span data-stu-id="82015-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="82015-137">Elle s’applique également si [l’exécution de tâches simultanées](batch-parallel-node-tasks.md) est activée. Dans ce cas, certains nœuds restent inactifs si le nombre de tâches est inférieur au nombre total de tâches simultanées possibles.</span><span class="sxs-lookup"><span data-stu-id="82015-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="82015-138">Lorsque vous n’exécutez pas la tâche de préparation du travail sur des nœuds inactifs, vous pouvez réduire vos frais de transfert de données.</span><span class="sxs-lookup"><span data-stu-id="82015-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="82015-139">[JobPreparationTask][net_job_prep_cloudjob] diffère de [CloudPool.StartTask][pool_starttask] dans la mesure où JobPreparationTask s’exécute au début de chaque travail, tandis que StartTask s’exécute uniquement lorsqu’un nœud de calcul rejoint un pool ou redémarre.</span><span class="sxs-lookup"><span data-stu-id="82015-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="82015-140">tâche de validation du travail</span><span class="sxs-lookup"><span data-stu-id="82015-140">Job release task</span></span>
<span data-ttu-id="82015-141">Lorsqu'un travail est marqué comme terminé, la tâche de validation du travail s'exécute sur chaque nœud dans le pool ayant exécuté au moins une tâche.</span><span class="sxs-lookup"><span data-stu-id="82015-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="82015-142">Vous marquez un travail comme terminé en émettant une requête de fin.</span><span class="sxs-lookup"><span data-stu-id="82015-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="82015-143">Le service Batch définit ensuite l’état du travail sur *arrêt*, met fin à toutes les tâches actives ou en cours d’exécution associées au travail, puis exécute la tâche de validation du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="82015-144">Le travail passe ensuite à l'état *terminé* .</span><span class="sxs-lookup"><span data-stu-id="82015-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="82015-145">La suppression du travail exécute également la tâche de validation du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="82015-146">Toutefois, si un travail a déjà été arrêté, la tâche de validation n’est pas exécutée une seconde fois si ce travail est supprimé par la suite.</span><span class="sxs-lookup"><span data-stu-id="82015-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="82015-147">Tâches de préparation et de validation du travail avec Batch.NET</span><span class="sxs-lookup"><span data-stu-id="82015-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="82015-148">Pour utiliser une tâche de préparation du travail, affectez un objet [JobPreparationTask][net_job_prep] à la propriété [CloudJob.JobPreparationTask][net_job_prep_cloudjob] de votre travail.</span><span class="sxs-lookup"><span data-stu-id="82015-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="82015-149">De même, initialisez la propriété [JobReleaseTask][net_job_release] et affectez-la à la propriété [CloudJob.JobReleaseTask][net_job_prep_cloudjob] de votre travail pour définir la tâche de validation du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="82015-150">Dans cet extrait de code, `myBatchClient` est une instance de [BatchClient][net_batch_client], et `myPool` est un pool existant dans le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="82015-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="82015-151">Comme mentionné ci-dessus, la tâche de validation est exécutée lorsqu’un travail est arrêté ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="82015-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="82015-152">Pour arrêter un travail, utilisez [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="82015-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="82015-153">Pour supprimer un travail, utilisez [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="82015-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="82015-154">Généralement, vous arrêtez ou supprimez un travail lorsque les tâches de ce dernier sont terminées ou qu’un délai d’expiration que vous avez défini a été atteint.</span><span class="sxs-lookup"><span data-stu-id="82015-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="82015-155">Exemple de code sur GitHub</span><span class="sxs-lookup"><span data-stu-id="82015-155">Code sample on GitHub</span></span>
<span data-ttu-id="82015-156">Pour découvrir les tâches de préparation et de validation du travail en action, consultez l’exemple de projet [JobPrepRelease][job_prep_release_sample] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="82015-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="82015-157">Cette application de console effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="82015-157">This console application does the following:</span></span>

1. <span data-ttu-id="82015-158">Crée un pool avec deux « petits » nœuds.</span><span class="sxs-lookup"><span data-stu-id="82015-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="82015-159">Crée un travail avec des tâches de préparation du travail, de validation et standard.</span><span class="sxs-lookup"><span data-stu-id="82015-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="82015-160">Exécute la tâche de préparation du travail qui écrit d'abord l'ID de nœud dans un fichier texte dans le répertoire « partagé » d'un nœud.</span><span class="sxs-lookup"><span data-stu-id="82015-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="82015-161">Exécute une tâche sur chaque nœud qui écrit son ID de tâche dans le même fichier texte.</span><span class="sxs-lookup"><span data-stu-id="82015-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="82015-162">Lorsque toutes les tâches sont terminées (ou que le délai d'attente est atteint), imprime le contenu du fichier texte de chaque nœud dans la console.</span><span class="sxs-lookup"><span data-stu-id="82015-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="82015-163">Lorsque le travail est terminé, exécute la tâche de validation du travail pour supprimer le fichier du nœud.</span><span class="sxs-lookup"><span data-stu-id="82015-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="82015-164">Imprime les codes de sortie des tâches de préparation et de validation du travail pour chaque nœud sur lequel elles sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="82015-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="82015-165">Interrompt l'exécution pour permettre la confirmation de la suppression du pool et/ou du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="82015-166">Le résultat de l'exemple d'application ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="82015-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob to reach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="82015-167">En raison de la variabilité des heures de création et de démarrage des nœuds dans un nouveau pool (certains nœuds sont prêts pour les tâches avant d’autres), vous risquez d’obtenir un résultat différent.</span><span class="sxs-lookup"><span data-stu-id="82015-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="82015-168">En particulier, étant donné que les tâches s’exécutent rapidement, l’un des nœuds du pool peut exécuter l’ensemble des tâches du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="82015-169">Si cela se produit, vous remarquerez que les tâches de préparation et de validation du travail n’existent pas pour le nœud qui n’a exécuté aucune tâche.</span><span class="sxs-lookup"><span data-stu-id="82015-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="82015-170">Inspection des tâches de préparation et de validation du travail dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="82015-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="82015-171">Lorsque vous exécutez l’exemple d’application, vous pouvez utiliser le [Portail Azure][portal] pour visualiser les propriétés du travail et ses tâches, ou même télécharger le fichier texte partagé modifié par les tâches du travail.</span><span class="sxs-lookup"><span data-stu-id="82015-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="82015-172">La capture d’écran ci-après illustre le **panneau Tâches de préparation** du Portail Azure après une exécution de l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="82015-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="82015-173">Accédez aux propriétés *JobPrepReleaseSampleJob* une fois les tâches terminées (mais avant la suppression de votre travail et du pool), puis cliquez sur **Tâches de préparation** ou sur **Tâches de fin** pour en visualiser les propriétés.</span><span class="sxs-lookup"><span data-stu-id="82015-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Propriétés de préparation du travail dans le portail Azure][1]

## <a name="next-steps"></a><span data-ttu-id="82015-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82015-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="82015-176">Packages d’applications</span><span class="sxs-lookup"><span data-stu-id="82015-176">Application packages</span></span>
<span data-ttu-id="82015-177">Outre la tâche de préparation du travail, vous pouvez également utiliser la fonctionnalité [packages d’application](batch-application-packages.md) de Batch pour préparer des nœuds de calcul à l’exécution de tâches.</span><span class="sxs-lookup"><span data-stu-id="82015-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="82015-178">Cette fonctionnalité est particulièrement utile pour déployer des applications qui ne nécessitent pas de programme d’installation, des applications qui contiennent de nombreux fichiers (plus de 100) ou des applications qui requièrent un contrôle de version strict.</span><span class="sxs-lookup"><span data-stu-id="82015-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="82015-179">Installation d’applications et de données intermédiaires</span><span class="sxs-lookup"><span data-stu-id="82015-179">Installing applications and staging data</span></span>
<span data-ttu-id="82015-180">Le billet MSDN ci-après fournit une vue d’ensemble de différentes méthodes de préparation de vos nœuds à l’exécution des tâches :</span><span class="sxs-lookup"><span data-stu-id="82015-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="82015-181">[Installing applications and staging data on Batch compute nodes][forum_post] (Installation d’applications et de données intermédiaires sur les nœuds de calcul Batch)</span><span class="sxs-lookup"><span data-stu-id="82015-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="82015-182">Rédigé par l’un des membres de l’équipe Azure Batch, ce billet décrit plusieurs techniques que vous pouvez utiliser pour déployer des applications et des données sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="82015-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
