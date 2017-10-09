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
# <a name="wcf-based-communication-stack-for-reliable-services"></a>Pile de communication WCF pour Reliable Services
pile de communication hello toochoose auteurs qu’ils souhaitent toouse pour leur service de service Hello framework permet des Services fiables. Il peuvent s’intégrer dans la pile de communication hello de leur choix via hello **ICommunicationListener** retourné à partir de hello [CreateServiceReplicaListeners ou CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) méthodes. infrastructure de Hello fournit une implémentation de pile de communication hello selon hello Windows Communication Foundation (WCF) pour les auteurs de service qui souhaitent toouse communication basée sur WCF.

## <a name="wcf-communication-listener"></a>Écouteur de communication WCF
implémentation de Hello spécifiques à WCF de **ICommunicationListener** est fournie par hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** classe.

Supposons que nous disposions d’un contrat de service de type `ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

Nous pouvons créer un écouteur de communication WCF Bonjour de service hello suivant manière.

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

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>Écriture de clients pour la pile de communication WCF hello
Pour écrire des clients toocommunicate avec les services à l’aide de WCF, le framework de hello fournit **WcfClientCommunicationFactory**, qui est l’implémentation hello spécifiques à WCF de [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

canal de communication WCF Hello est accessible à partir de hello **WcfCommunicationClient** créé par hello **WcfCommunicationClientFactory**.

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

Le code client peut utiliser hello **WcfCommunicationClientFactory** avec hello **WcfCommunicationClient** qui implémente **ServicePartitionClient** toodetermine Hello du point de terminaison de service et communiquer avec le service de hello.

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
> la valeur par défaut de Hello ServicePartitionResolver suppose que le client hello est en cours d’exécution dans le même cluster en tant que service de hello. Si c'est-à-dire pas hello cas, créez un objet ServicePartitionResolver et passer dans les points de terminaison de connexion hello cluster.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Appel de procédure distante avec Reliable Services à distance](service-fabric-reliable-services-communication-remoting.md)
* [API Web avec OWIN dans Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Sécurisation des communications pour Reliable Services](service-fabric-reliable-services-secure-communication.md)

