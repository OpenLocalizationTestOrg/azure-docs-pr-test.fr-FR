---
title: aaaReliable acteurs minuteries et rappels | Documents Microsoft
description: "Introduction tootimers et des rappels auprès de l’infrastructure de Service Reliable Actors."
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
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="8ded6-103">Minuteries et rappels d’acteur</span><span class="sxs-lookup"><span data-stu-id="8ded6-103">Actor timers and reminders</span></span>
<span data-ttu-id="8ded6-104">Les acteurs peuvent planifier un travail régulier par eux-mêmes en inscrivant des minuteries ou des rappels.</span><span class="sxs-lookup"><span data-stu-id="8ded6-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="8ded6-105">Cet article explique comment toouse minuteries et rappels et explique les différences de hello entre eux.</span><span class="sxs-lookup"><span data-stu-id="8ded6-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="8ded6-106">Minuteries des acteurs</span><span class="sxs-lookup"><span data-stu-id="8ded6-106">Actor timers</span></span>
<span data-ttu-id="8ded6-107">Les minuteurs acteur fournissent un wrapper simple autour d’un tooensure du minuteur .NET ou Java que les méthodes de rappel hello respectent les garanties de concurrence activer hello hello acteurs runtime fournit.</span><span class="sxs-lookup"><span data-stu-id="8ded6-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="8ded6-108">Intervenants peuvent utiliser hello `RegisterTimer`(c#) ou `registerTimer`(Java) et `UnregisterTimer`(c#) ou `unregisterTimer`méthodes (Java) sur la base de leur classe tooregister et annuler l’inscription de leurs minuteurs.</span><span class="sxs-lookup"><span data-stu-id="8ded6-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="8ded6-109">exemple Hello ci-dessous montre l’utilisation hello du minuteur d’API.</span><span class="sxs-lookup"><span data-stu-id="8ded6-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="8ded6-110">Hello API sont très similaires toohello .NET timer ou un minuteur de Java.</span><span class="sxs-lookup"><span data-stu-id="8ded6-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="8ded6-111">Dans cet exemple, lorsque le minuteur de hello arrive, hello acteurs runtime appellera hello `MoveObject`(c#) ou `moveObject`(méthode) (Java).</span><span class="sxs-lookup"><span data-stu-id="8ded6-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="8ded6-112">méthode Hello est garantie concurrence toorespect hello activer.</span><span class="sxs-lookup"><span data-stu-id="8ded6-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="8ded6-113">Aucune autre méthode d’acteur ou aucun autre rappel de minuterie n’est donc en cours d’exécution avant la fin de ce rappel.</span><span class="sxs-lookup"><span data-stu-id="8ded6-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

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
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

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
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
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

<span data-ttu-id="8ded6-114">Hello prochaine période de minuterie de hello démarre après que le rappel de hello termine l’exécution.</span><span class="sxs-lookup"><span data-stu-id="8ded6-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="8ded6-115">Cela implique ce minuteur hello est arrêté alors que le rappel de hello s’exécute et qu’il est démarré lorsque le rappel de hello se termine.</span><span class="sxs-lookup"><span data-stu-id="8ded6-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="8ded6-116">Hello acteurs runtime enregistre les modifications apportées Gestionnaire d’état d’acteur toohello issue de rappel de hello.</span><span class="sxs-lookup"><span data-stu-id="8ded6-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="8ded6-117">Si une erreur se produit dans l’enregistrement de l’état de hello, cet objet acteur sera désactivé et une nouvelle instance est activée.</span><span class="sxs-lookup"><span data-stu-id="8ded6-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="8ded6-118">Toutes les minuteries sont arrêtés lors de l’acteur de hello est désactivé dans le cadre du garbage collection.</span><span class="sxs-lookup"><span data-stu-id="8ded6-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="8ded6-119">Aucun rappel de minuterie n’est appelé après cela.</span><span class="sxs-lookup"><span data-stu-id="8ded6-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="8ded6-120">En outre, hello acteurs runtime ne conserve pas toutes les informations à propos des minuteries hello en cours d’exécution avant la désactivation.</span><span class="sxs-lookup"><span data-stu-id="8ded6-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="8ded6-121">C’est toohello acteur tooregister tous les minuteurs dont il a besoin lorsqu’il est réactivé Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="8ded6-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="8ded6-122">Pour plus d’informations, consultez la section de hello sur [nettoyage acteur](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="8ded6-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="8ded6-123">Rappels d’acteur</span><span class="sxs-lookup"><span data-stu-id="8ded6-123">Actor reminders</span></span>
<span data-ttu-id="8ded6-124">Les rappels sont un mécanisme tootrigger rappels persistants sur un acteur à certaines heures.</span><span class="sxs-lookup"><span data-stu-id="8ded6-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="8ded6-125">Leur fonctionnalité est tootimers similaire.</span><span class="sxs-lookup"><span data-stu-id="8ded6-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="8ded6-126">Mais contrairement aux minuteries, les rappels sont déclenchées en toutes circonstances jusqu'à ce que les acteur hello leur enregistrement explicitement ou acteur de hello est supprimé explicitement.</span><span class="sxs-lookup"><span data-stu-id="8ded6-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="8ded6-127">Plus précisément, des rappels sont déclenchées sur les basculements et les désactivations acteur car hello acteurs runtime conserve les informations sur les rappels d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="8ded6-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="8ded6-128">tooregister un rappel, un acteur appelle hello `RegisterReminderAsync` méthode fournie sur la classe de base hello, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8ded6-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

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
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="8ded6-129">Dans cet exemple, `"Pay cell phone bill"` est le nom de rappel hello.</span><span class="sxs-lookup"><span data-stu-id="8ded6-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="8ded6-130">Il s’agit d’une chaîne qui hello acteur utilise toouniquely identifier un rappel.</span><span class="sxs-lookup"><span data-stu-id="8ded6-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="8ded6-131">`BitConverter.GetBytes(amountInDollars)`(C#) est le contexte hello associé au rappel de hello.</span><span class="sxs-lookup"><span data-stu-id="8ded6-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="8ded6-132">Il sera passé toohello arrière acteur comme un rappel de rappel toohello argument, c'est-à-dire `IRemindable.ReceiveReminderAsync`(c#) ou `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="8ded6-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="8ded6-133">Les acteurs qui utilisent des rappels doivent implémenter hello `IRemindable` d’interface, comme indiqué dans l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8ded6-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

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

<span data-ttu-id="8ded6-134">Lorsqu’un rappel est déclenché, hello Reliable Actors runtime appelle hello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(méthode) (Java) sur hello acteur.</span><span class="sxs-lookup"><span data-stu-id="8ded6-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="8ded6-135">Un acteur peut enregistrer des rappels multiples et hello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(méthode) (Java) est appelé lorsque un de ces rappels est déclenché.</span><span class="sxs-lookup"><span data-stu-id="8ded6-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="8ded6-136">acteur de Hello peut utiliser le nom de rappel de hello qui est passé dans toohello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`toofigure de méthode (Java) à quels rappel a été déclenchée.</span><span class="sxs-lookup"><span data-stu-id="8ded6-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="8ded6-137">état d’acteur hello lorsque hello enregistre Hello acteurs runtime `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(Java) l’appel.</span><span class="sxs-lookup"><span data-stu-id="8ded6-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="8ded6-138">Si une erreur se produit dans l’enregistrement de l’état de hello, cet objet acteur sera désactivé et une nouvelle instance est activée.</span><span class="sxs-lookup"><span data-stu-id="8ded6-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="8ded6-139">toounregister un rappel, un acteur appelle hello `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`(méthode) (Java), comme indiqué dans les exemples hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8ded6-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="8ded6-140">Comme indiqué ci-dessus, hello `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`(Java) méthode accepte un `IActorReminder`(c#) ou `ActorReminder`interface (Java).</span><span class="sxs-lookup"><span data-stu-id="8ded6-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="8ded6-141">Hello prend en charge de la classe de base acteur un `GetReminder`(c#) ou `getReminder`(méthode) (Java) qui peut être utilisés tooretrieve hello `IActorReminder`(c#) ou `ActorReminder`interface (Java) en passant dans le nom de rappel hello.</span><span class="sxs-lookup"><span data-stu-id="8ded6-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="8ded6-142">Ceci est pratique, car l’acteur de hello n’a pas besoin toopersist hello `IActorReminder`(c#) ou `ActorReminder`interface (Java) qui a été retourné à partir de hello `RegisterReminder`(c#) ou `registerReminder`appel de méthode (Java).</span><span class="sxs-lookup"><span data-stu-id="8ded6-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ded6-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ded6-143">Next Steps</span></span>
<span data-ttu-id="8ded6-144">En savoir plus sur les événements acteurs fiables et la réentrance :</span><span class="sxs-lookup"><span data-stu-id="8ded6-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="8ded6-145">Événements d’acteurs</span><span class="sxs-lookup"><span data-stu-id="8ded6-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="8ded6-146">Réentrance des acteurs</span><span class="sxs-lookup"><span data-stu-id="8ded6-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
