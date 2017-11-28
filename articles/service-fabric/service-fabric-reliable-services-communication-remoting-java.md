---
title: "Communication à distance des services dans Azure Service Fabric | Microsoft Docs"
description: "La communication à distance dans Service Fabric permet aux clients et aux services de communiquer avec les services en utilisant un appel de procédure distante."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: dc4a362b5737bb424ca2c196c85f4c51b6ee5e30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="6a650-103">Communication à distance des services avec Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6a650-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a650-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="6a650-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="6a650-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="6a650-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="6a650-106">L’infrastructure Reliable Services fournit un mécanisme de communication à distance pour définir rapidement et facilement un appel de procédure distante pour des services.</span><span class="sxs-lookup"><span data-stu-id="6a650-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="6a650-107">Configuration de la communication à distance sur un service</span><span class="sxs-lookup"><span data-stu-id="6a650-107">Set up remoting on a service</span></span>
<span data-ttu-id="6a650-108">La configuration de communication à distance pour un service s'effectue en deux étapes simples :</span><span class="sxs-lookup"><span data-stu-id="6a650-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="6a650-109">Créez une interface pour implémenter votre service.</span><span class="sxs-lookup"><span data-stu-id="6a650-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="6a650-110">Cette interface définit les méthodes disponibles pour un appel de procédure distante sur votre service.</span><span class="sxs-lookup"><span data-stu-id="6a650-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="6a650-111">Ces méthodes doivent être des méthodes asynchrones retournant des tâches.</span><span class="sxs-lookup"><span data-stu-id="6a650-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="6a650-112">L'interface doit implémenter `microsoft.serviceFabric.services.remoting.Service` pour signaler que le service dispose d'une interface de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="6a650-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="6a650-113">Utilisez un écouteur de communication à distance dans votre service.</span><span class="sxs-lookup"><span data-stu-id="6a650-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="6a650-114">Il s'agit d'une implémentation `CommunicationListener` qui fournit des fonctionnalités de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="6a650-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="6a650-115">`FabricTransportServiceRemotingListener` peut être utilisé pour créer un écouteur de communication à distance à l’aide du protocole de transport de communication à distance par défaut.</span><span class="sxs-lookup"><span data-stu-id="6a650-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="6a650-116">Par exemple, le service sans état suivant expose une méthode unique pour obtenir « Hello World » sur un appel de procédure distante :</span><span class="sxs-lookup"><span data-stu-id="6a650-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="6a650-117">Les arguments et les types de retour dans l’interface du service peuvent être de type simple, complexe ou personnalisé, mais ils doivent être sérialisables.</span><span class="sxs-lookup"><span data-stu-id="6a650-117">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="6a650-118">Méthodes d’appel de service distant</span><span class="sxs-lookup"><span data-stu-id="6a650-118">Call remote service methods</span></span>
<span data-ttu-id="6a650-119">L’appel de méthodes sur un service à l’aide de la pile de communication à distance est effectué avec un proxy local pour le service via la classe `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` .</span><span class="sxs-lookup"><span data-stu-id="6a650-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="6a650-120">La méthode `ServiceProxyBase` crée un proxy local à l’aide de l’interface implémentée par le service.</span><span class="sxs-lookup"><span data-stu-id="6a650-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="6a650-121">Avec ce proxy, vous pouvez appeler simplement et à distance des méthodes sur l'interface.</span><span class="sxs-lookup"><span data-stu-id="6a650-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="6a650-122">L'infrastructure de communication à distance propage les exceptions levées au niveau du service au client.</span><span class="sxs-lookup"><span data-stu-id="6a650-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="6a650-123">Par conséquent, la logique de gestion des exceptions au niveau du client à l’aide de `ServiceProxyBase` peut directement traiter les exceptions levées par le service.</span><span class="sxs-lookup"><span data-stu-id="6a650-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="6a650-124">Durée de vie du proxy du service</span><span class="sxs-lookup"><span data-stu-id="6a650-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="6a650-125">Comme la création de proxy de service est une opération légère, l’utilisateur peut en créer autant de fois que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6a650-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="6a650-126">Le proxy de service peut être réutilisé tant que l’utilisateur en a besoin.</span><span class="sxs-lookup"><span data-stu-id="6a650-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="6a650-127">L’utilisateur peut réutiliser le même proxy en cas d’exception.</span><span class="sxs-lookup"><span data-stu-id="6a650-127">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="6a650-128">Chaque proxy de service contient un client de communication qui permet d’envoyer des messages sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="6a650-128">Each ServiceProxy contains communication client used to send messages over the wire.</span></span> <span data-ttu-id="6a650-129">Lors de l’appel de l’API, un contrôle interne vérifie si le client de communication utilisé est valide.</span><span class="sxs-lookup"><span data-stu-id="6a650-129">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="6a650-130">En fonction de ce résultat, nous recréons le client de communication.</span><span class="sxs-lookup"><span data-stu-id="6a650-130">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="6a650-131">Par conséquent, l’utilisateur n’a pas besoin de recréer le proxy de service en cas d’exception.</span><span class="sxs-lookup"><span data-stu-id="6a650-131">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="6a650-132">Durée de vie de la fabrique ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="6a650-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="6a650-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) est une fabrique qui crée un proxy pour différentes interfaces de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="6a650-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="6a650-134">Si vous utilisez l’API `ServiceProxyBase.create` pour la création du proxy, l’infrastructure crée ensuite un `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="6a650-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="6a650-135">Il est utile d’en créer un manuellement lorsque vous devez remplacer les propriétés de [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory).</span><span class="sxs-lookup"><span data-stu-id="6a650-135">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="6a650-136">La fabrique est une opération coûteuse.</span><span class="sxs-lookup"><span data-stu-id="6a650-136">Factory is an expensive operation.</span></span> <span data-ttu-id="6a650-137">`FabricServiceProxyFactory` conserve le cache des clients de communication.</span><span class="sxs-lookup"><span data-stu-id="6a650-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="6a650-138">Il est recommandé de mettre en cache `FabricServiceProxyFactory` aussi longtemps que possible.</span><span class="sxs-lookup"><span data-stu-id="6a650-138">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="6a650-139">Gestion des exceptions à distance</span><span class="sxs-lookup"><span data-stu-id="6a650-139">Remoting Exception Handling</span></span>
<span data-ttu-id="6a650-140">Toutes les exceptions distantes levées par l’API du service sont renvoyées au client sous la forme RuntimeException ou FabricException.</span><span class="sxs-lookup"><span data-stu-id="6a650-140">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="6a650-141">Le proxy de service gère toutes les exceptions de basculement pour la partition de service pour laquelle il a été créé.</span><span class="sxs-lookup"><span data-stu-id="6a650-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="6a650-142">Il résout à nouveau les points de terminaison s’il existe des exceptions de basculement (non temporaires) et retente l’appel avec le point de terminaison correct.</span><span class="sxs-lookup"><span data-stu-id="6a650-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="6a650-143">Le nombre de tentatives pour l’exception de basculement est illimité.</span><span class="sxs-lookup"><span data-stu-id="6a650-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="6a650-144">En cas d’exceptions temporaires, il retente uniquement l’appel.</span><span class="sxs-lookup"><span data-stu-id="6a650-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="6a650-145">Les paramètres de nouvelle tentative par défaut sont fournis par [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="6a650-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="6a650-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) L’utilisateur peut configurer ces valeurs en transmettant l’objet OperationRetrySettings au constructeur ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="6a650-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a650-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a650-147">Next steps</span></span>
* [<span data-ttu-id="6a650-148">Sécurisation des communications pour Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6a650-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
