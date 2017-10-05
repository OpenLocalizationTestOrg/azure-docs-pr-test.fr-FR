---
title: "Remarques sur Reliable Actors pour la sérialisation de type d’acteur | Documents Microsoft"
description: "Traite des exigences de base pour la définition des classes sérialisables pouvant servir à définir les interfaces et les états Service Fabric Reliable Actors"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4b48b893e5a3bf5620f00a336576efe1ad63def8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="035af-103">Remarques sur la sérialisation de type Reliable Actors Service Fabric</span><span class="sxs-lookup"><span data-stu-id="035af-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="035af-104">Les arguments de toutes les méthodes, les types de résultats des tâches retournées par chaque méthode dans une interface d’acteur et les objets stockés dans le Gestionnaire d’état d’un acteur doivent être [sérialisables en contrat de données](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="035af-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="035af-105">Cela s’applique également aux arguments des méthodes définies dans les [interfaces d’événement d’acteur](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="035af-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="035af-106">(Les méthodes d’interface d’événement d’acteur retournent toujours la valeur nulle.)</span><span class="sxs-lookup"><span data-stu-id="035af-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="035af-107">Types de données personnalisés</span><span class="sxs-lookup"><span data-stu-id="035af-107">Custom data types</span></span>
<span data-ttu-id="035af-108">Dans cet exemple, l’interface d’acteur suivante définit une méthode qui retourne un type de données personnalisé appelé `VoicemailBox` :</span><span class="sxs-lookup"><span data-stu-id="035af-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

<span data-ttu-id="035af-109">L’interface est implémentée par un acteur qui utilise le gestionnaire d’état pour stocker un objet `VoicemailBox` :</span><span class="sxs-lookup"><span data-stu-id="035af-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

<span data-ttu-id="035af-110">Dans cet exemple, l’objet `VoicemailBox` est sérialisé quand :</span><span class="sxs-lookup"><span data-stu-id="035af-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="035af-111">L’objet est transmis entre une instance d’acteur et un appelant.</span><span class="sxs-lookup"><span data-stu-id="035af-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="035af-112">L’objet est enregistré dans le gestionnaire d’état quand il est enregistré sur disque et répliqué vers d’autres nœuds.</span><span class="sxs-lookup"><span data-stu-id="035af-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="035af-113">L’infrastructure Reliable Actor utilise la sérialisation DataContract.</span><span class="sxs-lookup"><span data-stu-id="035af-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="035af-114">Par conséquent, les objets de données personnalisés et leurs membres doivent être annotés avec les attributs **DataContract** et **DataMember**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="035af-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a><span data-ttu-id="035af-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="035af-115">Next steps</span></span>
* [<span data-ttu-id="035af-116">Cycle de vie des acteurs et Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="035af-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="035af-117">Minuteries et rappels d’acteur</span><span class="sxs-lookup"><span data-stu-id="035af-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="035af-118">Événements d’acteurs</span><span class="sxs-lookup"><span data-stu-id="035af-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="035af-119">Réentrance des acteurs</span><span class="sxs-lookup"><span data-stu-id="035af-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="035af-120">Polymorphisme des acteurs et modèles de conception orientée objet</span><span class="sxs-lookup"><span data-stu-id="035af-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="035af-121">Diagnostics et surveillance des performances d’acteur</span><span class="sxs-lookup"><span data-stu-id="035af-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
