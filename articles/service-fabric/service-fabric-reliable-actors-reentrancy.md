---
title: "Réentrance dans les microservices Azure basés sur acteur | Microsoft Docs"
description: "Présentation de la réentrance pour Service Fabric Reliable Actors"
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
ms.openlocfilehash: 00fcccb379bf1ba3875fbaba57a05b00fa228622
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="aca7c-103">Réentrance Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="aca7c-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="aca7c-104">Par défaut, le runtime Reliable Actors autorise la réentrance des appels logiques selon le contexte.</span><span class="sxs-lookup"><span data-stu-id="aca7c-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="aca7c-105">Cela permet de réentrer des acteurs s'ils se trouvent dans la même chaîne de contexte d'appel.</span><span class="sxs-lookup"><span data-stu-id="aca7c-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="aca7c-106">Par exemple, un acteur A envoie un message à un acteur B qui envoie le message à un acteur C. Dans le cadre du traitement du message, si l’acteur C appelle l’acteur A, le message est réentrant et donc autorisé.</span><span class="sxs-lookup"><span data-stu-id="aca7c-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="aca7c-107">Tout autre message faisant partie d’un contexte d’appel différent est bloqué au niveau de l’acteur A jusqu’à ce qu’il termine le traitement.</span><span class="sxs-lookup"><span data-stu-id="aca7c-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="aca7c-108">Deux options disponibles pour la réentrance des acteurs sont définies dans l’enum `ActorReentrancyMode` :</span><span class="sxs-lookup"><span data-stu-id="aca7c-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="aca7c-109">`LogicalCallContext` (comportement par défaut)</span><span class="sxs-lookup"><span data-stu-id="aca7c-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="aca7c-110">`Disallowed` : désactive la réentrance</span><span class="sxs-lookup"><span data-stu-id="aca7c-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="aca7c-111">Vous pouvez configurer la réentrance dans les paramètres d’un `ActorService`lors de l’inscription.</span><span class="sxs-lookup"><span data-stu-id="aca7c-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="aca7c-112">Le paramètre s’applique à toutes les instances d’acteur créées dans le service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="aca7c-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="aca7c-113">L’exemple suivant montre un service d’acteur qui affecte la valeur `ActorReentrancyMode.Disallowed`au mode de réentrance.</span><span class="sxs-lookup"><span data-stu-id="aca7c-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="aca7c-114">Dans ce cas, si un acteur envoie un message réentrant à un autre acteur, une exception de type `FabricException` est levée.</span><span class="sxs-lookup"><span data-stu-id="aca7c-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="aca7c-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aca7c-115">Next steps</span></span>
* <span data-ttu-id="aca7c-116">En savoir plus sur la réentrance dans la [documentation de référence de l’API Actor](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="aca7c-116">Learn more about reentrancy in the [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
