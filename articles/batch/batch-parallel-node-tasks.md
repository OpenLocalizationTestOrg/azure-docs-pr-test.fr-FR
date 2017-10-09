---
title: "tâches parallèle toouse aaaRun ressources de calcul Azure Batch efficacement - | Documents Microsoft"
description: "Améliorer l’efficacité et réduire les coûts en utilisant moins de nœuds de calcul et en exécutant des tâches simultanées sur chaque nœud dans un pool Azure Batch"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Exécuter des tâches simultanément l’utilisation de toomaximize lot de nœuds de calcul 

En exécutant plusieurs tâches simultanément sur chaque nœud de calcul dans le pool de traitement par lots Azure, vous pouvez optimiser l’utilisation des ressources sur un plus petit nombre de nœuds dans le pool de hello. Pour certaines charges de travail, vous obtiendrez ainsi des durées de travail réduites et un coût inférieur.

Alors que certains scénarios de tirer parti de dédier la totalité de la seule tâche d’un nœud ressources tooa, plusieurs situations bénéficient de ce qui permet à plusieurs tâches tooshare ces ressources :

* **Réduire le transfert de données** lorsque les tâches sont en mesure de tooshare données. Dans ce scénario, vous pouvez réduire les frais de transfert de données en copiant les données partagées tooa plus petit nombre de nœuds et de l’exécution de tâches en parallèle sur chaque nœud. Cela s’applique en particulier si le nœud de hello données toobe tooeach copiées doit être transféré entre les régions géographiques.
* **Optimisation de l’utilisation de la mémoire** lorsque les tâches nécessitent une grande quantité de mémoire, mais seulement pendant de courtes périodes et à des moments variables au cours de l’exécution. Vous pouvez employer moins, mais la plus grande, de calcul des nœuds avec tooefficiently de mémoire plus gérer ces pics. Ces nœuds devrait avoir plusieurs tâches en cours d’exécution en parallèle sur chaque nœud, mais chaque tâche bénéficie de mémoire abondante de nœuds hello à des moments différents.
* **Atténuation des limites au nombre de nœuds** lorsque la communication entre les nœuds est requise au sein d’un pool. Actuellement, les pools configurés pour la communication entre les nœuds sont des nœuds de calcul too50 limité. Si chaque nœud dans un pool de ce type est en mesure de tooexecute les tâches en parallèle, un plus grand nombre de tâches pouvant être exécuté simultanément.
* **Réplication d’un cluster de calcul local**, par exemple lorsque vous commencez par déplacer un tooAzure d’environnement de calcul. Si votre solution sur site en cours s’exécute plusieurs tâches par nœud de calcul, vous pouvez augmenter le nombre maximal de hello des tâches de nœuds toomore reflètent précisément que la configuration.

## <a name="example-scenario"></a>Exemple de scénario
Comme un tooillustrate exemple hello les avantages de l’exécution de tâches parallèles, supposons que votre application de la tâche a processeur et de mémoire que [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nœuds sont suffisantes. Toutefois, dans le travail de hello ordre toofinish dans le temps de hello requis, 1 000 de ces nœuds sont nécessaires.

Au lieu d’utiliser les nœuds Standard\_D1 avec 1 cœur de processeur, vous pouvez utiliser des nœuds [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) avec 16 cœurs chacun, et activer l’exécution de tâches parallèles. Vous pouvez donc utiliser *16 fois moins de nœuds* : à la place des 1 000 nœuds, seuls 63 sont requis. En outre, si les fichiers d’application de grande taille ou des données de référence sont requises pour chaque nœud, l’efficacité et la durée du travail sont à nouveau améliorées hello les données étant copiées tooonly 16 nœuds.

## <a name="enable-parallel-task-execution"></a>Activer l’exécution des tâches parallèles
Vous configurez les nœuds de calcul pour l’exécution de la tâche parallèle au niveau du pool hello. Avec la bibliothèque de lot .NET hello, définissez hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propriété lorsque vous créez un pool. Si vous utilisez l’API REST de traitement par lots de hello, définissez hello [maxTasksPerNode] [ rest_addpool] élément dans le corps de la demande hello lors de la création du pool.

Traitement par lots Azure vous permet de tooset nombre maximum de tâches par nœud de toofour fois (x 4) hello nombre de cœurs de nœud. Par exemple, si hello pool est configuré avec les nœuds de taille « Grande » (quatre cœurs), puis `maxTasksPerNode` peut avoir la valeur too16. Pour plus d’informations sur le nombre hello de cœurs pour chacun des tailles de nœud hello, consultez [tailles pour les Services de Cloud](../cloud-services/cloud-services-sizes-specs.md). Pour plus d’informations sur les limites de service, consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md).

> [!TIP]
> Être vraiment tootake dans hello du compte `maxTasksPerNode` valeur lorsque vous construisez une [formule de mise à l’échelle] [ enable_autoscaling] pour votre pool. Par exemple, une formule qui évalue `$RunningTasks` pourrait être considérablement affectée par une augmentation des tâches par nœud. Consultez [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](batch-automatic-scaling.md) pour plus d’informations.
>
>

## <a name="distribution-of-tasks"></a>Répartition des tâches
Lorsque les nœuds de calcul hello dans un pool peuvent exécuter des tâches simultanément, il est important toospecify comment vous souhaitez que toobe de tâches hello répartis entre les nœuds hello dans le pool de hello.

À l’aide de hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] propriété, vous pouvez spécifier que les tâches doivent être assignées uniformément entre tous les nœuds dans le pool hello (« propagation »). Ou vous pouvez spécifier que les tâches autant que possible doivent être assignées tooeach nœud avant que les tâches sont assignées nœud tooanother pool hello (« compression »).

Prenons un exemple de comment cette fonctionnalité est utile, pool hello de [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nœuds (dans l’exemple hello ci-dessus) qui est configuré avec un [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] valeur 16. Si hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] est configuré avec un [ComputeNodeFillType] [ fill_type] de *Pack*, il optimiser l’utilisation de toutes les 16 noyaux de chaque nœud et autoriser une [échelle pool](batch-automatic-scaling.md) tooprune les nœuds inutilisés de pool de hello (nœuds sans toutes les tâches affectées). Ceci limite l'utilisation des ressources et permet d'économiser de l'argent.

## <a name="batch-net-example"></a>Exemple .NET Batch
Cela [Batch .NET] [ api_net] API de code montre une toocreate demande un pool qui contient les quatre nœuds de grande taille avec un maximum de quatre tâches par nœud. Elle spécifie une stratégie qui remplit chaque nœud tâches antérieures tooassigning tâches tooanother nœud du pool de hello de planification des tâches. Pour plus d’informations sur l’ajout de pools à l’aide de hello API .NET de traitement par lots, consultez [BatchClient.PoolOperations.CreatePool][poolcreate_net].

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a>Exemple REST Batch
Cela [lot reste] [ api_rest] API montre un toocreate demande un pool qui contient deux nœuds de grande taille avec un maximum de quatre tâches par nœud. Pour plus d’informations sur l’ajout de pools à l’aide de hello API REST, consultez [ajouter un compte du pool de tooan][rest_addpool].

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> Vous pouvez définir hello `maxTasksPerNode` élément et [MaxTasksPerComputeNode] [ maxtasks_net] propriété uniquement au moment de la création du pool. Ils ne peuvent pas être modifiés après qu'un pool a déjà été créé.
>
>

## <a name="code-sample"></a>Exemple de code
Hello [ParallelNodeTasks] [ parallel_tasks_sample] projet sur GitHub illustre l’utilisation de hello de hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propriété.

Cette application de console c# utilise hello [Batch .NET] [ api_net] toocreate de bibliothèque un pool avec un ou plusieurs nœuds de calcul. Il exécute un nombre configurable de tâches sur ces nœuds toosimulate la charge variable. Sortie de l’application hello spécifie les nœuds exécuté chaque tâche. application Hello fournit également un résumé des paramètres de la tâche hello et la durée. partie de résumé Hello de sortie hello de deux exécutions différentes de l’application d’exemple hello s’affiche ci-dessous.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

première exécution de Hello de l’exemple d’application hello montre que, avec un nœud unique dans le pool de hello et paramètre hello par défaut est une tâche par nœud, la durée du travail hello est plus de 30 minutes.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

Hello deuxième exécution de l’exemple hello montre une diminution considérable de la durée du travail. Il s’agit, car le pool de hello a été configurée avec quatre tâches par nœud, ce qui permet de travail de tâche parallèle d’exécution toocomplete hello dans près d’un quart de temps de hello.

> [!NOTE]
> durées de travail Hello dans des résumés d’hello ci-dessus n’incluent pas l’heure de création du pool. Chacune des tâches hello ci-dessus a été soumis toopreviously créé les pools dont les nœuds de calcul ont été Bonjour *inactif* état au moment de l’envoi.
>
>

## <a name="next-steps"></a>Étapes suivantes
### <a name="batch-explorer-heat-map"></a>Carte thermique Batch Explorer
Hello [Azure Batch Explorer][batch_explorer], un des hello Azure Batch [exemples d’applications][github_samples], contient un *cartethermique* fonctionnalité qui fournit la visualisation de l’exécution de la tâche. Lorsque vous avez exécuté l’hello [ParallelTasks] [ parallel_tasks_sample] exemple d’application, vous pouvez utiliser hello thermique fonctionnalité tooeasily visualiser l’exécution de hello de tâches en parallèle sur chaque nœud.

![Carte thermique Batch Explorer][1]

*Carte thermique Batch Explorer affichant un pool de quatre nœuds, chaque nœud exécutant quatre tâches*

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
