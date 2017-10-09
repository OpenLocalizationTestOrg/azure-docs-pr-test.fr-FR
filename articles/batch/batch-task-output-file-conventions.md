---
title: "aaaPersist projet et la tâche de sortie tooAzure stockage avec la bibliothèque de Conventions pour les fichiers hello pour .NET - Azure Batch | Documents Microsoft"
description: "Découvrez comment toouse bibliothèque de Conventions pour les fichiers par lots Azure pour .NET toopersist tâche de traitement par lots et tooAzure de sortie de travail stockage et vue Bonjour persistant sortie Bonjour portail Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>Conserver le travail et les données tooAzure stockage avec bibliothèque de Conventions pour les fichiers Batch hello pour .NET toopersist de tâches 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Une façon toopersist des données de tâche sont toouse hello [bibliothèque Conventions pour les fichiers par lots Azure pour .NET][nuget_package]. bibliothèque de Conventions pour les fichiers Hello simplifie les processus de hello de stocker le résultat de la tâche données tooAzure stockage et la récupération. Vous pouvez utiliser la bibliothèque de Conventions pour les fichiers de hello dans du code de tâche et le client &mdash; dans le code de tâche pour les fichiers de persistance et client toolist de code et de les récupérer. Votre code de tâche également utiliser hello bibliothèque tooretrieve hello sortie de tâches en amont, comme dans un [interdépendances](batch-task-dependencies.md) scénario. 

les fichiers de bibliothèque de Conventions pour les fichiers hello en sortie tooretrieve, vous pouvez localiser les fichiers hello pour un travail donné ou une tâche en les répertoriant par ID et l’objectif. Vous n’avez pas besoin les noms hello tooknow ou des emplacements de fichiers de hello. Par exemple, vous pouvez utiliser toolist de hello Conventions pour les fichiers bibliothèque tous les fichiers intermédiaires pour une tâche donnée, ou obtenir un aperçu de fichier pour un travail donné.

> [!TIP]
> Depuis la version 2017-05-01, hello API de service de traitement par lots prend en charge la persistance tooAzure de données de sortie stockage pour les tâches et le Gestionnaire des tâches qui s’exécutent sur des pools créés avec la configuration d’ordinateur virtuel hello. Hello API de service de traitement par lots fournit un toopersist moyen simple de sortie à partir de code hello qui crée une tâche et est considérée comme une bibliothèque de Conventions pour les fichiers toohello autre. Vous pouvez modifier votre sortie toopersist de lot client applications sans avoir besoin d’application hello tooupdate votre tâche est en cours d’exécution. Pour plus d’informations, consultez [conserver des tâches données tooAzure stockage avec hello API de lot](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Quand utiliser le résultat de la tâche hello Conventions pour les fichiers bibliothèque toopersist ?

Traitement par lots Azure fournit plusieurs méthodes toopersist sortie de la tâche. Hello Conventions pour les fichiers est meilleure que des scénarios toothese adaptée :

- Vous pouvez facilement modifier le code hello pour application hello que votre tâche est en cours d’exécution toopersist les fichiers à l’aide de la bibliothèque de Conventions pour les fichiers hello.
- Vous souhaitez toostream données tooAzure stockage alors que la tâche hello est en cours d’exécution.
- Vous souhaitez que les données de toopersist à partir des pools créés avec la configuration du service cloud hello ou de configuration d’ordinateur virtuel hello.
- Votre application cliente ou autres tâches dans hello toolocate des besoins de la tâche et téléchargement les fichiers de sortie de tâche par ID ou de leur rôle. 
- Vous souhaitez obtenir une sortie tâche tooview hello portail Azure.

Si votre scénario diffère de celles répertoriées ci-dessus, vous devrez peut-être tooconsider une approche différente. Pour plus d’informations sur les autres options pour la sortie de tâche persistantes, consultez [tooAzure stockage de sortie de projet de la persistance et la tâche](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>Nouveautés hello Conventions pour les fichiers Batch standard

Hello [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fournit un schéma d’affectation de noms pour les conteneurs de destination hello et toowhich de chemins d’accès d’objet blob vos fichiers de sortie sont écrites. TooAzure de fichiers persistant stockage qui adhèrent toohello Conventions standard pour les fichiers sont automatiquement disponibles pour l’affichage dans hello portail Azure. portail de Hello tient compte de la convention d’affectation de noms de hello et peut donc afficher des fichiers respectent tooit.

bibliothèque de Conventions pour les fichiers Hello pour .NET nomme automatiquement vos conteneurs de stockage et les fichiers de sortie de tâche en fonction de toohello Conventions standard pour les fichiers. bibliothèque de Conventions pour les fichiers Hello fournit également des fichiers de sortie tooquery de méthodes dans le stockage Azure selon toojob ID, ID de tâche ou objectif.   

Si vous développez avec une langue autre que .NET, vous pouvez implémenter standard de Conventions pour les fichiers hello vous-même dans votre application. Pour plus d’informations, consultez [sur standard de Conventions pour les fichiers Batch hello](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Lier un tooyour de compte de stockage Azure du compte Batch

toopersist tooAzure de données de sortie stockage à l’aide de la bibliothèque de Conventions pour les fichiers hello, vous devez d’abord lier un tooyour de compte de stockage Azure du compte Batch. Si vous n’avez pas déjà fait, lier un tooyour de compte de stockage du compte Batch à l’aide de hello [portail Azure](https://portal.azure.com):

1. Accédez à tooyour du compte Batch Bonjour portail Azure. 
2. Sous **Paramètres**, sélectionnez **Compte Storage**.
3. Si vous n’avez pas déjà associé de compte Storage à votre compte Batch, cliquez sur **Compte Storage (aucun)**.
4. Sélectionnez un compte de stockage à partir de la liste de hello pour votre abonnement. Pour de meilleures performances, utilisez un compte de stockage Azure qui se trouve dans hello même région que hello compte Batch en exécutant des tâches.

## <a name="persist-output-data"></a>Conserver les données de sortie

tâche toopersist travail sortie des données avec la bibliothèque de Conventions pour les fichiers hello, créer un conteneur dans le stockage Azure, puis enregistrer le conteneur de toohello sortie hello. Hello d’utilisation [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage) dans votre conteneur toohello de sortie de tâche tâche code tooupload hello. 

Pour en savoir plus sur les conteneurs et les objets blob dans Azure Storage, consultez l’article [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Toutes les sorties de projet et la tâche persistant avec hello Conventions pour les fichiers bibliothèque sont stockés dans hello même conteneur. Si un grand nombre de tâches essaient toopersist les fichiers à hello même moment, [limites de stockage](../storage/common/storage-performance-checklist.md#blobs) peut être appliquée.
> 
> 

### <a name="create-storage-container"></a>Créer un conteneur de stockage

tooAzure de sortie de tâche toopersist stockage, d’abord créer un conteneur en appelant [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Cette méthode d’extension nécessite un objet [CloudStorageAccount] [ net_cloudstorageaccount] comme paramètre. Il crée un conteneur nommé conséquente toohello Conventions pour les fichiers standard, afin que son contenu est détectable par hello Azure méthodes de récupération de portail et hello présentés plus loin dans l’article de hello.

En règle générale, vous placez toocreate de code hello un conteneur dans votre application cliente &mdash; hello application qui crée des pools, des tâches et des tâches.

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a>Stocker les sorties des tâches

Maintenant que vous avez préparé un conteneur dans le stockage Azure, les tâches peuvent enregistrer conteneur toohello de sortie à l’aide de hello [TaskOutputStorage] [ net_taskoutputstorage] classe trouvé dans la bibliothèque de Conventions pour les fichiers de hello.

Dans votre code de tâche, commencez par créer un [TaskOutputStorage] [ net_taskoutputstorage] de l’objet, puis lors de la tâche hello a terminé son travail, appelez hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] méthode toosave son tooAzure sortie stockage.

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

Hello `kind` paramètre Hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) méthode catégorise hello persistante des fichiers. Il existe quatre types prédéfinis [TaskOutputKind][net_taskoutputkind] : `TaskOutput`, `TaskPreview`, `TaskLog`, et `TaskIntermediate.`. Vous pouvez également définir des catégories de sortie personnalisées.

Ces types de sortie permettent de toospecify le type de sorties toolist lorsque vous interrogez ultérieurement par lots pour hello persistante des sorties d’une tâche donnée. En d’autres termes, lorsque vous répertoriez les sorties hello pour une tâche, vous pouvez filtrer la liste hello sur l’un des types de sorties hello. Par exemple, « donnez-moi hello *aperçu* de sortie de tâche *109*. » Plus d’informations sur l’affichage et la récupération des sorties apparaît dans [d’extraire la sortie](#retrieve-output) plus loin dans l’article de hello.

> [!TIP]
> Hello genre de sortie également détermine l’emplacement Bonjour Azure portal un fichier particulier : *TaskOutput*-fichiers catégorisés apparaissent sous **fichiers de sortie de la tâche**, et *TaskLog*fichiers apparaissent sous **des journaux de tâches**.
> 
> 

### <a name="store-job-outputs"></a>Stocker les sorties des travaux

En outre toostoring tâche fournit en sortie, vous pouvez stocker les sorties hello associés à un travail. Par exemple, dans la tâche de fusion hello d’un travail de rendu vidéo, vous pouvez rendre les films hello entièrement rendue comme une sortie de tâche. Lorsque votre tâche est terminée, votre application cliente peut répertorier et récupèrent des sorties hello pour le travail de hello, et ne doivent pas tooquery hello tâches individuelles.

Stocker la sortie de travail en appelant hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] (méthode) et spécifiez hello [JobOutputKind] [ net_joboutputkind] et le nom de fichier :

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Comme avec hello **TaskOutputKind** type pour les sorties de la tâche, vous utilisez hello [JobOutputKind] [ net_joboutputkind] type toocategorize un travail de persistante des fichiers. Ce paramètre vous permet de requête toolater pour un type spécifique de la sortie de la (liste). Hello **JobOutputKind** type inclut les catégories de sortie et aperçu et prend en charge la création de catégories personnalisées.

### <a name="store-task-logs"></a>Stocker les journaux de tâches

En outre, toopersisting un stockage de toodurable fichier lorsqu’une tâche ou une tâche terminée, vous devrez peut-être toopersist les fichiers qui sont mis à jour pendant l’exécution d’une tâche hello du &mdash; des fichiers journaux ou `stdout.txt` et `stderr.txt`, par exemple. Dans ce but, bibliothèque de Conventions pour les fichiers par lots Azure hello fournit hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] (méthode). Avec [SaveTrackedAsync][net_savetrackedasync], vous pouvez effectuer le suivi de fichier tooa de mises à jour sur le nœud hello (à un intervalle que vous spécifiez) et conserver ces mises à jour de tooAzure stockage.

Bonjour suivant extrait de code, nous utilisons [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` dans le stockage Azure lors de l’exécution de hello de tâche hello toutes les 15 secondes :

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

Hello commenté section `Code tooprocess data and produce output file(s)` est un espace réservé pour le code hello votre tâche exécute normalement. Par exemple, vous pouvez insérer un code qui télécharge des données à partir d’Azure Storage et effectue sur celles-ci des transformations ou des calculs. Hello importante pour cet extrait de code est montrant comment vous pouvez encapsuler ce code dans un `using` bloc tooperiodically mettre à jour un fichier avec [SaveTrackedAsync][net_savetrackedasync].

l’agent du nœud Hello est un programme qui s’exécute sur chaque nœud dans le pool de hello et fournit l’interface de commande et contrôle hello entre le nœud de hello et service de traitement par lots hello. Hello `Task.Delay` appel est nécessaire à la fin de hello de ce `using` tooensure bloc qui hello agent du nœud a contenu de hello tooflush heure de la norme fichier stdout.txt de toohello sur le nœud de hello. Sans ce délai, il est possible toomiss hello dernières secondes de sortie. Ce délai n’est pas forcément requis pour tous les fichiers.

> [!NOTE]
> Lorsque vous activez le suivi des modifications avec des fichiers **SaveTrackedAsync**, seule *ajoute* fichier faisant l’objet toohello sont persistante tooAzure de stockage. Utilisez cette méthode uniquement pour les en rotation des fichiers journaux de suivi ou autres fichiers qui sont écrits toowith ajouter fin de toohello d’opérations de fichier de hello.
> 
> 

## <a name="retrieve-output-data"></a>Récupérer les données de sortie

Lorsque vous récupérez votre sortie persistante à l’aide de la bibliothèque de Conventions pour les fichiers par lots Azure hello, faire de façon centrée sur la tâche et à la tâche. Vous pouvez demander hello de sortie de tâche ou tâche sans avoir besoin de tooknow son chemin d’accès dans le stockage Azure, ou encore son nom de fichier. À la place, vous pouvez effectuer des requêtes de fichiers de sortie par ID de tâche ou travail.

Hello extrait de code suivant itère au sein des tâches d’un travail, imprime des informations sur les fichiers de sortie hello pour la tâche hello, puis télécharge les fichiers à partir du stockage.

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a>Afficher les fichiers de sortie Bonjour portail Azure

portail Azure Hello affiche les fichiers de sortie de tâche et les journaux qui sont persistante tooa liés compte de stockage Azure à l’aide de hello [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Vous pouvez implémenter ces conventions vous-même Bonjour un langage de votre choix, ou vous pouvez utiliser la bibliothèque de Conventions pour les fichiers hello dans vos applications .NET.

affichage de hello tooenable de vos fichiers de sortie dans le portail de hello, vous devez satisfaire aux hello suivant les exigences :

1. [Lier un compte de stockage Azure](#requirement-linked-storage-account) tooyour compte Batch.
2. Respecter toohello prédéfini les conventions d’affectation de noms pour les fichiers et les conteneurs de stockage lors de la persistance des sorties. Vous pouvez trouver la définition de hello de ces conventions dans bibliothèque de Conventions pour les fichiers hello [Lisez-moi][github_file_conventions_readme]. Si vous utilisez hello [Conventions pour les fichiers par lots Azure] [ nuget_package] bibliothèque toopersist votre sortie, vos fichiers sont conservés en fonction de toohello Conventions standard pour les fichiers.

fichiers de sortie de la tâche tooview et connecte hello portail Azure, accédez de tâche toohello dont la sortie vous intéressez, puis cliquez sur **enregistré les fichiers de sortie** ou **des journaux enregistrés**. Cette image montre hello **enregistré les fichiers de sortie** pour la tâche hello avec l’ID « 007 » :

![Résultats de tâches panneau Bonjour portail Azure][2]

## <a name="code-sample"></a>Exemple de code

Hello [PersistOutputs] [ github_persistoutputs] exemple de projet est un des hello [exemples de code Azure Batch] [ github_samples] sur GitHub. Cette solution Visual Studio montre comment tâche toopersist de toouse hello Azure Batch Conventions pour les fichiers bibliothèque de sortie toodurable stockage. toorun hello exemple, procédez comme suit :

1. Projet ouvert hello dans **Visual Studio 2015 ou plus récente**.
2. Ajouter votre lot et un stockage **informations d’identification de compte** trop**AccountSettings.settings** dans le projet de Microsoft.Azure.Batch.Samples.Common hello.
3. **Build** (mais ne s’exécutent pas) hello solution. Restaurez les packages NuGet si vous y êtes invité.
4. Hello d’utilisation tooupload portail Azure un [package d’application](batch-application-packages.md) pour **PersistOutputsTask**. Inclure hello `PersistOutputsTask.exe` et ses assemblys dépendants dans le package .zip de hello, ID de l’application hello ensemble trop « PersistOutputsTask » et application hello version du package trop « 1.0 ».
5. **Démarrer** hello (exécution) **PersistOutputs** projet.
6. Lorsque toochoose demandées hello persistance technologie toouse pour l’exemple hello, entrez **1** toorun hello exemple à l’aide de la sortie de la tâche hello Conventions pour les fichiers bibliothèque toopersist. 

## <a name="next-steps"></a>Étapes suivantes

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Obtenir la bibliothèque de Conventions pour les fichiers Batch hello pour .NET

bibliothèque de Conventions pour les fichiers Batch Hello pour .NET est disponible sur [NuGet][nuget_package]. bibliothèque de Hello étend hello [CloudJob] [ net_cloudjob] et [CloudTask] [ net_cloudtask] classes avec de nouvelles méthodes. Voir aussi hello [documentation de référence](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) pour la bibliothèque de Conventions pour les fichiers hello.

Hello [code source] [ github_file_conventions] hello Conventions pour les fichiers bibliothèque est disponible sur GitHub Bonjour Microsoft Azure SDK pour le référentiel de .NET. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Explorer d’autres approches de conservation des données de sortie

- Consultez [tooAzure stockage de sortie de projet de la persistance et la tâche](batch-task-output.md) pour une vue d’ensemble de la persistance des données de tâche et tâche.
- Consultez [conserver des tâches données tooAzure stockage avec hello API de lot](batch-task-output-files.md) toolearn toouse hello API de lot toopersist comment les données de sortie.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Sélecteurs Saved output files (Fichiers de sortie enregistrés) et Fichiers enregistrés dans le portail"
[2]: ./media/batch-task-output/task-output-02.png "Résultats de tâches panneau Bonjour portail Azure"
