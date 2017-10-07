---
title: "aaaCreate votre premier microservice Azure basé sur acteur en C# | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello de création, de débogage et de déploiement d’un service basé sur acteur simple à l’aide de l’infrastructure de Service Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="219fc-103">Prise en main de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="219fc-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="219fc-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="219fc-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="219fc-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="219fc-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="219fc-106">Cet article explique les principes fondamentaux de hello de Azure Service Fabric Reliable Actors et vous présente la création, de débogage et de déploiement d’une application fiable acteur simple dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="219fc-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="219fc-107">Installation et configuration</span><span class="sxs-lookup"><span data-stu-id="219fc-107">Installation and setup</span></span>
<span data-ttu-id="219fc-108">Avant de commencer, assurez-vous d’avoir l’environnement de développement de Service Fabric hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="219fc-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="219fc-109">Si vous avez besoin de tooset, configurez-le, consultez les instructions détaillées sur [comment tooset d’environnement de développement hello](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="219fc-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="219fc-110">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="219fc-110">Basic concepts</span></span>
<span data-ttu-id="219fc-111">tooget main Reliable Actors, vous seulement devez toounderstand quelques concepts de base :</span><span class="sxs-lookup"><span data-stu-id="219fc-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="219fc-112">**Service d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="219fc-112">**Actor service**.</span></span> <span data-ttu-id="219fc-113">Reliable Actors sont empaquetées dans des Services fiables qui peut être déployé dans une infrastructure de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="219fc-114">Les instances d’acteur sont activées dans une instance de service nommée.</span><span class="sxs-lookup"><span data-stu-id="219fc-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="219fc-115">**Enregistrement d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="219fc-115">**Actor registration**.</span></span> <span data-ttu-id="219fc-116">Comme avec les Services fiables, un service Reliable Actor doit toobe inscrit avec le runtime du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="219fc-117">En outre, le type d’acteur hello doit toobe inscrit avec le runtime d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="219fc-118">**Interface d’acteur**.</span><span class="sxs-lookup"><span data-stu-id="219fc-118">**Actor interface**.</span></span> <span data-ttu-id="219fc-119">interface d’acteur Hello est toodefine utilisé une interface publique fortement typée d’un acteur.</span><span class="sxs-lookup"><span data-stu-id="219fc-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="219fc-120">Bonjour terminologie relative aux modèles de Reliable Actor, interface d’acteur hello définit hello types de messages hello acteur peuvent comprendre et traiter.</span><span class="sxs-lookup"><span data-stu-id="219fc-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="219fc-121">interface d’acteur Hello est utilisé par d’autres acteurs et les applications clientes trop « envoient » (de façon asynchrone) acteur toohello de messages.</span><span class="sxs-lookup"><span data-stu-id="219fc-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="219fc-122">Reliable Actors peut implémenter plusieurs interfaces.</span><span class="sxs-lookup"><span data-stu-id="219fc-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="219fc-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="219fc-123">**ActorProxy class**.</span></span> <span data-ttu-id="219fc-124">Hello ActorProxy classe est utilisée par le client applications tooinvoke hello méthodes exposées via l’interface d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="219fc-125">Hello ActorProxy classe fournit deux fonctionnalités importantes :</span><span class="sxs-lookup"><span data-stu-id="219fc-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="219fc-126">La résolution de noms : il s’agit d’acteur de hello toolocate en mesure de cluster de hello (rechercher le nœud hello du cluster hello où il est hébergé).</span><span class="sxs-lookup"><span data-stu-id="219fc-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="219fc-127">Gestion de défaillance : il peut réessayer d’appels de méthode et de résoudre cet emplacement hello intervenant après avoir, par exemple, un échec qui nécessite hello acteur toobe déplacé tooanother nœud de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="219fc-128">Hello, suivant les règles qui se rapportent les interfaces tooactor est intéressant de mentionner :</span><span class="sxs-lookup"><span data-stu-id="219fc-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="219fc-129">Les méthodes d'interface d'acteur ne peuvent pas être surchargées.</span><span class="sxs-lookup"><span data-stu-id="219fc-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="219fc-130">Les méthodes d’interface d'acteur ne doivent pas avoir de paramètres de sortie, de paramètres de référence ou de paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="219fc-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="219fc-131">Les interfaces génériques ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="219fc-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="219fc-132">Création d'un projet dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="219fc-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="219fc-133">Lancez Visual Studio 2015 ou Visual Studio 2017 en tant qu’administrateur et créez un projet d’application Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="219fc-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Outils Service Fabric pour Visual Studio - nouveau projet][1]

<span data-ttu-id="219fc-135">Dans la boîte de dialogue hello suivante, vous pouvez choisir de type hello de projet que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="219fc-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Modèles de projets Service Fabric][5]

<span data-ttu-id="219fc-137">Pour le projet HelloWorld de hello, nous allons utiliser le service de l’infrastructure de Service Reliable Actors hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="219fc-138">Une fois que vous avez créé des solutions de hello, vous devez voir hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="219fc-138">After you have created hello solution, you should see hello following structure:</span></span>

![Structure d’un projet Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="219fc-140">Blocs de construction de base des acteurs fiables</span><span class="sxs-lookup"><span data-stu-id="219fc-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="219fc-141">Une solution Reliable Actors standard est composée de trois projets :</span><span class="sxs-lookup"><span data-stu-id="219fc-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="219fc-142">**projet d’application Hello (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="219fc-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="219fc-143">Il s’agit de projet hello que tous les services hello ensemble pour le déploiement de packages.</span><span class="sxs-lookup"><span data-stu-id="219fc-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="219fc-144">Il contient hello *ApplicationManifest.xml* et les scripts PowerShell pour gérer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="219fc-145">**projet d’interface Hello (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="219fc-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="219fc-146">Il s’agit de projet hello qui contient la définition d’interface hello pour l’acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="219fc-147">Dans le projet de MyActor.Interfaces hello, vous pouvez définir les interfaces hello qui seront utilisés par les acteurs hello dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="219fc-148">Vos interfaces acteur peuvent être définies dans n’importe quel projet avec n’importe quel nom, mais l’interface de hello définit contrat acteur hello qui est partagé par implémentation d’acteur hello et clients hello appelant acteur de hello, il est donc généralement toodefine de sens dans un assembly séparer de hello acteur implémentation et peut être partagé par plusieurs autres projets.</span><span class="sxs-lookup"><span data-stu-id="219fc-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="219fc-149">**projet de service d’acteur Hello (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="219fc-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="219fc-150">Il s’agit de hello projet utilisé toodefine hello Service Fabric service est continu toohost hello acteur.</span><span class="sxs-lookup"><span data-stu-id="219fc-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="219fc-151">Il contient la mise en œuvre hello d’acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="219fc-152">Une implémentation d’un acteur est une classe qui dérive du type de base hello `Actor` et implémente hello des interfaces qui sont définis dans le projet de MyActor.Interfaces hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="219fc-153">Une classe d’acteur doit également implémenter un constructeur qui accepte un `ActorService` instance et un `ActorId` et les transmet toohello base `Actor` classe.</span><span class="sxs-lookup"><span data-stu-id="219fc-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="219fc-154">Cela permet l’injection d’une dépendance de constructeur pour des dépendances de plateforme.</span><span class="sxs-lookup"><span data-stu-id="219fc-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="219fc-155">service d’acteur Hello doit être enregistré avec un type de service dans le runtime du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="219fc-156">Dans commande pour hello acteur Service toorun vos instances de l’acteur, votre type d’acteur doit également être enregistré avec hello Service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="219fc-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="219fc-157">Hello `ActorRuntime` méthode d’inscription exécute cette tâche pour acteurs.</span><span class="sxs-lookup"><span data-stu-id="219fc-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

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

<span data-ttu-id="219fc-158">Si vous démarrez un nouveau projet dans Visual Studio et vous n'avez qu’une seule définition d’acteur, l’inscription de hello est incluse par défaut dans le code hello généré par Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="219fc-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="219fc-159">Si vous définissez les autres intervenants dans le service hello, vous devez l’inscription de tooadd hello intervenant à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="219fc-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="219fc-160">Hello acteurs de l’infrastructure de Service runtime émet certaines [événements et compteurs de performance liés tooactor méthodes](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="219fc-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="219fc-161">Ces événements sont utiles dans les diagnostics et la surveillance des performances.</span><span class="sxs-lookup"><span data-stu-id="219fc-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="219fc-162">Débogage</span><span class="sxs-lookup"><span data-stu-id="219fc-162">Debugging</span></span>
<span data-ttu-id="219fc-163">outils de Service Fabric Hello pour Visual Studio prend en charge le débogage sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="219fc-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="219fc-164">Vous pouvez démarrer une session de débogage en hello atteinte touche F5.</span><span class="sxs-lookup"><span data-stu-id="219fc-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="219fc-165">Visual Studio génère (si nécessaire) des packages.</span><span class="sxs-lookup"><span data-stu-id="219fc-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="219fc-166">Il déploie l’application hello Cluster Service Fabric local de hello et attache le débogueur de hello.</span><span class="sxs-lookup"><span data-stu-id="219fc-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="219fc-167">Au cours du processus de déploiement hello, vous pouvez voir la progression hello Bonjour **sortie** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="219fc-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Fenêtre de sortie de débogage Service Fabric][3]

## <a name="next-steps"></a><span data-ttu-id="219fc-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="219fc-169">Next steps</span></span>
<span data-ttu-id="219fc-170">En savoir plus sur [comment Reliable Actors utiliser hello Service Fabric](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="219fc-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
