---
title: aaaAvailability de services de Fabric du Service | Documents Microsoft
description: "Décrit la détection des erreurs, le basculement et la récupération pour les services"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Disponibilité des services Service Fabric
Cet article offre une vue d'ensemble de la manière dont Service Fabric maintient la disponibilité.

## <a name="availability-of-service-fabric-stateless-services"></a>Disponibilité des services sans état de Service Fabric
Les services Azure Service Fabric peuvent être avec ou sans état. Un service sans état est un service d’application qui n’a pas de [état local](service-fabric-concepts-state.md) qui doit toobe hautement disponible ou fiable.

La création d’un service sans état nécessite la définition d’un `InstanceCount`. nombre d’instances Hello définit le nombre de hello d’instances de service sans état hello logique d’application doit s’exécuter dans un cluster de hello. Augmentation du nombre hello d’instances est hello recommandé moyen de montée en puissance parallèle d’un service sans état.

Lorsqu’une instance de sans état nommé service échoue, une nouvelle instance est créée sur un nœud éligible dans le cluster de hello. Par exemple, une instance de service sans état peut échouer sur Node1 et être recréée sur Node5.

## <a name="availability-of-service-fabric-stateful-services"></a>Disponibilité des services avec état de Service Fabric
Un service avec état possède un état qui lui est associé. Dans Service Fabric, un service avec état est modelé comme un jeu de réplicas. Chaque réplica est une instance en cours d’exécution de code hello du service hello qui possède également une copie de l’état de hello pour ce service. Opérations de lecture et d’écriture sont effectuées dans un réplica (appelé hello principal). Toostate de modifications à partir d’opérations d’écriture sont *répliquées* toohello autres réplicas dans le jeu de réplicas hello (appelé secondaires actifs) et appliquée. 

Il ne peut y avoir qu’un seul réplica principal, mais il peut y avoir plusieurs réplicas secondaires actifs. nombre de Hello des réplicas secondaires actifs est configurable, et un plus grand nombre de réplicas peut tolérer un plus grand nombre de logiciels et des défaillances matérielles.

Si le réplica principal de hello tombe en panne, Service Fabric établissant l’une des hello secondaire Active réplicas hello nouveau réplica principal. Ce réplica secondaire actif a déjà la version hello mis à jour d’état de hello (via *réplication*), et peut continuer le traitement supplémentaire en lecture et les opérations d’écriture.

Ce concept, d’un réplica en cours d’un principal ou secondaire Active, est appelé hello rôle du réplica.

### <a name="replica-roles"></a>Rôles de réplica
rôle Hello d’un réplica est un cycle de vie utilisé toomanage hello d’état hello géré par ce réplica. Un réplica dont le rôle est principal traite les demandes de lecture. Hello principal gère également toutes les demandes d’écriture par la mise à jour son état et la réplication des modifications de hello. Ces modifications sont appliquée toohello les secondaires actifs dans le jeu de réplicas hello. tâche Hello secondaire Active est la modification d’état tooreceive hello réplica principal a été répliqué et mettre à jour son affichage de l’état de hello.

> [!NOTE]
> Modèles de programmation de niveau supérieur telles que [Reliable Actors](service-fabric-reliable-actors-introduction.md) et [des Services fiables](service-fabric-reliable-services-introduction.md) masquer le concept de hello du rôle de réplica du développeur de hello. Dans acteurs, notion hello du rôle n’est pas nécessaire, tout en dans Services, il est en grande partie simplifiée pour la plupart des scénarios.
>

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les concepts de l’infrastructure de Service, consultez hello suivant des articles :

- [Mise à l’échelle des applications Service Fabric](service-fabric-concepts-scalability.md)
- [Partitionnement des services Service Fabric](service-fabric-concepts-partitioning.md)
- [Définition et gestion de l'état](service-fabric-concepts-state.md)
- [Services fiables (Reliable Services)](service-fabric-reliable-services-introduction.md)
