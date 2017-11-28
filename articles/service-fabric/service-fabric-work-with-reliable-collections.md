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
# <a name="working-with-reliable-collections"></a><span data-ttu-id="b51f9-103">Utilisation des collections fiables</span><span class="sxs-lookup"><span data-stu-id="b51f9-103">Working with Reliable Collections</span></span>
<span data-ttu-id="b51f9-104">L’infrastructure de service offre un dynamique, les développeurs de modèles too.NET disponibles via les Collections fiable de programmation.</span><span class="sxs-lookup"><span data-stu-id="b51f9-104">Service Fabric offers a stateful programming model available too.NET developers via Reliable Collections.</span></span> <span data-ttu-id="b51f9-105">Plus précisément, Service Fabric fournit un dictionnaire fiable et des classes de file d’attente fiables.</span><span class="sxs-lookup"><span data-stu-id="b51f9-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="b51f9-106">Lorsque vous utilisez ces classes, votre état est partitionné (pour l’évolutivité) répliqué (pour la disponibilité) et traité dans une partition (pour la sémantique ACID).</span><span class="sxs-lookup"><span data-stu-id="b51f9-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="b51f9-107">Nous allons examiner un exemple d’utilisation type d’un objet de dictionnaire fiable afin de voir ses fonctionnalités réelles.</span><span class="sxs-lookup"><span data-stu-id="b51f9-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

<span data-ttu-id="b51f9-108">Toutes les opérations sur les objets de dictionnaire fiable (à l’exception de ClearAsync qui n’est pas annulable), nécessitent un objet ITransaction.</span><span class="sxs-lookup"><span data-stu-id="b51f9-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="b51f9-109">Cet objet est associé à n’importe quel et toutes les modifications que vous essayez de dictionnaire fiable de toomake tooany et/ou à des objets de file d’attente fiable au sein d’une seule partition.</span><span class="sxs-lookup"><span data-stu-id="b51f9-109">This object has associated with it any and all changes you’re attempting toomake tooany reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="b51f9-110">Vous acquérez une ITransaction objet en appelant la partition de hello de méthode de CreateTransaction de StateManager.</span><span class="sxs-lookup"><span data-stu-id="b51f9-110">You acquire an ITransaction object by calling hello partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="b51f9-111">Dans le code hello ci-dessus, objet ITransaction de hello est passé de méthode de AddAsync du dictionnaire tooa fiable.</span><span class="sxs-lookup"><span data-stu-id="b51f9-111">In hello code above, hello ITransaction object is passed tooa reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="b51f9-112">En interne, les méthodes de dictionnaire qui accepte une clé prennent un verrou de lecteur/writer associé hello clé.</span><span class="sxs-lookup"><span data-stu-id="b51f9-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with hello key.</span></span> <span data-ttu-id="b51f9-113">Si la méthode hello modifie la valeur de clé hello, méthode hello prend un verrou d’écriture sur la clé de hello et si la méthode hello lit uniquement à partir de la valeur de clé hello, un verrou de lecture est effectué sur la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="b51f9-113">If hello method modifies hello key’s value, hello method takes a write lock on hello key and if hello method only reads from hello key’s value, then a read lock is taken on hello key.</span></span> <span data-ttu-id="b51f9-114">Étant donné que AddAsync modifie toohello de valeur de la clé hello nouveau, valeur passée, verrou d’écriture de la clé hello est effectuée.</span><span class="sxs-lookup"><span data-stu-id="b51f9-114">Since AddAsync modifies hello key’s value toohello new, passed-in value, hello key’s write lock is taken.</span></span> <span data-ttu-id="b51f9-115">Par conséquent, si les threads de 2 (ou plus) tentent de valeurs tooadd avec hello même clé à hello même temps, un thread doit acquérir le verrou d’écriture hello et hello autres threads se bloquent.</span><span class="sxs-lookup"><span data-stu-id="b51f9-115">So, if 2 (or more) threads attempt tooadd values with hello same key at hello same time, one thread will acquire hello write lock and hello other threads will block.</span></span> <span data-ttu-id="b51f9-116">Par défaut, le bloc de méthodes pour le verrou de hello tooacquire too4 secondes ; après 4 secondes, les méthodes de hello lèvent une exception TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="b51f9-116">By default, methods block for up too4 seconds tooacquire hello lock; after 4 seconds, hello methods throw a TimeoutException.</span></span> <span data-ttu-id="b51f9-117">Les surcharges de méthode existent permettant vous toopass une valeur de délai d’attente explicite si vous préférez.</span><span class="sxs-lookup"><span data-stu-id="b51f9-117">Method overloads exist allowing you toopass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="b51f9-118">En règle générale, vous écrivez votre tooa tooreact de code TimeoutException en interceptant et recommencer l’opération entière de hello (comme indiqué dans le code hello ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="b51f9-118">Usually, you write your code tooreact tooa TimeoutException by catching it and retrying hello entire operation (as shown in hello code above).</span></span> <span data-ttu-id="b51f9-119">Dans mon code simple, j’appelle simplement Task.Delay en transmettant à chaque fois 100 millisecondes.</span><span class="sxs-lookup"><span data-stu-id="b51f9-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="b51f9-120">Mais, en réalité, vous pouvez juger préférable d’utiliser un type de délai de temporisation exponentiel.</span><span class="sxs-lookup"><span data-stu-id="b51f9-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="b51f9-121">Une fois que l’acquisition de verrou de hello, AddAsync ajoute la clé de hello et objet de valeur fait référence à tooan dictionnaire temporaire interne associé à hello ITransaction objet.</span><span class="sxs-lookup"><span data-stu-id="b51f9-121">Once hello lock is acquired, AddAsync adds hello key and value object references tooan internal temporary dictionary associated with hello ITransaction object.</span></span> <span data-ttu-id="b51f9-122">Cette opération est effectuée tooprovide vous avec la sémantique en lecture-your-propriétaire-écrit.</span><span class="sxs-lookup"><span data-stu-id="b51f9-122">This is done tooprovide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="b51f9-123">Autrement dit, après avoir appelé AddAsync, un tooTryGetValueAsync appel ultérieure (à l’aide de hello le même objet ITransaction) retourne la valeur de hello même si vous n’avez pas encore validé transaction de hello.</span><span class="sxs-lookup"><span data-stu-id="b51f9-123">That is, after you call AddAsync, a later call tooTryGetValueAsync (using hello same ITransaction object) will return hello value even if you have not yet committed hello transaction.</span></span> <span data-ttu-id="b51f9-124">Ensuite, AddAsync sérialise votre clé et valeur toobyte tableaux des objets et ajoute ces fichiers de journal octets tableaux tooa sur le nœud local hello.</span><span class="sxs-lookup"><span data-stu-id="b51f9-124">Next, AddAsync serializes your key and value objects toobyte arrays and appends these byte arrays tooa log file on hello local node.</span></span> <span data-ttu-id="b51f9-125">Pour finir, AddAsync envoie hello octets tableaux tooall hello réplicas secondaires afin qu’ils ont hello même cléent/valeur d’informations.</span><span class="sxs-lookup"><span data-stu-id="b51f9-125">Finally, AddAsync sends hello byte arrays tooall hello secondary replicas so they have hello same key/value information.</span></span> <span data-ttu-id="b51f9-126">Bien que les informations de clé/valeur hello a été écrit tooa du journal, les informations de hello ne sont pas considéré comme partie du dictionnaire de hello jusqu'à ce que la transaction de hello auxquels ils sont associés a été validée.</span><span class="sxs-lookup"><span data-stu-id="b51f9-126">Even though hello key/value information has been written tooa log file, hello information is not considered part of hello dictionary until hello transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="b51f9-127">Dans le code hello ci-dessus, hello appel tooCommitAsync valide toutes les opérations de la transaction hello.</span><span class="sxs-lookup"><span data-stu-id="b51f9-127">In hello code above, hello call tooCommitAsync commits all of hello transaction’s operations.</span></span> <span data-ttu-id="b51f9-128">Plus précisément, il ajoute le fichier journal toohello d’informations de validation sur le nœud local hello et envoie également hello validation tooall enregistrement hello réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="b51f9-128">Specifically, it appends commit information toohello log file on hello local node and also sends hello commit record tooall hello secondary replicas.</span></span> <span data-ttu-id="b51f9-129">Une fois qu’un quorum (majorité) des réplicas de hello a répondu, toutes les données de modifications sont considérées comme permanentes et tous les verrous associés aux clés qui ont été manipulées via l’objet de ITransaction hello sont libérés pour manipuler des autres threads/transactions hello des mêmes clés et leurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="b51f9-129">Once a quorum (majority) of hello replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via hello ITransaction object are released so other threads/transactions can manipulate hello same keys and their values.</span></span>

<span data-ttu-id="b51f9-130">Si CommitAsync n’est pas appelée (généralement en raison de la levée d’exception tooan), objet de ITransaction hello détruit.</span><span class="sxs-lookup"><span data-stu-id="b51f9-130">If CommitAsync is not called (usually due tooan exception being thrown), then hello ITransaction object gets disposed.</span></span> <span data-ttu-id="b51f9-131">Lorsque la suppression d’un objet de ITransaction non validé, le Service Fabric ajoute abandon informations toohello local du fichier journal des nœuds et aucune opération ne doit toobe envoyé tooany Hello réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="b51f9-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information toohello local node’s log file and nothing needs toobe sent tooany of hello secondary replicas.</span></span> <span data-ttu-id="b51f9-132">Et ensuite, tous les verrous associés aux clés qui ont été manipulées via les transactions hello sont libérées.</span><span class="sxs-lookup"><span data-stu-id="b51f9-132">And then, any locks associated with keys that were manipulated via hello transaction are released.</span></span>

## <a name="common-pitfalls-and-how-tooavoid-them"></a><span data-ttu-id="b51f9-133">Pièges courants et comment tooavoid les</span><span class="sxs-lookup"><span data-stu-id="b51f9-133">Common pitfalls and how tooavoid them</span></span>
<span data-ttu-id="b51f9-134">Maintenant que vous comprenez le fonctionnement des collections de fiable hello en interne, examinons certains frauduleuse courantes d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="b51f9-134">Now that you understand how hello reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="b51f9-135">Consultez le code hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b51f9-135">See hello code below:</span></span>

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

<span data-ttu-id="b51f9-136">Lorsque vous travaillez avec un dictionnaire .NET standard, vous pouvez ajouter un dictionnaire de toohello clé/valeur et puis modifiez la valeur hello d’une propriété (par exemple, LastLogin).</span><span class="sxs-lookup"><span data-stu-id="b51f9-136">When working with a regular .NET dictionary, you can add a key/value toohello dictionary and then change hello value of a property (such as LastLogin).</span></span> <span data-ttu-id="b51f9-137">Toutefois, ce code ne fonctionnera pas correctement avec un dictionnaire fiable.</span><span class="sxs-lookup"><span data-stu-id="b51f9-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="b51f9-138">N’oubliez pas de hello discussion précédente, appel hello tooAddAsync sérialise hello clé/valeur des objets toobyte tableaux et enregistre hello tableaux tooa des fichiers locaux, puis envoie les réplicas secondaires de toohello.</span><span class="sxs-lookup"><span data-stu-id="b51f9-138">Remember from hello earlier discussion, hello call tooAddAsync serializes hello key/value objects toobyte arrays and then saves hello arrays tooa local file and also sends them toohello secondary replicas.</span></span> <span data-ttu-id="b51f9-139">Si vous modifiez ultérieurement une propriété, cela modifie de valeur de la propriété hello en mémoire uniquement. Il n’affecte pas le fichier local de hello ou données hello envoyées toohello réplicas.</span><span class="sxs-lookup"><span data-stu-id="b51f9-139">If you later change a property, this changes hello property’s value in memory only; it does not impact hello local file or hello data sent toohello replicas.</span></span> <span data-ttu-id="b51f9-140">Si les processus hello tombe en panne, ce qui est en mémoire est levée immédiatement.</span><span class="sxs-lookup"><span data-stu-id="b51f9-140">If hello process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="b51f9-141">Lorsqu’un nouveau processus démarre, ou si un autre réplica devienne le réplica principal, puis hello ancienne valeur de propriété est ce qui est disponible.</span><span class="sxs-lookup"><span data-stu-id="b51f9-141">When a new process starts or if another replica becomes primary, then hello old property value is what is available.</span></span>

<span data-ttu-id="b51f9-142">Je ne parviens pas à une contrainte suffisamment comment il est facile de type hello de toomake d’erreur indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b51f9-142">I cannot stress enough how easy it is toomake hello kind of mistake shown above.</span></span> <span data-ttu-id="b51f9-143">Et vous seulement découvrirez commettre l’erreur hello si/quand les processus hello tombe en panne.</span><span class="sxs-lookup"><span data-stu-id="b51f9-143">And, you will only learn about hello mistake if/when hello process goes down.</span></span> <span data-ttu-id="b51f9-144">code de hello toowrite Hello façon correcte est simplement tooreverse hello deux lignes :</span><span class="sxs-lookup"><span data-stu-id="b51f9-144">hello correct way toowrite hello code is simply tooreverse hello two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="b51f9-145">Voici un autre exemple d’erreur courante :</span><span class="sxs-lookup"><span data-stu-id="b51f9-145">Here is another example showing a common mistake:</span></span>

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

<span data-ttu-id="b51f9-146">Là encore, avec les dictionnaires .NET régulières, code hello ci-dessus fonctionne correctement et est un modèle commun : développeur de hello utilise une clé toolook une valeur.</span><span class="sxs-lookup"><span data-stu-id="b51f9-146">Again, with regular .NET dictionaries, hello code above works fine and is a common pattern: hello developer uses a key toolook up a value.</span></span> <span data-ttu-id="b51f9-147">Si la valeur de hello existe, développeur de hello modifie une valeur de propriété.</span><span class="sxs-lookup"><span data-stu-id="b51f9-147">If hello value exists, hello developer changes a property’s value.</span></span> <span data-ttu-id="b51f9-148">Toutefois, les regroupements fiable, ce code expose hello même problème comme indiqué précédemment : **vous ne devez pas modifier un objet une fois que vous avez donné il collecte fiable de tooa.**</span><span class="sxs-lookup"><span data-stu-id="b51f9-148">However, with reliable collections, this code exhibits hello same problem as already discussed: **you MUST not modify an object once you have given it tooa reliable collection.**</span></span>

<span data-ttu-id="b51f9-149">Hello correct tooupdate de façon une valeur dans une collection fiable, est tooget une valeur existante de référence toohello et envisagez hello fait référence objet tooby cette référence immuable.</span><span class="sxs-lookup"><span data-stu-id="b51f9-149">hello correct way tooupdate a value in a reliable collection, is tooget a reference toohello existing value and consider hello object referred tooby this reference immutable.</span></span> <span data-ttu-id="b51f9-150">Ensuite, créez un nouvel objet qui est une copie exacte de l’objet d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="b51f9-150">Then, create a new object which is an exact copy of hello original object.</span></span> <span data-ttu-id="b51f9-151">Maintenant, vous pouvez modifier l’état de hello de ce nouvel objet et écrire du nouvel objet de hello dans la collection de hello afin qu’elle est sérialisée toobyte tableaux, toohello ajouté des fichiers locaux et envoyé toohello réplicas.</span><span class="sxs-lookup"><span data-stu-id="b51f9-151">Now, you can modify hello state of this new object and write hello new object into hello collection so that it gets serialized toobyte arrays, appended toohello local file and sent toohello replicas.</span></span> <span data-ttu-id="b51f9-152">Après validation hello modification (s), les objets en mémoire hello, fichier local de hello, et tous les réplicas de hello ont hello même exacte d’état.</span><span class="sxs-lookup"><span data-stu-id="b51f9-152">After committing hello change(s), hello in-memory objects, hello local file, and all hello replicas have hello same exact state.</span></span> <span data-ttu-id="b51f9-153">Tout est parfait !</span><span class="sxs-lookup"><span data-stu-id="b51f9-153">All is good!</span></span>

<span data-ttu-id="b51f9-154">code Hello ci-dessous montre tooupdate de façon correcte hello une valeur dans une collection fiable :</span><span class="sxs-lookup"><span data-stu-id="b51f9-154">hello code below shows hello correct way tooupdate a value in a reliable collection:</span></span>

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

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a><span data-ttu-id="b51f9-155">Erreur de données immuables types tooprevent programmeur de définir</span><span class="sxs-lookup"><span data-stu-id="b51f9-155">Define immutable data types tooprevent programmer error</span></span>
<span data-ttu-id="b51f9-156">Dans l’idéal, nous aimerions les erreurs tooreport hello du compilateur lorsque vous produisez accidentellement le code qui transforme l’état d’un objet que vous êtes supposé tooconsider immuable.</span><span class="sxs-lookup"><span data-stu-id="b51f9-156">Ideally, we’d like hello compiler tooreport errors when you accidentally produce code that mutates state of an object that you are supposed tooconsider immutable.</span></span> <span data-ttu-id="b51f9-157">Mais, du compilateur c# hello n’a pas hello capacité toodo cela.</span><span class="sxs-lookup"><span data-stu-id="b51f9-157">But, hello C# compiler does not have hello ability toodo this.</span></span> <span data-ttu-id="b51f9-158">C’est le cas, tooavoid potentielle programmeur aux bogues, nous recommandons vivement que vous définissez les types hello que vous utilisez avec des types de collections fiable toobe immuable.</span><span class="sxs-lookup"><span data-stu-id="b51f9-158">So, tooavoid potential programmer bugs, we highly recommend that you define hello types you use with reliable collections toobe immutable types.</span></span> <span data-ttu-id="b51f9-159">Plus précisément, cela signifie que vous respectez toocore des types de valeur (par exemple, des nombres [Int32, UInt64, etc.], DateTime, Guid, TimeSpan et hello comme).</span><span class="sxs-lookup"><span data-stu-id="b51f9-159">Specifically, this means that you stick toocore value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and hello like).</span></span> <span data-ttu-id="b51f9-160">Et, bien sûr, vous pouvez également utiliser des chaînes.</span><span class="sxs-lookup"><span data-stu-id="b51f9-160">And, of course, you can also use String.</span></span> <span data-ttu-id="b51f9-161">Il s’agit des propriétés de collection tooavoid meilleures en tant que la sérialisation et désérialisant permettre fréquemment peut nuire aux performances.</span><span class="sxs-lookup"><span data-stu-id="b51f9-161">It is best tooavoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="b51f9-162">Toutefois, si vous souhaitez que les propriétés de la collection toouse, nous vous recommandons utiliser hello. Bibliothèque de collections immuables de NET ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="b51f9-162">However, if you want toouse collection properties, we highly recommend hello use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="b51f9-163">Cette bibliothèque est disponible au téléchargement sur http://nuget.org. Nous vous recommandons également de sceller vos classes et de définir les champs en lecture seule chaque fois que cela est possible.</span><span class="sxs-lookup"><span data-stu-id="b51f9-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="b51f9-164">Hello type UserInfo ci-dessous montre comment toodefine un immuable type en tirant profit des recommandations susmentionnées.</span><span class="sxs-lookup"><span data-stu-id="b51f9-164">hello UserInfo type below demonstrates how toodefine an immutable type taking advantage of aforementioned recommendations.</span></span>

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

<span data-ttu-id="b51f9-165">Hello ItemId type est également un type immuable comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="b51f9-165">hello ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="b51f9-166">Contrôle de version du schéma (mises à niveau)</span><span class="sxs-lookup"><span data-stu-id="b51f9-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="b51f9-167">En interne, les collections fiables sérialisent vos objets à l’aide du DataContractSerializer de .NET.</span><span class="sxs-lookup"><span data-stu-id="b51f9-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="b51f9-168">les objets sérialisé de Hello sont disque du réplica principal toohello persistantes et également transmise toohello réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="b51f9-168">hello serialized objects are persisted toohello primary replica’s local disk and are also transmitted toohello secondary replicas.</span></span> <span data-ttu-id="b51f9-169">Votre service arrive à maturité, il est probable que vous souhaitiez le genre de hello toochange de données (schéma), que votre service requiert.</span><span class="sxs-lookup"><span data-stu-id="b51f9-169">As your service matures, it’s likely you’ll want toochange hello kind of data (schema) your service requires.</span></span> <span data-ttu-id="b51f9-170">Vous devez aborder la question du contrôle de version de vos données avec une extrême prudence.</span><span class="sxs-lookup"><span data-stu-id="b51f9-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="b51f9-171">Tout d’abord, vous devez toujours être en mesure de toodeserialize anciennes données.</span><span class="sxs-lookup"><span data-stu-id="b51f9-171">First and foremost, you must always be able toodeserialize old data.</span></span> <span data-ttu-id="b51f9-172">Plus précisément, cela signifie que votre code de désérialisation doit être infini descendante : 333 de Version de votre code de service doit être en mesure de toooperate sur les données placées dans une collection fiable par la version 1 de votre code de service, il y a 5 ans.</span><span class="sxs-lookup"><span data-stu-id="b51f9-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able toooperate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="b51f9-173">En outre, le code de service est mis à niveau à raison d’un domaine de mise à niveau à la fois.</span><span class="sxs-lookup"><span data-stu-id="b51f9-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="b51f9-174">Par conséquent, pendant une mise à niveau, deux versions différentes de votre code de service s’exécutent simultanément.</span><span class="sxs-lookup"><span data-stu-id="b51f9-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="b51f9-175">Vous devez éviter hello nouvelle version de votre code de service utilisent hello nouveau schéma comme les anciennes versions de votre code de service peuvent ne pas être en mesure de toohandle schéma hello.</span><span class="sxs-lookup"><span data-stu-id="b51f9-175">You must avoid having hello new version of your service code use hello new schema as old versions of your service code might not be able toohandle hello new schema.</span></span> <span data-ttu-id="b51f9-176">Lorsque cela est possible, vous devez concevoir chaque version de votre ascendante toobe de service par la 1 version.</span><span class="sxs-lookup"><span data-stu-id="b51f9-176">When possible, you should design each version of your service toobe forward compatible by 1 version.</span></span> <span data-ttu-id="b51f9-177">Plus précisément, cela signifie que V1 de votre code de service doit être en mesure de toosimply ignorer tous les éléments de schéma ne gère pas explicitement.</span><span class="sxs-lookup"><span data-stu-id="b51f9-177">Specifically, this means that V1 of your service code should be able toosimply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="b51f9-178">Toutefois, il doit être en mesure de toosave toutes les données qu’elle n’explicitement connaître et il suffit d’écrire de restauration lors de la mise à jour d’une valeur ou une clé de dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="b51f9-178">However, it must be able toosave any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="b51f9-179">Pendant que vous pouvez modifier le schéma hello d’une clé, vous devez vous assurer que le code de hachage de votre clé et algorithmes d’est égal à sont stables.</span><span class="sxs-lookup"><span data-stu-id="b51f9-179">While you can modify hello schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="b51f9-180">Si vous modifiez un de ces algorithmes de fonctionnement, vous pas sera en mesure de toolook clé hello au sein du dictionnaire de fiable hello jamais à nouveau.</span><span class="sxs-lookup"><span data-stu-id="b51f9-180">If you change how either of these algorithms operate, you will not be able toolook up hello key within hello reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="b51f9-181">Vous pouvez également effectuer ce qui est généralement référencés tooas une phase 2 mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="b51f9-181">Alternatively, you can perform what is typically referred tooas a 2-phase upgrade.</span></span> <span data-ttu-id="b51f9-182">Une mise à niveau de la phase 2, vous mettez à niveau votre service V1 tooV2 : V2 contient le code hello qui sait comment toodeal avec un nouveau changement de schéma hello mais ce code ne s’exécute.</span><span class="sxs-lookup"><span data-stu-id="b51f9-182">With a 2-phase upgrade, you upgrade your service from V1 tooV2: V2 contains hello code that knows how toodeal with hello new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="b51f9-183">Lorsque hello V2 code lit les données de V1, il fonctionne sur celui-ci et écrit des données de V1.</span><span class="sxs-lookup"><span data-stu-id="b51f9-183">When hello V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="b51f9-184">Ensuite, une fois la mise à niveau hello est terminée sur tous les domaines de mise à niveau, vous pouvez signaler toohello en cours d’exécution V2 instances que cette mise à niveau hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="b51f9-184">Then, after hello upgrade is complete across all upgrade domains, you can somehow signal toohello running V2 instances that hello upgrade is complete.</span></span> <span data-ttu-id="b51f9-185">(Une façon toosignal tooroll une mise à niveau de la configuration ; c’est ce qui en fait une mise à niveau de la phase 2.) Maintenant, hello V2 instances peuvent lire les données de V1, convertir les données tooV2, exploiter et écrire en tant que données V2.</span><span class="sxs-lookup"><span data-stu-id="b51f9-185">(One way toosignal this is tooroll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, hello V2 instances can read V1 data, convert it tooV2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="b51f9-186">Lorsque d’autres instances de lire les données de V2, ils n’ont pas besoin tooconvert, elles fonctionnent sur ce dernier et simplement écrire les données de V2.</span><span class="sxs-lookup"><span data-stu-id="b51f9-186">When other instances read V2 data, they do not need tooconvert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b51f9-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b51f9-187">Next Steps</span></span>
<span data-ttu-id="b51f9-188">toolearn sur la création de contrats de données compatible vers l’avant, consultez [les contrats de données de compatibilité ascendante](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="b51f9-188">toolearn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="b51f9-189">meilleures pratiques de toolearn sur le contrôle de version des contrats de données, consultez [contrôle de version de contrat de données](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="b51f9-189">toolearn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="b51f9-190">toolearn les contrats de données à tolérance de version tooimplement, voir [des rappels de sérialisation avec tolérance de Version](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="b51f9-190">toolearn how tooimplement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="b51f9-191">toolearn tooprovide une structure de données qui peut interagir entre plusieurs versions, voir [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="b51f9-191">toolearn how tooprovide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
