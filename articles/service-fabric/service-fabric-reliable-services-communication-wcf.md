---
title: Pile de communication WCF de Reliable Services | Documents Microsoft
description: "La pile de communication WCF intégrée dans Service Fabric fournit une communication WCF client-service pour Reliable Services."
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
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="40c23-103">Pile de communication WCF pour Reliable Services</span><span class="sxs-lookup"><span data-stu-id="40c23-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="40c23-104">L'infrastructure Reliable Services permet aux auteurs de service de choisir la pile de communication qu'ils souhaitent utiliser pour leur service.</span><span class="sxs-lookup"><span data-stu-id="40c23-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="40c23-105">Ils peuvent intégrer la pile de communication de leur choix par le biais du **ICommunicationListener** retourné à partir des méthodes [CreateServiceReplicaListeners ou CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) .</span><span class="sxs-lookup"><span data-stu-id="40c23-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="40c23-106">L'infrastructure fournit une implémentation de la pile de communication basée sur Windows Communication Foundation (WCF) pour les auteurs de service qui souhaitent utiliser une communication WCF.</span><span class="sxs-lookup"><span data-stu-id="40c23-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="40c23-107">Écouteur de communication WCF</span><span class="sxs-lookup"><span data-stu-id="40c23-107">WCF Communication Listener</span></span>
<span data-ttu-id="40c23-108">La classe **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** fournit l’implémentation WCF de **ICommunicationListener**.</span><span class="sxs-lookup"><span data-stu-id="40c23-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="40c23-109">Supposons que nous disposions d’un contrat de service de type `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="40c23-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="40c23-110">Nous pouvons créer un écouteur de communication WCF dans le service de la manière suivante.</span><span class="sxs-lookup"><span data-stu-id="40c23-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="40c23-111">Écriture de clients pour la pile de communication WCF</span><span class="sxs-lookup"><span data-stu-id="40c23-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="40c23-112">Pour l’écriture de clients communiquant avec les services à l’aide de la méthode WCF, l’infrastructure fournit **WcfClientCommunicationFactory**, qui est l’implémentation propre à WCF de [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="40c23-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="40c23-113">Le canal de communication WCF est accessible à partir du **WcfCommunicationClient** créé par **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="40c23-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="40c23-114">Le code client peut utiliser **WcfCommunicationClientFactory** avec **WcfCommunicationClient** qui implémente **ServicePartitionClient** pour déterminer le point de terminaison du service et communiquer avec le service.</span><span class="sxs-lookup"><span data-stu-id="40c23-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="40c23-115">L’élément ServicePartitionResolver par défaut suppose que le client s’exécute dans le même cluster que le service.</span><span class="sxs-lookup"><span data-stu-id="40c23-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="40c23-116">Dans le cas contraire, créez un objet ServicePartitionResolver et transmettez les points de terminaison de connexion du cluster.</span><span class="sxs-lookup"><span data-stu-id="40c23-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="40c23-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40c23-117">Next steps</span></span>
* [<span data-ttu-id="40c23-118">Appel de procédure distante avec Reliable Services à distance</span><span class="sxs-lookup"><span data-stu-id="40c23-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="40c23-119">API Web avec OWIN dans Reliable Services</span><span class="sxs-lookup"><span data-stu-id="40c23-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="40c23-120">Sécurisation des communications pour Reliable Services</span><span class="sxs-lookup"><span data-stu-id="40c23-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

