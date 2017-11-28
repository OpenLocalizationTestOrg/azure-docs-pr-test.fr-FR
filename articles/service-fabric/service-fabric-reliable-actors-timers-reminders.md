---
title: Minuteries et rappels pour Reliable Actors | Microsoft Docs
description: "Présentation des minuteries et rappels pour Service Fabric Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 06b026ce06e0f16a77ac238de0af2263f272933c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="b116e-103">Minuteries et rappels d’acteur</span><span class="sxs-lookup"><span data-stu-id="b116e-103">Actor timers and reminders</span></span>
<span data-ttu-id="b116e-104">Les acteurs peuvent planifier un travail régulier par eux-mêmes en inscrivant des minuteries ou des rappels.</span><span class="sxs-lookup"><span data-stu-id="b116e-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="b116e-105">Cet article montre comment utiliser des minuteries et des rappels, puis explique les différences entre les deux.</span><span class="sxs-lookup"><span data-stu-id="b116e-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="b116e-106">Minuteries des acteurs</span><span class="sxs-lookup"><span data-stu-id="b116e-106">Actor timers</span></span>
<span data-ttu-id="b116e-107">Les minuteries des acteurs fournissent un wrapper simple autour de minuteries .NET ou Java pour veiller à ce que les méthodes de rappel respectent les garanties d’un accès concurrentiel en alternance fournies par le runtime Actors.</span><span class="sxs-lookup"><span data-stu-id="b116e-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="b116e-108">Les acteurs peuvent utiliser les méthodes `RegisterTimer` (C#) ou `registerTimer` (Java) et `UnregisterTimer` (C#) ou `unregisterTimer` (Java) sur leur classe de base pour inscrire et désinscrire leurs minuteries.</span><span class="sxs-lookup"><span data-stu-id="b116e-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="b116e-109">L'exemple ci-dessous montre l'utilisation des API de minuterie.</span><span class="sxs-lookup"><span data-stu-id="b116e-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="b116e-110">Les API sont très similaires à la minuterie .NET ou Java.</span><span class="sxs-lookup"><span data-stu-id="b116e-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="b116e-111">Dans cet exemple, quand la minuterie arrive à son terme, le runtime Actors appelle la méthode `MoveObject` (C#) ou `moveObject` (Java).</span><span class="sxs-lookup"><span data-stu-id="b116e-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="b116e-112">Le respect par la méthode de l’accès concurrentiel en alternance est garanti.</span><span class="sxs-lookup"><span data-stu-id="b116e-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="b116e-113">Aucune autre méthode d’acteur ou aucun autre rappel de minuterie n’est donc en cours d’exécution avant la fin de ce rappel.</span><span class="sxs-lookup"><span data-stu-id="b116e-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="b116e-114">La période suivante de la minuterie démarre après la fin du rappel.</span><span class="sxs-lookup"><span data-stu-id="b116e-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="b116e-115">Cela implique que la minuterie s’arrête pendant l’exécution du rappel, puis démarre quand le rappel se termine.</span><span class="sxs-lookup"><span data-stu-id="b116e-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="b116e-116">Le runtime Actors enregistre les modifications apportées au Gestionnaire d’état de l’acteur à la fin du rappel.</span><span class="sxs-lookup"><span data-stu-id="b116e-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="b116e-117">Si une erreur se produit lors de l'enregistrement de l'état, cet objet acteur sera désactivé et une nouvelle instance sera activée.</span><span class="sxs-lookup"><span data-stu-id="b116e-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="b116e-118">Toutes les minuteries sont arrêtées quand l’acteur est désactivé dans le cadre du nettoyage de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="b116e-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="b116e-119">Aucun rappel de minuterie n’est appelé après cela.</span><span class="sxs-lookup"><span data-stu-id="b116e-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="b116e-120">En outre, le runtime Actors ne conserve aucune information concernant les minuteries qui étaient exécutées avant la désactivation.</span><span class="sxs-lookup"><span data-stu-id="b116e-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="b116e-121">C'est à l'acteur d'inscrire toutes les minuteries dont il a besoin lors d'une réactivation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b116e-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="b116e-122">Pour plus d’informations, consultez la section sur le [nettoyage de la mémoire d’acteur](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="b116e-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="b116e-123">Rappels d’acteur</span><span class="sxs-lookup"><span data-stu-id="b116e-123">Actor reminders</span></span>
<span data-ttu-id="b116e-124">Les rappels sont un mécanisme permettant de déclencher des rappels persistants sur un acteur à certaines heures.</span><span class="sxs-lookup"><span data-stu-id="b116e-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="b116e-125">Leur fonctionnalité est semblable à celle des minuteries.</span><span class="sxs-lookup"><span data-stu-id="b116e-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="b116e-126">Toutefois, contrairement aux minuteries, les rappels sont déclenchés en toutes circonstances jusqu’à ce que l’acteur les désinscrive ou qu’il soit supprimé explicitement.</span><span class="sxs-lookup"><span data-stu-id="b116e-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="b116e-127">Plus précisément, les rappels sont déclenchés lors des désactivations d'acteur et des basculements car le runtime Actors conserve des informations sur les rappels de l'acteur.</span><span class="sxs-lookup"><span data-stu-id="b116e-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="b116e-128">Pour inscrire un rappel, un acteur appelle la méthode `RegisterReminderAsync` fournie dans la classe de base, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b116e-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="b116e-129">Dans cet exemple, `"Pay cell phone bill"` est le nom du rappel.</span><span class="sxs-lookup"><span data-stu-id="b116e-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="b116e-130">Il s’agit d’une chaîne que l’acteur utilise pour identifier de façon unique un rappel.</span><span class="sxs-lookup"><span data-stu-id="b116e-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="b116e-131">`BitConverter.GetBytes(amountInDollars)` (C#) est le contexte associé au rappel.</span><span class="sxs-lookup"><span data-stu-id="b116e-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="b116e-132">Il est renvoyé à l’acteur en tant qu’argument vers le rappel, soit `IRemindable.ReceiveReminderAsync` (C#) ou `Remindable.receiveReminderAsync` (Java).</span><span class="sxs-lookup"><span data-stu-id="b116e-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="b116e-133">Les acteurs qui utilisent des rappels doivent implémenter l’interface `IRemindable` , comme illustré dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b116e-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="b116e-134">Quand un rappel est déclenché, le runtime Reliable Actors appelle la méthode `ReceiveReminderAsync` (C#) ou `receiveReminderAsync` (Java) sur l’acteur.</span><span class="sxs-lookup"><span data-stu-id="b116e-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="b116e-135">Un acteur peut inscrire plusieurs rappels, et la méthode `ReceiveReminderAsync` (C#) ou `receiveReminderAsync` (Java) est appelée chaque fois qu’un de ces rappels est déclenché.</span><span class="sxs-lookup"><span data-stu-id="b116e-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="b116e-136">L’acteur peut ensuite utiliser le nom du rappel qui est envoyé à la méthode `ReceiveReminderAsync` (C#) ou `receiveReminderAsync` (Java) pour identifier le rappel qui a été déclenché.</span><span class="sxs-lookup"><span data-stu-id="b116e-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="b116e-137">Le runtime Actors enregistre l’état de l’acteur à la fin de l’appel `ReceiveReminderAsync` (C#) ou `receiveReminderAsync` (Java).</span><span class="sxs-lookup"><span data-stu-id="b116e-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="b116e-138">Si une erreur se produit lors de l'enregistrement de l'état, cet objet acteur sera désactivé et une nouvelle instance sera activée.</span><span class="sxs-lookup"><span data-stu-id="b116e-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="b116e-139">Pour désinscrire un rappel, un acteur appelle la méthode `UnregisterReminderAsync` (C#) ou `unregisterReminderAsync` (Java), comme l’illustre l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b116e-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="b116e-140">Comme indiqué ci-dessus, la méthode `UnregisterReminderAsync`(C#) ou `unregisterReminderAsync`(Java) accepte une interface `IActorReminder` (C#) ou `ActorReminder` (Java).</span><span class="sxs-lookup"><span data-stu-id="b116e-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="b116e-141">La classe de base de l’acteur prend en charge une méthode `GetReminder` (C#) ou `getReminder` (Java) qui peut être utilisée pour récupérer l’interface `IActorReminder` (C#) ou `ActorReminder` (Java) en passant le nom du rappel.</span><span class="sxs-lookup"><span data-stu-id="b116e-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="b116e-142">C’est pratique, car l’acteur n’a pas besoin de conserver l’interface `IActorReminder` (C#) ou `ActorReminder` (Java) renvoyée par l’appel de la méthode `RegisterReminder` (C#) ou `registerReminder` (Java).</span><span class="sxs-lookup"><span data-stu-id="b116e-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b116e-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b116e-143">Next Steps</span></span>
<span data-ttu-id="b116e-144">En savoir plus sur les événements acteurs fiables et la réentrance :</span><span class="sxs-lookup"><span data-stu-id="b116e-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="b116e-145">Événements d’acteurs</span><span class="sxs-lookup"><span data-stu-id="b116e-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="b116e-146">Réentrance des acteurs</span><span class="sxs-lookup"><span data-stu-id="b116e-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
