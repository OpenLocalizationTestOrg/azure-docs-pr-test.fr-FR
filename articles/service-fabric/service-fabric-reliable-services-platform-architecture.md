---
title: architecture de service aaaReliable | Documents Microsoft
description: "Vue d’ensemble de l’architecture de Service fiable hello pour les services avec ou sans état"
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Architecture de services Reliable Services avec et sans état
Un service Reliable Service Azure Service Fabric peut être avec état ou sans état. Chaque type de service s’exécute au sein d’une architecture spécifique. Ces architectures sont décrites dans cet article.
Consultez hello [vue d’ensemble du Service fiable](service-fabric-reliable-services-introduction.md) pour plus d’informations sur les différences de hello entre les services avec ou sans état.

## <a name="stateful-reliable-services"></a>Services fiables avec état
### <a name="architecture-of-a-stateful-service"></a>Architecture d'un service avec état
![Graphique d’architecture d’un service avec état](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Service fiable avec état
Un Service fiable avec état peuvent dériver de hello StatefulService ou StatefulServiceBase classe. Les deux classes de base sont fournies par Service Fabric. Ils offrent différents niveaux de prise en charge et d’abstraction pour toointerface de service avec état hello avec Service Fabric--et tooparticipate en tant que service dans le cluster Service Fabric de hello.

StatefulService provient de StatefulServiceBase. StatefulServiceBase propose des services plus de souplesse, mais nécessite une compréhension plus de mécanismes internes de hello de Service Fabric.
Consultez hello [vue d’ensemble du Service fiable](service-fabric-reliable-services-introduction.md) et [l’utilisation avancée de Service fiable](service-fabric-reliable-services-advanced-usage.md) pour plus d’informations sur les spécificités de hello de l’écriture de services à l’aide des classes StatefulService et StatefulServiceBase de hello .

Les deux classes de base gérer la durée de vie hello et rôle d’implémentation de service hello. implémentation de service Hello peut substituer des méthodes virtuelles d’une classe de base si implémentation de service hello a toodo de travail à ces moments dans hello service mise en œuvre du cycle de vie--ou s’il veut toocreate un objet écouteur de communication. Notez que bien que l’implémentation d’un service peut implémenter son propre objet écouteur de communication exposition ICommunicationListener, dans le diagramme de hello ci-dessus, écouteur de communications hello est implémentée par le Service Fabric--comme hello d’implémentation de service utilise un écouteur de communication est implémentée par le Service Fabric.

Un Service fiable sans état utilise parti de tootake manager hello état fiable de collections fiables. Collections fiables sont des structures de données local qui sont hautement disponible toohello service--, elles sont toujours disponibles, quelle que soit le service de basculement. Chaque type de collection fiable est implémenté par un fournisseur d'état fiable.
Pour plus d’informations sur les collections fiables, consultez hello [présentation des regroupements fiable](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Fournisseurs et gestionnaire d'état fiable
Gestionnaire d’état fiable Hello est un objet hello qui gère les fournisseurs d’état fiable. Il a hello toocreate de fonctionnalités, supprimer, énumérer et assurez-vous que les fournisseurs d’état fiable hello sont persistantes et hautement disponible. Une instance de fournisseur d’état fiable représente une instance d’une structure de données persistante et hautement disponible, comme un dictionnaire ou une file d’attente.

Chaque fournisseur d’état fiable expose une interface qui est utilisée par un toointeract de service avec état avec un fournisseur d’état fiable hello. Par exemple, IReliableDictionary est utilisé toointerface dictionnaire fiable de hello, tandis que IReliableQueue est toointerface utilisé avec la file d’attente fiable de hello. Tous les fournisseurs d’état fiable implémentent l’interface de IReliableState hello.

Gestionnaire d’état fiable Hello possède une interface nommée IReliableStateManager, ce qui permet de tooit d’accès à partir d’un service avec état. Interfaces tooreliable des fournisseurs d’état sont retournées via IReliableStateManager.

Gestionnaire d’état fiable Hello utilise une architecture de plug-in afin que les nouveaux types de collections fiables peuvent être branchés dynamiquement.

dictionnaire de fiable Hello et file d’attente fiable sont appuient sur des implémentation hello de hautes performances, le contrôle de version du magasin différentielle.

### <a name="transactional-replicator"></a>Réplicateur transactionnel
composant du réplicateur transactionnel Hello est chargé de s’assurer qu’état hello d’un service (autrement dit, l’état hello dans le Gestionnaire d’état fiable hello et les collections fiable hello) est cohérente sur tous les réplicas exécutant hello service. Cela garantit également que l’état de hello est persistant dans le journal de hello. Bonjour interfaces de gestionnaire d’état fiable avec réplicateur transactionnel de hello via un mécanisme privé.

Réplicateur transactionnel de Hello utilise un état de toocommunicate de protocole réseau avec d’autres réplicas hello des instances de service afin que tous les réplicas ont des informations d’état à jour.

Réplicateur transactionnel de Hello utilise un enregistrement des informations d’état toopersist afin que les informations d’état hello survit processus ou nœud tombe en panne. journal de toohello interface Hello est via un mécanisme privé.

### <a name="log"></a>Journal
composant de journal Hello fournit un magasin persistant de hautes performances qui peut être optimisé pour l’écriture de toospinning ou disques SSD.  conception de Hello du journal de hello est pour le stockage persistant hello (autrement dit, les disques durs) toobe toohello local nœuds qui exécutent un service avec état hello. Cela permet à faible latence et un débit élevé, en tant que stockage persistant tooremote comparés, ce qui n’est pas local toohello nœud.

composant de journal Hello utilise plusieurs fichiers journaux. Il existe un fichier journal partagé au niveau du nœud qui utilisent de tous les réplicas comme il peut fournir une latence plus faible hello et un débit plus élevé pour le stockage des données d’état. Par défaut, les journaux partagés hello sont placé dans le répertoire de travail nœud hello Service Fabric, mais il peut également être configuré toobe placé sur un autre emplacement, dans l’idéal, sur un disque réservé pour que le journal de partagé hello. Chaque réplica pour le service de hello possède également un fichier journal dédié et hello dédié est stocké dans le répertoire de travail du service hello. Il n’existe aucun toobe de journal mécanisme tooconfigure hello dédié placé dans un autre emplacement.

journal partagé de Hello est une zone de transition pour les informations d’état du réplica hello, hello lors de fichier journal dédié est sa destination finale hello où elle est persistante. Dans cette conception, les informations d’état hello sont le premier fichier de journal partagé toohello écrite et puis déplacées tardivement toohello des fichiers journaux dédié en arrière-plan de hello. De cette façon, hello toohello écriture du journal partagé aurait latence la plus faible de hello et un débit plus élevé qui permet de progression toomake du service de hello plus rapidement.

Lit et écrit les journaux partagés toohello s’effectuent via direct d’espace toopreallocated e/s sur disque hello pour les fichiers journaux partagés hello. tooallow une utilisation optimale d’espace disque sur le lecteur de hello avec journaux dédiés, fichier journal dédié de hello est créé comme un fichier partiellement alloué NTFS. Notez que cela permettra un surapprovisionnement d’espace disque et hello du système d’exploitation affiche les fichiers de journal hello dédié à l’aide de beaucoup plus d’espace disque qui est réellement utilisée.

Un journal de toohello interface minimale en mode utilisateur, à l’exception de journal de hello est écrit comme un pilote en mode noyau. En tant qu’un pilote en mode noyau, journal de hello peut fournir des performances maximales de hello les services tooall qui l’utilisent.

Pour plus d’informations sur la configuration des journaux de hello, consultez [configuration des Services fiables avec état](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Service fiable sans état
### <a name="architecture-of-a-stateless-service"></a>Architecture d'un service sans état
![Graphique d’architecture d’un service sans état](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Service fiable sans état
Les implémentations de service sans état dérivent hello StatelessService ou StatelessServiceBase classe. Hello StatelessServiceBase classe permet plus de souplesse que hello StatelessService classe.
Les deux classes de base gérer la durée de vie hello et le rôle d’un service.

implémentation de service Hello peut substituer des méthodes virtuelles d’une classe de base si le service de hello a toodo de travail à ces moments dans le cycle de vie du service hello--ou s’il veut toocreate un objet écouteur de communication. Notez que bien que le service de hello peut implémenter son propre objet écouteur de communication exposition ICommunicationListener, dans le diagramme de hello ci-dessus, écouteur de communications hello est implémentée par l’infrastructure de Service, car l’implémentation de ce service utilise une communication écouteur qui est implémentée par le Service Fabric.

Consultez hello [vue d’ensemble du Service fiable](service-fabric-reliable-services-introduction.md) et [l’utilisation avancée de Service fiable](service-fabric-reliable-services-advanced-usage.md) pour plus d’informations sur les spécificités de hello de l’écriture de services à l’aide des classes de StatelessService et StatelessServiceBase hello .

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
Pour plus d'informations sur Service Fabric, consultez :

[Présentation du service fiable](service-fabric-reliable-services-introduction.md)

[Démarrage rapide](service-fabric-reliable-services-quick-start.md)

[Présentation des collections fiables](service-fabric-reliable-services-reliable-collections.md)

[Utilisation avancée du service fiable](service-fabric-reliable-services-advanced-usage.md)

[Configuration du service fiable](service-fabric-reliable-services-configuration.md)  

