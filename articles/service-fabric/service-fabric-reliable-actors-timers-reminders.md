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
# <a name="actor-timers-and-reminders"></a>Minuteries et rappels d’acteur
Les acteurs peuvent planifier un travail régulier par eux-mêmes en inscrivant des minuteries ou des rappels. Cet article explique comment toouse minuteries et rappels et explique les différences de hello entre eux.

## <a name="actor-timers"></a>Minuteries des acteurs
Les minuteurs acteur fournissent un wrapper simple autour d’un tooensure du minuteur .NET ou Java que les méthodes de rappel hello respectent les garanties de concurrence activer hello hello acteurs runtime fournit.

Intervenants peuvent utiliser hello `RegisterTimer`(c#) ou `registerTimer`(Java) et `UnregisterTimer`(c#) ou `unregisterTimer`méthodes (Java) sur la base de leur classe tooregister et annuler l’inscription de leurs minuteurs. exemple Hello ci-dessous montre l’utilisation hello du minuteur d’API. Hello API sont très similaires toohello .NET timer ou un minuteur de Java. Dans cet exemple, lorsque le minuteur de hello arrive, hello acteurs runtime appellera hello `MoveObject`(c#) ou `moveObject`(méthode) (Java). méthode Hello est garantie concurrence toorespect hello activer. Aucune autre méthode d’acteur ou aucun autre rappel de minuterie n’est donc en cours d’exécution avant la fin de ce rappel.

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

Hello prochaine période de minuterie de hello démarre après que le rappel de hello termine l’exécution. Cela implique ce minuteur hello est arrêté alors que le rappel de hello s’exécute et qu’il est démarré lorsque le rappel de hello se termine.

Hello acteurs runtime enregistre les modifications apportées Gestionnaire d’état d’acteur toohello issue de rappel de hello. Si une erreur se produit dans l’enregistrement de l’état de hello, cet objet acteur sera désactivé et une nouvelle instance est activée.

Toutes les minuteries sont arrêtés lors de l’acteur de hello est désactivé dans le cadre du garbage collection. Aucun rappel de minuterie n’est appelé après cela. En outre, hello acteurs runtime ne conserve pas toutes les informations à propos des minuteries hello en cours d’exécution avant la désactivation. C’est toohello acteur tooregister tous les minuteurs dont il a besoin lorsqu’il est réactivé Bonjour futures. Pour plus d’informations, consultez la section de hello sur [nettoyage acteur](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Rappels d’acteur
Les rappels sont un mécanisme tootrigger rappels persistants sur un acteur à certaines heures. Leur fonctionnalité est tootimers similaire. Mais contrairement aux minuteries, les rappels sont déclenchées en toutes circonstances jusqu'à ce que les acteur hello leur enregistrement explicitement ou acteur de hello est supprimé explicitement. Plus précisément, des rappels sont déclenchées sur les basculements et les désactivations acteur car hello acteurs runtime conserve les informations sur les rappels d’acteur hello.

tooregister un rappel, un acteur appelle hello `RegisterReminderAsync` méthode fournie sur la classe de base hello, comme indiqué dans hello l’exemple suivant :

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

Dans cet exemple, `"Pay cell phone bill"` est le nom de rappel hello. Il s’agit d’une chaîne qui hello acteur utilise toouniquely identifier un rappel. `BitConverter.GetBytes(amountInDollars)`(C#) est le contexte hello associé au rappel de hello. Il sera passé toohello arrière acteur comme un rappel de rappel toohello argument, c'est-à-dire `IRemindable.ReceiveReminderAsync`(c#) ou `Remindable.receiveReminderAsync`(Java).

Les acteurs qui utilisent des rappels doivent implémenter hello `IRemindable` d’interface, comme indiqué dans l’exemple hello ci-dessous.

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

Lorsqu’un rappel est déclenché, hello Reliable Actors runtime appelle hello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(méthode) (Java) sur hello acteur. Un acteur peut enregistrer des rappels multiples et hello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(méthode) (Java) est appelé lorsque un de ces rappels est déclenché. acteur de Hello peut utiliser le nom de rappel de hello qui est passé dans toohello `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`toofigure de méthode (Java) à quels rappel a été déclenchée.

état d’acteur hello lorsque hello enregistre Hello acteurs runtime `ReceiveReminderAsync`(c#) ou `receiveReminderAsync`(Java) l’appel. Si une erreur se produit dans l’enregistrement de l’état de hello, cet objet acteur sera désactivé et une nouvelle instance est activée.

toounregister un rappel, un acteur appelle hello `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`(méthode) (Java), comme indiqué dans les exemples hello ci-dessous.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Comme indiqué ci-dessus, hello `UnregisterReminderAsync`(c#) ou `unregisterReminderAsync`(Java) méthode accepte un `IActorReminder`(c#) ou `ActorReminder`interface (Java). Hello prend en charge de la classe de base acteur un `GetReminder`(c#) ou `getReminder`(méthode) (Java) qui peut être utilisés tooretrieve hello `IActorReminder`(c#) ou `ActorReminder`interface (Java) en passant dans le nom de rappel hello. Ceci est pratique, car l’acteur de hello n’a pas besoin toopersist hello `IActorReminder`(c#) ou `ActorReminder`interface (Java) qui a été retourné à partir de hello `RegisterReminder`(c#) ou `registerReminder`appel de méthode (Java).

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les événements acteurs fiables et la réentrance :
* [Événements d’acteurs](service-fabric-reliable-actors-events.md)
* [Réentrance des acteurs](service-fabric-reliable-actors-reentrancy.md)
