---
title: "aaaDefragmentation de métriques dans Azure Service Fabric | Documents Microsoft"
description: "Une présentation de l’utilisation de la défragmentation ou de la compression en tant que stratégie pour les métriques dans Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>Défragmentation des mesures et de la charge dans Service Fabric
stratégie par défaut de Hello Service Fabric Cluster du Gestionnaire de ressources pour la gestion des mesures de charge dans le cluster de hello est la charge de hello toodistribute. S’assurer que les nœuds sont utilisés uniformément évite à chaud et à froids taches conduire tooboth contention et gaspillage des ressources. Distribuer les charges de travail dans un cluster de hello est également hello plus sûre en termes de survivant d’échecs, car elle garantit qu’une défaillance ne retirez un grand pourcentage de charge de travail donné. 

Hello, Gestionnaire de ressources du Cluster Service Fabric ne prend pas en charge une autre stratégie pour la gestion de charge, ce qui est la défragmentation. Défragmentation signifie qu’au lieu de la tentative d’utilisation de hello toodistribute d’une mesure sur le cluster de hello, il est consolidé. La consolidation est simplement une inversion de stratégie – au lieu de réduction hello moyenne écart type de charge de métrique d’équilibrage de la valeur par défaut hello, hello Gestionnaire de ressources de Cluster tente de tooincrease il.

## <a name="when-toouse-defragmentation"></a>Lors de la défragmentation de toouse
Répartition de charge dans le cluster de hello consomme des ressources hello sur chaque nœud. Certaines charges de travail créent des services qui sont particulièrement volumineux et qui consomment la plus grande partie voire la totalité d’un nœud. Dans ces cas, il est possible que lorsqu’il existe de grandes charges de travail créés qu’il ne suffit pas de l’espace sur toorun de n’importe quel nœud les. Grandes charges de travail ne sont pas un problème dans l’infrastructure de Service ; dans ces hello cas Gestionnaire de ressources de Cluster détermine qu’il nécessite de salle de toomake cluster tooreorganize hello pour cette grande charge de travail. Toutefois, dans hello attendant cette charge de travail a toobe toowait planifié dans un cluster de hello.

S’il existe de nombreux services et toomove état autour, il peut prendre beaucoup de temps pour hello grande charge de travail toobe est placé dans un cluster de hello. Il est plus probable si les autres charges de travail dans un cluster de hello sont également volumineux et par conséquent, prennent tooreorganize plus de temps. équipe de Service Fabric Hello mesurée heures de création de simulations de ce scénario. Nous avons constaté que la création de services volumineux prend beaucoup plus de temps dès que l’utilisation de clusters se situe entre 30 et 50 %. toohandle ce scénario, nous avons présenté comme une stratégie d’équilibrage de la défragmentation. Nous avons trouvé que pour les charges de travail importantes, notamment ceux où l’heure de création était important, la défragmentation a vraiment aidé à ces nouvelles charges de travail obtient planifiées dans le cluster de hello.

Vous pouvez configurer la défragmentation métriques toohave hello charge de hello tooproactively du Gestionnaire de ressources du Cluster try toocondense des services de hello en moins de nœuds. Cela permet de s’assurer qu’il est presque toujours place pour les services volumineux sans réorganiser les cluster hello. N’ayant ne pas de cluster de hello tooreorganize permet de créer rapidement de grandes charges de travail.

La plupart des utilisateurs n’ont pas besoin de la défragmentation. Les services sont généralement être petite, donc il n’est pas salle toofind dur pour eux dans un cluster de hello. Lorsqu’une réorganisation est possible, elle se déroule rapidement car la plupart des services sont petits et peuvent être déplacés rapidement et en parallèle. Toutefois, si vous les services de grande taille et avez besoin de créer rapidement hello stratégie de défragmentation est pour vous. Nous aborderons compromis hello d’ensuite à l’aide de la défragmentation. 

## <a name="defragmentation-tradeoffs"></a>Compromis concernant la défragmentation
La défragmentation peut augmenter la probabilité que les défaillances aient un impact car plus de services sont exécutés sur des nœuds défaillants. Défragmentation peut également augmenter les coûts, étant donné que les ressources de cluster de hello doivent être gardées en réserve, en attente pour la création de hello de grandes charges de travail.

Hello diagramme suivant donne une représentation visuelle de deux clusters, qui est la défragmentation et qui n’est pas. 

<center>
![Comparaison de clusters équilibré et défragmenté][Image1]
</center>

Dans les cas de hello équilibré, envisagez nombre hello mouvements qui seraient nécessaire tooplace un des objets de service de plus grande hello. Dans un cluster de défragmenté hello, grande charge de travail hello peut être placé sur des nœuds de quatre ou cinq sans avoir toowait pour n’importe quel autre toomove de services.

## <a name="defragmentation-pros-and-cons"></a>Avantages et inconvénients de la défragmentation
Quelles sont donc ces autres compromis ? Voici un tableau rapide de choses toothink sur :

| Avantages de la défragmentation | Inconvénients de la défragmentation |
| --- | --- |
| Permet la création plus rapide de services de grande taille |Concentre la charge dans un plus petit nombre de nœuds, ce qui augmente la contention |
| Permet de diminuer le déplacement des données lors de la création |Les défaillances peuvent avoir un impact sur d’autres services et provoquer une plus grande désinscription |
| Permet de décrire en détail les exigences et la récupération d’espace |Configuration générale plus complexe de la gestion des ressources |

Vous pouvez combiner défragmenté et de mesures normales hello même cluster. Hello Gestionnaire de ressources de Cluster essaie tooconsolidate hello défragmentation métriques autant que possible lors de la répartition des hello d’autres. résultats Hello de mélange de défragmentation et équilibrage des stratégies dépend de plusieurs facteurs, notamment :
  - nombre de Hello d’équilibrage de la métrique contre le nombre de hello de métriques de défragmentation
  - si un service utilise ces deux types de mesures 
  - poids de métrique Hello
  - les charges actuelles des mesures
  
Expérimentation toodetermine requis hello exacte configuration est nécessaire. Nous vous recommandons d’effectuer une mesure minutieuse de vos charges de travail avant d’activer les mesures de défragmentation en production. Cela est particulièrement vrai lorsque vous mélangez défragmentation et équilibrage de charge de métriques dans hello même service. 

## <a name="configuring-defragmentation-metrics"></a>Configuration de mesures de défragmentation
Configuration des métriques de défragmentation est une décision globale dans un cluster de hello et mesures individuelles peuvent être sélectionnées pour la défragmentation. Hello, suivant la configuration des extraits de code montrent comment tooconfigure les métriques pour la défragmentation. Dans ce cas, « Metric1 » est configuré en tant que la défragmentation métrique, alors que « Metric2 » continue toobe équilibrée normalement. 

ClusterManifest.xml :

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>Étapes suivantes
- Hello Gestionnaire de ressources du Cluster a des options de man pour décrire le cluster de hello. toofind plus d’informations à leur sujet, consultez cet article sur [décrivant un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- Les métriques sont comment hello Gestionnaire de ressources du Cluster Service Fabric gère la consommation et la capacité en cluster de hello. toolearn plus d’informations sur les métriques et comment tooconfigure, extraire [cet article](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
