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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>TooReliableConcurrentQueue introduction dans Azure Service Fabric
Une file d’attente simultanée fiable est une file d’attente asynchrone, transactionnelle et répliquée, qui permet d’effectuer des opérations de mise en file d’attente et de retrait de file d’attente avec un niveau élevé de simultanéité. Il est conçu toodeliver un débit élevé et une faible latence en assouplissant hello FIFO ordre strict fournie par [file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) et fournit à la place un classement du meilleur effort.

## <a name="apis"></a>API

|File d’attente simultanée                |File d’attente simultanée fiable                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Task EnqueueAsync(ITransaction tx, T item)                       |
| bool TryDequeue(out T result)  | Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)  |
| int Count()                    | long Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Comparaison avec un [File d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx)

File d’attente simultanées fiable est proposé comme alternative trop[file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx). Elle doit être utilisée dans les cas où la séquence stricte de premier entré, premier sorti n’est pas requise, celle-ci nécessitant un compromis sur le plan de la simultanéité.  [File d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) utilise des verrous tooenforce FIFO classement, avec au maximum une transaction autorisée tooenqueue et une transaction au maximum autorisé toodequeue à la fois. En comparaison, fiable de file d’attente simultanée assouplit hello classement de contrainte et permet de n’importe quel nombre toointerleave de transactions simultanées leur file d’attente et les opérations de retrait. Classement du meilleur effort n’est fourni, toutefois hello l’ordre relatif de deux valeurs dans une file d’attente simultanées fiable peut ne jamais être garantie.

Une file d’attente simultanée fiable offre un débit supérieur et une latence moindre qu’une [file d’attente fiable](https://msdn.microsoft.com/library/azure/dn971527.aspx) chaque fois que plusieurs transactions simultanées effectuent des mises en file d’attente ou des retraits de file d’attente.

Un exemple de cas d’usage pour hello ReliableConcurrentQueue est hello [file d’attente de Message](https://en.wikipedia.org/wiki/Message_queue) scénario. Dans ce scénario, un ou plusieurs producteurs de message créer et ajouter des éléments toohello file et un ou plusieurs consommateurs de message des messages à partir de la file d’attente hello et les traitent. Plusieurs producteurs et consommateurs peuvent travailler indépendamment, à l’aide de transactions simultanées dans la file d’attente de commande tooprocess hello.

## <a name="usage-guidelines"></a>Instructions d’utilisation
* file d’attente Hello attend que les éléments de hello dans la file d’attente hello ont une période de rétention basse. Autrement dit, les éléments de hello ne seraient pas restent dans la file d’attente hello pendant une longue période.
* file d’attente Hello ne garantit pas l’ordre de FIFO strict.
* file d’attente Hello ne lit pas sa propre écritures. Si un élément est placé dans une transaction, il ne sera pas dequeuer tooa visible dans hello même transaction.
* Les retraits de file d’attente ne sont pas isolés les uns des autres. Si l’élément *A* est dépilé dans transaction *txnA*, même si *txnA* n’est pas validée, élément *A* ne serait pas visible tooa simultanées transaction *txnB*.  Si *txnA* est abandonnée, *A* deviennent visibles trop*txnB* immédiatement.
* *TryPeekAsync* comportement peut être implémenté à l’aide un *TryDequeueAsync* et l’abandon de la transaction de hello puis. Vous trouverez un exemple de cette Bonjour section des modèles de programmation.
* Count est non transactionnel. Il peut être utilisé tooget une idée du nombre de hello d’éléments dans la file d’attente de hello, mais représente un point dans le temps et ne peut pas être fiables.
* Coûteux hello de traitement des éléments de file d’attente ne doivent pas être effectuées lors de la transaction de hello est active, les transactions longues tooavoid qui peuvent avoir un impact sur les performances sur le système de hello.

## <a name="code-snippets"></a>Extraits de code
Examinons quelques extraits de code et leurs sorties attendues. La gestion des exceptions est ignorée dans cette section.

### <a name="enqueueasync"></a>EnqueueAsync
Voici quelques extraits de code pour l’utilisation d’EnqueueAsync, suivis de leurs sorties attendues.

- *Cas 1 : tâche de mise en file d’attente unique*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Supposons que cette tâche hello s’est terminée correctement, et qui n’a aucune modification de file d’attente hello des transactions simultanées. utilisateur de Hello peut s’attendre à hello file d’attente toocontain hello des éléments dans un des hello suivant de commandes :

> 10, 20

> 20, 10


- *Cas 2 : tâche de mise en file d’attente parallèle*

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

Supposons que hello tâches terminées avec succès, que les tâches hello se sont exécutées en parallèle et qu’aucune autre transaction simultanée modification de file d’attente hello. Aucune inférence ne peut être effectuée sur l’ordre des éléments dans la file d’attente hello hello. Pour cet extrait de code, les éléments de hello peuvent apparaître dans un des 4 de hello ! classements possibles.  file d’attente Hello tentera d’éléments de hello tookeep par ordre hello d’origine (en attente), mais peut être forcé tooreorder leur échéance tooconcurrent opérations ou des erreurs.


### <a name="dequeueasync"></a>DequeueAsync
Voici quelques extraits de code pour l’utilisation de TryDequeueAsync suivie de sorties de hello attendu. Supposons que cette file d’attente hello est déjà remplie avec hello éléments dans la file d’attente hello suivants :
> 10, 20, 30, 40, 50, 60

- *Cas 1 : simple tâche de retrait de file d’attente*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Supposons que cette tâche hello s’est terminée correctement, et qui n’a aucune modification de file d’attente hello des transactions simultanées. Dans la mesure où aucune inférence n’est possible sur l’ordre des éléments hello dans la file d’attente hello hello, trois des éléments de hello peut dépilé dans n’importe quel ordre. file d’attente Hello tentera d’éléments de hello tookeep par ordre hello d’origine (en attente), mais peut être forcé tooreorder leur échéance tooconcurrent opérations ou des erreurs.  

- *Cas 2 : tâche de retrait de file d’attente parallèle*

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

Supposons que hello tâches terminées avec succès, que les tâches hello se sont exécutées en parallèle et qu’aucune autre transaction simultanée modification de file d’attente hello. Dans la mesure où aucune inférence n’est possible sur l’ordre des éléments hello dans la file d’attente hello hello, hello listes *dequeue1* et *dequeue2* chacun contient tous les éléments de deux, dans n’importe quel ordre.

Hello sera du même élément *pas* s’affichent dans les deux listes. Par conséquent, si la liste dequeue1 comprend *10* et *30*, la liste dequeue2 contient *20* et *40*.

- *Cas 3 : ordre de retrait de file d’attente avec abandon de transaction*

Abandon de la transaction en cours avec l’enlève les éléments hello replace sur head hello de file d’attente hello. commande Hello dans lequel les éléments hello sont remis sur head hello de file d’attente hello n’est pas garantie. Examinons hello suivant de code :

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Partons du principe que les éléments hello ont été dépilés Bonjour suivant l’ordre :
> 10, 20

Lorsque nous abandonner la transaction de hello, les éléments hello sont ajoutés head toohello précédent de la file d’attente hello dans un des hello suivant de commandes :
> 10, 20

> 20, 10

Hello est également vrai pour tous les cas où les transactions hello n’a pas été *validé*.

## <a name="programming-patterns"></a>Modèles de programmation
Dans cette section, nous examinons quelques modèles de programmation qui peuvent s’avérer utiles lors de l’utilisation de ReliableConcurrentQueue.

### <a name="batch-dequeues"></a>Retraits de file d’attente par lot
Recommandée est de modèle de programmation pour hello consommateur tâche toobatch son enlève au lieu d’effectuer un retrait à la fois. utilisateur de Hello peut choisir des retards toothrottle entre chaque lot ou hello la taille du lot. Hello extrait de code suivant illustre ce modèle de programmation.  Notez que dans cet exemple, le traitement de hello est effectué une fois hello transaction est validée, donc si une erreur a été toooccur lors du traitement, hello éléments non traités seront perdus sans avoir été traitée.  Vous pouvez également le traitement de hello peut être effectué dans l’étendue de la transaction hello, toutefois, cela peut avoir un impact négatif sur les performances et nécessite un traitement d’éléments de hello déjà traitement.

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

### <a name="best-effort-notification-based-processing"></a>Traitement basé sur une notification d’effort optimal
Un autre modèle de programmation intéressant utilise hello nombre d’API. Ici, nous pouvons implémenter le traitement meilleur effort notification pour la file d’attente hello. la file d’attente de Hello nombre peut être utilisé toothrottle une file d’attente ou une tâche de retrait.  Notez que dans l’exemple précédent de hello, étant donné que le traitement de hello se produit en dehors de la transaction de hello, des éléments non traités peuvent être perdues si une erreur se produit lors du traitement.

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

### <a name="best-effort-drain"></a>Drainage d’effort optimal
Ne garantit pas un drainage de file d’attente hello en raison de la nature de simultanées toohello de structure de données hello.  Il est possible que, même si aucune opération de l’utilisateur sur la file d’attente hello n’est en cours, une tooTryDequeueAsync appel particulier peut retourner pas un élément qui était auparavant en file d’attente et validée.  élément en file d’attente de Hello est garantie trop*finalement* deviennent visible toodequeue, mais sans un mécanisme de communication d’out-of-band, un consommateur indépendant ne peut pas savoir à cette file d’attente hello a atteint un état stable même si toutes les producteurs ont été arrêtés et aucune nouvelle opération de file d’attente n’est autorisées. Par conséquent, opération de vidange hello est mieux implémenté ci-dessous.

Hello utilisateur doit arrêter toutes les autres producteurs et les tâches du consommateur et attendre que n’importe quel toocommit des transactions en cours ou l’abandon, avant de tenter de file d’attente de toodrain hello.  Si l’utilisateur de hello sait nombre hello attendu d’éléments dans la file d’attente hello, ils peuvent définir une notification qui signale que tous les éléments ont été dépilés.

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

### <a name="peek"></a>Aperçu
ReliableConcurrentQueue ne fournit pas de hello *TryPeekAsync* api. Les utilisateurs peuvent obtenir une lecture de hello sémantique en utilisant un *TryDequeueAsync* et l’abandon de la transaction de hello puis. Dans cet exemple, enlève sont traitées uniquement si la valeur de l’élément hello est supérieur à *10*.

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

## <a name="must-read"></a>À lire
* [Démarrage rapide de Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Utilisation des collections fiables](service-fabric-work-with-reliable-collections.md)
* [Notifications Reliable Services](service-fabric-reliable-services-notifications.md)
* [Sauvegarde et restauration de Reliable Services (récupération d’urgence)](service-fabric-reliable-services-backup-restore.md)
* [Configuration du Gestionnaire d’état fiable](service-fabric-reliable-services-configuration.md)
* [Prise en main des services API Web de Service Fabric](service-fabric-reliable-services-communication-webapi.md)
* [Utilisation avancée de hello modèle de programmation des Services fiables](service-fabric-reliable-services-advanced-usage.md)
* [Référence du développeur pour les Collections fiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
