---
title: "les requêtes de liste efficace aaaDesign - Azure Batch | Documents Microsoft"
description: "Améliorez les performances en filtrant vos requêtes lorsque vous demandez des informations sur des ressources Batch comme les pools, les travaux, les tâches et les nœuds de calcul."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a>Créer efficacement les ressources de traitement par lots toolist des requêtes

Ici, vous allez apprendre comment tooincrease les performances de votre application Azure Batch en réduisant la quantité de hello de données qui sont retournées par le service de hello lorsque vous interrogez des travaux, des tâches et les nœuds de calcul avec hello [Batch .NET] [ api_net] bibliothèque.

Presque toutes les applications de traitement par lots doivent tooperform un type de contrôle ou autre opération qui interroge le service de traitement par lots de hello, souvent à intervalles réguliers. Par exemple, toodetermine indique s’il existe des tâches en file d’attente restant dans un travail, vous devez obtenir des données sur chaque tâche dans la tâche de hello. état de hello toodetermine de nœuds dans le pool, vous devez obtenir données sur chaque nœud dans le pool de hello. Cet article explique comment tooexecute ces requêtes Bonjour moyen le plus efficace.

> [!NOTE]
> Hello service Batch fournit la prise en charge spéciale des API pour le scénario courant de hello de comptage des tâches dans un projet. Au lieu d’utiliser une requête de liste dans ce cas, vous pouvez appeler hello [obtenir le nombre de tâches] [ rest_get_task_counts] opération. L’opération Obtenir le nombre de tâches indique le nombre de tâches en attente, en cours d’exécution ou terminées, ainsi que le nombre de tâches ayant réussi ou échoué. L’opération Obtenir le nombre de tâches est plus efficace qu’une requête de liste. Pour plus d’informations, consultez [Compter les tâches d’un travail par état (préversion)](batch-get-task-counts.md). 
>
> Hello opération d’obtenir le nombre de tâches n’est pas disponible dans les versions de service de traitement par lots 2017-06-01.5.1 au plus tôt. Si vous utilisez une version antérieure du service de hello, puis utilisez une liste des tâches toocount requête dans un travail à la place.
>
> 

## <a name="meet-hello-detaillevel"></a>Hello satisfont à niveau de détail
Dans une application de traitement de production, des entités telles que les travaux, les tâches et les nœuds de calcul peuvent numéro Bonjour des milliers. Lorsque vous demandez des informations sur ces ressources, une quantité volumineuse de données « établissant câble de hello » à partir de l’application tooyour de hello lot service sur chaque requête. En limitant le nombre de hello d’éléments et le type d’informations retournées par une requête, vous pouvez augmenter la vitesse de hello de vos requêtes et hello par conséquent les performances de votre application.

Cela [Batch .NET] [ api_net] listes d’extrait de code API *chaque* tâche qui est associée à un travail, avec *tous les* de propriétés hello de chaque tâche :

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

Vous pouvez effectuer une requête de liste beaucoup plus efficace, toutefois, en appliquant une requête tooyour « niveau de détail ». Pour cela, vous devez fournir un [ODATADetailLevel] [ odata] objet toohello [JobOperations.ListTasks] [ net_list_tasks] (méthode). Cet extrait retourne uniquement l’ID de hello, ligne de commande et propriétés d’informations de nœud de calcul de tâches terminées :

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

Dans cet exemple de scénario, s’il existe des milliers de tâches dans la tâche de hello, hello résultats à partir de la deuxième requête de hello généralement seront renvoyées beaucoup plus rapidement que hello en premier. Vous trouverez plus d’informations sur l’utilisation de ODATADetailLevel liste des éléments par hello API .NET de lot [ci-dessous](#efficient-querying-in-batch-net).

> [!IMPORTANT]
> Il est fortement recommandé que vous *toujours* fournissez une liste d’API .NET tooyour ODATADetailLevel objet appelle tooensure une efficacité maximale et les performances de votre application. En spécifiant un niveau de détail, vous pouvez aider toolower temps de réponse du lot, améliorer l’utilisation du réseau et réduire l’utilisation de la mémoire par les applications clientes.
> 
> 

## <a name="filter-select-and-expand"></a>Filtrer, sélectionner et développer
Hello [Batch .NET] [ api_net] et [lot reste] [ api_rest] API fournissent des éléments qui sont renvoyés dans une liste, à la fois nombre hello hello capacité tooreduce ainsi que hello quantité d’informations retournées pour chacun. Pour ce faire, spécifiez des chaînes **filter**, **select** et **expand** lors de l’exécution des requêtes de liste.

### <a name="filter"></a>Filtrer
chaîne de filtrage Hello est une expression qui réduit le nombre de hello d’éléments qui sont retournés. Par exemple, liste uniquement hello en cours d’exécution des tâches pour un travail ou liste seuls nœuds de calcul qui sont des tâches toorun prêt.

* chaîne de filtrage Hello se compose d’une ou plusieurs expressions, avec une expression qui se compose d’un nom de propriété, un opérateur et une valeur. propriétés Hello qui peuvent être spécifiées sont type d’entité tooeach spécifique que vous interrogez, comme les opérateurs hello qui sont pris en charge pour chaque propriété.
* Plusieurs expressions peuvent être combinées à l’aide des opérateurs logiques de hello `and` et `or`.
* Cet exemple montre comment filtrer des listes de chaîne uniquement les tâches hello en cours d’exécution « afficher » : `(state eq 'running') and startswith(id, 'renderTask')`.

### <a name="select"></a>Sélectionnez
select la chaîne Hello limite les valeurs de propriété hello qui sont retournées pour chaque élément. Vous spécifiez une liste de noms de propriétés, et seules les valeurs de propriété sont retournées pour les éléments de hello dans les résultats de la requête hello.

* chaîne de select Hello se compose d’une liste séparée par des virgules de noms de propriétés. Vous pouvez spécifier une des propriétés hello pour le type d’entité hello que vous interrogez.
* Cet exemple de chaîne select spécifie que seules trois valeurs de propriété doivent être retournées pour chaque tâche : `id, state, stateTransitionTime`.

### <a name="expand"></a>Développez
Hello développez chaîne allège hello d’appels d’API qui sont requis tooobtain certaines informations. Lorsque vous utilisez une chaîne expand, vous pouvez obtenir davantage d'informations sur chaque élément avec un seul appel d'API. Au lieu de la première obtention hello la liste des entités, puis demander des informations pour chaque élément de liste de hello, vous utilisez une chaîne de développer tooobtain hello les mêmes informations dans un seul appel d’API. Plus le nombre d'appels d'API est faible, plus les performances sont élevées.

* Chaîne sélectionnez toohello semblable, hello développer les contrôles de chaîne si certaines données sont incluses dans les résultats de requête de liste.
* Hello développez chaîne est uniquement pris en charge lorsqu’elle est utilisée dans la liste des travaux, des planifications de travaux, des tâches et des pools. Actuellement, elle ne prend en charge que les informations statistiques.
* Lorsque toutes les propriétés sont requises, et aucune chaîne select est spécifiée, hello développez chaîne *doit* être tooget utilisé les informations statistiques. Si une chaîne de sélection est tooobtain utilisé un sous-ensemble de propriétés, puis `stats` peut être spécifié dans la chaîne de sélection hello et hello développez chaîne toobe spécifié n’a pas besoin.
* Cet exemple montre comment étendre la chaîne spécifie que les informations statistiques doivent être retournées pour chaque élément de liste de hello : `stats`.

> [!NOTE]
> Lors de la construction des hello trois types de chaîne de requête (filtre, sélectionnez et développez), vous devez vous assurer que les noms de propriété hello et des cas correspondent à celles de leurs équivalents d’élément d’API REST. Par exemple, lorsque vous travaillez avec hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) (classe), vous devez spécifier **état** au lieu de **état**, même si hello propriété .NET est [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state). Consultez les tableaux de hello ci-dessous pour les mappages de propriété entre hello API .NET et REST.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>Règles des chaînes filter, select et expand
* Les noms de propriétés de filtre, sélectionnez et développez les chaînes doivent apparaître comme dans hello [lot reste] [ api_rest] API--même lorsque vous utilisez [Batch .NET] [ api_net] ou l’un des hello autres kits de développement de lot.
* Les noms de propriété respectent la casse contrairement aux valeurs de propriété.
* Les chaînes de date/heure peuvent être d’un format ou de l’autre et doivent être précédées de `DateTime`.
  
  * Exemple de format W3C-DTF : `creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * Exemple de format RFC 1123 : `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* Les chaînes booléennes ont la valeur `true` ou `false`.
* Si une propriété ou un opérateur non valide est spécifié, une erreur `400 (Bad Request)` se produit.

## <a name="efficient-querying-in-batch-net"></a>Interrogation efficace dans Batch.NET
Au sein de hello [Batch .NET] [ api_net] API, hello [ODATADetailLevel] [ odata] classe est utilisée pour fournir le filtre, sélectionnez et développez les chaînes opérations de toolist. Hello ODataDetailLevel classe possède trois propriétés publiques de chaîne qui peuvent être spécifiées dans le constructeur de hello ou définir directement sur l’objet de hello. Vous passez ensuite hello ODataDetailLevel objet comme un paramètre toohello diverses opérations de liste tel que [ListPools][net_list_pools], [ListJobs][net_list_jobs], et [ListTasks][net_list_tasks].

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: limiter le nombre de hello d’éléments qui sont retournés.
* [ODATADetailLevel][odata].[SelectClause][odata_select] : spécifie les valeurs de propriétés retournées avec chaque élément.
* [ODATADetailLevel][odata].[ExpandClause][odata_expand] : récupère les données de tous les éléments en utilisant un seul appel d’API et non des appels distincts pour chaque élément.

Hello extrait de code suivant utilise service Batch hello API .NET de lot tooefficiently requête hello pour les statistiques de hello d’un ensemble spécifique de pools de. Dans ce scénario, utilisateur de lot hello a des pools de test et de production. pool de test Hello ID sont précédés de « test », et le regroupement de production hello ID sont précédés de « production ». Dans l’extrait de code hello, *myBatchClient* est une instance initialisée correctement de hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) classe.

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> Une instance de [ODATADetailLevel] [ odata] qui est configuré avec Select et des clauses de développement peuvent également être transmis les méthodes Get tooappropriate tels que [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , montant de hello toolimit de données qui sont retournée.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>Mappages REST too.NET API de lot
Les noms de propriété dans les chaînes filter, select et expand *doivent* refléter leurs homologues dans l’API REST, aussi bien au niveau du nom que de la casse. tables Hello ci-dessous fournissent des mappages entre hello .NET et les API REST.

### <a name="mappings-for-filter-strings"></a>Mappages pour les chaînes filter
* **Répertorier les méthodes .NET**: chacune des méthodes d’API .NET hello dans cette colonne accepte une [ODATADetailLevel] [ odata] objet en tant que paramètre.
* **Liste de demandes REST**: API REST de chaque page tooin lié, cette colonne contient une table qui spécifie les propriétés de hello et les opérations qui est autorisée dans *filtre* chaînes. Vous devez utiliser ces noms de propriétés et ces opérations lors de la construction d’une chaîne [ODATADetailLevel.FilterClause][odata_filter].

| Méthodes de liste .NET | Requêtes de liste REST |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[Liste des certificats hello dans un compte][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[Liste des fichiers hello associés à une tâche][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Répertorier l’état de préparation du travail hello et tâches de mise en production d’une tâche hello][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[Liste des travaux hello dans un compte][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[Liste des fichiers sur un nœud hello][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[Liste des tâches hello associés à un travail][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[Liste des planifications de travaux hello dans un compte][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[Liste des travaux hello associés à une planification de travail][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[Hello de la liste des nœuds de calcul dans un pool][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[Liste des pools de hello d’un compte][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>Mappages pour les chaînes select
* **Types .NET Batch**: types d’API .NET Batch.
* **Entités de l’API REST**: chaque page dans cette colonne contient une ou plusieurs tables qui répertorient les noms de propriété hello API REST pour le type de hello. Ces noms de propriétés sont utilisés lorsque vous construisez des chaînes *select* . Vous devez utiliser ces mêmes noms de propriétés lors de la construction d’une chaîne [ODATADetailLevel.SelectClause][odata_select].

| Types .NET Batch | Entités de l’API REST |
| --- | --- |
| [Certificate][net_cert] |[Obtenir des informations sur un certificat][rest_get_cert] |
| [CloudJob][net_job] |[Obtenir des informations sur un travail][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[Obtenir des informations sur la planification d’un travail][rest_get_schedule] |
| [ComputeNode][net_node] |[Obtenir des informations sur un nœud][rest_get_node] |
| [CloudPool][net_pool] |[Obtenir des informations sur un pool][rest_get_pool] |
| [CloudTask][net_task] |[Obtenir des informations sur une tâche][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>Exemple : Construire une chaîne filter
Lorsque vous construisez une chaîne de filtre pour [ODATADetailLevel.FilterClause][odata_filter], consultez le tableau hello ci-dessus sous « Mappages pour les chaînes de filtre » toofind hello API REST page de la documentation correspondant opération de liste toohello que vous souhaitez tooperform. Vous trouverez les propriétés filtrables hello et leurs opérateurs pris en charge dans la première table multilignes hello sur cette page. Si vous le souhaitez tooretrieve toutes les tâches dont le code de sortie était différent de zéro, par exemple, cette ligne sur [liste des tâches hello associées à un travail] [ rest_list_tasks] spécifie la chaîne de la propriété applicable hello et opérateurs autorisées :

| Propriété | Opérations autorisées | Type |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

Par conséquent, chaîne de filtre hello pour répertorier toutes les tâches avec un code de sortie différent de zéro serait :

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>Exemple : Construire une chaîne select
tooconstruct [ODATADetailLevel.SelectClause][odata_select], consultez la table hello ci-dessus sous « Mappages pour les chaînes de sélection » et de naviguer page API REST toohello correspondant de type toohello de l’entité que vous avez Répertoriez. Vous trouverez les propriétés pouvant être hello et leurs opérateurs pris en charge dans la première table multilignes hello sur cette page. Si vous souhaitez tooretrieve uniquement hello ID et la ligne de commande pour chaque tâche dans une liste, par exemple, vous trouverez ces lignes dans la table d’applicable hello sur [obtenir des informations sur une tâche][rest_get_task]:

| Propriété | Type | Remarques |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

select la chaîne Hello pour inclure uniquement les ID hello et ligne de commande avec chaque tâche dans la liste serait alors :

`id, commandLine`

## <a name="code-samples"></a>Exemples de code
### <a name="efficient-list-queries-code-sample"></a>Exemple de code pour des requêtes de liste efficaces
Extraire hello [EfficientListQueries] [ efficient_query_sample] exemple de projet sur GitHub toosee de l’efficacité interrogation de la liste peut affecter les performances dans une application. Cette application de console c# crée et ajoute un grand nombre de travaux tooa de tâches. Ensuite, il effectue plusieurs appels toohello [JobOperations.ListTasks] [ net_list_tasks] méthode et passe [ODATADetailLevel] [ odata] les objets qui sont configuré avec la propriété différentes valeurs toovary hello quantité toobe des données retournée. Il génère suivant toohello similaire de sortie :

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

Comme indiqué dans le temps hello, vous pouvez réduire considérablement les temps de réponse en limitant les propriétés hello et nombre de hello d’éléments qui sont retournés. Vous pouvez trouver cette et autres exemples de projets dans hello [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub.

### <a name="batchmetrics-library-and-code-sample"></a>Bibliothèque BatchMetrics et exemple de code
Exemple de code EfficientListQueries toohello ci-dessus, vous pouvez également trouver hello [BatchMetrics] [ batch_metrics] projet Bonjour [exemples de traitement par lots azure] [ github_samples] Référentiel GitHub. exemple de projet Hello BatchMetrics montre comment tooefficiently surveiller la progression du travail à l’aide des API de lot de hello Azure Batch.

Hello [BatchMetrics] [ batch_metrics] exemple inclut un projet de bibliothèque de classes .NET qui vous pouvez incorporer dans vos projets et une simple ligne de commande du programme tooexercise et illustre l’utilisation de hello Hello bibliothèque.

exemple d’application Hello dans le projet de hello illustre hello opérations suivantes :

1. Sélection des attributs spécifiques dans les propriétés de hello seul ordre toodownload vous avez besoin
2. Le filtrage sur les temps de transition d’état dans toodownload de commande modifie uniquement depuis la dernière requête de hello

Par exemple, hello méthode apparaît Bonjour BatchMetrics bibliothèque. Elle retourne un ODATADetailLevel qui spécifie que seul hello `id` et `state` propriétés doivent être obtenues pour les entités de hello sont interrogées. Il spécifie également que seules les entités dont l’état a changé depuis hello spécifié `DateTime` paramètre doit être retourné.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>Étapes suivantes
### <a name="parallel-node-tasks"></a>Tâches parallèles de nœud
[Optimiser l’utilisation des ressources calcul Azure Batch avec les tâches simultanées nœud](batch-parallel-node-tasks.md) est un autre article liées tooBatch des performances des applications. Certains types de charge de travail peuvent tirer parti de l’exécution de tâches parallèles sur des nœuds de calcul plus volumineux, mais moins nombreux. Extraire hello [exemple de scénario](batch-parallel-node-tasks.md#example-scenario) dans l’article hello pour plus d’informations sur ce scénario.

### <a name="batch-forum"></a>Forum Azure Batch
Hello [Forum de traitement par lots Azure] [ forum] sur MSDN est une bonne placer toodiscuss lot et poser des questions sur le service de hello. Consultez le forum pour obtenir des publications « permanentes » utiles et publiez les questions que vous vous posez pendant la création de vos solutions Batch.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

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

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job