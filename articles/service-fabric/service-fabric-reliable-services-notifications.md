---
title: "Notifications Reliable Services | Microsoft Docs"
description: Documentation conceptuelle relative aux notifications Reliable Services Service Fabric
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: c6a53d851510ed5e6eec1f3ac0f636ad034a6d4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="2c723-103">Notifications Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2c723-103">Reliable Services notifications</span></span>
<span data-ttu-id="2c723-104">Les notifications permettent aux clients de suivre les modifications apportées à un objet qui les intéresse.</span><span class="sxs-lookup"><span data-stu-id="2c723-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="2c723-105">Deux types d’objets prennent en charge les notifications : *Gestionnaire d’état fiable* et *Dictionnaire fiable*.</span><span class="sxs-lookup"><span data-stu-id="2c723-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="2c723-106">Raisons courantes d’utiliser les notifications :</span><span class="sxs-lookup"><span data-stu-id="2c723-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="2c723-107">Construction de vues matérialisées, comme des index secondaires ou des vues filtrées agrégées de l’état du réplica.</span><span class="sxs-lookup"><span data-stu-id="2c723-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="2c723-108">Par exemple, un index trié de toutes les clés d’un dictionnaire fiable.</span><span class="sxs-lookup"><span data-stu-id="2c723-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="2c723-109">Envoi de données de surveillance comme le nombre d’utilisateurs ajoutés durant la dernière heure.</span><span class="sxs-lookup"><span data-stu-id="2c723-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="2c723-110">Les notifications sont déclenchées dans le cadre de l’application d’opérations.</span><span class="sxs-lookup"><span data-stu-id="2c723-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="2c723-111">Pour cette raison, les notifications doivent être traitées le plus rapidement possible, et les événements synchrones ne doivent pas inclure d’opérations coûteuses.</span><span class="sxs-lookup"><span data-stu-id="2c723-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="2c723-112">Notifications du Gestionnaire d’état fiable</span><span class="sxs-lookup"><span data-stu-id="2c723-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="2c723-113">Le Gestionnaire d’état fiable fournit des notifications pour les événements suivants :</span><span class="sxs-lookup"><span data-stu-id="2c723-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="2c723-114">Transaction</span><span class="sxs-lookup"><span data-stu-id="2c723-114">Transaction</span></span>
  * <span data-ttu-id="2c723-115">Validation</span><span class="sxs-lookup"><span data-stu-id="2c723-115">Commit</span></span>
* <span data-ttu-id="2c723-116">Gestionnaire d’état</span><span class="sxs-lookup"><span data-stu-id="2c723-116">State manager</span></span>
  * <span data-ttu-id="2c723-117">Reconstruction</span><span class="sxs-lookup"><span data-stu-id="2c723-117">Rebuild</span></span>
  * <span data-ttu-id="2c723-118">Ajout d’un état fiable</span><span class="sxs-lookup"><span data-stu-id="2c723-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="2c723-119">Suppression d’un état fiable</span><span class="sxs-lookup"><span data-stu-id="2c723-119">Removal of a reliable state</span></span>

<span data-ttu-id="2c723-120">Le Gestionnaire d’état fiable effectue le suivi à la volée des transactions en cours.</span><span class="sxs-lookup"><span data-stu-id="2c723-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="2c723-121">Le seul changement d’état de transaction qui déclenche une notification est une transaction en cours de validation.</span><span class="sxs-lookup"><span data-stu-id="2c723-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="2c723-122">Le Gestionnaire d’état fiable tient à jour une collection d’états fiables comme Dictionnaire fiable et File d’attente fiable.</span><span class="sxs-lookup"><span data-stu-id="2c723-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="2c723-123">Le Gestionnaire d’état fiable déclenche des notifications quand cette collection est modifiée : un état fiable est ajouté, supprimé, ou la collection entière est reconstruite.</span><span class="sxs-lookup"><span data-stu-id="2c723-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="2c723-124">La collection du Gestionnaire d’état fiable est reconstruite dans trois cas :</span><span class="sxs-lookup"><span data-stu-id="2c723-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="2c723-125">Récupération : quand un réplica démarre, il récupère son état précédent à partir du disque.</span><span class="sxs-lookup"><span data-stu-id="2c723-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="2c723-126">À la fin de la récupération, il utilise **NotifyStateManagerChangedEventArgs** pour déclencher un événement qui contient l’ensemble des états fiables récupérés.</span><span class="sxs-lookup"><span data-stu-id="2c723-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="2c723-127">Copie complète : avant qu’un réplica puisse rejoindre le jeu de configuration, il doit être créé.</span><span class="sxs-lookup"><span data-stu-id="2c723-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="2c723-128">Dans certains cas, il est nécessaire d’appliquer une copie complète de l’état du Gestionnaire d’état fiable du réplica principal au réplica secondaire inactif.</span><span class="sxs-lookup"><span data-stu-id="2c723-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="2c723-129">Le Gestionnaire d’état fiable sur le réplica secondaire utilise **NotifyStateManagerChangedEventArgs** pour déclencher un événement qui contient l’ensemble des états fiables qu’il a acquis à partir du réplica principal.</span><span class="sxs-lookup"><span data-stu-id="2c723-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="2c723-130">Restauration : dans les scénarios de récupération d’urgence, vous pouvez restaurer l’état du réplica à partir d’une sauvegarde par le biais de **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="2c723-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="2c723-131">Dans ces cas-là, le Gestionnaire d’état fiable sur le réplica secondaire utilise **NotifyStateManagerChangedEventArgs** pour déclencher un événement qui contient l’ensemble des états fiables qu’il a restauré à partir de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="2c723-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="2c723-132">Pour vous inscrire aux notifications de transactions et/ou notifications du Gestionnaire d’état, vous devez vous inscrire auprès de l’événement **TransactionChanged** ou **StateManagerChanged** sur le Gestionnaire d’état fiable.</span><span class="sxs-lookup"><span data-stu-id="2c723-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="2c723-133">Le constructeur de votre élément StatefulService est un endroit courant où s’inscrire auprès de ces gestionnaires d’événements.</span><span class="sxs-lookup"><span data-stu-id="2c723-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="2c723-134">Si vous êtes inscrit dans le constructeur, vous ne manquerez aucune notification due à une modification pendant la durée de vie de **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="2c723-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="2c723-135">Le gestionnaire d’événements **TransactionChanged** utilise **NotifyTransactionChangedEventArgs** pour fournir des détails sur l’événement.</span><span class="sxs-lookup"><span data-stu-id="2c723-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="2c723-136">Il contient la propriété d’action (par exemple, **NotifyTransactionChangedAction.Commit**) qui spécifie le type de modification.</span><span class="sxs-lookup"><span data-stu-id="2c723-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="2c723-137">Il contient également la propriété de transaction qui fournit une référence à la transaction qui a changé.</span><span class="sxs-lookup"><span data-stu-id="2c723-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="2c723-138">Aujourd’hui, les événements **TransactionChanged** sont déclenchés uniquement si la transaction est validée.</span><span class="sxs-lookup"><span data-stu-id="2c723-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="2c723-139">L’action est alors égale à **NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="2c723-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="2c723-140">Mais à l’avenir, des événements pourront être déclenchés pour d’autres types de modifications d’état de transaction.</span><span class="sxs-lookup"><span data-stu-id="2c723-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="2c723-141">Nous vous recommandons de vérifier l’action et de traiter l’événement uniquement s’il correspond à ce que vous attendez.</span><span class="sxs-lookup"><span data-stu-id="2c723-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="2c723-142">Voici un exemple de gestionnaire d’événements **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="2c723-142">Following is an example **TransactionChanged** event handler.</span></span>

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

<span data-ttu-id="2c723-143">Le gestionnaire d’événements **StateManagerChanged** utilise **NotifyStateManagerChangedEventArgs** pour fournir des détails sur l’événement.</span><span class="sxs-lookup"><span data-stu-id="2c723-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="2c723-144">**NotifyStateManagerChangedEventArgs** comporte deux sous-classes : **NotifyStateManagerRebuildEventArgs** et **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="2c723-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="2c723-145">Vous utilisez la propriété d’action dans **NotifyStateManagerChangedEventArgs** pour convertir **NotifyStateManagerChangedEventArgs** en la sous-classe correcte :</span><span class="sxs-lookup"><span data-stu-id="2c723-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="2c723-146">**NotifyStateManagerChangedAction.Rebuild** : **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="2c723-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="2c723-147">**NotifyStateManagerChangedAction.Add** et **NotifyStateManagerChangedAction.Remove** : **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="2c723-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="2c723-148">Voici un exemple de gestionnaire de notification **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="2c723-148">Following is an example **StateManagerChanged** notification handler.</span></span>

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="2c723-149">Notifications Dictionnaire fiable</span><span class="sxs-lookup"><span data-stu-id="2c723-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="2c723-150">Dictionnaire fiable fournit des notifications pour les événements suivants :</span><span class="sxs-lookup"><span data-stu-id="2c723-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="2c723-151">Reconstruction : appelée quand **ReliableDictionary** a récupéré son état à partir d’une sauvegarde ou d’un état local récupéré ou copié.</span><span class="sxs-lookup"><span data-stu-id="2c723-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="2c723-152">Effacement : appelée quand l’état de **ReliableDictionary** a été effacé par le biais de la méthode **ClearAsync**.</span><span class="sxs-lookup"><span data-stu-id="2c723-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="2c723-153">Ajout : appelée quand un élément a été ajouté à **ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="2c723-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="2c723-154">Mise à jour : appelée quand un élément de **IReliableDictionary** a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="2c723-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="2c723-155">Suppression : appelée quand un élément de **IReliableDictionary** a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="2c723-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="2c723-156">Pour obtenir des notifications Dictionnaire fiable, vous devez vous inscrire auprès du gestionnaire d’événements **DictionaryChanged** sur **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="2c723-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="2c723-157">La notification d’ajout **ReliableStateManager.StateManagerChanged** est une situation courante au cours de laquelle l’utilisateur s’inscrit auprès de ces gestionnaires d’événements.</span><span class="sxs-lookup"><span data-stu-id="2c723-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="2c723-158">L’inscription quand **IReliableDictionary** est ajouté à **IReliableStateManager** permet de s’assurer que vous ne manquerez aucune notification.</span><span class="sxs-lookup"><span data-stu-id="2c723-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="2c723-159">**ProcessStateManagerSingleEntityNotification** est l’exemple de méthode appelée par l’exemple **OnStateManagerChangedHandler** précédent.</span><span class="sxs-lookup"><span data-stu-id="2c723-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="2c723-160">Le code précédent définit l’interface **IReliableNotificationAsyncCallback**, ainsi que **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="2c723-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="2c723-161">Étant donné que **NotifyDictionaryRebuildEventArgs** contient une interface **IAsyncEnumerable** qui doit être énumérée de façon asynchrone, des notifications de reconstruction sont déclenchées par le biais de **RebuildNotificationAsyncCallback** au lieu de **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="2c723-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> <span data-ttu-id="2c723-162">Dans le code précédent, dans le cadre du traitement de la notification de reconstruction, l’état agrégé est d’abord effacé.</span><span class="sxs-lookup"><span data-stu-id="2c723-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="2c723-163">La collection fiable étant en cours de reconstruction avec un nouvel état, toutes les notifications précédentes sont sans intérêt.</span><span class="sxs-lookup"><span data-stu-id="2c723-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="2c723-164">Le gestionnaire d’événements **DictionaryChanged** utilise **NotifyDictionaryChangedEventArgs** pour fournir des détails sur l’événement.</span><span class="sxs-lookup"><span data-stu-id="2c723-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="2c723-165">**NotifyDictionaryChangedEventArgs** a cinq sous-classes.</span><span class="sxs-lookup"><span data-stu-id="2c723-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="2c723-166">Utilisez la propriété d’action dans **NotifyDictionaryChangedEventArgs** pour convertir **NotifyDictionaryChangedEventArgs** en la sous-classe correcte :</span><span class="sxs-lookup"><span data-stu-id="2c723-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="2c723-167">**NotifyDictionaryChangedAction.Rebuild** : **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="2c723-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="2c723-168">**NotifyDictionaryChangedAction.Clear** : **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="2c723-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="2c723-169">**NotifyDictionaryChangedAction.Add** et **NotifyDictionaryChangedAction.Remove** : **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="2c723-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="2c723-170">**NotifyDictionaryChangedAction.Update** : **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="2c723-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="2c723-171">**NotifyDictionaryChangedAction.Remove** : **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="2c723-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a><span data-ttu-id="2c723-172">Recommandations</span><span class="sxs-lookup"><span data-stu-id="2c723-172">Recommendations</span></span>
* <span data-ttu-id="2c723-173">*Complétez* les événements de notification le plus rapidement possible.</span><span class="sxs-lookup"><span data-stu-id="2c723-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="2c723-174">*N’exécutez aucune* opération coûteuse (par exemple des opérations d’E/S) dans le cadre d’événements synchrones.</span><span class="sxs-lookup"><span data-stu-id="2c723-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="2c723-175">*Vérifiez* le type d’action avant de traiter l’événement.</span><span class="sxs-lookup"><span data-stu-id="2c723-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="2c723-176">De nouveaux types d’actions pourront être ajoutés à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="2c723-176">New action types might be added in the future.</span></span>

<span data-ttu-id="2c723-177">Voici quelques points à retenir :</span><span class="sxs-lookup"><span data-stu-id="2c723-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="2c723-178">Les notifications sont déclenchées dans le cadre de l’exécution d’une opération.</span><span class="sxs-lookup"><span data-stu-id="2c723-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="2c723-179">Par exemple, une notification de restauration est déclenchée comme dernière étape d’une opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="2c723-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="2c723-180">Une restauration ne se termine pas tant que l’événement de notification n’a pas été traité.</span><span class="sxs-lookup"><span data-stu-id="2c723-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="2c723-181">Les notifications étant déclenchées dans le cadre des opérations d’application, les clients ne voient que les notifications des opérations validées localement.</span><span class="sxs-lookup"><span data-stu-id="2c723-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="2c723-182">De plus, dans la mesure où les opérations sont garanties uniquement pour être validées localement (en d’autres termes consignées), elles risquent de ne pas pouvoir être annulées par la suite.</span><span class="sxs-lookup"><span data-stu-id="2c723-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="2c723-183">Lors d’une opération de rétablissement, une seule notification est déclenchée pour chaque opération appliquée.</span><span class="sxs-lookup"><span data-stu-id="2c723-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="2c723-184">Cela signifie que si la transaction T1 inclut Create(X), Delete(X) et Create(X), vous obtiendrez une notification pour la création de X, une autre pour sa suppression et une autre pour sa création, dans cet ordre.</span><span class="sxs-lookup"><span data-stu-id="2c723-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="2c723-185">Pour les transactions qui contiennent plusieurs opérations, les opérations sont appliquées dans l’ordre dans lequel elles ont été reçues sur le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="2c723-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="2c723-186">Lors du traitement d’une mauvaise progression, certaines opérations peuvent être annulées.</span><span class="sxs-lookup"><span data-stu-id="2c723-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="2c723-187">Des notifications sont déclenchées pour ces opérations d’annulation afin de ramener le réplica à un état stable.</span><span class="sxs-lookup"><span data-stu-id="2c723-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="2c723-188">Les notifications d’annulation présentent une importante différence. En effet, les événements avec des clés en double sont agrégés.</span><span class="sxs-lookup"><span data-stu-id="2c723-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="2c723-189">Par exemple, si la transaction T1 est annulée, vous ne verrez qu’une seule notification Delete(X).</span><span class="sxs-lookup"><span data-stu-id="2c723-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c723-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c723-190">Next steps</span></span>
* [<span data-ttu-id="2c723-191">Collections fiables</span><span class="sxs-lookup"><span data-stu-id="2c723-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="2c723-192">Démarrage rapide de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2c723-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="2c723-193">Sauvegarde et restauration de Reliable Services (récupération d’urgence)</span><span class="sxs-lookup"><span data-stu-id="2c723-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="2c723-194">Référence du développeur pour les Collections fiables</span><span class="sxs-lookup"><span data-stu-id="2c723-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

