---
title: "Exécuter des applications MPI avec des tâches multi-instances - Azure Batch | Microsoft Docs"
description: "Découvrez comment exécuter des applications MPI (Message Passing Interface) en utilisant des tâches de type multi-instances dans Azure Batch."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="200fc-103">Utiliser les tâches multi-instances pour exécuter des applications MPI (Message Passing Interface) dans Batch</span><span class="sxs-lookup"><span data-stu-id="200fc-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="200fc-104">Les tâches multi-instances vous permettent d’exécuter une tâche Azure Batch sur plusieurs nœuds de calcul simultanément.</span><span class="sxs-lookup"><span data-stu-id="200fc-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="200fc-105">Ces tâches permettent de mettre en œuvre des scénarios de calcul haute performance tels que les applications MPI (Message Passing Interface) dans Batch.</span><span class="sxs-lookup"><span data-stu-id="200fc-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="200fc-106">Dans cet article, vous découvrez comment exécuter des tâches multi-instances à l’aide de la bibliothèque [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="200fc-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="200fc-107">Bien que les exemples de cet article portent sur Batch .NET, MS-MPI et les nœuds de calcul Windows, les concepts de tâches multi-instances présentés ici s’appliquent à d’autres plateformes et technologies (Python et Intel MPI sur des nœuds Linux, par exemple).</span><span class="sxs-lookup"><span data-stu-id="200fc-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="200fc-108">Présentation des tâches multi-instances</span><span class="sxs-lookup"><span data-stu-id="200fc-108">Multi-instance task overview</span></span>
<span data-ttu-id="200fc-109">Dans Azure Batch, chaque tâche est normalement exécutée sur un nœud de calcul unique : vous soumettez plusieurs tâches à un travail, et le service Azure Batch planifie l’exécution de chacune d’entre elles sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="200fc-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="200fc-110">Toutefois, en configurant les **paramètres multi-instances** d’une tâche, vous pouvez indiquer à la place à Batch de créer une tâche principale et quelques tâches subordonnées qui sont ensuite exécutées sur plusieurs nœuds.</span><span class="sxs-lookup"><span data-stu-id="200fc-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="200fc-111">![Présentation des tâches multi-instances][1]</span><span class="sxs-lookup"><span data-stu-id="200fc-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="200fc-112">Lorsque vous envoyez à un travail une tâche dotée de paramètres multi-instances, Azure Batch exécute plusieurs étapes uniques aux tâches multi-instances :</span><span class="sxs-lookup"><span data-stu-id="200fc-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="200fc-113">Le service Batch crée une **tâche principale** et plusieurs **tâches subordonnées** selon les paramètres multi-instances.</span><span class="sxs-lookup"><span data-stu-id="200fc-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="200fc-114">Le nombre total de tâches (tâche principale, ainsi que toutes les tâches subordonnées) correspond au nombre **d’instances** (nœuds de calcul) que vous spécifiez dans les paramètres multi-instances.</span><span class="sxs-lookup"><span data-stu-id="200fc-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="200fc-115">Batch désigne l’un des nœuds de calcul comme **principal** et planifie la tâche principale à exécuter sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="200fc-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="200fc-116">Il planifie les tâches subordonnées à exécuter sur le reste des nœuds de calcul alloués à la tâche multi-instance, une tâche subordonnée par nœud.</span><span class="sxs-lookup"><span data-stu-id="200fc-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="200fc-117">La tâche principale et toutes les tâches subordonnées téléchargent les **fichiers de ressources communs** que vous indiquez dans les paramètres multi-instances.</span><span class="sxs-lookup"><span data-stu-id="200fc-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="200fc-118">Une fois les fichiers de ressources communs téléchargés, la tâche principale et les tâches subordonnées exécutent la **commande de coordination** que vous indiquez dans les paramètres multi-instances.</span><span class="sxs-lookup"><span data-stu-id="200fc-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="200fc-119">La commande de coordination sert généralement à préparer des nœuds en vue de l’exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="200fc-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="200fc-120">Cela peut impliquer de démarrer les services d’arrière-plan (par exemple `smpd.exe` de [Microsoft MPI][msmpi_msdn]) et de vérifier que les nœuds sont prêts à traiter les messages entre nœuds.</span><span class="sxs-lookup"><span data-stu-id="200fc-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="200fc-121">La tâche principale exécute la **commande d’application** du nœud principal *une fois que* la tâche principale et toutes les tâches subordonnées ont fini d’exécuter la commande de coordination.</span><span class="sxs-lookup"><span data-stu-id="200fc-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="200fc-122">La commande d’application est la ligne de commande de la tâche multi-instances. Elle est exécutée uniquement par la tâche principale.</span><span class="sxs-lookup"><span data-stu-id="200fc-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="200fc-123">Dans une solution basée sur [MS-MPI][msmpi_msdn], c’est là où vous exécutez votre application prenant en charge MPI au moyen du fichier `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="200fc-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="200fc-124">Même si elle est différente d’un point de vue fonctionnel, la « tâche multi-instances » n’est pas un type de tâche unique comme [StartTask][net_starttask] ou [JobPreparationTask][net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="200fc-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="200fc-125">La tâche multi-instances est simplement une tâche Batch standard ([CloudTask][net_task] dans Batch .NET) dont les paramètres multi-instances ont été configurés.</span><span class="sxs-lookup"><span data-stu-id="200fc-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="200fc-126">Dans cet article, nous parlons de **tâche multi-instances**.</span><span class="sxs-lookup"><span data-stu-id="200fc-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="200fc-127">Configuration requise pour les tâches multi-instances</span><span class="sxs-lookup"><span data-stu-id="200fc-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="200fc-128">Les tâches multi-instances nécessitent un pool avec **communication entre les nœuds activée** et **exécution de tâches simultanées désactivée**.</span><span class="sxs-lookup"><span data-stu-id="200fc-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="200fc-129">Pour désactiver l’exécution des tâches simultanées, définissez la propriété [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) sur 1.</span><span class="sxs-lookup"><span data-stu-id="200fc-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="200fc-130">Cet extrait de code montre comment créer un pool pour les tâches multi-instances à l’aide de la bibliothèque Batch .NET.</span><span class="sxs-lookup"><span data-stu-id="200fc-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="200fc-131">Si vous essayez d’exécuter une tâche multi-instances dans un pool dont la communication entre les nœuds a été désactivée ou avec une valeur *maxTasksPerNode* supérieure à 1, la tâche ne sera jamais planifiée et restera indéfiniment à l’état « actif ».</span><span class="sxs-lookup"><span data-stu-id="200fc-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="200fc-132">Les tâches multi-instances peuvent s’exécuter uniquement sur des nœuds dans des pools créés après le 14 décembre 2015.</span><span class="sxs-lookup"><span data-stu-id="200fc-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="200fc-133">Utiliser une tâche de début pour installer MPI</span><span class="sxs-lookup"><span data-stu-id="200fc-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="200fc-134">Pour exécuter des applications MPI avec une tâche multi-instances, vous devez d’abord installer une implémentation MPI (MS-MPI ou Intel MPI par exemple) sur les nœuds de calcul du pool.</span><span class="sxs-lookup"><span data-stu-id="200fc-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="200fc-135">C’est là une bonne occasion d’utiliser une tâche [StartTask][net_starttask] qui s’exécute à chaque fois qu’un nœud rejoint un pool ou est redémarré.</span><span class="sxs-lookup"><span data-stu-id="200fc-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="200fc-136">Cet extrait de code crée une tâche StartTask qui spécifie le package d’installation de MS-MPI comme un [fichier de ressources][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="200fc-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="200fc-137">La ligne de commande de la tâche de début est exécutée une fois le fichier de ressources téléchargé sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="200fc-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="200fc-138">Dans ce cas, la ligne de commande effectue une installation sans assistance de MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="200fc-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="200fc-139">Accès direct à la mémoire à distance (RDMA)</span><span class="sxs-lookup"><span data-stu-id="200fc-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="200fc-140">Lorsque vous utilisez une [Taille compatible RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) comme A9 pour les nœuds de calcul dans votre pool Batch, votre application MPI peut tirer parti du réseau d’accès direct à la mémoire à distance (RDMA) haute performance d’Azure.</span><span class="sxs-lookup"><span data-stu-id="200fc-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="200fc-141">Recherchez les tailles spécifiées comme « compatibles RDMA » dans les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="200fc-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="200fc-142">Pools **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="200fc-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="200fc-143">[Tailles de services cloud](../cloud-services/cloud-services-sizes-specs.md) (Windows uniquement)</span><span class="sxs-lookup"><span data-stu-id="200fc-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="200fc-144">Pools **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="200fc-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="200fc-145">[Tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="200fc-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="200fc-146">[Tailles des machines virtuelles dans Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="200fc-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="200fc-147">Pour tirer parti de RDMA sur des [nœuds de calcul Linux](batch-linux-nodes.md), vous devez utiliser **Intel MPI** sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="200fc-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="200fc-148">Pour plus d’informations sur les pools CloudServiceConfiguration et VirtualMachineConfiguration, consultez la section Pool de la [vue d’ensemble des fonctionnalités Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="200fc-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="200fc-149">Créer une tâche multi-instances avec Batch.NET</span><span class="sxs-lookup"><span data-stu-id="200fc-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="200fc-150">Maintenant que nous avons abordé les exigences du pool et l’installation du package MPI, nous allons créer la tâche multi-instances.</span><span class="sxs-lookup"><span data-stu-id="200fc-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="200fc-151">Dans cet extrait de code, nous créons une [CloudTask][net_task] standard, puis nous configurons sa propriété [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="200fc-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="200fc-152">Comme mentionné ci-dessus, la tâche multi-instances n’est pas un type de tâche distinct, mais une tâche Batch standard configurée avec des paramètres multi-instances.</span><span class="sxs-lookup"><span data-stu-id="200fc-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="200fc-153">Tâche principale et tâches subordonnées</span><span class="sxs-lookup"><span data-stu-id="200fc-153">Primary task and subtasks</span></span>
<span data-ttu-id="200fc-154">Lorsque vous créez les paramètres multi-instances d’une tâche, vous indiquez le nombre de nœuds de calcul qui vont exécuter la tâche.</span><span class="sxs-lookup"><span data-stu-id="200fc-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="200fc-155">Lorsque vous soumettez la tâche à un travail, le service Batch crée une tâche **principale** et suffisamment de **tâches subordonnées** pour le nombre de nœuds indiqué.</span><span class="sxs-lookup"><span data-stu-id="200fc-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="200fc-156">Ces tâches se voient affecter un identifiant entier allant de 0 à *numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="200fc-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="200fc-157">La tâche dont l’identifiant est 0 est la tâche principale, tandis que tous les autres identifiants correspondent aux tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="200fc-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="200fc-158">Par exemple, si vous créez les paramètres multi-instances suivants d’une tâche, la tâche principale a pour identifiant 0 et les tâches subordonnées, des identifiants allant de 1 à 9.</span><span class="sxs-lookup"><span data-stu-id="200fc-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="200fc-159">Nœud principal</span><span class="sxs-lookup"><span data-stu-id="200fc-159">Master node</span></span>
<span data-ttu-id="200fc-160">Quand vous soumettez une tâche multi-instance, le service Batch désigne l’un des nœuds de calcul comme nœud « principal » et planifie la tâche principale à exécuter sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="200fc-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="200fc-161">Les tâches subordonnées sont planifiées pour s’exécuter sur le reste des nœuds alloués à la tâche multi-instance.</span><span class="sxs-lookup"><span data-stu-id="200fc-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="200fc-162">commande de coordination</span><span class="sxs-lookup"><span data-stu-id="200fc-162">Coordination command</span></span>
<span data-ttu-id="200fc-163">La **commande de coordination** est exécutée à la fois par la tâche principale et les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="200fc-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="200fc-164">L’appel de la commande de coordination bloque : Azure Batch exécute uniquement la commande d’application lorsque la commande de coordination a été renvoyée avec succès pour toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="200fc-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="200fc-165">Par conséquent, la commande de coordination doit démarrer tous les services d’arrière-plan requis, vérifier qu’ils sont prêts à être utilisés, puis se fermer.</span><span class="sxs-lookup"><span data-stu-id="200fc-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="200fc-166">Par exemple, cette commande coordination pour une solution qui utilise la version 7 de MS-MPI démarre le service SMPD sur le nœud, puis se ferme :</span><span class="sxs-lookup"><span data-stu-id="200fc-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="200fc-167">Notez l’utilisation de `start` dans cette commande de coordination.</span><span class="sxs-lookup"><span data-stu-id="200fc-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="200fc-168">Cela est nécessaire, car l’application `smpd.exe` n’est pas immédiatement renvoyée après l’exécution.</span><span class="sxs-lookup"><span data-stu-id="200fc-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="200fc-169">Sans l’utilisation de la commande [start][cmd_start], cette commande de coordination ne serait pas renvoyée et bloquerait par conséquent l’exécution de la commande d’application.</span><span class="sxs-lookup"><span data-stu-id="200fc-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="200fc-170">Commande d’application</span><span class="sxs-lookup"><span data-stu-id="200fc-170">Application command</span></span>
<span data-ttu-id="200fc-171">Une fois que la tâche principale et toutes les tâches subordonnées ont terminé d’exécuter la commande de coordination, la ligne de commande de la tâche multi-instances est exécutée par la tâche principale *uniquement*.</span><span class="sxs-lookup"><span data-stu-id="200fc-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="200fc-172">Nous appelons cette ligne de commande la **commande d’application** pour la différencier de la commande de coordination.</span><span class="sxs-lookup"><span data-stu-id="200fc-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="200fc-173">Pour les applications MS-MPI, utilisez la commande d’application pour exécuter votre application MPI avec `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="200fc-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="200fc-174">Par exemple, voici une commande d’application pour une solution qui utilise la version 7 de MS-MPI :</span><span class="sxs-lookup"><span data-stu-id="200fc-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="200fc-175">Étant donné que `mpiexec.exe` de MS-MPI utilise la variable `CCP_NODES` par défaut (voir [Variables d’environnement](#environment-variables)), l’exemple de ligne de commande d’application ci-dessus l’exclut.</span><span class="sxs-lookup"><span data-stu-id="200fc-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="200fc-176">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="200fc-176">Environment variables</span></span>
<span data-ttu-id="200fc-177">Batch crée plusieurs [variables d’environnement][msdn_env_var] propres aux tâches multi-instances sur les nœuds de calcul affectés à une tâche multi-instance.</span><span class="sxs-lookup"><span data-stu-id="200fc-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="200fc-178">Vos lignes de commande d’application et de coordination peuvent référencer ces variables d’environnement, de même que les scripts et les programmes qu’elles exécutent.</span><span class="sxs-lookup"><span data-stu-id="200fc-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="200fc-179">Les variables d’environnement suivantes sont créées par le service Batch pour les tâches multi-instances :</span><span class="sxs-lookup"><span data-stu-id="200fc-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="200fc-180">Pour plus d’informations sur les variables d’environnement des nœuds de calcul Batch, notamment leur contenu et leur visibilité, consultez la page [Variables d’environnement des nœuds de calcul][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="200fc-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="200fc-181">L’exemple de code Batch Linux MPI contient un exemple d’utilisation de plusieurs d’entre elles.</span><span class="sxs-lookup"><span data-stu-id="200fc-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="200fc-182">Le script Batch [coordination-cmd][coord_cmd_example] télécharge les fichiers d’application et d’entrée communs sur le Stockage Azure, autorise le partage Network File System (NFS) sur le nœud principal et configure les autres nœuds alloués à la tâche multi-instance en tant que clients NFS.</span><span class="sxs-lookup"><span data-stu-id="200fc-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="200fc-183">Fichiers de ressources</span><span class="sxs-lookup"><span data-stu-id="200fc-183">Resource files</span></span>
<span data-ttu-id="200fc-184">Il existe deux ensembles de fichiers de ressources à prendre en compte pour les tâches multi-instances : les **fichiers de ressources communs** que *toutes* les tâches téléchargent (tâche principale et tâches subordonnées) et les **fichiers de ressources** indiqués pour la tâche multi-instances elle-même que *seule la tâche principale* télécharge.</span><span class="sxs-lookup"><span data-stu-id="200fc-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="200fc-185">Vous pouvez indiquer un ou plusieurs **fichiers de ressources communs** dans les paramètres multi-instances d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="200fc-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="200fc-186">Ces fichiers de ressources communs sont téléchargés à partir du [Stockage Azure](../storage/common/storage-introduction.md) dans le **répertoire partagé de tâche** de chaque nœud, par la tâche principale et toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="200fc-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="200fc-187">Vous pouvez accéder au répertoire partagé de la tâche à partir de l’application et des lignes de commande de coordination à l’aide de la variable d’environnement `AZ_BATCH_TASK_SHARED_DIR` .</span><span class="sxs-lookup"><span data-stu-id="200fc-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="200fc-188">Le chemin d’accès `AZ_BATCH_TASK_SHARED_DIR` est identique sur tous les nœuds alloués à la tâche multi-instance. Vous pouvez par conséquent partager une commande de coordination unique entre la tâche principale et toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="200fc-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="200fc-189">Batch ne « partage » pas le répertoire dans le sens de l’accès à distance, mais vous pouvez l’utiliser comme point de montage ou de partage comme cela a été mentionné dans le conseil sur les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="200fc-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="200fc-190">Les fichiers de ressources que vous spécifiez pour la tâche multi-instance sont téléchargés dans le répertoire de travail de la tâche, `AZ_BATCH_TASK_WORKING_DIR` par défaut.</span><span class="sxs-lookup"><span data-stu-id="200fc-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="200fc-191">Comme nous l’avons mentionné, contrairement aux fichiers de ressources communs, seule la tâche principale télécharge les fichiers de ressources spécifiés pour la tâche multi-instances.</span><span class="sxs-lookup"><span data-stu-id="200fc-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="200fc-192">Veillez à toujours utiliser les variables d’environnement `AZ_BATCH_TASK_SHARED_DIR` et `AZ_BATCH_TASK_WORKING_DIR` pour faire référence à ces répertoires dans vos lignes de commande.</span><span class="sxs-lookup"><span data-stu-id="200fc-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="200fc-193">N’essayez pas de construire les chemins d’accès manuellement.</span><span class="sxs-lookup"><span data-stu-id="200fc-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="200fc-194">Durée de vie de la tâche</span><span class="sxs-lookup"><span data-stu-id="200fc-194">Task lifetime</span></span>
<span data-ttu-id="200fc-195">La durée de vie de la tâche principale contrôle la durée de vie de la tâche multi-instances tout entière.</span><span class="sxs-lookup"><span data-stu-id="200fc-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="200fc-196">Lorsque la tâche principale s’arrête, toutes les tâches subordonnées s’arrêtent aussi.</span><span class="sxs-lookup"><span data-stu-id="200fc-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="200fc-197">Le code de sortie de la tâche principale est le code de sortie de la tâche. Il est donc utilisé pour déterminer la réussite ou l’échec de la tâche pour toutes nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="200fc-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="200fc-198">Si l’une des tâches subordonnées échoue, par exemple en se fermant avec un code de retour différent de zéro, la tâche multi-instances tout entière échoue.</span><span class="sxs-lookup"><span data-stu-id="200fc-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="200fc-199">La tâche multi-instances s’arrête ensuite puis reprend, dans la limite du nombre de nouvelles tentatives défini.</span><span class="sxs-lookup"><span data-stu-id="200fc-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="200fc-200">Quand vous supprimez une tâche multi-instances, la tâche principale et toutes les tâches subordonnées sont également supprimées par le service Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="200fc-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="200fc-201">Tous les répertoires des tâches subordonnées et leurs fichiers sont supprimés des nœuds de calcul, à l’image d’une tâche standard.</span><span class="sxs-lookup"><span data-stu-id="200fc-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="200fc-202">Les [TaskConstraints][net_taskconstraints] d’une tâche multi-instances, par exemple les propriétés [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock] et [RetentionTime][net_taskconstraint_retention], sont honorées en l’état pour une tâche standard, puis s’appliquent à la tâche principale et à toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="200fc-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="200fc-203">Toutefois, si vous modifiez la propriété [RetentionTime][net_taskconstraint_retention] après l’ajout de la tâche multi-instances au travail, cette modification s’applique uniquement à la tâche principale.</span><span class="sxs-lookup"><span data-stu-id="200fc-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="200fc-204">Toutes les tâches subordonnées continuent d’utiliser la propriété [RetentionTime][net_taskconstraint_retention] d’origine.</span><span class="sxs-lookup"><span data-stu-id="200fc-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="200fc-205">Une liste des tâches récentes d’un nœud de calcul reflète l’identifiant d’une tâche subordonnée si la tâche récente faisait partie d’une tâche multi-instances.</span><span class="sxs-lookup"><span data-stu-id="200fc-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="200fc-206">Obtenir des informations sur les tâches subordonnées</span><span class="sxs-lookup"><span data-stu-id="200fc-206">Obtain information about subtasks</span></span>
<span data-ttu-id="200fc-207">Pour obtenir plus d’informations sur les tâches subordonnées à l’aide de la bibliothèque Batch.NET, appelez la méthode [CloudTask.ListSubtasks][net_task_listsubtasks].</span><span class="sxs-lookup"><span data-stu-id="200fc-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="200fc-208">Cette méthode renvoie des informations sur toutes les tâches subordonnées, ainsi que sur le nœud de calcul qui a exécuté les tâches.</span><span class="sxs-lookup"><span data-stu-id="200fc-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="200fc-209">À partir de ces informations, vous pouvez déterminer le répertoire racine de chaque tâche subordonnée, l’identifiant du pool, son état actuel, le code de sortie, etc.</span><span class="sxs-lookup"><span data-stu-id="200fc-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="200fc-210">Utilisez ces informations en même temps que la méthode [PoolOperations.GetNodeFile][poolops_getnodefile] pour obtenir les fichiers de la tâche subordonnée.</span><span class="sxs-lookup"><span data-stu-id="200fc-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="200fc-211">Notez que cette méthode ne renvoie pas d’informations pour la tâche principale (identifiant 0).</span><span class="sxs-lookup"><span data-stu-id="200fc-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="200fc-212">Sauf indication contraire, les méthodes Batch.NET qui interviennent sur la tâche multi-instances [CloudTask][net_task] elle-même s’appliquent *uniquement* à la tâche principale.</span><span class="sxs-lookup"><span data-stu-id="200fc-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="200fc-213">Par exemple, lorsque vous appelez la méthode [CloudTask.ListNodeFiles][net_task_listnodefiles] sur une tâche multi-instances, seuls les fichiers de la tâche principale sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="200fc-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="200fc-214">L’extrait de code suivant montre comment obtenir des informations sur les tâches subordonnées et comment demander le contenu du fichier à partir des nœuds sur lesquels elles sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="200fc-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="200fc-215">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="200fc-215">Code sample</span></span>
<span data-ttu-id="200fc-216">L’exemple de code [MultiInstanceTasks][github_mpi] sur GitHub montre comment une tâche multi-instances permet d’exécuter une application [MS-MPI][msmpi_msdn] sur des nœuds de calcul Batch.</span><span class="sxs-lookup"><span data-stu-id="200fc-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="200fc-217">Pour exécuter l’exemple, suivez les étapes de [préparation](#preparation) et d’[exécution](#execution).</span><span class="sxs-lookup"><span data-stu-id="200fc-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="200fc-218">Préparation</span><span class="sxs-lookup"><span data-stu-id="200fc-218">Preparation</span></span>
1. <span data-ttu-id="200fc-219">Suivez les deux premières étapes dans [How to compile and run a simple MS-MPI program][msmpi_howto] (Comment compiler et exécuter un simple programme MS-MPI).</span><span class="sxs-lookup"><span data-stu-id="200fc-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="200fc-220">Ces étapes permettent de satisfaire les conditions requises pour l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="200fc-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="200fc-221">Créez une version de *mise en production* de l’exemple de programme MPI [MPIHelloWorld][helloworld_proj].</span><span class="sxs-lookup"><span data-stu-id="200fc-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="200fc-222">Il s’agit du programme qui sera exécuté par la tâche multi-instances sur des nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="200fc-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="200fc-223">Créez un fichier .zip contenant `MPIHelloWorld.exe` (que vous avez créé à l’étape 2) et `MSMpiSetup.exe` (que vous avez téléchargé à l’étape 1).</span><span class="sxs-lookup"><span data-stu-id="200fc-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="200fc-224">À l’étape suivante, vous allez télécharger ce fichier .zip en tant que package d’application.</span><span class="sxs-lookup"><span data-stu-id="200fc-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="200fc-225">Utilisez le [Portail Azure][portal] pour créer une [application](batch-application-packages.md) Batch appelée « MPIHelloWorld » et spécifiez le fichier .zip que vous avez créé à l’étape précédente en tant que version « 1.0 » du package d’application.</span><span class="sxs-lookup"><span data-stu-id="200fc-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="200fc-226">Pour plus d’informations, consultez [Téléchargement et gestion des applications](batch-application-packages.md#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="200fc-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="200fc-227">Créez une version de *mise en production* de `MPIHelloWorld.exe` afin que vous ne soyez pas obligé d’inclure toutes les dépendances supplémentaires (par exemple `msvcp140d.dll` ou `vcruntime140d.dll`) dans votre package d’application.</span><span class="sxs-lookup"><span data-stu-id="200fc-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="200fc-228">Exécution</span><span class="sxs-lookup"><span data-stu-id="200fc-228">Execution</span></span>
1. <span data-ttu-id="200fc-229">Téléchargez les [exemples Azure Batch][github_samples_zip] à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="200fc-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="200fc-230">Ouvrez la **solution** MultiInstanceTasks dans Visual Studio 2015 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="200fc-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="200fc-231">Le fichier de solution `MultiInstanceTasks.sln` se trouve à cet emplacement :</span><span class="sxs-lookup"><span data-stu-id="200fc-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="200fc-232">Entrez vos informations d’identification de compte Batch et Stockage dans `AccountSettings.settings` dans le projet **Microsoft.Azure.Batch.Samples.Common**.</span><span class="sxs-lookup"><span data-stu-id="200fc-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="200fc-233">**Générez et exécutez** la solution MultiInstanceTasks pour exécuter l’exemple d’application MPI sur des nœuds de calcul dans un pool Batch.</span><span class="sxs-lookup"><span data-stu-id="200fc-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="200fc-234">*Facultatif*: utilisez le [Portail Azure][portal] ou [Batch Explorer][batch_explorer] pour examiner les exemples de pool, de travail et de tâche (« MultiInstanceSamplePool », « MultiInstanceSampleJob », « MultiInstanceSampleTask ») avant de supprimer les ressources.</span><span class="sxs-lookup"><span data-stu-id="200fc-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="200fc-235">Vous pouvez télécharger [Visual Studio Community][visual_studio] gratuitement si vous n’avez pas Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="200fc-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="200fc-236">Le résultat de `MultiInstanceTasks.exe` ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="200fc-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="200fc-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="200fc-237">Next steps</span></span>
* <span data-ttu-id="200fc-238">Le blog de l’équipe Microsoft HPC et Azure Batch présente [Prise en charge MPI pour Linux sur Azure Batch][blog_mpi_linux], et inclut des informations sur l’utilisation de [OpenFOAM][openfoam] avec Batch.</span><span class="sxs-lookup"><span data-stu-id="200fc-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="200fc-239">Vous trouverez des exemples de code Python dans [l’exemple OpenFOAM sur GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="200fc-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="200fc-240">Découvrez comment [créer des pools de nœuds de calcul Linux](batch-linux-nodes.md) à utiliser dans vos solutions MPI Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="200fc-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Présentation multi-instances"
