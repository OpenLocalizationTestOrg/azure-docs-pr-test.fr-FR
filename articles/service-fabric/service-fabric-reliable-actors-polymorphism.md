---
title: "Polymorphisme dans l’infrastructure Reliable Actors | Microsoft Docs"
description: "Concevez des hiérarchies d’interfaces et de types .NET dans l’infrastructure Reliable Actors afin de réutiliser des fonctionnalités et des définitions d'API."
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
ms.openlocfilehash: 36a59a41b2261369a2062c76ef90aebf7e24a221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="polymorphism-in-the-reliable-actors-framework"></a><span data-ttu-id="72cc7-103">Polymorphisme dans l’infrastructure Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="72cc7-103">Polymorphism in the Reliable Actors framework</span></span>
<span data-ttu-id="72cc7-104">L’infrastructure Reliable Actors vous permet de générer des acteurs en utilisant bon nombre des mêmes techniques que celles employées dans la conception orientée objet.</span><span class="sxs-lookup"><span data-stu-id="72cc7-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="72cc7-105">L’une de ces techniques est le polymorphisme, qui permet à des types et à des interfaces d’hériter de parents plus généralisés.</span><span class="sxs-lookup"><span data-stu-id="72cc7-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span></span> <span data-ttu-id="72cc7-106">L’héritage dans l’infrastructure Reliable Actors suit généralement le modèle .NET avec quelques contraintes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="72cc7-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span></span> <span data-ttu-id="72cc7-107">Dans le cas de Java/Linux, il suit le modèle Java.</span><span class="sxs-lookup"><span data-stu-id="72cc7-107">In case of Java/Linux, it follows the Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="72cc7-108">Interfaces</span><span class="sxs-lookup"><span data-stu-id="72cc7-108">Interfaces</span></span>
<span data-ttu-id="72cc7-109">L’infrastructure Reliable Actors exige que vous définissiez au moins une interface que votre type d’acteur doit implémenter.</span><span class="sxs-lookup"><span data-stu-id="72cc7-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span></span> <span data-ttu-id="72cc7-110">Cette interface est utilisée pour générer une classe proxy, utilisable par des clients pour communiquer avec vos acteurs.</span><span class="sxs-lookup"><span data-stu-id="72cc7-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span></span> <span data-ttu-id="72cc7-111">Les interfaces peuvent hériter d’autres interfaces dès lors que toutes les interfaces implémentées par un type d’acteur et tous ses parents dérivent au final d’IActor (C#) ou d’Actor (Java).</span><span class="sxs-lookup"><span data-stu-id="72cc7-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="72cc7-112">IActor(C#) et Actor(Java) sont les interfaces de base définies par la plateforme pour les acteurs dans les infrastructures .NET et Java, respectivement.</span><span class="sxs-lookup"><span data-stu-id="72cc7-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span></span> <span data-ttu-id="72cc7-113">Par conséquent, voici à quoi peut ressembler un exemple de polymorphisme classique qui utilise des formes :</span><span class="sxs-lookup"><span data-stu-id="72cc7-113">Thus, the classic polymorphism example using shapes might look something like this:</span></span>

![Hiérarchie d'interfaces pour les acteurs de forme][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="72cc7-115">Types</span><span class="sxs-lookup"><span data-stu-id="72cc7-115">Types</span></span>
<span data-ttu-id="72cc7-116">Vous pouvez également créer une hiérarchie des types d’acteur, qui sont dérivés de la classe de base Actor fournie par la plateforme.</span><span class="sxs-lookup"><span data-stu-id="72cc7-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span></span> <span data-ttu-id="72cc7-117">Dans le cas de formes, vous pouvez avoir un type `Shape` (C#) ou `ShapeImpl` (Java) de base :</span><span class="sxs-lookup"><span data-stu-id="72cc7-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="72cc7-118">Les sous-types de `Shape` (C#) ou `ShapeImpl` (Java) peuvent remplacer des méthodes de la base.</span><span class="sxs-lookup"><span data-stu-id="72cc7-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span></span>

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

<span data-ttu-id="72cc7-119">Notez l’attribut `ActorService` sur le type d'intervenant.</span><span class="sxs-lookup"><span data-stu-id="72cc7-119">Note the `ActorService` attribute on the actor type.</span></span> <span data-ttu-id="72cc7-120">Cet attribut indique à l’infrastructure Reliable Actor qu’elle doit automatiquement créer un service pour héberger des acteurs de ce type.</span><span class="sxs-lookup"><span data-stu-id="72cc7-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="72cc7-121">Dans certains cas, vous pouvez souhaiter créer un type de base destiné exclusivement à la fonctionnalité de partage avec des sous-types, qui ne sera jamais utilisé pour instancier des acteurs concrets.</span><span class="sxs-lookup"><span data-stu-id="72cc7-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span></span> <span data-ttu-id="72cc7-122">Dans ce cas, vous devez utiliser le mot clé `abstract` pour indiquer que vous ne créerez jamais d’acteur basé sur ce type.</span><span class="sxs-lookup"><span data-stu-id="72cc7-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72cc7-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72cc7-123">Next steps</span></span>
* <span data-ttu-id="72cc7-124">Découvrez [comment l’infrastructure Reliable Actors s’appuie sur la plateforme Service Fabric](service-fabric-reliable-actors-platform.md) pour garantir la fiabilité, l’extensibilité et la cohérence.</span><span class="sxs-lookup"><span data-stu-id="72cc7-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="72cc7-125">En savoir plus sur le [cycle de vie des acteurs](service-fabric-reliable-actors-lifecycle.md)</span><span class="sxs-lookup"><span data-stu-id="72cc7-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
