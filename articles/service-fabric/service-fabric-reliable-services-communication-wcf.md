---
title: pile de communication des Services WCF aaaReliable | Documents Microsoft
description: "pile de communication de WCF intégré Hello dans Service Fabric fournit la communication WCF de service du client pour les Services fiables."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="addf1-103">Pile de communication WCF pour Reliable Services</span><span class="sxs-lookup"><span data-stu-id="addf1-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="addf1-104">pile de communication hello toochoose auteurs qu’ils souhaitent toouse pour leur service de service Hello framework permet des Services fiables.</span><span class="sxs-lookup"><span data-stu-id="addf1-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="addf1-105">Il peuvent s’intégrer dans la pile de communication hello de leur choix via hello **ICommunicationListener** retourné à partir de hello [CreateServiceReplicaListeners ou CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) méthodes.</span><span class="sxs-lookup"><span data-stu-id="addf1-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="addf1-106">infrastructure de Hello fournit une implémentation de pile de communication hello selon hello Windows Communication Foundation (WCF) pour les auteurs de service qui souhaitent toouse communication basée sur WCF.</span><span class="sxs-lookup"><span data-stu-id="addf1-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="addf1-107">Écouteur de communication WCF</span><span class="sxs-lookup"><span data-stu-id="addf1-107">WCF Communication Listener</span></span>
<span data-ttu-id="addf1-108">implémentation de Hello spécifiques à WCF de **ICommunicationListener** est fournie par hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** classe.</span><span class="sxs-lookup"><span data-stu-id="addf1-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="addf1-109">Supposons que nous disposions d’un contrat de service de type `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="addf1-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="addf1-110">Nous pouvons créer un écouteur de communication WCF Bonjour de service hello suivant manière.</span><span class="sxs-lookup"><span data-stu-id="addf1-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="addf1-111">Écriture de clients pour la pile de communication WCF hello</span><span class="sxs-lookup"><span data-stu-id="addf1-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="addf1-112">Pour écrire des clients toocommunicate avec les services à l’aide de WCF, le framework de hello fournit **WcfClientCommunicationFactory**, qui est l’implémentation hello spécifiques à WCF de [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="addf1-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="addf1-113">canal de communication WCF Hello est accessible à partir de hello **WcfCommunicationClient** créé par hello **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="addf1-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="addf1-114">Le code client peut utiliser hello **WcfCommunicationClientFactory** avec hello **WcfCommunicationClient** qui implémente **ServicePartitionClient** toodetermine Hello du point de terminaison de service et communiquer avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="addf1-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="addf1-115">la valeur par défaut de Hello ServicePartitionResolver suppose que le client hello est en cours d’exécution dans le même cluster en tant que service de hello.</span><span class="sxs-lookup"><span data-stu-id="addf1-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="addf1-116">Si c'est-à-dire pas hello cas, créez un objet ServicePartitionResolver et passer dans les points de terminaison de connexion hello cluster.</span><span class="sxs-lookup"><span data-stu-id="addf1-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="addf1-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="addf1-117">Next steps</span></span>
* [<span data-ttu-id="addf1-118">Appel de procédure distante avec Reliable Services à distance</span><span class="sxs-lookup"><span data-stu-id="addf1-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="addf1-119">API Web avec OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="addf1-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="addf1-120">Sécurisation des communications pour Reliable Services</span><span class="sxs-lookup"><span data-stu-id="addf1-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

