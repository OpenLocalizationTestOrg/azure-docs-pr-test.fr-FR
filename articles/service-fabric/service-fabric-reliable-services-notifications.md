---
title: notifications de Services aaaReliable | Documents Microsoft
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
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="e4f5f-103">Notifications Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e4f5f-103">Reliable Services notifications</span></span>
<span data-ttu-id="e4f5f-104">Notifications d’autorisent les clients modifications hello tootrack qui font objet tooan qui les intéresse.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="e4f5f-105">Deux types d’objets prennent en charge les notifications : *Gestionnaire d’état fiable* et *Dictionnaire fiable*.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="e4f5f-106">Raisons courantes d’utiliser les notifications :</span><span class="sxs-lookup"><span data-stu-id="e4f5f-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="e4f5f-107">Construction matérialisée, tels que les index secondaires ou agrégées des vues filtrées de l’état du réplica hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="e4f5f-108">Par exemple, un index trié de toutes les clés d’un dictionnaire fiable.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="e4f5f-109">Envoi de données analyse, tels que quantité, hello pour les utilisateurs ajoutés Bonjour dernière heure.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="e4f5f-110">Les notifications sont déclenchées dans le cadre de l’application d’opérations.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="e4f5f-111">Pour cette raison, les notifications doivent être traitées le plus rapidement possible, et les événements synchrones ne doivent pas inclure d’opérations coûteuses.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="e4f5f-112">Notifications du Gestionnaire d’état fiable</span><span class="sxs-lookup"><span data-stu-id="e4f5f-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="e4f5f-113">Gestionnaire d’état de fiable fournit des notifications pour hello suivant des événements :</span><span class="sxs-lookup"><span data-stu-id="e4f5f-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="e4f5f-114">Transaction</span><span class="sxs-lookup"><span data-stu-id="e4f5f-114">Transaction</span></span>
  * <span data-ttu-id="e4f5f-115">Validation</span><span class="sxs-lookup"><span data-stu-id="e4f5f-115">Commit</span></span>
* <span data-ttu-id="e4f5f-116">Gestionnaire d’état</span><span class="sxs-lookup"><span data-stu-id="e4f5f-116">State manager</span></span>
  * <span data-ttu-id="e4f5f-117">Reconstruction</span><span class="sxs-lookup"><span data-stu-id="e4f5f-117">Rebuild</span></span>
  * <span data-ttu-id="e4f5f-118">Ajout d’un état fiable</span><span class="sxs-lookup"><span data-stu-id="e4f5f-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="e4f5f-119">Suppression d’un état fiable</span><span class="sxs-lookup"><span data-stu-id="e4f5f-119">Removal of a reliable state</span></span>

<span data-ttu-id="e4f5f-120">Gestionnaire d’état de Reliable assure le suivi des hello actuel séquentiels.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="e4f5f-121">Hello de seule modification dans l’état de transaction qui provoque un toobe notification déclenché est une transaction en cours de validation.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="e4f5f-122">Le Gestionnaire d’état fiable tient à jour une collection d’états fiables comme Dictionnaire fiable et File d’attente fiable.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="e4f5f-123">Gestionnaire d’état de Reliable déclenche des notifications lors de la modification de cette collection : un état fiable est ajouté ou supprimé, ou ensemble de la collection hello est reconstruit.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="e4f5f-124">Hello collection du Gestionnaire d’état fiable est reconstruit dans trois cas :</span><span class="sxs-lookup"><span data-stu-id="e4f5f-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="e4f5f-125">Récupération : Démarrage d’un réplica, il récupère son état précédent à partir du disque de hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="e4f5f-126">À la fin hello de la récupération, il utilise **NotifyStateManagerChangedEventArgs** toofire un événement qui contient le jeu hello des États fiables récupérées.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="e4f5f-127">Copie complète : avant un réplica peut joindre le jeu de configuration hello, il a toobe généré.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="e4f5f-128">Dans certains cas, cela nécessite une copie complète de l’état du Gestionnaire d’état fiable hello réplica principal toobe toohello appliqué inactif réplica secondaire.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="e4f5f-129">Gestionnaire d’état de la fiable sur les utilisations de réplica secondaire hello **NotifyStateManagerChangedEventArgs** toofire un événement qui contient le jeu hello des États fiables dont elle a acquis à partir du réplica principal de hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="e4f5f-130">Restauration : Dans les scénarios de récupération d’urgence, état du réplica hello peut être restaurée à partir d’une sauvegarde via **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="e4f5f-131">Dans ce cas, le Gestionnaire d’état fiable sur le réplica principal de hello utilise **NotifyStateManagerChangedEventArgs** toofire un événement qui contient le jeu hello des États fiables dont il est restauré à partir de la sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="e4f5f-132">tooregister pour les notifications de transactions et/ou notifications de gestionnaire d’état, vous devez tooregister avec hello **TransactionChanged** ou **StateManagerChanged** événements sur le Gestionnaire d’état fiable.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="e4f5f-133">Un emplacement commun tooregister avec ces gestionnaires d’événements est le constructeur hello de votre service avec état.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="e4f5f-134">Lorsque vous enregistrez sur le constructeur de hello, toute notification qui est provoquée par une modification au cours de la durée de vie hello de ne pas perdre **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="e4f5f-135">Hello **TransactionChanged** Gestionnaire d’événements **NotifyTransactionChangedEventArgs** tooprovide plus d’informations sur l’événement hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="e4f5f-136">Il contient la propriété d’action hello (par exemple, **NotifyTransactionChangedAction.Commit**) qui spécifie le type hello de modification.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="e4f5f-137">Il contient également la propriété transaction hello qui fournit une transaction toohello de référence qui a modifié.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="e4f5f-138">Aujourd'hui, **TransactionChanged** sont déclenchés uniquement si hello transaction est validée.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="e4f5f-139">Hello action est alors égale trop**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="e4f5f-140">Mais dans hello future, des événements peuvent être levées pour les autres types de modifications d’état de transaction.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="e4f5f-141">Nous vous recommandons de vérifier l’action de hello et le traitement d’événement de hello uniquement si c’est un que vous attendez.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="e4f5f-142">Voici un exemple de gestionnaire d’événements **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="e4f5f-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="e4f5f-143">Hello **StateManagerChanged** Gestionnaire d’événements **NotifyStateManagerChangedEventArgs** tooprovide plus d’informations sur l’événement hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="e4f5f-144">**NotifyStateManagerChangedEventArgs** comporte deux sous-classes : **NotifyStateManagerRebuildEventArgs** et **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="e4f5f-145">Vous utilisez la propriété d’action hello dans **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** sous-classe correcte de toohello :</span><span class="sxs-lookup"><span data-stu-id="e4f5f-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="e4f5f-146">**NotifyStateManagerChangedAction.Rebuild** : **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e4f5f-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="e4f5f-147">**NotifyStateManagerChangedAction.Add** et **NotifyStateManagerChangedAction.Remove** : **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e4f5f-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="e4f5f-148">Voici un exemple de gestionnaire de notification **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="e4f5f-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="e4f5f-149">Notifications Dictionnaire fiable</span><span class="sxs-lookup"><span data-stu-id="e4f5f-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="e4f5f-150">Dictionnaire fiable fournit des notifications pour hello suivant des événements :</span><span class="sxs-lookup"><span data-stu-id="e4f5f-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="e4f5f-151">Reconstruction : appelée quand **ReliableDictionary** a récupéré son état à partir d’une sauvegarde ou d’un état local récupéré ou copié.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="e4f5f-152">Effacer : Appelée quand hello état de **ReliableDictionary** a été effacé via hello **ClearAsync** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e4f5f-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="e4f5f-153">Ajouter : Appelée quand un élément a été ajouté trop**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="e4f5f-154">Mise à jour : appelée quand un élément de **IReliableDictionary** a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="e4f5f-155">Suppression : appelée quand un élément de **IReliableDictionary** a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="e4f5f-156">notifications de dictionnaire fiable tooget, vous devez tooregister avec hello **DictionaryChanged** Gestionnaire d’événements **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="e4f5f-157">Un emplacement commun tooregister avec ces gestionnaires d’événements est Bonjour **ReliableStateManager.StateManagerChanged** ajouter la notification.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="e4f5f-158">L’inscription lorsque **IReliableDictionary** est ajouté trop**IReliableStateManager** permet de s’assurer que vous ne perdrez toutes les notifications.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="e4f5f-159">**ProcessStateManagerSingleEntityNotification** est méthode d’échantillonnage hello que hello précédent **OnStateManagerChangedHandler** exemple appelle.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="e4f5f-160">Hello code précédent définit hello **IReliableNotificationAsyncCallback** de l’interface, ainsi que par **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="e4f5f-161">Étant donné que **NotifyDictionaryRebuildEventArgs** contient un **IAsyncEnumerable** interface--qui nécessite le toobe énuméré de façon asynchrone--reconstruction notifications sont déclenchées par le biais  **RebuildNotificationAsyncCallback** au lieu de **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="e4f5f-162">Bonjour précédant le code, dans le cadre de la notification de traitement hello rebuild, première hello conservées États agrégés est désactivée.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="e4f5f-163">Étant donné que la collection fiable de hello est reconstruite avec un nouvel état, toutes les notifications précédentes sont sans importance.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="e4f5f-164">Hello **DictionaryChanged** Gestionnaire d’événements **NotifyDictionaryChangedEventArgs** tooprovide plus d’informations sur l’événement hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="e4f5f-165">**NotifyDictionaryChangedEventArgs** a cinq sous-classes.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="e4f5f-166">Utilisez la propriété d’action hello dans **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** sous-classe correcte de toohello :</span><span class="sxs-lookup"><span data-stu-id="e4f5f-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="e4f5f-167">**NotifyDictionaryChangedAction.Rebuild** : **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e4f5f-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="e4f5f-168">**NotifyDictionaryChangedAction.Clear** : **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e4f5f-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="e4f5f-169">**NotifyDictionaryChangedAction.Add** et **NotifyDictionaryChangedAction.Remove** : **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e4f5f-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="e4f5f-170">**NotifyDictionaryChangedAction.Update** : **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e4f5f-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="e4f5f-171">**NotifyDictionaryChangedAction.Remove** : **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="e4f5f-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="e4f5f-172">Recommandations</span><span class="sxs-lookup"><span data-stu-id="e4f5f-172">Recommendations</span></span>
* <span data-ttu-id="e4f5f-173">*Complétez* les événements de notification le plus rapidement possible.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="e4f5f-174">*N’exécutez aucune* opération coûteuse (par exemple des opérations d’E/S) dans le cadre d’événements synchrones.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="e4f5f-175">*Faire* vérifier le type d’action hello avant de traiter les événements hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="e4f5f-176">Nouveaux types d’action peuvent être ajoutées dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="e4f5f-177">Voici certains tookeep choses à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="e4f5f-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="e4f5f-178">Les notifications sont déclenchées dans le cadre de l’exécution de hello d’une opération.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="e4f5f-179">Par exemple, une notification de restauration est déclenchée comme hello dernière étape d’une opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="e4f5f-180">Une restauration ne se termine pas tant qu’événement de notification hello est traité.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="e4f5f-181">Étant donné que les notifications sont déclenchées dans le cadre de hello appliquant opérations, les clients voient uniquement les notifications pour les opérations validées localement.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="e4f5f-182">Et parce que les opérations sont garanties uniquement les toobe validée localement (en d’autres termes, connecté), elles peuvent ou ne peuvent pas être annulées dans hello futures.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="e4f5f-183">Sur le chemin d’accès de la restauration par progression hello, une seule notification est déclenchée pour chaque opération appliquée.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="e4f5f-184">Cela signifie que si la transaction T1 inclut Create(X), Delete(X) et Create(X), vous recevrez une notification pour la création de hello de X, une pour la suppression de hello et une pour la création de hello, dans cet ordre.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="e4f5f-185">Pour les transactions qui contiennent plusieurs opérations, les opérations sont appliquées dans l’ordre de hello dans lequel ils ont été reçus sur le réplica principal à partir de l’utilisateur de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="e4f5f-186">Lors du traitement d’une mauvaise progression, certaines opérations peuvent être annulées.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="e4f5f-187">Pour des opérations d’annulation, état hello hello réplica tooa arrière stable point de restauration, les notifications sont déclenchées.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="e4f5f-188">Les notifications d’annulation présentent une importante différence. En effet, les événements avec des clés en double sont agrégés.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="e4f5f-189">Par exemple, si la transaction T1 est annulée, vous verrez un tooDelete(X) notification unique.</span><span class="sxs-lookup"><span data-stu-id="e4f5f-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4f5f-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e4f5f-190">Next steps</span></span>
* [<span data-ttu-id="e4f5f-191">Collections fiables</span><span class="sxs-lookup"><span data-stu-id="e4f5f-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="e4f5f-192">Démarrage rapide de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="e4f5f-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="e4f5f-193">Sauvegarde et restauration de Reliable Services (récupération d’urgence)</span><span class="sxs-lookup"><span data-stu-id="e4f5f-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="e4f5f-194">Référence du développeur pour les Collections fiables</span><span class="sxs-lookup"><span data-stu-id="e4f5f-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

