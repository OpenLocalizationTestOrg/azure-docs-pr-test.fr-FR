---
title: ReliableConcurrentQueue dans Azure Service Fabric
description: "ReliableConcurrentQueue est une file d’attente à débit élevé qui permet des mises en file d’attente et retraits de file d’attente parallèles."
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 122cb48149477f295a65b8ee623c647b6db10a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="0605d-103">Présentation de ReliableConcurrentQueue dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0605d-103">Introduction to ReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="0605d-104">Une file d’attente simultanée fiable est une file d’attente asynchrone, transactionnelle et répliquée, qui permet d’effectuer des opérations de mise en file d’attente et de retrait de file d’attente avec un niveau élevé de simultanéité.</span><span class="sxs-lookup"><span data-stu-id="0605d-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="0605d-105">Elle est conçue pour offrir un débit élevé et une latence faible en assouplissant la séquence stricte de premier entré, premier sorti fournie par une [file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx), et fournit à la place un classement selon le principe de l’effort optimal.</span><span class="sxs-lookup"><span data-stu-id="0605d-105">It is designed to deliver high throughput and low latency by relaxing the strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="0605d-106">API</span><span class="sxs-lookup"><span data-stu-id="0605d-106">APIs</span></span>

|<span data-ttu-id="0605d-107">File d’attente simultanée</span><span class="sxs-lookup"><span data-stu-id="0605d-107">Concurrent Queue</span></span>                |<span data-ttu-id="0605d-108">File d’attente simultanée fiable</span><span class="sxs-lookup"><span data-stu-id="0605d-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="0605d-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="0605d-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="0605d-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="0605d-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="0605d-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="0605d-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="0605d-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="0605d-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="0605d-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="0605d-113">int Count()</span></span>                    | <span data-ttu-id="0605d-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="0605d-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="0605d-115">Comparaison avec un [File d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="0605d-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="0605d-116">Une file d’attente simultanée fiable est proposée en guise d’alternative à une [file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="0605d-116">Reliable Concurrent Queue is offered as an alternative to [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="0605d-117">Elle doit être utilisée dans les cas où la séquence stricte de premier entré, premier sorti n’est pas requise, celle-ci nécessitant un compromis sur le plan de la simultanéité.</span><span class="sxs-lookup"><span data-stu-id="0605d-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="0605d-118">Une [File d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) utilise des verrous pour appliquer la séquence de premier entré, premier sorti, avec au plus une transaction autorisée pour la mise en file d’attente et une transaction autorisée pour le retrait de file d’attente à la fois.</span><span class="sxs-lookup"><span data-stu-id="0605d-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks to enforce FIFO ordering, with at most one transaction allowed to enqueue and at most one transaction allowed to dequeue at a time.</span></span> <span data-ttu-id="0605d-119">En comparaison, une file d’attente simultanée fiable assouplit la contrainte de séquence et permet qu’un nombre quelconque de transactions simultanées entrelacent leurs opérations de mise en file d’attente et de retrait de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-119">In comparison, Reliable Concurrent Queue relaxes the ordering constraint and allows any number concurrent transactions to interleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="0605d-120">Un classement selon le principe de l’effort optimal est fourni, mais l’ordre relatif de deux valeurs dans une file d’attente simultanée fiable ne peut jamais être garanti.</span><span class="sxs-lookup"><span data-stu-id="0605d-120">Best-effort ordering is provided, however the relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="0605d-121">Une file d’attente simultanée fiable offre un débit supérieur et une latence moindre qu’une [file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) chaque fois que plusieurs transactions simultanées effectuent des mises en file d’attente ou des retraits de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="0605d-122">Un exemple de cas d’utilisation de ReliableConcurrentQueue est le scénario de la [File d’attente des messages](https://en.wikipedia.org/wiki/Message_queue).</span><span class="sxs-lookup"><span data-stu-id="0605d-122">A sample use case for the ReliableConcurrentQueue is the [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="0605d-123">Dans ce scénario, un ou plusieurs producteurs de messages créent et ajoutent des éléments à la file d’attente, et un ou plusieurs consommateurs de messages extraient des messages de la file d’attente et les traitent.</span><span class="sxs-lookup"><span data-stu-id="0605d-123">In this scenario, one or more message producers create and add items to the queue, and one or more message consumers pull messages from the queue and process them.</span></span> <span data-ttu-id="0605d-124">Plusieurs producteurs et consommateurs peuvent travailler de façon indépendante, en utilisant des transactions simultanées pour traiter la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-124">Multiple producers and consumers can work independently, using concurrent transactions in order to process the queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="0605d-125">Instructions d’utilisation</span><span class="sxs-lookup"><span data-stu-id="0605d-125">Usage Guidelines</span></span>
* <span data-ttu-id="0605d-126">La file d’attente attend que la période de rétention des éléments qu’elle contient soit courte.</span><span class="sxs-lookup"><span data-stu-id="0605d-126">The queue expects that the items in the queue have a low retention period.</span></span> <span data-ttu-id="0605d-127">Autrement dit, ces éléments ne sont pas supposés rester longtemps dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-127">That is, the items would not stay in the queue for a long time.</span></span>
* <span data-ttu-id="0605d-128">La file d’attente ne garantit pas le respect strict de la séquence de premier entré, premier sorti.</span><span class="sxs-lookup"><span data-stu-id="0605d-128">The queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="0605d-129">La file d’attente ne lit pas ses propres écritures.</span><span class="sxs-lookup"><span data-stu-id="0605d-129">The queue does not read its own writes.</span></span> <span data-ttu-id="0605d-130">Si un élément est mis en file d’attente dans le cadre d’une transaction, il n’est pas visible pour un retrait de file d’attente dans le cadre de la même transaction.</span><span class="sxs-lookup"><span data-stu-id="0605d-130">If an item is enqueued within a transaction, it will not be visible to a dequeuer within the same transaction.</span></span>
* <span data-ttu-id="0605d-131">Les retraits de file d’attente ne sont pas isolés les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="0605d-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="0605d-132">Si un élément *A* est retiré d’une file d’attente dans le cadre d’une transaction *txnA*, même si la transaction *txnA* n’est pas validée, l’élément *A* n’est pas visible pour une transaction simultanée *txnB*.</span><span class="sxs-lookup"><span data-stu-id="0605d-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible to a concurrent transaction *txnB*.</span></span>  <span data-ttu-id="0605d-133">Si la transaction *txnA* est abandonnée, l’élément *A* devient immédiatement visible pour la transaction *txnB*.</span><span class="sxs-lookup"><span data-stu-id="0605d-133">If *txnA* aborts, *A* will become visible to *txnB* immediately.</span></span>
* <span data-ttu-id="0605d-134">Le comportement *TryPeekAsync* peut être implémenté à l’aide de *TryDequeueAsync* puis abandonner la transaction.</span><span class="sxs-lookup"><span data-stu-id="0605d-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="0605d-135">Cela est illustré dans la section Modèles de programmation.</span><span class="sxs-lookup"><span data-stu-id="0605d-135">An example of this can be found in the Programming Patterns section.</span></span>
* <span data-ttu-id="0605d-136">Count est non transactionnel.</span><span class="sxs-lookup"><span data-stu-id="0605d-136">Count is non-transactional.</span></span> <span data-ttu-id="0605d-137">Il peut être utilisé pour obtenir une idée du nombre d’éléments présents dans la file d’attente, mais représente un point dans le temps non fiable.</span><span class="sxs-lookup"><span data-stu-id="0605d-137">It can be used to get an idea of the number of elements in the queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="0605d-138">Un traitement coûteux sur les éléments retirés de la file d’attente ne doit pas être effectué pendant que la transaction est active, afin d’éviter des transactions à long terme qui peuvent avoir une incidence sur les performances du système.</span><span class="sxs-lookup"><span data-stu-id="0605d-138">Expensive processing on the dequeued items should not be performed while the transaction is active, to avoid long-running transactions which may have a performance impact on the system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="0605d-139">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="0605d-139">Code Snippets</span></span>
<span data-ttu-id="0605d-140">Examinons quelques extraits de code et leurs sorties attendues.</span><span class="sxs-lookup"><span data-stu-id="0605d-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="0605d-141">La gestion des exceptions est ignorée dans cette section.</span><span class="sxs-lookup"><span data-stu-id="0605d-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="0605d-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="0605d-142">EnqueueAsync</span></span>
<span data-ttu-id="0605d-143">Voici quelques extraits de code pour l’utilisation d’EnqueueAsync, suivis de leurs sorties attendues.</span><span class="sxs-lookup"><span data-stu-id="0605d-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="0605d-144">*Cas 1 : tâche de mise en file d’attente unique*</span><span class="sxs-lookup"><span data-stu-id="0605d-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="0605d-145">Supposons que la tâche s’est achevée correctement et qu’aucune transaction simultanée ne modifiait la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-145">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="0605d-146">L’utilisateur peut s’attendre à ce que la file d’attente contienne les éléments dans n’importe lequel des ordres suivants :</span><span class="sxs-lookup"><span data-stu-id="0605d-146">The user can expect the queue to contain the items in any of the following orders:</span></span>

> <span data-ttu-id="0605d-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="0605d-147">10, 20</span></span>

> <span data-ttu-id="0605d-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="0605d-148">20, 10</span></span>


- <span data-ttu-id="0605d-149">*Cas 2 : tâche de mise en file d’attente parallèle*</span><span class="sxs-lookup"><span data-stu-id="0605d-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="0605d-150">Supposons que les tâches aient été accomplies avec succès, qu’elles aient été exécutées en parallèle et qu’aucune autre transaction simultanée modifiant la file d’attente n’ait eu lieu.</span><span class="sxs-lookup"><span data-stu-id="0605d-150">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="0605d-151">Il n’est pas possible d’inférer l’ordre des éléments dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-151">No inference can be made about the order of items in the queue.</span></span> <span data-ttu-id="0605d-152">Pour cet extrait de code, les éléments peuvent apparaître dans un de 4 !</span><span class="sxs-lookup"><span data-stu-id="0605d-152">For this code snippet, the items may appear in any of the 4!</span></span> <span data-ttu-id="0605d-153">classements possibles.</span><span class="sxs-lookup"><span data-stu-id="0605d-153">possible orderings.</span></span>  <span data-ttu-id="0605d-154">La file d’attente essaie de conserver les éléments dans l’ordre (de mise en file d’attente) d’origine, mais peut être obligée à les réorganiser en raison d’opérations simultanées ou d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="0605d-154">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="0605d-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="0605d-155">DequeueAsync</span></span>
<span data-ttu-id="0605d-156">Voici quelques extraits de code pour l’utilisation de TryDequeueAsync, suivis des résultats attendus.</span><span class="sxs-lookup"><span data-stu-id="0605d-156">Here are a few code snippets for using TryDequeueAsync followed by the expected outputs.</span></span> <span data-ttu-id="0605d-157">Supposons que la file d’attente contient déjà les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0605d-157">Assume that the queue is already populated with the following items in the queue:</span></span>
> <span data-ttu-id="0605d-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="0605d-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="0605d-159">*Cas 1 : simple tâche de retrait de file d’attente*</span><span class="sxs-lookup"><span data-stu-id="0605d-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="0605d-160">Supposons que la tâche s’est achevée correctement et qu’aucune transaction simultanée ne modifiait la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-160">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="0605d-161">Dans la mesure où aucune inférence ne peut être effectuée concernant l’ordre des éléments dans la file d’attente, trois éléments quelconques peuvent être retirés de celle-ci, dans n’importe quel ordre.</span><span class="sxs-lookup"><span data-stu-id="0605d-161">Since no inference can be made about the order of the items in the queue, any three of the items may be dequeued, in any order.</span></span> <span data-ttu-id="0605d-162">La file d’attente essaie de conserver les éléments dans l’ordre (de mise en file d’attente) d’origine, mais peut être obligée à les réorganiser en raison d’opérations simultanées ou d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="0605d-162">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>  

- <span data-ttu-id="0605d-163">*Cas 2 : tâche de retrait de file d’attente parallèle*</span><span class="sxs-lookup"><span data-stu-id="0605d-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="0605d-164">Supposons que les tâches aient été accomplies avec succès, qu’elles aient été exécutées en parallèle et qu’aucune autre transaction simultanée modifiant la file d’attente n’ait eu lieu.</span><span class="sxs-lookup"><span data-stu-id="0605d-164">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="0605d-165">Dans la mesure où aucune inférence ne peut être effectuée concernant l’ordre des éléments dans la file d’attente, les listes *dequeue1* et *dequeue2* contiennent chacune deux éléments quelconques, dans n’importe quel ordre.</span><span class="sxs-lookup"><span data-stu-id="0605d-165">Since no inference can be made about the order of the items in the queue, the lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="0605d-166">Un même élément n’apparaît *pas* dans les deux listes.</span><span class="sxs-lookup"><span data-stu-id="0605d-166">The same item will *not* appear in both lists.</span></span> <span data-ttu-id="0605d-167">Par conséquent, si la liste dequeue1 comprend *10* et *30*, la liste dequeue2 contient *20* et *40*.</span><span class="sxs-lookup"><span data-stu-id="0605d-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="0605d-168">*Cas 3 : ordre de retrait de file d’attente avec abandon de transaction*</span><span class="sxs-lookup"><span data-stu-id="0605d-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="0605d-169">L’abandon d’une transaction avec des retraits de file d’attente a pour effet de remettre les éléments en tête de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-169">Aborting a transaction with in-flight dequeues puts the items back on the head of the queue.</span></span> <span data-ttu-id="0605d-170">L’ordre dans lequel les éléments sont remis en tête de la file d’attente n’est pas garanti.</span><span class="sxs-lookup"><span data-stu-id="0605d-170">The order in which the items are put back on the head of the queue is not guaranteed.</span></span> <span data-ttu-id="0605d-171">Examinons le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0605d-171">Let us look at the following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort the transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="0605d-172">Supposons que les éléments ont été retirés de la file d’attente dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="0605d-172">Assume that the items were dequeued in the following order:</span></span>
> <span data-ttu-id="0605d-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="0605d-173">10, 20</span></span>

<span data-ttu-id="0605d-174">Lors de l’abandon de la transaction, les éléments seraient rajoutés en tête de la file d’attente dans l’un des ordres suivants :</span><span class="sxs-lookup"><span data-stu-id="0605d-174">When we abort the transaction, the items would be added back to the head of the queue in any of the following orders:</span></span>
> <span data-ttu-id="0605d-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="0605d-175">10, 20</span></span>

> <span data-ttu-id="0605d-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="0605d-176">20, 10</span></span>

<span data-ttu-id="0605d-177">Il en va de même dans tous les cas où la transaction n’a pas été *validée*.</span><span class="sxs-lookup"><span data-stu-id="0605d-177">The same is true for all cases where the transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="0605d-178">Modèles de programmation</span><span class="sxs-lookup"><span data-stu-id="0605d-178">Programming Patterns</span></span>
<span data-ttu-id="0605d-179">Dans cette section, nous examinons quelques modèles de programmation qui peuvent s’avérer utiles lors de l’utilisation de ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="0605d-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="0605d-180">Retraits de file d’attente par lot</span><span class="sxs-lookup"><span data-stu-id="0605d-180">Batch Dequeues</span></span>
<span data-ttu-id="0605d-181">Un modèle de programmation recommandé est que la tâche cliente traite en lots les retraits de file d’attente au lieu d’effectuer un retrait à la fois.</span><span class="sxs-lookup"><span data-stu-id="0605d-181">A recommended programming pattern is for the consumer task to batch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="0605d-182">L’utilisateur peut choisir de limiter les délais entre chaque lot ou la taille des lots.</span><span class="sxs-lookup"><span data-stu-id="0605d-182">The user can choose to throttle delays between every batch or the batch size.</span></span> <span data-ttu-id="0605d-183">L’extrait de code suivant illustre ce modèle de programmation.</span><span class="sxs-lookup"><span data-stu-id="0605d-183">The following code snippet shows this programming model.</span></span>  <span data-ttu-id="0605d-184">Notez que, dans cet exemple, le traitement est effectué une fois la transaction validée. Dès lors, si une erreur se produit lors du traitement, les éléments non traités sont perdus sans avoir été traités.</span><span class="sxs-lookup"><span data-stu-id="0605d-184">Note that in this example, the processing is done after the transaction is committed, so if a fault were to occur while processing, the unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="0605d-185">Le traitement peut également être effectué dans l’étendue de la transaction, mais cela peut avoir une incidence négative sur les performances et nécessiter de gérer les éléments déjà traités.</span><span class="sxs-lookup"><span data-stu-id="0605d-185">Alternatively, the processing can be done within the transaction's scope, however this may have a negative impact on performance and requires handling of the items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break the for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="0605d-186">Traitement basé sur une notification d’effort optimal</span><span class="sxs-lookup"><span data-stu-id="0605d-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="0605d-187">Un autre modèle de programmation intéressant utilise l’API Count.</span><span class="sxs-lookup"><span data-stu-id="0605d-187">Another interesting programming pattern uses the Count API.</span></span> <span data-ttu-id="0605d-188">Ici, nous pouvons implémenter un traitement basé sur une notification d’effort optimal pour la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-188">Here, we can implement best-effort notification-based processing for the queue.</span></span> <span data-ttu-id="0605d-189">Le dénombrement (Count) des éléments contenus dans la file d’attente permet de limiter une tâche de mise en file d’attente ou de retrait de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-189">The queue Count can be used to throttle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="0605d-190">Notez que, comme dans l’exemple précédent, le traitement se produisant en dehors de la transaction, les éléments non traités peuvent être perdus si une erreur se produit en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="0605d-190">Note that as in the previous example, since the processing occurs outside the transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If the queue does not have the threshold number of items, delay the task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process the queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="0605d-191">Drainage d’effort optimal</span><span class="sxs-lookup"><span data-stu-id="0605d-191">Best-Effort Drain</span></span>
<span data-ttu-id="0605d-192">Un drainage de la file d’attente ne peut pas être garanti en raison de la nature simultanée de la structure de données.</span><span class="sxs-lookup"><span data-stu-id="0605d-192">A drain of the queue cannot be guaranteed due to the concurrent nature of the data structure.</span></span>  <span data-ttu-id="0605d-193">Il se peut que, même si aucune opération d’utilisateur sur la file d’attente n’est en cours, un appel particulier de TryDequeueAsync ne retourne pas un élément précédemment mis en file d’attente et validé.</span><span class="sxs-lookup"><span data-stu-id="0605d-193">It is possible that, even if no user operations on the queue are in-flight, a particular call to TryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="0605d-194">Il est garanti que l’élément en file d’attente deviendra *finalement* visible pour retrait de la file d’attente. Toutefois, à défaut d’un mécanisme de communication hors bande, un client indépendant ne peut pas savoir que la file d’attente a atteint un état stable, même si tous les producteurs ont été arrêtés et si aucune nouvelle opération de mise en file d’attente n’est autorisée.</span><span class="sxs-lookup"><span data-stu-id="0605d-194">The enqueued item is guaranteed to *eventually* become visible to dequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that the queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="0605d-195">Par conséquent, l’opération de drainage est implémentée selon le principe de l’effort optimal, comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0605d-195">Thus, the drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="0605d-196">L’utilisateur doit arrêter toutes les tâches de producteur et de client, et attendre que toutes les transactions en cours soient validées ou abandonnées, avant de tenter de drainer la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-196">The user should stop all further producer and consumer tasks, and wait for any in-flight transactions to commit or abort, before attempting to drain the queue.</span></span>  <span data-ttu-id="0605d-197">Si l’utilisateur connaît le nombre attendu d’éléments dans la file d’attente, il peut définir une notification qui signale que tous les éléments ont été retirés de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0605d-197">If the user knows the expected number of items in the queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer the dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="0605d-198">Aperçu</span><span class="sxs-lookup"><span data-stu-id="0605d-198">Peek</span></span>
<span data-ttu-id="0605d-199">ReliableConcurrentQueue ne fournit pas l’API *TryPeekAsync*.</span><span class="sxs-lookup"><span data-stu-id="0605d-199">ReliableConcurrentQueue does not provide the *TryPeekAsync* api.</span></span> <span data-ttu-id="0605d-200">Les utilisateurs peuvent obtenir la sémantique d’aperçu en utilisant *TryDequeueAsync*, puis en abandonnant la transaction.</span><span class="sxs-lookup"><span data-stu-id="0605d-200">Users can get the peek semantic by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="0605d-201">Dans cet exemple, les retraits de file d’attente sont traités uniquement si la valeur est supérieure à *10*.</span><span class="sxs-lookup"><span data-stu-id="0605d-201">In this example, dequeues are processed only if the item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process the item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="0605d-202">À lire</span><span class="sxs-lookup"><span data-stu-id="0605d-202">Must Read</span></span>
* [<span data-ttu-id="0605d-203">Démarrage rapide de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0605d-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="0605d-204">Utilisation des collections fiables</span><span class="sxs-lookup"><span data-stu-id="0605d-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="0605d-205">Notifications Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0605d-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="0605d-206">Sauvegarde et restauration de Reliable Services (récupération d’urgence)</span><span class="sxs-lookup"><span data-stu-id="0605d-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="0605d-207">Configuration du Gestionnaire d’état fiable</span><span class="sxs-lookup"><span data-stu-id="0605d-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="0605d-208">Prise en main des services API Web de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0605d-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="0605d-209">Utilisation avancée du modèle de programmation de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0605d-209">Advanced Usage of the Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="0605d-210">Référence du développeur pour les Collections fiables</span><span class="sxs-lookup"><span data-stu-id="0605d-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
