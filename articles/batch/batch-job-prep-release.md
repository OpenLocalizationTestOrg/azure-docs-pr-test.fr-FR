---
title: "aaaCreate tâches tooprepare travaux et complètes sur les nœuds de calcul - Azure Batch | Documents Microsoft"
description: "Utiliser les données au niveau de la tâche de préparation du toominimize de tâches transférer les nœuds de calcul de lot tooAzure et libérer des tâches de nettoyage du nœud à la fin de la tâche."
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
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="1b6e8-103">Exécuter des tâches de préparation et de validation du travail sur les nœuds de calcul Batch</span><span class="sxs-lookup"><span data-stu-id="1b6e8-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="1b6e8-104">Un travail Azure Batch nécessite souvent une certaine forme de préparation avant l’exécution de ses tâches, ainsi qu’une maintenance ultérieure une fois les tâches terminées.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="1b6e8-105">Que vous deviez nœuds de calcul du tooyour des données d’entrée de la tâche commune toodownload, ou télécharger tooAzure de données de sortie tâche stockage une fois hello travail terminé.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="1b6e8-106">Vous pouvez utiliser **préparation de la tâche** et **mise en production de la tâche** tâches tooperform ces opérations.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="1b6e8-107">En quoi consistent les tâches de préparation et de validation du travail ?</span><span class="sxs-lookup"><span data-stu-id="1b6e8-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="1b6e8-108">Avant l’exécution de tâches d’un projet, tâche de préparation du travail hello s’exécute sur tous les toorun planifiée nœuds de calcul au moins une tâche.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="1b6e8-109">Une fois le travail de hello est terminé, version de tâche hello s’exécute sur chaque nœud dans le pool de hello exécutée au moins une tâche.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="1b6e8-110">Comme avec les tâches de traitement normal, vous pouvez spécifier un toobe de ligne de commande appelé lorsqu’une tâche de préparation du ou des tâches de mise en production sont exécutée.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="1b6e8-111">Les tâches de préparation et de validation du travail offrent des fonctionnalités de tâche Batch courantes, telles que téléchargement de fichiers ([fichiers de ressources][net_job_prep_resourcefiles]), exécution avec élévation de privilèges, variables d’environnement personnalisées, durée d’exécution maximale, nombre de tentatives et période de rétention des fichiers.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="1b6e8-112">Bonjour les sections suivantes, vous allez apprendre comment toouse hello [JobPreparationTask] [ net_job_prep] et [JobReleaseTask] [ net_job_release] classes trouvées dans hello [Batch .NET] [ api_net] bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="1b6e8-113">Les tâches de préparation et de validation du travail sont particulièrement utiles dans les environnements de « pool partagé », dans lesquels un pool de nœuds de calcul persiste entre les exécutions d’un travail et est utilisé par de nombreux travaux.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="1b6e8-114">Lorsque toouse préparation du travail et tâches</span><span class="sxs-lookup"><span data-stu-id="1b6e8-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="1b6e8-115">Préparation du travail et les tâches de mise en production sont adaptées pour hello suivant situations :</span><span class="sxs-lookup"><span data-stu-id="1b6e8-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="1b6e8-116">**Télécharger les données de tâche communes**</span><span class="sxs-lookup"><span data-stu-id="1b6e8-116">**Download common task data**</span></span>

<span data-ttu-id="1b6e8-117">Traitements par lots nécessitent souvent un ensemble commun de données comme entrée pour les tâches du travail hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="1b6e8-118">Par exemple, dans les calculs de l’analyse des risques quotidiennes, les données de marché sont spécifiques à un projet, mais courantes tâches tooall travail de hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="1b6e8-119">Ces données de marché, souvent plusieurs gigaoctets, la taille doivent être téléchargé tooeach de nœud de calcul qu’une seule fois afin que toutes les tâches qui s’exécute sur le nœud de hello peuvent l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="1b6e8-120">Utilisez un **tâche de préparation** toodownload ce nœud tooeach de données avant l’exécution de hello du travail de hello's d’autres tâches.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="1b6e8-121">**Supprimer la sortie des travaux et des tâches**</span><span class="sxs-lookup"><span data-stu-id="1b6e8-121">**Delete job and task output**</span></span>

<span data-ttu-id="1b6e8-122">Dans un environnement « shared pool », où les nœuds de calcul d’un pool ne sont pas retirés entre les travaux, vous devrez peut-être les données entre les exécutions de la tâche toodelete.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="1b6e8-123">Vous devrez peut-être tooconserve espace disque sur les nœuds hello ou répondre aux stratégies de sécurité de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="1b6e8-124">Utilisez un **version tâche** toodelete les données qui ont été téléchargées par une tâche de préparation ou générées pendant l’exécution de tâches.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="1b6e8-125">**Rétention des journaux**</span><span class="sxs-lookup"><span data-stu-id="1b6e8-125">**Log retention**</span></span>

<span data-ttu-id="1b6e8-126">Vous souhaiterez peut-être tookeep une copie de fichiers journaux qui génèrent de vos tâches, ou peut-être les fichiers de vidage sur incident qui peuvent être générés par les applications ayant échouées.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="1b6e8-127">Utilisez un **version tâche** dans ces cas de toocompress et télécharger ce tooan données [Azure Storage] [ azure_storage] compte.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="1b6e8-128">Une autre façon toopersist journaux de travail et d’autres tâches sortie de données sont toouse hello [Conventions pour les fichiers par lots Azure](batch-task-output.md) bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="1b6e8-129">tâche de préparation du travail</span><span class="sxs-lookup"><span data-stu-id="1b6e8-129">Job preparation task</span></span>
<span data-ttu-id="1b6e8-130">Avant l’exécution de tâches d’un projet, Batch exécute la tâche de préparation du travail hello sur chaque nœud de calcul qui est planifiée toorun une tâche.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="1b6e8-131">Par défaut, hello service Batch attend hello travail préparation tâche toobe est terminée avant d’exécuter tooexecute de hello tâches planifiées sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="1b6e8-132">Toutefois, vous pouvez configurer le service de hello toowait pas.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="1b6e8-133">Si le nœud de hello redémarre, hello préparation tâche s’exécute à nouveau, mais vous pouvez également désactiver ce comportement.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="1b6e8-134">tâche de préparation du travail Hello est exécutée uniquement sur les nœuds qui sont planifiée toorun une tâche.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="1b6e8-135">Cela empêche l’exécution d’inutiles d’hello d’une tâche de préparation dans le cas où un nœud ne possède pas d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="1b6e8-136">Cela peut se produire lorsque le nombre de hello de tâches pour un travail est inférieur au nombre de hello de nœuds dans un pool de.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="1b6e8-137">Il s’applique également si [l’exécution de tâches simultanées](batch-parallel-node-tasks.md) est activé, qui laisse certains nœuds inactive si nombre de tâches hello est inférieur à tâches simultanées possibles total hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="1b6e8-138">En tâche de préparation du travail hello n’exécutant ne pas sur les nœuds inactifs, vous pouvez consacrer moins d’argent sur les frais de transfert de données.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="1b6e8-139">[JobPreparationTask] [ net_job_prep_cloudjob] diffère [CloudPool.StartTask] [ pool_starttask] dans la mesure où JobPreparationTask s’exécute au démarrage de hello de chaque travail, tandis que StartTask s’exécute uniquement lorsqu’un nœud de calcul joint tout d’abord un pool ou redémarre.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="1b6e8-140">tâche de validation du travail</span><span class="sxs-lookup"><span data-stu-id="1b6e8-140">Job release task</span></span>
<span data-ttu-id="1b6e8-141">Une fois qu’une tâche est marquée comme terminée, la mise en production tâche hello est exécutée sur chaque nœud dans le pool hello exécutées au moins une tâche.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="1b6e8-142">Vous marquez un travail comme terminé en émettant une requête de fin.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="1b6e8-143">Hello service Batch puis jeux hello état de la tâche trop*fin*, met fin à toutes les tâches actives ou en cours d’exécution associés au travail de hello et exécute la tâche de mise en production de projet hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="1b6e8-144">travail de Hello déplace ensuite toohello *terminé* état.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="1b6e8-145">Suppression de travail exécute également la mise en production tâche hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="1b6e8-146">Toutefois, si un travail a déjà été arrêté, tâche de mise en production hello n'est pas exécutée une deuxième fois si la tâche de hello est supprimé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="1b6e8-147">Tâches de préparation et de validation du travail avec Batch.NET</span><span class="sxs-lookup"><span data-stu-id="1b6e8-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="1b6e8-148">toouse une tâche de préparation du travail, affecter une [JobPreparationTask] [ net_job_prep] la tâche objet tooyour [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] propriété .</span><span class="sxs-lookup"><span data-stu-id="1b6e8-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="1b6e8-149">De même, initialiser un [JobReleaseTask] [ net_job_release] et l’assigner du travail tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] hello tooset de propriété tâche de mise en production de la tâche.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="1b6e8-150">Dans cet extrait de code, `myBatchClient` est une instance de [BatchClient][net_batch_client], et `myPool` est un pool existant au sein de hello compte Batch.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="1b6e8-151">Comme mentionné précédemment, la tâche de mise en production de hello est exécutée lorsqu’un travail est terminé ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="1b6e8-152">Pour arrêter un travail, utilisez [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="1b6e8-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="1b6e8-153">Pour supprimer un travail, utilisez [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="1b6e8-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="1b6e8-154">Généralement, vous arrêtez ou supprimez un travail lorsque les tâches de ce dernier sont terminées ou qu’un délai d’expiration que vous avez défini a été atteint.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="1b6e8-155">Exemple de code sur GitHub</span><span class="sxs-lookup"><span data-stu-id="1b6e8-155">Code sample on GitHub</span></span>
<span data-ttu-id="1b6e8-156">tâches de préparation et de la version de projet dans action, toosee extraire hello [JobPrepRelease] [ job_prep_release_sample] exemple de projet sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="1b6e8-157">Cette application de console hello suivant :</span><span class="sxs-lookup"><span data-stu-id="1b6e8-157">This console application does hello following:</span></span>

1. <span data-ttu-id="1b6e8-158">Crée un pool avec deux « petits » nœuds.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="1b6e8-159">Crée un travail avec des tâches de préparation du travail, de validation et standard.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="1b6e8-160">S’exécute hello tâche Préparation du travail, qui écrit d’abord le fichier texte tooa hello nœud ID dans le répertoire de « partagé » d’un nœud.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="1b6e8-161">Exécute une tâche sur chaque nœud qui écrit son toohello d’ID de tâche même fichier texte.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="1b6e8-162">Une fois que toutes les tâches sont terminées (ou du délai de hello), imprime le contenu hello console de toohello de fichier de texte de chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="1b6e8-163">À la fin du travail hello, exécute le fichier hello de toodelete la tâche hello travail version à partir du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="1b6e8-164">Hello d’imprime les codes de préparation du travail hello de sortie et libérer des tâches pour chaque nœud sur lequel ils exécutée.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="1b6e8-165">Confirmation de tooallow suspend l’exécution de suppression de travail et/ou de pool.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="1b6e8-166">Sortie de l’exemple d’application hello est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b6e8-166">Output from hello sample application is similar toohello following:</span></span>

```
Attempting toocreate pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
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

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> <span data-ttu-id="1b6e8-167">Échéance toohello variable création et heure de début de nœuds dans un nouveau pool (certains nœuds sont prêts pour les tâches avant les autres), vous pouvez voir une sortie différente.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="1b6e8-168">Plus précisément, étant donné que les tâches de hello s’achèvent rapidement, un des nœuds du pool hello peut exécuter toutes les tâches du travail hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="1b6e8-169">Si cela se produit, vous pouvez remarquer que hello préparation du travail et de tâches n’existent pas pour le nœud hello exécutées aucune tâche.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="1b6e8-170">Inspectez la préparation du travail et des tâches de mise en production de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1b6e8-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="1b6e8-171">Lorsque vous exécutez exemple d’application hello, vous pouvez utiliser hello [portail Azure] [ portal] tooview hello les propriétés du travail de hello et ses tâches, ou même télécharger de fichier partagé texte hello est modifié par les tâches du travail hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="1b6e8-172">Hello capture d’écran ci-dessous montre hello **Panneau de tâches de préparation** Bonjour Azure portal après une exécution de l’exemple d’application hello.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="1b6e8-173">Accédez toohello *JobPrepReleaseSampleJob* propriétés une fois les tâches terminées (mais avant de supprimer votre travail et le pool) et cliquez sur **tâches de préparation** ou **detâches** tooview leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Propriétés de préparation du travail dans le portail Azure][1]

## <a name="next-steps"></a><span data-ttu-id="1b6e8-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1b6e8-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="1b6e8-176">packages d’application</span><span class="sxs-lookup"><span data-stu-id="1b6e8-176">Application packages</span></span>
<span data-ttu-id="1b6e8-177">Dans la tâche de préparation du travail de toohello de plus, vous pouvez également utiliser hello [les packages d’applications](batch-application-packages.md) nœuds pour l’exécution de la tâche de calcul de la fonctionnalité de traitement par lots tooprepare.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="1b6e8-178">Cette fonctionnalité est particulièrement utile pour déployer des applications qui ne nécessitent pas de programme d’installation, des applications qui contiennent de nombreux fichiers (plus de 100) ou des applications qui requièrent un contrôle de version strict.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="1b6e8-179">Installation d’applications et de données intermédiaires</span><span class="sxs-lookup"><span data-stu-id="1b6e8-179">Installing applications and staging data</span></span>
<span data-ttu-id="1b6e8-180">Le billet MSDN ci-après fournit une vue d’ensemble de différentes méthodes de préparation de vos nœuds à l’exécution des tâches :</span><span class="sxs-lookup"><span data-stu-id="1b6e8-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="1b6e8-181">[Installing applications and staging data on Batch compute nodes][forum_post] (Installation d’applications et de données intermédiaires sur les nœuds de calcul Batch)</span><span class="sxs-lookup"><span data-stu-id="1b6e8-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="1b6e8-182">Écrit par un des membres de l’équipe Azure Batch hello, il présente plusieurs techniques que vous pouvez utiliser des nœuds de toocompute des applications et des données toodeploy.</span><span class="sxs-lookup"><span data-stu-id="1b6e8-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

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
