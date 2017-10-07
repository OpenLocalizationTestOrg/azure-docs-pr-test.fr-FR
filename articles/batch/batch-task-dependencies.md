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
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>Créer des interdépendances toorun les tâches qui dépendent d’autres tâches

Vous pouvez définir toorun des dépendances de tâche une tâche ou un ensemble de tâches uniquement après qu’une tâche parente est terminée. Voici quelques scénarios dont les dépendances de tâche sont utiles :

* Charges de travail MapReduce de style dans le cloud de hello.
* des travaux dont les tâches de traitement des données peuvent être exprimées sous la forme d’un graphe orienté acyclique (DAG) ;
* Processus de rendu avant et après le rendu, où chaque tâche doit se terminer avant le début de la tâche suivante hello.
* N’importe quel travail dans lequel les tâches en aval dépendent de sortie hello de tâches en amont.

Avec les dépendances de tâche de traitement par lots, vous pouvez créer des tâches qui sont planifiées pour l’exécution sur les nœuds de calcul après l’achèvement de hello d’une ou plusieurs tâches parent. Par exemple, vous pouvez créer un travail qui restitue chaque image d’un film 3D avec des tâches parallèles distinctes. tâche finale de Hello--hello « tâche de fusion »--fusions hello images rendue dans la vidéo complète de hello uniquement une fois toutes les images ont été correctement rendus.

Par défaut, les tâches dépendantes sont planifiées pour l’exécution uniquement après hello parent est terminée avec succès. Vous pouvez spécifier un comportement par défaut de dépendance action toooverride hello et exécuter des tâches en cas d’échec de la tâche parente de hello. Consultez hello [actions de dépendance](#dependency-actions) pour plus d’informations.  

Vous pouvez créer des tâches qui dépendent d’autres tâches dans une relation un-à-un ou un-à-plusieurs. Vous pouvez également créer une dépendance de la plage où une tâche dépend d’achèvement hello d’un groupe de tâches au sein d’une plage d’ID de tâche spécifiée. Vous pouvez combiner ces trois relations plusieurs-à-plusieurs de toocreate des scénarios de base.

## <a name="task-dependencies-with-batch-net"></a>Dépendances de tâches avec Batch.NET
Dans cet article, nous expliquons comment tooconfigure les dépendances de tâche à l’aide de hello [Batch .NET] [ net_msdn] bibliothèque. Nous avons tout d’abord montrent comment trop[activer interdépendance](#enable-task-dependencies) dans vos projets, puis d’illustrer comment trop[configurer une tâche avec des dépendances](#create-dependent-tasks). Nous expliquons également comment toospecify une dépendance action toorun tâches dépendantes si le parent de hello échoue. Enfin, nous évoquerons hello [scénarios dépendance](#dependency-scenarios) qui prend en charge de traitement par lots.

## <a name="enable-task-dependencies"></a>Activation des dépendances de tâches
toouse les dépendances de tâches dans votre application de traitement par lots, vous devez d’abord configurer interdépendances toouse de travail hello. Dans .NET de lot, l’activer sur votre [CloudJob] [ net_cloudjob] en définissant son [UsesTaskDependencies] [ net_usestaskdependencies] propriété trop`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

Bonjour précédant l’extrait de code, « batchClient » est une instance de hello [BatchClient] [ net_batchclient] classe.

## <a name="create-dependent-tasks"></a>Création de tâches dépendantes
toocreate une tâche qui dépend d’achèvement hello d’une ou plusieurs tâches parent, vous pouvez spécifier que hello hello de tâche « dépend » autres tâches. Dans .NET de lot, configurer hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] propriété avec une instance de hello [TaskDependencies] [ net_taskdependencies] classe :

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

Cet extrait de code crée une tâche dépendante avec l’ID de tâche « Flowers ». Hello « Fleurs » tâche dépend des tâches « Train » et « Sun ». La tâche « Fleurs » sera toorun planifiée sur un nœud de calcul uniquement une fois les tâches « Train » et « Sun » sont terminés.

> [!NOTE]
> Une tâche est considérée comme toobe s’est terminée correctement quand il sera hello **terminé** état et son **code de sortie** est `0`. Dans .NET de traitement par lots, cela signifie une [CloudTask][net_cloudtask].[ État] [ net_taskstate] valeur de propriété `Completed` et hello du CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] valeur de propriété est `0`.
> 
> 

## <a name="dependency-scenarios"></a>scénarios de dépendance
Vous pouvez utiliser trois scénarios de dépendance de tâches de base dans Azure Batch : un-à-un, un-à-plusieurs et dépendance de plage d’ID de tâche. Il peuvent être combiné tooprovide une quatrième scénario, plusieurs-à-plusieurs.

| Scénario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Exemple |  |
|:---:| --- | --- |
|  [Un-à-un](#one-to-one) |*taskB* dépend de *taskA* <p/> *taskB* n’est pas planifié pour s’exécuter tant que l’exécution de *taskA* n’est pas terminée |![Schéma : dépendance de tâches un-à-un][1] |
|  [Un-à-plusieurs](#one-to-many) |*taskC* dépend de *taskA* et de *taskB* <p/> *taskC* n’est pas planifié pour s’exécuter tant que l’exécution de *taskA* et *taskB* n’est pas terminée |![Schéma : dépendance de tâches un-à-plusieurs][2] |
|  [Plage d’ID de tâche](#task-id-range) |*taskD* dépend d’une plage de tâches <p/> *taskD* ne sera pas planifié pour l’exécution jusqu'à ce que les tâches hello avec des ID *1* via *10* terminées avec succès |![Schéma : dépendance de plage d’ID de tâche][3] |

> [!TIP]
> Vous pouvez créer **plusieurs-à-plusieurs** relations, telles que les tâches C, D, E et F chaque où dépendent de tâches A et B. Cela est utile, par exemple, dans des scénarios de prétraitement parallélisées où vos tâches en aval dépendent de sortie hello de plusieurs tâches en amont.
> 
> Dans les exemples hello dans cette section, une tâche dépendante s’exécute uniquement une fois hello parent tâches terminées. Ce comportement est le comportement par défaut de hello pour une tâche dépendante. Vous pouvez exécuter une tâche dépendante après l’échec d’une tâche parent en spécifiant un comportement par défaut de dépendance action toooverride hello. Consultez hello [actions de dépendance](#dependency-actions) pour plus d’informations.

### <a name="one-to-one"></a>Un-à-un
Dans le type de relation, une tâche dépend hello tâche se termine correctement un seul parent. toocreate hello dépendance, fournissez un toohello d’ID de tâche unique [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] une méthode statique lorsque vous remplissez hello [DependsOn] [ net_dependson] propriété du [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>Un-à-plusieurs
Dans une relation un-à-plusieurs, une tâche dépend à la fin de hello de plusieurs tâches parent. toocreate hello dépendance, fournissent une collection de tâches ID toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] une méthode statique lorsque vous remplissez hello [DependsOn] [ net_dependson] propriété du [CloudTask] [ net_cloudtask].

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

### <a name="task-id-range"></a>Plage d’ID de tâche
Une dépendance sur une plage de tâches parentes, une tâche dépend à la fin de hello hello de tâches dont les ID se situent dans une plage.
dépendance de hello toocreate, fournir tout d’abord les hello et dernier ID de tâches dans hello plage toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] une méthode statique lorsque vous remplissez hello [DependsOn] [ net_dependson] propriété du [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> Lorsque vous utilisez des plages d’ID de tâche pour les dépendances, hello ID de tâche dans la plage de hello *doit* être représentations sous forme de chaîne de valeurs entières.
> 
> Chaque tâche dans la plage de hello doit satisfaire la dépendance de hello, terminé ou en procédant avec un échec est l’action de dépendance mappé tooa définie trop**satisfaction**. Consultez hello [actions de dépendance](#dependency-actions) pour plus d’informations.
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

## <a name="dependency-actions"></a>Actions de dépendance

Par défaut, une tâche dépendante ou un ensemble de tâches s’exécute uniquement après la fin d’une tâche parente. Dans certains scénarios, vous pouvez vouloir toorun des tâches dépendantes même si la tâche parent hello échoue. Vous pouvez remplacer le comportement par défaut de hello en spécifiant une action de dépendance. Une action de dépendance Spécifie si une tâche dépendante est éligible toorun, en fonction de la réussite de hello ou l’échec de la tâche parente de hello. 

Par exemple, supposons qu’une tâche dépendante est en attente de données à partir de la fin de hello de tâche en amont hello. Si la tâche en amont hello échoue, tâche dépendante hello peut-être toujours en mesure de toorun à l’aide des données plus anciennes. Dans ce cas, une action de dépendance peut spécifier que cette tâche de dépendants hello est éligible toorun en dépit de l’échec hello de la tâche parente de hello.

Une action de dépendance est basée sur une condition de sortie de la tâche parente de hello. Vous pouvez spécifier une action de dépendance des hello suivant des conditions de sortie ; pour .NET, consultez hello [ExitConditions] [ net_exitconditions] classe pour plus d’informations :

- Lorsqu’une erreur de prétraitement se produit.
- Lorsqu’une erreur de chargement de fichier se produit. Si la tâche hello se termine avec un code de sortie qui a été spécifié via **exitCodes** ou **exitCodeRanges**, puis rencontre une erreur de chargement du fichier, l’action hello spécifié par hello exit code est prioritaire.
- Lorsque la tâche hello se termine avec un code de sortie défini par hello **ExitCodes** propriété.
- Lorsque la tâche hello se termine avec un code de sortie qui se situe dans une plage spécifiée par hello **ExitCodeRanges** propriété.
- Hello cas par défaut, si la tâche hello se termine avec un code de sortie non défini par **ExitCodes** ou **ExitCodeRanges**, ou si la tâche hello se termine avec une erreur de prétraitement et hello **PreProcessingError**  propriété n’est pas définie, ou si hello de tâches échoue avec un fichier télécharger erreur et hello **FileUploadError** propriété n’est pas définie. 

toospecify une action de dépendance dans .NET, jeu hello [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] propriété de condition de sortie hello. Hello **DependencyAction** propriété prend l’une des deux valeurs :

- Hello du paramètre **DependencyAction** propriété trop**satisfaction** indique que les tâches dépendantes sont éligible toorun si la tâche parente de hello se termine avec une erreur spécifiée.
- Hello du paramètre **DependencyAction** propriété trop**bloc** indique que les tâches dépendantes ne sont pas éligible toorun.

Hello du paramètre par défaut pour hello **DependencyAction** propriété **satisfaction** pour le code de sortie 0, et **bloc** pour toutes les autres conditions de sortie.

Hello extrait de code suivant définit hello **DependencyAction** propriété pour une tâche parente. Si tâche parente de hello se termine avec une erreur de traitement préliminaire ou par hello les codes d’erreur spécifié, hello dépendants tâche est bloquée. Si la tâche parente de hello se termine avec une autre erreur non nulle, les tâches dépendantes hello sont toorun éligible.

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

## <a name="code-sample"></a>Exemple de code
Hello [TaskDependencies] [ github_taskdependencies] exemple de projet est un des hello [exemples de code Azure Batch] [ github_samples] sur GitHub. La solution Visual Studio montre :

- Comment tooenable tâche dépendant d’un travail
- Comment toocreate tâches qui dépendent d’autres tâches
- Comment tooexecute ces tâches sur un pool de nœuds de calcul.

## <a name="next-steps"></a>Étapes suivantes
### <a name="application-deployment"></a>Déploiement des applications
Hello [des packages d’application](batch-application-packages.md) fonctionnalité du lot fournit une facilement tooboth déployer et une version applications hello vos tâches s’exécutent sur les nœuds de calcul.

### <a name="installing-applications-and-staging-data"></a>Installation d’applications et de données intermédiaires
Consultez [l’installation d’applications et de mise en attente de traitement par lots des nœuds de calcul] [ forum_post] dans le forum Azure Batch hello pour une vue d’ensemble des méthodes pour la préparation de vos nœuds toorun tâches. Écrit par un des membres de l’équipe Azure Batch hello, que cette publication est une bonne introduction sur les applications de toocopy de différentes façons de hello, les données d’entrée de tâches et autres tooyour fichiers nœuds de calcul.

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
