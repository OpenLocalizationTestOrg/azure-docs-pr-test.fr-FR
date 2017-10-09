---
title: "sérialisation de type de notes d’acteurs d’aaaReliable sur acteur | Documents Microsoft"
description: "Décrit les exigences de base pour la définition d’interfaces et des classes sérialisables qui peuvent être utilisé toodefine Service Fabric Reliable Actors États"
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
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="55a5d-103">Remarques sur la sérialisation de type Reliable Actors Service Fabric</span><span class="sxs-lookup"><span data-stu-id="55a5d-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="55a5d-104">arguments Hello de toutes les méthodes, types de résultats de tâches de hello retournées par chaque méthode dans une interface d’acteur et objets stockés dans le Gestionnaire d’état d’un acteur doivent être [de contrat de données sérialisable](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="55a5d-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="55a5d-105">Cela s’applique également toohello les arguments des méthodes hello définies dans [interfaces d’événements acteur](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="55a5d-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="55a5d-106">(Les méthodes d’interface d’événement d’acteur retournent toujours la valeur nulle.)</span><span class="sxs-lookup"><span data-stu-id="55a5d-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="55a5d-107">Types de données personnalisés</span><span class="sxs-lookup"><span data-stu-id="55a5d-107">Custom data types</span></span>
<span data-ttu-id="55a5d-108">Dans cet exemple, hello suivant interface d’acteur définit une méthode qui retourne un type de données personnalisé appelé `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="55a5d-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="55a5d-109">interface de Hello est implémentée par un acteur qui utilise hello état manager toostore un `VoicemailBox` objet :</span><span class="sxs-lookup"><span data-stu-id="55a5d-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="55a5d-110">Dans cet exemple, hello `VoicemailBox` l’objet est sérialisé lorsque :</span><span class="sxs-lookup"><span data-stu-id="55a5d-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="55a5d-111">objet de Hello transmise entre une instance de l’acteur et un appelant.</span><span class="sxs-lookup"><span data-stu-id="55a5d-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="55a5d-112">objet de Hello est enregistré dans le Gestionnaire d’état hello où elle est persistante toodisk et répliquées tooother nœuds.</span><span class="sxs-lookup"><span data-stu-id="55a5d-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="55a5d-113">infrastructure de Reliable Actor Hello utilise la sérialisation de DataContract.</span><span class="sxs-lookup"><span data-stu-id="55a5d-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="55a5d-114">Hello, par conséquent, les objets de données personnalisés et leurs membres doivent être annotés avec hello **DataContract** et **DataMember** des attributs, respectivement.</span><span class="sxs-lookup"><span data-stu-id="55a5d-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="55a5d-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="55a5d-115">Next steps</span></span>
* [<span data-ttu-id="55a5d-116">Cycle de vie des acteurs et Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="55a5d-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="55a5d-117">Minuteries et rappels d’acteur</span><span class="sxs-lookup"><span data-stu-id="55a5d-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="55a5d-118">Événements d’acteurs</span><span class="sxs-lookup"><span data-stu-id="55a5d-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="55a5d-119">Réentrance des acteurs</span><span class="sxs-lookup"><span data-stu-id="55a5d-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="55a5d-120">Polymorphisme des acteurs et modèles de conception orientée objet</span><span class="sxs-lookup"><span data-stu-id="55a5d-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="55a5d-121">Diagnostics et surveillance des performances d’acteur</span><span class="sxs-lookup"><span data-stu-id="55a5d-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
