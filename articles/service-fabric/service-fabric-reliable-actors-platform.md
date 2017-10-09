---
title: aaaReliable acteurs sur Service Fabric | Documents Microsoft
description: "Décrit comment Reliable Actors sont posés en couches sur des Services fiables et utiliser les fonctionnalités de hello de plateforme de Service Fabric hello."
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
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="f3600-103">Comment Reliable Actors utiliser hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3600-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="f3600-104">Cet article explique le fonctionnement des acteurs fiable sur la plateforme Azure Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="f3600-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="f3600-105">Reliable Actors s’exécutent dans une infrastructure qui est hébergée dans une implémentation d’un service fiable avec état appelée hello *service d’acteur*.</span><span class="sxs-lookup"><span data-stu-id="f3600-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="f3600-106">service d’acteur Hello contient tous les cycle de vie hello composants nécessaires toomanage hello et un message destiné à votre acteurs :</span><span class="sxs-lookup"><span data-stu-id="f3600-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="f3600-107">Hello acteur Runtime gère le cycle de vie, le garbage collection et applique l’accès de thread unique.</span><span class="sxs-lookup"><span data-stu-id="f3600-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="f3600-108">Un écouteur de la communication à distance d’acteur service accepte tooactors des appels de l’accès à distance et les envoie instance de tooa répartiteur tooroute toohello acteur approprié.</span><span class="sxs-lookup"><span data-stu-id="f3600-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="f3600-109">Hello fournisseur d’état acteur encapsule les fournisseurs d’état (par exemple, le fournisseur d’état de Collections fiable hello) et fournit un adaptateur pour la gestion d’état acteur.</span><span class="sxs-lookup"><span data-stu-id="f3600-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="f3600-110">Ces framework Reliable Actor de composants forment hello.</span><span class="sxs-lookup"><span data-stu-id="f3600-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="f3600-111">Couches de service</span><span class="sxs-lookup"><span data-stu-id="f3600-111">Service layering</span></span>
<span data-ttu-id="f3600-112">Étant donné que le service d’acteur hello lui-même est un service fiable, tous les hello [modèle d’application](service-fabric-application-model.md), cycle de vie, [empaquetage](service-fabric-package-apps.md), [déploiement](service-fabric-deploy-remove-applications.md), mettre à niveau et mise à l’échelle des concepts de Services fiables appliquent hello même tooactor façon dont les services.</span><span class="sxs-lookup"><span data-stu-id="f3600-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![Superposition de service d’acteur][1]

<span data-ttu-id="f3600-114">Hello diagramme précédent montre relation hello entre les infrastructures d’application Service Fabric hello et code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f3600-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="f3600-115">Éléments bleus représentent l’infrastructure d’application des Services fiables hello, orange représente le framework d’acteur fiable hello et verte représente le code utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f3600-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="f3600-116">Dans les Services fiables, votre service hérite hello `StatefulService` classe.</span><span class="sxs-lookup"><span data-stu-id="f3600-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="f3600-117">Cette classe est dérivée de `StatefulServiceBase` (ou `StatelessService` pour les services sans état).</span><span class="sxs-lookup"><span data-stu-id="f3600-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="f3600-118">Dans Reliable Actors, vous utilisez service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="f3600-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="f3600-119">service d’acteur Hello est une implémentation différente de hello `StatefulServiceBase` classe ce modèle d’acteur hello implémente où votre acteurs exécutent.</span><span class="sxs-lookup"><span data-stu-id="f3600-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="f3600-120">Étant donné que le service d’acteur hello lui-même est simplement une implémentation de `StatefulServiceBase`, vous pouvez écrire votre propre service qui dérive de `ActorService` et fonctionnalités de niveau de service implémentent hello même façon que lors de l’héritage `StatefulService`, telles que :</span><span class="sxs-lookup"><span data-stu-id="f3600-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="f3600-121">Sauvegarde et restauration du service.</span><span class="sxs-lookup"><span data-stu-id="f3600-121">Service backup and restore.</span></span>
* <span data-ttu-id="f3600-122">Fonctionnalité partagée par tous les acteurs. Par exemple, un disjoncteur.</span><span class="sxs-lookup"><span data-stu-id="f3600-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="f3600-123">Appels de procédure distante sur le service d’acteur hello proprement dit et sur chaque acteur individuel.</span><span class="sxs-lookup"><span data-stu-id="f3600-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="f3600-124">Actuellement, les services avec état ne sont pas pris en charge par Java / Linux.</span><span class="sxs-lookup"><span data-stu-id="f3600-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="f3600-125">À l’aide du service d’acteur hello</span><span class="sxs-lookup"><span data-stu-id="f3600-125">Using hello actor service</span></span>
<span data-ttu-id="f3600-126">Les instances d’acteur ont service d’acteur toohello accès dans lequel ils sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f3600-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="f3600-127">Via le service d’acteur hello, instances de l’acteur peuvent obtenir par programmation le contexte de service hello.</span><span class="sxs-lookup"><span data-stu-id="f3600-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="f3600-128">contexte de service Hello a l’ID de partition hello, nom du service, nom de l’application et autres informations spécifiques à la plateforme de l’infrastructure de Service :</span><span class="sxs-lookup"><span data-stu-id="f3600-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="f3600-129">Comme tous les Services fiables, le service d’acteur hello doit être inscrite avec un type de service dans le runtime du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f3600-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="f3600-130">Pour du service d’acteur de hello toorun vos instances de l’acteur, votre type d’acteur doit également être inscrit dans hello acteur service.</span><span class="sxs-lookup"><span data-stu-id="f3600-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="f3600-131">Hello `ActorRuntime` méthode d’inscription exécute cette tâche pour acteurs.</span><span class="sxs-lookup"><span data-stu-id="f3600-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="f3600-132">Dans le cas le plus simple hello, vous pouvez inscrire simplement votre type d’acteur et service d’acteur hello avec les paramètres par défaut sera utilisé implicitement :</span><span class="sxs-lookup"><span data-stu-id="f3600-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="f3600-133">Vous pouvez également utiliser une expression lambda fournie par service d’acteur hello inscription méthode tooconstruct hello, vous-même.</span><span class="sxs-lookup"><span data-stu-id="f3600-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="f3600-134">Vous pouvez ensuite configurer le service d’acteur hello et construire explicitement vos instances de l’acteur, où vous pouvez injecter un acteur tooyour de dépendances via son constructeur :</span><span class="sxs-lookup"><span data-stu-id="f3600-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="f3600-135">Méthodes du service d’acteur</span><span class="sxs-lookup"><span data-stu-id="f3600-135">Actor service methods</span></span>
<span data-ttu-id="f3600-136">Hello implémente de service d’acteur `IActorService` (c#) ou `ActorService` (Java), qui à son tour implémente `IService` (c#) ou `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="f3600-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="f3600-137">Il s’agit d’interface hello utilisé par la communication à distance des Services fiables, ce qui autorise les appels de procédure distante sur les méthodes de service.</span><span class="sxs-lookup"><span data-stu-id="f3600-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="f3600-138">Elle contient des méthodes de niveau de service qui peuvent être appelées à distance via la communication à distance des services.</span><span class="sxs-lookup"><span data-stu-id="f3600-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="f3600-139">Énumération des acteurs</span><span class="sxs-lookup"><span data-stu-id="f3600-139">Enumerating actors</span></span>
<span data-ttu-id="f3600-140">service d’acteur Hello permet à un client tooenumerate des métadonnées sur des intervenants hello qui héberge le service de hello.</span><span class="sxs-lookup"><span data-stu-id="f3600-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="f3600-141">Étant donné que le service d’acteur hello est un service avec état partitionné, l’énumération est effectuée par partition.</span><span class="sxs-lookup"><span data-stu-id="f3600-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="f3600-142">Étant donné que chaque partition peut contenir de nombreux acteurs, énumération de hello est retournée en tant qu’ensemble de résultats paginés.</span><span class="sxs-lookup"><span data-stu-id="f3600-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="f3600-143">pages de Hello sont boucle jusqu'à ce que toutes les pages sont lues.</span><span class="sxs-lookup"><span data-stu-id="f3600-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="f3600-144">Hello suivant montre l’exemple de comment toocreate une liste de tous les intervenants actives dans une partition d’un service d’acteur :</span><span class="sxs-lookup"><span data-stu-id="f3600-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="f3600-145">Suppression d’acteurs</span><span class="sxs-lookup"><span data-stu-id="f3600-145">Deleting actors</span></span>
<span data-ttu-id="f3600-146">service d’acteur Hello fournit également une fonction de suppression des acteurs :</span><span class="sxs-lookup"><span data-stu-id="f3600-146">hello actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="f3600-147">Pour plus d’informations sur la suppression des acteurs et leur état, consultez hello [documentation du cycle de vie acteur](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="f3600-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="f3600-148">Service d’acteur personnalisé</span><span class="sxs-lookup"><span data-stu-id="f3600-148">Custom actor service</span></span>
<span data-ttu-id="f3600-149">À l’aide de lambda de hello acteur d’inscription, vous pouvez inscrire votre propre service d’acteur personnalisée qui dérive de `ActorService` (c#) et `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="f3600-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="f3600-150">Dans ce service d’acteur personnalisé, vous pouvez implémenter vos propres fonctionnalités de niveau de service en écrivant une classe de service qui hérite de `ActorService` (c#) ou `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="f3600-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="f3600-151">Un service d’acteur personnalisée hérite de toutes les fonctionnalités de runtime acteur hello de `ActorService` (c#) ou `FabricActorService` (Java) et peut être utilisé tooimplement vos propres méthodes de service.</span><span class="sxs-lookup"><span data-stu-id="f3600-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="f3600-152">Implémentation d’une sauvegarde et restauration d’acteur</span><span class="sxs-lookup"><span data-stu-id="f3600-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="f3600-153">Dans l’exemple suivant de hello, service d’acteur personnalisée hello expose un tooback (méthode), les données d’acteur en tirant parti de l’écouteur de la communication à distance hello déjà présente dans `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="f3600-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

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
           // store hello contents of backupInfo.Directory
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
           // store hello contents of backupInfo.Directory
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


<span data-ttu-id="f3600-154">Dans cet exemple, `IMyActorService` est un contrat de communication à distance qui implémente `IService` (C#) et `Service` (Java) et est ensuite implémenté par `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="f3600-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="f3600-155">En ajoutant ce contrat la communication à distance, les méthodes sur `IMyActorService` sont désormais également disponibles tooa client en créant un proxy de communication à distance via `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="f3600-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="f3600-156">Modèle d'application</span><span class="sxs-lookup"><span data-stu-id="f3600-156">Application model</span></span>
<span data-ttu-id="f3600-157">Services d’acteur étant des Services fiables, modèle d’application hello est hello identiques.</span><span class="sxs-lookup"><span data-stu-id="f3600-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="f3600-158">Toutefois, des outils de génération hello acteur framework génèrent des fichiers de modèle d’application hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="f3600-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="f3600-159">Manifeste de service</span><span class="sxs-lookup"><span data-stu-id="f3600-159">Service manifest</span></span>
<span data-ttu-id="f3600-160">outils de génération de framework Hello acteur génèrent automatiquement le contenu hello du fichier de ServiceManifest.xml de votre service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="f3600-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="f3600-161">Ce fichier inclut :</span><span class="sxs-lookup"><span data-stu-id="f3600-161">This file includes:</span></span>

* <span data-ttu-id="f3600-162">Le type de service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="f3600-162">Actor service type.</span></span> <span data-ttu-id="f3600-163">nom de type Hello est généré en fonction du nom du projet de votre acteur.</span><span class="sxs-lookup"><span data-stu-id="f3600-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="f3600-164">En fonction de l’attribut de persistance hello sur votre acteur, hello HasPersistedState indicateur est également définie en conséquence.</span><span class="sxs-lookup"><span data-stu-id="f3600-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="f3600-165">le package de code ;</span><span class="sxs-lookup"><span data-stu-id="f3600-165">Code package.</span></span>
* <span data-ttu-id="f3600-166">le package de configuration ;</span><span class="sxs-lookup"><span data-stu-id="f3600-166">Config package.</span></span>
* <span data-ttu-id="f3600-167">les ressources et points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="f3600-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="f3600-168">Manifeste d’application</span><span class="sxs-lookup"><span data-stu-id="f3600-168">Application manifest</span></span>
<span data-ttu-id="f3600-169">outils de génération de framework Hello acteur créent automatiquement une définition de service par défaut pour votre service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="f3600-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="f3600-170">outils de génération Hello remplissent les propriétés de service par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="f3600-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="f3600-171">Nombre de jeu de réplica est déterminé par l’attribut persistance hello sur votre acteur.</span><span class="sxs-lookup"><span data-stu-id="f3600-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="f3600-172">Chaque attribut de persistance hello heure sur votre acteur est modifié, nombre de jeu de réplica hello dans la définition de service par défaut hello est réinitialisé en conséquence.</span><span class="sxs-lookup"><span data-stu-id="f3600-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="f3600-173">Plage et le schéma de partition sont définies tooUniform Int64 avec complète plage de clés Int64 hello.</span><span class="sxs-lookup"><span data-stu-id="f3600-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="f3600-174">Concepts de partition Service Fabric pour les acteurs</span><span class="sxs-lookup"><span data-stu-id="f3600-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="f3600-175">Les services d’acteur sont des services partitionnés avec état.</span><span class="sxs-lookup"><span data-stu-id="f3600-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="f3600-176">Chaque partition d’un service d’acteur contient un ensemble d’acteurs.</span><span class="sxs-lookup"><span data-stu-id="f3600-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="f3600-177">Les partitions de service sont automatiquement distribuées sur plusieurs nœuds dans Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f3600-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="f3600-178">Par conséquent, les instances d’acteur sont distribuées.</span><span class="sxs-lookup"><span data-stu-id="f3600-178">Actor instances are distributed as a result.</span></span>

![Partitionnement et distribution d’acteur][5]

<span data-ttu-id="f3600-180">Vous pouvez créer des Reliable Services avec différents schémas de partition et plages de clés de partition.</span><span class="sxs-lookup"><span data-stu-id="f3600-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="f3600-181">service d’acteur Hello utilise schéma de partitionnement hello Int64 avec toomap acteurs toopartitions hello complètes Int64 plage de clés.</span><span class="sxs-lookup"><span data-stu-id="f3600-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="f3600-182">ID d’acteur</span><span class="sxs-lookup"><span data-stu-id="f3600-182">Actor ID</span></span>
<span data-ttu-id="f3600-183">Chaque acteur qui est créé dans le service hello a un ID unique associé, représenté par hello `ActorId` classe.</span><span class="sxs-lookup"><span data-stu-id="f3600-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="f3600-184">`ActorId`est une valeur d’ID opaque pouvant servir pour une distribution uniforme des acteurs sur plusieurs partitions de service hello en générant des identifiants aléatoires :</span><span class="sxs-lookup"><span data-stu-id="f3600-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="f3600-185">Chaque `ActorId` est haché tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="f3600-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="f3600-186">C’est pourquoi le service d’acteur hello doit utiliser un schéma de partitionnement de Int64 avec complète plage de clés Int64 hello.</span><span class="sxs-lookup"><span data-stu-id="f3600-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="f3600-187">Toutefois, vous pouvez utiliser des valeurs d’ID personnalisées pour un `ActorID`, dont des GUID / UUID, des chaînes et des valeurs Int64s.</span><span class="sxs-lookup"><span data-stu-id="f3600-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="f3600-188">Lorsque vous utilisez des chaînes et des GUID/UUID, les valeurs hello sont haché tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="f3600-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="f3600-189">Toutefois, lorsque vous êtes en fournissant explicitement un tooan Int64 `ActorId`, hello Int64 mappera directement tooa partition sans davantage de hachage.</span><span class="sxs-lookup"><span data-stu-id="f3600-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="f3600-190">Vous pouvez utiliser cette toocontrol technique qui acteurs hello de partition sont placés dans.</span><span class="sxs-lookup"><span data-stu-id="f3600-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3600-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3600-191">Next steps</span></span>
* [<span data-ttu-id="f3600-192">Gestion des états d’acteur</span><span class="sxs-lookup"><span data-stu-id="f3600-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="f3600-193">Cycle de vie des acteurs et Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="f3600-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="f3600-194">Documentation de référence de l’API Actors</span><span class="sxs-lookup"><span data-stu-id="f3600-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="f3600-195">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="f3600-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="f3600-196">Exemple de code Java</span><span class="sxs-lookup"><span data-stu-id="f3600-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
