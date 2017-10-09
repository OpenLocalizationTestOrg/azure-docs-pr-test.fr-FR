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
# <a name="reliable-services-notifications"></a>Notifications Reliable Services
Notifications d’autorisent les clients modifications hello tootrack qui font objet tooan qui les intéresse. Deux types d’objets prennent en charge les notifications : *Gestionnaire d’état fiable* et *Dictionnaire fiable*.

Raisons courantes d’utiliser les notifications :

* Construction matérialisée, tels que les index secondaires ou agrégées des vues filtrées de l’état du réplica hello. Par exemple, un index trié de toutes les clés d’un dictionnaire fiable.
* Envoi de données analyse, tels que quantité, hello pour les utilisateurs ajoutés Bonjour dernière heure.

Les notifications sont déclenchées dans le cadre de l’application d’opérations. Pour cette raison, les notifications doivent être traitées le plus rapidement possible, et les événements synchrones ne doivent pas inclure d’opérations coûteuses.

## <a name="reliable-state-manager-notifications"></a>Notifications du Gestionnaire d’état fiable
Gestionnaire d’état de fiable fournit des notifications pour hello suivant des événements :

* Transaction
  * Validation
* Gestionnaire d’état
  * Reconstruction
  * Ajout d’un état fiable
  * Suppression d’un état fiable

Gestionnaire d’état de Reliable assure le suivi des hello actuel séquentiels. Hello de seule modification dans l’état de transaction qui provoque un toobe notification déclenché est une transaction en cours de validation.

Le Gestionnaire d’état fiable tient à jour une collection d’états fiables comme Dictionnaire fiable et File d’attente fiable. Gestionnaire d’état de Reliable déclenche des notifications lors de la modification de cette collection : un état fiable est ajouté ou supprimé, ou ensemble de la collection hello est reconstruit.
Hello collection du Gestionnaire d’état fiable est reconstruit dans trois cas :

* Récupération : Démarrage d’un réplica, il récupère son état précédent à partir du disque de hello. À la fin hello de la récupération, il utilise **NotifyStateManagerChangedEventArgs** toofire un événement qui contient le jeu hello des États fiables récupérées.
* Copie complète : avant un réplica peut joindre le jeu de configuration hello, il a toobe généré. Dans certains cas, cela nécessite une copie complète de l’état du Gestionnaire d’état fiable hello réplica principal toobe toohello appliqué inactif réplica secondaire. Gestionnaire d’état de la fiable sur les utilisations de réplica secondaire hello **NotifyStateManagerChangedEventArgs** toofire un événement qui contient le jeu hello des États fiables dont elle a acquis à partir du réplica principal de hello.
* Restauration : Dans les scénarios de récupération d’urgence, état du réplica hello peut être restaurée à partir d’une sauvegarde via **RestoreAsync**. Dans ce cas, le Gestionnaire d’état fiable sur le réplica principal de hello utilise **NotifyStateManagerChangedEventArgs** toofire un événement qui contient le jeu hello des États fiables dont il est restauré à partir de la sauvegarde de hello.

tooregister pour les notifications de transactions et/ou notifications de gestionnaire d’état, vous devez tooregister avec hello **TransactionChanged** ou **StateManagerChanged** événements sur le Gestionnaire d’état fiable. Un emplacement commun tooregister avec ces gestionnaires d’événements est le constructeur hello de votre service avec état. Lorsque vous enregistrez sur le constructeur de hello, toute notification qui est provoquée par une modification au cours de la durée de vie hello de ne pas perdre **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Hello **TransactionChanged** Gestionnaire d’événements **NotifyTransactionChangedEventArgs** tooprovide plus d’informations sur l’événement hello. Il contient la propriété d’action hello (par exemple, **NotifyTransactionChangedAction.Commit**) qui spécifie le type hello de modification. Il contient également la propriété transaction hello qui fournit une transaction toohello de référence qui a modifié.

> [!NOTE]
> Aujourd'hui, **TransactionChanged** sont déclenchés uniquement si hello transaction est validée. Hello action est alors égale trop**NotifyTransactionChangedAction.Commit**. Mais dans hello future, des événements peuvent être levées pour les autres types de modifications d’état de transaction. Nous vous recommandons de vérifier l’action de hello et le traitement d’événement de hello uniquement si c’est un que vous attendez.
> 
> 

Voici un exemple de gestionnaire d’événements **TransactionChanged** .

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

Hello **StateManagerChanged** Gestionnaire d’événements **NotifyStateManagerChangedEventArgs** tooprovide plus d’informations sur l’événement hello.
**NotifyStateManagerChangedEventArgs** comporte deux sous-classes : **NotifyStateManagerRebuildEventArgs** et **NotifyStateManagerSingleEntityChangedEventArgs**.
Vous utilisez la propriété d’action hello dans **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** sous-classe correcte de toohello :

* **NotifyStateManagerChangedAction.Rebuild** : **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** et **NotifyStateManagerChangedAction.Remove** : **NotifyStateManagerSingleEntityChangedEventArgs**

Voici un exemple de gestionnaire de notification **StateManagerChanged** .

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

## <a name="reliable-dictionary-notifications"></a>Notifications Dictionnaire fiable
Dictionnaire fiable fournit des notifications pour hello suivant des événements :

* Reconstruction : appelée quand **ReliableDictionary** a récupéré son état à partir d’une sauvegarde ou d’un état local récupéré ou copié.
* Effacer : Appelée quand hello état de **ReliableDictionary** a été effacé via hello **ClearAsync** (méthode).
* Ajouter : Appelée quand un élément a été ajouté trop**ReliableDictionary**.
* Mise à jour : appelée quand un élément de **IReliableDictionary** a été mis à jour.
* Suppression : appelée quand un élément de **IReliableDictionary** a été supprimé.

notifications de dictionnaire fiable tooget, vous devez tooregister avec hello **DictionaryChanged** Gestionnaire d’événements **IReliableDictionary**. Un emplacement commun tooregister avec ces gestionnaires d’événements est Bonjour **ReliableStateManager.StateManagerChanged** ajouter la notification.
L’inscription lorsque **IReliableDictionary** est ajouté trop**IReliableStateManager** permet de s’assurer que vous ne perdrez toutes les notifications.

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
> **ProcessStateManagerSingleEntityNotification** est méthode d’échantillonnage hello que hello précédent **OnStateManagerChangedHandler** exemple appelle.
> 
> 

Hello code précédent définit hello **IReliableNotificationAsyncCallback** de l’interface, ainsi que par **DictionaryChanged**. Étant donné que **NotifyDictionaryRebuildEventArgs** contient un **IAsyncEnumerable** interface--qui nécessite le toobe énuméré de façon asynchrone--reconstruction notifications sont déclenchées par le biais  **RebuildNotificationAsyncCallback** au lieu de **OnDictionaryChangedHandler**.

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
> Bonjour précédant le code, dans le cadre de la notification de traitement hello rebuild, première hello conservées États agrégés est désactivée. Étant donné que la collection fiable de hello est reconstruite avec un nouvel état, toutes les notifications précédentes sont sans importance.
> 
> 

Hello **DictionaryChanged** Gestionnaire d’événements **NotifyDictionaryChangedEventArgs** tooprovide plus d’informations sur l’événement hello.
**NotifyDictionaryChangedEventArgs** a cinq sous-classes. Utilisez la propriété d’action hello dans **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** sous-classe correcte de toohello :

* **NotifyDictionaryChangedAction.Rebuild** : **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear** : **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** et **NotifyDictionaryChangedAction.Remove** : **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update** : **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove** : **NotifyDictionaryItemRemovedEventArgs**

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

## <a name="recommendations"></a>Recommandations
* *Complétez* les événements de notification le plus rapidement possible.
* *N’exécutez aucune* opération coûteuse (par exemple des opérations d’E/S) dans le cadre d’événements synchrones.
* *Faire* vérifier le type d’action hello avant de traiter les événements hello. Nouveaux types d’action peuvent être ajoutées dans hello futures.

Voici certains tookeep choses à l’esprit :

* Les notifications sont déclenchées dans le cadre de l’exécution de hello d’une opération. Par exemple, une notification de restauration est déclenchée comme hello dernière étape d’une opération de restauration. Une restauration ne se termine pas tant qu’événement de notification hello est traité.
* Étant donné que les notifications sont déclenchées dans le cadre de hello appliquant opérations, les clients voient uniquement les notifications pour les opérations validées localement. Et parce que les opérations sont garanties uniquement les toobe validée localement (en d’autres termes, connecté), elles peuvent ou ne peuvent pas être annulées dans hello futures.
* Sur le chemin d’accès de la restauration par progression hello, une seule notification est déclenchée pour chaque opération appliquée. Cela signifie que si la transaction T1 inclut Create(X), Delete(X) et Create(X), vous recevrez une notification pour la création de hello de X, une pour la suppression de hello et une pour la création de hello, dans cet ordre.
* Pour les transactions qui contiennent plusieurs opérations, les opérations sont appliquées dans l’ordre de hello dans lequel ils ont été reçus sur le réplica principal à partir de l’utilisateur de hello de hello.
* Lors du traitement d’une mauvaise progression, certaines opérations peuvent être annulées. Pour des opérations d’annulation, état hello hello réplica tooa arrière stable point de restauration, les notifications sont déclenchées. Les notifications d’annulation présentent une importante différence. En effet, les événements avec des clés en double sont agrégés. Par exemple, si la transaction T1 est annulée, vous verrez un tooDelete(X) notification unique.

## <a name="next-steps"></a>Étapes suivantes
* [Collections fiables](service-fabric-work-with-reliable-collections.md)
* [Démarrage rapide de Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Sauvegarde et restauration de Reliable Services (récupération d’urgence)](service-fabric-reliable-services-backup-restore.md)
* [Référence du développeur pour les Collections fiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

