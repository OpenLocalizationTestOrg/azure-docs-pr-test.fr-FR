---
title: "aaaOverview du cycle de vie microservices de Azure basé sur acteur | Documents Microsoft"
description: "Explique le cycle de vie Service Fabric Reliable Actor, le Garbage Collection et la suppression manuelle des acteurs et de leur état"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>Cycle de vie des acteurs, Garbage Collection automatique et suppression manuelle
Un acteur est activé hello la première fois, un appel est fait tooany de ses méthodes. Un acteur est désactivé (garbage collection par le runtime d’acteurs hello) s’il n’est pas utilisé pendant une période configurable. Un acteur et son état peuvent également être supprimés manuellement, à tout moment.

## <a name="actor-activation"></a>Activation de l’acteur
Lorsqu’un acteur est activé, hello événements suivants se produisent :

* Quand un appel est émis vers un acteur qui n'est pas actif, un autre acteur est créé.
* état de Hello acteur est chargé si elle maintient l’état.
* Hello `OnActivateAsync` (c#) ou `onActivateAsync` (méthode) (Java) (qui peut être substituée dans une implémentation d’acteur hello) est appelée.
* acteur de Hello est désormais considérée comme active.

## <a name="actor-deactivation"></a>Désactivation de l’acteur
Lorsqu’un acteur est désactivé, hello événements suivants se produisent :

* Lorsqu’un intervenant n’est pas utilisé pendant un certain temps, il est supprimé à partir de la table des acteurs Active hello.
* Hello `OnDeactivateAsync` (c#) ou `onDeactivateAsync` (méthode) (Java) (qui peut être substituée dans une implémentation d’acteur hello) est appelée. Cela efface toutes les minuteries hello pour l’acteur de hello. Les opérations de l’acteur, comme la modification de l’état, ne doivent pas être appelées avec cette méthode.

> [!TIP]
> Hello acteurs de l’ensemble fibre optique exécution émet certaines [tooactor activation et désactivation des événements associés](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters). Ces événements sont utiles dans les diagnostics et la surveillance des performances.
>
>

### <a name="actor-garbage-collection"></a>Garbage Collection des acteurs
Lorsqu’un acteur est désactivé, objet de références toohello acteur sont libérées et il peut être le garbage collecté normalement par hello common language runtime (CLR) ou le garbage collector de java virtual machine (JVM). Le garbage collection uniquement nettoie les objets d’acteur hello ; Il effectue **pas** supprimer l’état stocké dans le Gestionnaire d’état d’acteur hello. Hello prochaine heure hello acteur est activé, un nouvel objet acteur est créé et son état est restauré.

Quel compte comme « utilisés » à des fins de hello de désactivation et de garbage collection ?

* Réception d'un appel
* `IRemindable.ReceiveReminderAsync`méthode appelée (applicable uniquement si l’acteur de hello utilise des rappels)

> [!NOTE]
> Si les acteur hello utilise des minuteurs et son rappel du minuteur est appelé, il ne **pas** en tant que le « utilisé ».
>
>

Avant d’entrer les détails de hello de désactivation, il est hello important toodefine dispositions suivantes :

* *Intervalle d'analyse*. Il s’agit d’intervalle hello sur l’acteurs hello runtime analyse sa table acteurs Active pour les acteurs qui peuvent être désactivés et que le garbage collector. valeur par défaut de Hello est 1 minute.
* *Délai d'inactivité*. Cela est hello temps qu’un acteur doit tooremain inutilisées (inactif) avant d’être désactivé et que le garbage collector. valeur par défaut de Hello est de 60 minutes.

En règle générale, il est inutile toochange ces valeurs par défaut. Toutefois, si nécessaire, ces intervalles peuvent être modifiés via `ActorServiceSettings` lorsque vous enregistrez votre [Service d’acteur](service-fabric-reliable-actors-platform.md):

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
Pour chaque acteur active, hello acteur runtime effectue le suivi de durée hello pendant laquelle il a été inactif pendant (c'est-à-dire, non utilisé). Hello acteur runtime vérifie chacune des acteurs de hello chaque `ScanIntervalInSeconds` toosee si elle peut être garbage collectées et il collecte, s’il a été inactif pendant `IdleTimeoutInSeconds`.

Chaque fois qu’un acteur est utilisé, sa durée d’inactivité est too0 de réinitialisation. Après cela, acteur de hello peut être le garbage collecté uniquement s’il reste encore inactif pour `IdleTimeoutInSeconds`. Rappelez-vous qu’un acteur est considéré comme toohave été utilisée si une méthode d’interface acteur ou d’un rappel de rappel d’acteur est exécuté. Un acteur est **pas** considéré comme toohave été si son rappel du minuteur est exécuté.

Hello diagramme suivant montre hello de cycle de vie d’un tooillustrate unique acteur ces concepts.

![Exemple de temps d'inactivité][1]

Il montre Hello impact hello des appels de méthode intervenant, les rappels, les minuteurs de durée de vie hello de cet acteur. Hello points sur hello exemple suivants est intéressant de mentionner :

* ScanInterval et IdleTimeout sont définies respectivement too5 et 10. (Unités de n’importe pas ici, car notre objectif n'est que le concept de hello tooillustrate.)
* analyse de Hello pour les acteurs toobe les garbage collecté se produit au T = 0, 5, 10, 15, 20, 25, tel que défini par l’intervalle d’analyse hello de 5.
* Une minuterie périodique se déclenche à T=4,8,12,16,20,24 et son rappel s'exécute. Il n’affecte pas la durée d’inactivité hello d’acteur de hello.
* Un appel de méthode intervenant au niveau de T = 7 réinitialise too0 du temps d’inactivité hello et retarde hello le garbage collection d’acteur de hello.
* Un rappel de rappel acteur s’exécute à T = 14 et plus les retards hello le garbage collection d’acteur de hello.
* Au cours de hello analyse de garbage collection à T = 25, durée d’inactivité d’acteur hello dépasse enfin délai d’inactivité de hello de 10 et acteur de hello est le garbage collecté.

Un acteur ne peut jamais faire l’objet d’un Garbage Collection quand il exécute l’une de ses méthodes, quelle que soit la durée d’exécution de cette méthode. Comme mentionné précédemment, l’exécution de hello de méthodes d’interface acteur et les rappels de rappel empêche le garbage collection en réinitialisant too0 de durée d’inactivité d’acteur hello. l’exécution de Hello de rappels de la minuterie ne réinitialise pas too0 du temps d’inactivité hello. Toutefois, hello le garbage collection d’acteur de hello est différé jusqu'à ce que la fin de l’exécution du rappel timer hello.

## <a name="deleting-actors-and-their-state"></a>Suppression des acteurs et de leur état
Le garbage collection d’acteurs désactivés nettoie uniquement objet d’acteur hello, mais elle ne supprime pas les données stockées dans le Gestionnaire d’état d’un acteur. Lorsqu’un acteur est réactivé, ses données sont effectuées tooit disponible via le Gestionnaire d’état de hello. Dans les cas où acteurs stocker des données dans le Gestionnaire d’état et sont désactivées, mais jamais nouveau activés, il peut être nécessaire tooclean leurs données.

Hello [acteur Service](service-fabric-reliable-actors-platform.md) fournit une fonction de suppression des intervenants à partir d’un appelant distant :

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

La suppression d’un acteur a hello suivant effets selon l’acteur de hello soit actif ou non :

* **Acteur actif**
  * L’acteur est supprimé de la liste des acteurs actifs et est désactivé.
  * Son état est définitivement supprimé.
* **Acteur inactif**
  * Son état est définitivement supprimé.

Notez qu’un acteur ne peut pas appeler delete sur lui-même à partir d’une de ses méthodes intervenant comme acteur de hello ne peut pas être supprimé pendant l’exécution d’un contexte d’appel acteur, dans quel hello runtime a obtenu un verrou autour hello acteur tooenforce monothread accès par appel de.

## <a name="next-steps"></a>Étapes suivantes
* [Minuteries et rappels d’acteur](service-fabric-reliable-actors-timers-reminders.md)
* [Événements d’acteurs](service-fabric-reliable-actors-events.md)
* [Réentrance des acteurs](service-fabric-reliable-actors-reentrancy.md)
* [Diagnostics et surveillance des performances d’acteur](service-fabric-reliable-actors-diagnostics.md)
* [Documentation de référence de l’API d’acteur](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Exemple de code C#](https://github.com/Azure/servicefabric-samples)
* [Exemple de code Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
