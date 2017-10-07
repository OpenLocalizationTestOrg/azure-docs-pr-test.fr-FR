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
# <a name="actor-events"></a>Événements d’acteurs
Événements d’acteur notifier un moyen toosend meilleur effort à partir de clients de toohello hello acteur. Les événements d’acteur sont conçus pour la communication acteur-client et ne doivent pas être utilisés pour la communication acteur-acteur.

afficher des extraits de code de la code Hello suivant comment toouse les événements intervenant dans votre application.

Définissez une interface qui décrit les événements hello publiés par acteur de hello. Cette interface doit être dérivée de hello `IActorEvents` interface. les arguments des méthodes de hello Hello doivent être [de contrat de données sérialisable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md). les méthodes de Hello doivent retourner void, en tant qu’événement notifications sont une façon et meilleur effort.

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
Déclarer des événements hello publiés par acteur hello dans l’interface d’acteur hello.

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
Côté client de hello, implémentez le Gestionnaire d’événements hello.

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

Sur le client de hello, créez un acteur toohello proxy qui publie les événements hello et abonner les événements de tooits.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

En cas de hello de basculements, acteur de hello peut basculer tooa autre processus ou de nœud. proxy d’acteur Hello gère les abonnements actifs hello et automatiquement nouveau s’abonne les. Vous pouvez contrôler l’intervalle de RE-abonnement hello via hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API. toounsubscribe, utilisez hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.

Sur l’acteur de hello, simplement publier des événements de hello comme ils se produisent. S’il existe des événements de toohello abonnés, hello acteurs runtime envoie les hello notification.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>Étapes suivantes
* [Réentrance des acteurs](service-fabric-reliable-actors-reentrancy.md)
* [Diagnostics et surveillance des performances d’acteur](service-fabric-reliable-actors-diagnostics.md)
* [Documentation de référence de l’API d’acteur](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Exemple de code C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemple de code C# .NET Core](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Exemple de code Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)
