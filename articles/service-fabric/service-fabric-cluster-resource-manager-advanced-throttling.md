---
title: aaaThrottling dans le Gestionnaire de ressources de cluster Service Fabric hello | Documents Microsoft
description: "Découvrez les accélérateurs de hello tooconfigure fournies par hello Gestionnaire de ressources du Cluster Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>La limitation hello Gestionnaire de ressources du Cluster Service Fabric
Même si vous avez correctement configuré hello Gestionnaire de ressources du Cluster, le cluster de hello peut obtenir interrompue. Par exemple, il peut y avoir nœud et erreur domaine défaillances simultanées - ce qui se passerait si qui s’est produite pendant une mise à niveau ? Hello Gestionnaire de ressources de Cluster tente toujours de toofix tout, consomment des ressources du cluster hello la tentative de cluster de hello tooreorganize et les résoudre. Les limitations permettent une protection afin que le cluster de hello peut utiliser des ressources toostabilize - les nœuds hello reviennent, réparer des partitions de réseau hello, bits corrigés sont déployés.

toohelp avec ces types de situations, hello Gestionnaire de ressources du Cluster Service Fabric comprend plusieurs limitations. Ces limitations sont toutes relativement importantes. En règle générale, elles ne doivent pas être modifiées sans une planification et des tests minutieux.

Si vous modifiez les limitations du Gestionnaire de ressources Cluster hello, vous devez la régler les charge réelle de tooyour attendu. Vous pouvez déterminer que vous devez toohave certaines limite en place, même si cela implique de cluster de hello prend plus de temps toostabilize dans certaines situations. Le test est requis toodetermine hello des valeurs correctes pour les limitations. Les limitations doivent toobe tooallow suffisamment élevée hello cluster toorespond toochanges dans un délai raisonnable et faible suffisamment tooactually empêcher trop de la consommation des ressources. 

Limitations, qu'il a été, car ils étaient déjà présents dans un environnement de la ressource d’utiliser plus de hello que nous avons vu des clients. Il peut s’agir la bande passante réseau limitée pour des nœuds individuels ou des disques qui ne sont pas en mesure de toobuild nombre de réplicas avec état dans parallèle en raison des limitations de toothroughput. Sans les limitations, les opérations pourraient surcharger ces ressources, à l’origine des opérations toofail ou lente. Dans ces situations clients utilisé des accélérateurs et connaissaient qu’ils ont été extension quantité hello de temps qu’il faudrait hello cluster tooreach un état stable. Les clients comprenaient également qu’ils pourraient fonctionner avec une fiabilité globale inférieure pendant l’application des limitations.


## <a name="configuring-hello-throttles"></a>Configuration hello accélérateurs

Service Fabric a deux mécanismes de limitation du nombre de hello des mouvements de réplica. mécanisme par défaut Hello qui existaient avant le Service Fabric 5.7 représente sous forme de nombre absolu de déplacements autorisés de limitation. Il ne fonctionne pas avec des clusters de toutes tailles. En particulier, pour valeur par défaut de clusters volumineux hello valeur peut être insuffisante, ralentir considérablement d’équilibrage de la même lorsqu’il est nécessaire, tout en n’ayant aucun effet dans des clusters plus petits. Ce mécanisme préalable a été remplacé par la limitation basée sur un pourcentage, qui est mieux adapté à avec des clusters dynamiques dans le numéro de hello de services et modification de nœuds régulièrement.

les limitations de Hello sont basées sur un pourcentage du nombre de hello de réplicas dans les clusters de hello. Les accélérateurs Percetage basé activer la règle de hello exprimant : « ne déplacez pas plus de 10 % de réplicas dans un intervalle de 10 minutes », par exemple.

paramètres de configuration de Hello pour la limitation basée sur le pourcentage sont :

  - GlobalMovementThrottleThresholdPercentage - le nombre maximal de mouvements autorisée dans un cluster à tout moment, exprimé en pourcentage du nombre total de réplicas dans un cluster de hello. 0 indique aucune limite. Hello par défaut est 0. Si ce paramètre et le GlobalMovementThrottleThreshold sont spécifiés, puis hello plus conservateur limite est utilisée.
  - GlobalMovementThrottleThresholdPercentageForPlacement - le nombre maximal de mouvements autorisées pendant la phase de la sélection élective hello, exprimé en pourcentage du nombre total de réplicas dans un cluster de hello. 0 indique aucune limite. Hello par défaut est 0. Si ce paramètre et le GlobalMovementThrottleThresholdForPlacement sont spécifiés, puis hello plus conservateur limite est utilisée.
  - GlobalMovementThrottleThresholdPercentageForBalancing - le nombre maximal de mouvements autorisé pendant hello l’équilibrage de la phase, exprimé en pourcentage du nombre total de réplicas dans un cluster de hello. 0 indique aucune limite. Hello par défaut est 0. Si ce paramètre et le GlobalMovementThrottleThresholdForBalancing sont spécifiés, puis hello plus conservateur limite est utilisée.

Lorsque vous spécifiez le pourcentage de l’accélérateur hello, vous spécifiez 5 % comme 0,05. intervalle de salutation sur lequel ces limitations sont régies est hello GlobalMovementThrottleCountingInterval, qui est exprimée en secondes.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>Limitations basées sur le nombre par défaut
Ces informations sont fournies dans le cas où vous avez d’anciens clusters ou conservez ces configurations en clusters qui ont par la suite été mis à niveau. En règle générale, il est recommandé que ces sont remplacées par hello en pourcentage les limitations ci-dessus. Étant donné que la limitation basée sur le pourcentage est désactivée par défaut, ces limitations restent hello des accélérateurs de valeur par défaut pour un cluster jusqu'à ce qu’ils sont désactivés et remplacées par les limitations de pourcentage hello. 

  - GlobalMovementThrottleThreshold – ce paramètre contrôle nombre total de hello des mouvements de cluster de hello sur un certain temps. Durée Hello est spécifiée dans les secondes sous la forme hello GlobalMovementThrottleCountingInterval. valeur par défaut de Hello pour hello GlobalMovementThrottleThreshold est comprise entre 1000 et valeur par défaut de hello pour hello GlobalMovementThrottleCountingInterval est 600.
  - MovementPerPartitionThrottleThreshold – ce paramètre contrôle nombre total de hello des mouvements d’une partition de service sur un certain temps. Durée Hello est spécifiée dans les secondes sous la forme hello MovementPerPartitionThrottleCountingInterval. valeur par défaut de Hello pour hello MovementPerPartitionThrottleThreshold est 50 et valeur par défaut de hello pour hello MovementPerPartitionThrottleCountingInterval est 600.

configuration Hello pour ces accélérateurs suit hello même motif comme hello en pourcentage de limitation.

## <a name="next-steps"></a>Étapes suivantes
- toofind out sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, consultez l’article de hello sur [équilibrage de charge](service-fabric-cluster-resource-manager-balancing.md)
- Hello, Gestionnaire de ressources du Cluster possède de nombreuses options permettant de décrire le cluster de hello. toofind plus d’informations à leur sujet, consultez cet article sur [décrivant un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
