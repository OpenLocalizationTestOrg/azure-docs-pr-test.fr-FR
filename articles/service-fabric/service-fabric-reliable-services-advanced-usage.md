---
title: "utilisation d’aaaAdvanced des Services fiables | Documents Microsoft"
description: "En savoir plus sur l’utilisation avancée de Reliable Services de Service Fabric pour améliorer la flexibilité de vos services."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>L’utilisation du modèle de programmation des Services fiables hello avancée
Azure Service Fabric simplifie l’écriture et la gestion des services fiables avec et sans état. Ce guide parle utilisations avancées des Services fiables toogain davantage de contrôle et de flexibilité sur vos services. Tooreading préalable de ce guide, familiarisez-vous avec [modèle de programmation de Services fiables hello](service-fabric-reliable-services-introduction.md).

Les services avec et sans état ont deux points d’entrée principaux pour le code utilisateur :

* `RunAsync(C#) / runAsync(Java)` est un point d’entrée à usage général pour votre code de service.
* `CreateServiceReplicaListeners(C#)` et `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` sont utilisés pour l’ouverture des écouteurs de communication pour les requêtes du client.

Pour la plupart des services, ces deux points d’entrée sont suffisants. Dans de rares cas, lorsque davantage de contrôle sur le cycle de vie d’un service est requis, des événements de cycle de vie supplémentaires sont disponibles.

## <a name="stateless-service-instance-lifecycle"></a>Cycle de vie d’instance de service sans état
Le cycle de vie d’un service sans état est très simple. Un service sans état peut uniquement être ouvert, fermé ou abandonné. `RunAsync` dans un service sans état est exécuté quand une instance de service est ouverte, et annulée quand une instance de service est fermée ou abandonnée.

Bien que `RunAsync` doit être suffisante dans presque tous les cas, hello ouvrir, fermer et abandonner les événements dans un service sans état sont également disponibles :

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync est appelé lorsque l’instance de service sans état hello concerne toobe utilisé. Les tâches d'initialisation de service étendues peuvent être démarrées à ce stade.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync est appelé lorsque l’instance de service sans état hello est en train de toobe arrêt en douceur. Cela peut se produire lorsque hello du code est en cours de mise à niveau, l’instance de service hello est déplacé en raison de l’équilibrage de la tooload ou une erreur transitoire est détectée. OnCloseAsync peut être utilisé toosafely fermer toutes les ressources, arrêtez tout le traitement en arrière-plan, terminer l’enregistrement de l’état externe ou fermer les connexions existantes.
* `void OnAbort() - C# / void onAbort() - Java`OnAbort est appelé lorsque l’instance de service sans état hello est forcé arrêté. Cela est généralement appelée lorsqu’une erreur permanente est détectée sur le nœud de hello, ou lorsque l’infrastructure de Service ne peut pas gérer le cycle de vie de l’instance de service hello en raison d’échecs de toointernal de manière fiable.

## <a name="stateful-service-replica-lifecycle"></a>Cycle de vie d’un réplica de service avec état

> [!NOTE]
> Les services fiables avec état ne sont pas encore pris en charge par Java.
>
>

Le cycle de vie d’un réplica de service avec état est beaucoup plus complexe qu’une instance de service sans état. En outre tooopen, fermez et abandonner les événements, un réplica de service avec état subit des modifications de rôle pendant sa durée de vie. Quand un réplica de service avec état change de rôle, hello `OnChangeRoleAsync` est déclenché :

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync est appelé lorsque le réplica de service avec état hello est la modification de rôle, par exemple tooprimary ou base de données secondaire. Les réplicas principaux figurent un statut d’écriture (sont autorisés à toocreate et écrire des Collections de tooReliable). Les réplicas secondaires se voient affecter un état de lecture (ils peuvent uniquement lire à partir de collections fiables existantes). La plupart du travail dans un service avec état est effectué au réplica principal de hello. Les réplicas secondaires peuvent effectuer la validation en lecture seule, la génération de rapports, l’exploration de données ou d’autres tâches en lecture seule.

Dans un service avec état, seuls les réplicas principal hello a un accès en écriture toostate et sont donc généralement lorsque le service de hello effectue le travail réel. Hello `RunAsync` méthode dans un service avec état est exécutée que lorsque le réplica de service avec état hello est principal. Hello `RunAsync` méthode est annulée lorsque des modifications de rôle d’un réplica principal en s’éloignant de principal, ainsi qu’au cours de hello ferment et abandonner les événements.

À l’aide de hello `OnChangeRoleAsync` événements vous permet de travail tooperform en fonction du rôle de réplica, ainsi que dans les modifications de toorole de réponse.

Un service avec état fournit également des hello quatre même cycle de vie des événements comme un service sans état, avec hello même sémantique et en cas d’utilisation :

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>Étapes suivantes
Pour plus avancées rubriques connexes tooService Fabric, consultez hello suivant des articles :

* [Configuration de Reliable Services avec état](service-fabric-reliable-services-configuration.md)
* [Présentation de l’intégrité de Service Fabric](service-fabric-health-introduction.md)
* [Utilisation des rapports d’intégrité système pour la résolution des problèmes](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Configuration des Services avec hello Gestionnaire de ressources du Cluster Service Fabric](service-fabric-cluster-resource-manager-configure-services.md)
