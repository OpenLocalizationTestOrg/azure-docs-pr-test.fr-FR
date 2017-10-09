---
title: "aaaCreate votre première application de Service Fabric en C# | Documents Microsoft"
description: "Introduction toocreating une application Microsoft Azure Service Fabric avec et sans état des services."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="fae60-103">Prise en main de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="fae60-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fae60-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="fae60-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="fae60-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="fae60-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="fae60-106">Une application Azure Service Fabric contient un ou plusieurs services qui exécutent votre code.</span><span class="sxs-lookup"><span data-stu-id="fae60-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="fae60-107">Ce guide vous montre comment toocreate avec et sans état des applications de Service Fabric avec [des Services fiables](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fae60-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="fae60-108">Cette vidéo Microsoft Virtual Academy montre également comment toocreate un service fiable sans état :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="fae60-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="fae60-109">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="fae60-109">Basic concepts</span></span>
<span data-ttu-id="fae60-110">tooget en main des Services fiables, vous seulement devez toounderstand quelques concepts de base :</span><span class="sxs-lookup"><span data-stu-id="fae60-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="fae60-111">**Type de service** : il s’agit de l’implémentation de votre service.</span><span class="sxs-lookup"><span data-stu-id="fae60-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="fae60-112">Il est défini par la classe hello vous écrivez qui étend `StatelessService` et tout autre code ou les dépendances utilisés ici, avec un nom et un numéro de version.</span><span class="sxs-lookup"><span data-stu-id="fae60-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="fae60-113">**Instance de service nommée**: toorun votre service, vous créez des instances nommées de votre type de service, beaucoup comme vous créez des instances d’objet d’un type de classe.</span><span class="sxs-lookup"><span data-stu-id="fae60-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="fae60-114">Une instance de service a un nom sous forme de hello d’un URI à l’aide de hello « fabric : / « schéma, tel que « fabric : / MyApp/MyService ».</span><span class="sxs-lookup"><span data-stu-id="fae60-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="fae60-115">**Hôte de service**: hello nommé des instances de service que vous créez toorun nécessaire à l’intérieur d’un processus hôte.</span><span class="sxs-lookup"><span data-stu-id="fae60-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="fae60-116">hôte de service Hello est simplement un processus dans lequel les instances de votre service peuvent exécuter.</span><span class="sxs-lookup"><span data-stu-id="fae60-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="fae60-117">**Inscription du service** : l’inscription rassemble tous les éléments.</span><span class="sxs-lookup"><span data-stu-id="fae60-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="fae60-118">Hello service type doit être inscrit avec hello Service Fabric runtime dans un service hôte tooallow Service Fabric toocreate ses instances toorun.</span><span class="sxs-lookup"><span data-stu-id="fae60-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="fae60-119">Création d'un service sans état</span><span class="sxs-lookup"><span data-stu-id="fae60-119">Create a stateless service</span></span>
<span data-ttu-id="fae60-120">Un service sans état est un type de service est actuellement la norme hello dans les applications de cloud.</span><span class="sxs-lookup"><span data-stu-id="fae60-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="fae60-121">Il est considéré comme sans état, car le service hello lui-même ne contienne pas de données qui doit toobe stockées de manière fiable ou hautement disponible.</span><span class="sxs-lookup"><span data-stu-id="fae60-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="fae60-122">Si une instance d’un service sans état est arrêtée, tout son état interne est perdu.</span><span class="sxs-lookup"><span data-stu-id="fae60-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="fae60-123">Dans ce type de service, état doit être persistante tooan magasin externe, telles que les Tables Azure ou d’une base de données SQL, pour qu’il toobe apportées hautement fiable et disponible.</span><span class="sxs-lookup"><span data-stu-id="fae60-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="fae60-124">Lancez Visual Studio 2015 ou Visual Studio 2017 en tant qu’administrateur et créez un projet d’application Service Fabric nommé *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="fae60-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Utilisez toocreate de boîte dialogue hello nouveau projet une nouvelle application de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="fae60-126">Créez ensuite un projet de service sans état nommé *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="fae60-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Dans la deuxième boîte de dialogue hello, créez un projet de service sans état](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="fae60-128">Votre solution contient maintenant deux projets :</span><span class="sxs-lookup"><span data-stu-id="fae60-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="fae60-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="fae60-129">*HelloWorld*.</span></span> <span data-ttu-id="fae60-130">Il s’agit de hello *application* projet qui contient votre *services*.</span><span class="sxs-lookup"><span data-stu-id="fae60-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="fae60-131">Il contient également le manifeste de l’application hello décrivant application hello, ainsi que d’un nombre de scripts PowerShell qui vous aident à toodeploy votre application.</span><span class="sxs-lookup"><span data-stu-id="fae60-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="fae60-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="fae60-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="fae60-133">Il s’agit de projet de service hello.</span><span class="sxs-lookup"><span data-stu-id="fae60-133">This is hello service project.</span></span> <span data-ttu-id="fae60-134">Il contient d’implémentation de service sans état hello.</span><span class="sxs-lookup"><span data-stu-id="fae60-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="fae60-135">Implémenter le service de hello</span><span class="sxs-lookup"><span data-stu-id="fae60-135">Implement hello service</span></span>
<span data-ttu-id="fae60-136">Ouvrez hello **HelloWorldStateless.cs** fichier dans le projet de service hello.</span><span class="sxs-lookup"><span data-stu-id="fae60-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="fae60-137">Dans Service Fabric, un service peut exécuter n’importe quelle logique métier.</span><span class="sxs-lookup"><span data-stu-id="fae60-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="fae60-138">API de service Hello fournit deux points d’entrée pour votre code :</span><span class="sxs-lookup"><span data-stu-id="fae60-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="fae60-139">Une méthode de point d’entrée de durée indéterminée appelée *RunAsync*avec laquelle vous pouvez commencer l’exécution de toute charge de travail, y compris les charges de travail de calcul de longue durée.</span><span class="sxs-lookup"><span data-stu-id="fae60-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="fae60-140">Un point d’entrée de communication où vous pouvez connecter votre pile de communication, notamment ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="fae60-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="fae60-141">C’est là que vous pouvez commencer à recevoir des demandes des utilisateurs et des autres services.</span><span class="sxs-lookup"><span data-stu-id="fae60-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="fae60-142">Dans ce didacticiel, nous allons nous concentrer sur hello `RunAsync()` méthode point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="fae60-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="fae60-143">C’est là que vous pouvez commencer immédiatement à exécuter votre code.</span><span class="sxs-lookup"><span data-stu-id="fae60-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="fae60-144">modèle de projet Hello inclut un exemple d’implémentation de `RunAsync()` qui incrémente un compteur propagée.</span><span class="sxs-lookup"><span data-stu-id="fae60-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="fae60-145">Pour plus d’informations sur la façon dont la pile toowork avec une communication, consultez [services API Web du Service Fabric avec OWIN auto-hébergement](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="fae60-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="fae60-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="fae60-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="fae60-147">plateforme de Hello appelle cette méthode lorsqu’une instance d’un service est tooexecute endroit et est prêt.</span><span class="sxs-lookup"><span data-stu-id="fae60-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="fae60-148">Pour un service sans état, cela signifie simplement lors de l’instance de service hello est ouverte.</span><span class="sxs-lookup"><span data-stu-id="fae60-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="fae60-149">Un jeton d’annulation est fourni toocoordinate lorsque votre instance de service doit toobe fermé.</span><span class="sxs-lookup"><span data-stu-id="fae60-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="fae60-150">Dans l’infrastructure de Service, ce cycle d’ouverture/fermeture d’une instance de service peut se produire plusieurs fois sur la durée de vie hello du service de hello dans sa globalité.</span><span class="sxs-lookup"><span data-stu-id="fae60-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="fae60-151">Il existe diverses raisons à cela, notamment :</span><span class="sxs-lookup"><span data-stu-id="fae60-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="fae60-152">système de Hello déplace vos instances de service pour l’équilibrage des ressources.</span><span class="sxs-lookup"><span data-stu-id="fae60-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="fae60-153">Des erreurs surviennent dans votre code.</span><span class="sxs-lookup"><span data-stu-id="fae60-153">Faults occur in your code.</span></span>
* <span data-ttu-id="fae60-154">application Hello ou système est mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="fae60-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="fae60-155">matériel sous-jacent de Hello connaît une panne.</span><span class="sxs-lookup"><span data-stu-id="fae60-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="fae60-156">Cette orchestration est gérée par hello système tookeep votre service hautement disponible et correctement à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="fae60-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="fae60-157">`RunAsync()` ne doit pas se bloquer de façon synchrone.</span><span class="sxs-lookup"><span data-stu-id="fae60-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="fae60-158">Votre implémentation de RunAsync doit retourner une tâche ou await sur n’importe quel toocontinue d’exécution des opérations longues ou blocage tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="fae60-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="fae60-159">Remarque Bonjour `while(true)` boucle dans l’exemple précédent hello, qui retourne une tâche `await Task.Delay()` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="fae60-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="fae60-160">Si votre charge de travail doit se bloquer de façon synchrone, vous devez planifier une tâche avec `Task.Run()` dans votre implémentation de `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="fae60-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="fae60-161">L’annulation de votre charge de travail est un effort conjoint orchestré par hello fourni le jeton d’annulation.</span><span class="sxs-lookup"><span data-stu-id="fae60-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="fae60-162">système de Hello attend votre tooend tâche (par la réussite, l’annulation ou erreur) avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="fae60-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="fae60-163">Il est important toohonor hello annulation jeton, terminer un travail et quitter `RunAsync()` aussi rapidement que possible lorsque le système de hello demande l’annulation.</span><span class="sxs-lookup"><span data-stu-id="fae60-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="fae60-164">Dans cet exemple de service sans état, nombre de hello est stocké dans une variable locale.</span><span class="sxs-lookup"><span data-stu-id="fae60-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="fae60-165">Mais comme il s’agit d’un service sans état, valeur hello stockée existe uniquement pour hello en cours du cycle de vie de son instance de service.</span><span class="sxs-lookup"><span data-stu-id="fae60-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="fae60-166">Lorsque le service de hello déplace ou redémarre, la valeur de hello est perdue.</span><span class="sxs-lookup"><span data-stu-id="fae60-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="fae60-167">Création d'un service avec état</span><span class="sxs-lookup"><span data-stu-id="fae60-167">Create a stateful service</span></span>
<span data-ttu-id="fae60-168">Service Fabric introduit un nouveau type de service qui est avec état.</span><span class="sxs-lookup"><span data-stu-id="fae60-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="fae60-169">Un service avec état permettre conserver l’état fiable dans service hello lui-même, colocalisé avec le code hello qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="fae60-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="fae60-170">État est hautement disponible par l’infrastructure de Service sans confirmation hello besoin toopersist tooan externe le magasin d’état.</span><span class="sxs-lookup"><span data-stu-id="fae60-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="fae60-171">tooconvert une valeur de compteur de toohighly sans état disponible et permanente, même lorsque le service de hello déplace ou redémarre, vous devez un service avec état.</span><span class="sxs-lookup"><span data-stu-id="fae60-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="fae60-172">Dans hello même *HelloWorld* application, vous pouvez ajouter un nouveau service en cliquant sur les références de Services hello dans le projet d’application hello et en sélectionnant **Ajouter -> nouveau Service Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="fae60-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Ajouter un tooyour service application Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="fae60-174">Sélectionnez **Service avec état** et nommez-le *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="fae60-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="fae60-175">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="fae60-175">Click **OK**.</span></span>

![Utilisez toocreate de boîte dialogue hello nouveau projet un nouveau service avec état Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="fae60-177">Votre application devez maintenant avoir deux services : hello service sans état *HelloWorldStateless* et un service avec état hello *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="fae60-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="fae60-178">Un service avec état a hello même points d’entrée comme un service sans état.</span><span class="sxs-lookup"><span data-stu-id="fae60-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="fae60-179">Hello principale différence est la disponibilité de hello d’un *fournisseur d’état* qui peuvent stocker l’état fiable.</span><span class="sxs-lookup"><span data-stu-id="fae60-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="fae60-180">L’infrastructure de service est fourni avec une implémentation de fournisseur d’état appelée [Collections fiable](service-fabric-reliable-services-reliable-collections.md), ce qui vous permet de créer des structures de données répliquées via hello fiable Gestionnaire d’état.</span><span class="sxs-lookup"><span data-stu-id="fae60-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="fae60-181">Un Reliable Service avec état utilise ce fournisseur d’état par défaut.</span><span class="sxs-lookup"><span data-stu-id="fae60-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="fae60-182">Ouvrez **HelloWorldStateful.cs** dans *HelloWorldStateful*, qui contient hello RunAsync méthode :</span><span class="sxs-lookup"><span data-stu-id="fae60-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="fae60-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="fae60-183">RunAsync</span></span>
<span data-ttu-id="fae60-184">`RunAsync()` fonctionne de la même façon dans les services avec ou sans état.</span><span class="sxs-lookup"><span data-stu-id="fae60-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="fae60-185">Toutefois, dans un service avec état, plateforme de hello exécute une tâche supplémentaire de votre part avant d’exécuter `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="fae60-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="fae60-186">Ce travail peut notamment s’assurer de ce gestionnaire d’état fiable hello et fiable de Collections sont toouse prêt.</span><span class="sxs-lookup"><span data-stu-id="fae60-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="fae60-187">Fiable des Collections et hello fiable Gestionnaire d’état</span><span class="sxs-lookup"><span data-stu-id="fae60-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="fae60-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) est une implémentation de dictionnaire qui vous permet de stocker l’état de tooreliably dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="fae60-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="fae60-189">Avec l’infrastructure de Service et les Collections fiable, vous pouvez stocker des données directement dans votre service sans avoir besoin de hello pour un magasin persistant externe.</span><span class="sxs-lookup"><span data-stu-id="fae60-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="fae60-190">Les Reliable Collections rendent vos données hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="fae60-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="fae60-191">Pour ce faire, Service Fabric crée et gère plusieurs *réplicas* de votre service pour vous.</span><span class="sxs-lookup"><span data-stu-id="fae60-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="fae60-192">Il fournit également une API qui résume les complexités hello éloignée de la gestion de ces réplicas et les transitions d’état.</span><span class="sxs-lookup"><span data-stu-id="fae60-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="fae60-193">Les collections fiables peuvent stocker n’importe quel type .NET, y compris vos types personnalisés, avec quelques inconvénients :</span><span class="sxs-lookup"><span data-stu-id="fae60-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="fae60-194">Service Fabric rend votre état hautement disponible par *réplication* stockage de vos données toolocal disque l’état entre les nœuds et fiable sur chaque réplica.</span><span class="sxs-lookup"><span data-stu-id="fae60-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="fae60-195">Cela signifie que tout ce qui est stocké dans les Reliable Collections doit être *sérialisable*.</span><span class="sxs-lookup"><span data-stu-id="fae60-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="fae60-196">Par défaut, les Collections fiables utilisent [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) pour la sérialisation, il est donc important toomake assurer que vos types sont [pris en charge par le sérialiseur de contrat de données de hello](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) lorsque vous utilisez la valeur par défaut de hello sérialiseur.</span><span class="sxs-lookup"><span data-stu-id="fae60-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="fae60-197">Les objets sont répliqués à des fins de haute disponibilité quand vous envoyez des transactions sur des collections fiables.</span><span class="sxs-lookup"><span data-stu-id="fae60-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="fae60-198">Les objets stockés dans les collections fiables sont conservés dans la mémoire locale de votre service.</span><span class="sxs-lookup"><span data-stu-id="fae60-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="fae60-199">Cela signifie que vous disposez d’un objet de toohello référence locale.</span><span class="sxs-lookup"><span data-stu-id="fae60-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="fae60-200">Il est important que vous mute pas les instances locales de ces objets sans effectuer une opération de mise à jour de collection fiable de hello dans une transaction.</span><span class="sxs-lookup"><span data-stu-id="fae60-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="fae60-201">Il s’agit, car les instances de toolocal de modifications d’objets ne seront pas répliquées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="fae60-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="fae60-202">Vous devez Réinsérez les objet hello dans le dictionnaire de hello ou utilisez une des hello *mettre à jour* méthodes sur le dictionnaire de hello.</span><span class="sxs-lookup"><span data-stu-id="fae60-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="fae60-203">Hello Gestionnaire d’état fiable gère les Collections fiable pour vous.</span><span class="sxs-lookup"><span data-stu-id="fae60-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="fae60-204">Vous pouvez simplement demander hello fiable Gestionnaire d’état pour un regroupement fiable par nom à tout moment et en tout lieu dans votre service.</span><span class="sxs-lookup"><span data-stu-id="fae60-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="fae60-205">Hello fiable Gestionnaire d’état permet de s’assurer que vous obtenez une référence arrière.</span><span class="sxs-lookup"><span data-stu-id="fae60-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="fae60-206">Nous ne recommandé d’enregistrer les références d’instances de collection tooreliable dans les variables de membre de classe ou de propriétés.</span><span class="sxs-lookup"><span data-stu-id="fae60-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="fae60-207">Une attention particulière doit prendre tooensure hello référence est définie tooan instance à tout moment dans le cycle de vie hello service.</span><span class="sxs-lookup"><span data-stu-id="fae60-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="fae60-208">Hello Gestionnaire d’état fiable gère ce travail pour vous, et il est optimisé pour les visites de répétitions.</span><span class="sxs-lookup"><span data-stu-id="fae60-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="fae60-209">Opérations transactionnelles et asynchrones</span><span class="sxs-lookup"><span data-stu-id="fae60-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="fae60-210">Collections fiables possèdent de nombreuses hello mêmes opérations que leurs `System.Collections.Generic` et `System.Collections.Concurrent` équivalents, excepté LINQ.</span><span class="sxs-lookup"><span data-stu-id="fae60-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="fae60-211">Les opérations sur les Reliable Collections sont asynchrones.</span><span class="sxs-lookup"><span data-stu-id="fae60-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="fae60-212">Il s’agit, car les opérations d’écriture avec des Collections fiable effectuer tooreplicate d’opérations d’e/s et rendre persistantes des données toodisk.</span><span class="sxs-lookup"><span data-stu-id="fae60-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="fae60-213">Les opérations des Reliable Collections sont *transactionnelles*. Ainsi, vous pouvez conserver un état cohérent entre plusieurs Reliable Collections et opérations.</span><span class="sxs-lookup"><span data-stu-id="fae60-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="fae60-214">Par exemple, vous pouvez enlever un élément de travail à partir d’une file d’attente fiable, effectuer une opération sur lui et enregistrer le résultat de hello dans un dictionnaire fiable, toutes les tâches dans une transaction unique.</span><span class="sxs-lookup"><span data-stu-id="fae60-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="fae60-215">Il est considéré comme une opération atomique, et elle garantit que toute l’opération hello réussira ou annule toute l’opération hello.</span><span class="sxs-lookup"><span data-stu-id="fae60-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="fae60-216">Si une erreur se produit une fois que vous enlever les éléments hello mais avant d’enregistrer le résultat de hello, hello toute transaction est annulée et l’élément hello conserve dans la file d’attente hello pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="fae60-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="fae60-217">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="fae60-217">Run hello application</span></span>
<span data-ttu-id="fae60-218">Nous renvoyons maintenant toohello *HelloWorld* application.</span><span class="sxs-lookup"><span data-stu-id="fae60-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="fae60-219">Vous pouvez désormais générer et déployer vos services.</span><span class="sxs-lookup"><span data-stu-id="fae60-219">You can now build and deploy your services.</span></span> <span data-ttu-id="fae60-220">Lorsque vous appuyez sur **F5**, votre application sera cluster local de tooyour générées et déployées.</span><span class="sxs-lookup"><span data-stu-id="fae60-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="fae60-221">Après le démarrage en cours d’exécution des services hello, vous pouvez afficher les événements de suivi d’événements pour Windows (ETW) hello généré dans un **des événements de Diagnostic** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="fae60-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="fae60-222">Notez que les événements hello affichés sont à partir d’un service sans état hello et un service avec état dans une application hello hello.</span><span class="sxs-lookup"><span data-stu-id="fae60-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="fae60-223">Vous pouvez interrompre le flux de données hello en cliquant sur hello **suspendre** bouton.</span><span class="sxs-lookup"><span data-stu-id="fae60-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="fae60-224">Vous pouvez ensuite examiner les détails hello d’un message en développant ce message.</span><span class="sxs-lookup"><span data-stu-id="fae60-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="fae60-225">Avant d’exécuter application hello, assurez-vous que vous disposez d’un cluster de développement local en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fae60-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="fae60-226">Extraire hello [mise en route](service-fabric-get-started.md) pour plus d’informations sur la configuration de votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="fae60-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Afficher les événements de diagnostic dans Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="fae60-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fae60-228">Next steps</span></span>
[<span data-ttu-id="fae60-229">Déboguer votre application Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fae60-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="fae60-230">Prise en main : services de l’API Web Service Fabric avec auto-hébergement OWIN</span><span class="sxs-lookup"><span data-stu-id="fae60-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="fae60-231">En savoir plus sur les Collections fiables</span><span class="sxs-lookup"><span data-stu-id="fae60-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="fae60-232">Déployer une application</span><span class="sxs-lookup"><span data-stu-id="fae60-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="fae60-233">Mise à niveau de l’application</span><span class="sxs-lookup"><span data-stu-id="fae60-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="fae60-234">Référence du développeur pour les services fiables</span><span class="sxs-lookup"><span data-stu-id="fae60-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

