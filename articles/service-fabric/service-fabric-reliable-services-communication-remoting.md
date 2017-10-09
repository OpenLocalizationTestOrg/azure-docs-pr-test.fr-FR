---
title: "la communication à distance d’aaaService dans l’infrastructure de Service | Documents Microsoft"
description: "La communication à distance de l’infrastructure de service permet aux clients et services toocommunicate avec les services à l’aide d’un appel de procédure distante."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="91fa0-103">Communication à distance des services avec Reliable Services</span><span class="sxs-lookup"><span data-stu-id="91fa0-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="91fa0-104">Pour les services qui ne sont pas liés tooa le protocole de communication particulier ou de la pile, par exemple WebAPI, Windows Communication Foundation (WCF) ou d’autres, le framework de Services fiables hello fournit un tooquickly de mécanisme de communication à distance et facilement configurer l’appel de procédure distante pour les services.</span><span class="sxs-lookup"><span data-stu-id="91fa0-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="91fa0-105">Configuration de la communication à distance sur un service</span><span class="sxs-lookup"><span data-stu-id="91fa0-105">Set up remoting on a service</span></span>
<span data-ttu-id="91fa0-106">La configuration de communication à distance pour un service s'effectue en deux étapes simples :</span><span class="sxs-lookup"><span data-stu-id="91fa0-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="91fa0-107">Créez une interface pour votre tooimplement de service.</span><span class="sxs-lookup"><span data-stu-id="91fa0-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="91fa0-108">Cette interface définit les méthodes hello qui seront disponibles pour un appel de procédure distante sur votre service.</span><span class="sxs-lookup"><span data-stu-id="91fa0-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="91fa0-109">les méthodes Hello doivent être retournant des tâches méthodes asynchrones.</span><span class="sxs-lookup"><span data-stu-id="91fa0-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="91fa0-110">Hello interface doit implémenter `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal qui hello service dispose d’une interface de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="91fa0-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="91fa0-111">Utilisez un écouteur de communication à distance dans votre service.</span><span class="sxs-lookup"><span data-stu-id="91fa0-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="91fa0-112">Il s'agit d'une implémentation `ICommunicationListener` qui fournit des fonctionnalités de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="91fa0-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="91fa0-113">Hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` espace de noms contient une méthode d’extension,`CreateServiceRemotingListener` pour avec et sans état des services qui permettre être utilisé toocreate un écouteur de la communication à distance à l’aide de protocole de transport de la communication à distance par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="91fa0-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="91fa0-114">Remarque : hello `Remoting` espace de noms est disponible comme package nuget distinct appelé`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="91fa0-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="91fa0-115">Par exemple, hello service sans état suivant expose une méthode unique de tooget « Hello World » via un appel de procédure distante.</span><span class="sxs-lookup"><span data-stu-id="91fa0-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="91fa0-116">Hello arguments et hello retournent types dans l’interface de service hello peuvent être des types simples, complexes ou personnalisées, mais ils doivent être sérialisables par hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="91fa0-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="91fa0-117">Méthodes d’appel de service distant</span><span class="sxs-lookup"><span data-stu-id="91fa0-117">Call remote service methods</span></span>
<span data-ttu-id="91fa0-118">Appel de méthodes sur un service à l’aide de pile de communication à distance hello est effectuée à l’aide d’un service de toohello proxy local via hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="91fa0-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="91fa0-119">Hello `ServiceProxy` méthode crée un proxy local à l’aide de hello même interface que hello service implémente.</span><span class="sxs-lookup"><span data-stu-id="91fa0-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="91fa0-120">Avec ce serveur proxy, vous pouvez simplement appeler des méthodes sur les interface hello à distance.</span><span class="sxs-lookup"><span data-stu-id="91fa0-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="91fa0-121">infrastructure de communication à distance Hello propage les exceptions levées au client du service de toohello hello.</span><span class="sxs-lookup"><span data-stu-id="91fa0-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="91fa0-122">Logique, gestion des exceptions au client hello à l’aide de `ServiceProxy` peut gérer directement les exceptions hello service lève une exception.</span><span class="sxs-lookup"><span data-stu-id="91fa0-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="91fa0-123">Durée de vie du proxy du service</span><span class="sxs-lookup"><span data-stu-id="91fa0-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="91fa0-124">Comme la création de proxy de service est une opération légère, l’utilisateur peut en créer autant de fois que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="91fa0-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="91fa0-125">Le proxy de service peut être réutilisé tant que l’utilisateur en a besoin.</span><span class="sxs-lookup"><span data-stu-id="91fa0-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="91fa0-126">Utilisateur peut réutiliser hello proxy même en cas d’Exception.</span><span class="sxs-lookup"><span data-stu-id="91fa0-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="91fa0-127">Chaque ServiceProxy contient intersites client utilisé toosend messages acheminement hello.</span><span class="sxs-lookup"><span data-stu-id="91fa0-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="91fa0-128">Lors de l’appel d’API, nous avons toosee de contrôle interne si le client de communication utilisé est valide.</span><span class="sxs-lookup"><span data-stu-id="91fa0-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="91fa0-129">En fonction de ce résultat, nous recréer client de communication hello.</span><span class="sxs-lookup"><span data-stu-id="91fa0-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="91fa0-130">Par conséquent, les utilisateurs n’avez pas besoin serviceproxy toorecreate en cas d’Exception.</span><span class="sxs-lookup"><span data-stu-id="91fa0-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="91fa0-131">Durée de vie de la fabrique ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="91fa0-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="91fa0-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) est une fabrique qui crée le proxy pour différentes interfaces de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="91fa0-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="91fa0-133">Si vous utilisez l’API ServiceProxy.Create pour la création du proxy, l’infrastructure crée hello singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="91fa0-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="91fa0-134">Il est utile toocreate une manuellement lorsque vous avez besoin de toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) propriétés.</span><span class="sxs-lookup"><span data-stu-id="91fa0-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="91fa0-135">La fabrique est une opération coûteuse.</span><span class="sxs-lookup"><span data-stu-id="91fa0-135">Factory is an expensive operation.</span></span> <span data-ttu-id="91fa0-136">ServiceProxyFactory conserve le cache du client de communication.</span><span class="sxs-lookup"><span data-stu-id="91fa0-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="91fa0-137">Il est recommandé toocache ServiceProxyFactory aussi longtemps que possible.</span><span class="sxs-lookup"><span data-stu-id="91fa0-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="91fa0-138">Gestion des exceptions à distance</span><span class="sxs-lookup"><span data-stu-id="91fa0-138">Remoting Exception Handling</span></span>
<span data-ttu-id="91fa0-139">Tous les hello à distance d’exception levée par l’API de service, sont envoyées toohello précédent client comme AggregateException.</span><span class="sxs-lookup"><span data-stu-id="91fa0-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="91fa0-140">RemoteExceptions doivent être sérialisables DataContract sinon [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) est levée toohello proxy API avec l’erreur de sérialisation hello qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="91fa0-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="91fa0-141">ServiceProxy gère toutes les exceptions de basculement pour la partition de service hello il est créé pour.</span><span class="sxs-lookup"><span data-stu-id="91fa0-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="91fa0-142">Nouveau, il résout les points de terminaison hello si Failover Exceptions(Non-Transient Exceptions) et nouvelles tentatives appel hello avec le point de terminaison correct hello est.</span><span class="sxs-lookup"><span data-stu-id="91fa0-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="91fa0-143">Le nombre de tentatives pour l’exception de basculement est illimité.</span><span class="sxs-lookup"><span data-stu-id="91fa0-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="91fa0-144">En cas de TransientExceptions, il réessaie uniquement appel de hello.</span><span class="sxs-lookup"><span data-stu-id="91fa0-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="91fa0-145">Les paramètres de nouvelle tentative par défaut sont fournis par [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="91fa0-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="91fa0-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Utilisateur peut configurer ces valeurs en passant le constructeur de tooServiceProxyFactory OperationRetrySettings objet.</span><span class="sxs-lookup"><span data-stu-id="91fa0-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91fa0-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="91fa0-147">Next steps</span></span>
* [<span data-ttu-id="91fa0-148">API Web avec OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="91fa0-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="91fa0-149">Communication WCF avec Reliable Services</span><span class="sxs-lookup"><span data-stu-id="91fa0-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="91fa0-150">Sécurisation des communications pour Reliable Services</span><span class="sxs-lookup"><span data-stu-id="91fa0-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
