---
title: "aaaService Gestionnaire de ressources de Cluster de l’ensemble fibre optique - affinité | Documents Microsoft"
description: "Présentation de la configuration de l’affinité pour les services Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>Configuration et utilisation de l’affinité de service dans Service Fabric
Affinité est un contrôle qui est fourni principalement toohelp facilité hello transition de grandes applications monolithiques dans le cloud et microservices Bonjour. Il est également utilisé en guise d’optimisation pour améliorer les performances de hello de services, bien que cela peut avoir les effets secondaires.

Supposons que vous importez une application plus volumineuse ou avec un uniquement n’a pas été conçue avec microservices dans l’esprit, tooService Fabric (ou n’importe quel environnement distribué). Ce type de transition est courant. Vous commencez par levage hello ensemble de votre application dans un environnement de hello, empaqueter et s’assurer qu’il fonctionne correctement. Puis vous démarrez avec rupture dans différents services plus petits que tous les contacter tooeach autres.

Par la suite, vous pouvez constater qu’application hello rencontrent des problèmes. problèmes de Hello appartiennent généralement à une de ces catégories :

1. Quelques composants X, dans l’application monolithique hello avait une dépendance non documentée sur le composant Y, et vous avez activé uniquement les composants en services distincts. Étant donné que ces services sont en cours d’exécution sur différents nœuds dans un cluster de hello, ils sont rompus.
2. Ces composants communiquent (canaux nommés locaux | mémoire partagée | fichiers sur le disque) et ils ont vraiment besoin toobe toowrite en mesure de la ressource locale tooa partagé pour des raisons de performances dès maintenant. Cette dépendance ferme est éventuellement supprimée ultérieurement.
3. Tout fonctionne correctement, sauf que ces deux composants sont en fait très occupés et sensibles aux performances. Lorsqu’ils sont transférés dans des services distincts, la performance globale des applications diminue ou la latence augmente. Par conséquent, hello globales de l’application ne répond pas aux attentes.

Dans ce cas, nous ne voulez toolose notre travail de refactorisation ou non toogo toohello arrière monolithique. Hello dernière condition peut même être souhaitable, dans une optimisation simple. Toutefois, jusqu'à ce que nous pouvons reconcevoir hello composants toowork naturellement en tant que services (ou jusqu'à ce que nous pouvons résoudre une autre façon les attentes de performance hello) nous allons tooneed un sens de la localité.

Le toodo ? Il est possible d’activer l’affinité.

## <a name="how-tooconfigure-affinity"></a>Comment les affinités tooconfigure
tooset une affinité, vous définissez une relation d’affinité entre deux services. Cela revient à faire pointer un service sur un autre, ce qui fait qu’un service peut uniquement fonctionner quand cet autre service est en cours d’exécution. Nous appelons parfois tooaffinity une relation parent/enfant (où vous pointez les enfants hello au parent de hello). Affinité garantit que les réplicas hello ou instances d’un service sont placés sur hello même nœuds en tant que ceux d’un autre service.

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> Un service enfant ne peut participer qu’à une seule relation d’affinité. Si vous souhaitiez hello enfant toobe d’affinité tootwo parent services à la fois, vous avez deux options :
> - Inverser les relations hello (avoir parentService1 et parentService2 point au niveau de service d’enfants actuelle hello), ou
> - Un des parents de hello désigner comme un concentrateur, par convention et avoir tous les services pointent vers ce service. 
>
> Hello, ce qui entraîne le comportement de placement dans un cluster de hello doit être hello même.
>

## <a name="different-affinity-options"></a>Différentes options d’affinité
L’affinité est représentée par un des jeux de corrélations et comporte deux modes différents. Hello le mode courants d’affinité est ce que nous appelons NonAlignedAffinity. Dans NonAlignedAffinity, hello réplicas ou les instances de services différents de hello sont placés sur hello même nœuds. Bonjour autre mode est AlignedAffinity. L’affinité alignée est utilisée uniquement avec les services avec état. Configuration dynamique de deux services toohave aligné affinité garantit qu’indistinctement hello de ces services est placés sur hello mêmes nœuds les uns des autres. Il est également générée chaque paire de bases de données secondaires pour ces toobe services placé sur hello même nœuds. Il est également possible (bien que moins fréquent) tooconfigure NonAlignedAffinity pour les services avec état. Pour NonAlignedAffinity, différents réplicas de hello Hello deux services avec état s’exécuterait sur hello mêmes nœuds, mais leurs couleurs primaires peuvent se retrouver sur différents nœuds.

<center>
![Modes d’affinité et leurs effets][Image1]
</center>

### <a name="best-effort-desired-state"></a>Meilleur état souhaité
Une relation d’affinité est conseillée. Il ne fournit pas hello mêmes garanties de fiabilité qui est en cours d’exécution dans hello même processus exécutable ou de colocalisation. services Hello dans une relation d’affinité sont fondamentalement différentes entités peuvent échouer et être déplacées séparément. Une relation d’affinité peut également être interrompue, bien que ces interruptions soient temporaires. Par exemple, les limites de capacité peuvent signifier que seules certaines hello des objets de service dans la relation d’affinité hello peuvent tenir sur un nœud donné. Dans ces cas même s’il existe une relation d’affinité sur place, il ne peut pas être appliquée échéance toohello autres contraintes. S’il est donc possible toodo, violation de hello est corrigée automatiquement plus tard.

### <a name="chains-vs-stars"></a>Chaînes et étoiles
Aujourd'hui, hello Gestionnaire de ressources du Cluster n’est pas toomodel en mesure des chaînes de relations d’affinité. Cela signifie qu’un service qui est un service enfant dans une relation d’affinité ne peut pas être un parent dans une autre relation d’affinité. Si vous souhaitez toomodel ce type de relation, vous disposez effectivement toomodel comme une étoile, plutôt qu’une chaîne. toomove à partir d’une étoile tooa chaîne, les enfants plus bas hello serait parent du toohello apparenté premier enfant à la place. Selon la disposition de hello de vos services, vous avez peut-être toodo cette opération plusieurs fois. S’il n’existe aucun service parent naturel, vous avez peut-être toocreate qui sert d’espace réservé. Selon vos besoins, vous pouvez également toolook dans [groupes d’applications](service-fabric-cluster-resource-manager-application-groups.md).

<center>
![Chaînes et Étoiles dans le contexte des relations d’affinité de hello][Image2]
</center>

Aujourd'hui, un autre chose toonote, sur les relations d’affinité est qu’ils sont directionnelles. Cela signifie que cette règle d’affinité hello applique uniquement cet enfant hello placé avec le parent de hello. Il ne garantit pas le que parent hello se trouve avec les enfants hello. Il est également important toonote qui hello relation d’affinité ne peut pas être idéal ou instantanément appliquée, car les différents services ont des différents cycles de vie et peuvent échouer et déplacer indépendamment. Par exemple, supposons que parent de hello subit une défaillance sur le nœud de tooanother, car il est arrêté anormalement. Hello Gestionnaire de ressources du Cluster et le handle du Gestionnaire de basculement hello tout d’abord, le basculement en conservant les services hello, cohérente et disponibles étant priorité de hello. Une fois le basculement de hello se termine, relation d’affinité hello est interrompue, mais hello Gestionnaire de ressources du Cluster pense que tout se passe bien jusqu'à ce qu’il remarque que les enfants hello n’est pas situé sur le parent de hello. Ces types de vérifications sont effectuées régulièrement. Vous trouverez plus d’informations sur comment hello Gestionnaire de ressources du Cluster évalue les contraintes dans [cet article](service-fabric-cluster-resource-manager-management-integration.md#constraint-types), et [celle-ci](service-fabric-cluster-resource-manager-balancing.md) présente plus en détail comment tooconfigure hello cadence à laquelle ces contraintes sont évaluée.   


### <a name="partitioning-support"></a>Prise en charge du partitionnement
toonotice de dernière chose Hello sur l’affinité est que les relations d’affinité ne sont pas pris en charge où le parent de hello est partitionnée. Des services parent partitionnés peuvent être pris en charge par la suite, mais cela n’est pas autorisé à l’heure actuelle.

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur la configuration des services, consultez la rubrique [En savoir plus sur la configuration des services](service-fabric-cluster-resource-manager-configure-services.md)
- services de toolimit tooa un petit ensemble d’ordinateurs ou d’agrégation charge hello de services, utilisez [groupes d’applications](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png