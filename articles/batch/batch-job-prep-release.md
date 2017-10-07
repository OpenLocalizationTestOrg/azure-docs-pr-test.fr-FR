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
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Exécuter des tâches de préparation et de validation du travail sur les nœuds de calcul Batch

 Un travail Azure Batch nécessite souvent une certaine forme de préparation avant l’exécution de ses tâches, ainsi qu’une maintenance ultérieure une fois les tâches terminées. Que vous deviez nœuds de calcul du tooyour des données d’entrée de la tâche commune toodownload, ou télécharger tooAzure de données de sortie tâche stockage une fois hello travail terminé. Vous pouvez utiliser **préparation de la tâche** et **mise en production de la tâche** tâches tooperform ces opérations.

## <a name="what-are-job-preparation-and-release-tasks"></a>En quoi consistent les tâches de préparation et de validation du travail ?
Avant l’exécution de tâches d’un projet, tâche de préparation du travail hello s’exécute sur tous les toorun planifiée nœuds de calcul au moins une tâche. Une fois le travail de hello est terminé, version de tâche hello s’exécute sur chaque nœud dans le pool de hello exécutée au moins une tâche. Comme avec les tâches de traitement normal, vous pouvez spécifier un toobe de ligne de commande appelé lorsqu’une tâche de préparation du ou des tâches de mise en production sont exécutée.

Les tâches de préparation et de validation du travail offrent des fonctionnalités de tâche Batch courantes, telles que téléchargement de fichiers ([fichiers de ressources][net_job_prep_resourcefiles]), exécution avec élévation de privilèges, variables d’environnement personnalisées, durée d’exécution maximale, nombre de tentatives et période de rétention des fichiers.

Bonjour les sections suivantes, vous allez apprendre comment toouse hello [JobPreparationTask] [ net_job_prep] et [JobReleaseTask] [ net_job_release] classes trouvées dans hello [Batch .NET] [ api_net] bibliothèque.

> [!TIP]
> Les tâches de préparation et de validation du travail sont particulièrement utiles dans les environnements de « pool partagé », dans lesquels un pool de nœuds de calcul persiste entre les exécutions d’un travail et est utilisé par de nombreux travaux.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Lorsque toouse préparation du travail et tâches
Préparation du travail et les tâches de mise en production sont adaptées pour hello suivant situations :

**Télécharger les données de tâche communes**

Traitements par lots nécessitent souvent un ensemble commun de données comme entrée pour les tâches du travail hello. Par exemple, dans les calculs de l’analyse des risques quotidiennes, les données de marché sont spécifiques à un projet, mais courantes tâches tooall travail de hello. Ces données de marché, souvent plusieurs gigaoctets, la taille doivent être téléchargé tooeach de nœud de calcul qu’une seule fois afin que toutes les tâches qui s’exécute sur le nœud de hello peuvent l’utiliser. Utilisez un **tâche de préparation** toodownload ce nœud tooeach de données avant l’exécution de hello du travail de hello's d’autres tâches.

**Supprimer la sortie des travaux et des tâches**

Dans un environnement « shared pool », où les nœuds de calcul d’un pool ne sont pas retirés entre les travaux, vous devrez peut-être les données entre les exécutions de la tâche toodelete. Vous devrez peut-être tooconserve espace disque sur les nœuds hello ou répondre aux stratégies de sécurité de votre organisation. Utilisez un **version tâche** toodelete les données qui ont été téléchargées par une tâche de préparation ou générées pendant l’exécution de tâches.

**Rétention des journaux**

Vous souhaiterez peut-être tookeep une copie de fichiers journaux qui génèrent de vos tâches, ou peut-être les fichiers de vidage sur incident qui peuvent être générés par les applications ayant échouées. Utilisez un **version tâche** dans ces cas de toocompress et télécharger ce tooan données [Azure Storage] [ azure_storage] compte.

> [!TIP]
> Une autre façon toopersist journaux de travail et d’autres tâches sortie de données sont toouse hello [Conventions pour les fichiers par lots Azure](batch-task-output.md) bibliothèque.
> 
> 

## <a name="job-preparation-task"></a>tâche de préparation du travail
Avant l’exécution de tâches d’un projet, Batch exécute la tâche de préparation du travail hello sur chaque nœud de calcul qui est planifiée toorun une tâche. Par défaut, hello service Batch attend hello travail préparation tâche toobe est terminée avant d’exécuter tooexecute de hello tâches planifiées sur le nœud de hello. Toutefois, vous pouvez configurer le service de hello toowait pas. Si le nœud de hello redémarre, hello préparation tâche s’exécute à nouveau, mais vous pouvez également désactiver ce comportement.

tâche de préparation du travail Hello est exécutée uniquement sur les nœuds qui sont planifiée toorun une tâche. Cela empêche l’exécution d’inutiles d’hello d’une tâche de préparation dans le cas où un nœud ne possède pas d’une tâche. Cela peut se produire lorsque le nombre de hello de tâches pour un travail est inférieur au nombre de hello de nœuds dans un pool de. Il s’applique également si [l’exécution de tâches simultanées](batch-parallel-node-tasks.md) est activé, qui laisse certains nœuds inactive si nombre de tâches hello est inférieur à tâches simultanées possibles total hello. En tâche de préparation du travail hello n’exécutant ne pas sur les nœuds inactifs, vous pouvez consacrer moins d’argent sur les frais de transfert de données.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] diffère [CloudPool.StartTask] [ pool_starttask] dans la mesure où JobPreparationTask s’exécute au démarrage de hello de chaque travail, tandis que StartTask s’exécute uniquement lorsqu’un nœud de calcul joint tout d’abord un pool ou redémarre.
> 
> 

## <a name="job-release-task"></a>tâche de validation du travail
Une fois qu’une tâche est marquée comme terminée, la mise en production tâche hello est exécutée sur chaque nœud dans le pool hello exécutées au moins une tâche. Vous marquez un travail comme terminé en émettant une requête de fin. Hello service Batch puis jeux hello état de la tâche trop*fin*, met fin à toutes les tâches actives ou en cours d’exécution associés au travail de hello et exécute la tâche de mise en production de projet hello. travail de Hello déplace ensuite toohello *terminé* état.

> [!NOTE]
> Suppression de travail exécute également la mise en production tâche hello. Toutefois, si un travail a déjà été arrêté, tâche de mise en production hello n'est pas exécutée une deuxième fois si la tâche de hello est supprimé ultérieurement.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Tâches de préparation et de validation du travail avec Batch.NET
toouse une tâche de préparation du travail, affecter une [JobPreparationTask] [ net_job_prep] la tâche objet tooyour [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] propriété . De même, initialiser un [JobReleaseTask] [ net_job_release] et l’assigner du travail tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] hello tooset de propriété tâche de mise en production de la tâche.

Dans cet extrait de code, `myBatchClient` est une instance de [BatchClient][net_batch_client], et `myPool` est un pool existant au sein de hello compte Batch.

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

Comme mentionné précédemment, la tâche de mise en production de hello est exécutée lorsqu’un travail est terminé ou supprimé. Pour arrêter un travail, utilisez [JobOperations.TerminateJobAsync][net_job_terminate]. Pour supprimer un travail, utilisez [JobOperations.DeleteJobAsync][net_job_delete]. Généralement, vous arrêtez ou supprimez un travail lorsque les tâches de ce dernier sont terminées ou qu’un délai d’expiration que vous avez défini a été atteint.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Exemple de code sur GitHub
tâches de préparation et de la version de projet dans action, toosee extraire hello [JobPrepRelease] [ job_prep_release_sample] exemple de projet sur GitHub. Cette application de console hello suivant :

1. Crée un pool avec deux « petits » nœuds.
2. Crée un travail avec des tâches de préparation du travail, de validation et standard.
3. S’exécute hello tâche Préparation du travail, qui écrit d’abord le fichier texte tooa hello nœud ID dans le répertoire de « partagé » d’un nœud.
4. Exécute une tâche sur chaque nœud qui écrit son toohello d’ID de tâche même fichier texte.
5. Une fois que toutes les tâches sont terminées (ou du délai de hello), imprime le contenu hello console de toohello de fichier de texte de chaque nœud.
6. À la fin du travail hello, exécute le fichier hello de toodelete la tâche hello travail version à partir du nœud de hello.
7. Hello d’imprime les codes de préparation du travail hello de sortie et libérer des tâches pour chaque nœud sur lequel ils exécutée.
8. Confirmation de tooallow suspend l’exécution de suppression de travail et/ou de pool.

Sortie de l’exemple d’application hello est similaire toohello suivantes :

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
> Échéance toohello variable création et heure de début de nœuds dans un nouveau pool (certains nœuds sont prêts pour les tâches avant les autres), vous pouvez voir une sortie différente. Plus précisément, étant donné que les tâches de hello s’achèvent rapidement, un des nœuds du pool hello peut exécuter toutes les tâches du travail hello. Si cela se produit, vous pouvez remarquer que hello préparation du travail et de tâches n’existent pas pour le nœud hello exécutées aucune tâche.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>Inspectez la préparation du travail et des tâches de mise en production de hello portail Azure
Lorsque vous exécutez exemple d’application hello, vous pouvez utiliser hello [portail Azure] [ portal] tooview hello les propriétés du travail de hello et ses tâches, ou même télécharger de fichier partagé texte hello est modifié par les tâches du travail hello.

Hello capture d’écran ci-dessous montre hello **Panneau de tâches de préparation** Bonjour Azure portal après une exécution de l’exemple d’application hello. Accédez toohello *JobPrepReleaseSampleJob* propriétés une fois les tâches terminées (mais avant de supprimer votre travail et le pool) et cliquez sur **tâches de préparation** ou **detâches** tooview leurs propriétés.

![Propriétés de préparation du travail dans le portail Azure][1]

## <a name="next-steps"></a>Étapes suivantes
### <a name="application-packages"></a>packages d’application
Dans la tâche de préparation du travail de toohello de plus, vous pouvez également utiliser hello [les packages d’applications](batch-application-packages.md) nœuds pour l’exécution de la tâche de calcul de la fonctionnalité de traitement par lots tooprepare. Cette fonctionnalité est particulièrement utile pour déployer des applications qui ne nécessitent pas de programme d’installation, des applications qui contiennent de nombreux fichiers (plus de 100) ou des applications qui requièrent un contrôle de version strict.

### <a name="installing-applications-and-staging-data"></a>Installation d’applications et de données intermédiaires
Le billet MSDN ci-après fournit une vue d’ensemble de différentes méthodes de préparation de vos nœuds à l’exécution des tâches :

[Installing applications and staging data on Batch compute nodes][forum_post] (Installation d’applications et de données intermédiaires sur les nœuds de calcul Batch)

Écrit par un des membres de l’équipe Azure Batch hello, il présente plusieurs techniques que vous pouvez utiliser des nœuds de toocompute des applications et des données toodeploy.

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
