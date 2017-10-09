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
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="d23f0-103">Réentrance Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="d23f0-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="d23f0-104">par défaut, Hello Reliable Actors runtime, permet de réentrance basée sur le contexte d’appel logique.</span><span class="sxs-lookup"><span data-stu-id="d23f0-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="d23f0-105">Ainsi, reentrant de toobe acteurs s’ils sont en hello même appeler la chaîne du contexte.</span><span class="sxs-lookup"><span data-stu-id="d23f0-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="d23f0-106">Par exemple, acteur A envoie un message de tooActor B, qui envoie un message de tooActor C. Dans le cadre du traitement du message de salutation, si acteur C appelle acteur A, message de type hello est réentrant, afin qu’il sera possible.</span><span class="sxs-lookup"><span data-stu-id="d23f0-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="d23f0-107">Tout autre message faisant partie d’un contexte d’appel différent est bloqué au niveau de l’acteur A jusqu’à ce qu’il termine le traitement.</span><span class="sxs-lookup"><span data-stu-id="d23f0-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="d23f0-108">Il existe deux options disponibles pour la réentrance acteur définie dans hello `ActorReentrancyMode` enum :</span><span class="sxs-lookup"><span data-stu-id="d23f0-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="d23f0-109">`LogicalCallContext` (comportement par défaut)</span><span class="sxs-lookup"><span data-stu-id="d23f0-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="d23f0-110">`Disallowed` : désactive la réentrance</span><span class="sxs-lookup"><span data-stu-id="d23f0-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="d23f0-111">Vous pouvez configurer la réentrance dans les paramètres d’un `ActorService`lors de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="d23f0-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="d23f0-112">paramètre de Hello applique des instances d’acteur tooall créés dans le service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="d23f0-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="d23f0-113">Hello suivant montre un service d’acteur qui définit le mode de réentrance hello trop`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="d23f0-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="d23f0-114">Dans ce cas, si un intervenant envoie un acteur tooanother message réentrant, une exception de type `FabricException` sera levée.</span><span class="sxs-lookup"><span data-stu-id="d23f0-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="d23f0-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d23f0-115">Next steps</span></span>
* <span data-ttu-id="d23f0-116">En savoir plus sur la réentrance Bonjour [documentation de référence des API d’acteur](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="d23f0-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
