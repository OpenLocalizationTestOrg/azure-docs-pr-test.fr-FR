---
title: "Vue d’ensemble du cycle de vie des microservices Azure basés sur acteur | Microsoft Docs"
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
ms.openlocfilehash: 75b7b77a0bef2051599a4f61183109cfb2ffff3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="ae29c-103">Cycle de vie des acteurs, Garbage Collection automatique et suppression manuelle</span><span class="sxs-lookup"><span data-stu-id="ae29c-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="ae29c-104">Un acteur est activé la première fois qu’un appel est effectué à l’une de ses méthodes.</span><span class="sxs-lookup"><span data-stu-id="ae29c-104">An actor is activated the first time a call is made to any of its methods.</span></span> <span data-ttu-id="ae29c-105">Un acteur est désactivé (fait l’objet d’un Garbage Collection par le runtime Actors) s’il n’est pas utilisé pendant une durée configurable.</span><span class="sxs-lookup"><span data-stu-id="ae29c-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="ae29c-106">Un acteur et son état peuvent également être supprimés manuellement, à tout moment.</span><span class="sxs-lookup"><span data-stu-id="ae29c-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="ae29c-107">Activation de l’acteur</span><span class="sxs-lookup"><span data-stu-id="ae29c-107">Actor activation</span></span>
<span data-ttu-id="ae29c-108">Quand un acteur est activé, les événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="ae29c-108">When an actor is activated, the following occurs:</span></span>

* <span data-ttu-id="ae29c-109">Quand un appel est émis vers un acteur qui n'est pas actif, un autre acteur est créé.</span><span class="sxs-lookup"><span data-stu-id="ae29c-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="ae29c-110">L’état de l’acteur est chargé s’il maintient l’état.</span><span class="sxs-lookup"><span data-stu-id="ae29c-110">The actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="ae29c-111">La méthode `OnActivateAsync` (C#) ou `onActivateAsync` (Java), qui peut être remplacée dans l’implémentation de l’acteur, est appelée.</span><span class="sxs-lookup"><span data-stu-id="ae29c-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span>
* <span data-ttu-id="ae29c-112">L’acteur est désormais considéré comme actif.</span><span class="sxs-lookup"><span data-stu-id="ae29c-112">The actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="ae29c-113">Désactivation de l’acteur</span><span class="sxs-lookup"><span data-stu-id="ae29c-113">Actor deactivation</span></span>
<span data-ttu-id="ae29c-114">Quand un acteur est désactivé, les événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="ae29c-114">When an actor is deactivated, the following occurs:</span></span>

* <span data-ttu-id="ae29c-115">Quand un acteur n'est pas utilisé pendant un certain temps, il est supprimé de la table d'acteurs actifs.</span><span class="sxs-lookup"><span data-stu-id="ae29c-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span></span>
* <span data-ttu-id="ae29c-116">La méthode `OnDeactivateAsync` (C#) ou `onDeactivateAsync` (Java), qui peut être remplacée dans l’implémentation de l’acteur, est appelée.</span><span class="sxs-lookup"><span data-stu-id="ae29c-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span> <span data-ttu-id="ae29c-117">Cette opération efface toutes les minuteries applicables à l'acteur.</span><span class="sxs-lookup"><span data-stu-id="ae29c-117">This clears all the timers for the actor.</span></span> <span data-ttu-id="ae29c-118">Les opérations de l’acteur, comme la modification de l’état, ne doivent pas être appelées avec cette méthode.</span><span class="sxs-lookup"><span data-stu-id="ae29c-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="ae29c-119">Le runtime Fabric Actors émet des [événements liés à l’activation et la désactivation des acteurs](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="ae29c-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="ae29c-120">Ces derniers sont utiles dans les diagnostics et la surveillance des performances.</span><span class="sxs-lookup"><span data-stu-id="ae29c-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="ae29c-121">Garbage Collection des acteurs</span><span class="sxs-lookup"><span data-stu-id="ae29c-121">Actor garbage collection</span></span>
<span data-ttu-id="ae29c-122">Quand un acteur est désactivé, les références à l’objet acteur sont libérées et celui-ci peut faire l’objet d’un garbage collection normal par le récupérateur de mémoire CLR (common language runtime) ou de la machine virtuelle Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="ae29c-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="ae29c-123">L’opération Garbage Collection nettoie uniquement l’objet acteur. Elle ne supprime **pas** l’état stocké dans le Gestionnaire d’état de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="ae29c-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span></span> <span data-ttu-id="ae29c-124">La prochaine fois que l’acteur est activé, un nouvel objet acteur est créé et son état est restauré.</span><span class="sxs-lookup"><span data-stu-id="ae29c-124">The next time the actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="ae29c-125">Que signifie « être utilisé » dans le cadre de la désactivation et du Garbage Collection ?</span><span class="sxs-lookup"><span data-stu-id="ae29c-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="ae29c-126">Réception d'un appel</span><span class="sxs-lookup"><span data-stu-id="ae29c-126">Receiving a call</span></span>
* <span data-ttu-id="ae29c-127">`IRemindable.ReceiveReminderAsync` (applicable uniquement si l'acteur utilise des rappels)</span><span class="sxs-lookup"><span data-stu-id="ae29c-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="ae29c-128">Si l’acteur utilise des minuteries et que son rappel de minuterie est appelé, cela ne signifie **pas** qu’il est « utilisé ».</span><span class="sxs-lookup"><span data-stu-id="ae29c-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="ae29c-129">Avant d’aborder les détails de la désactivation, il est important de définir les termes suivants :</span><span class="sxs-lookup"><span data-stu-id="ae29c-129">Before we go into the details of deactivation, it is important to define the following terms:</span></span>

* <span data-ttu-id="ae29c-130">*Intervalle d'analyse*.</span><span class="sxs-lookup"><span data-stu-id="ae29c-130">*Scan interval*.</span></span> <span data-ttu-id="ae29c-131">Il s’agit de l’intervalle pendant lequel le runtime Actors recherche dans sa table d’acteurs actifs les acteurs qui peuvent faire l’objet d’une désactivation ou d’un Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="ae29c-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="ae29c-132">La valeur par défaut est 1 minute.</span><span class="sxs-lookup"><span data-stu-id="ae29c-132">The default value for this is 1 minute.</span></span>
* <span data-ttu-id="ae29c-133">*Délai d'inactivité*.</span><span class="sxs-lookup"><span data-stu-id="ae29c-133">*Idle timeout*.</span></span> <span data-ttu-id="ae29c-134">Il s’agit de la durée pendant laquelle un acteur reste inutilisé (inactif) avant de faire l’objet d’une désactivation ou d’un Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="ae29c-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="ae29c-135">La valeur par défaut est 60 minutes.</span><span class="sxs-lookup"><span data-stu-id="ae29c-135">The default value for this is 60 minutes.</span></span>

<span data-ttu-id="ae29c-136">En général, vous n'avez pas besoin de modifier les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="ae29c-136">Typically, you do not need to change these defaults.</span></span> <span data-ttu-id="ae29c-137">Toutefois, si nécessaire, ces intervalles peuvent être modifiés via `ActorServiceSettings` lorsque vous enregistrez votre [Service d’acteur](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="ae29c-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

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
<span data-ttu-id="ae29c-138">Pour chaque acteur actif, le runtime Actors effectue le suivi de la durée pendant laquelle il a été inactif (c’est-à-dire non utilisé).</span><span class="sxs-lookup"><span data-stu-id="ae29c-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="ae29c-139">Le runtime Actors vérifie chacun des acteurs toutes les `ScanIntervalInSeconds` pour voir s’il peut faire l’objet d’un Garbage Collection, et le collecte s’il est inactif depuis `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="ae29c-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="ae29c-140">Chaque fois qu'un acteur est utilisé, son délai d'inactivité est réinitialisé à 0.</span><span class="sxs-lookup"><span data-stu-id="ae29c-140">Anytime an actor is used, its idle time is reset to 0.</span></span> <span data-ttu-id="ae29c-141">Ensuite, l'acteur peut uniquement faire l'objet d'un Garbage Collection s'il reste encore inactif pendant `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="ae29c-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="ae29c-142">N’oubliez pas qu’un acteur est considéré utilisé si une méthode d’interface d’acteur ou un rappel de rappel d’acteur est exécuté.</span><span class="sxs-lookup"><span data-stu-id="ae29c-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="ae29c-143">Un acteur n'est **pas** considéré utilisé si son rappel de minuterie est exécuté.</span><span class="sxs-lookup"><span data-stu-id="ae29c-143">An actor is **not** considered to have been used if its timer callback is executed.</span></span>

<span data-ttu-id="ae29c-144">Le diagramme suivant illustre le cycle de vie d’un seul acteur pour illustrer ces concepts.</span><span class="sxs-lookup"><span data-stu-id="ae29c-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span></span>

![Exemple de temps d'inactivité][1]

<span data-ttu-id="ae29c-146">L'exemple montre l'impact des appels de méthode d'acteur, les rappels et les minuteries sur la durée de vie de cet acteur.</span><span class="sxs-lookup"><span data-stu-id="ae29c-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span></span> <span data-ttu-id="ae29c-147">Voici les points importants de l'exemple :</span><span class="sxs-lookup"><span data-stu-id="ae29c-147">The following points about the example are worth mentioning:</span></span>

* <span data-ttu-id="ae29c-148">ScanInterval et IdleTimeout sont définis sur 5 et 10, respectivement.</span><span class="sxs-lookup"><span data-stu-id="ae29c-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span></span> <span data-ttu-id="ae29c-149">(Les unités n'importent pas ici, dans la mesure où notre objectif se borne à illustrer le concept.)</span><span class="sxs-lookup"><span data-stu-id="ae29c-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span></span>
* <span data-ttu-id="ae29c-150">La recherche d'acteurs ayant fait l'objet d'un Garbage Collection s'effectue à T=0,5,10,15,20,25, comme défini par la valeur 5 de l'intervalle d'analyse.</span><span class="sxs-lookup"><span data-stu-id="ae29c-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span></span>
* <span data-ttu-id="ae29c-151">Une minuterie périodique se déclenche à T=4,8,12,16,20,24 et son rappel s'exécute.</span><span class="sxs-lookup"><span data-stu-id="ae29c-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="ae29c-152">Il n'affecte pas la durée d'inactivité de l'acteur.</span><span class="sxs-lookup"><span data-stu-id="ae29c-152">It does not impact the idle time of the actor.</span></span>
* <span data-ttu-id="ae29c-153">Un appel de méthode d'acteur à T=7 réinitialise la durée d'inactivité à 0 et retarde le Garbage Collection de l'acteur.</span><span class="sxs-lookup"><span data-stu-id="ae29c-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="ae29c-154">Un rappel de rappel d'acteur s'exécute à T=14 et retarde davantage le Garbage Collection de l'acteur.</span><span class="sxs-lookup"><span data-stu-id="ae29c-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="ae29c-155">Lors de l'analyse de Garbage Collection à T=25, la durée d'inactivité de l'acteur dépasse la valeur 10 du paramètre Délai d'inactivité et l'acteur fait l'objet d'un Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="ae29c-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span></span>

<span data-ttu-id="ae29c-156">Un acteur ne peut jamais faire l’objet d’un Garbage Collection quand il exécute l’une de ses méthodes, quelle que soit la durée d’exécution de cette méthode.</span><span class="sxs-lookup"><span data-stu-id="ae29c-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="ae29c-157">Comme mentionné précédemment, l'exécution des méthodes d'interface d'acteur et des rappels de rappel empêche le Garbage Collection en réinitialisant la durée d'inactivité de l'acteur à 0.</span><span class="sxs-lookup"><span data-stu-id="ae29c-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span></span> <span data-ttu-id="ae29c-158">L'exécution des rappels de minuterie ne réinitialise pas la durée d'inactivité à 0.</span><span class="sxs-lookup"><span data-stu-id="ae29c-158">The execution of timer callbacks does not reset the idle time to 0.</span></span> <span data-ttu-id="ae29c-159">Toutefois, le Garbage Collection de l'acteur est différé jusqu'à ce que le rappel de minuterie ait terminé son exécution.</span><span class="sxs-lookup"><span data-stu-id="ae29c-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="ae29c-160">Suppression des acteurs et de leur état</span><span class="sxs-lookup"><span data-stu-id="ae29c-160">Deleting actors and their state</span></span>
<span data-ttu-id="ae29c-161">Le Garbage Collection des acteurs désactivés nettoie uniquement l’objet acteur, mais il ne supprime pas les données stockées dans le Gestionnaire d’état d’un acteur.</span><span class="sxs-lookup"><span data-stu-id="ae29c-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="ae29c-162">Lorsqu’un acteur est réactivé, ses données sont de nouveau rendues disponibles par le biais du Gestionnaire d’état.</span><span class="sxs-lookup"><span data-stu-id="ae29c-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span></span> <span data-ttu-id="ae29c-163">Dans les cas où les acteurs stockent des données dans le Gestionnaire d’état et sont désactivés mais jamais réactivés, il peut être nécessaire de nettoyer leurs données.</span><span class="sxs-lookup"><span data-stu-id="ae29c-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span></span>

<span data-ttu-id="ae29c-164">Le [Service d’acteur](service-fabric-reliable-actors-platform.md) fournit une fonction de suppression des acteurs à partir d’un appelant à distance :</span><span class="sxs-lookup"><span data-stu-id="ae29c-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

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

<span data-ttu-id="ae29c-165">La suppression d’un acteur a les effets suivants selon que l’acteur est actuellement actif ou pas :</span><span class="sxs-lookup"><span data-stu-id="ae29c-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span></span>

* <span data-ttu-id="ae29c-166">**Acteur actif**</span><span class="sxs-lookup"><span data-stu-id="ae29c-166">**Active Actor**</span></span>
  * <span data-ttu-id="ae29c-167">L’acteur est supprimé de la liste des acteurs actifs et est désactivé.</span><span class="sxs-lookup"><span data-stu-id="ae29c-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="ae29c-168">Son état est définitivement supprimé.</span><span class="sxs-lookup"><span data-stu-id="ae29c-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="ae29c-169">**Acteur inactif**</span><span class="sxs-lookup"><span data-stu-id="ae29c-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="ae29c-170">Son état est définitivement supprimé.</span><span class="sxs-lookup"><span data-stu-id="ae29c-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="ae29c-171">Notez qu’un acteur ne peut pas effectuer un appel de suppression sur lui-même à partir de l’une de ses méthodes d’acteur, car l’acteur ne peut pas être supprimé pendant qu’il est exécuté dans un contexte d’appel d’acteur, dans lequel le runtime a obtenu un verrou autour de l’appel d’acteur pour autoriser l’accès monothread.</span><span class="sxs-lookup"><span data-stu-id="ae29c-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae29c-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae29c-172">Next steps</span></span>
* [<span data-ttu-id="ae29c-173">Minuteries et rappels d’acteur</span><span class="sxs-lookup"><span data-stu-id="ae29c-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="ae29c-174">Événements d’acteurs</span><span class="sxs-lookup"><span data-stu-id="ae29c-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="ae29c-175">Réentrance des acteurs</span><span class="sxs-lookup"><span data-stu-id="ae29c-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="ae29c-176">Diagnostics et surveillance des performances d’acteur</span><span class="sxs-lookup"><span data-stu-id="ae29c-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="ae29c-177">Documentation de référence de l’API d’acteur</span><span class="sxs-lookup"><span data-stu-id="ae29c-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="ae29c-178">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="ae29c-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="ae29c-179">Exemple de code Java</span><span class="sxs-lookup"><span data-stu-id="ae29c-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
