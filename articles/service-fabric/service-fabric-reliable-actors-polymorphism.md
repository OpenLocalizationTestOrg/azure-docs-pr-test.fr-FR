---
title: aaaPolymorphism Framework de Reliable Actors hello | Documents Microsoft
description: "Créer des hiérarchies de types Bonjour fonctionnalité tooreuse de framework Reliable Actors et définitions de l’API et interfaces .NET."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Polymorphisme dans framework Reliable Actors de hello
Hello Reliable Actors framework vous permet des acteurs toobuild l’aide de plusieurs hello les mêmes techniques que vous utiliseriez dans la conception orientée objet. Un de ces techniques est le polymorphisme, ce qui permet aux types et interfaces tooinherit à partir de plusieurs généralisé parents. L’héritage dans le cadre de Reliable Actors hello suit généralement le modèle de .NET hello avec quelques contraintes supplémentaires. En cas de Java/Linux, il suit les modèle de Java hello.

## <a name="interfaces"></a>Interfaces
infrastructure de Reliable Actors Hello nécessite que vous toodefine toobe au moins une interface implémentée par le type d’acteur. Cette interface est utilisée toogenerate une classe proxy qui peut être utilisée par toocommunicate de clients avec votre acteurs. Les interfaces peuvent hériter d’autres interfaces dès lors que toutes les interfaces implémentées par un type d’acteur et tous ses parents dérivent au final d’IActor (C#) ou d’Actor (Java). IActor(C#) et Actor(Java) sont respectivement hello définie par la plateforme interfaces de base pour les acteurs dans les infrastructures hello .NET et Java. Par conséquent, exemple de polymorphisme classique hello à l’aide de formes peut ressembler à ceci :

![Hiérarchie d'interfaces pour les acteurs de forme][shapes-interface-hierarchy]

## <a name="types"></a>Types
Vous pouvez également créer une hiérarchie des types d’acteur, qui sont dérivés de hello acteur classe de base qui est fourni par la plateforme de hello. Dans cas hello de formes, vous pouvez avoir une base de `Shape`(c#) ou `ShapeImpl`type (Java) :

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

Sous-types de `Shape`(c#) ou `ShapeImpl`(Java) peut substituer les méthodes à partir de la base de hello.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

Hello de note `ActorService` attribut sur le type d’acteur hello. Cet attribut indique le framework d’acteur fiable hello qu’il doit automatiquement créer un service pour l’hébergement des acteurs de ce type. Dans certains cas, vous souhaiterez peut-être toocreate un type de base est destiné uniquement pour le partage des fonctionnalités avec les sous-types et ne seront jamais utilisée tooinstantiate acteurs concrètes. Dans ce cas, vous devez utiliser hello `abstract` tooindicate (mot clé) que vous allez créer jamais un acteur en fonction de ce type.

## <a name="next-steps"></a>Étapes suivantes
* Consultez [comment framework de Reliable Actors hello s’appuie sur la plateforme de Service Fabric hello](service-fabric-reliable-actors-platform.md) tooprovide la fiabilité, d’évolutivité et un état cohérent.
* En savoir plus sur hello [cycle de vie acteur](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
