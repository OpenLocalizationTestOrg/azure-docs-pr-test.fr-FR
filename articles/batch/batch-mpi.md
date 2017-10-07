---
title: "les instances multiples aaaUse tâches des applications MPI toorun - Azure Batch | Documents Microsoft"
description: "Découvrez comment les applications tooexecute Interface MPI (Message Passing) à l’aide de la tâche d’instances multiples hello tapez dans Azure Batch."
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
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="7e3af-103">Utiliser les applications multi-instance tâches toorun Interface MPI (Message Passing) dans le lot</span><span class="sxs-lookup"><span data-stu-id="7e3af-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="7e3af-104">Instances multiples tâches permettent toorun une tâche de traitement par lots Azure sur plusieurs nœuds de calcul simultanément.</span><span class="sxs-lookup"><span data-stu-id="7e3af-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="7e3af-105">Ces tâches permettent de mettre en œuvre des scénarios de calcul haute performance tels que les applications MPI (Message Passing Interface) dans Batch.</span><span class="sxs-lookup"><span data-stu-id="7e3af-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="7e3af-106">Dans cet article, vous apprendrez comment les tâches de plusieurs instances de tooexecute à l’aide de hello [Batch .NET] [ api_net] bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="7e3af-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="7e3af-107">Tandis que les exemples de hello dans cet article se concentrent sur .NET de traitement par lots, MS-MPI, et les nœuds de calcul de Windows, concepts de tâche hello multi-instance présentées ici sont applicables tooother plateformes et les technologies (Python et MPI Intel des nœuds Linux, par exemple).</span><span class="sxs-lookup"><span data-stu-id="7e3af-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="7e3af-108">Présentation des tâches multi-instances</span><span class="sxs-lookup"><span data-stu-id="7e3af-108">Multi-instance task overview</span></span>
<span data-ttu-id="7e3af-109">Dans le traitement par lots, chaque tâche est normalement exécutée sur un nœud de calcul unique--vous soumettez le travail de plusieurs tâches tooa et hello service Batch planifie chaque tâche d’exécution sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="7e3af-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="7e3af-110">Toutefois, en configurant d’une tâche **paramètres d’instances multiples**, vous indiquez le lot tooinstead créer une tâche principale et plusieurs tâches subordonnées qui sont ensuite exécutées sur plusieurs nœuds.</span><span class="sxs-lookup"><span data-stu-id="7e3af-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="7e3af-111">![Présentation des tâches multi-instances][1]</span><span class="sxs-lookup"><span data-stu-id="7e3af-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="7e3af-112">Lorsque vous soumettez une tâche avec la tâche d’instances multiples paramètres tooa, lot effectue plusieurs tâches de toomulti-instance unique de comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e3af-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="7e3af-113">Hello service Batch crée un **principal** et plusieurs **sous-tâches** en fonction des paramètres d’instances multiples hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="7e3af-114">Nombre total de Hello de tâches (principales ainsi que toutes les tâches subordonnées) correspond au nombre de hello de **instances** (nœuds de calcul) vous spécifiez dans les paramètres de plusieurs instances de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="7e3af-115">Lot désigne l’un des hello nœuds de calcul en tant que hello **master**, et les planifications hello tooexecute tâche principale sur le contrôleur de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="7e3af-116">Il planifie tooexecute des sous-tâches hello sur reste hello de tâche hello calcul nœuds toohello allouée à plusieurs instances, une sous-tâche par nœud.</span><span class="sxs-lookup"><span data-stu-id="7e3af-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="7e3af-117">téléchargement Hello primaire et toutes les tâches subordonnées **des fichiers de ressources communes** vous spécifiez dans les paramètres de plusieurs instances de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="7e3af-118">Une fois que les fichiers de ressources communs hello ont été téléchargées, hello principal et les tâches subordonnées exécutent hello **commande de coordination** vous spécifiez dans les paramètres de plusieurs instances de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="7e3af-119">commande de coordination Hello est nœuds tooprepare généralement utilisées pour exécuter la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="7e3af-120">Cela peut inclure le démarrage des services d’arrière-plan (tel que [Microsoft MPI][msmpi_msdn]de `smpd.exe`) et en vérifiant que les nœuds de hello sont des messages entre les nœuds de tooprocess prêt.</span><span class="sxs-lookup"><span data-stu-id="7e3af-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="7e3af-121">la tâche principale Hello exécute hello **commande application** sur le nœud principal de hello *après* commande de coordination hello a été correctement effectuée par hello primaire et toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="7e3af-122">commande de l’application Hello hello ligne de commande de tâche d’instances multiples hello lui-même et est exécutée uniquement par la tâche principale de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="7e3af-123">Dans une solution basée sur [MS-MPI][msmpi_msdn], c’est là où vous exécutez votre application prenant en charge MPI au moyen du fichier `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="7e3af-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="7e3af-124">S’il est fonctionnellement distincte, hello « tâche multi-instance » n’est pas un type de tâche unique comme hello [StartTask] [ net_starttask] ou [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="7e3af-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="7e3af-125">tâche d’instances multiples Hello est simplement une tâche de traitement par lots standard ([CloudTask] [ net_task] dans .NET de lot) dont les paramètres de plusieurs instances ont été configurés.</span><span class="sxs-lookup"><span data-stu-id="7e3af-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="7e3af-126">Dans cet article, nous nous référons toothis comme hello **tâche d’instances multiples**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="7e3af-127">Configuration requise pour les tâches multi-instances</span><span class="sxs-lookup"><span data-stu-id="7e3af-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="7e3af-128">Les tâches multi-instances nécessitent un pool avec **communication entre les nœuds activée** et **exécution de tâches simultanées désactivée**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="7e3af-129">l’exécution des tâches simultanées toodisable, jeu hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 de propriété.</span><span class="sxs-lookup"><span data-stu-id="7e3af-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="7e3af-130">Cet extrait de code montre comment toocreate un pool pour plusieurs instances de tâches à l’aide de la bibliothèque de lot .NET hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

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
> <span data-ttu-id="7e3af-131">Si vous essayez de toorun une tâche à instances multiples dans un pool de communication entre les nœuds est désactivée, ou avec un *maxTasksPerNode* valeur supérieure à 1, la tâche hello n’est pas planifiée--il reste indéfiniment dans l’état « actif » de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="7e3af-132">Les tâches multi-instances peuvent s’exécuter uniquement sur des nœuds dans des pools créés après le 14 décembre 2015.</span><span class="sxs-lookup"><span data-stu-id="7e3af-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="7e3af-133">Utiliser un tooinstall StartTask MPI</span><span class="sxs-lookup"><span data-stu-id="7e3af-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="7e3af-134">toorun des applications MPI avec une tâche à plusieurs instances, vous devez tout d’abord tooinstall une implémentation MPI (MS-MPI ou MPI Intel, par exemple) sur les nœuds de calcul hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="7e3af-135">Il s’agit d’un temps toouse un [StartTask][net_starttask], qui s’exécute chaque fois qu’un nœud rejoint un pool ou est redémarré.</span><span class="sxs-lookup"><span data-stu-id="7e3af-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="7e3af-136">Cet extrait de code crée une tâche de début qui spécifie le package d’installation hello MS-MPI comme un [fichier de ressources][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="7e3af-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="7e3af-137">ligne de commande Hello démarrer la tâche est exécutée une fois le fichier de ressources hello est téléchargés toohello nœud.</span><span class="sxs-lookup"><span data-stu-id="7e3af-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="7e3af-138">Dans ce cas, la ligne de commande hello effectue une installation sans assistance de MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="7e3af-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="7e3af-139">Accès direct à la mémoire à distance (RDMA)</span><span class="sxs-lookup"><span data-stu-id="7e3af-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="7e3af-140">Lorsque vous choisissez un [taille prenant en charge RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) comme A9 hello pour les nœuds de calcul dans votre pool de traitement par lots, votre application MPI peut prendre parti de hautes performances et à faible latence mémoire directe à distance (RDMA) d’accès réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="7e3af-141">Recherchez les tailles de hello spécifiées en tant que « RDMA compatibles avec » Bonjour suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="7e3af-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="7e3af-142">Pools **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="7e3af-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="7e3af-143">[Tailles de services cloud](../cloud-services/cloud-services-sizes-specs.md) (Windows uniquement)</span><span class="sxs-lookup"><span data-stu-id="7e3af-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="7e3af-144">Pools **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="7e3af-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="7e3af-145">[Tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="7e3af-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="7e3af-146">[Tailles des machines virtuelles dans Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="7e3af-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="7e3af-147">avantage tootake de RDMA sur [nœuds de calcul Linux](batch-linux-nodes.md), vous devez utiliser **Intel MPI** sur les nœuds hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="7e3af-148">Pour plus d’informations sur les pools de CloudServiceConfiguration et VirtualMachineConfiguration, consultez hello section Pool Hello [vue d’ensemble de lot](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="7e3af-149">Créer une tâche multi-instances avec Batch.NET</span><span class="sxs-lookup"><span data-stu-id="7e3af-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="7e3af-150">Maintenant que nous avons couvert les exigences du pool hello et installation du package MPI, nous allons créer de tâche d’instances multiples hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="7e3af-151">Dans cet extrait de code, nous créons une [CloudTask][net_task] standard, puis nous configurons sa propriété [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="7e3af-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="7e3af-152">Comme mentionné précédemment, tâche d’instances multiples hello n’est pas un type de tâche distinctes, mais une tâche de traitement par lots standard configurés avec les paramètres de plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="7e3af-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="7e3af-153">Tâche principale et tâches subordonnées</span><span class="sxs-lookup"><span data-stu-id="7e3af-153">Primary task and subtasks</span></span>
<span data-ttu-id="7e3af-154">Lorsque vous créez des paramètres à plusieurs instances d’une tâche hello, vous spécifiez le nombre hello de nœuds de calcul qui sont des tâches de hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="7e3af-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="7e3af-155">Quand vous envoyez tooa de tâche hello, hello service Batch crée un **principal** tâche et suffisamment **sous-tâches** ensemble correspondant à nombre hello de nœuds que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="7e3af-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="7e3af-156">Ces tâches sont affectées un id d’entier dans la plage 0 hello trop*numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="7e3af-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="7e3af-157">Hello tâche avec l’id 0 est hello primaire et tous les autres ID sont des tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="7e3af-158">Par exemple, si vous créez hello suivant les paramètres de plusieurs instances d’une tâche, la tâche principale hello aurait un id égal à 0 et hello sous-tâches aurait ID 1 à 9.</span><span class="sxs-lookup"><span data-stu-id="7e3af-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="7e3af-159">Nœud principal</span><span class="sxs-lookup"><span data-stu-id="7e3af-159">Master node</span></span>
<span data-ttu-id="7e3af-160">Lorsque vous soumettez une tâche à plusieurs instances, hello service Batch désigne l’un des hello nœuds de calcul en tant que nœud de « maître » hello et planifications hello tooexecute tâche principale sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="7e3af-161">Hello sous-tâches sont planifiée tooexecute sur reste hello de nœuds hello allouée de tâche d’instances multiples toohello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="7e3af-162">commande de coordination</span><span class="sxs-lookup"><span data-stu-id="7e3af-162">Coordination command</span></span>
<span data-ttu-id="7e3af-163">Hello **commande de coordination** est exécutée en hello principal et les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="7e3af-164">appel de Hello de commande de coordination hello bloque--lot n’exécute pas de commande de l’application hello jusqu'à ce que la commande de coordination hello a retourné avec succès pour toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="7e3af-165">commande de coordination Hello doit par conséquent démarrer tous les services requis, vérifiez qu’ils sont prêts pour une utilisation et puis quittez.</span><span class="sxs-lookup"><span data-stu-id="7e3af-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="7e3af-166">Par exemple, cette commande de coordination pour une solution à l’aide de MS-MPI version 7 démarre le service SMPD hello sur le nœud de hello, puis se ferme :</span><span class="sxs-lookup"><span data-stu-id="7e3af-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="7e3af-167">Notez que hello `start` dans cette commande de coordination.</span><span class="sxs-lookup"><span data-stu-id="7e3af-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="7e3af-168">Cela est nécessaire car hello `smpd.exe` application ne renvoie pas immédiatement après l’exécution.</span><span class="sxs-lookup"><span data-stu-id="7e3af-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="7e3af-169">Sans utiliser hello hello [Démarrer] [ cmd_start] de commande, cette commande de coordination ne retournerait pas et bloque par conséquent commande hello application de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="7e3af-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="7e3af-170">Commande d’application</span><span class="sxs-lookup"><span data-stu-id="7e3af-170">Application command</span></span>
<span data-ttu-id="7e3af-171">Une fois la tâche principale hello et toutes les tâches subordonnées l’exécution de commande de coordination hello, ligne de commande de la tâche hello multi-instance est exécutée par la tâche principale hello *uniquement*.</span><span class="sxs-lookup"><span data-stu-id="7e3af-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="7e3af-172">Nous appelons cette hello **commande application** toodistinguish à partir de la commande de coordination hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="7e3af-173">Pour les applications de MS-MPI, utilisez hello application commande tooexecute votre application MPI avec `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="7e3af-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="7e3af-174">Par exemple, voici une commande d’application pour une solution qui utilise la version 7 de MS-MPI :</span><span class="sxs-lookup"><span data-stu-id="7e3af-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="7e3af-175">Étant donné que MS-MPI `mpiexec.exe` utilise hello `CCP_NODES` variable par défaut (voir [variables d’environnement](#environment-variables)) exemple hello l’exclut de ligne de commande d’application ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7e3af-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="7e3af-176">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="7e3af-176">Environment variables</span></span>
<span data-ttu-id="7e3af-177">Traitement par lots crée plusieurs [variables d’environnement] [ msdn_env_var] tâches toomulti-instance spécifique sur hello nœuds alloué la tâche d’instances multiples tooa de calcul.</span><span class="sxs-lookup"><span data-stu-id="7e3af-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="7e3af-178">Votre application et coordination de lignes de commande peut faire référence à ces variables d’environnement, comme vous pouvez hello scripts et les programmes qu’ils s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="7e3af-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="7e3af-179">Hello variables d’environnement suivantes sont créées par le service de traitement par lots hello pour une utilisation par les tâches de plusieurs instances :</span><span class="sxs-lookup"><span data-stu-id="7e3af-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="7e3af-180">Pour plus de détails sur ces et hello autres lot calcul nœud variables d’environnement, y compris leur contenu et la visibilité, consultez [variables d’environnement de nœud de calcul][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="7e3af-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="7e3af-181">exemple de code de lot Linux MPI Hello contient un exemple d’utilisation de plusieurs de ces variables d’environnement peuvent être.</span><span class="sxs-lookup"><span data-stu-id="7e3af-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="7e3af-182">Hello [cmd de coordination] [ coord_cmd_example] script télécharge l’application courante et les fichiers d’entrée depuis le stockage Azure, permet à un partage système NFS (Network File) sur le nœud principal de hello et configure un interpréteur de commandes hello autres nœuds allouée tâche d’instances multiples toohello en tant que clients NFS.</span><span class="sxs-lookup"><span data-stu-id="7e3af-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="7e3af-183">Fichiers de ressources</span><span class="sxs-lookup"><span data-stu-id="7e3af-183">Resource files</span></span>
<span data-ttu-id="7e3af-184">Il existe deux ensembles de tooconsider de fichiers de ressources pour les tâches d’instances multiples : **des fichiers de ressources communes** qui *tous les* tâches téléchargement (principaux et des tâches subordonnées) et hello **lesfichiersderessources** spécifiée pour hello à plusieurs instances de tâches elle-même, ce qui *uniquement les hello principal* téléchargements de tâches.</span><span class="sxs-lookup"><span data-stu-id="7e3af-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="7e3af-185">Vous pouvez spécifier un ou plusieurs **des fichiers de ressources communes** dans les paramètres de plusieurs instances de hello pour une tâche.</span><span class="sxs-lookup"><span data-stu-id="7e3af-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="7e3af-186">Ces fichiers de ressources communs sont téléchargés à partir de [Azure Storage](../storage/common/storage-introduction.md) dans chaque nœud **répertoire partagé de tâche** par hello primaire et toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="7e3af-187">Vous pouvez également accéder à répertoire partagé de tâche hello à partir de l’application et coordination de lignes de commande à l’aide de hello `AZ_BATCH_TASK_SHARED_DIR` variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="7e3af-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="7e3af-188">Hello `AZ_BATCH_TASK_SHARED_DIR` chemin d’accès est identique sur chaque tâche de plusieurs instances de nœud toohello alloué, par conséquent, vous pouvez partager une commande unique coordination entre hello primaire et toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="7e3af-189">Lot ne partage pas de » « hello répertoire dans un sens de l’accès à distance, mais vous pouvez l’utiliser comme un montage ou partager le dossier comme mentionné précédemment dans l’info-bulle hello sur les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="7e3af-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="7e3af-190">Fichiers de ressources que vous spécifiez pour le répertoire de travail de la tâche toohello téléchargé, sont hello tâche d’instances multiples `AZ_BATCH_TASK_WORKING_DIR`, par défaut.</span><span class="sxs-lookup"><span data-stu-id="7e3af-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="7e3af-191">Comme indiqué, en revanche toocommon des fichiers de ressources, seule la tâche principale hello télécharge les fichiers de ressources spécifiés pour la tâche d’instances multiples hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="7e3af-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e3af-192">Utilisez toujours des variables d’environnement hello `AZ_BATCH_TASK_SHARED_DIR` et `AZ_BATCH_TASK_WORKING_DIR` répertoires de toothese toorefer dans les lignes de commande.</span><span class="sxs-lookup"><span data-stu-id="7e3af-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="7e3af-193">N’essayez pas chemins d’accès de hello tooconstruct manuellement.</span><span class="sxs-lookup"><span data-stu-id="7e3af-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="7e3af-194">Durée de vie de la tâche</span><span class="sxs-lookup"><span data-stu-id="7e3af-194">Task lifetime</span></span>
<span data-ttu-id="7e3af-195">durée de vie Hello de hello tâche principale contrôles hello durée de vie de tâche d’instances multiples ensemble hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="7e3af-196">Lorsque hello principal s’arrête, toutes les tâches subordonnées de hello sont terminées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="7e3af-197">code de sortie Hello hello principal est le code de sortie hello de tâche hello et est donc utilisé toodetermine hello réussite ou l’échec de la tâche hello à des fins de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="7e3af-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="7e3af-198">Si une des tâches subordonnées de hello échouent, fermeture avec un code de retour différente de zéro, par exemple, hello multi-instance entière tâche échoue.</span><span class="sxs-lookup"><span data-stu-id="7e3af-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="7e3af-199">Hello multi-instance tâche est ensuite arrêtée et retentée des tooits nombre maximal de tentatives.</span><span class="sxs-lookup"><span data-stu-id="7e3af-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="7e3af-200">Lorsque vous supprimez une tâche à plusieurs instances, hello primaire et toutes les tâches subordonnées sont également supprimées par hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="7e3af-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="7e3af-201">Sous-tâche à tous les répertoires et leurs fichiers sont supprimés à partir des nœuds de calcul hello, comme pour une tâche standard.</span><span class="sxs-lookup"><span data-stu-id="7e3af-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="7e3af-202">[TaskConstraints] [ net_taskconstraints] pour une tâche à instances multiples, par exemple hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], et [RetentionTime] [ net_taskconstraint_retention] propriétés, sont honorées tels qu’ils sont destinés à une tâche standard, appliquent toohello primaire et toutes les tâches subordonnées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="7e3af-203">Toutefois, si vous modifiez hello [RetentionTime] [ net_taskconstraint_retention] propriété après l’ajout de hello multi-instance toohello tâche, cette modification est appliquée toohello uniquement la tâche principale.</span><span class="sxs-lookup"><span data-stu-id="7e3af-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="7e3af-204">Toutes les tâches subordonnées hello continuent toouse hello original [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="7e3af-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="7e3af-205">Liste des tâches récentes d’un nœud de calcul reflète id hello d’une tâche subordonnée si la tâche récente hello faisait partie d’une tâche à instances multiples.</span><span class="sxs-lookup"><span data-stu-id="7e3af-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="7e3af-206">Obtenir des informations sur les tâches subordonnées</span><span class="sxs-lookup"><span data-stu-id="7e3af-206">Obtain information about subtasks</span></span>
<span data-ttu-id="7e3af-207">tooobtain plus d’informations sur les tâches subordonnées à l’aide hello Batch .NET bibliothèque, appel hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] (méthode).</span><span class="sxs-lookup"><span data-stu-id="7e3af-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="7e3af-208">Cette méthode retourne des informations sur toutes les tâches subordonnées et informations hello calcul nœud hello tâches exécutées.</span><span class="sxs-lookup"><span data-stu-id="7e3af-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="7e3af-209">À partir de ces informations, vous pouvez déterminer le répertoire racine de la tâche subordonnée, id du pool hello, son état actuel, le code de sortie et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="7e3af-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="7e3af-210">Vous pouvez utiliser ces informations en combinaison avec hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] les fichiers de méthode tooobtain hello la tâche subordonnée.</span><span class="sxs-lookup"><span data-stu-id="7e3af-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="7e3af-211">Notez que cette méthode ne retourne pas d’informations pour la tâche principale hello (id 0).</span><span class="sxs-lookup"><span data-stu-id="7e3af-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="7e3af-212">Sauf indication contraire, les méthodes .NET de traitement par lots qui fonctionnent sur hello multi-instance [CloudTask] [ net_task] lui-même s’appliquent *uniquement* toohello la tâche principale.</span><span class="sxs-lookup"><span data-stu-id="7e3af-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="7e3af-213">Par exemple, lorsque vous appelez hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] méthode sur une tâche à plusieurs instances, seuls les fichiers de la tâche hello principal sont retournés.</span><span class="sxs-lookup"><span data-stu-id="7e3af-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="7e3af-214">Hello extrait de code suivant montre comment tooobtain sous-tâche plus d’informations, ainsi que demander le contenu du fichier à partir des nœuds hello sur lequel ils exécutée.</span><span class="sxs-lookup"><span data-stu-id="7e3af-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="7e3af-215">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="7e3af-215">Code sample</span></span>
<span data-ttu-id="7e3af-216">Hello [MultiInstanceTasks] [ github_mpi] exemple de code sur GitHub montre comment toouse un à plusieurs instances de tâches toorun un [MS-MPI] [ msmpi_msdn] application sur les nœuds de calcul de lot.</span><span class="sxs-lookup"><span data-stu-id="7e3af-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="7e3af-217">Suivez les étapes de hello dans [préparation](#preparation) et [exécution](#execution) toorun hello exemple.</span><span class="sxs-lookup"><span data-stu-id="7e3af-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="7e3af-218">Préparation</span><span class="sxs-lookup"><span data-stu-id="7e3af-218">Preparation</span></span>
1. <span data-ttu-id="7e3af-219">Suivez les deux premières étapes de hello dans [comment toocompile et exécuter un programme MS-MPI simple][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="7e3af-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="7e3af-220">Cela satisfait prerequesites hello pour hello suivant l’étape.</span><span class="sxs-lookup"><span data-stu-id="7e3af-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="7e3af-221">Générer un *version* version de hello [MPIHelloWorld] [ helloworld_proj] exemple de programme MPI.</span><span class="sxs-lookup"><span data-stu-id="7e3af-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="7e3af-222">Il s’agit de programme hello qui est exécutée sur les nœuds de calcul par la tâche d’instances multiples hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="7e3af-223">Créez un fichier .zip contenant `MPIHelloWorld.exe` (que vous avez créé à l’étape 2) et `MSMpiSetup.exe` (que vous avez téléchargé à l’étape 1).</span><span class="sxs-lookup"><span data-stu-id="7e3af-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="7e3af-224">Vous allez télécharger ce fichier zip en tant qu’un package d’application à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="7e3af-225">Hello d’utilisation [portail Azure] [ portal] toocreate un lot [application](batch-application-packages.md) appelé « MPIHelloWorld » et spécifiez le fichier zip de hello créé à l’étape précédente de hello en tant que version « 1.0 » de package d’application Hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="7e3af-226">Pour plus d’informations, consultez [Téléchargement et gestion des applications](batch-application-packages.md#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="7e3af-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="7e3af-227">Générer un *version* version de `MPIHelloWorld.exe` afin que vous n’avez pas tooinclude toutes les dépendances supplémentaires (par exemple, `msvcp140d.dll` ou `vcruntime140d.dll`) dans votre package d’application.</span><span class="sxs-lookup"><span data-stu-id="7e3af-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="7e3af-228">Exécution</span><span class="sxs-lookup"><span data-stu-id="7e3af-228">Execution</span></span>
1. <span data-ttu-id="7e3af-229">Télécharger hello [exemples de traitement par lots azure] [ github_samples_zip] à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="7e3af-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="7e3af-230">Ouvrez hello MultiInstanceTasks **solution** dans Visual Studio 2015 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="7e3af-231">Hello `MultiInstanceTasks.sln` fichier solution se trouve dans :</span><span class="sxs-lookup"><span data-stu-id="7e3af-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="7e3af-232">Entrez vos informations d’identification compte Batch et de stockage dans `AccountSettings.settings` Bonjour **Microsoft.Azure.Batch.Samples.Common** projet.</span><span class="sxs-lookup"><span data-stu-id="7e3af-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="7e3af-233">**Générez et exécutez** hello MultiInstanceTasks solution tooexecute hello MPI exemple d’application sur les nœuds de calcul dans un pool de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="7e3af-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="7e3af-234">*Facultatif*: hello d’utilisation [portail Azure] [ portal] ou hello [lot Explorer] [ batch_explorer] tooexamine pool d’exemple hello, travail, et tâches (« MultiInstanceSamplePool », « MultiInstanceSampleJob », « MultiInstanceSampleTask ») avant de supprimer les ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="7e3af-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="7e3af-235">Vous pouvez télécharger [Visual Studio Community][visual_studio] gratuitement si vous n’avez pas Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7e3af-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="7e3af-236">Sortie de `MultiInstanceTasks.exe` est similaire toohello suivant :</span><span class="sxs-lookup"><span data-stu-id="7e3af-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

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

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="7e3af-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e3af-237">Next steps</span></span>
* <span data-ttu-id="7e3af-238">blog de l’équipe de lot de Azure et de Microsoft HPC Hello traite [MPI prise en charge de Linux sur Azure Batch][blog_mpi_linux]et inclut des informations sur l’utilisation de [OpenFOAM] [ openfoam] traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="7e3af-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="7e3af-239">Vous trouverez des exemples de code Python pour hello [exemple OpenFOAM sur GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="7e3af-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="7e3af-240">Découvrez comment trop[créer des pools de nœuds de calcul Linux](batch-linux-nodes.md) à utiliser dans vos solutions Azure Batch MPI.</span><span class="sxs-lookup"><span data-stu-id="7e3af-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
