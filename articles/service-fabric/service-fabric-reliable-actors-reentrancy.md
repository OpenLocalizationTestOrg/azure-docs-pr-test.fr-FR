---
title: "aaaReentrancy dans microservices de Azure basé sur acteur | Documents Microsoft"
description: "Tooreentrancy d’introduction pour Service Fabric Reliable Actors"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a>Réentrance Reliable Actors
par défaut, Hello Reliable Actors runtime, permet de réentrance basée sur le contexte d’appel logique. Ainsi, reentrant de toobe acteurs s’ils sont en hello même appeler la chaîne du contexte. Par exemple, acteur A envoie un message de tooActor B, qui envoie un message de tooActor C. Dans le cadre du traitement du message de salutation, si acteur C appelle acteur A, message de type hello est réentrant, afin qu’il sera possible. Tout autre message faisant partie d’un contexte d’appel différent est bloqué au niveau de l’acteur A jusqu’à ce qu’il termine le traitement.

Il existe deux options disponibles pour la réentrance acteur définie dans hello `ActorReentrancyMode` enum :

* `LogicalCallContext` (comportement par défaut)
* `Disallowed` : désactive la réentrance

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
Vous pouvez configurer la réentrance dans les paramètres d’un `ActorService`lors de l’inscription. paramètre de Hello applique des instances d’acteur tooall créés dans le service d’acteur hello.

Hello suivant montre un service d’acteur qui définit le mode de réentrance hello trop`ActorReentrancyMode.Disallowed`. Dans ce cas, si un intervenant envoie un acteur tooanother message réentrant, une exception de type `FabricException` sera levée.

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la réentrance Bonjour [documentation de référence des API d’acteur](https://msdn.microsoft.com/library/azure/dn971626.aspx)
