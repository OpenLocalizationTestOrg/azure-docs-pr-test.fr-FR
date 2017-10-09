---
title: "communication à distance aaaService dans Azure Service Fabric | Documents Microsoft"
description: "La communication à distance de l’infrastructure de service permet aux clients et services toocommunicate avec les services à l’aide d’un appel de procédure distante."
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
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="78f29-103">Communication à distance des services avec Reliable Services</span><span class="sxs-lookup"><span data-stu-id="78f29-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="78f29-104">C# sur Windows</span><span class="sxs-lookup"><span data-stu-id="78f29-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="78f29-105">Java sur Linux</span><span class="sxs-lookup"><span data-stu-id="78f29-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="78f29-106">infrastructure de Services fiables Hello fournit un tooquickly de mécanisme de communication à distance et facilement configurer l’appel de procédure distante pour les services.</span><span class="sxs-lookup"><span data-stu-id="78f29-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="78f29-107">Configuration de la communication à distance sur un service</span><span class="sxs-lookup"><span data-stu-id="78f29-107">Set up remoting on a service</span></span>
<span data-ttu-id="78f29-108">La configuration de communication à distance pour un service s'effectue en deux étapes simples :</span><span class="sxs-lookup"><span data-stu-id="78f29-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="78f29-109">Créez une interface pour votre tooimplement de service.</span><span class="sxs-lookup"><span data-stu-id="78f29-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="78f29-110">Cette interface définit les méthodes hello qui sont disponibles pour un appel de procédure distante sur votre service.</span><span class="sxs-lookup"><span data-stu-id="78f29-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="78f29-111">les méthodes Hello doivent être retournant des tâches méthodes asynchrones.</span><span class="sxs-lookup"><span data-stu-id="78f29-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="78f29-112">Hello interface doit implémenter `microsoft.serviceFabric.services.remoting.Service` toosignal qui hello service dispose d’une interface de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="78f29-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="78f29-113">Utilisez un écouteur de communication à distance dans votre service.</span><span class="sxs-lookup"><span data-stu-id="78f29-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="78f29-114">Il s'agit d'une implémentation `CommunicationListener` qui fournit des fonctionnalités de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="78f29-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="78f29-115">`FabricTransportServiceRemotingListener`peut être utilisé toocreate un écouteur de la communication à distance à l’aide du protocole de transport de la communication à distance par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="78f29-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="78f29-116">Par exemple, hello service sans état suivant expose une méthode unique de tooget « Hello World » via un appel de procédure distante.</span><span class="sxs-lookup"><span data-stu-id="78f29-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="78f29-117">Hello et les arguments de hello retournent des types dans l’interface de service hello peuvent être des types simples, complexes ou personnalisées, mais ils doivent être sérialisables.</span><span class="sxs-lookup"><span data-stu-id="78f29-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="78f29-118">Méthodes d’appel de service distant</span><span class="sxs-lookup"><span data-stu-id="78f29-118">Call remote service methods</span></span>
<span data-ttu-id="78f29-119">Appel de méthodes sur un service à l’aide de pile de communication à distance hello est effectuée à l’aide d’un service de toohello proxy local via hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe.</span><span class="sxs-lookup"><span data-stu-id="78f29-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="78f29-120">Hello `ServiceProxyBase` méthode crée un proxy local à l’aide de hello même interface que hello service implémente.</span><span class="sxs-lookup"><span data-stu-id="78f29-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="78f29-121">Avec ce serveur proxy, vous pouvez simplement appeler des méthodes sur les interface hello à distance.</span><span class="sxs-lookup"><span data-stu-id="78f29-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="78f29-122">infrastructure de communication à distance Hello propage les exceptions levées au client du service de toohello hello.</span><span class="sxs-lookup"><span data-stu-id="78f29-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="78f29-123">Logique, gestion des exceptions au client hello à l’aide de `ServiceProxyBase` peut gérer directement les exceptions hello service lève une exception.</span><span class="sxs-lookup"><span data-stu-id="78f29-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="78f29-124">Durée de vie du proxy du service</span><span class="sxs-lookup"><span data-stu-id="78f29-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="78f29-125">Comme la création de proxy de service est une opération légère, l’utilisateur peut en créer autant de fois que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="78f29-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="78f29-126">Le proxy de service peut être réutilisé tant que l’utilisateur en a besoin.</span><span class="sxs-lookup"><span data-stu-id="78f29-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="78f29-127">Utilisateur peut réutiliser hello proxy même en cas d’Exception.</span><span class="sxs-lookup"><span data-stu-id="78f29-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="78f29-128">Chaque ServiceProxy contient des messages de communication client utilisé toosend acheminement hello.</span><span class="sxs-lookup"><span data-stu-id="78f29-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="78f29-129">Lors de l’appel d’API, nous avons toosee de contrôle interne si le client de communication utilisé est valide.</span><span class="sxs-lookup"><span data-stu-id="78f29-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="78f29-130">En fonction de ce résultat, nous recréer client de communication hello.</span><span class="sxs-lookup"><span data-stu-id="78f29-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="78f29-131">Par conséquent, les utilisateurs n’avez pas besoin serviceproxy toorecreate en cas d’Exception.</span><span class="sxs-lookup"><span data-stu-id="78f29-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="78f29-132">Durée de vie de la fabrique ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="78f29-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="78f29-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) est une fabrique qui crée un proxy pour différentes interfaces de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="78f29-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="78f29-134">Si vous utilisez l’API `ServiceProxyBase.create` pour la création du proxy, l’infrastructure crée ensuite un `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="78f29-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="78f29-135">Il est utile toocreate une manuellement lorsque vous avez besoin de toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) propriétés.</span><span class="sxs-lookup"><span data-stu-id="78f29-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="78f29-136">La fabrique est une opération coûteuse.</span><span class="sxs-lookup"><span data-stu-id="78f29-136">Factory is an expensive operation.</span></span> <span data-ttu-id="78f29-137">`FabricServiceProxyFactory` conserve le cache des clients de communication.</span><span class="sxs-lookup"><span data-stu-id="78f29-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="78f29-138">Il est préférable toocache `FabricServiceProxyFactory` aussi longtemps que possible.</span><span class="sxs-lookup"><span data-stu-id="78f29-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="78f29-139">Gestion des exceptions à distance</span><span class="sxs-lookup"><span data-stu-id="78f29-139">Remoting Exception Handling</span></span>
<span data-ttu-id="78f29-140">Tous les hello à distance d’exception levée par l’API de service, sont envoyés toohello précédent client sous la forme RuntimeException ou FabricException.</span><span class="sxs-lookup"><span data-stu-id="78f29-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="78f29-141">ServiceProxy gère toutes les exceptions de basculement pour la partition de service hello il est créé pour.</span><span class="sxs-lookup"><span data-stu-id="78f29-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="78f29-142">Nouveau, il résout les points de terminaison hello si Failover Exceptions(Non-Transient Exceptions) et nouvelles tentatives appel hello avec le point de terminaison correct hello est.</span><span class="sxs-lookup"><span data-stu-id="78f29-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="78f29-143">Le nombre de tentatives pour l’exception de basculement est illimité.</span><span class="sxs-lookup"><span data-stu-id="78f29-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="78f29-144">En cas de TransientExceptions, il réessaie uniquement appel de hello.</span><span class="sxs-lookup"><span data-stu-id="78f29-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="78f29-145">Les paramètres de nouvelle tentative par défaut sont fournis par [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="78f29-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="78f29-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Utilisateur peut configurer ces valeurs en passant le constructeur de tooServiceProxyFactory OperationRetrySettings objet.</span><span class="sxs-lookup"><span data-stu-id="78f29-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78f29-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78f29-147">Next steps</span></span>
* [<span data-ttu-id="78f29-148">Sécurisation des communications pour Reliable Services</span><span class="sxs-lookup"><span data-stu-id="78f29-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
