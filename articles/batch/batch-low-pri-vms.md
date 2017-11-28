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
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="f6972-103">Utiliser des machines virtuelles de faible priorité avec Batch (préversion)</span><span class="sxs-lookup"><span data-stu-id="f6972-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="f6972-104">Traitement par lots Azure offre un coût de hello de tooreduce-priorité faible virtual machines virtuelles de charges de travail de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="f6972-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="f6972-105">Les machines virtuelles de faible priorité rendent possibles de nouveaux types de charges de travail Batch en fournissant une grande quantité de puissance de calcul qui est également rentable.</span><span class="sxs-lookup"><span data-stu-id="f6972-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="f6972-106">Les machines virtuelles de faible priorité tirent parti de la capacité excédentaire dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f6972-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="f6972-107">Lorsque vous spécifiez des machines virtuelles de faible priorité dans vos pools, Azure Batch peut utiliser automatiquement ce surplus lorsqu’il est disponible.</span><span class="sxs-lookup"><span data-stu-id="f6972-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="f6972-108">compromis Hello pour l’utilisation de machines virtuelles de faible priorité est que ces machines virtuelles peuvent être interrompus lorsque aucune capacité excédentaire n’est disponible dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f6972-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="f6972-109">Pour cette raison, les machines virtuelles de faible priorité sont plus adaptées à certains types de charges de travail.</span><span class="sxs-lookup"><span data-stu-id="f6972-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="f6972-110">Utiliser des machines virtuelles de faible priorité pour le lot et le traitement asynchrone des charges de travail où heure d’achèvement de tâche de hello est flexible et travail de hello est réparti sur plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f6972-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="f6972-111">Les machines virtuelles de faible priorité coûtent beaucoup moins cher que les machines virtuelles dédiées.</span><span class="sxs-lookup"><span data-stu-id="f6972-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="f6972-112">Pour plus d’informations sur la tarification, consultez [Tarification Batch](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="f6972-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="f6972-113">Pour une discussion plue de machines virtuelles de faible priorité, consultez l’annonce hello blog : [informatiques à une fraction du prix de hello du lot](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="f6972-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6972-114">Les machines virtuelles de faible priorité sont actuellement en préversion et sont uniquement disponibles pour les charges de travail s’exécutant dans Batch.</span><span class="sxs-lookup"><span data-stu-id="f6972-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="f6972-115">Cas d’utilisation des machines virtuelles de faible priorité</span><span class="sxs-lookup"><span data-stu-id="f6972-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="f6972-116">Étant donné les caractéristiques hello de machines virtuelles de faible priorité, les charges de travail peuvent et ne peut pas les utiliser ?</span><span class="sxs-lookup"><span data-stu-id="f6972-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="f6972-117">En règle générale, les charges de traitement par lots sont adaptées, dans la mesure où les travaux sont répartis entre plusieurs tâches parallèles, ou s’il existe de nombreux travaux montés et distribués entre plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f6972-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="f6972-118">Utilisez toomaximize de capacité excédentaire dans Azure, et convient travaux peut monter en charge.</span><span class="sxs-lookup"><span data-stu-id="f6972-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="f6972-119">Parfois les machines virtuelles ne peuvent pas être disponibles ou seront anticipés, ce qui entraîne une capacité réduite pour les travaux et peut entraîner le rediffusions et l’interruption de tootask.</span><span class="sxs-lookup"><span data-stu-id="f6972-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="f6972-120">Travaux doivent donc être flexibles dans le temps de hello qu’ils peuvent prendre toorun.</span><span class="sxs-lookup"><span data-stu-id="f6972-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="f6972-121">Les travaux avec des tâches plus longues peuvent être davantage impactés s’ils se trouvent interrompus.</span><span class="sxs-lookup"><span data-stu-id="f6972-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="f6972-122">Si des longues tâches implémentent progression toosave de points de contrôle qu’ils s’exécutent, alors l’impact de l’interruption est beaucoup moins.</span><span class="sxs-lookup"><span data-stu-id="f6972-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="f6972-123">Tâches avec des temps d’exécution plus courts ont tendance toowork mieux avec des machines virtuelles de priorité faible impact hello d’interruption est beaucoup moins.</span><span class="sxs-lookup"><span data-stu-id="f6972-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="f6972-124">Long terme des travaux MPI qui utilisent plusieurs machines virtuelles ne sont pas adapté toouse machines virtuelles de faible priorité comme une machine virtuelle préemptée seront probablement prospect toohello ensemble du projet ayant toobe exécuter à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f6972-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="f6972-125">Quelques exemples de traitement par lots toouse bien adaptés de cas sont des machines virtuelles de faible priorité, utilisez :</span><span class="sxs-lookup"><span data-stu-id="f6972-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="f6972-126">**Développement et test** : d’importantes économies peuvent être réalisées, en particulier en cas de développement de solutions à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="f6972-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="f6972-127">Tous les types de tests peuvent tirer parti de l’utilisation de machines virtuelles de faible priorité, mais les tests de charge à grande échelle et les tests de régression sont particulièrement concernés.</span><span class="sxs-lookup"><span data-stu-id="f6972-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="f6972-128">**En complément de la capacité de la demande**: machines virtuelles de faible priorité peuvent être utilisés pour compléter les regular dédié de machines virtuelles - lorsqu’il est disponible, les travaux permettre mettre à l’échelle et par conséquent se terminer plus rapidement à moindre coût ; lorsque non disponible, hello planning de référence dédié machines virtuelles sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="f6972-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="f6972-129">**Durée d’exécution de travail flexible**: s’il existe une grande souplesse dans les travaux du minuteur hello ont toocomplete, puis chutes potentielles de capacité peuvent être tolérées ; Toutefois, avec hello les plus de travaux de machines virtuelles de faible priorité seront exécutées fréquemment plus rapidement et pour un coût inférieur.</span><span class="sxs-lookup"><span data-stu-id="f6972-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="f6972-130">Pools de traitement par lots peuvent être configuré toouse VMs faible priorité de plusieurs façons, selon la souplesse de hello dans la durée d’exécution de la tâche :</span><span class="sxs-lookup"><span data-stu-id="f6972-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="f6972-131">Les machines virtuelles de faible priorité peuvent être uniquement utilisées dans un pool et Batch récupèrera simplement les capacités reportées lorsqu’elles seront disponibles.</span><span class="sxs-lookup"><span data-stu-id="f6972-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="f6972-132">Il s’agit de travaux tooexecute façon moins coûteux de hello machines virtuelles de faible priorité seulement sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="f6972-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="f6972-133">Les machines virtuelles de faible priorité peuvent être utilisées conjointement avec une ligne de base fixe de machines virtuelles dédiées.</span><span class="sxs-lookup"><span data-stu-id="f6972-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="f6972-134">Hello nombre fixe de machines virtuelles dédiées garantit qu'est toujours certaines tookeep capacité une progression du travail.</span><span class="sxs-lookup"><span data-stu-id="f6972-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="f6972-135">Il peut y avoir combinaison dynamique des machines virtuelles dédiées et une priorité basse, afin que les machines virtuelles de faible priorité moins chers sont utilisés uniquement lorsqu’il est disponible, mais les machines virtuelles de hello prix intégral dédié sont mis à l’échelle à la demande, tookeep une quantité minimale de travaux de la capacité disponible tookeep hello progression.</span><span class="sxs-lookup"><span data-stu-id="f6972-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="f6972-136">Prise en charge des machines virtuelles de faible priorité par Batch</span><span class="sxs-lookup"><span data-stu-id="f6972-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="f6972-137">Traitement par lots Azure fournit plusieurs fonctionnalités qui rendent facile tooconsume et tirer parti de machines virtuelles de faible priorité :</span><span class="sxs-lookup"><span data-stu-id="f6972-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="f6972-138">Les pools Batch peuvent contenir à la fois des machines virtuelles dédiées et des machines virtuelles de faible priorité.</span><span class="sxs-lookup"><span data-stu-id="f6972-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="f6972-139">nombre de Hello de chaque type de machine virtuelle peut être spécifié lorsqu’un pool est créé ou modifié à tout moment pour un pool existant, à l’aide d’opération de redimensionnement explicite de hello ou à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="f6972-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="f6972-140">Soumission de projet et la tâche peut rester inchangée et ne doivent pas nécessairement être concerné avec les types de machine virtuelle hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="f6972-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="f6972-141">Il est également possible de toohave un pool complètement utiliser travaux de faible priorité machines virtuelles toorun peu coûteux que possible, mais les machines virtuelles dédiées de rotation si la capacité de hello tombe sous un seuil minimal, pour conserver les travaux en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f6972-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="f6972-142">Pools de lot recherchent automatiquement toohello numéro de cible de machines virtuelles de faible priorité.</span><span class="sxs-lookup"><span data-stu-id="f6972-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="f6972-143">Si les machines virtuelles sont prévus pour, lot tentera hello tooreplace perdu la capacité et retour toohello cible.</span><span class="sxs-lookup"><span data-stu-id="f6972-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="f6972-144">Dans les cas de hello de tâches en cours d’interruption, lot détectera et automatiquement replacez toobe tâches exécuter à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f6972-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="f6972-145">Les machines virtuelles basse priorité ont un quota de cœurs différent de celui des machines virtuelles dédiées.</span><span class="sxs-lookup"><span data-stu-id="f6972-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="f6972-146">Hello devis pour les machines virtuelles de faible priorité est supérieure à celle des machines virtuelles de dédié, étant donné que les machines virtuelles de priorité faible coûtent inférieur.</span><span class="sxs-lookup"><span data-stu-id="f6972-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="f6972-147">Pour plus d’informations, consultez [Quotas et limites du service Batch](batch-quota-limit.md#resource-quotas).</span><span class="sxs-lookup"><span data-stu-id="f6972-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="f6972-148">Machines virtuelles de faible priorité ne sont pas actuellement pris en charge pour les comptes de lot où le mode d’allocation de pool hello est défini trop[abonnement utilisateur](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="f6972-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="f6972-149">Créer et mettre à jour des pools</span><span class="sxs-lookup"><span data-stu-id="f6972-149">Create and update pools</span></span>

<span data-ttu-id="f6972-150">Un pool de traitement par lots peut contenir des machines virtuelles de dédié et une priorité basse (également désignées tooas nœuds de calcul).</span><span class="sxs-lookup"><span data-stu-id="f6972-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="f6972-151">Vous pouvez définir le nombre de cible de hello de nœuds de calcul pour les machines virtuelles dédiées et une priorité basse.</span><span class="sxs-lookup"><span data-stu-id="f6972-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="f6972-152">nombre de hello spécifie Hello nombre cible de nœuds de machines virtuelles, vous souhaitez toohave dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="f6972-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="f6972-153">Par exemple, toocreate un pool à l’aide de machines virtuelles de service cloud Azure avec une cible de 5 dédié machines virtuelles et 20 ordinateurs virtuels de faible priorité :</span><span class="sxs-lookup"><span data-stu-id="f6972-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="f6972-154">toocreate un pool à l’aide de machines virtuelles (dans ce cas, les machines virtuelles Linux) avec une cible de 5 dédié des machines virtuelles et 20 ordinateurs virtuels de faible priorité :</span><span class="sxs-lookup"><span data-stu-id="f6972-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

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

<span data-ttu-id="f6972-155">Vous pouvez obtenir le nombre actuel de hello de nœuds pour les machines virtuelles dédiées et une priorité basse :</span><span class="sxs-lookup"><span data-stu-id="f6972-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="f6972-156">Les nœuds de pool ont une propriété tooindicate si le nœud de hello est un ordinateur de virtuel dédié ou à faible priorité :</span><span class="sxs-lookup"><span data-stu-id="f6972-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="f6972-157">Lorsqu’un ou plusieurs nœuds dans un pool sont prévus pour, une opération de nœuds de liste sur le pool retourne toujours ces nœuds, nombre actuel de hello de nœuds de faible priorité reste inchangée, mais ces nœuds ont leur état défini toothe **anticipé**état.</span><span class="sxs-lookup"><span data-stu-id="f6972-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="f6972-158">Lot va tenter de remplacement de toofind machines virtuelles et, en cas de réussite, les nœuds hello verrons **création** , puis **départ** États avant de devenir disponible pour l’exécution de la tâche, comme les nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="f6972-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="f6972-159">Mettre à l’échelle un pool contenant des machines virtuelles de faible priorité</span><span class="sxs-lookup"><span data-stu-id="f6972-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="f6972-160">Comme pools constitué uniquement d’ordinateurs virtuels dédiés, il est possible tooscale une pool contenant faible priorité VMs en appelant la méthode de redimensionnement hello ou à l’aide de l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="f6972-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="f6972-161">opération de redimensionnement de pool Hello prend un paramètre facultatif deuxième qui met à jour la valeur de **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="f6972-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="f6972-162">formule de Hello pool à l’échelle automatique prend en charge les machines virtuelles de faible priorité comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6972-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="f6972-163">Vous pouvez obtenir ou hello la valeur de variable défini par le service de hello **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="f6972-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="f6972-164">Vous pouvez obtenir la valeur hello de variable défini par le service de hello **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="f6972-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="f6972-165">Vous pouvez obtenir la valeur hello de variable défini par le service de hello **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="f6972-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="f6972-166">Cette variable retourne le nombre de hello de nœuds de hello prévus pour état et permet d’augmenter ou diminuer le nombre de hello de nœuds dédiés, selon le nombre de hello de nœuds préemptés qui ne sont pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="f6972-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="f6972-167">Travaux et tâches</span><span class="sxs-lookup"><span data-stu-id="f6972-167">Jobs and tasks</span></span>

<span data-ttu-id="f6972-168">Projets et des tâches nécessitent très peu de prise en charge pour les nœuds de faible priorité ; prend en charge uniquement de Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6972-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="f6972-169">Hello propriété JobManagerTask d’une tâche a une nouvelle propriété, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="f6972-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="f6972-170">Lorsque cette propriété est true, tâche hello du gestionnaire peut être planifié sur un nœud dédié ou à faible priorité.</span><span class="sxs-lookup"><span data-stu-id="f6972-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="f6972-171">Si cette propriété a la valeur false, tâche du gestionnaire hello sera planifiée tooa nœud dédié uniquement.</span><span class="sxs-lookup"><span data-stu-id="f6972-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="f6972-172">Un [variable d’environnement](batch-compute-node-environment-variables.md) est disponible tooa d’application de tâches afin qu’elle peut déterminer si elle est en cours d’exécution sur un nœud de priorité basse ou dédié.</span><span class="sxs-lookup"><span data-stu-id="f6972-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="f6972-173">variable d’environnement Hello est AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="f6972-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="f6972-174">Gestion de préemption</span><span class="sxs-lookup"><span data-stu-id="f6972-174">Handling preemption</span></span>

<span data-ttu-id="f6972-175">Machines virtuelles peuvent parfois être anticipés ; Dans ce cas, lot hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f6972-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="f6972-176">machines virtuelles préemptés Hello ont leur état mis à jour trop**anticipé**.</span><span class="sxs-lookup"><span data-stu-id="f6972-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="f6972-177">Si les tâches en cours d’exécution hello prévus pour machines virtuelles de nœud, ces tâches sont remis et exécutez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f6972-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="f6972-178">Hello machine virtuelle est supprimé, tooany les données stockées localement sur hello perte de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f6972-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="f6972-179">pool de Hello tente continuellement le nombre de cibles tooreach hello de nœuds de faible priorité disponibles.</span><span class="sxs-lookup"><span data-stu-id="f6972-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="f6972-180">Une fois la capacité de remplacement trouvée, les nœuds conservent leur ID, mais ils sont réinitialisés. Ils passent par les états **Création** et **Démarrage** avant d’être disponibles pour la planification des tâches.</span><span class="sxs-lookup"><span data-stu-id="f6972-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="f6972-181">Nombres de préemption sont disponibles en tant que métrique Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f6972-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="f6972-182">Mesures</span><span class="sxs-lookup"><span data-stu-id="f6972-182">Metrics</span></span>

<span data-ttu-id="f6972-183">Nouvelles mesures sont disponibles dans hello [portail Azure](https://portal.azure.com) pour les nœuds de faible priorité.</span><span class="sxs-lookup"><span data-stu-id="f6972-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="f6972-184">Ces mesures sont :</span><span class="sxs-lookup"><span data-stu-id="f6972-184">These metrics are:</span></span>

- <span data-ttu-id="f6972-185">Nombre de nœuds à priorité basse</span><span class="sxs-lookup"><span data-stu-id="f6972-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="f6972-186">Nombre de cœurs à priorité basse</span><span class="sxs-lookup"><span data-stu-id="f6972-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="f6972-187">Nombre de nœuds reportés</span><span class="sxs-lookup"><span data-stu-id="f6972-187">Preempted Node Count</span></span>

<span data-ttu-id="f6972-188">métriques tooview Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="f6972-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="f6972-189">Accédez tooyour compte Batch dans le portail de hello et afficher les paramètres de hello pour votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="f6972-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="f6972-190">Sélectionnez **métriques** de hello **analyse** section.</span><span class="sxs-lookup"><span data-stu-id="f6972-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="f6972-191">Sélectionner des mesures hello souhaité à partir de hello **métriques disponibles** liste.</span><span class="sxs-lookup"><span data-stu-id="f6972-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![Mesures pour les nœuds de priorité basse](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="f6972-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6972-193">Next steps</span></span>

* <span data-ttu-id="f6972-194">Hello de lecture [vue d’ensemble de lot pour les développeurs](batch-api-basics.md), des informations essentielles pour toute personne préparation toouse lot.</span><span class="sxs-lookup"><span data-stu-id="f6972-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="f6972-195">Hello contient des informations détaillées sur les ressources du service de traitement par lots comme pools, nœuds, travaux, tâches et des hello nombreuses fonctionnalités de l’API que vous pouvez utiliser lors de la génération de votre application de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="f6972-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="f6972-196">En savoir plus sur hello [outils et API de lot](batch-apis-tools.md) disponibles pour la création de solutions de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="f6972-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
