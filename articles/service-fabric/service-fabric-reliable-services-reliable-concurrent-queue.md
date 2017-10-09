---
title: aaaReliableConcurrentQueue dans Azure Service Fabric
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
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="d0ffb-103">TooReliableConcurrentQueue introduction dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d0ffb-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="d0ffb-104">Une file d’attente simultanée fiable est une file d’attente asynchrone, transactionnelle et répliquée, qui permet d’effectuer des opérations de mise en file d’attente et de retrait de file d’attente avec un niveau élevé de simultanéité.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="d0ffb-105">Il est conçu toodeliver un débit élevé et une faible latence en assouplissant hello FIFO ordre strict fournie par [file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) et fournit à la place un classement du meilleur effort.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="d0ffb-106">API</span><span class="sxs-lookup"><span data-stu-id="d0ffb-106">APIs</span></span>

|<span data-ttu-id="d0ffb-107">File d’attente simultanée</span><span class="sxs-lookup"><span data-stu-id="d0ffb-107">Concurrent Queue</span></span>                |<span data-ttu-id="d0ffb-108">File d’attente simultanée fiable</span><span class="sxs-lookup"><span data-stu-id="d0ffb-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="d0ffb-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="d0ffb-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="d0ffb-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="d0ffb-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="d0ffb-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="d0ffb-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="d0ffb-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="d0ffb-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="d0ffb-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="d0ffb-113">int Count()</span></span>                    | <span data-ttu-id="d0ffb-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="d0ffb-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="d0ffb-115">Comparaison avec un [File d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="d0ffb-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="d0ffb-116">File d’attente simultanées fiable est proposé comme alternative trop[file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0ffb-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="d0ffb-117">Elle doit être utilisée dans les cas où la séquence stricte de premier entré, premier sorti n’est pas requise, celle-ci nécessitant un compromis sur le plan de la simultanéité.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="d0ffb-118">[File d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) utilise des verrous tooenforce FIFO classement, avec au maximum une transaction autorisée tooenqueue et une transaction au maximum autorisé toodequeue à la fois.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="d0ffb-119">En comparaison, fiable de file d’attente simultanée assouplit hello classement de contrainte et permet de n’importe quel nombre toointerleave de transactions simultanées leur file d’attente et les opérations de retrait.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="d0ffb-120">Classement du meilleur effort n’est fourni, toutefois hello l’ordre relatif de deux valeurs dans une file d’attente simultanées fiable peut ne jamais être garantie.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="d0ffb-121">Une file d’attente simultanée fiable offre un débit supérieur et une latence moindre qu’une [file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) chaque fois que plusieurs transactions simultanées effectuent des mises en file d’attente ou des retraits de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="d0ffb-122">Un exemple de cas d’usage pour hello ReliableConcurrentQueue est hello [file d’attente de Message](https://en.wikipedia.org/wiki/Message_queue) scénario.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="d0ffb-123">Dans ce scénario, un ou plusieurs producteurs de message créer et ajouter des éléments toohello file et un ou plusieurs consommateurs de message des messages à partir de la file d’attente hello et les traitent.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="d0ffb-124">Plusieurs producteurs et consommateurs peuvent travailler indépendamment, à l’aide de transactions simultanées dans la file d’attente de commande tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="d0ffb-125">Instructions d’utilisation</span><span class="sxs-lookup"><span data-stu-id="d0ffb-125">Usage Guidelines</span></span>
* <span data-ttu-id="d0ffb-126">file d’attente Hello attend que les éléments de hello dans la file d’attente hello ont une période de rétention basse.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="d0ffb-127">Autrement dit, les éléments de hello ne seraient pas restent dans la file d’attente hello pendant une longue période.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="d0ffb-128">file d’attente Hello ne garantit pas l’ordre de FIFO strict.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="d0ffb-129">file d’attente Hello ne lit pas sa propre écritures.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="d0ffb-130">Si un élément est placé dans une transaction, il ne sera pas dequeuer tooa visible dans hello même transaction.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="d0ffb-131">Les retraits de file d’attente ne sont pas isolés les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="d0ffb-132">Si l’élément *A* est dépilé dans transaction *txnA*, même si *txnA* n’est pas validée, élément *A* ne serait pas visible tooa simultanées transaction *txnB*.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="d0ffb-133">Si *txnA* est abandonnée, *A* deviennent visibles trop*txnB* immédiatement.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="d0ffb-134">*TryPeekAsync* comportement peut être implémenté à l’aide un *TryDequeueAsync* et l’abandon de la transaction de hello puis.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="d0ffb-135">Vous trouverez un exemple de cette Bonjour section des modèles de programmation.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="d0ffb-136">Count est non transactionnel.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-136">Count is non-transactional.</span></span> <span data-ttu-id="d0ffb-137">Il peut être utilisé tooget une idée du nombre de hello d’éléments dans la file d’attente de hello, mais représente un point dans le temps et ne peut pas être fiables.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="d0ffb-138">Coûteux hello de traitement des éléments de file d’attente ne doivent pas être effectuées lors de la transaction de hello est active, les transactions longues tooavoid qui peuvent avoir un impact sur les performances sur le système de hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="d0ffb-139">Extraits de code</span><span class="sxs-lookup"><span data-stu-id="d0ffb-139">Code Snippets</span></span>
<span data-ttu-id="d0ffb-140">Examinons quelques extraits de code et leurs sorties attendues.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="d0ffb-141">La gestion des exceptions est ignorée dans cette section.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="d0ffb-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="d0ffb-142">EnqueueAsync</span></span>
<span data-ttu-id="d0ffb-143">Voici quelques extraits de code pour l’utilisation d’EnqueueAsync, suivis de leurs sorties attendues.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="d0ffb-144">*Cas 1 : tâche de mise en file d’attente unique*</span><span class="sxs-lookup"><span data-stu-id="d0ffb-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="d0ffb-145">Supposons que cette tâche hello s’est terminée correctement, et qui n’a aucune modification de file d’attente hello des transactions simultanées.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="d0ffb-146">utilisateur de Hello peut s’attendre à hello file d’attente toocontain hello des éléments dans un des hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d0ffb-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="d0ffb-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="d0ffb-147">10, 20</span></span>

> <span data-ttu-id="d0ffb-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="d0ffb-148">20, 10</span></span>


- <span data-ttu-id="d0ffb-149">*Cas 2 : tâche de mise en file d’attente parallèle*</span><span class="sxs-lookup"><span data-stu-id="d0ffb-149">*Case 2: Parallel Enqueue Task*</span></span>

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

<span data-ttu-id="d0ffb-150">Supposons que hello tâches terminées avec succès, que les tâches hello se sont exécutées en parallèle et qu’aucune autre transaction simultanée modification de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="d0ffb-151">Aucune inférence ne peut être effectuée sur l’ordre des éléments dans la file d’attente hello hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="d0ffb-152">Pour cet extrait de code, les éléments de hello peuvent apparaître dans un des 4 de hello !</span><span class="sxs-lookup"><span data-stu-id="d0ffb-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="d0ffb-153">classements possibles.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-153">possible orderings.</span></span>  <span data-ttu-id="d0ffb-154">file d’attente Hello tentera d’éléments de hello tookeep par ordre hello d’origine (en attente), mais peut être forcé tooreorder leur échéance tooconcurrent opérations ou des erreurs.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="d0ffb-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="d0ffb-155">DequeueAsync</span></span>
<span data-ttu-id="d0ffb-156">Voici quelques extraits de code pour l’utilisation de TryDequeueAsync suivie de sorties de hello attendu.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="d0ffb-157">Supposons que cette file d’attente hello est déjà remplie avec hello éléments dans la file d’attente hello suivants :</span><span class="sxs-lookup"><span data-stu-id="d0ffb-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="d0ffb-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="d0ffb-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="d0ffb-159">*Cas 1 : simple tâche de retrait de file d’attente*</span><span class="sxs-lookup"><span data-stu-id="d0ffb-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="d0ffb-160">Supposons que cette tâche hello s’est terminée correctement, et qui n’a aucune modification de file d’attente hello des transactions simultanées.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="d0ffb-161">Dans la mesure où aucune inférence n’est possible sur l’ordre des éléments hello dans la file d’attente hello hello, trois des éléments de hello peut dépilé dans n’importe quel ordre.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="d0ffb-162">file d’attente Hello tentera d’éléments de hello tookeep par ordre hello d’origine (en attente), mais peut être forcé tooreorder leur échéance tooconcurrent opérations ou des erreurs.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="d0ffb-163">*Cas 2 : tâche de retrait de file d’attente parallèle*</span><span class="sxs-lookup"><span data-stu-id="d0ffb-163">*Case 2: Parallel Dequeue Task*</span></span>

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

<span data-ttu-id="d0ffb-164">Supposons que hello tâches terminées avec succès, que les tâches hello se sont exécutées en parallèle et qu’aucune autre transaction simultanée modification de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="d0ffb-165">Dans la mesure où aucune inférence n’est possible sur l’ordre des éléments hello dans la file d’attente hello hello, hello listes *dequeue1* et *dequeue2* chacun contient tous les éléments de deux, dans n’importe quel ordre.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="d0ffb-166">Hello sera du même élément *pas* s’affichent dans les deux listes.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="d0ffb-167">Par conséquent, si la liste dequeue1 comprend *10* et *30*, la liste dequeue2 contient *20* et *40*.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="d0ffb-168">*Cas 3 : ordre de retrait de file d’attente avec abandon de transaction*</span><span class="sxs-lookup"><span data-stu-id="d0ffb-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="d0ffb-169">Abandon de la transaction en cours avec l’enlève les éléments hello replace sur head hello de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="d0ffb-170">commande Hello dans lequel les éléments hello sont remis sur head hello de file d’attente hello n’est pas garantie.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="d0ffb-171">Examinons hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="d0ffb-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="d0ffb-172">Partons du principe que les éléments hello ont été dépilés Bonjour suivant l’ordre :</span><span class="sxs-lookup"><span data-stu-id="d0ffb-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="d0ffb-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="d0ffb-173">10, 20</span></span>

<span data-ttu-id="d0ffb-174">Lorsque nous abandonner la transaction de hello, les éléments hello sont ajoutés head toohello précédent de la file d’attente hello dans un des hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d0ffb-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="d0ffb-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="d0ffb-175">10, 20</span></span>

> <span data-ttu-id="d0ffb-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="d0ffb-176">20, 10</span></span>

<span data-ttu-id="d0ffb-177">Hello est également vrai pour tous les cas où les transactions hello n’a pas été *validé*.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="d0ffb-178">Modèles de programmation</span><span class="sxs-lookup"><span data-stu-id="d0ffb-178">Programming Patterns</span></span>
<span data-ttu-id="d0ffb-179">Dans cette section, nous examinons quelques modèles de programmation qui peuvent s’avérer utiles lors de l’utilisation de ReliableConcurrentQueue.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="d0ffb-180">Retraits de file d’attente par lot</span><span class="sxs-lookup"><span data-stu-id="d0ffb-180">Batch Dequeues</span></span>
<span data-ttu-id="d0ffb-181">Recommandée est de modèle de programmation pour hello consommateur tâche toobatch son enlève au lieu d’effectuer un retrait à la fois.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="d0ffb-182">utilisateur de Hello peut choisir des retards toothrottle entre chaque lot ou hello la taille du lot.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="d0ffb-183">Hello extrait de code suivant illustre ce modèle de programmation.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="d0ffb-184">Notez que dans cet exemple, le traitement de hello est effectué une fois hello transaction est validée, donc si une erreur a été toooccur lors du traitement, hello éléments non traités seront perdus sans avoir été traitée.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="d0ffb-185">Vous pouvez également le traitement de hello peut être effectué dans l’étendue de la transaction hello, toutefois, cela peut avoir un impact négatif sur les performances et nécessite un traitement d’éléments de hello déjà traitement.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

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
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="d0ffb-186">Traitement basé sur une notification d’effort optimal</span><span class="sxs-lookup"><span data-stu-id="d0ffb-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="d0ffb-187">Un autre modèle de programmation intéressant utilise hello nombre d’API.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="d0ffb-188">Ici, nous pouvons implémenter le traitement meilleur effort notification pour la file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="d0ffb-189">la file d’attente de Hello nombre peut être utilisé toothrottle une file d’attente ou une tâche de retrait.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="d0ffb-190">Notez que dans l’exemple précédent de hello, étant donné que le traitement de hello se produit en dehors de la transaction de hello, des éléments non traités peuvent être perdues si une erreur se produit lors du traitement.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

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
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="d0ffb-191">Drainage d’effort optimal</span><span class="sxs-lookup"><span data-stu-id="d0ffb-191">Best-Effort Drain</span></span>
<span data-ttu-id="d0ffb-192">Ne garantit pas un drainage de file d’attente hello en raison de la nature de simultanées toohello de structure de données hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="d0ffb-193">Il est possible que, même si aucune opération de l’utilisateur sur la file d’attente hello n’est en cours, une tooTryDequeueAsync appel particulier peut retourner pas un élément qui était auparavant en file d’attente et validée.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="d0ffb-194">élément en file d’attente de Hello est garantie trop*finalement* deviennent visible toodequeue, mais sans un mécanisme de communication d’out-of-band, un consommateur indépendant ne peut pas savoir à cette file d’attente hello a atteint un état stable même si toutes les producteurs ont été arrêtés et aucune nouvelle opération de file d’attente n’est autorisées.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="d0ffb-195">Par conséquent, opération de vidange hello est mieux implémenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="d0ffb-196">Hello utilisateur doit arrêter toutes les autres producteurs et les tâches du consommateur et attendre que n’importe quel toocommit des transactions en cours ou l’abandon, avant de tenter de file d’attente de toodrain hello.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="d0ffb-197">Si l’utilisateur de hello sait nombre hello attendu d’éléments dans la file d’attente hello, ils peuvent définir une notification qui signale que tous les éléments ont été dépilés.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

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
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="d0ffb-198">Aperçu</span><span class="sxs-lookup"><span data-stu-id="d0ffb-198">Peek</span></span>
<span data-ttu-id="d0ffb-199">ReliableConcurrentQueue ne fournit pas de hello *TryPeekAsync* api.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="d0ffb-200">Les utilisateurs peuvent obtenir une lecture de hello sémantique en utilisant un *TryDequeueAsync* et l’abandon de la transaction de hello puis.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="d0ffb-201">Dans cet exemple, enlève sont traitées uniquement si la valeur de l’élément hello est supérieur à *10*.</span><span class="sxs-lookup"><span data-stu-id="d0ffb-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
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

## <a name="must-read"></a><span data-ttu-id="d0ffb-202">À lire</span><span class="sxs-lookup"><span data-stu-id="d0ffb-202">Must Read</span></span>
* [<span data-ttu-id="d0ffb-203">Démarrage rapide de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d0ffb-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="d0ffb-204">Utilisation des collections fiables</span><span class="sxs-lookup"><span data-stu-id="d0ffb-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="d0ffb-205">Notifications Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d0ffb-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="d0ffb-206">Sauvegarde et restauration de Reliable Services (récupération d’urgence)</span><span class="sxs-lookup"><span data-stu-id="d0ffb-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="d0ffb-207">Configuration du Gestionnaire d’état fiable</span><span class="sxs-lookup"><span data-stu-id="d0ffb-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="d0ffb-208">Prise en main des services API Web de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d0ffb-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="d0ffb-209">Utilisation avancée de hello modèle de programmation des Services fiables</span><span class="sxs-lookup"><span data-stu-id="d0ffb-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="d0ffb-210">Référence du développeur pour les Collections fiables</span><span class="sxs-lookup"><span data-stu-id="d0ffb-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
