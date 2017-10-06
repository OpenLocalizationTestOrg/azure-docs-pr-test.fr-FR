---
title: "aaaAzure Service Fabric, vue d’ensemble de la gestion des API | Documents Microsoft"
description: Cet article est une introduction de toousing gestion des API Azure comme une application de Service Fabric tooyour passerelle.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Vue d’ensemble d’Azure Service Fabric avec Gestion des API

Les applications de cloud doivent généralement un tooprovide passerelle frontale un point d’entrée unique pour les utilisateurs, appareils ou d’autres applications. Dans Service Fabric, une passerelle peut être n’importe quel service sans état, comme une [application ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), ou un autre service conçu pour l’entrée de trafic, par exemple les [concentrateurs d’événements](https://docs.microsoft.com/azure/event-hubs/), [IoT Hub](https://docs.microsoft.com/azure/iot-hub/) ou [Gestion des API Azure](https://docs.microsoft.com/azure/api-management/).

Cet article est une introduction de toousing gestion des API Azure comme une application de Service Fabric tooyour passerelle. Gestion des API s’intègre directement à l’infrastructure de Service, ce qui vous toopublish API avec un ensemble complet de services de Fabric du Service routage règles tooyour back-end. 

## <a name="architecture"></a>Architecture
Une architecture commune de l’infrastructure de Service utilise une application d’une page web qui rend les appels HTTP des services de tooback-end qui exposent APIs HTTP. Hello [Service Fabric route exemple d’application](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) montre un exemple de cette architecture.

Dans ce scénario, un service web sans état sert de passerelle de hello en hello application Service Fabric. Cette approche, vous toowrite un service web qui peut le proxy HTTP demande des services de tooback-end, comme indiqué dans hello suivant schéma :

![Vue d’ensemble de la topologie Service Fabric avec Gestion des API][sf-web-app-stateless-gateway]

Comme les applications de croître en complexité, afin de hello passerelles qui doivent présenter une API devant une multitude services back-end. Gestion des API Azure est conçue toohandle API complexes avec des règles de routage, contrôle d’accès, limitation du débit, surveillance, la journalisation des événements et la réponse mise en cache avec un minimum de travail. Gestion des API Azure prend en charge la découverte du service Service Fabric, une résolution de partition, et itinéraire de réplication Sélection toointelligently demande directement tooback-end services dans l’infrastructure de Service, vous n’avez toowrite votre propre passerelle API sans état. 

Dans ce scénario, hello web de que l’interface utilisateur est toujours desservie via un service web, tandis que les appels API HTTP sont gérés et routés via la gestion des API Azure, comme indiqué dans hello suivant schéma :

![Vue d’ensemble de la topologie Service Fabric avec Gestion des API][sf-apim-web-app]

## <a name="application-scenarios"></a>Scénarios d’application

Les services de Service Fabric peuvent être sans état ou avec état, et ils peuvent être partitionnés selon l’un des trois modèles : singleton, plage Int64, et nommé. La résolution du point de terminaison de service requiert l’identification d’une partition spécifique d’une instance de service spécifique. Lors de la résolution d’un point de terminaison d’un service, les deux hello nom d’instance de service (par exemple, `fabric:/myapp/myservice`) ainsi que la partition spécifique de hello du service de hello doit être spécifiée, sauf dans les cas de hello de partition de singleton.

Gestion des API Azure peut être utilisée avec n’importe quelle combinaison de services sans état, services avec état et schéma de partition.

## <a name="send-traffic-tooa-stateless-service"></a>Envoyer le trafic tooa sans état

Dans le cas le plus simple hello, le trafic est transféré à l’instance du service sans état tooa. tooachieve, une opération de gestion des API contient une stratégie du traitement entrant avec un Service Fabric back-end qui mappe l’instance de service sans état spécifique tooa dans hello Service Fabric principal. Les demandes envoyées toothat service sont envoyés tooa de réplica aléatoire de l’instance de service sans état hello.

#### <a name="example"></a>Exemple
Bonjour scénario, une application de Service Fabric contient un service sans état nommé `fabric:/app/fooservice`, qui expose une API HTTP interne. nom de l’instance service Hello est bien connu et peut être codées en dur directement dans hello traitement entrant de gestion des API de la stratégie. 

![Vue d’ensemble de la topologie Service Fabric avec Gestion des API][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Envoyer le trafic tooa avec état

Scénario de service sans état toohello similaire, le trafic peut être transféré tooa l’instance du service avec état. Dans ce cas, une opération de gestion des API contient une stratégie du traitement entrant avec un Service Fabric back-end qui mappe une partition spécifique de tooa de demande d’une spécifique *avec état* instance de service. toomap de partition Hello chaque toois demande calculée via une méthode d’expression lambda à l’aide des entrées de hello demande HTTP entrante, telle qu’une valeur dans le chemin d’accès des URL hello. stratégie de Hello peut être configuré toosend demandes toohello réplica principal uniquement, ou tooa aléatoire réplica pour les opérations de lecture.

#### <a name="example"></a>Exemple

Bonjour scénario, une application de Service Fabric contient un service avec état partitionné nommé `fabric:/app/userservice` qui expose une API HTTP interne. nom de l’instance service Hello est bien connu et peut être codées en dur directement dans hello traitement entrant de gestion des API de la stratégie.  

Hello service est partitionné à l’aide du schéma de partition hello Int64 avec deux partitions et une plage de clés qui s’étend sur `Int64.MinValue` trop`Int64.MaxValue`. stratégie de serveur principal Hello calcule une clé de partition dans la plage en convertissant hello `id` la valeur fournie pour hello URL demande chemin d’accès tooa entier 64 bits, bien que n’importe quel algorithme peut être la clé de partition hello utilisé toocompute ici. 

![Vue d’ensemble de la topologie Service Fabric avec Gestion des API][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>Envoyer le trafic toomultiple les services sans état

Dans les scénarios plus avancés, vous pouvez définir une opération de gestion des API que les cartes de demandes toomore à une instance d’un service. Dans ce cas, chaque opération contient une stratégie qui mappe des demandes d’instance de service spécifique tooa selon les valeurs à partir de hello demande HTTP entrante, tels que chaîne de chemin d’accès ou de requête URL hello et en cas de hello de services avec état, une partition dans l’instance de service hello . 

tooachieve cela, une gestion des API opération contient une stratégie du traitement entrant avec un Service Fabric back-end qui mappe l’instance de service sans état tooa dans hello Service Fabric principal en fonction des valeurs récupérées à partir de la demande HTTP entrante hello. Instance de service tooa demandes sont envoyées réplica aléatoire de tooa hello des instances de service.

#### <a name="example"></a>Exemple

Dans cet exemple, une nouvelle instance de service sans état est créée pour chaque utilisateur d’une application avec un nom généré de manière dynamique à l’aide de hello formule suivante :
 
 - `fabric:/app/users/<username>`

 Chaque service a un nom unique, mais les noms hello ne sont pas connus initial, car les services de hello sont créés dans la réponse toouser ou administrateur d’entrée et par conséquent ne peut pas être codées en dur dans les stratégies APIM ou des règles de routage. Au lieu de cela, nom hello de hello service toowhich toosend une demande est générée dans la définition de stratégie principal hello de hello `name` la valeur fournie pour le chemin d’accès de la demande hello URL. Par exemple :

  - Une requête trop`/api/users/foo` est routé tooservice instance`fabric:/app/users/foo`
  - Une requête trop`/api/users/bar` est routé tooservice instance`fabric:/app/users/bar`

![Vue d’ensemble de la topologie Service Fabric avec Gestion des API][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>Envoyer le trafic toomultiple les services avec état

Exemple de service sans état toohello similaire, une gestion des API opération capable de mapper les demandes toomore à un **avec état** instance de service, auquel cas vous également peut-être tooperform une résolution de partition pour chaque service avec état instance.

tooachieve cela, une gestion des API opération contient une stratégie du traitement entrant avec un Service Fabric back-end qui mappe l’instance de service avec état tooa dans hello Service Fabric principal en fonction des valeurs récupérées à partir de la demande HTTP entrante hello. En outre toomapping une instance de service demande toospecific, demande de hello peut également être mappé tooa de partition spécifique au sein de l’instance de service hello et éventuellement de réplica principal de tooeither hello ou un réplica secondaire aléatoire au sein de la partition de hello.

#### <a name="example"></a>Exemple

Dans cet exemple, une nouvelle instance de service avec état est créée pour chaque utilisateur de l’application hello avec un nom généré de manière dynamique à l’aide de hello formule suivante :
 
 - `fabric:/app/users/<username>`

 Chaque service a un nom unique, mais les noms hello ne sont pas connus initial, car les services de hello sont créés dans la réponse toouser ou administrateur d’entrée et par conséquent ne peut pas être codées en dur dans les stratégies APIM ou des règles de routage. Au lieu de cela, nom hello de hello service toowhich toosend une demande est générée dans la définition de stratégie principal hello de hello `name` le chemin d’accès de valeur fourni hello URL demande. Par exemple :

  - Une requête trop`/api/users/foo` est routé tooservice instance`fabric:/app/users/foo`
  - Une requête trop`/api/users/bar` est routé tooservice instance`fabric:/app/users/bar`

Chaque instance de service est partitionné également à l’aide du schéma de partition hello Int64 avec deux partitions et une plage de clés qui s’étend sur `Int64.MinValue` trop`Int64.MaxValue`. stratégie de serveur principal Hello calcule une clé de partition dans la plage en convertissant hello `id` la valeur fournie pour hello URL demande chemin d’accès tooa entier 64 bits, bien que n’importe quel algorithme peut être la clé de partition hello utilisé toocompute ici. 

![Vue d’ensemble de la topologie Service Fabric avec Gestion des API][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>Étapes suivantes

Suivez hello [guide de démarrage rapide](service-fabric-api-management-quick-start.md) tooset de votre premier Service Fabric cluster associé à l’API de gestion et le flux des demandes via les services de gestion des API tooyour.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png