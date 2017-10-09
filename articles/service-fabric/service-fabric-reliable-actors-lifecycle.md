---
title: "aaaOverview du cycle de vie microservices de Azure basé sur acteur | Documents Microsoft"
description: "Explique le cycle de vie Service Fabric Reliable Actor, le Garbage Collection et la suppression manuelle des acteurs et de leur état"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="905d7-103">Cycle de vie des acteurs, Garbage Collection automatique et suppression manuelle</span><span class="sxs-lookup"><span data-stu-id="905d7-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="905d7-104">Un acteur est activé hello la première fois, un appel est fait tooany de ses méthodes.</span><span class="sxs-lookup"><span data-stu-id="905d7-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="905d7-105">Un acteur est désactivé (garbage collection par le runtime d’acteurs hello) s’il n’est pas utilisé pendant une période configurable.</span><span class="sxs-lookup"><span data-stu-id="905d7-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="905d7-106">Un acteur et son état peuvent également être supprimés manuellement, à tout moment.</span><span class="sxs-lookup"><span data-stu-id="905d7-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="905d7-107">Activation de l’acteur</span><span class="sxs-lookup"><span data-stu-id="905d7-107">Actor activation</span></span>
<span data-ttu-id="905d7-108">Lorsqu’un acteur est activé, hello événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="905d7-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="905d7-109">Quand un appel est émis vers un acteur qui n'est pas actif, un autre acteur est créé.</span><span class="sxs-lookup"><span data-stu-id="905d7-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="905d7-110">état de Hello acteur est chargé si elle maintient l’état.</span><span class="sxs-lookup"><span data-stu-id="905d7-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="905d7-111">Hello `OnActivateAsync` (c#) ou `onActivateAsync` (méthode) (Java) (qui peut être substituée dans une implémentation d’acteur hello) est appelée.</span><span class="sxs-lookup"><span data-stu-id="905d7-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="905d7-112">acteur de Hello est désormais considérée comme active.</span><span class="sxs-lookup"><span data-stu-id="905d7-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="905d7-113">Désactivation de l’acteur</span><span class="sxs-lookup"><span data-stu-id="905d7-113">Actor deactivation</span></span>
<span data-ttu-id="905d7-114">Lorsqu’un acteur est désactivé, hello événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="905d7-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="905d7-115">Lorsqu’un intervenant n’est pas utilisé pendant un certain temps, il est supprimé à partir de la table des acteurs Active hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="905d7-116">Hello `OnDeactivateAsync` (c#) ou `onDeactivateAsync` (méthode) (Java) (qui peut être substituée dans une implémentation d’acteur hello) est appelée.</span><span class="sxs-lookup"><span data-stu-id="905d7-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="905d7-117">Cela efface toutes les minuteries hello pour l’acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="905d7-118">Les opérations de l’acteur, comme la modification de l’état, ne doivent pas être appelées avec cette méthode.</span><span class="sxs-lookup"><span data-stu-id="905d7-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="905d7-119">Hello acteurs de l’ensemble fibre optique exécution émet certaines [tooactor activation et désactivation des événements associés](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="905d7-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="905d7-120">Ces événements sont utiles dans les diagnostics et la surveillance des performances.</span><span class="sxs-lookup"><span data-stu-id="905d7-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="905d7-121">Garbage Collection des acteurs</span><span class="sxs-lookup"><span data-stu-id="905d7-121">Actor garbage collection</span></span>
<span data-ttu-id="905d7-122">Lorsqu’un acteur est désactivé, objet de références toohello acteur sont libérées et il peut être le garbage collecté normalement par hello common language runtime (CLR) ou le garbage collector de java virtual machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="905d7-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="905d7-123">Le garbage collection uniquement nettoie les objets d’acteur hello ; Il effectue **pas** supprimer l’état stocké dans le Gestionnaire d’état d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="905d7-124">Hello prochaine heure hello acteur est activé, un nouvel objet acteur est créé et son état est restauré.</span><span class="sxs-lookup"><span data-stu-id="905d7-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="905d7-125">Quel compte comme « utilisés » à des fins de hello de désactivation et de garbage collection ?</span><span class="sxs-lookup"><span data-stu-id="905d7-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="905d7-126">Réception d'un appel</span><span class="sxs-lookup"><span data-stu-id="905d7-126">Receiving a call</span></span>
* <span data-ttu-id="905d7-127">`IRemindable.ReceiveReminderAsync`méthode appelée (applicable uniquement si l’acteur de hello utilise des rappels)</span><span class="sxs-lookup"><span data-stu-id="905d7-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="905d7-128">Si les acteur hello utilise des minuteurs et son rappel du minuteur est appelé, il ne **pas** en tant que le « utilisé ».</span><span class="sxs-lookup"><span data-stu-id="905d7-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="905d7-129">Avant d’entrer les détails de hello de désactivation, il est hello important toodefine dispositions suivantes :</span><span class="sxs-lookup"><span data-stu-id="905d7-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="905d7-130">*Intervalle d'analyse*.</span><span class="sxs-lookup"><span data-stu-id="905d7-130">*Scan interval*.</span></span> <span data-ttu-id="905d7-131">Il s’agit d’intervalle hello sur l’acteurs hello runtime analyse sa table acteurs Active pour les acteurs qui peuvent être désactivés et que le garbage collector.</span><span class="sxs-lookup"><span data-stu-id="905d7-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="905d7-132">valeur par défaut de Hello est 1 minute.</span><span class="sxs-lookup"><span data-stu-id="905d7-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="905d7-133">*Délai d'inactivité*.</span><span class="sxs-lookup"><span data-stu-id="905d7-133">*Idle timeout*.</span></span> <span data-ttu-id="905d7-134">Cela est hello temps qu’un acteur doit tooremain inutilisées (inactif) avant d’être désactivé et que le garbage collector.</span><span class="sxs-lookup"><span data-stu-id="905d7-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="905d7-135">valeur par défaut de Hello est de 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="905d7-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="905d7-136">En règle générale, il est inutile toochange ces valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="905d7-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="905d7-137">Toutefois, si nécessaire, ces intervalles peuvent être modifiés via `ActorServiceSettings` lorsque vous enregistrez votre [Service d’acteur](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="905d7-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
<span data-ttu-id="905d7-138">Pour chaque acteur active, hello acteur runtime effectue le suivi de durée hello pendant laquelle il a été inactif pendant (c'est-à-dire, non utilisé).</span><span class="sxs-lookup"><span data-stu-id="905d7-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="905d7-139">Hello acteur runtime vérifie chacune des acteurs de hello chaque `ScanIntervalInSeconds` toosee si elle peut être garbage collectées et il collecte, s’il a été inactif pendant `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="905d7-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="905d7-140">Chaque fois qu’un acteur est utilisé, sa durée d’inactivité est too0 de réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="905d7-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="905d7-141">Après cela, acteur de hello peut être le garbage collecté uniquement s’il reste encore inactif pour `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="905d7-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="905d7-142">Rappelez-vous qu’un acteur est considéré comme toohave été utilisée si une méthode d’interface acteur ou d’un rappel de rappel d’acteur est exécuté.</span><span class="sxs-lookup"><span data-stu-id="905d7-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="905d7-143">Un acteur est **pas** considéré comme toohave été si son rappel du minuteur est exécuté.</span><span class="sxs-lookup"><span data-stu-id="905d7-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="905d7-144">Hello diagramme suivant montre hello de cycle de vie d’un tooillustrate unique acteur ces concepts.</span><span class="sxs-lookup"><span data-stu-id="905d7-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![Exemple de temps d'inactivité][1]

<span data-ttu-id="905d7-146">Il montre Hello impact hello des appels de méthode intervenant, les rappels, les minuteurs de durée de vie hello de cet acteur.</span><span class="sxs-lookup"><span data-stu-id="905d7-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="905d7-147">Hello points sur hello exemple suivants est intéressant de mentionner :</span><span class="sxs-lookup"><span data-stu-id="905d7-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="905d7-148">ScanInterval et IdleTimeout sont définies respectivement too5 et 10.</span><span class="sxs-lookup"><span data-stu-id="905d7-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="905d7-149">(Unités de n’importe pas ici, car notre objectif n'est que le concept de hello tooillustrate.)</span><span class="sxs-lookup"><span data-stu-id="905d7-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="905d7-150">analyse de Hello pour les acteurs toobe les garbage collecté se produit au T = 0, 5, 10, 15, 20, 25, tel que défini par l’intervalle d’analyse hello de 5.</span><span class="sxs-lookup"><span data-stu-id="905d7-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="905d7-151">Une minuterie périodique se déclenche à T=4,8,12,16,20,24 et son rappel s'exécute.</span><span class="sxs-lookup"><span data-stu-id="905d7-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="905d7-152">Il n’affecte pas la durée d’inactivité hello d’acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="905d7-153">Un appel de méthode intervenant au niveau de T = 7 réinitialise too0 du temps d’inactivité hello et retarde hello le garbage collection d’acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="905d7-154">Un rappel de rappel acteur s’exécute à T = 14 et plus les retards hello le garbage collection d’acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="905d7-155">Au cours de hello analyse de garbage collection à T = 25, durée d’inactivité d’acteur hello dépasse enfin délai d’inactivité de hello de 10 et acteur de hello est le garbage collecté.</span><span class="sxs-lookup"><span data-stu-id="905d7-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="905d7-156">Un acteur ne peut jamais faire l’objet d’un Garbage Collection quand il exécute l’une de ses méthodes, quelle que soit la durée d’exécution de cette méthode.</span><span class="sxs-lookup"><span data-stu-id="905d7-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="905d7-157">Comme mentionné précédemment, l’exécution de hello de méthodes d’interface acteur et les rappels de rappel empêche le garbage collection en réinitialisant too0 de durée d’inactivité d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="905d7-158">l’exécution de Hello de rappels de la minuterie ne réinitialise pas too0 du temps d’inactivité hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="905d7-159">Toutefois, hello le garbage collection d’acteur de hello est différé jusqu'à ce que la fin de l’exécution du rappel timer hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="905d7-160">Suppression des acteurs et de leur état</span><span class="sxs-lookup"><span data-stu-id="905d7-160">Deleting actors and their state</span></span>
<span data-ttu-id="905d7-161">Le garbage collection d’acteurs désactivés nettoie uniquement objet d’acteur hello, mais elle ne supprime pas les données stockées dans le Gestionnaire d’état d’un acteur.</span><span class="sxs-lookup"><span data-stu-id="905d7-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="905d7-162">Lorsqu’un acteur est réactivé, ses données sont effectuées tooit disponible via le Gestionnaire d’état de hello.</span><span class="sxs-lookup"><span data-stu-id="905d7-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="905d7-163">Dans les cas où acteurs stocker des données dans le Gestionnaire d’état et sont désactivées, mais jamais nouveau activés, il peut être nécessaire tooclean leurs données.</span><span class="sxs-lookup"><span data-stu-id="905d7-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="905d7-164">Hello [acteur Service](service-fabric-reliable-actors-platform.md) fournit une fonction de suppression des intervenants à partir d’un appelant distant :</span><span class="sxs-lookup"><span data-stu-id="905d7-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="905d7-165">La suppression d’un acteur a hello suivant effets selon l’acteur de hello soit actif ou non :</span><span class="sxs-lookup"><span data-stu-id="905d7-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="905d7-166">**Acteur actif**</span><span class="sxs-lookup"><span data-stu-id="905d7-166">**Active Actor**</span></span>
  * <span data-ttu-id="905d7-167">L’acteur est supprimé de la liste des acteurs actifs et est désactivé.</span><span class="sxs-lookup"><span data-stu-id="905d7-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="905d7-168">Son état est définitivement supprimé.</span><span class="sxs-lookup"><span data-stu-id="905d7-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="905d7-169">**Acteur inactif**</span><span class="sxs-lookup"><span data-stu-id="905d7-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="905d7-170">Son état est définitivement supprimé.</span><span class="sxs-lookup"><span data-stu-id="905d7-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="905d7-171">Notez qu’un acteur ne peut pas appeler delete sur lui-même à partir d’une de ses méthodes intervenant comme acteur de hello ne peut pas être supprimé pendant l’exécution d’un contexte d’appel acteur, dans quel hello runtime a obtenu un verrou autour hello acteur tooenforce monothread accès par appel de.</span><span class="sxs-lookup"><span data-stu-id="905d7-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="905d7-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="905d7-172">Next steps</span></span>
* [<span data-ttu-id="905d7-173">Minuteries et rappels d’acteur</span><span class="sxs-lookup"><span data-stu-id="905d7-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="905d7-174">Événements d’acteurs</span><span class="sxs-lookup"><span data-stu-id="905d7-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="905d7-175">Réentrance des acteurs</span><span class="sxs-lookup"><span data-stu-id="905d7-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="905d7-176">Diagnostics et surveillance des performances d’acteur</span><span class="sxs-lookup"><span data-stu-id="905d7-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="905d7-177">Documentation de référence de l’API d’acteur</span><span class="sxs-lookup"><span data-stu-id="905d7-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="905d7-178">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="905d7-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="905d7-179">Exemple de code Java</span><span class="sxs-lookup"><span data-stu-id="905d7-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
