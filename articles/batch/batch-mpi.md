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
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a>Utiliser les applications multi-instance tâches toorun Interface MPI (Message Passing) dans le lot

Instances multiples tâches permettent toorun une tâche de traitement par lots Azure sur plusieurs nœuds de calcul simultanément. Ces tâches permettent de mettre en œuvre des scénarios de calcul haute performance tels que les applications MPI (Message Passing Interface) dans Batch. Dans cet article, vous apprendrez comment les tâches de plusieurs instances de tooexecute à l’aide de hello [Batch .NET] [ api_net] bibliothèque.

> [!NOTE]
> Tandis que les exemples de hello dans cet article se concentrent sur .NET de traitement par lots, MS-MPI, et les nœuds de calcul de Windows, concepts de tâche hello multi-instance présentées ici sont applicables tooother plateformes et les technologies (Python et MPI Intel des nœuds Linux, par exemple).
>
>

## <a name="multi-instance-task-overview"></a>Présentation des tâches multi-instances
Dans le traitement par lots, chaque tâche est normalement exécutée sur un nœud de calcul unique--vous soumettez le travail de plusieurs tâches tooa et hello service Batch planifie chaque tâche d’exécution sur un nœud. Toutefois, en configurant d’une tâche **paramètres d’instances multiples**, vous indiquez le lot tooinstead créer une tâche principale et plusieurs tâches subordonnées qui sont ensuite exécutées sur plusieurs nœuds.

![Présentation des tâches multi-instances][1]

Lorsque vous soumettez une tâche avec la tâche d’instances multiples paramètres tooa, lot effectue plusieurs tâches de toomulti-instance unique de comme suit :

1. Hello service Batch crée un **principal** et plusieurs **sous-tâches** en fonction des paramètres d’instances multiples hello. Nombre total de Hello de tâches (principales ainsi que toutes les tâches subordonnées) correspond au nombre de hello de **instances** (nœuds de calcul) vous spécifiez dans les paramètres de plusieurs instances de hello.
2. Lot désigne l’un des hello nœuds de calcul en tant que hello **master**, et les planifications hello tooexecute tâche principale sur le contrôleur de hello. Il planifie tooexecute des sous-tâches hello sur reste hello de tâche hello calcul nœuds toohello allouée à plusieurs instances, une sous-tâche par nœud.
3. téléchargement Hello primaire et toutes les tâches subordonnées **des fichiers de ressources communes** vous spécifiez dans les paramètres de plusieurs instances de hello.
4. Une fois que les fichiers de ressources communs hello ont été téléchargées, hello principal et les tâches subordonnées exécutent hello **commande de coordination** vous spécifiez dans les paramètres de plusieurs instances de hello. commande de coordination Hello est nœuds tooprepare généralement utilisées pour exécuter la tâche hello. Cela peut inclure le démarrage des services d’arrière-plan (tel que [Microsoft MPI][msmpi_msdn]de `smpd.exe`) et en vérifiant que les nœuds de hello sont des messages entre les nœuds de tooprocess prêt.
5. la tâche principale Hello exécute hello **commande application** sur le nœud principal de hello *après* commande de coordination hello a été correctement effectuée par hello primaire et toutes les tâches subordonnées. commande de l’application Hello hello ligne de commande de tâche d’instances multiples hello lui-même et est exécutée uniquement par la tâche principale de hello. Dans une solution basée sur [MS-MPI][msmpi_msdn], c’est là où vous exécutez votre application prenant en charge MPI au moyen du fichier `mpiexec.exe`.

> [!NOTE]
> S’il est fonctionnellement distincte, hello « tâche multi-instance » n’est pas un type de tâche unique comme hello [StartTask] [ net_starttask] ou [JobPreparationTask] [ net_jobprep]. tâche d’instances multiples Hello est simplement une tâche de traitement par lots standard ([CloudTask] [ net_task] dans .NET de lot) dont les paramètres de plusieurs instances ont été configurés. Dans cet article, nous nous référons toothis comme hello **tâche d’instances multiples**.
>
>

## <a name="requirements-for-multi-instance-tasks"></a>Configuration requise pour les tâches multi-instances
Les tâches multi-instances nécessitent un pool avec **communication entre les nœuds activée** et **exécution de tâches simultanées désactivée**. l’exécution des tâches simultanées toodisable, jeu hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 de propriété.

Cet extrait de code montre comment toocreate un pool pour plusieurs instances de tâches à l’aide de la bibliothèque de lot .NET hello.

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
> Si vous essayez de toorun une tâche à instances multiples dans un pool de communication entre les nœuds est désactivée, ou avec un *maxTasksPerNode* valeur supérieure à 1, la tâche hello n’est pas planifiée--il reste indéfiniment dans l’état « actif » de hello. 
>
> Les tâches multi-instances peuvent s’exécuter uniquement sur des nœuds dans des pools créés après le 14 décembre 2015.
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a>Utiliser un tooinstall StartTask MPI
toorun des applications MPI avec une tâche à plusieurs instances, vous devez tout d’abord tooinstall une implémentation MPI (MS-MPI ou MPI Intel, par exemple) sur les nœuds de calcul hello dans le pool de hello. Il s’agit d’un temps toouse un [StartTask][net_starttask], qui s’exécute chaque fois qu’un nœud rejoint un pool ou est redémarré. Cet extrait de code crée une tâche de début qui spécifie le package d’installation hello MS-MPI comme un [fichier de ressources][net_resourcefile]. ligne de commande Hello démarrer la tâche est exécutée une fois le fichier de ressources hello est téléchargés toohello nœud. Dans ce cas, la ligne de commande hello effectue une installation sans assistance de MS-MPI.

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

### <a name="remote-direct-memory-access-rdma"></a>Accès direct à la mémoire à distance (RDMA)
Lorsque vous choisissez un [taille prenant en charge RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) comme A9 hello pour les nœuds de calcul dans votre pool de traitement par lots, votre application MPI peut prendre parti de hautes performances et à faible latence mémoire directe à distance (RDMA) d’accès réseau Azure.

Recherchez les tailles de hello spécifiées en tant que « RDMA compatibles avec » Bonjour suivant des articles :

* Pools **CloudServiceConfiguration**

  * [Tailles de services cloud](../cloud-services/cloud-services-sizes-specs.md) (Windows uniquement)
* Pools **VirtualMachineConfiguration**

  * [Tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)
  * [Tailles des machines virtuelles dans Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)

> [!NOTE]
> avantage tootake de RDMA sur [nœuds de calcul Linux](batch-linux-nodes.md), vous devez utiliser **Intel MPI** sur les nœuds hello. Pour plus d’informations sur les pools de CloudServiceConfiguration et VirtualMachineConfiguration, consultez hello section Pool Hello [vue d’ensemble de lot](batch-api-basics.md).
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a>Créer une tâche multi-instances avec Batch.NET
Maintenant que nous avons couvert les exigences du pool hello et installation du package MPI, nous allons créer de tâche d’instances multiples hello. Dans cet extrait de code, nous créons une [CloudTask][net_task] standard, puis nous configurons sa propriété [MultiInstanceSettings][net_multiinstance_prop]. Comme mentionné précédemment, tâche d’instances multiples hello n’est pas un type de tâche distinctes, mais une tâche de traitement par lots standard configurés avec les paramètres de plusieurs instances.

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

## <a name="primary-task-and-subtasks"></a>Tâche principale et tâches subordonnées
Lorsque vous créez des paramètres à plusieurs instances d’une tâche hello, vous spécifiez le nombre hello de nœuds de calcul qui sont des tâches de hello tooexecute. Quand vous envoyez tooa de tâche hello, hello service Batch crée un **principal** tâche et suffisamment **sous-tâches** ensemble correspondant à nombre hello de nœuds que vous avez spécifié.

Ces tâches sont affectées un id d’entier dans la plage 0 hello trop*numberOfInstances* - 1. Hello tâche avec l’id 0 est hello primaire et tous les autres ID sont des tâches subordonnées. Par exemple, si vous créez hello suivant les paramètres de plusieurs instances d’une tâche, la tâche principale hello aurait un id égal à 0 et hello sous-tâches aurait ID 1 à 9.

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a>Nœud principal
Lorsque vous soumettez une tâche à plusieurs instances, hello service Batch désigne l’un des hello nœuds de calcul en tant que nœud de « maître » hello et planifications hello tooexecute tâche principale sur le nœud principal de hello. Hello sous-tâches sont planifiée tooexecute sur reste hello de nœuds hello allouée de tâche d’instances multiples toohello.

## <a name="coordination-command"></a>commande de coordination
Hello **commande de coordination** est exécutée en hello principal et les tâches subordonnées.

appel de Hello de commande de coordination hello bloque--lot n’exécute pas de commande de l’application hello jusqu'à ce que la commande de coordination hello a retourné avec succès pour toutes les tâches subordonnées. commande de coordination Hello doit par conséquent démarrer tous les services requis, vérifiez qu’ils sont prêts pour une utilisation et puis quittez. Par exemple, cette commande de coordination pour une solution à l’aide de MS-MPI version 7 démarre le service SMPD hello sur le nœud de hello, puis se ferme :

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

Notez que hello `start` dans cette commande de coordination. Cela est nécessaire car hello `smpd.exe` application ne renvoie pas immédiatement après l’exécution. Sans utiliser hello hello [Démarrer] [ cmd_start] de commande, cette commande de coordination ne retournerait pas et bloque par conséquent commande hello application de s’exécuter.

## <a name="application-command"></a>Commande d’application
Une fois la tâche principale hello et toutes les tâches subordonnées l’exécution de commande de coordination hello, ligne de commande de la tâche hello multi-instance est exécutée par la tâche principale hello *uniquement*. Nous appelons cette hello **commande application** toodistinguish à partir de la commande de coordination hello.

Pour les applications de MS-MPI, utilisez hello application commande tooexecute votre application MPI avec `mpiexec.exe`. Par exemple, voici une commande d’application pour une solution qui utilise la version 7 de MS-MPI :

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> Étant donné que MS-MPI `mpiexec.exe` utilise hello `CCP_NODES` variable par défaut (voir [variables d’environnement](#environment-variables)) exemple hello l’exclut de ligne de commande d’application ci-dessus.
>
>

## <a name="environment-variables"></a>Variables d’environnement
Traitement par lots crée plusieurs [variables d’environnement] [ msdn_env_var] tâches toomulti-instance spécifique sur hello nœuds alloué la tâche d’instances multiples tooa de calcul. Votre application et coordination de lignes de commande peut faire référence à ces variables d’environnement, comme vous pouvez hello scripts et les programmes qu’ils s’exécutent.

Hello variables d’environnement suivantes sont créées par le service de traitement par lots hello pour une utilisation par les tâches de plusieurs instances :

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

Pour plus de détails sur ces et hello autres lot calcul nœud variables d’environnement, y compris leur contenu et la visibilité, consultez [variables d’environnement de nœud de calcul][msdn_env_var].

> [!TIP]
> exemple de code de lot Linux MPI Hello contient un exemple d’utilisation de plusieurs de ces variables d’environnement peuvent être. Hello [cmd de coordination] [ coord_cmd_example] script télécharge l’application courante et les fichiers d’entrée depuis le stockage Azure, permet à un partage système NFS (Network File) sur le nœud principal de hello et configure un interpréteur de commandes hello autres nœuds allouée tâche d’instances multiples toohello en tant que clients NFS.
>
>

## <a name="resource-files"></a>Fichiers de ressources
Il existe deux ensembles de tooconsider de fichiers de ressources pour les tâches d’instances multiples : **des fichiers de ressources communes** qui *tous les* tâches téléchargement (principaux et des tâches subordonnées) et hello **lesfichiersderessources** spécifiée pour hello à plusieurs instances de tâches elle-même, ce qui *uniquement les hello principal* téléchargements de tâches.

Vous pouvez spécifier un ou plusieurs **des fichiers de ressources communes** dans les paramètres de plusieurs instances de hello pour une tâche. Ces fichiers de ressources communs sont téléchargés à partir de [Azure Storage](../storage/common/storage-introduction.md) dans chaque nœud **répertoire partagé de tâche** par hello primaire et toutes les tâches subordonnées. Vous pouvez également accéder à répertoire partagé de tâche hello à partir de l’application et coordination de lignes de commande à l’aide de hello `AZ_BATCH_TASK_SHARED_DIR` variable d’environnement. Hello `AZ_BATCH_TASK_SHARED_DIR` chemin d’accès est identique sur chaque tâche de plusieurs instances de nœud toohello alloué, par conséquent, vous pouvez partager une commande unique coordination entre hello primaire et toutes les tâches subordonnées. Lot ne partage pas de » « hello répertoire dans un sens de l’accès à distance, mais vous pouvez l’utiliser comme un montage ou partager le dossier comme mentionné précédemment dans l’info-bulle hello sur les variables d’environnement.

Fichiers de ressources que vous spécifiez pour le répertoire de travail de la tâche toohello téléchargé, sont hello tâche d’instances multiples `AZ_BATCH_TASK_WORKING_DIR`, par défaut. Comme indiqué, en revanche toocommon des fichiers de ressources, seule la tâche principale hello télécharge les fichiers de ressources spécifiés pour la tâche d’instances multiples hello lui-même.

> [!IMPORTANT]
> Utilisez toujours des variables d’environnement hello `AZ_BATCH_TASK_SHARED_DIR` et `AZ_BATCH_TASK_WORKING_DIR` répertoires de toothese toorefer dans les lignes de commande. N’essayez pas chemins d’accès de hello tooconstruct manuellement.
>
>

## <a name="task-lifetime"></a>Durée de vie de la tâche
durée de vie Hello de hello tâche principale contrôles hello durée de vie de tâche d’instances multiples ensemble hello. Lorsque hello principal s’arrête, toutes les tâches subordonnées de hello sont terminées. code de sortie Hello hello principal est le code de sortie hello de tâche hello et est donc utilisé toodetermine hello réussite ou l’échec de la tâche hello à des fins de nouvelle tentative.

Si une des tâches subordonnées de hello échouent, fermeture avec un code de retour différente de zéro, par exemple, hello multi-instance entière tâche échoue. Hello multi-instance tâche est ensuite arrêtée et retentée des tooits nombre maximal de tentatives.

Lorsque vous supprimez une tâche à plusieurs instances, hello primaire et toutes les tâches subordonnées sont également supprimées par hello service Batch. Sous-tâche à tous les répertoires et leurs fichiers sont supprimés à partir des nœuds de calcul hello, comme pour une tâche standard.

[TaskConstraints] [ net_taskconstraints] pour une tâche à instances multiples, par exemple hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], et [RetentionTime] [ net_taskconstraint_retention] propriétés, sont honorées tels qu’ils sont destinés à une tâche standard, appliquent toohello primaire et toutes les tâches subordonnées. Toutefois, si vous modifiez hello [RetentionTime] [ net_taskconstraint_retention] propriété après l’ajout de hello multi-instance toohello tâche, cette modification est appliquée toohello uniquement la tâche principale. Toutes les tâches subordonnées hello continuent toouse hello original [RetentionTime][net_taskconstraint_retention].

Liste des tâches récentes d’un nœud de calcul reflète id hello d’une tâche subordonnée si la tâche récente hello faisait partie d’une tâche à instances multiples.

## <a name="obtain-information-about-subtasks"></a>Obtenir des informations sur les tâches subordonnées
tooobtain plus d’informations sur les tâches subordonnées à l’aide hello Batch .NET bibliothèque, appel hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] (méthode). Cette méthode retourne des informations sur toutes les tâches subordonnées et informations hello calcul nœud hello tâches exécutées. À partir de ces informations, vous pouvez déterminer le répertoire racine de la tâche subordonnée, id du pool hello, son état actuel, le code de sortie et bien plus encore. Vous pouvez utiliser ces informations en combinaison avec hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] les fichiers de méthode tooobtain hello la tâche subordonnée. Notez que cette méthode ne retourne pas d’informations pour la tâche principale hello (id 0).

> [!NOTE]
> Sauf indication contraire, les méthodes .NET de traitement par lots qui fonctionnent sur hello multi-instance [CloudTask] [ net_task] lui-même s’appliquent *uniquement* toohello la tâche principale. Par exemple, lorsque vous appelez hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] méthode sur une tâche à plusieurs instances, seuls les fichiers de la tâche hello principal sont retournés.
>
>

Hello extrait de code suivant montre comment tooobtain sous-tâche plus d’informations, ainsi que demander le contenu du fichier à partir des nœuds hello sur lequel ils exécutée.

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

## <a name="code-sample"></a>Exemple de code
Hello [MultiInstanceTasks] [ github_mpi] exemple de code sur GitHub montre comment toouse un à plusieurs instances de tâches toorun un [MS-MPI] [ msmpi_msdn] application sur les nœuds de calcul de lot. Suivez les étapes de hello dans [préparation](#preparation) et [exécution](#execution) toorun hello exemple.

### <a name="preparation"></a>Préparation
1. Suivez les deux premières étapes de hello dans [comment toocompile et exécuter un programme MS-MPI simple][msmpi_howto]. Cela satisfait prerequesites hello pour hello suivant l’étape.
2. Générer un *version* version de hello [MPIHelloWorld] [ helloworld_proj] exemple de programme MPI. Il s’agit de programme hello qui est exécutée sur les nœuds de calcul par la tâche d’instances multiples hello.
3. Créez un fichier .zip contenant `MPIHelloWorld.exe` (que vous avez créé à l’étape 2) et `MSMpiSetup.exe` (que vous avez téléchargé à l’étape 1). Vous allez télécharger ce fichier zip en tant qu’un package d’application à l’étape suivante de hello.
4. Hello d’utilisation [portail Azure] [ portal] toocreate un lot [application](batch-application-packages.md) appelé « MPIHelloWorld » et spécifiez le fichier zip de hello créé à l’étape précédente de hello en tant que version « 1.0 » de package d’application Hello. Pour plus d’informations, consultez [Téléchargement et gestion des applications](batch-application-packages.md#upload-and-manage-applications).

> [!TIP]
> Générer un *version* version de `MPIHelloWorld.exe` afin que vous n’avez pas tooinclude toutes les dépendances supplémentaires (par exemple, `msvcp140d.dll` ou `vcruntime140d.dll`) dans votre package d’application.
>
>

### <a name="execution"></a>Exécution
1. Télécharger hello [exemples de traitement par lots azure] [ github_samples_zip] à partir de GitHub.
2. Ouvrez hello MultiInstanceTasks **solution** dans Visual Studio 2015 ou version ultérieure. Hello `MultiInstanceTasks.sln` fichier solution se trouve dans :

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. Entrez vos informations d’identification compte Batch et de stockage dans `AccountSettings.settings` Bonjour **Microsoft.Azure.Batch.Samples.Common** projet.
4. **Générez et exécutez** hello MultiInstanceTasks solution tooexecute hello MPI exemple d’application sur les nœuds de calcul dans un pool de traitement par lots.
5. *Facultatif*: hello d’utilisation [portail Azure] [ portal] ou hello [lot Explorer] [ batch_explorer] tooexamine pool d’exemple hello, travail, et tâches (« MultiInstanceSamplePool », « MultiInstanceSampleJob », « MultiInstanceSampleTask ») avant de supprimer les ressources de hello.

> [!TIP]
> Vous pouvez télécharger [Visual Studio Community][visual_studio] gratuitement si vous n’avez pas Visual Studio.
>
>

Sortie de `MultiInstanceTasks.exe` est similaire toohello suivant :

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

## <a name="next-steps"></a>Étapes suivantes
* blog de l’équipe de lot de Azure et de Microsoft HPC Hello traite [MPI prise en charge de Linux sur Azure Batch][blog_mpi_linux]et inclut des informations sur l’utilisation de [OpenFOAM] [ openfoam] traitement par lots. Vous trouverez des exemples de code Python pour hello [exemple OpenFOAM sur GitHub][github_mpi].
* Découvrez comment trop[créer des pools de nœuds de calcul Linux](batch-linux-nodes.md) à utiliser dans vos solutions Azure Batch MPI.

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
