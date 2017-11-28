---
title: "<span data-ttu-id=\"9c5ac-101\">Communication à distance des services dans Service Fabric | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"9c5ac-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"9c5ac-102\">La communication à distance dans Service Fabric permet aux clients et aux services de communiquer avec les services en utilisant un appel de procédure distante.</span><span class=\"sxs-lookup\"><span data-stu-id=\"9c5ac-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
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
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="9c5ac-103">Communication à distance des services avec Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c5ac-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="9c5ac-104">Pour les services qui ne sont pas liés à une pile ou un protocole de communication particulier, comme WebAPI, Windows Communication Foundation (WCF) ou autres, l’infrastructure Reliable Services fournit un mécanisme de communication à distance pour configurer rapidement et facilement un appel de procédure distante pour les services.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="9c5ac-105">Configuration de la communication à distance sur un service</span><span class="sxs-lookup"><span data-stu-id="9c5ac-105">Set up remoting on a service</span></span>
<span data-ttu-id="9c5ac-106">La configuration de communication à distance pour un service s'effectue en deux étapes simples :</span><span class="sxs-lookup"><span data-stu-id="9c5ac-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="9c5ac-107">Créez une interface pour implémenter votre service.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="9c5ac-108">Cette interface définit les méthodes disponibles pour l'appel de procédure distante sur votre service.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="9c5ac-109">Ces méthodes doivent être des méthodes asynchrones retournant des tâches.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="9c5ac-110">L'interface doit implémenter `Microsoft.ServiceFabric.Services.Remoting.IService` pour signaler que le service dispose d'une interface de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="9c5ac-111">Utilisez un écouteur de communication à distance dans votre service.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="9c5ac-112">Il s'agit d'une implémentation `ICommunicationListener` qui fournit des fonctionnalités de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="9c5ac-113">L’espace de noms `Microsoft.ServiceFabric.Services.Remoting.Runtime` contient une méthode d’extension `CreateServiceRemotingListener` pour les services avec et sans état qui peuvent être utilisés pour créer un écouteur de communication à distance à l’aide du protocole de transport de communication à distance par défaut.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="9c5ac-114">Remarque : L’espace de noms `Remoting` est disponible sous la forme d’un package NuGet distinct appelé `Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="9c5ac-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="9c5ac-115">Par exemple, le service sans état suivant expose une méthode unique pour obtenir « Hello World » sur un appel de procédure distante :</span><span class="sxs-lookup"><span data-stu-id="9c5ac-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="9c5ac-116">Les arguments et les types de retour dans l’interface de service peuvent être de type simple, complexe ou personnalisé, mais ils doivent être sérialisables par l’élément [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).NET.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="9c5ac-117">Méthodes d’appel de service distant</span><span class="sxs-lookup"><span data-stu-id="9c5ac-117">Call remote service methods</span></span>
<span data-ttu-id="9c5ac-118">L’appel de méthodes sur un service à l’aide de la pile de communication à distance est effectué avec un proxy local pour le service via la classe `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` .</span><span class="sxs-lookup"><span data-stu-id="9c5ac-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="9c5ac-119">La méthode `ServiceProxy` crée un proxy local à l’aide de l’interface implémentée par le service.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="9c5ac-120">Avec ce proxy, vous pouvez appeler simplement et à distance des méthodes sur l'interface.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="9c5ac-121">L'infrastructure de communication à distance propage les exceptions levées au niveau du service au client.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="9c5ac-122">Par conséquent, la logique de gestion des exceptions au niveau du client à l’aide de `ServiceProxy` peut directement traiter les exceptions levées par le service.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="9c5ac-123">Durée de vie du proxy du service</span><span class="sxs-lookup"><span data-stu-id="9c5ac-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="9c5ac-124">Comme la création de proxy de service est une opération légère, l’utilisateur peut en créer autant de fois que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="9c5ac-125">Le proxy de service peut être réutilisé tant que l’utilisateur en a besoin.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="9c5ac-126">L’utilisateur peut réutiliser le même proxy en cas d’exception.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="9c5ac-127">Chaque proxy de service contient un client de communication qui permet d’envoyer des messages sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="9c5ac-128">Lors de l’appel de l’API, un contrôle interne vérifie si le client de communication utilisé est valide.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="9c5ac-129">En fonction de ce résultat, nous recréons le client de communication.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="9c5ac-130">Par conséquent, l’utilisateur n’a pas besoin de recréer le proxy de service en cas d’exception.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="9c5ac-131">Durée de vie de la fabrique ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="9c5ac-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="9c5ac-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) est une fabrique qui crée le proxy pour différentes interfaces de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="9c5ac-133">Si vous utilisez l’API ServiceProxy.Create pour la création de proxy, l’infrastructure crée le ServiceProxyFactory singleton.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="9c5ac-134">Il est utile d’en créer un manuellement lorsque vous devez remplacer les propriétés [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory).</span><span class="sxs-lookup"><span data-stu-id="9c5ac-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="9c5ac-135">La fabrique est une opération coûteuse.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-135">Factory is an expensive operation.</span></span> <span data-ttu-id="9c5ac-136">ServiceProxyFactory conserve le cache du client de communication.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="9c5ac-137">Il est recommandé de mettre en cache ServiceProxyFactory aussi longtemps que possible.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="9c5ac-138">Gestion des exceptions à distance</span><span class="sxs-lookup"><span data-stu-id="9c5ac-138">Remoting Exception Handling</span></span>
<span data-ttu-id="9c5ac-139">Toutes les exceptions à distance levées par l’API de service sont envoyées au client en tant que AggregateException.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="9c5ac-140">Les exceptions à distance doivent être des contrats de données sérialisables. Sinon, une exception [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) est envoyée à l’API de proxy en indiquant l’erreur de sérialisation.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="9c5ac-141">Le proxy de service gère toutes les exceptions de basculement pour la partition de service pour laquelle il a été créé.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="9c5ac-142">Il résout à nouveau les points de terminaison s’il existe des exceptions de basculement (non temporaires) et retente l’appel avec le point de terminaison correct.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="9c5ac-143">Le nombre de tentatives pour l’exception de basculement est illimité.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="9c5ac-144">En cas d’exceptions temporaires, il retente uniquement l’appel.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="9c5ac-145">Les paramètres de nouvelle tentative par défaut sont fournis par [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="9c5ac-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="9c5ac-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) L’utilisateur peut configurer ces valeurs en transmettant l’objet OperationRetrySettings au constructeur ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="9c5ac-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c5ac-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9c5ac-147">Next steps</span></span>
* [<span data-ttu-id="9c5ac-148">API Web avec OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c5ac-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="9c5ac-149">Communication WCF avec Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c5ac-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="9c5ac-150">Sécurisation des communications pour Reliable Services</span><span class="sxs-lookup"><span data-stu-id="9c5ac-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
