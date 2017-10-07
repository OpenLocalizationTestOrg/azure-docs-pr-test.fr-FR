---
title: "les charges de travail Azure Batch aaaRun sur des machines virtuelles de faible priorité économiques (version préliminaire) | Documents Microsoft"
description: "Découvrez comment hello de tooreduce de machines virtuelles de faible priorité tooprovision coût des charges de travail de traitement par lots Azure."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>Utiliser des machines virtuelles de faible priorité avec Batch (préversion)

Traitement par lots Azure offre un coût de hello de tooreduce-priorité faible virtual machines virtuelles de charges de travail de traitement par lots. Les machines virtuelles de faible priorité rendent possibles de nouveaux types de charges de travail Batch en fournissant une grande quantité de puissance de calcul qui est également rentable.

Les machines virtuelles de faible priorité tirent parti de la capacité excédentaire dans Azure. Lorsque vous spécifiez des machines virtuelles de faible priorité dans vos pools, Azure Batch peut utiliser automatiquement ce surplus lorsqu’il est disponible.

compromis Hello pour l’utilisation de machines virtuelles de faible priorité est que ces machines virtuelles peuvent être interrompus lorsque aucune capacité excédentaire n’est disponible dans Azure. Pour cette raison, les machines virtuelles de faible priorité sont plus adaptées à certains types de charges de travail. Utiliser des machines virtuelles de faible priorité pour le lot et le traitement asynchrone des charges de travail où heure d’achèvement de tâche de hello est flexible et travail de hello est réparti sur plusieurs machines virtuelles.

Les machines virtuelles de faible priorité coûtent beaucoup moins cher que les machines virtuelles dédiées. Pour plus d’informations sur la tarification, consultez [Tarification Batch](https://azure.microsoft.com/pricing/details/batch/).

Pour une discussion plue de machines virtuelles de faible priorité, consultez l’annonce hello blog : [informatiques à une fraction du prix de hello du lot](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Les machines virtuelles de faible priorité sont actuellement en préversion et sont uniquement disponibles pour les charges de travail s’exécutant dans Batch. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Cas d’utilisation des machines virtuelles de faible priorité

Étant donné les caractéristiques hello de machines virtuelles de faible priorité, les charges de travail peuvent et ne peut pas les utiliser ? En règle générale, les charges de traitement par lots sont adaptées, dans la mesure où les travaux sont répartis entre plusieurs tâches parallèles, ou s’il existe de nombreux travaux montés et distribués entre plusieurs machines virtuelles.

-   Utilisez toomaximize de capacité excédentaire dans Azure, et convient travaux peut monter en charge.

-   Parfois les machines virtuelles ne peuvent pas être disponibles ou seront anticipés, ce qui entraîne une capacité réduite pour les travaux et peut entraîner le rediffusions et l’interruption de tootask. Travaux doivent donc être flexibles dans le temps de hello qu’ils peuvent prendre toorun.

-   Les travaux avec des tâches plus longues peuvent être davantage impactés s’ils se trouvent interrompus. Si des longues tâches implémentent progression toosave de points de contrôle qu’ils s’exécutent, alors l’impact de l’interruption est beaucoup moins. Tâches avec des temps d’exécution plus courts ont tendance toowork mieux avec des machines virtuelles de priorité faible impact hello d’interruption est beaucoup moins.

-   Long terme des travaux MPI qui utilisent plusieurs machines virtuelles ne sont pas adapté toouse machines virtuelles de faible priorité comme une machine virtuelle préemptée seront probablement prospect toohello ensemble du projet ayant toobe exécuter à nouveau.

Quelques exemples de traitement par lots toouse bien adaptés de cas sont des machines virtuelles de faible priorité, utilisez :

-   **Développement et test** : d’importantes économies peuvent être réalisées, en particulier en cas de développement de solutions à grande échelle. Tous les types de tests peuvent tirer parti de l’utilisation de machines virtuelles de faible priorité, mais les tests de charge à grande échelle et les tests de régression sont particulièrement concernés.

-   **En complément de la capacité de la demande**: machines virtuelles de faible priorité peuvent être utilisés pour compléter les regular dédié de machines virtuelles - lorsqu’il est disponible, les travaux permettre mettre à l’échelle et par conséquent se terminer plus rapidement à moindre coût ; lorsque non disponible, hello planning de référence dédié machines virtuelles sont disponibles.

-   **Durée d’exécution de travail flexible**: s’il existe une grande souplesse dans les travaux du minuteur hello ont toocomplete, puis chutes potentielles de capacité peuvent être tolérées ; Toutefois, avec hello les plus de travaux de machines virtuelles de faible priorité seront exécutées fréquemment plus rapidement et pour un coût inférieur.

Pools de traitement par lots peuvent être configuré toouse VMs faible priorité de plusieurs façons, selon la souplesse de hello dans la durée d’exécution de la tâche :

-   Les machines virtuelles de faible priorité peuvent être uniquement utilisées dans un pool et Batch récupèrera simplement les capacités reportées lorsqu’elles seront disponibles. Il s’agit de travaux tooexecute façon moins coûteux de hello machines virtuelles de faible priorité seulement sont utilisés.

-   Les machines virtuelles de faible priorité peuvent être utilisées conjointement avec une ligne de base fixe de machines virtuelles dédiées. Hello nombre fixe de machines virtuelles dédiées garantit qu'est toujours certaines tookeep capacité une progression du travail.

-   Il peut y avoir combinaison dynamique des machines virtuelles dédiées et une priorité basse, afin que les machines virtuelles de faible priorité moins chers sont utilisés uniquement lorsqu’il est disponible, mais les machines virtuelles de hello prix intégral dédié sont mis à l’échelle à la demande, tookeep une quantité minimale de travaux de la capacité disponible tookeep hello progression.

## <a name="batch-support-for-low-priority-vms"></a>Prise en charge des machines virtuelles de faible priorité par Batch

Traitement par lots Azure fournit plusieurs fonctionnalités qui rendent facile tooconsume et tirer parti de machines virtuelles de faible priorité :

-   Les pools Batch peuvent contenir à la fois des machines virtuelles dédiées et des machines virtuelles de faible priorité. nombre de Hello de chaque type de machine virtuelle peut être spécifié lorsqu’un pool est créé ou modifié à tout moment pour un pool existant, à l’aide d’opération de redimensionnement explicite de hello ou à l’échelle automatique. Soumission de projet et la tâche peut rester inchangée et ne doivent pas nécessairement être concerné avec les types de machine virtuelle hello dans le pool de hello. Il est également possible de toohave un pool complètement utiliser travaux de faible priorité machines virtuelles toorun peu coûteux que possible, mais les machines virtuelles dédiées de rotation si la capacité de hello tombe sous un seuil minimal, pour conserver les travaux en cours d’exécution.

-   Pools de lot recherchent automatiquement toohello numéro de cible de machines virtuelles de faible priorité. Si les machines virtuelles sont prévus pour, lot tentera hello tooreplace perdu la capacité et retour toohello cible.

-   Dans les cas de hello de tâches en cours d’interruption, lot détectera et automatiquement replacez toobe tâches exécuter à nouveau.

-   Les machines virtuelles basse priorité ont un quota de cœurs différent de celui des machines virtuelles dédiées. 
    Hello devis pour les machines virtuelles de faible priorité est supérieure à celle des machines virtuelles de dédié, étant donné que les machines virtuelles de priorité faible coûtent inférieur. Pour plus d’informations, consultez [Quotas et limites du service Batch](batch-quota-limit.md#resource-quotas).    

> [!NOTE]
> Machines virtuelles de faible priorité ne sont pas actuellement pris en charge pour les comptes de lot où le mode d’allocation de pool hello est défini trop[abonnement utilisateur](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Créer et mettre à jour des pools

Un pool de traitement par lots peut contenir des machines virtuelles de dédié et une priorité basse (également désignées tooas nœuds de calcul). Vous pouvez définir le nombre de cible de hello de nœuds de calcul pour les machines virtuelles dédiées et une priorité basse. nombre de hello spécifie Hello nombre cible de nœuds de machines virtuelles, vous souhaitez toohave dans le pool de hello.

Par exemple, toocreate un pool à l’aide de machines virtuelles de service cloud Azure avec une cible de 5 dédié machines virtuelles et 20 ordinateurs virtuels de faible priorité :

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

toocreate un pool à l’aide de machines virtuelles (dans ce cas, les machines virtuelles Linux) avec une cible de 5 dédié des machines virtuelles et 20 ordinateurs virtuels de faible priorité :

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

Vous pouvez obtenir le nombre actuel de hello de nœuds pour les machines virtuelles dédiées et une priorité basse :

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

Les nœuds de pool ont une propriété tooindicate si le nœud de hello est un ordinateur de virtuel dédié ou à faible priorité :

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Lorsqu’un ou plusieurs nœuds dans un pool sont prévus pour, une opération de nœuds de liste sur le pool retourne toujours ces nœuds, nombre actuel de hello de nœuds de faible priorité reste inchangée, mais ces nœuds ont leur état défini toothe **anticipé**état. Lot va tenter de remplacement de toofind machines virtuelles et, en cas de réussite, les nœuds hello verrons **création** , puis **départ** États avant de devenir disponible pour l’exécution de la tâche, comme les nouveaux nœuds.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Mettre à l’échelle un pool contenant des machines virtuelles de faible priorité

Comme pools constitué uniquement d’ordinateurs virtuels dédiés, il est possible tooscale une pool contenant faible priorité VMs en appelant la méthode de redimensionnement hello ou à l’aide de l’échelle automatique.

opération de redimensionnement de pool Hello prend un paramètre facultatif deuxième qui met à jour la valeur de **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

formule de Hello pool à l’échelle automatique prend en charge les machines virtuelles de faible priorité comme suit :

-   Vous pouvez obtenir ou hello la valeur de variable défini par le service de hello **$TargetLowPriorityNodes**.

-   Vous pouvez obtenir la valeur hello de variable défini par le service de hello **$CurrentLowPriorityNodes**.

-   Vous pouvez obtenir la valeur hello de variable défini par le service de hello **$PreemptedNodeCount**. 
    Cette variable retourne le nombre de hello de nœuds de hello prévus pour état et permet d’augmenter ou diminuer le nombre de hello de nœuds dédiés, selon le nombre de hello de nœuds préemptés qui ne sont pas disponibles.

## <a name="jobs-and-tasks"></a>Travaux et tâches

Projets et des tâches nécessitent très peu de prise en charge pour les nœuds de faible priorité ; prend en charge uniquement de Hello est comme suit :

-   Hello propriété JobManagerTask d’une tâche a une nouvelle propriété, **AllowLowPriorityNode**. 
    Lorsque cette propriété est true, tâche hello du gestionnaire peut être planifié sur un nœud dédié ou à faible priorité. Si cette propriété a la valeur false, tâche du gestionnaire hello sera planifiée tooa nœud dédié uniquement.

-   Un [variable d’environnement](batch-compute-node-environment-variables.md) est disponible tooa d’application de tâches afin qu’elle peut déterminer si elle est en cours d’exécution sur un nœud de priorité basse ou dédié. variable d’environnement Hello est AZ_BATCH_NODE_IS_DEDICATED.

## <a name="handling-preemption"></a>Gestion de préemption

Machines virtuelles peuvent parfois être anticipés ; Dans ce cas, lot hello suivant :

-   machines virtuelles préemptés Hello ont leur état mis à jour trop**anticipé**.
-   Si les tâches en cours d’exécution hello prévus pour machines virtuelles de nœud, ces tâches sont remis et exécutez à nouveau.
-   Hello machine virtuelle est supprimé, tooany les données stockées localement sur hello perte de machine virtuelle.
-   pool de Hello tente continuellement le nombre de cibles tooreach hello de nœuds de faible priorité disponibles. Une fois la capacité de remplacement trouvée, les nœuds conservent leur ID, mais ils sont réinitialisés. Ils passent par les états **Création** et **Démarrage** avant d’être disponibles pour la planification des tâches.
-   Nombres de préemption sont disponibles en tant que métrique Bonjour portail Azure.

## <a name="metrics"></a>Mesures

Nouvelles mesures sont disponibles dans hello [portail Azure](https://portal.azure.com) pour les nœuds de faible priorité. Ces mesures sont :

- Nombre de nœuds à priorité basse
- Nombre de cœurs à priorité basse 
- Nombre de nœuds reportés

métriques tooview Bonjour portail Azure :

1. Accédez tooyour compte Batch dans le portail de hello et afficher les paramètres de hello pour votre compte Batch.
2. Sélectionnez **métriques** de hello **analyse** section.
3. Sélectionner des mesures hello souhaité à partir de hello **métriques disponibles** liste.

![Mesures pour les nœuds de priorité basse](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Étapes suivantes

* Hello de lecture [vue d’ensemble de lot pour les développeurs](batch-api-basics.md), des informations essentielles pour toute personne préparation toouse lot. Hello contient des informations détaillées sur les ressources du service de traitement par lots comme pools, nœuds, travaux, tâches et des hello nombreuses fonctionnalités de l’API que vous pouvez utiliser lors de la génération de votre application de traitement par lots.
* En savoir plus sur hello [outils et API de lot](batch-apis-tools.md) disponibles pour la création de solutions de traitement par lots.
