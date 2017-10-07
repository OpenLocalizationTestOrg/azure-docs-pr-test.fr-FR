---
title: aaaBalance votre cluster Azure Service Fabric | Documents Microsoft
description: "Une présentation toobalancing votre cluster avec hello Gestionnaire de ressources du Cluster Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a>Équilibrage de votre cluster Service Fabric
Hello, Gestionnaire de ressources du Cluster Service Fabric prend en charge les modifications de la charge dynamique, réaction tooadditions ou les suppressions de nœuds ou des services. Elle corrige également automatiquement les violations de contrainte et rééquilibrage de façon proactive les cluster hello. Mais à quelle fréquence ces actions sont-elles effectuées, et quel en est l’élément déclencheur ?

Il existe trois différentes catégories de travail que hello effectue de gestionnaire de ressources du Cluster. Il s'agit de :

1. Positionnement : cette étape a trait au placement des réplicas avec état ou des instances sans état manquants. Le positionnement inclut non seulement les nouveaux services, mais aussi les réplicas avec état ou les instances sans état qui ont échoué. La suppression et l’annulation des réplicas ou des instances sont gérées ici.
2. Contrainte vérifie – cette étape vérifie et corrige les violations de contraintes de positionnement différents hello (règles) dans le système de hello. Le non-dépassement de la capacité des nœuds et le respect des contraintes de positionnement d’un service sont des exemples de règles.
3. Équilibrage – cette étape vérifie toosee si rééquilibrage est nécessaire en fonction de hello configuré souhaité au niveau du solde pour les mesures de différents. Cas dans ce, il tente toofind AGENCEMENT Bonjour de cluster qui est plus équilibrée.

## <a name="configuring-cluster-resource-manager-timers"></a>Configuration des minuteurs Cluster Resource Manager
Hello premier ensemble de contrôles autour de l’équilibrage sont un ensemble d’événements d’horloge. Ces minuteries régissent la fréquence à laquelle hello Gestionnaire de ressources du Cluster examine le cluster de hello et effectue des actions correctives.

Chacune de ces différents types de hello corrections Gestionnaire de ressources de Cluster peuvent rendre est contrôlé par un minuteur différent qui détermine sa fréquence. Lorsque chaque se déclenche, la tâche hello est planifiée. Par défaut hello Gestionnaire de ressources :

* analyse son état et applique des mises à jour (comme l’enregistrement de l’arrêt d’un nœud) tous les dixièmes de seconde ;
* définit l’indicateur de vérification de la sélection élective hello 
* définit d’indicateur de vérification de contrainte hello par seconde
* définit hello équilibrage indicateur toutes les cinq secondes.

Exemples de configuration hello régissant ces minuteries sont les suivants :

ClusterManifest.xml :

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

Aujourd'hui hello Gestionnaire de ressources de Cluster effectue uniquement une de ces actions à la fois, séquentiellement. C’est pourquoi nous font référence les minuteurs toothese en tant que « intervalles minimaux » et hello actions obtient effectuées lorsque les minuteurs hello se déclencher en tant que « définition des indicateurs ». Par exemple, Gestionnaire de ressources de Cluster prend en charge en attente de hello demande des services de toocreate avant hello cluster d’équilibrage. Comme vous pouvez le voir par intervalles de temps par défaut hello spécifiés, hello Gestionnaire de ressources du Cluster de l’analyse pour tout élément besoins toodo fréquemment. Normalement, cela signifie que le jeu hello des modifications apportées à chaque étape est petite. Apporter de petites modifications fréquemment permet hello toobe du Gestionnaire de ressources du Cluster réactif lorsque les événements se produisent dans le cluster de hello. Hello minuteries de valeur par défaut fournissent certains le traitement par lot, car de nombreux hello même les types d’événements ont tendance toooccur simultanément. 

Par exemple, lorsque des nœuds échouent, ils se produisent simultanément dans des domaines d’erreur entiers. Ces échecs sont capturées au cours de l’état suivant de hello de mise à jour après hello *PLBRefreshGap*. corrections de Hello sont déterminées pendant hello après la sélection élective, vérification de contrainte et équilibrage s’exécute. Par hello de valeur par défaut Gestionnaire de ressources du Cluster n’est pas analysant les heures des modifications dans un cluster de hello et la tentative de tooaddress toutes les modifications apportées à la fois. Cela entraînerait toobursts d’évolution.

Hello, Gestionnaire de ressources du Cluster doit également certaines toodetermine des informations supplémentaires si hello cluster déséquilibré. Nous disposons pour cela de deux autres éléments de configuration : *BalancingThresholds* et *ActivityThresholds*.

## <a name="balancing-thresholds"></a>Seuils d’équilibrage
Un seuil d’équilibrage est contrôle principal de hello pour déclencher le rééquilibrage. Bonjour équilibrage de seuil pour une métrique est un _ratio_. Si charge hello pour une métrique de hello chargé plus divisé par quantité hello hello moins chargé de la charge de nœud nœud dépasse cette métrique *BalancingThreshold*, puis le cluster de hello est déséquilibré. Équilibrage de charge ainsi est suivant hello de temps hello déclenchées vérifie du Gestionnaire de ressources du Cluster. Hello *MinLoadBalancingInterval* minuteur définit la fréquence à laquelle hello Gestionnaire de ressources du Cluster doit vérifier s’il est nécessaire de rééquilibrage. Cette vérification ne signifie pas que quelque chose se produit. 

Équilibrage des seuils sont définis sur une base par métrique dans le cadre de la définition de cluster hello. Pour plus d’informations sur les mesures, consultez [cet article](service-fabric-cluster-resource-manager-metrics.md).

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<center>
Exemple de seuil d’équilibrage![][Image1]
</center>

Dans cet exemple, chaque service utilise une unité d’une mesure donnée. Dans hello exemple supérieur, hello maximale de la charge sur un nœud est de cinq et minimum de hello est deux. Supposons que hello équilibrage seuil pour cette métrique est de trois. Étant donné que le ratio hello dans un cluster de hello est 5/2 = 2.5 et qu’il est inférieure à celle spécifiée de hello équilibrage du seuil de trois, cluster de hello est équilibrée. Aucun équilibrage n’est déclenchée lorsque hello Gestionnaire de ressources du Cluster vérifie.

Dans l’exemple hello du bas, charge maximale de hello sur un nœud est 10, alors que le minimum de hello est de deux, ce qui entraîne un ratio de cinq. Cinq est supérieure au seuil de contrepartie désigné hello de trois pour cette métrique. Par conséquent, une série de rééquilibrage sera planifiée hello temps suivant, l’équilibrage de minuteur se déclenche. Dans une telle situation, une charge est généralement distribuées tooNode3. Étant donné que hello Gestionnaire de ressources du Cluster Service Fabric n’utilise pas une approche gourmande, une charge peut également être tooNode2 distribuée. 

<center>
Actions de l’exemple de seuil d’équilibrage![][Image2]
</center>

> [!NOTE]
> « L’équilibrage » adopte deux stratégies différentes pour gérer la charge de votre cluster. stratégie par défaut Hello hello utilisations du Gestionnaire de ressources du Cluster est toodistribute charge sur les nœuds hello dans un cluster de hello. Hello autre stratégie est [défragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md). La défragmentation s’effectue pendant hello équilibrage de la même exécution. Hello défragmentation et équilibrage des stratégies peuvent être utilisés pour des mesures différentes dans hello même cluster. Un service peut avoir à la fois des mesures d’équilibrage et de défragmentation. Pour les métriques de défragmentation, rapport hello hello charge dans les déclencheurs de cluster hello rééquilibrage lorsqu’il est _ci-dessous_ hello équilibrage du seuil. 
>

Mise en route ci-dessous hello équilibrage seuil n’est pas un objectif explicit. Les seuils d’équilibrage ne sont qu’un *déclencheur*. Lors de l’équilibrage de charge s’exécute hello Gestionnaire de ressources de Cluster détermine quelles améliorations possibles, le cas échéant. Une analyse d’équilibrage ne signifie pas que des données sont déplacées. Hello cluster est parfois toocorrect déséquilibré mais trop limitée. Vous pouvez également les améliorations de hello requièrent les mouvements sont trop [coûteux](service-fabric-cluster-resource-manager-movement-cost.md)).

## <a name="activity-thresholds"></a>seuils d’activité
Dans certains cas, bien que les nœuds sont relativement déséquilibrés, hello *total* de charge dans le cluster de hello est faible. manque de Hello de charge peut être une adresse dip temporaire ou parce que le cluster de hello est nouveau et uniquement lors de l’obtention amorcé. Dans les deux cas, vous souhaiterez pas temps toospend équilibrage de cluster de hello, car il est peu toobe acquise. Si le cluster de hello avoir subi l’équilibrage de vous consacrer réseau et éléments toomove ressources de calcul sans apporter tout grand *absolu* différence. tooavoid inutile se déplace, il existe un autre contrôle appelé seuils d’activité. Seuils d’activité vous permet de toospecify limite de certaines inférieure absolue pour l’activité. Si aucun nœud ne se trouve sur ce seuil, l’équilibrage n’est pas déclenché même si hello équilibrage seuil est atteint.

Supposons que nous conservons notre seuil d’équilibrage de 3 pour cette mesure. Supposons également que nous avons un seuil d’activité de 1 536. Dans le premier cas de hello, alors que le cluster de hello est déséquilibré par hello il seuil d’équilibrage n’est aucun répond aux nœuds de ce seuil d’activité, donc rien se produit. Dans l’exemple hello du bas, Node1 se sur hello seuil de l’activité. Étant donné que deux hello seuil d’équilibrage et hello seuil de l’activité de mesure de hello sont atteints, l’équilibrage est planifié. Par exemple, examinons hello suivant schéma : 

<center>
Exemple de seuil d’activité![][Image3]
</center>

Tout comme l’équilibrage des seuils, des seuils d’activité sont définies par le système métrique via la définition de cluster hello :

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

Seuils d’équilibrage et activité sont tous deux métrique spécifique de tooa liée - équilibrage est déclenchée uniquement si les deux hello seuil d’équilibrage et activité seuil est dépassée pour hello même mesure.

## <a name="balancing-services-together"></a>Équilibrage de plusieurs services en même temps
Si le cluster de hello est déséquilibré ou non est une décision à l’échelle du cluster. Toutefois, moyen hello nous allez résoudre est le déplacement des réplicas de service individuels et les instances autour. Logique, n’est-ce pas ? Si la mémoire est empilée sur un nœud, plusieurs réplicas ou les instances pourraient être cause tooit. Déséquilibre de la correction hello peut nécessiter de déplacer les réplicas avec état de hello ou des instances sans état qui utilisent la métrique de déséquilibré hello.

À l’occasion Cependant, un service qui n’a pas été déséquilibré lui-même est déplacé (n’oubliez pas de discussion hello local et global des poids plus haut). Pourquoi un service serait-il déplacé si toutes les mesures de ce service ont été équilibrées ? Examinons un exemple :

- Prenons par exemple quatre services : Service1, Service2, Service3 et Service4. 
- Service1 signale les mesures Metric1 et Metric2. 
- Service2 signale les mesures Metric2 et Metric3. 
- Service3 signale les mesures Metric3 et Metric4.
- Service4 signale la mesure Metric99. 

Vous voyez certainement où je veux en venir : il s’agit d’une chaîne ! Nous n’avons pas vraiment quatre services indépendants, mais plutôt trois services qui sont liés et un qui est indépendant.

<center>
![Équilibrage de plusieurs services en même temps][Image4]
</center>

En raison de cette chaîne, il est possible qu’un déséquilibre de métriques de 1 à 4 peut provoquer des réplicas ou instances appartenant tooservices toomove 1-3 autour. Nous savons également qu’un déséquilibre de la mesure Metric1, Metric2 ou Metric3 ne peut pas provoquer de déplacements pour le service Service4. Il serait absurde depuis le déplacement de réplicas de hello ou instances appartenant tooService4 autour peut faire rien tooimpact hello équilibre entre les mesures de 1 à 3.

Hello, Gestionnaire de ressources de Cluster effectue automatiquement les services associés. Ajout, suppression ou modification de métriques hello pour les services peuvent avoir un impact sur leurs relations. Par exemple, entre deux exécutions de l’équilibrage de Service2 a peut-être été mis à jour tooremove Metric2. Cela arrête la chaîne hello entre Service1 et Service2. Au lieu de deux groupes de services liés, vous en avez à présent trois :

<center>
![Équilibrage de plusieurs services en même temps][Image5]
</center>

## <a name="next-steps"></a>Étapes suivantes
* Les métriques sont comment hello Gestionnaire de ressources du Cluster Service Fabric gère la consommation et la capacité en cluster de hello. toolearn plus d’informations sur les métriques et comment tooconfigure, extraire [cet article](service-fabric-cluster-resource-manager-metrics.md)
* Le coût du mouvement constitue une méthode de signalisation toohello Gestionnaire de ressources de Cluster que certains services sont toomove plus coûteuse que d’autres. Pour plus d’informations sur le coût du mouvement, consultez trop[cet article](service-fabric-cluster-resource-manager-movement-cost.md)
* Hello, Gestionnaire de ressources du Cluster a plusieurs limitations que vous pouvez configurer tooslow vers le bas de l’évolution du cluster de hello. Elles ne sont normalement pas nécessaires mais, si vous en avez besoin, vous pouvez en savoir plus sur ces limitations [ici](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
