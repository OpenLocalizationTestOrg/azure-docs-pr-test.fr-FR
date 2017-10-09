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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="bb51c-103">Polymorphisme dans framework Reliable Actors de hello</span><span class="sxs-lookup"><span data-stu-id="bb51c-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="bb51c-104">Hello Reliable Actors framework vous permet des acteurs toobuild l’aide de plusieurs hello les mêmes techniques que vous utiliseriez dans la conception orientée objet.</span><span class="sxs-lookup"><span data-stu-id="bb51c-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="bb51c-105">Un de ces techniques est le polymorphisme, ce qui permet aux types et interfaces tooinherit à partir de plusieurs généralisé parents.</span><span class="sxs-lookup"><span data-stu-id="bb51c-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="bb51c-106">L’héritage dans le cadre de Reliable Actors hello suit généralement le modèle de .NET hello avec quelques contraintes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="bb51c-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="bb51c-107">En cas de Java/Linux, il suit les modèle de Java hello.</span><span class="sxs-lookup"><span data-stu-id="bb51c-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="bb51c-108">Interfaces</span><span class="sxs-lookup"><span data-stu-id="bb51c-108">Interfaces</span></span>
<span data-ttu-id="bb51c-109">infrastructure de Reliable Actors Hello nécessite que vous toodefine toobe au moins une interface implémentée par le type d’acteur.</span><span class="sxs-lookup"><span data-stu-id="bb51c-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="bb51c-110">Cette interface est utilisée toogenerate une classe proxy qui peut être utilisée par toocommunicate de clients avec votre acteurs.</span><span class="sxs-lookup"><span data-stu-id="bb51c-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="bb51c-111">Les interfaces peuvent hériter d’autres interfaces dès lors que toutes les interfaces implémentées par un type d’acteur et tous ses parents dérivent au final d’IActor (C#) ou d’Actor (Java).</span><span class="sxs-lookup"><span data-stu-id="bb51c-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="bb51c-112">IActor(C#) et Actor(Java) sont respectivement hello définie par la plateforme interfaces de base pour les acteurs dans les infrastructures hello .NET et Java.</span><span class="sxs-lookup"><span data-stu-id="bb51c-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="bb51c-113">Par conséquent, exemple de polymorphisme classique hello à l’aide de formes peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="bb51c-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![Hiérarchie d'interfaces pour les acteurs de forme][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="bb51c-115">Types</span><span class="sxs-lookup"><span data-stu-id="bb51c-115">Types</span></span>
<span data-ttu-id="bb51c-116">Vous pouvez également créer une hiérarchie des types d’acteur, qui sont dérivés de hello acteur classe de base qui est fourni par la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="bb51c-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="bb51c-117">Dans cas hello de formes, vous pouvez avoir une base de `Shape`(c#) ou `ShapeImpl`type (Java) :</span><span class="sxs-lookup"><span data-stu-id="bb51c-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="bb51c-118">Sous-types de `Shape`(c#) ou `ShapeImpl`(Java) peut substituer les méthodes à partir de la base de hello.</span><span class="sxs-lookup"><span data-stu-id="bb51c-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

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

<span data-ttu-id="bb51c-119">Hello de note `ActorService` attribut sur le type d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="bb51c-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="bb51c-120">Cet attribut indique le framework d’acteur fiable hello qu’il doit automatiquement créer un service pour l’hébergement des acteurs de ce type.</span><span class="sxs-lookup"><span data-stu-id="bb51c-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="bb51c-121">Dans certains cas, vous souhaiterez peut-être toocreate un type de base est destiné uniquement pour le partage des fonctionnalités avec les sous-types et ne seront jamais utilisée tooinstantiate acteurs concrètes.</span><span class="sxs-lookup"><span data-stu-id="bb51c-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="bb51c-122">Dans ce cas, vous devez utiliser hello `abstract` tooindicate (mot clé) que vous allez créer jamais un acteur en fonction de ce type.</span><span class="sxs-lookup"><span data-stu-id="bb51c-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb51c-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb51c-123">Next steps</span></span>
* <span data-ttu-id="bb51c-124">Consultez [comment framework de Reliable Actors hello s’appuie sur la plateforme de Service Fabric hello](service-fabric-reliable-actors-platform.md) tooprovide la fiabilité, d’évolutivité et un état cohérent.</span><span class="sxs-lookup"><span data-stu-id="bb51c-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="bb51c-125">En savoir plus sur hello [cycle de vie acteur](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="bb51c-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
