---
title: aaaOverview de hello du cycle de vie des Services fiables de Azure Service Fabric | Documents Microsoft
description: "En savoir plus sur les événements de cycle de vie différent hello dans les services fiables Service Fabric"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Vue d’ensemble du cycle de vie de Reliable Services
> [!div class="op_single_selector"]
> * [C# sur Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java sur Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Quand vous réfléchissez à hello de cycles de vie des Services fiables, principes de base hello du cycle de vie hello sont hello plus importante. En général :

- Lors du démarrage
  - Les services sont construits
  - Ils ont une tooconstruct opportunité et retournent zéro ou plusieurs écouteurs
  - Tous les écouteurs retournés sont ouverte, ce qui permet la communication avec le service hello
  - RunAsync du Service Hello méthode est appelée, ce qui permet de hello toodo à long terme de service ou travail d’arrière-plan
- Lors de l’arrêt
  - tooRunAsync passé jeton d’annulation Hello est annulée et les écouteurs hello sont fermées.
  - Une fois cette opération terminée, objet de service hello lui-même est détruite

Il n’y a plus d’informations sur hello exact de classement de ces événements. En particulier, commande hello d’événements peut varier légèrement selon que hello Service fiable est sans état ou avec état. En outre, pour les services avec état, nous avons toodeal avec le scénario principal swap hello. Au cours de cette séquence, rôle hello des principaux est transféré tooanother réplica (ou est restauré) sans arrêt du service hello. Enfin, nous avons toothink sur les conditions d’erreur ou d’échec.

## <a name="stateless-service-startup"></a>Démarrage de service sans état
Hello de cycle de vie d’un service sans état est assez simple. Voici l’ordre hello des événements :

1. Hello Service est construit
2. Ensuite, deux choses se produisent en parallèle :
    - `StatelessService.CreateServiceInstanceListeners()` est appelé et les écouteurs retournés sont ouverts. `ICommunicationListener.OpenAsync()` est appelé sur chaque écouteur.
    - Hello du service `StatelessService.RunAsync()` méthode est appelée.
3. Le cas échéant, hello du service `StatelessService.OnOpenAsync()` méthode est appelée. Il s’agit d’un remplacement rare, mais possible.

Il est important toonote qu’il n’existe aucun classement entre hello appels toocreate et les écouteurs hello ouvert et RunAsync. les écouteurs Hello peut s’ouvrir avant le démarrage de RunAsync. De même, RunAsync peut finir appelé avant que les écouteurs de communication hello sont ouverts, ou même ont été construits. Si aucune synchronisation n’est requise, elle est considérée comme un implémenteur de toohello exercice. Solutions courantes :

  - Parfois, les écouteurs ne peuvent pas fonctionner avant que d’autres informations ne soient créées ou un travail effectué. Pour les services sans état qui sont actifs, cela peut se faire dans d’autres emplacements, tels que les suivants : 
    - dans le constructeur du service hello
    - au cours de hello `CreateServiceInstanceListeners()` appeler
    - dans le cadre de la construction de hello d’écouteur hello lui-même
  - Parfois hello code dans RunAsync ne veut pas toostart jusqu'à ce que les écouteurs hello sont ouverts. Dans ce cas, une coordination supplémentaire est nécessaire. Une solution courante consiste à certains indicateur dans les écouteurs hello indiquant quand elles sont terminées. Cet indicateur est alors vérifié dans RunAsync avant de poursuivre le travail de tooactual.

## <a name="stateless-service-shutdown"></a>Arrêt de service sans état
Lorsque vous arrêtez un service sans état, hello même modèle est suivi, dans le sens inverse :

1. En parallèle
    - Tous les écouteurs sont fermés. `ICommunicationListener.CloseAsync()` est appelé sur chaque écouteur.
    - jeton d’annulation Hello passé trop`RunAsync()` est annulée. Du jeton de vérification hello annulation `IsCancellationRequested` propriété retourne la valeur est true et si elle est appelée du jeton hello `ThrowIfCancellationRequested` méthode lève une exception une `OperationCanceledException`.
2. Une fois `CloseAsync()` se termine sur chaque port d’écoute et `RunAsync()` termine également du service hello `StatelessService.OnCloseAsync()` méthode est appelée, le cas échéant. Il est rare toooverride `StatelessService.OnCloseAsync()`.
3. Après avoir `StatelessService.OnCloseAsync()` terminée, objet de service hello est détruite.

## <a name="stateful-service-startup"></a>Démarrage de service avec état
Les services avec état ont un modèle toostateless des services similaires, avec quelques modifications. Lors du démarrage d’un service avec état, hello ordre des événements est comme suit :

1. Hello Service est construit
2. `StatefulServiceBase.OnOpenAsync()` est appelée. Il est substitué uncommonly dans le service hello.
3. Hello événements suivants se produisent en parallèle
    - `StatefulServiceBase.CreateServiceReplicaListeners()` est appelé. 
      - Si le service de hello est un serveur principal, tous les écouteurs retournés sont ouverts. `ICommunicationListener.OpenAsync()` est appelé sur chaque écouteur.
      - Si le service de hello est une base de données secondaire, que ces écouteurs marqué comme `ListenOnSecondary = true` sont ouverts. Il est plus rare d’avoir des écouteurs ouverts dans les réplicas secondaires.
    - Hello si hello Service est actuellement un service principal, hello `StatefulServiceBase.RunAsync()` méthode est appelée.
4. Une fois que tous les hello de l’écouteur du réplica `OpenAsync()` appelle et `RunAsync()` est appelée, `StatefulServiceBase.OnChangeRoleAsync()` est appelée. Il est substitué uncommonly dans le service hello.

De même toostateless services, il n’existe aucune coordination entre la commande hello dans le hello écouteurs sont créés et ouvert et lorsque RunAsync est appelée. Si vous avez besoin de coordination, les solutions de hello sont bien hello même. Il existe un cas supplémentaire : dire que les appels de hello arrivent sur les écouteurs de communication hello nécessitent informations conservées à l’intérieur de certains [fiable Collections](service-fabric-reliable-services-reliable-collections.md). Étant donné que les écouteurs de communication hello pu ouvrir avant que les collections fiable hello sont accessibles en lecture ou en écriture, et avant RunAsync a pu démarrer, certains coordination supplémentaire est nécessaire. solution la plus simple et le plus courante de Hello concerne hello communication écouteurs tooreturn qui hello client utilise tooknow tooretry hello demande un code d’erreur.

## <a name="stateful-service-shutdown"></a>Arrêt de service avec état
De même tooStateless services, événements de cycle de vie hello lors de l’arrêt sont hello même pendant le démarrage, mais inversée. Lorsqu’un service avec état est en cours d’arrêt, hello événements suivants se produisent :

1. En parallèle
    - Tous les écouteurs sont fermés. `ICommunicationListener.CloseAsync()` est appelé sur chaque écouteur.
    - jeton d’annulation Hello passé trop`RunAsync()` est annulée. Du jeton de vérification hello annulation `IsCancellationRequested` propriété retourne la valeur est true et si elle est appelée du jeton hello `ThrowIfCancellationRequested` méthode lève une exception une `OperationCanceledException`.
2. Une fois `CloseAsync()` se termine sur chaque port d’écoute et `RunAsync()` termine également du service hello `StatefulServiceBase.OnChangeRoleAsync()` est appelée. (Cela est uncommonly substituée dans le service hello.)
    - En attente de RunAsync toocomplete est nécessaire uniquement si ce réplica de service a été principal.
3. Une fois hello `StatefulServiceBase.OnChangeRoleAsync()` méthode se termine, hello `StatefulServiceBase.OnCloseAsync()` méthode est appelée. Il s’agit d’un remplacement rare, mais possible.
3. Après avoir `StatefulServiceBase.OnCloseAsync()` terminée, objet de service hello est détruite.

## <a name="stateful-service-primary-swaps"></a>Échanges de réplica principal de service avec état
Pendant l’exécution d’un service avec état, hello réplicas principaux du que les services avec état suffit leurs écouteurs de communication ouverts et leur méthode RunAsync appelée. Les réplicas secondaires sont construits mais ne reçoivent aucun autre appel. Pendant l’exécution toutefois un service avec état, quel réplica est actuellement hello principal peut modifier. Que cela signifie en termes d’événements de cycle de vie hello capable de détecter un réplica ? Hello comportement hello réplica avec état consulte dépend s’il s’agit de réplica de hello est rétrogradé ou promue au cours de l’échange de hello.

### <a name="for-hello-primary-being-demoted"></a>Pourquoi principal qui est rétrogradé.
Service Fabric a besoin de cette toostop réplica le traitement des messages et quittez n’importe quel travail d’arrière-plan qu'il fait. Par conséquent, ce service de hello étape apparemment similaires toowhen est en cours d’arrêt. Une différence est que hello Service n’est pas détruite ou fermé, car il demeure sous la forme d’une base de données secondaire. Hello suivant API est appelée :

1. En parallèle
    - Tous les écouteurs sont fermés. `ICommunicationListener.CloseAsync()` est appelé sur chaque écouteur.
    - jeton d’annulation Hello passé trop`RunAsync()` est annulée. Du jeton de vérification hello annulation `IsCancellationRequested` propriété retourne la valeur est true et si elle est appelée du jeton hello `ThrowIfCancellationRequested` méthode lève une exception une `OperationCanceledException`.
2. Une fois `CloseAsync()` se termine sur chaque port d’écoute et `RunAsync()` termine également du service hello `StatefulServiceBase.OnChangeRoleAsync()` est appelée. Il est substitué uncommonly dans le service hello.

### <a name="for-hello-secondary-being-promoted"></a>Pourquoi secondaire en cours de promotion
De même, le Service Fabric a besoin de cette toostart de réplica à l’écoute des messages sur le câble de hello et démarrer toutes les tâches en arrière-plan qu'il reconnaît les. Par conséquent, cette recherche de processus similaires service de hello toowhen est créé, à l’exception de ce réplica hello lui-même existe déjà. Hello suivant API est appelée :

1. En parallèle
    - `StatefulServiceBase.CreateServiceReplicaListeners()` est appelé et les écouteurs retournés sont ouverts. `ICommunicationListener.OpenAsync()` est appelé sur chaque écouteur.
    - Hello du service `StatefulServiceBase.RunAsync()` méthode est appelée.
2. Une fois que tous les hello de l’écouteur du réplica `OpenAsync()` appelle et `RunAsync()` a été appelée, `StatefulServiceBase.OnChangeRoleAsync()` est appelée. Il est substitué uncommonly dans le service hello.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Problèmes courants se produisant pendant l’arrêt d’un service avec état et la rétrogradation du réplica principal
Modifications de service Fabric hello principal d’un service avec état pour diverses raisons. Hello plus courantes sont [cluster rééquilibrage](service-fabric-cluster-resource-manager-balancing.md) et [mise à niveau de l’application](service-fabric-application-upgrade.md). Pendant ces opérations (ainsi que lors de l’arrêt normal du service, que vous verriez si le service de hello a été supprimé), il est important que hello égard du service hello `CancellationToken`. Les services qui ne gèrent pas l’annulation « proprement » seront confrontés à plusieurs problèmes. En particulier, ces opérations sera lentes, car le Service Fabric attend hello services toostop en douceur. Cela peut entraîner des mises à niveau toofailed ce délai d’attente finalement et l’annulation. Jeton d’annulation échec toohonor hello peut également provoquer des clusters déséquilibrés, car les nœuds obtenir à chaud, mais les services hello ne peut pas être rééquilibrées, car il prend trop de temps toomove les ailleurs. 

Étant donné que les services de hello sont avec état, il est également probable qu’ils utilisent hello [fiable Collections](service-fabric-reliable-services-reliable-collections.md). Dans l’infrastructure de Service, lorsqu’un serveur principal est rétrogradé, une des choses de première hello qui se produit est que l’état de l’accès en écriture toohello sous-jacent est révoqué. Cela conduit tooa deuxième ensemble de problèmes qui peuvent avoir un impact sur le cycle de vie hello service. collections Hello retournées Exceptions basées sur le minutage de hello et indique si les réplicas hello est déplacé ou l’arrêt. Ces exceptions doivent être gérées correctement. Les exceptions levées par Service Fabric sont soit permanentes [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet), soit passagères [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet). Exceptions permanentes doivent être connectées et levées, alors que les exceptions transitoires hello peuvent être retentées selon une logique de nouvelle tentative.

La gestion des exceptions hello provenant de l’utilisation de hello `ReliableCollections` conjointement avec les événements du cycle de vie du service est une partie importante de test et la validation d’un Service fiable. Hello recommandation n’est toujours toorun le service sous charge lors de l’exécution des mises à niveau et [chaos test](service-fabric-controlled-chaos.md) avant de déployer des tooproduction jamais. Ces étapes de base vous permettent de vérifier que votre service est correctement implémenté et qu’il gère correctement les événements de cycle de vie.


## <a name="notes-on-service-lifecycle"></a>Remarques sur le cycle de vie du service
  - Les deux hello `RunAsync()` méthode et hello `CreateServiceReplicaListeners/CreateServiceInstanceListeners` appels sont facultatifs. Un service peut avoir l’un des deux, les deux ou aucun. Par exemple, si le service de hello ne tout le travail dans les appels de toouser de réponse, il est inutile pour qu’il tooimplement `RunAsync()`. Que les écouteurs de communication hello et son code associé sont nécessaires. De même, créer et de retourner des écouteurs de communication sont facultative, comme hello service devra peut-être uniquement en arrière-plan toodo de travail et seulement doit tooimplement`RunAsync()`
  - Il n’est valide pour un service toocomplete `RunAsync()` avec succès et le retour à partir de celui-ci. Le fait qu’il se termine ne correspond pas à une condition d’échec. Fin de `RunAsync()` indique que le travail d’arrière-plan hello du service de hello est terminée. Pour les services fiables avec état, `RunAsync()` est rappelée si les réplicas hello ont été rétrogradé de tooSecondary principal et ensuite promu tooPrimary précédent.
  - Si un service quitte `RunAsync()` en levant une exception inattendue, il s’agit d’un échec. objet de service Hello est arrêté et une erreur d’intégrité est signalée.
  - Il n’existe aucune limite de temps au retour de ces méthodes, vous immédiatement perdez hello capacité toowrite tooReliable Collections et par conséquent ne peut pas se terminer tout travail réel. Il est recommandé de retourner aussi rapidement que possible lors de la réception de demande d’annulation hello. Si votre service ne répond pas les appels d’API de toothese dans un délai raisonnable que service Fabric peut forcer mettre fin à votre service. En général, cela se produit uniquement lors de mises à niveau d’application ou lorsqu’un service est en cours de suppression. Par défaut, ce délai d’attente est de 15 minutes.
  - Échecs Bonjour `OnCloseAsync()` résultat du chemin d’accès dans `OnAbort()` appelée qui est une opportunité de meilleur effort dernière chance pour hello service tooclean des et libérer toutes les ressources qu’ils ont demandé.

## <a name="next-steps"></a>Étapes suivantes
- [Introduction tooReliable Services](service-fabric-reliable-services-introduction.md)
- [Démarrage rapide de Reliable Services](service-fabric-reliable-services-quick-start.md)
- [Utilisation avancée de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
