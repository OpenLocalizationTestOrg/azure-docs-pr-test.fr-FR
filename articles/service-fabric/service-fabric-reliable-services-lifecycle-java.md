---
title: aaaOverview de hello du cycle de vie des Services fiables de Azure Service Fabric | Documents Microsoft
description: "En savoir plus sur les événements de cycle de vie différent hello dans les services fiables Service Fabric"
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
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

* Lors du démarrage
  * Les services sont construits
  * Ils ont une tooconstruct opportunité et retournent zéro ou plusieurs écouteurs
  * Tous les écouteurs retournés sont ouverte, ce qui permet la communication avec le service hello
  * du Service Hello runAsync est appelée, permettant de hello toodo de service à long terme ou de travail d’arrière-plan
* Lors de l’arrêt
  * toorunAsync passé jeton d’annulation Hello est annulée et les écouteurs hello sont fermées.
  * Une fois cette opération terminée, objet de service hello lui-même est détruite

Il n’y a plus d’informations sur hello exact de classement de ces événements. En particulier, commande hello d’événements peut varier légèrement selon que hello Service fiable est sans état ou avec état. En outre, pour les services avec état, nous avons toodeal avec le scénario principal swap hello. Au cours de cette séquence, rôle hello des principaux est transféré tooanother réplica (ou est restauré) sans arrêt du service hello. Enfin, nous avons toothink sur les conditions d’erreur ou d’échec.

## <a name="stateless-service-startup"></a>Démarrage de service sans état
Hello de cycle de vie d’un service sans état est assez simple. Voici l’ordre hello des événements :

1. Hello Service est construit
2. Ensuite, deux choses se produisent en parallèle :
    - `StatelessService.createServiceInstanceListeners()` est appelée et les écouteurs retournés sont ouverts (`CommunicationListener.openAsync()` est appelée sur chaque écouteur)
    - méthode de runAsync du service de Hello (`StatelessService.runAsync()`) est appelé
3. Le cas échéant, méthode d’onOpenAsync hello du service est appelée (plus précisément, `StatelessService.onOpenAsync()` est appelée. Il s’agit d’un remplacement rare, mais il est disponible).

Il est important toonote qu’il n’existe aucun classement entre hello appels toocreate et les écouteurs hello ouvert et runAsync. les écouteurs Hello peut s’ouvrir avant le démarrage de runAsync. De même, runAsync peut finir appelé avant que les écouteurs de communication hello sont ouverts, ou même ont été construits. Si aucune synchronisation n’est requise, elle est considérée comme un implémenteur de toohello exercice. Solutions courantes :

* Parfois, les écouteurs ne peuvent pas fonctionner avant que d’autres informations ne soient créées ou un travail effectué. Pour les services sans état qui travail peut se faire dans le constructeur du service hello pendant hello `createServiceInstanceListeners()` appeler, ou dans le cadre de la construction de hello d’écouteur hello lui-même.
* Parfois hello code dans runAsync ne veut pas toostart jusqu'à ce que les écouteurs hello sont ouverts. Dans ce cas, une coordination supplémentaire est nécessaire. Une solution courante consiste à certains indicateur dans les écouteurs hello indiquant quand ils ont terminé, qui est sélectionné dans runAsync avant de poursuivre le travail de tooactual.

## <a name="stateless-service-shutdown"></a>Arrêt de service sans état
Lorsque vous arrêtez un service sans état, hello même modèle est suivi, dans le sens inverse :

1. En parallèle
    - Les écouteurs ouverts sont fermés (`CommunicationListener.closeAsync()` est appelée sur chaque écouteur)
    - jeton d’annulation Hello passé trop`runAsync()` est annulée (vérification du jeton d’annulation hello `isCancelled` propriété retourne la valeur est true et si elle est appelée du jeton hello `throwIfCancellationRequested` méthode lève une exception un `CancellationException`)
2. Une fois `closeAsync()` se termine sur chaque port d’écoute et `runAsync()` termine également du service hello `StatelessService.onCloseAsync()` méthode est appelée, le cas échéant (c’est à nouveau un remplacement rare).
3. Après avoir `StatelessService.onCloseAsync()` terminée, objet de service hello est détruite.

## <a name="notes-on-service-lifecycle"></a>Remarques sur le cycle de vie du service
* Les deux hello `runAsync()` méthode et hello `createServiceInstanceListeners` appels sont facultatifs. Un service peut avoir l’un des deux, les deux ou aucun. Par exemple, si le service de hello ne tout le travail dans les appels de toouser de réponse, il est inutile pour qu’il tooimplement `runAsync()`. Que les écouteurs de communication hello et son code associé sont nécessaires. De même, créer et de retourner des écouteurs de communication sont facultative, comme hello service devra peut-être uniquement en arrière-plan toodo de travail et seulement doit tooimplement`runAsync()`
* Il n’est valide pour un service toocomplete `runAsync()` avec succès et le retour à partir de celui-ci. Cela n’est pas considéré comme une condition d’échec et représente le travail d’arrière-plan hello de fin de service hello. Pour les services fiables avec état `runAsync()` serait être rappelée si le service de hello ont été rétrogradé du serveur principal et ensuite promu tooprimary précédent.
* Si un service s’arrête de `runAsync()` en levant une exception inattendue, il s’agit d’une défaillance et objet de service hello est arrêté et une erreur d’intégrité est signalée.
* Il n’existe aucune limite de temps au retour de ces méthodes, vous immédiatement perdez hello capacité toowrite et par conséquent ne peut pas se terminer tout travail réel. Il est recommandé de retourner aussi rapidement que possible lors de la réception de demande d’annulation hello. Si votre service ne répond pas les appels d’API de toothese dans un délai raisonnable que service Fabric peut forcer mettre fin à votre service. En général, cela se produit uniquement lors de mises à niveau d’application ou lorsqu’un service est en cours de suppression. Par défaut, ce délai d’attente est de 15 minutes.
* Échecs Bonjour `onCloseAsync()` résultat du chemin d’accès dans `onAbort()` appelée qui est une opportunité de meilleur effort dernière chance pour hello service tooclean des et libérer toutes les ressources qu’ils ont demandé.

> [!NOTE]
> Les services fiables avec état ne sont pas encore pris en charge par Java.
>
>

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooReliable Services](service-fabric-reliable-services-introduction.md)
* [Démarrage rapide de Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Utilisation avancée de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
