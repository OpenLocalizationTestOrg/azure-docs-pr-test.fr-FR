---
title: "Vue d’ensemble de la communication Reliable Services | Microsoft Docs"
description: "Présentation du modèle de communication Reliable Services, notamment de l’ouverture d’écouteurs sur les services, de la résolution des points de terminaison et de la communication entre les services."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: b418904f50b772c12bfcdbb95beb9312c8b9fb00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="07d6e-103">Utilisation des API de communication de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="07d6e-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="07d6e-104">Azure Service Fabric, en tant que plateforme, est totalement indépendant de la communication entre les services.</span><span class="sxs-lookup"><span data-stu-id="07d6e-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="07d6e-105">Tous les protocoles et toutes les piles sont acceptables, de UDP à HTTP.</span><span class="sxs-lookup"><span data-stu-id="07d6e-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="07d6e-106">C'est au développeur de services de choisir comment les services doivent communiquer.</span><span class="sxs-lookup"><span data-stu-id="07d6e-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="07d6e-107">L’infrastructure d’application de Reliable Services fournit des piles de communication intégrées, ainsi que des API que vous pouvez utiliser pour générer vos composants de communication personnalisés.</span><span class="sxs-lookup"><span data-stu-id="07d6e-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="07d6e-108">Configurer la communication de service</span><span class="sxs-lookup"><span data-stu-id="07d6e-108">Set up service communication</span></span>
<span data-ttu-id="07d6e-109">L'API Reliable Services utilise une interface simple pour la communication de service.</span><span class="sxs-lookup"><span data-stu-id="07d6e-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="07d6e-110">Pour ouvrir un point de terminaison pour votre service, implémentez simplement cette interface :</span><span class="sxs-lookup"><span data-stu-id="07d6e-110">To open an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="07d6e-111">Vous pouvez ensuite ajouter votre implémentation d’écouteur de communication en la retournant dans une substitution de méthode de classe de base de services.</span><span class="sxs-lookup"><span data-stu-id="07d6e-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="07d6e-112">Pour des services sans état :</span><span class="sxs-lookup"><span data-stu-id="07d6e-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="07d6e-113">Pour des services avec état :</span><span class="sxs-lookup"><span data-stu-id="07d6e-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="07d6e-114">Les services fiables ne sont pas encore pris en charge par Java.</span><span class="sxs-lookup"><span data-stu-id="07d6e-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="07d6e-115">Dans les deux cas, vous retournez une collection d’écouteurs.</span><span class="sxs-lookup"><span data-stu-id="07d6e-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="07d6e-116">Cela permet à votre service d’écouter sur plusieurs points de terminaison, utilisant éventuellement différents protocoles, à l’aide de plusieurs écouteurs.</span><span class="sxs-lookup"><span data-stu-id="07d6e-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="07d6e-117">Par exemple, vous pouvez avoir un écouteur HTTP et un écouteur WebSocket distinct.</span><span class="sxs-lookup"><span data-stu-id="07d6e-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="07d6e-118">Chaque écouteur obtient un nom et la collection qui résulte des paires *nom : adresse* est représentée en tant qu’objet JSON quand un client demande les adresses d’écoute pour une instance de service ou une partition.</span><span class="sxs-lookup"><span data-stu-id="07d6e-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="07d6e-119">Dans un service sans état, la substitution retourne une collection de ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="07d6e-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="07d6e-120">Un `ServiceInstanceListener` contient une fonction permettant de créer un `ICommunicationListener(C#) / CommunicationListener(Java)` et de lui donner un nom.</span><span class="sxs-lookup"><span data-stu-id="07d6e-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="07d6e-121">Pour les services avec état, la substitution retourne une collection de ServiceReplicaListener.</span><span class="sxs-lookup"><span data-stu-id="07d6e-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="07d6e-122">Cela diffère légèrement de son homologue sans état, car un `ServiceReplicaListener` a une option pour ouvrir un `ICommunicationListener` sur des réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="07d6e-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="07d6e-123">Non seulement vous pouvez utiliser plusieurs écouteurs de communication dans un service, mais vous pouvez également spécifier ceux qui acceptent les demandes sur les réplicas secondaires, et ceux qui écoutent uniquement sur les réplicas principaux.</span><span class="sxs-lookup"><span data-stu-id="07d6e-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="07d6e-124">Par exemple, vous pouvez avoir un ServiceRemotingListener qui ne prend les appels RPC que sur les réplicas principaux, et un second écouteur personnalisé qui prend les demandes de lecture sur les réplicas secondaires sur HTTP :</span><span class="sxs-lookup"><span data-stu-id="07d6e-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="07d6e-125">Lors de la création de plusieurs écouteurs pour un service, vous **devez** affecter un nom unique à chaque écouteur.</span><span class="sxs-lookup"><span data-stu-id="07d6e-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="07d6e-126">Pour finir, décrivez les points de terminaison nécessaires pour le service dans le [manifeste de service](service-fabric-application-model.md) , dans la section consacrée aux points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="07d6e-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="07d6e-127">L’écouteur de communication peut accéder aux ressources de point de terminaison qui lui sont allouées à partir du `CodePackageActivationContext` dans `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="07d6e-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="07d6e-128">L’écouteur peut alors commencer à écouter les demandes quand il est ouvert.</span><span class="sxs-lookup"><span data-stu-id="07d6e-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="07d6e-129">Les ressources de point de terminaison sont communes au package de service entier et elles sont allouées par Service Fabric à l’activation du package de service.</span><span class="sxs-lookup"><span data-stu-id="07d6e-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="07d6e-130">Plusieurs réplicas de service hébergés dans le même ServiceHost peuvent partager le même port.</span><span class="sxs-lookup"><span data-stu-id="07d6e-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="07d6e-131">Cela signifie que l'écouteur de communication doit prendre en charge le partage de port.</span><span class="sxs-lookup"><span data-stu-id="07d6e-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="07d6e-132">La méthode recommandée consiste à configurer l’écouteur de communication afin qu’il utiliser l’ID de la partition et l’ID du réplica/de l’instance lors de la génération de l’adresse d’écoute.</span><span class="sxs-lookup"><span data-stu-id="07d6e-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="07d6e-133">Enregistrement d’adresse de service</span><span class="sxs-lookup"><span data-stu-id="07d6e-133">Service address registration</span></span>
<span data-ttu-id="07d6e-134">Un service système appelé *service d’attribution de noms* s’exécute sur les clusters Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="07d6e-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="07d6e-135">Le service d’attribution de noms est un bureau d’enregistrement pour les services et leurs adresses sur lesquelles chaque instance ou réplica du service écoute.</span><span class="sxs-lookup"><span data-stu-id="07d6e-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="07d6e-136">Une fois l’exécution de la méthode `OpenAsync(C#) / openAsync(Java)` d’un `ICommunicationListener(C#) / CommunicationListener(Java)` terminée, la valeur retournée est enregistrée dans le service d’attribution de noms.</span><span class="sxs-lookup"><span data-stu-id="07d6e-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="07d6e-137">Cette valeur publiée dans le service d’attribution de noms est une chaîne dont le contenu peut être absolument quelconque.</span><span class="sxs-lookup"><span data-stu-id="07d6e-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="07d6e-138">Cette valeur de chaîne est ce que les clients voient quand ils demandent au service d’attribution de noms une adresse pour le service.</span><span class="sxs-lookup"><span data-stu-id="07d6e-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // the string returned here will be published in the Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="07d6e-139">Service Fabric fournit des API qui permettent aux clients et à d’autres services de demander cette adresse par nom de service.</span><span class="sxs-lookup"><span data-stu-id="07d6e-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="07d6e-140">Ceci est important, car l’adresse du service n’est pas statique.</span><span class="sxs-lookup"><span data-stu-id="07d6e-140">This is important because the service address is not static.</span></span> <span data-ttu-id="07d6e-141">Les services se déplacent dans le cluster à des fins d’équilibrage des ressources et de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="07d6e-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="07d6e-142">Ce mécanisme permet aux clients de résoudre l'adresse d'écoute pour un service.</span><span class="sxs-lookup"><span data-stu-id="07d6e-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="07d6e-143">Pour une vue d’ensemble complète de l’écriture d’un écouteur de communication, consultez [Services de l’API Web Service Fabric avec auto-hébergement OWIN](service-fabric-reliable-services-communication-webapi.md) pour C#. Pour Java, vous pouvez écrire votre propre implémentation de serveur HTTP en suivant l’exemple d’application EchoServer sur https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="07d6e-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="07d6e-144">Communication avec un service</span><span class="sxs-lookup"><span data-stu-id="07d6e-144">Communicating with a service</span></span>
<span data-ttu-id="07d6e-145">L’API Reliable Services fournit les bibliothèques suivantes pour l’écriture de clients qui communiquent avec des services.</span><span class="sxs-lookup"><span data-stu-id="07d6e-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="07d6e-146">Résolution de point de terminaison de service</span><span class="sxs-lookup"><span data-stu-id="07d6e-146">Service endpoint resolution</span></span>
<span data-ttu-id="07d6e-147">La première étape de la communication avec un service consiste à résoudre une adresse de point de terminaison de la partition ou une instance du service avec lequel vous souhaitez communiquer.</span><span class="sxs-lookup"><span data-stu-id="07d6e-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="07d6e-148">La classe utilitaire `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` est une primitive de base qui aide les clients à déterminer le point de terminaison d’un service au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="07d6e-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="07d6e-149">Dans la terminologie Service Fabric, le processus de détermination du point de terminaison d’un service est appelé *résolution de point de terminaison de service*.</span><span class="sxs-lookup"><span data-stu-id="07d6e-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="07d6e-150">Pour vous connecter à des services dans un cluster, vous pouvez créer un ServicePartitionResolver à l’aide de paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="07d6e-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="07d6e-151">Il s’agit de l’utilisation recommandée pour la plupart des situations :</span><span class="sxs-lookup"><span data-stu-id="07d6e-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="07d6e-152">Pour vous connecter à des services figurant dans un autre cluster, vous pouvez créer un ServicePartitionResolver avec un ensemble de points de terminaison de passerelle de cluster.</span><span class="sxs-lookup"><span data-stu-id="07d6e-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="07d6e-153">Notez que les points de terminaison de passerelle sont simplement des points de terminaison différents pour la connexion au même cluster.</span><span class="sxs-lookup"><span data-stu-id="07d6e-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="07d6e-154">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="07d6e-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="07d6e-155">En guise d’alternative, un `ServicePartitionResolver` peut recevoir une fonction de création d’un `FabricClient` à utiliser en interne :</span><span class="sxs-lookup"><span data-stu-id="07d6e-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="07d6e-156">`FabricClient` est l’objet utilisé pour communiquer avec le cluster Service Fabric pour diverses opérations de gestion sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="07d6e-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="07d6e-157">Cela est utile quand vous souhaitez contrôler davantage la façon dont un programme de résolution de partition de service interagit avec votre cluster.</span><span class="sxs-lookup"><span data-stu-id="07d6e-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="07d6e-158">`FabricClient` effectue la mise en cache en interne et sa création est généralement coûteuse. Il est donc important de réutiliser les instances `FabricClient` autant que possible.</span><span class="sxs-lookup"><span data-stu-id="07d6e-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="07d6e-159">Une méthode de résolution est ensuite utilisée pour récupérer l’adresse d’un service ou d’une partition de service pour les services partitionnés.</span><span class="sxs-lookup"><span data-stu-id="07d6e-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="07d6e-160">Un ServicePartitionResolver peut facilement résoudre une adresse de service, mais il faut davantage de travail pour s’assurer que l’adresse résolue est correctement utilisable.</span><span class="sxs-lookup"><span data-stu-id="07d6e-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="07d6e-161">Votre client doit détecter si la tentative de connexion a échoué en raison d’une erreur temporaire et peut être retentée (par exemple, le service a changé d’emplacement ou est temporairement indisponible), ou d’une erreur permanente (par exemple, le service a été supprimé ou la ressource demandée n’existe plus).</span><span class="sxs-lookup"><span data-stu-id="07d6e-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="07d6e-162">Des instances de service ou réplicas peuvent passer d’un nœud à l’autre à tout moment pour plusieurs raisons.</span><span class="sxs-lookup"><span data-stu-id="07d6e-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="07d6e-163">L’adresse de service résolue par le biais de ServicePartitionResolver peut être obsolète au moment où votre code client tente de se connecter.</span><span class="sxs-lookup"><span data-stu-id="07d6e-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="07d6e-164">Dans ce cas encore, le client doit à nouveau résoudre l’adresse.</span><span class="sxs-lookup"><span data-stu-id="07d6e-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="07d6e-165">Le code `ResolvedServicePartition` précédent indique que le programme de résolution doit effectuer une nouvelle tentative au lieu de simplement récupérer une adresse en mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="07d6e-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="07d6e-166">Généralement, le code client ne doit pas fonctionner directement avec ServicePartitionResolver.</span><span class="sxs-lookup"><span data-stu-id="07d6e-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="07d6e-167">Il est créé et transmis à des fabriques de clients de communication dans l’API Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="07d6e-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="07d6e-168">Les fabriques utilisent le programme de résolution en interne pour générer un objet client utilisable pour communiquer avec les services.</span><span class="sxs-lookup"><span data-stu-id="07d6e-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="07d6e-169">Fabriques et clients de communication</span><span class="sxs-lookup"><span data-stu-id="07d6e-169">Communication clients and factories</span></span>
<span data-ttu-id="07d6e-170">La bibliothèque de fabrique de communication implémente un modèle standard de nouvelle tentative de gestion des erreurs, qui facilite les nouvelles tentatives de connexion aux points de terminaison de service résolus.</span><span class="sxs-lookup"><span data-stu-id="07d6e-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="07d6e-171">La bibliothèque de fabrique fournit le mécanisme de nouvelle tentative, tandis que vous fournissez les gestionnaires d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="07d6e-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="07d6e-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` définit l’interface de base implémentée par une fabrique de clients de communication qui produit des clients capables de communiquer avec un service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="07d6e-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="07d6e-173">L’implémentation de CommunicationClientFactory dépend de la pile de communication utilisée par le service Service Fabric avec lequel le client veut communiquer.</span><span class="sxs-lookup"><span data-stu-id="07d6e-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="07d6e-174">L’API Reliable Services fournit un `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="07d6e-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="07d6e-175">Celui-ci assure une implémentation de base de l’interface CommunicationClientFactory et effectue des tâches communes à toutes les piles de communication.</span><span class="sxs-lookup"><span data-stu-id="07d6e-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="07d6e-176">(ces tâches incluent l’utilisation d’un ServicePartitionResolver pour déterminer le point de terminaison de service).</span><span class="sxs-lookup"><span data-stu-id="07d6e-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="07d6e-177">Les clients implémentent généralement la classe abstraite CommunicationClientFactoryBase pour gérer la logique spécifique de la pile de communication.</span><span class="sxs-lookup"><span data-stu-id="07d6e-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="07d6e-178">Le client de communication reçoit simplement une adresse qu’il utilise pour se connecter à un service.</span><span class="sxs-lookup"><span data-stu-id="07d6e-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="07d6e-179">Le client peut utiliser n’importe quel protocole.</span><span class="sxs-lookup"><span data-stu-id="07d6e-179">The client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="07d6e-180">La fabrique de clients est principalement responsable de la création de clients de communication.</span><span class="sxs-lookup"><span data-stu-id="07d6e-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="07d6e-181">Pour les clients qui ne maintiennent de connexion permanente, tel un client HTTP, la fabrique doit uniquement créer et retourner le client.</span><span class="sxs-lookup"><span data-stu-id="07d6e-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="07d6e-182">D’autres protocoles qui maintiennent une connexion permanente, tels certains protocoles binaires, doivent également être validés par la fabrique pour déterminer si la connexion doit être recréée.</span><span class="sxs-lookup"><span data-stu-id="07d6e-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="07d6e-183">Enfin, un gestionnaire d’exceptions doit déterminer l’action à exécuter si une exception se produit.</span><span class="sxs-lookup"><span data-stu-id="07d6e-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="07d6e-184">Les exceptions sont classées en **reproductibles** et **non reproductibles**.</span><span class="sxs-lookup"><span data-stu-id="07d6e-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="07d6e-185">Les exceptions **Non reproductibles** sont simplement renvoyées à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="07d6e-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="07d6e-186">Les exceptions **reproductibles** sont encore classées en **temporaires** et **non temporaires**.</span><span class="sxs-lookup"><span data-stu-id="07d6e-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="07d6e-187">**temporaires** sont celles qui peuvent simplement faire l’objet d’une nouvelle tentative, sans nouvelle résolution de l’adresse du point de terminaison de service.</span><span class="sxs-lookup"><span data-stu-id="07d6e-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="07d6e-188">Elles incluent notamment des problèmes réseau temporaires ou des réponses d’erreur de service autres que celles indiquant que l’adresse du point de terminaison de service est inexistante.</span><span class="sxs-lookup"><span data-stu-id="07d6e-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="07d6e-189">**Non-transient** sont celles qui nécessitent une nouvelle résolution de l’adresse du point de terminaison de service.</span><span class="sxs-lookup"><span data-stu-id="07d6e-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="07d6e-190">Elles incluent notamment les exceptions indiquant que le point de terminaison de service n’a pas pu être atteint, ce qui signifie que le service s’est déplacé vers un autre nœud.</span><span class="sxs-lookup"><span data-stu-id="07d6e-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="07d6e-191">La fonction `TryHandleException` prend une décision concernant une exception donnée.</span><span class="sxs-lookup"><span data-stu-id="07d6e-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="07d6e-192">Si elle **ne sait pas** quelle décision prendre à propos d’une exception, elle doit retourner la valeur **false**.</span><span class="sxs-lookup"><span data-stu-id="07d6e-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="07d6e-193">Si elle **sait** quelle décision prendre, elle doit définir le résultat en conséquence et retourner la valeur **true**.</span><span class="sxs-lookup"><span data-stu-id="07d6e-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="07d6e-194">Exemple complet</span><span class="sxs-lookup"><span data-stu-id="07d6e-194">Putting it all together</span></span>
<span data-ttu-id="07d6e-195">Avec des composants `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` et `IExceptionHandler(C#) / ExceptionHandler(Java)` construits autour d’un protocole de communication, un `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` encapsule le tout et fournit la boucle de gestion des erreurs et de résolution d’adresse de partition de service autour de ces composants.</span><span class="sxs-lookup"><span data-stu-id="07d6e-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="07d6e-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07d6e-196">Next steps</span></span>
* <span data-ttu-id="07d6e-197">Pour obtenir un exemple de communication HTTP entre services, consultez cet [exemple de projet C# sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) ou cet [exemple de projet Java sur GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="07d6e-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="07d6e-198">Appels de procédure distante avec Reliable Services à distance</span><span class="sxs-lookup"><span data-stu-id="07d6e-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="07d6e-199">API Web qui utilise OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="07d6e-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="07d6e-200">Communication WCF à l’aide de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="07d6e-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
