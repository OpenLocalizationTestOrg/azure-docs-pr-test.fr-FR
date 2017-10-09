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
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a>Remarques sur la sérialisation de type Reliable Actors Service Fabric
arguments Hello de toutes les méthodes, types de résultats de tâches de hello retournées par chaque méthode dans une interface d’acteur et objets stockés dans le Gestionnaire d’état d’un acteur doivent être [de contrat de données sérialisable](https://msdn.microsoft.com/library/ms731923.aspx). Cela s’applique également toohello les arguments des méthodes hello définies dans [interfaces d’événements acteur](service-fabric-reliable-actors-events.md). (Les méthodes d’interface d’événement d’acteur retournent toujours la valeur nulle.)

## <a name="custom-data-types"></a>Types de données personnalisés
Dans cet exemple, hello suivant interface d’acteur définit une méthode qui retourne un type de données personnalisé appelé `VoicemailBox`:

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

interface de Hello est implémentée par un acteur qui utilise hello état manager toostore un `VoicemailBox` objet :

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

Dans cet exemple, hello `VoicemailBox` l’objet est sérialisé lorsque :

* objet de Hello transmise entre une instance de l’acteur et un appelant.
* objet de Hello est enregistré dans le Gestionnaire d’état hello où elle est persistante toodisk et répliquées tooother nœuds.

infrastructure de Reliable Actor Hello utilise la sérialisation de DataContract. Hello, par conséquent, les objets de données personnalisés et leurs membres doivent être annotés avec hello **DataContract** et **DataMember** des attributs, respectivement.

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


## <a name="next-steps"></a>Étapes suivantes
* [Cycle de vie des acteurs et Garbage Collection](service-fabric-reliable-actors-lifecycle.md)
* [Minuteries et rappels d’acteur](service-fabric-reliable-actors-timers-reminders.md)
* [Événements d’acteurs](service-fabric-reliable-actors-events.md)
* [Réentrance des acteurs](service-fabric-reliable-actors-reentrancy.md)
* [Polymorphisme des acteurs et modèles de conception orientée objet](service-fabric-reliable-actors-polymorphism.md)
* [Diagnostics et surveillance des performances d’acteur](service-fabric-reliable-actors-diagnostics.md)
