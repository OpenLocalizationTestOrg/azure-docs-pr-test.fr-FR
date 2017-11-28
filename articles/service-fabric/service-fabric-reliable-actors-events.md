---
title: "aaaEvents dans microservices de Azure basé sur acteur | Documents Microsoft"
description: "Tooevents d’introduction pour Service Fabric Reliable Actors."
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
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="8e643-103">Événements d’acteurs</span><span class="sxs-lookup"><span data-stu-id="8e643-103">Actor events</span></span>
<span data-ttu-id="8e643-104">Événements d’acteur notifier un moyen toosend meilleur effort à partir de clients de toohello hello acteur.</span><span class="sxs-lookup"><span data-stu-id="8e643-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="8e643-105">Les événements d’acteur sont conçus pour la communication acteur-client et ne doivent pas être utilisés pour la communication acteur-acteur.</span><span class="sxs-lookup"><span data-stu-id="8e643-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="8e643-106">afficher des extraits de code de la code Hello suivant comment toouse les événements intervenant dans votre application.</span><span class="sxs-lookup"><span data-stu-id="8e643-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="8e643-107">Définissez une interface qui décrit les événements hello publiés par acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="8e643-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="8e643-108">Cette interface doit être dérivée de hello `IActorEvents` interface.</span><span class="sxs-lookup"><span data-stu-id="8e643-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="8e643-109">les arguments des méthodes de hello Hello doivent être [de contrat de données sérialisable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="8e643-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="8e643-110">les méthodes de Hello doivent retourner void, en tant qu’événement notifications sont une façon et meilleur effort.</span><span class="sxs-lookup"><span data-stu-id="8e643-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="8e643-111">Déclarer des événements hello publiés par acteur hello dans l’interface d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="8e643-111">Declare hello events published by hello actor in hello actor interface.</span></span>

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
<span data-ttu-id="8e643-112">Côté client de hello, implémentez le Gestionnaire d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="8e643-112">On hello client side, implement hello event handler.</span></span>

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

<span data-ttu-id="8e643-113">Sur le client de hello, créez un acteur toohello proxy qui publie les événements hello et abonner les événements de tooits.</span><span class="sxs-lookup"><span data-stu-id="8e643-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="8e643-114">En cas de hello de basculements, acteur de hello peut basculer tooa autre processus ou de nœud.</span><span class="sxs-lookup"><span data-stu-id="8e643-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="8e643-115">proxy d’acteur Hello gère les abonnements actifs hello et automatiquement nouveau s’abonne les.</span><span class="sxs-lookup"><span data-stu-id="8e643-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="8e643-116">Vous pouvez contrôler l’intervalle de RE-abonnement hello via hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="8e643-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="8e643-117">toounsubscribe, utilisez hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="8e643-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="8e643-118">Sur l’acteur de hello, simplement publier des événements de hello comme ils se produisent.</span><span class="sxs-lookup"><span data-stu-id="8e643-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="8e643-119">S’il existe des événements de toohello abonnés, hello acteurs runtime envoie les hello notification.</span><span class="sxs-lookup"><span data-stu-id="8e643-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="8e643-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e643-120">Next steps</span></span>
* [<span data-ttu-id="8e643-121">Réentrance des acteurs</span><span class="sxs-lookup"><span data-stu-id="8e643-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="8e643-122">Diagnostics et surveillance des performances d’acteur</span><span class="sxs-lookup"><span data-stu-id="8e643-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="8e643-123">Documentation de référence de l’API d’acteur</span><span class="sxs-lookup"><span data-stu-id="8e643-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="8e643-124">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="8e643-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="8e643-125">Exemple de code C# .NET Core</span><span class="sxs-lookup"><span data-stu-id="8e643-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="8e643-126">Exemple de code Java</span><span class="sxs-lookup"><span data-stu-id="8e643-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
