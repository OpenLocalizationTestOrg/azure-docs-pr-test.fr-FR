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
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Comment toouse hello API de communication des Services fiables
Azure Service Fabric, en tant que plateforme, est totalement indépendant de la communication entre les services. Tous les protocoles et les piles sont acceptables, UDP tooHTTP. C’est toohello service développeur toochoose comment les services doivent communiquer. infrastructure d’application des Services fiables Hello fournit des piles de communication intégrée, ainsi que des API que vous pouvez utiliser toobuild vos composants de communication personnalisées.

## <a name="set-up-service-communication"></a>Configurer la communication de service
Hello API des Services fiables utilise une interface simple pour la communication de service. tooopen un point de terminaison pour votre service, implémentez simplement cette interface :

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

Vous pouvez ensuite ajouter votre implémentation d’écouteur de communication en la retournant dans une substitution de méthode de classe de base de services.

Pour des services sans état :

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

Pour des services avec état :

> [!NOTE]
> Les services fiables ne sont pas encore pris en charge par Java.
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

Dans les deux cas, vous retournez une collection d’écouteurs. Cela permet à votre toolisten service sur plusieurs points de terminaison, éventuellement à l’aide de différents protocoles, à l’aide de plusieurs écouteurs. Par exemple, vous pouvez avoir un écouteur HTTP et un écouteur WebSocket distinct. Chaque écouteur Obtient le nom et la collection résultante de hello de *nom : adresse* paires sont représentées en tant qu’objet JSON, lorsqu’un client demande des adresses d’écoute hello pour une instance de service ou d’une partition.

Dans un service sans état, hello remplacement retourne une collection de ServiceInstanceListeners. A `ServiceInstanceListener` contient une fonction toocreate un `ICommunicationListener(C#) / CommunicationListener(Java)` et lui attribue un nom. Pour les services avec état, hello remplacement retourne une collection de ServiceReplicaListeners. Cela est légèrement différente de son homologue sans état, car un `ServiceReplicaListener` a une option tooopen un `ICommunicationListener` sur les réplicas secondaires. Non seulement vous pouvez utiliser plusieurs écouteurs de communication dans un service, mais vous pouvez également spécifier ceux qui acceptent les demandes sur les réplicas secondaires, et ceux qui écoutent uniquement sur les réplicas principaux.

Par exemple, vous pouvez avoir un ServiceRemotingListener qui ne prend les appels RPC que sur les réplicas principaux, et un second écouteur personnalisé qui prend les demandes de lecture sur les réplicas secondaires sur HTTP :

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
> Lors de la création de plusieurs écouteurs pour un service, vous **devez** affecter un nom unique à chaque écouteur.
>
>

Enfin, décrivez les points de terminaison hello qui sont requis pour le service hello Bonjour [manifeste de service](service-fabric-application-model.md) sous la section hello sur les points de terminaison.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

écouteur de communications Hello peut accéder aux ressources de point de terminaison de hello allouées tooit de hello `CodePackageActivationContext` Bonjour `ServiceContext`. écouteur de Hello peut alors commencer à écouter les requêtes lorsqu’il est ouvert.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Ressources du point de terminaison sont package de service entier toohello courants, et ils sont alloués par l’infrastructure de Service lorsque le package de service hello est activé. Plusieurs réplicas de service hébergés dans hello même ServiceHost peut-être partager hello même port. Cela signifie que cet écouteur de communication hello doit prendre en charge le partage de port. Hello recommandé d’effectuer cette opération consiste pour hello communication écouteur toouse hello partition ID et l’ID de réplica/instance lorsqu’il génère l’adresse d’écoute hello.
>
>

### <a name="service-address-registration"></a>Enregistrement d’adresse de service
Un service système appelé hello *Naming Service* s’exécute sur des clusters Service Fabric. Hello d’affectation de noms de Service est un bureau d’enregistrement pour les services et leurs adresses qui écoute sur chaque instance ou un réplica du service de hello. Hello lorsque `OpenAsync(C#) / openAsync(Java)` méthode d’un `ICommunicationListener(C#) / CommunicationListener(Java)` terminée, son retour valeur enregistrée Bonjour Naming Service. Cette retourne la valeur qui obtient hello publiée dans le Service d’affectation de noms est une chaîne dont la valeur peut être rien du tout. Cette valeur de chaîne est ce que les clients voient quand ils demandent une adresse de service hello hello Naming Service.

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

L’infrastructure de service fournit des API qui autorisent les clients et les autres toothen services demandera cette adresse par nom de service. Ceci est important, car l’adresse du service hello n’est pas statique. Les services sont déplacés dans le cluster hello pour à des fins de disponibilité et de l’équilibrage de la ressource. Il s’agit de mécanisme hello qui permettent aux clients hello tooresolve adresse pour un service d’écoute.

> [!NOTE]
> Pour une présentation complète des toowrite un écouteur de communication, voir [services API Web du Service Fabric avec OWIN auto-hébergement](service-fabric-reliable-services-communication-webapi.md) pour c#, tandis que pour Java, vous pouvez écrire votre propre implémentation de serveur HTTP, consultez EchoServer application exemple à https://github.com/Azure-Samples/service-fabric-java-getting-started.
>
>

## <a name="communicating-with-a-service"></a>Communication avec un service
Hello API des Services fiables fournit hello suivant clients toowrite bibliothèques qui communiquent avec les services.

### <a name="service-endpoint-resolution"></a>Résolution de point de terminaison de service
Hello première étape toocommunication avec un service est tooresolve une adresse de point de terminaison de la partition de hello ou une instance du service hello tootalk à. Hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` classe utilitaire est une primitive de base qui aide les clients à déterminer le point de terminaison hello d’un service en cours d’exécution. Dans la terminologie de Service Fabric, processus hello permettant de déterminer le point de terminaison hello d’un service est référencé tooas hello *résolution de point de terminaison de service*.

tooservices tooconnect au sein d’un cluster, ServicePartitionResolver peut être créé à l’aide des paramètres par défaut. Il s’agit de hello recommandé d’utilisation pour la plupart des situations :

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooservices tooconnect dans un cluster différent, un ServicePartitionResolver peut être créée avec un ensemble de points de terminaison de passerelle de cluster. Notez que les points de terminaison de passerelle sont uniquement des points de terminaison pour la connexion toohello même cluster. Par exemple :

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

Vous pouvez également `ServicePartitionResolver` peut être accordée à une fonction de création d’un `FabricClient` toouse en interne :

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

`FabricClient`est un objet hello toocommunicate utilisé avec un cluster Service Fabric de hello pour plusieurs opérations de gestion sur le cluster de hello. Cela est utile quand vous souhaitez contrôler davantage la façon dont un programme de résolution de partition de service interagit avec votre cluster. `FabricClient`effectue la mise en cache en interne et est généralement coûteuse toocreate, par conséquent, il est important tooreuse `FabricClient` instances autant que possibles.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

Une méthode de résolution est utilisé tooretrieve hello adresse d’un service ou une partition de service pour les services partitionnées.

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

Une adresse de service peut être résolue facilement à l’aide d’un ServicePartitionResolver, mais le travail supplémentaire est nécessaire tooensure hello résolu l’adresse peut être utilisée correctement. Votre client doit toodetect si la tentative de connexion hello a échoué en raison d’une erreur temporaire et peut être retentée (par exemple, service déplacé ou est temporairement indisponible), ou une erreur permanente (par exemple, le service a été supprimé ou le hello ressource demandée n’existe plus). Instances de service ou de réplicas peuvent déplacer à partir du nœud toonode à tout moment pour plusieurs raisons. adresse du service Hello résolu par ServicePartitionResolver peut-être être obsolète par heure hello que tooconnect tente de votre code client. Dans ce cas à nouveau hello client a besoin adresse de hello toore résoudre. Fournissant hello précédente `ResolvedServicePartition` indique que hello tootry des besoins de programme de résolution à nouveau au lieu de simplement récupérer une adresse en mémoire cache.

En règle générale, le code client hello devez fonctionne pas avec hello ServicePartitionResolver directement. Elle est créée et passée sur les fabriques de client toocommunication Bonjour API des Services fiables. fabriques de Hello utilisent le programme de résolution hello en interne un objet client qui peut être toocommunicate utilisé avec les services de toogenerate.

### <a name="communication-clients-and-factories"></a>Fabriques et clients de communication
bibliothèque de fabrique de communication Hello implémente un modèle de nouvelle tentative de gestion d’erreurs standard qui facilite la nouvelle tentative points de terminaison de service tooresolved connexions. bibliothèque de fabrique Hello fournit le mécanisme de nouvelle tentative hello pendant que vous fournissez des gestionnaires d’erreurs hello.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`définit l’interface de base hello implémentée par une fabrique de client de communication qui produit des clients qui peuvent communiquer avec les services de Service Fabric tooa. Bonjour implémentation de hello que communicationclientfactory dépend de la pile de communication hello utilisé par le service de Service Fabric hello où le client de hello veut toocommunicate. Hello fiable API des Services fournit un `CommunicationClientFactoryBase<TCommunicationClient>`. Cela fournit une implémentation de base de l’interface de CommunicationClientFactory hello et effectue des tâches qui sont des piles de communication commun tooall hello. (Ces tâches incluent à l’aide d’un point de terminaison ServicePartitionResolver toodetermine hello). Les clients implémentent généralement hello abstraite CommunicationClientFactoryBase toohandle logique de la classe qui est la pile de communication toohello spécifique.

client de communication Hello simplement reçoit une adresse et il utilise le service de tooa tooconnect. client de la Hello peut utiliser tout protocole il veut.

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

fabrique de clients Hello est principalement responsable de la création de clients de communication. Pour les clients qui ne maintiennent pas une connexion permanente, tel qu’un client HTTP, la fabrique de hello doit uniquement toocreate et client de retour hello. Autres protocoles permettant de maintenir une connexion permanente, telles que certains protocoles binaire, doivent également être validés par hello fabrique toodetermine si la connexion de hello doit toobe recréée.  

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

Enfin, un gestionnaire d’exceptions est chargé de déterminer quel tootake action lorsqu’une exception se produit. Les exceptions sont classées en **reproductibles** et **non reproductibles**.

* **Non renouvelable** exceptions simplement obtient à nouveau levées toohello arrière appelant.
* Les exceptions **reproductibles** sont encore classées en **temporaires** et **non temporaires**.
  * **Transitoire** exceptions sont ceux qui peut simplement être tentée sans adresse de point de terminaison de service hello résoudre à nouveau. Il s’agit notamment des problèmes réseau temporaires ou réponses d’erreur service autre que ceux qui indiquent l’adresse de point de terminaison de service hello n’existe pas.
  * **Non transitoires** exceptions sont ceux qui nécessitent des toobe d’adresse du point de terminaison de service hello résolu à nouveau. Il s’agit notamment des exceptions qui indiquent le point de terminaison de service hello est inaccessible, indiquant le service de hello a été déplacé tooa autre nœud.

Hello `TryHandleException` prend une décision sur une exception donnée. Si elle **ne sait pas** le toomake décisions relatives à une exception, elle doit retourner **false**. Si elle **connaît** quel toomake de décision, il doit définir le résultat de hello en conséquence et retourner **true**.

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
### <a name="putting-it-all-together"></a>Exemple complet
Avec un `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, et `IExceptionHandler(C#) / ExceptionHandler(Java)` construit autour d’un protocole de communication, un `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` encapsule tous les éléments et fournit la gestion des erreurs de hello et boucle de résolution service partition adresse autour de ces composants.

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

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir un exemple de communication HTTP entre services, consultez cet [exemple de projet C# sur GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) ou cet [exemple de projet Java sur GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Appels de procédure distante avec Reliable Services à distance](service-fabric-reliable-services-communication-remoting.md)
* [API Web qui utilise OWIN dans Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Communication WCF à l’aide de Reliable Services](service-fabric-reliable-services-communication-wcf.md)
