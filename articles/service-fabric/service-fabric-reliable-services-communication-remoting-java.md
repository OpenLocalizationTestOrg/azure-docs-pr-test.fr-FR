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
# <a name="service-remoting-with-reliable-services"></a>Communication à distance des services avec Reliable Services
> [!div class="op_single_selector"]
> * [C# sur Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java sur Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

infrastructure de Services fiables Hello fournit un tooquickly de mécanisme de communication à distance et facilement configurer l’appel de procédure distante pour les services.

## <a name="set-up-remoting-on-a-service"></a>Configuration de la communication à distance sur un service
La configuration de communication à distance pour un service s'effectue en deux étapes simples :

1. Créez une interface pour votre tooimplement de service. Cette interface définit les méthodes hello qui sont disponibles pour un appel de procédure distante sur votre service. les méthodes Hello doivent être retournant des tâches méthodes asynchrones. Hello interface doit implémenter `microsoft.serviceFabric.services.remoting.Service` toosignal qui hello service dispose d’une interface de communication à distance.
2. Utilisez un écouteur de communication à distance dans votre service. Il s'agit d'une implémentation `CommunicationListener` qui fournit des fonctionnalités de communication à distance. `FabricTransportServiceRemotingListener`peut être utilisé toocreate un écouteur de la communication à distance à l’aide du protocole de transport de la communication à distance par défaut hello.

Par exemple, hello service sans état suivant expose une méthode unique de tooget « Hello World » via un appel de procédure distante.

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
> Hello et les arguments de hello retournent des types dans l’interface de service hello peuvent être des types simples, complexes ou personnalisées, mais ils doivent être sérialisables.
>
>

## <a name="call-remote-service-methods"></a>Méthodes d’appel de service distant
Appel de méthodes sur un service à l’aide de pile de communication à distance hello est effectuée à l’aide d’un service de toohello proxy local via hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe. Hello `ServiceProxyBase` méthode crée un proxy local à l’aide de hello même interface que hello service implémente. Avec ce serveur proxy, vous pouvez simplement appeler des méthodes sur les interface hello à distance.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

infrastructure de communication à distance Hello propage les exceptions levées au client du service de toohello hello. Logique, gestion des exceptions au client hello à l’aide de `ServiceProxyBase` peut gérer directement les exceptions hello service lève une exception.

## <a name="service-proxy-lifetime"></a>Durée de vie du proxy du service
Comme la création de proxy de service est une opération légère, l’utilisateur peut en créer autant de fois que nécessaire. Le proxy de service peut être réutilisé tant que l’utilisateur en a besoin. Utilisateur peut réutiliser hello proxy même en cas d’Exception. Chaque ServiceProxy contient des messages de communication client utilisé toosend acheminement hello. Lors de l’appel d’API, nous avons toosee de contrôle interne si le client de communication utilisé est valide. En fonction de ce résultat, nous recréer client de communication hello. Par conséquent, les utilisateurs n’avez pas besoin serviceproxy toorecreate en cas d’Exception.

### <a name="serviceproxyfactory-lifetime"></a>Durée de vie de la fabrique ServiceProxyFactory
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) est une fabrique qui crée un proxy pour différentes interfaces de communication à distance. Si vous utilisez l’API `ServiceProxyBase.create` pour la création du proxy, l’infrastructure crée ensuite un `FabricServiceProxyFactory`.
Il est utile toocreate une manuellement lorsque vous avez besoin de toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) propriétés.
La fabrique est une opération coûteuse. `FabricServiceProxyFactory` conserve le cache des clients de communication.
Il est préférable toocache `FabricServiceProxyFactory` aussi longtemps que possible.

## <a name="remoting-exception-handling"></a>Gestion des exceptions à distance
Tous les hello à distance d’exception levée par l’API de service, sont envoyés toohello précédent client sous la forme RuntimeException ou FabricException.

ServiceProxy gère toutes les exceptions de basculement pour la partition de service hello il est créé pour. Nouveau, il résout les points de terminaison hello si Failover Exceptions(Non-Transient Exceptions) et nouvelles tentatives appel hello avec le point de terminaison correct hello est. Le nombre de tentatives pour l’exception de basculement est illimité.
En cas de TransientExceptions, il réessaie uniquement appel de hello.

Les paramètres de nouvelle tentative par défaut sont fournis par [OperationRetrySettings]. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Utilisateur peut configurer ces valeurs en passant le constructeur de tooServiceProxyFactory OperationRetrySettings objet.

## <a name="next-steps"></a>Étapes suivantes
* [Sécurisation des communications pour Reliable Services](service-fabric-reliable-services-secure-communication.md)
