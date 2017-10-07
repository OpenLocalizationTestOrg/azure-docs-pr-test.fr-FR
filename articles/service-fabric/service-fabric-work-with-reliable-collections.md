---
title: aaaWorking avec des Collections fiable | Documents Microsoft
description: En savoir plus hello meilleures pratiques pour travailler avec des Collections fiable.
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a>Utilisation des collections fiables
L’infrastructure de service offre un dynamique, les développeurs de modèles too.NET disponibles via les Collections fiable de programmation. Plus précisément, Service Fabric fournit un dictionnaire fiable et des classes de file d’attente fiables. Lorsque vous utilisez ces classes, votre état est partitionné (pour l’évolutivité) répliqué (pour la disponibilité) et traité dans une partition (pour la sémantique ACID). Nous allons examiner un exemple d’utilisation type d’un objet de dictionnaire fiable afin de voir ses fonctionnalités réelles.

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

Toutes les opérations sur les objets de dictionnaire fiable (à l’exception de ClearAsync qui n’est pas annulable), nécessitent un objet ITransaction. Cet objet est associé à n’importe quel et toutes les modifications que vous essayez de dictionnaire fiable de toomake tooany et/ou à des objets de file d’attente fiable au sein d’une seule partition. Vous acquérez une ITransaction objet en appelant la partition de hello de méthode de CreateTransaction de StateManager.

Dans le code hello ci-dessus, objet ITransaction de hello est passé de méthode de AddAsync du dictionnaire tooa fiable. En interne, les méthodes de dictionnaire qui accepte une clé prennent un verrou de lecteur/writer associé hello clé. Si la méthode hello modifie la valeur de clé hello, méthode hello prend un verrou d’écriture sur la clé de hello et si la méthode hello lit uniquement à partir de la valeur de clé hello, un verrou de lecture est effectué sur la clé de hello. Étant donné que AddAsync modifie toohello de valeur de la clé hello nouveau, valeur passée, verrou d’écriture de la clé hello est effectuée. Par conséquent, si les threads de 2 (ou plus) tentent de valeurs tooadd avec hello même clé à hello même temps, un thread doit acquérir le verrou d’écriture hello et hello autres threads se bloquent. Par défaut, le bloc de méthodes pour le verrou de hello tooacquire too4 secondes ; après 4 secondes, les méthodes de hello lèvent une exception TimeoutException. Les surcharges de méthode existent permettant vous toopass une valeur de délai d’attente explicite si vous préférez.

En règle générale, vous écrivez votre tooa tooreact de code TimeoutException en interceptant et recommencer l’opération entière de hello (comme indiqué dans le code hello ci-dessus). Dans mon code simple, j’appelle simplement Task.Delay en transmettant à chaque fois 100 millisecondes. Mais, en réalité, vous pouvez juger préférable d’utiliser un type de délai de temporisation exponentiel.

Une fois que l’acquisition de verrou de hello, AddAsync ajoute la clé de hello et objet de valeur fait référence à tooan dictionnaire temporaire interne associé à hello ITransaction objet. Cette opération est effectuée tooprovide vous avec la sémantique en lecture-your-propriétaire-écrit. Autrement dit, après avoir appelé AddAsync, un tooTryGetValueAsync appel ultérieure (à l’aide de hello le même objet ITransaction) retourne la valeur de hello même si vous n’avez pas encore validé transaction de hello. Ensuite, AddAsync sérialise votre clé et valeur toobyte tableaux des objets et ajoute ces fichiers de journal octets tableaux tooa sur le nœud local hello. Pour finir, AddAsync envoie hello octets tableaux tooall hello réplicas secondaires afin qu’ils ont hello même cléent/valeur d’informations. Bien que les informations de clé/valeur hello a été écrit tooa du journal, les informations de hello ne sont pas considéré comme partie du dictionnaire de hello jusqu'à ce que la transaction de hello auxquels ils sont associés a été validée.

Dans le code hello ci-dessus, hello appel tooCommitAsync valide toutes les opérations de la transaction hello. Plus précisément, il ajoute le fichier journal toohello d’informations de validation sur le nœud local hello et envoie également hello validation tooall enregistrement hello réplicas secondaires. Une fois qu’un quorum (majorité) des réplicas de hello a répondu, toutes les données de modifications sont considérées comme permanentes et tous les verrous associés aux clés qui ont été manipulées via l’objet de ITransaction hello sont libérés pour manipuler des autres threads/transactions hello des mêmes clés et leurs valeurs.

Si CommitAsync n’est pas appelée (généralement en raison de la levée d’exception tooan), objet de ITransaction hello détruit. Lorsque la suppression d’un objet de ITransaction non validé, le Service Fabric ajoute abandon informations toohello local du fichier journal des nœuds et aucune opération ne doit toobe envoyé tooany Hello réplicas secondaires. Et ensuite, tous les verrous associés aux clés qui ont été manipulées via les transactions hello sont libérées.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>Pièges courants et comment tooavoid les
Maintenant que vous comprenez le fonctionnement des collections de fiable hello en interne, examinons certains frauduleuse courantes d'entre eux. Consultez le code hello ci-dessous :

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

Lorsque vous travaillez avec un dictionnaire .NET standard, vous pouvez ajouter un dictionnaire de toohello clé/valeur et puis modifiez la valeur hello d’une propriété (par exemple, LastLogin). Toutefois, ce code ne fonctionnera pas correctement avec un dictionnaire fiable. N’oubliez pas de hello discussion précédente, appel hello tooAddAsync sérialise hello clé/valeur des objets toobyte tableaux et enregistre hello tableaux tooa des fichiers locaux, puis envoie les réplicas secondaires de toohello. Si vous modifiez ultérieurement une propriété, cela modifie de valeur de la propriété hello en mémoire uniquement. Il n’affecte pas le fichier local de hello ou données hello envoyées toohello réplicas. Si les processus hello tombe en panne, ce qui est en mémoire est levée immédiatement. Lorsqu’un nouveau processus démarre, ou si un autre réplica devienne le réplica principal, puis hello ancienne valeur de propriété est ce qui est disponible.

Je ne parviens pas à une contrainte suffisamment comment il est facile de type hello de toomake d’erreur indiqué ci-dessus. Et vous seulement découvrirez commettre l’erreur hello si/quand les processus hello tombe en panne. code de hello toowrite Hello façon correcte est simplement tooreverse hello deux lignes :


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

Voici un autre exemple d’erreur courante :

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

Là encore, avec les dictionnaires .NET régulières, code hello ci-dessus fonctionne correctement et est un modèle commun : développeur de hello utilise une clé toolook une valeur. Si la valeur de hello existe, développeur de hello modifie une valeur de propriété. Toutefois, les regroupements fiable, ce code expose hello même problème comme indiqué précédemment : **vous ne devez pas modifier un objet une fois que vous avez donné il collecte fiable de tooa.**

Hello correct tooupdate de façon une valeur dans une collection fiable, est tooget une valeur existante de référence toohello et envisagez hello fait référence objet tooby cette référence immuable. Ensuite, créez un nouvel objet qui est une copie exacte de l’objet d’origine de hello. Maintenant, vous pouvez modifier l’état de hello de ce nouvel objet et écrire du nouvel objet de hello dans la collection de hello afin qu’elle est sérialisée toobyte tableaux, toohello ajouté des fichiers locaux et envoyé toohello réplicas. Après validation hello modification (s), les objets en mémoire hello, fichier local de hello, et tous les réplicas de hello ont hello même exacte d’état. Tout est parfait !

code Hello ci-dessous montre tooupdate de façon correcte hello une valeur dans une collection fiable :

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>Erreur de données immuables types tooprevent programmeur de définir
Dans l’idéal, nous aimerions les erreurs tooreport hello du compilateur lorsque vous produisez accidentellement le code qui transforme l’état d’un objet que vous êtes supposé tooconsider immuable. Mais, du compilateur c# hello n’a pas hello capacité toodo cela. C’est le cas, tooavoid potentielle programmeur aux bogues, nous recommandons vivement que vous définissez les types hello que vous utilisez avec des types de collections fiable toobe immuable. Plus précisément, cela signifie que vous respectez toocore des types de valeur (par exemple, des nombres [Int32, UInt64, etc.], DateTime, Guid, TimeSpan et hello comme). Et, bien sûr, vous pouvez également utiliser des chaînes. Il s’agit des propriétés de collection tooavoid meilleures en tant que la sérialisation et désérialisant permettre fréquemment peut nuire aux performances. Toutefois, si vous souhaitez que les propriétés de la collection toouse, nous vous recommandons utiliser hello. Bibliothèque de collections immuables de NET ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). Cette bibliothèque est disponible au téléchargement sur http://nuget.org. Nous vous recommandons également de sceller vos classes et de définir les champs en lecture seule chaque fois que cela est possible.

Hello type UserInfo ci-dessous montre comment toodefine un immuable type en tirant profit des recommandations susmentionnées.

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

Hello ItemId type est également un type immuable comme indiqué ici :

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a>Contrôle de version du schéma (mises à niveau)
En interne, les collections fiables sérialisent vos objets à l’aide du DataContractSerializer de .NET. les objets sérialisé de Hello sont disque du réplica principal toohello persistantes et également transmise toohello réplicas secondaires. Votre service arrive à maturité, il est probable que vous souhaitiez le genre de hello toochange de données (schéma), que votre service requiert. Vous devez aborder la question du contrôle de version de vos données avec une extrême prudence. Tout d’abord, vous devez toujours être en mesure de toodeserialize anciennes données. Plus précisément, cela signifie que votre code de désérialisation doit être infini descendante : 333 de Version de votre code de service doit être en mesure de toooperate sur les données placées dans une collection fiable par la version 1 de votre code de service, il y a 5 ans.

En outre, le code de service est mis à niveau à raison d’un domaine de mise à niveau à la fois. Par conséquent, pendant une mise à niveau, deux versions différentes de votre code de service s’exécutent simultanément. Vous devez éviter hello nouvelle version de votre code de service utilisent hello nouveau schéma comme les anciennes versions de votre code de service peuvent ne pas être en mesure de toohandle schéma hello. Lorsque cela est possible, vous devez concevoir chaque version de votre ascendante toobe de service par la 1 version. Plus précisément, cela signifie que V1 de votre code de service doit être en mesure de toosimply ignorer tous les éléments de schéma ne gère pas explicitement. Toutefois, il doit être en mesure de toosave toutes les données qu’elle n’explicitement connaître et il suffit d’écrire de restauration lors de la mise à jour d’une valeur ou une clé de dictionnaire.

> [!WARNING]
> Pendant que vous pouvez modifier le schéma hello d’une clé, vous devez vous assurer que le code de hachage de votre clé et algorithmes d’est égal à sont stables. Si vous modifiez un de ces algorithmes de fonctionnement, vous pas sera en mesure de toolook clé hello au sein du dictionnaire de fiable hello jamais à nouveau.
>
>

Vous pouvez également effectuer ce qui est généralement référencés tooas une phase 2 mise à niveau. Une mise à niveau de la phase 2, vous mettez à niveau votre service V1 tooV2 : V2 contient le code hello qui sait comment toodeal avec un nouveau changement de schéma hello mais ce code ne s’exécute. Lorsque hello V2 code lit les données de V1, il fonctionne sur celui-ci et écrit des données de V1. Ensuite, une fois la mise à niveau hello est terminée sur tous les domaines de mise à niveau, vous pouvez signaler toohello en cours d’exécution V2 instances que cette mise à niveau hello est terminée. (Une façon toosignal tooroll une mise à niveau de la configuration ; c’est ce qui en fait une mise à niveau de la phase 2.) Maintenant, hello V2 instances peuvent lire les données de V1, convertir les données tooV2, exploiter et écrire en tant que données V2. Lorsque d’autres instances de lire les données de V2, ils n’ont pas besoin tooconvert, elles fonctionnent sur ce dernier et simplement écrire les données de V2.

## <a name="next-steps"></a>Étapes suivantes
toolearn sur la création de contrats de données compatible vers l’avant, consultez [les contrats de données de compatibilité ascendante](https://msdn.microsoft.com/library/ms731083.aspx).

meilleures pratiques de toolearn sur le contrôle de version des contrats de données, consultez [contrôle de version de contrat de données](https://msdn.microsoft.com/library/ms731138.aspx).

toolearn les contrats de données à tolérance de version tooimplement, voir [des rappels de sérialisation avec tolérance de Version](https://msdn.microsoft.com/library/ms733734.aspx).

toolearn tooprovide une structure de données qui peut interagir entre plusieurs versions, voir [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).
