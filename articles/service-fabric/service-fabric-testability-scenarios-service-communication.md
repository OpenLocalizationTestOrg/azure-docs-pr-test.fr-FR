---
title: "Testabilité : communication de service | Microsoft Docs"
description: "La communication service à service constitue un point d’intégration critique d’une application Service Fabric. Cet article aborde les problématiques de conception et les techniques de test."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>Scénarios de testabilité de Service Fabric : communication de service
Les microservices et les styles architecturaux orientés services émergent naturellement dans Azure Service Fabric. Dans ces types d’architectures distribuées, les applications basées sur des composants microservice sont généralement composées de plusieurs services qui doivent tootalk tooeach autres. Dans les cas les plus simples hello même, vous avez généralement au moins un service web sans état et un service de stockage de données avec état qui doivent toocommunicate.

Les communications de service sont un point d’intégration critiques d’une application, car chaque service expose un tooother les services API à distance. L’utilisation d’un ensemble de limites d’API impliquant un trafic d’E/S nécessite bien souvent une attention particulière, secondée par de solides méthodes de test et de validation.

Il existe plusieurs considérations toomake lorsque ces limites de service sont reliées entre elles dans un système distribué :

* *Protocole de transfert*. Allez-vous utiliser le protocole HTTP, pour une interopérabilité améliorée, ou un protocole binaire personnalisé favorisant un débit optimal ?
* *Gestion des erreurs*. Comment les erreurs permanentes et temporaires sont-elles traitées ? Que se passe-t-il lorsqu’un service déplace tooa autre nœud ?
* *Délais d’attente et latence*. Dans les applications multicouches, comment chaque couche de service gère latence par un utilisateur de la pile et toohello hello ?

Si vous utilisez un des composants de communication hello service intégré fournis par l’infrastructure de Service ou si vous générez votre propre, interactions hello entre vos services de test est résilience tooensuring critiques dans votre application.

## <a name="prepare-for-services-toomove"></a>Préparer les services toomove
Les instances de service peuvent se déplacer au fil du temps. Ce déplacement est particulièrement avéré quand elles sont configurées avec des mesures de charge dédiées à l’équilibrage personnalisé optimal des ressources. Service Fabric déplace votre toomaximize d’instances de service leur disponibilité même pendant les mises à niveau, les basculements, montée en puissance parallèle et d’autres situations qui se produisent sur la durée de vie hello d’un système distribué.

Services de se déplacement dans un cluster de hello, vos clients et autres services doivent être préparée toohandle deux scénarios lorsqu’ils parlent tooa service :

* réplica de partition ou instance de service Hello a été déplacée depuis hello heure de la dernière, nous vous avons tooit. Il s’agit d’un composant normal d’un cycle de vie du service, et il doit être toohappen attendu pendant la durée de vie hello de votre application.
* réplica de partition ou instance de service Hello est en cours de hello de déplacement. Bien que le basculement d’un service à partir d’un nœud tooanother s’effectue très rapidement dans l’infrastructure de Service, il peut avoir un délai de disponibilité si le composant de communication hello de votre service est lente toostart.

Pour bénéficier d’un système pleinement fonctionnel, il est nécessaire de gérer ces scénarios de manière appropriée. toodo, gardez à l’esprit que :

* Tous les services qui peuvent être connectés toohas un *adresse* qu’il écoute sur (par exemple, HTTP ou WebSocket). Quand une instance ou partition de service se déplace, le point de terminaison de son adresse change. (Il déplace tooa autre nœud avec une autre adresse IP.) Si vous utilisez des composants de communication intégrée hello, ils gèrent ré-résolution des adresses de service pour vous.
* Il peut y avoir une augmentation de latence de service en tant qu’instance de service hello démarre son écouteur à nouveau. Cela dépend de la rapidité avec laquelle le service de hello ouvre à un écouteur de hello après le déplacement de l’instance de service hello.
* Toutes les connexions existantes doivent toobe fermée et rouverte après ouverture du service de hello sur un nouveau nœud. Un arrêt correct de nœuds ou redémarrage permet pour toobe de connexions existant s’arrête.

### <a name="test-it-move-service-instances"></a>Test : déplacement des instances de service
À l’aide des outils de test de Service Fabric, vous pouvez créer un tootest de scénario de test à ces situations de différentes façons :

1. Déplacez un réplica principal de service avec état.
   
    Hello réplica principal d’une partition de service avec état peut être déplacé pour différentes raisons. Utilisez cet tootarget hello un réplica principal d’un toosee partition spécifique comment votre toohello réagissent de services se déplacent de façon très contrôlée.
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. Arrêtez un nœud.
   
    Lorsqu’un nœud est arrêté, se déplace le Service Fabric tous hello service instances ou les partitions qui étaient présents sur ce tooone de nœud de hello autres nœuds disponibles dans le cluster de hello. Utilisez cette tootest une situation où un nœud est perdu à partir de votre cluster et des instances de service hello et les réplicas sur le nœud toomove.
   
    Vous pouvez arrêter un nœud à l’aide de hello PowerShell **Stop-ServiceFabricNode** applet de commande :
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>Maintenir la disponibilité du service
En tant que plateforme, Service Fabric est conçue tooprovide haute disponibilité de vos services. Mais dans des cas extrêmes, les problèmes liés à l’infrastructure sous-jacente peuvent quand même entraîner une indisponibilité. Il est trop important tootest pour ces scénarios.

Les services avec état utiliser un état de tooreplicate système basé sur le quorum pour la haute disponibilité. Cela signifie qu’un quorum de réplicas doit toobe tooperform disponibles les opérations d’écriture. Dans de rares cas, comme celui d’une défaillance matérielle étendue, aucun quorum de réplicas ne peut être disponible. Dans ce cas, vous ne serez pas en mesure de tooperform les opérations d’écriture, mais vous serez toujours en mesure de tooperform des opérations de lecture.

### <a name="test-it-write-operation-unavailability"></a>Test : écriture de l’indisponibilité des opérations
À l’aide des outils de testabilité hello dans l’infrastructure de Service, vous pouvez injecter une erreur qui induit une perte de quorum en tant que test. Bien que ce cas soit rare, il est important que les clients et les services qui dépendent d’un service avec état sont préparés toohandle les situations où ils ne peuvent pas apporter tooit de demandes d’écriture. Il est également important que hello avec état service tient compte de cette possibilité et peut le communiquer en douceur toocallers.

Vous est susceptible d’entraîner une perte de quorum à l’aide de hello PowerShell **Invoke-ServiceFabricPartitionQuorumLoss** applet de commande :

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

Dans cet exemple, nous avons défini `QuorumLossMode` trop`QuorumReplicas` tooindicate que nous souhaitons perte de quorum tooinduce sans arrêter tous les réplicas. Ainsi, les opérations de lecture sont toujours possibles. tootest un scénario où un ensemble de la partition est indisponible, vous pouvez définir ce commutateur trop`AllReplicas`.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur les actions de testabilité](service-fabric-testability-actions.md)

[En savoir plus sur les scénarios de testabilité](service-fabric-testability-scenarios.md)

