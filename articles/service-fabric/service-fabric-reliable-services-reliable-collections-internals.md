---
title: "aaaAzure mécanismes internes de gestionnaire d’état de Service Fabric fiable et Collection fiable | Documents Microsoft"
description: "Présentation approfondie sur la conception et les concepts de collection fiable dans Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Éléments internes de collection fiable et de gestionnaire d’état fiable Azure Service Fabric
Ce document examine dans toosee fiable Gestionnaire d’état et les Collections fiable de fonctionnement des composants principaux coulisses hello.

> [!NOTE]
> Ce document est en évolution. Ajouter des commentaires toothis article tootell nous sujet que vous aimeriez toolearn plus en détail.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>Modèle de persistance local : journal et point de contrôle
Hello fiable Gestionnaire d’état et les Collections fiable suivent un modèle de persistance qui est appelé point de contrôle et de journal.
Dans ce modèle, chaque changement d’état est d’abord enregistré sur le disque, puis appliqué dans la mémoire.
Hello complète état lui-même est rendu persistant qu’occasionnellement (aussi appelé) Point de contrôle).
avantages de Hello sont que les deltas sont transformées en séquentiel en mode append-only écritures sur disque pour améliorer les performances.

toobetter comprendre hello journal et le modèle de point de contrôle, commençons par examiner au scénario de disque infinie hello.
Hello fiable Gestionnaire d’état enregistre chaque opération avant sa réplication.
Journalisation permet hello Collections fiable tooapply hello uniquement en mémoire.
Étant donné que les journaux sont conservées, même lorsque le réplica de hello échoue et qu’il doit toobe redémarré, hello fiable Gestionnaire d’état a suffisamment d’informations dans ses tooreplay journal toutes les opérations de hello a perdu le réplica de hello.
Comme disque de hello est infinie, les enregistrements de journal n’ont jamais besoin toobe supprimé et état de toomanage uniquement hello en mémoire doit hello Collection fiable.

Maintenant examinons le scénario de disque finie hello.
Comme les enregistrements de journal s’accumulent, hello fiable Gestionnaire d’état manquiez d’espace disque.
Avant cela, hello fiable Gestionnaire d’état doit tootruncate son espace de toomake de journal pour les enregistrements de nouveaux hello.
Des demandes du gestionnaire Reliable état hello Collections fiable toocheckpoint toodisk de leur état en mémoire.
À ce stade, hello Collections fiable' serait conserver son état en mémoire.
Une fois que les Collections fiable hello terminé leurs points de contrôle, hello fiable Gestionnaire d’état peut tronquer toofree de journal hello l’espace disque.
Lorsque les besoins de réplica de hello toobe redémarré, Collections fiable récupérer leur état de point de contrôle et récupère hello Gestionnaire d’état fiable et lit toutes les modifications d’état hello qui se sont produites depuis le dernier point de contrôle hello.

Le point de contrôle améliore également les délais de récupération dans les cas courants. Journal contient toutes les opérations qui se sont produites depuis le dernier point de contrôle hello.
Par conséquent, il peut inclure plusieurs versions d’un élément. Par exemple, plusieurs valeurs pour une ligne donnée dans le dictionnaire fiable.
En revanche, points de contrôle de la Collection fiable hello uniquement la version la plus récente de chaque valeur d’une clé.

## <a name="next-steps"></a>Étapes suivantes
* [Transactions et verrous](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

