---
title: "aaaMonitor de progression d’une tâche en comptant les tâches par état - Azure Batch | Documents Microsoft"
description: "Surveiller la progression de hello d’un travail en appelant l’opération d’obtenir le nombre de tâches hello toocount tâches pour un travail. Vous pouvez obtenir un nombre de tâches actives, en cours d’exécution et terminées et selon que les tâches ont réussi ou échoué."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Nombre de tâches par état toomonitor l’avancement d’une tâche (version préliminaire)

Traitement par lots Azure fournit une manière efficace toomonitor hello de progression d’une tâche lorsqu’elle s’exécute ses tâches. Vous pouvez appeler hello [obtenir le nombre de tâches] [ rest_get_task_counts] toofind opération le nombre de tâches est dans un état actif, en cours d’exécution ou terminé, et combien ont réussi ou échoué. En comptant le nombre de hello de tâches dans chaque état, vous pouvez plus facilement afficher l’utilisateur de tooa de progression du travail hello ou détecter des retards inattendus ou des échecs qui peuvent affecter les travaux hello.

> [!IMPORTANT]
> Bonjour opération d’obtenir le nombre de tâches est actuellement en version préliminaire et n’est pas encore disponible dans Azure Government Azure Chine et Azure situés en Allemagne. 
>
>

## <a name="how-tasks-are-counted"></a>Comptage des tâches

Hello opération d’obtenir le nombre de tâches compte les tâches par état, comme suit :

- Une tâche est comptée comme **active** quand il est toorun en file d’attente et en mesure, mais n’est pas actuellement affecté tooa de nœud de calcul. Une tâche est également comptée comme **active** si elle dépend d’une tâche parente qui n’est pas encore terminée. Pour plus d’informations sur les dépendances de tâche, consultez [toorun les tâches qui dépendent d’autres tâches de créer des interdépendances](batch-task-dependencies.md). 
- Une tâche est comptée comme **en cours d’exécution** quand il a été affecté tooa de nœud de calcul, mais n’est pas encore terminée. Une tâche est comptée comme **en cours d’exécution** lorsque son état est `preparing` ou `running`, comme indiqué par hello [obtenir des informations sur une tâche] [ rest_get_task] opération.
- Une tâche est comptée comme **terminé** quand il n’est plus toorun éligible. Une tâche comptée comme **terminée** est une tâche qui s’est généralement déroulée correctement ou qui a échoué et a épuisé par ailleurs son nombre maximal de tentatives. 

Hello opération d’obtenir le nombre de tâches signale également le nombre de tâches ayant a réussi ou échoué. Traitement par lots détermine si une tâche a réussi ou échoué en vérifiant hello **résultat** propriété Hello [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] propriété :

    - Une tâche est comptée comme **a réussi** si le résultat de hello d’exécution de la tâche est `success`.
    - Une tâche est comptée comme **échec** si le résultat de hello d’exécution de la tâche est `failure`.

Pour plus d’informations sur les états des tâches, consultez [Obtenir des informations sur une tâche][rest_get_task].

Hello .NET code exemple suivant montre comment les tâches tooretrieve nombres par état : 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> Vous pouvez utiliser un modèle semblable pour REST et autres langages pris en charge tooget tâche compte pour un travail. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>Vérification de la cohérence des nombres de tâches

service de traitement par lots Hello agrège les nombres de la tâche en collectant des données à partir de plusieurs parties d’un système distribué asynchrone. tooensure que les nombres de la tâche sont corrects, lot fournit une validation supplémentaire pour les États comptes en effectuant des vérifications de cohérence par rapport à plusieurs composants du système de hello. Lot effectue ces vérifications de cohérence tant qu’il existe moins de 200 000 tâches dans la tâche de hello. Hello improbable que la vérification de cohérence hello trouve des erreurs, lot corrige le résultat de hello d’opération d’obtenir le nombre de tâches hello basée sur les résultats de hello hello de vérification de cohérence. Bonjour la vérification de cohérence est une tooensure mesure supplémentaire que les clients qui s’appuient sur hello obtenir le nombre de tâches l’opération obtiennent des informations de droit hello que dont ils ont besoin pour leur solution.

Hello **validationStatus** propriété dans la réponse de hello indique si lot a effectué la vérification de cohérence hello. Si le lot n’a pas été en mesure de toocheck des nombres d’état contre les États réel hello contenues dans le système de hello, puis hello **validationStatus** propriété a la valeur trop`unvalidated`. Pour des raisons de performances, traitement par lots n’effectuera pas si le travail hello inclut la vérification de cohérence hello plus de 200 000 tâches, c’est le cas hello **validationStatus** propriété peut être définie trop`unvalidated` dans ce cas. Toutefois, nombre de tâches hello n’est pas nécessairement incorrect dans ce cas, même une perte de données très limité est très improbable. 

Lorsqu’une tâche change d’état, pipeline de d’agrégation hello traite les modifications de hello dans quelques secondes. Hello opération d’obtenir le nombre de tâches reflète le nombre de tâches hello mis à jour dans ce délai. Toutefois, si une modification dans un état de la tâche des absences dans le pipeline d’agrégation hello, puis modification n’est pas inscrit jusqu'à ce que le test de validation suivant hello. Pendant ce temps, le nombre de tâches peut-être être légèrement erroné en raison de l’événement de manquées toohello, mais elles sont corrigées dans le test de validation suivant hello.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>Bonnes pratiques pour le comptage des tâches d’un travail

L’appel d’opération d’obtenir le nombre de tâches hello est tooreturn de façon plus efficace hello un décompte de base des tâches d’un travail par état. Si vous utilisez la version du service de traitement par lots 2017-06-01.5.1, nous vous recommandons d’écrire ou de mise à jour de votre toouse code obtenir le nombre de tâches.

Hello opération d’obtenir le nombre de tâches n’est pas disponible dans les versions de service de traitement par lots 2017-06-01.5.1 au plus tôt. Si vous utilisez une version antérieure du service de hello, puis utilisez une liste des tâches toocount requête dans un travail à la place. Pour plus d’informations, consultez [créer efficacement les ressources de traitement par lots toolist requêtes](batch-efficient-list-queries.md).

## <a name="next-steps"></a>Étapes suivantes

* Consultez hello [vue d’ensemble de lot](batch-api-basics.md) toolearn plus d’informations sur les fonctionnalités et les concepts du service de traitement par lots. Hello article traite des ressources de traitement principales hello tels que les pools, les nœuds de calcul, les opérations et les tâches et fournit une vue d’ensemble des fonctionnalités du service hello.
* Principes fondamentaux du développement d’une application activée de lot à l’aide de hello hello [bibliothèque cliente .NET de lot](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md). Ces articles d’introduction vous guident dans une application opérationnelle qui utilise hello lot service tooexecute une charge de travail sur plusieurs nœuds de calcul.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
