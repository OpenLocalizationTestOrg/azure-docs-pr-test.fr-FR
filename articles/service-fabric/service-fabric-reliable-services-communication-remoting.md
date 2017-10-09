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
# <a name="service-remoting-with-reliable-services"></a>Communication à distance des services avec Reliable Services
Pour les services qui ne sont pas liés tooa le protocole de communication particulier ou de la pile, par exemple WebAPI, Windows Communication Foundation (WCF) ou d’autres, le framework de Services fiables hello fournit un tooquickly de mécanisme de communication à distance et facilement configurer l’appel de procédure distante pour les services.

## <a name="set-up-remoting-on-a-service"></a>Configuration de la communication à distance sur un service
La configuration de communication à distance pour un service s'effectue en deux étapes simples :

1. Créez une interface pour votre tooimplement de service. Cette interface définit les méthodes hello qui seront disponibles pour un appel de procédure distante sur votre service. les méthodes Hello doivent être retournant des tâches méthodes asynchrones. Hello interface doit implémenter `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal qui hello service dispose d’une interface de communication à distance.
2. Utilisez un écouteur de communication à distance dans votre service. Il s'agit d'une implémentation `ICommunicationListener` qui fournit des fonctionnalités de communication à distance. Hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` espace de noms contient une méthode d’extension,`CreateServiceRemotingListener` pour avec et sans état des services qui permettre être utilisé toocreate un écouteur de la communication à distance à l’aide de protocole de transport de la communication à distance par défaut hello.

Remarque : hello `Remoting` espace de noms est disponible comme package nuget distinct appelé`Microsoft.ServiceFabric.Services.Remoting` 

Par exemple, hello service sans état suivant expose une méthode unique de tooget « Hello World » via un appel de procédure distante.

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
> Hello arguments et hello retournent types dans l’interface de service hello peuvent être des types simples, complexes ou personnalisées, mais ils doivent être sérialisables par hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Méthodes d’appel de service distant
Appel de méthodes sur un service à l’aide de pile de communication à distance hello est effectuée à l’aide d’un service de toohello proxy local via hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe. Hello `ServiceProxy` méthode crée un proxy local à l’aide de hello même interface que hello service implémente. Avec ce serveur proxy, vous pouvez simplement appeler des méthodes sur les interface hello à distance.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

infrastructure de communication à distance Hello propage les exceptions levées au client du service de toohello hello. Logique, gestion des exceptions au client hello à l’aide de `ServiceProxy` peut gérer directement les exceptions hello service lève une exception.

## <a name="service-proxy-lifetime"></a>Durée de vie du proxy du service
Comme la création de proxy de service est une opération légère, l’utilisateur peut en créer autant de fois que nécessaire. Le proxy de service peut être réutilisé tant que l’utilisateur en a besoin. Utilisateur peut réutiliser hello proxy même en cas d’Exception. Chaque ServiceProxy contient intersites client utilisé toosend messages acheminement hello. Lors de l’appel d’API, nous avons toosee de contrôle interne si le client de communication utilisé est valide. En fonction de ce résultat, nous recréer client de communication hello. Par conséquent, les utilisateurs n’avez pas besoin serviceproxy toorecreate en cas d’Exception.

### <a name="serviceproxyfactory-lifetime"></a>Durée de vie de la fabrique ServiceProxyFactory
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) est une fabrique qui crée le proxy pour différentes interfaces de communication à distance. Si vous utilisez l’API ServiceProxy.Create pour la création du proxy, l’infrastructure crée hello singelton ServiceProxyFactory.
Il est utile toocreate une manuellement lorsque vous avez besoin de toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) propriétés.
La fabrique est une opération coûteuse. ServiceProxyFactory conserve le cache du client de communication.
Il est recommandé toocache ServiceProxyFactory aussi longtemps que possible.

## <a name="remoting-exception-handling"></a>Gestion des exceptions à distance
Tous les hello à distance d’exception levée par l’API de service, sont envoyées toohello précédent client comme AggregateException. RemoteExceptions doivent être sérialisables DataContract sinon [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) est levée toohello proxy API avec l’erreur de sérialisation hello qu’elle contient.

ServiceProxy gère toutes les exceptions de basculement pour la partition de service hello il est créé pour. Nouveau, il résout les points de terminaison hello si Failover Exceptions(Non-Transient Exceptions) et nouvelles tentatives appel hello avec le point de terminaison correct hello est. Le nombre de tentatives pour l’exception de basculement est illimité.
En cas de TransientExceptions, il réessaie uniquement appel de hello.

Les paramètres de nouvelle tentative par défaut sont fournis par [OperationRetrySettings]. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Utilisateur peut configurer ces valeurs en passant le constructeur de tooServiceProxyFactory OperationRetrySettings objet.

## <a name="next-steps"></a>Étapes suivantes
* [API Web avec OWIN dans Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Communication WCF avec Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Sécurisation des communications pour Reliable Services](service-fabric-reliable-services-secure-communication.md)
