---
title: "vue d’ensemble de la communication aaaReliable Services | Documents Microsoft"
description: "Vue d’ensemble du modèle de communication des Services fiables hello, y compris lors de l’ouverture des écouteurs sur les services, résolution des points de terminaison et pour communiquer entre les services."
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
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="d0104-103">Comment toouse hello API de communication des Services fiables</span><span class="sxs-lookup"><span data-stu-id="d0104-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="d0104-104">Azure Service Fabric, en tant que plateforme, est totalement indépendant de la communication entre les services.</span><span class="sxs-lookup"><span data-stu-id="d0104-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="d0104-105">Tous les protocoles et les piles sont acceptables, UDP tooHTTP.</span><span class="sxs-lookup"><span data-stu-id="d0104-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="d0104-106">C’est toohello service développeur toochoose comment les services doivent communiquer.</span><span class="sxs-lookup"><span data-stu-id="d0104-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="d0104-107">infrastructure d’application des Services fiables Hello fournit des piles de communication intégrée, ainsi que des API que vous pouvez utiliser toobuild vos composants de communication personnalisées.</span><span class="sxs-lookup"><span data-stu-id="d0104-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="d0104-108">Configurer la communication de service</span><span class="sxs-lookup"><span data-stu-id="d0104-108">Set up service communication</span></span>
<span data-ttu-id="d0104-109">Hello API des Services fiables utilise une interface simple pour la communication de service.</span><span class="sxs-lookup"><span data-stu-id="d0104-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="d0104-110">tooopen un point de terminaison pour votre service, implémentez simplement cette interface :</span><span class="sxs-lookup"><span data-stu-id="d0104-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="d0104-111">Vous pouvez ensuite ajouter votre implémentation d’écouteur de communication en la retournant dans une substitution de méthode de classe de base de services.</span><span class="sxs-lookup"><span data-stu-id="d0104-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="d0104-112">Pour des services sans état :</span><span class="sxs-lookup"><span data-stu-id="d0104-112">For stateless services:</span></span>

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

<span data-ttu-id="d0104-113">Pour des services avec état :</span><span class="sxs-lookup"><span data-stu-id="d0104-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="d0104-114">Les services fiables ne sont pas encore pris en charge par Java.</span><span class="sxs-lookup"><span data-stu-id="d0104-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="d0104-115">Dans les deux cas, vous retournez une collection d’écouteurs.</span><span class="sxs-lookup"><span data-stu-id="d0104-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="d0104-116">Cela permet à votre toolisten service sur plusieurs points de terminaison, éventuellement à l’aide de différents protocoles, à l’aide de plusieurs écouteurs.</span><span class="sxs-lookup"><span data-stu-id="d0104-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="d0104-117">Par exemple, vous pouvez avoir un écouteur HTTP et un écouteur WebSocket distinct.</span><span class="sxs-lookup"><span data-stu-id="d0104-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="d0104-118">Chaque écouteur Obtient le nom et la collection résultante de hello de *nom : adresse* paires sont représentées en tant qu’objet JSON, lorsqu’un client demande des adresses d’écoute hello pour une instance de service ou d’une partition.</span><span class="sxs-lookup"><span data-stu-id="d0104-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="d0104-119">Dans un service sans état, hello remplacement retourne une collection de ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="d0104-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="d0104-120">A `ServiceInstanceListener` contient une fonction toocreate un `ICommunicationListener(C#) / CommunicationListener(Java)` et lui attribue un nom.</span><span class="sxs-lookup"><span data-stu-id="d0104-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="d0104-121">Pour les services avec état, hello remplacement retourne une collection de ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="d0104-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="d0104-122">Cela est légèrement différente de son homologue sans état, car un `ServiceReplicaListener` a une option tooopen un `ICommunicationListener` sur les réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="d0104-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="d0104-123">Non seulement vous pouvez utiliser plusieurs écouteurs de communication dans un service, mais vous pouvez également spécifier ceux qui acceptent les demandes sur les réplicas secondaires, et ceux qui écoutent uniquement sur les réplicas principaux.</span><span class="sxs-lookup"><span data-stu-id="d0104-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="d0104-124">Par exemple, vous pouvez avoir un ServiceRemotingListener qui ne prend les appels RPC que sur les réplicas principaux, et un second écouteur personnalisé qui prend les demandes de lecture sur les réplicas secondaires sur HTTP :</span><span class="sxs-lookup"><span data-stu-id="d0104-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="d0104-125">Lors de la création de plusieurs écouteurs pour un service, vous **devez** affecter un nom unique à chaque écouteur.</span><span class="sxs-lookup"><span data-stu-id="d0104-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="d0104-126">Enfin, décrivez les points de terminaison hello qui sont requis pour le service hello Bonjour [manifeste de service](service-fabric-application-model.md) sous la section hello sur les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d0104-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="d0104-127">écouteur de communications Hello peut accéder aux ressources de point de terminaison de hello allouées tooit de hello `CodePackageActivationContext` Bonjour `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="d0104-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="d0104-128">écouteur de Hello peut alors commencer à écouter les requêtes lorsqu’il est ouvert.</span><span class="sxs-lookup"><span data-stu-id="d0104-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="d0104-129">Ressources du point de terminaison sont package de service entier toohello courants, et ils sont alloués par l’infrastructure de Service lorsque le package de service hello est activé.</span><span class="sxs-lookup"><span data-stu-id="d0104-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="d0104-130">Plusieurs réplicas de service hébergés dans hello même ServiceHost peut-être partager hello même port.</span><span class="sxs-lookup"><span data-stu-id="d0104-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="d0104-131">Cela signifie que cet écouteur de communication hello doit prendre en charge le partage de port.</span><span class="sxs-lookup"><span data-stu-id="d0104-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="d0104-132">Hello recommandé d’effectuer cette opération consiste pour hello communication écouteur toouse hello partition ID et l’ID de réplica/instance lorsqu’il génère l’adresse d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="d0104-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="d0104-133">Enregistrement d’adresse de service</span><span class="sxs-lookup"><span data-stu-id="d0104-133">Service address registration</span></span>
<span data-ttu-id="d0104-134">Un service système appelé hello *Naming Service* s’exécute sur des clusters Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d0104-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="d0104-135">Hello d’affectation de noms de Service est un bureau d’enregistrement pour les services et leurs adresses qui écoute sur chaque instance ou un réplica du service de hello.</span><span class="sxs-lookup"><span data-stu-id="d0104-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="d0104-136">Hello lorsque `OpenAsync(C#) / openAsync(Java)` méthode d’un `ICommunicationListener(C#) / CommunicationListener(Java)` terminée, son retour valeur enregistrée Bonjour Naming Service.</span><span class="sxs-lookup"><span data-stu-id="d0104-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="d0104-137">Cette retourne la valeur qui obtient hello publiée dans le Service d’affectation de noms est une chaîne dont la valeur peut être rien du tout.</span><span class="sxs-lookup"><span data-stu-id="d0104-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="d0104-138">Cette valeur de chaîne est ce que les clients voient quand ils demandent une adresse de service hello hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="d0104-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

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

    // hello string returned here will be published in hello Naming Service.
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

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="d0104-139">L’infrastructure de service fournit des API qui autorisent les clients et les autres toothen services demandera cette adresse par nom de service.</span><span class="sxs-lookup"><span data-stu-id="d0104-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="d0104-140">Ceci est important, car l’adresse du service hello n’est pas statique.</span><span class="sxs-lookup"><span data-stu-id="d0104-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="d0104-141">Les services sont déplacés dans le cluster hello pour à des fins de disponibilité et de l’équilibrage de la ressource.</span><span class="sxs-lookup"><span data-stu-id="d0104-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="d0104-142">Il s’agit de mécanisme hello qui permettent aux clients hello tooresolve adresse pour un service d’écoute.</span><span class="sxs-lookup"><span data-stu-id="d0104-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="d0104-143">Pour une présentation complète des toowrite un écouteur de communication, voir [services API Web du Service Fabric avec OWIN auto-hébergement](service-fabric-reliable-services-communication-webapi.md) pour c#, tandis que pour Java, vous pouvez écrire votre propre implémentation de serveur HTTP, consultez EchoServer application exemple à https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="d0104-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="d0104-144">Communication avec un service</span><span class="sxs-lookup"><span data-stu-id="d0104-144">Communicating with a service</span></span>
<span data-ttu-id="d0104-145">Hello API des Services fiables fournit hello suivant clients toowrite bibliothèques qui communiquent avec les services.</span><span class="sxs-lookup"><span data-stu-id="d0104-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="d0104-146">Résolution de point de terminaison de service</span><span class="sxs-lookup"><span data-stu-id="d0104-146">Service endpoint resolution</span></span>
<span data-ttu-id="d0104-147">Hello première étape toocommunication avec un service est tooresolve une adresse de point de terminaison de la partition de hello ou une instance du service hello tootalk à.</span><span class="sxs-lookup"><span data-stu-id="d0104-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="d0104-148">Hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` classe utilitaire est une primitive de base qui aide les clients à déterminer le point de terminaison hello d’un service en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d0104-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="d0104-149">Dans la terminologie de Service Fabric, processus hello permettant de déterminer le point de terminaison hello d’un service est référencé tooas hello *résolution de point de terminaison de service*.</span><span class="sxs-lookup"><span data-stu-id="d0104-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="d0104-150">tooservices tooconnect au sein d’un cluster, ServicePartitionResolver peut être créé à l’aide des paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="d0104-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="d0104-151">Il s’agit de hello recommandé d’utilisation pour la plupart des situations :</span><span class="sxs-lookup"><span data-stu-id="d0104-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="d0104-152">tooservices tooconnect dans un cluster différent, un ServicePartitionResolver peut être créée avec un ensemble de points de terminaison de passerelle de cluster.</span><span class="sxs-lookup"><span data-stu-id="d0104-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="d0104-153">Notez que les points de terminaison de passerelle sont uniquement des points de terminaison pour la connexion toohello même cluster.</span><span class="sxs-lookup"><span data-stu-id="d0104-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="d0104-154">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d0104-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="d0104-155">Vous pouvez également `ServicePartitionResolver` peut être accordée à une fonction de création d’un `FabricClient` toouse en interne :</span><span class="sxs-lookup"><span data-stu-id="d0104-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

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

<span data-ttu-id="d0104-156">`FabricClient`est un objet hello toocommunicate utilisé avec un cluster Service Fabric de hello pour plusieurs opérations de gestion sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d0104-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="d0104-157">Cela est utile quand vous souhaitez contrôler davantage la façon dont un programme de résolution de partition de service interagit avec votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d0104-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="d0104-158">`FabricClient`effectue la mise en cache en interne et est généralement coûteuse toocreate, par conséquent, il est important tooreuse `FabricClient` instances autant que possibles.</span><span class="sxs-lookup"><span data-stu-id="d0104-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="d0104-159">Une méthode de résolution est utilisé tooretrieve hello adresse d’un service ou une partition de service pour les services partitionnées.</span><span class="sxs-lookup"><span data-stu-id="d0104-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="d0104-160">Une adresse de service peut être résolue facilement à l’aide d’un ServicePartitionResolver, mais le travail supplémentaire est nécessaire tooensure hello résolu l’adresse peut être utilisée correctement.</span><span class="sxs-lookup"><span data-stu-id="d0104-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="d0104-161">Votre client doit toodetect si la tentative de connexion hello a échoué en raison d’une erreur temporaire et peut être retentée (par exemple, service déplacé ou est temporairement indisponible), ou une erreur permanente (par exemple, le service a été supprimé ou le hello ressource demandée n’existe plus).</span><span class="sxs-lookup"><span data-stu-id="d0104-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="d0104-162">Instances de service ou de réplicas peuvent déplacer à partir du nœud toonode à tout moment pour plusieurs raisons.</span><span class="sxs-lookup"><span data-stu-id="d0104-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="d0104-163">adresse du service Hello résolu par ServicePartitionResolver peut-être être obsolète par heure hello que tooconnect tente de votre code client.</span><span class="sxs-lookup"><span data-stu-id="d0104-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="d0104-164">Dans ce cas à nouveau hello client a besoin adresse de hello toore résoudre.</span><span class="sxs-lookup"><span data-stu-id="d0104-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="d0104-165">Fournissant hello précédente `ResolvedServicePartition` indique que hello tootry des besoins de programme de résolution à nouveau au lieu de simplement récupérer une adresse en mémoire cache.</span><span class="sxs-lookup"><span data-stu-id="d0104-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="d0104-166">En règle générale, le code client hello devez fonctionne pas avec hello ServicePartitionResolver directement.</span><span class="sxs-lookup"><span data-stu-id="d0104-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="d0104-167">Elle est créée et passée sur les fabriques de client toocommunication Bonjour API des Services fiables.</span><span class="sxs-lookup"><span data-stu-id="d0104-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="d0104-168">fabriques de Hello utilisent le programme de résolution hello en interne un objet client qui peut être toocommunicate utilisé avec les services de toogenerate.</span><span class="sxs-lookup"><span data-stu-id="d0104-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="d0104-169">Fabriques et clients de communication</span><span class="sxs-lookup"><span data-stu-id="d0104-169">Communication clients and factories</span></span>
<span data-ttu-id="d0104-170">bibliothèque de fabrique de communication Hello implémente un modèle de nouvelle tentative de gestion d’erreurs standard qui facilite la nouvelle tentative points de terminaison de service tooresolved connexions.</span><span class="sxs-lookup"><span data-stu-id="d0104-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="d0104-171">bibliothèque de fabrique Hello fournit le mécanisme de nouvelle tentative hello pendant que vous fournissez des gestionnaires d’erreurs hello.</span><span class="sxs-lookup"><span data-stu-id="d0104-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="d0104-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`définit l’interface de base hello implémentée par une fabrique de client de communication qui produit des clients qui peuvent communiquer avec les services de Service Fabric tooa.</span><span class="sxs-lookup"><span data-stu-id="d0104-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="d0104-173">Bonjour implémentation de hello que communicationclientfactory dépend de la pile de communication hello utilisé par le service de Service Fabric hello où le client de hello veut toocommunicate.</span><span class="sxs-lookup"><span data-stu-id="d0104-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="d0104-174">Hello fiable API des Services fournit un `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="d0104-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="d0104-175">Cela fournit une implémentation de base de l’interface de CommunicationClientFactory hello et effectue des tâches qui sont des piles de communication commun tooall hello.</span><span class="sxs-lookup"><span data-stu-id="d0104-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="d0104-176">(Ces tâches incluent à l’aide d’un point de terminaison ServicePartitionResolver toodetermine hello).</span><span class="sxs-lookup"><span data-stu-id="d0104-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="d0104-177">Les clients implémentent généralement hello abstraite CommunicationClientFactoryBase toohandle logique de la classe qui est la pile de communication toohello spécifique.</span><span class="sxs-lookup"><span data-stu-id="d0104-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="d0104-178">client de communication Hello simplement reçoit une adresse et il utilise le service de tooa tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d0104-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="d0104-179">client de la Hello peut utiliser tout protocole il veut.</span><span class="sxs-lookup"><span data-stu-id="d0104-179">hello client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="d0104-180">fabrique de clients Hello est principalement responsable de la création de clients de communication.</span><span class="sxs-lookup"><span data-stu-id="d0104-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="d0104-181">Pour les clients qui ne maintiennent pas une connexion permanente, tel qu’un client HTTP, la fabrique de hello doit uniquement toocreate et client de retour hello.</span><span class="sxs-lookup"><span data-stu-id="d0104-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="d0104-182">Autres protocoles permettant de maintenir une connexion permanente, telles que certains protocoles binaire, doivent également être validés par hello fabrique toodetermine si la connexion de hello doit toobe recréée.</span><span class="sxs-lookup"><span data-stu-id="d0104-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

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

<span data-ttu-id="d0104-183">Enfin, un gestionnaire d’exceptions est chargé de déterminer quel tootake action lorsqu’une exception se produit.</span><span class="sxs-lookup"><span data-stu-id="d0104-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="d0104-184">Les exceptions sont classées en **reproductibles** et **non reproductibles**.</span><span class="sxs-lookup"><span data-stu-id="d0104-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="d0104-185">**Non renouvelable** exceptions simplement obtient à nouveau levées toohello arrière appelant.</span><span class="sxs-lookup"><span data-stu-id="d0104-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="d0104-186">Les exceptions **reproductibles** sont encore classées en **temporaires** et **non temporaires**.</span><span class="sxs-lookup"><span data-stu-id="d0104-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="d0104-187">**Transitoire** exceptions sont ceux qui peut simplement être tentée sans adresse de point de terminaison de service hello résoudre à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d0104-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="d0104-188">Il s’agit notamment des problèmes réseau temporaires ou réponses d’erreur service autre que ceux qui indiquent l’adresse de point de terminaison de service hello n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="d0104-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="d0104-189">**Non transitoires** exceptions sont ceux qui nécessitent des toobe d’adresse du point de terminaison de service hello résolu à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d0104-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="d0104-190">Il s’agit notamment des exceptions qui indiquent le point de terminaison de service hello est inaccessible, indiquant le service de hello a été déplacé tooa autre nœud.</span><span class="sxs-lookup"><span data-stu-id="d0104-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="d0104-191">Hello `TryHandleException` prend une décision sur une exception donnée.</span><span class="sxs-lookup"><span data-stu-id="d0104-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="d0104-192">Si elle **ne sait pas** le toomake décisions relatives à une exception, elle doit retourner **false**.</span><span class="sxs-lookup"><span data-stu-id="d0104-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="d0104-193">Si elle **connaît** quel toomake de décision, il doit définir le résultat de hello en conséquence et retourner **true**.</span><span class="sxs-lookup"><span data-stu-id="d0104-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

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

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
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

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="d0104-194">Exemple complet</span><span class="sxs-lookup"><span data-stu-id="d0104-194">Putting it all together</span></span>
<span data-ttu-id="d0104-195">Avec un `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, et `IExceptionHandler(C#) / ExceptionHandler(Java)` construit autour d’un protocole de communication, un `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` encapsule tous les éléments et fournit la gestion des erreurs de hello et boucle de résolution service partition adresse autour de ces composants.</span><span class="sxs-lookup"><span data-stu-id="d0104-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
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
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="d0104-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0104-196">Next steps</span></span>
* <span data-ttu-id="d0104-197">Pour obtenir un exemple de communication HTTP entre services, consultez cet [exemple de projet C# sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) ou cet [exemple de projet Java sur GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="d0104-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="d0104-198">Appels de procédure distante avec Reliable Services à distance</span><span class="sxs-lookup"><span data-stu-id="d0104-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="d0104-199">API Web qui utilise OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d0104-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="d0104-200">Communication WCF à l’aide de Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d0104-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
