---
title: Reliable Actors dans Service Fabric | Microsoft Docs
description: "Décrit comment les Reliable Actors sont superposés en couches sur des Reliable Services et utilisent les fonctionnalités de la plateforme Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 0a12da52b6e74c721cd25f89e7cde3c07153a396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="30128-103">Comment le service Reliable Actors utilise la plateforme Service Fabric</span><span class="sxs-lookup"><span data-stu-id="30128-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="30128-104">Cet article décrit le fonctionnement du service Reliable Actors sur la plateforme Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="30128-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="30128-105">La solution Reliable Actors s’exécute dans une infrastructure hébergée dans une implémentation d’un service fiable avec état nommé *service d’acteur*.</span><span class="sxs-lookup"><span data-stu-id="30128-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="30128-106">Le service d’acteur contient tous les composants nécessaires pour gérer le cycle de vie et la distribution des messages destinés à vos acteurs :</span><span class="sxs-lookup"><span data-stu-id="30128-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="30128-107">Le runtime de l’acteur gère le cycle de vie et le nettoyage de la mémoire, et applique une accès monothread.</span><span class="sxs-lookup"><span data-stu-id="30128-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="30128-108">Un écouteur de communication à distance du service d’acteur accepte les appels d’accès à distance adressés aux acteurs, et les transmet à un répartiteur qui les route vers l’instance d’acteur appropriée.</span><span class="sxs-lookup"><span data-stu-id="30128-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="30128-109">Le fournisseur d’état de l’acteur encapsule des fournisseurs d’état (par exemple, le fournisseur d’état Collections fiables), et fournit un adaptateur pour la gestion de l’état de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="30128-110">Ces composants forment ensemble l’infrastructure d’acteur fiable.</span><span class="sxs-lookup"><span data-stu-id="30128-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="30128-111">Couches de service</span><span class="sxs-lookup"><span data-stu-id="30128-111">Service layering</span></span>
<span data-ttu-id="30128-112">Étant donné que le service d’acteur est un service fiable, l’ensemble des concepts des Reliable Services relatifs au [modèle d’application](service-fabric-application-model.md), au cycle de vie, à [l’empaquetage](service-fabric-package-apps.md), au [déploiement](service-fabric-deploy-remove-applications.md), à la mise à niveau et à la mise à l’échelle s’appliquent de la même manière aux services d’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![Superposition de service d’acteur][1]

<span data-ttu-id="30128-114">Le diagramme précédent montre la relation entre les infrastructures d’application de Service Fabric et le code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="30128-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="30128-115">Les éléments en bleu représentent l’infrastructure d’application de Reliable Services, ceux en orange l’infrastructure de Reliable Actors, et ceux en vert le code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="30128-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="30128-116">Dans Reliable Services, votre service hérite de la classe `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="30128-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="30128-117">Cette classe est dérivée de `StatefulServiceBase` (ou `StatelessService` pour les services sans état).</span><span class="sxs-lookup"><span data-stu-id="30128-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="30128-118">Dans les Reliable Actors, vous utilisez le service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="30128-119">Le service d’acteur est une implémentation différente de la classe `StatefulServiceBase` qui implémente le modèle d’acteur dans lequel vos acteurs s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="30128-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="30128-120">Le service d’acteur proprement dit est simplement une implémentation de `StatefulServiceBase`. Vous pouvez donc écrire votre propre service qui dérive de `ActorService` et implémenter des fonctionnalités au niveau du service de la même façon que si vous héritiez de `StatefulService`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="30128-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="30128-121">Sauvegarde et restauration du service.</span><span class="sxs-lookup"><span data-stu-id="30128-121">Service backup and restore.</span></span>
* <span data-ttu-id="30128-122">Fonctionnalité partagée par tous les acteurs. Par exemple, un disjoncteur.</span><span class="sxs-lookup"><span data-stu-id="30128-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="30128-123">Appels de procédure à distance sur le service d’acteur proprement dit et sur chaque acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="30128-124">Actuellement, les services avec état ne sont pas pris en charge par Java / Linux.</span><span class="sxs-lookup"><span data-stu-id="30128-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="30128-125">Utilisation du service d’acteur</span><span class="sxs-lookup"><span data-stu-id="30128-125">Using the actor service</span></span>
<span data-ttu-id="30128-126">Les instances d’acteur ont accès au service d’acteur dans lequel elles s’exécutent.</span><span class="sxs-lookup"><span data-stu-id="30128-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="30128-127">Via le service d’acteur, les instances d’acteur peuvent obtenir par programmation le contexte de service.</span><span class="sxs-lookup"><span data-stu-id="30128-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="30128-128">Le contexte de service comprend l’ID de partition, le nom du service, le nom de l’application et d’autres informations spécifiques de la plateforme Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="30128-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="30128-129">Comme tous les services Reliable Services, le service d’acteur doit être inscrit avec un type de service dans le runtime de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="30128-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="30128-130">Pour que le service d’acteur exécute vos instances d’acteur, votre type d’acteur doit également être inscrit auprès du service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="30128-131">La méthode d’inscription `ActorRuntime` effectue ce travail pour les acteurs.</span><span class="sxs-lookup"><span data-stu-id="30128-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="30128-132">Dans le cas le plus simple, vous pouvez simplement enregistrer votre type d’acteur. Le service d’acteur avec les paramètres par défaut est alors utilisé de façon implicite :</span><span class="sxs-lookup"><span data-stu-id="30128-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="30128-133">Vous pouvez également utiliser une expression lambda fournie par la méthode d’inscription pour construire vous-même le service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="30128-134">Vous pouvez alors configurer le service d’acteur et construire explicitement vos instances d’acteur, pour y injecter des dépendances à votre acteur via son constructeur :</span><span class="sxs-lookup"><span data-stu-id="30128-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="30128-135">Méthodes du service d’acteur</span><span class="sxs-lookup"><span data-stu-id="30128-135">Actor service methods</span></span>
<span data-ttu-id="30128-136">Le service d’acteur implémente `IActorService` (C#) `ActorService` (Java), qui implémente à son tour `IService` (C#) ou `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="30128-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="30128-137">Il s’agit de l’interface qu’utilise la communication à distance de Reliable Services, qui autorise des appels de procédure distante sur les méthodes de service.</span><span class="sxs-lookup"><span data-stu-id="30128-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="30128-138">Elle contient des méthodes de niveau de service qui peuvent être appelées à distance via la communication à distance des services.</span><span class="sxs-lookup"><span data-stu-id="30128-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="30128-139">Énumération des acteurs</span><span class="sxs-lookup"><span data-stu-id="30128-139">Enumerating actors</span></span>
<span data-ttu-id="30128-140">Le service d’acteur permet à un client d’énumérer des métadonnées sur les acteurs hébergés par le service.</span><span class="sxs-lookup"><span data-stu-id="30128-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="30128-141">Le service d’acteur est un service avec état partitionné. L’énumération est donc effectuée par partition.</span><span class="sxs-lookup"><span data-stu-id="30128-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="30128-142">Étant donné que chaque partition peut contenir de nombreux acteurs, l’énumération est renvoyée sous la forme d’un ensemble de résultats paginés.</span><span class="sxs-lookup"><span data-stu-id="30128-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="30128-143">Les pages sont traitées en boucle jusqu’à ce qu’elles aient toutes été lues.</span><span class="sxs-lookup"><span data-stu-id="30128-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="30128-144">L’exemple suivant montre comment créer une liste de tous les acteurs actifs dans une partition d’un service d’acteur :</span><span class="sxs-lookup"><span data-stu-id="30128-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="30128-145">Suppression d’acteurs</span><span class="sxs-lookup"><span data-stu-id="30128-145">Deleting actors</span></span>
<span data-ttu-id="30128-146">Le service d’acteur fournit également une fonction permettant de supprimer des acteurs :</span><span class="sxs-lookup"><span data-stu-id="30128-146">The actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="30128-147">Pour plus d’informations sur la suppression des acteurs et de leur état, consultez la [documentation sur le cycle de vie des acteurs](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="30128-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="30128-148">Service d’acteur personnalisé</span><span class="sxs-lookup"><span data-stu-id="30128-148">Custom actor service</span></span>
<span data-ttu-id="30128-149">En utilisant la fonction lambda de l’inscription d’acteur, vous pouvez enregistrer votre propre service d’acteur personnalisé qui dérive de `ActorService` (c#) et `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="30128-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="30128-150">Dans ce service d’acteur personnalisé, vous pouvez implémenter vos propres fonctionnalités de niveau de service en écrivant une classe de service qui hérite de `ActorService` (c#) ou `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="30128-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="30128-151">Un service d’acteur personnalisé hérite de toutes les fonctionnalités de runtime d’acteur de `ActorService` (C#) ou `FabricActorService` (Java). Vous pouvez l’utiliser pour implémenter vos propres méthodes de service.</span><span class="sxs-lookup"><span data-stu-id="30128-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
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
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="30128-152">Implémentation d’une sauvegarde et restauration d’acteur</span><span class="sxs-lookup"><span data-stu-id="30128-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="30128-153">Dans l’exemple suivant, le service d’acteur personnalisé expose une méthode pour sauvegarder des données d’acteur en tirant parti de l’écouteur de communication à distance déjà présent dans `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="30128-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store the contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="30128-154">Dans cet exemple, `IMyActorService` est un contrat de communication à distance qui implémente `IService` (C#) et `Service` (Java) et est ensuite implémenté par `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="30128-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="30128-155">Suite à l’ajout de ce contrat de communication à distance, vous pouvez rendre les méthodes sur `IMyActorService` également disponibles pour un client en créant un proxy de communication à distance via `ActorServiceProxy` :</span><span class="sxs-lookup"><span data-stu-id="30128-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="30128-156">Modèle d'application</span><span class="sxs-lookup"><span data-stu-id="30128-156">Application model</span></span>
<span data-ttu-id="30128-157">Les services d’acteur étant des Reliable Services, le modèle d’application est le même.</span><span class="sxs-lookup"><span data-stu-id="30128-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="30128-158">Toutefois, les outils de génération d’infrastructure d’acteur produisent certains fichiers de modèle d’application pour vous.</span><span class="sxs-lookup"><span data-stu-id="30128-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="30128-159">Manifeste de service</span><span class="sxs-lookup"><span data-stu-id="30128-159">Service manifest</span></span>
<span data-ttu-id="30128-160">Les outils de génération d’infrastructure d’acteur génèrent automatiquement le contenu du fichier ServiceManifest.xml de votre service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="30128-161">Ce fichier inclut :</span><span class="sxs-lookup"><span data-stu-id="30128-161">This file includes:</span></span>

* <span data-ttu-id="30128-162">Le type de service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-162">Actor service type.</span></span> <span data-ttu-id="30128-163">Le nom du type est généré en fonction du nom du projet d’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="30128-164">En fonction de l’attribut de persistance sur votre acteur, l’indicateur HasPersistedState est également défini en conséquence.</span><span class="sxs-lookup"><span data-stu-id="30128-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="30128-165">le package de code ;</span><span class="sxs-lookup"><span data-stu-id="30128-165">Code package.</span></span>
* <span data-ttu-id="30128-166">le package de configuration ;</span><span class="sxs-lookup"><span data-stu-id="30128-166">Config package.</span></span>
* <span data-ttu-id="30128-167">les ressources et points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="30128-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="30128-168">Manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="30128-168">Application manifest</span></span>
<span data-ttu-id="30128-169">Les outils de génération d’infrastructure d’acteur créent automatiquement une définition de service par défaut pour votre service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="30128-170">Les outils de génération définissent les propriétés de service par défaut :</span><span class="sxs-lookup"><span data-stu-id="30128-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="30128-171">Le nombre de jeux de réplicas est déterminé par l’attribut de persistance sur votre acteur.</span><span class="sxs-lookup"><span data-stu-id="30128-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="30128-172">À chaque modification de l’attribut de persistance sur votre acteur, le nombre de jeux de réplicas dans la définition de service par défaut est réinitialisé en conséquence.</span><span class="sxs-lookup"><span data-stu-id="30128-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="30128-173">La plage et le schéma de partition ont une valeur Int64 uniforme avec la plage complète de clés Int64.</span><span class="sxs-lookup"><span data-stu-id="30128-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="30128-174">Concepts de partition Service Fabric pour les acteurs</span><span class="sxs-lookup"><span data-stu-id="30128-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="30128-175">Les services d’acteur sont des services partitionnés avec état.</span><span class="sxs-lookup"><span data-stu-id="30128-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="30128-176">Chaque partition d’un service d’acteur contient un ensemble d’acteurs.</span><span class="sxs-lookup"><span data-stu-id="30128-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="30128-177">Les partitions de service sont automatiquement distribuées sur plusieurs nœuds dans Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="30128-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="30128-178">Par conséquent, les instances d’acteur sont distribuées.</span><span class="sxs-lookup"><span data-stu-id="30128-178">Actor instances are distributed as a result.</span></span>

![Partitionnement et distribution d’acteur][5]

<span data-ttu-id="30128-180">Vous pouvez créer des Reliable Services avec différents schémas de partition et plages de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="30128-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="30128-181">Le service d’acteur utilise le schéma de partitionnement Int64 avec la plage complète de clés Int64 pour mapper des acteurs à des partitions.</span><span class="sxs-lookup"><span data-stu-id="30128-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="30128-182">ID d’acteur</span><span class="sxs-lookup"><span data-stu-id="30128-182">Actor ID</span></span>
<span data-ttu-id="30128-183">Chaque acteur créé dans le service possède un ID unique associé, représenté par la classe `ActorId` .</span><span class="sxs-lookup"><span data-stu-id="30128-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="30128-184">`ActorId` est une valeur d’ID opaque qui peut être utilisée pour une distribution uniforme des acteurs sur les partitions de service en générant des identifiants aléatoires :</span><span class="sxs-lookup"><span data-stu-id="30128-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="30128-185">Chaque `ActorId` est haché en Int64.</span><span class="sxs-lookup"><span data-stu-id="30128-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="30128-186">C’est pourquoi le service d’acteur doit utiliser un schéma de partitionnement Int64 avec la plage complète de clés Int64.</span><span class="sxs-lookup"><span data-stu-id="30128-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="30128-187">Toutefois, vous pouvez utiliser des valeurs d’ID personnalisées pour un `ActorID`, dont des GUID / UUID, des chaînes et des valeurs Int64s.</span><span class="sxs-lookup"><span data-stu-id="30128-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="30128-188">Lorsque vous utilisez des chaînes et des GUID / UUID, les valeurs sont hachées en Int64.</span><span class="sxs-lookup"><span data-stu-id="30128-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="30128-189">Toutefois, lorsque vous fournissez explicitement une valeur Int64 à un `ActorId`, la valeur Int64 mappe directement à une partition sans hachage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="30128-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="30128-190">Vous pouvez utiliser cette technique pour contrôler la partition dans laquelle les acteurs sont placés.</span><span class="sxs-lookup"><span data-stu-id="30128-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30128-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30128-191">Next steps</span></span>
* [<span data-ttu-id="30128-192">Gestion des états d’acteur</span><span class="sxs-lookup"><span data-stu-id="30128-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="30128-193">Cycle de vie des acteurs et Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="30128-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="30128-194">Documentation de référence de l’API Actors</span><span class="sxs-lookup"><span data-stu-id="30128-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="30128-195">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="30128-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="30128-196">Exemple de code Java</span><span class="sxs-lookup"><span data-stu-id="30128-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
