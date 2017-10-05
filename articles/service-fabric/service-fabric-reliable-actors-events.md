---
title: "Événements dans les microservices Azure basés sur acteur | Microsoft Docs"
description: "Présentation des événements pour Reliable Actors Service Fabric"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: d936670c548ff709fc2e935d3f28d94e4bde8a04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-events"></a><span data-ttu-id="5401d-103">Événements d’acteurs</span><span class="sxs-lookup"><span data-stu-id="5401d-103">Actor events</span></span>
<span data-ttu-id="5401d-104">Les événements d’acteur sont un moyen d’envoyer des notifications Meilleur effort de l’acteur aux clients.</span><span class="sxs-lookup"><span data-stu-id="5401d-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="5401d-105">Les événements d’acteur sont conçus pour la communication acteur-client et ne doivent pas être utilisés pour la communication acteur-acteur.</span><span class="sxs-lookup"><span data-stu-id="5401d-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="5401d-106">L’extrait de code suivant montre comment utiliser les événements d’acteur dans votre application.</span><span class="sxs-lookup"><span data-stu-id="5401d-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="5401d-107">Définissez une interface qui décrit les événements publiés par l'acteur.</span><span class="sxs-lookup"><span data-stu-id="5401d-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="5401d-108">Cette interface doit être dérivée de l'interface `IActorEvents` .</span><span class="sxs-lookup"><span data-stu-id="5401d-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="5401d-109">Les arguments des méthodes doivent être [sérialisables en contrat de données](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="5401d-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="5401d-110">Les méthodes doivent retourner une valeur nulle, car les notifications d’événement sont unidirectionnelles et Meilleur effort.</span><span class="sxs-lookup"><span data-stu-id="5401d-110">The methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="5401d-111">Déclarez les événements publiés par l'acteur dans l'interface d'acteur.</span><span class="sxs-lookup"><span data-stu-id="5401d-111">Declare the events published by the actor in the actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="5401d-112">Côté client, implémentez le gestionnaire d'événements.</span><span class="sxs-lookup"><span data-stu-id="5401d-112">On the client side, implement the event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="5401d-113">Sur le client, créez un proxy pour l'acteur qui publie l'événement et s'abonne à ses événements.</span><span class="sxs-lookup"><span data-stu-id="5401d-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="5401d-114">En cas de basculement, l’acteur peut basculer sur un nœud ou processus différent.</span><span class="sxs-lookup"><span data-stu-id="5401d-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="5401d-115">Le proxy de l’acteur gère les abonnements actifs et s’y réabonne automatiquement.</span><span class="sxs-lookup"><span data-stu-id="5401d-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="5401d-116">Vous pouvez contrôler l’intervalle de réabonnement via l’API `ActorProxyEventExtensions.SubscribeAsync<TEvent>` .</span><span class="sxs-lookup"><span data-stu-id="5401d-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="5401d-117">Pour vous désabonner, utilisez l’API `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` .</span><span class="sxs-lookup"><span data-stu-id="5401d-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="5401d-118">Sur l'acteur, publiez simplement les événements à mesure qu'ils se produisent.</span><span class="sxs-lookup"><span data-stu-id="5401d-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="5401d-119">Le runtime Actors envoie la notification aux abonnés à l’événement, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="5401d-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="5401d-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5401d-120">Next steps</span></span>
* [<span data-ttu-id="5401d-121">Réentrance des acteurs</span><span class="sxs-lookup"><span data-stu-id="5401d-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="5401d-122">Diagnostics et surveillance des performances d’acteur</span><span class="sxs-lookup"><span data-stu-id="5401d-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="5401d-123">Documentation de référence de l’API d’acteur</span><span class="sxs-lookup"><span data-stu-id="5401d-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="5401d-124">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="5401d-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="5401d-125">Exemple de code C# .NET Core</span><span class="sxs-lookup"><span data-stu-id="5401d-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="5401d-126">Exemple de code Java</span><span class="sxs-lookup"><span data-stu-id="5401d-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
