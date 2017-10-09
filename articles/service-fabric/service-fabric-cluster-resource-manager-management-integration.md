---
title: "aaaService Gestionnaire de ressources de Cluster de l’ensemble fibre optique - intégration de la gestion | Documents Microsoft"
description: "Vue d’ensemble de points d’intégration hello entre hello Gestionnaire de ressources du Cluster et la gestion de l’infrastructure de Service."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>Intégration de Cluster Resource Manager à la gestion de cluster Service Fabric
Hello, Gestionnaire de ressources du Cluster Service Fabric ne lecteur mises à niveau dans l’infrastructure de Service, mais il est impliqué. Hello première manière permet de gestionnaire de ressources du Cluster hello avec la gestion par le suivi hello souhaité état du cluster de hello et services hello qu’il contient. Hello, Gestionnaire de ressources de Cluster envoie des rapports d’intégrité lorsqu’il ne peut pas mettre le cluster de hello dans la configuration souhaitée de hello. Par exemple, s’il ne suffit pas hello de capacité Gestionnaire de ressources de Cluster envoie les avertissements et erreurs indiquant hello problème. Une autre partie de l’intégration a toodo avec le fonctionnement des mises à niveau. Hello, Gestionnaire de ressources de Cluster modifie son comportement légèrement pendant les mises à niveau.  

## <a name="health-integration"></a>Intégration de l’intégrité
Hello Gestionnaire de ressources de Cluster suit en permanence règles hello définies pour placer vos services. Il suit également hello restant de capacité pour chaque mesure sur les nœuds hello dans le cluster de hello et dans le cluster de hello dans sa globalité. S’il ne peut pas respecter ces règles ou si la capacité est insuffisante, des erreurs et des avertissements d’intégrité sont émis. Par exemple, si un nœud est sur la capacité et hello Gestionnaire de ressources du Cluster essaiera situation de hello toofix en déplaçant des services. Si elle ne peut pas corriger la situation de hello, il émet un avertissement de contrôle d’intégrité indiquant que le nœud est sur la capacité, ainsi que pour les mesures.

Un autre exemple d’avertissements de l’intégrité du Gestionnaire de ressources hello est les violations de contraintes de placement. Par exemple, si vous avez défini une contrainte de placement (par exemple `“NodeColor == Blue”`) et hello Gestionnaire de ressources détecte une violation de cette contrainte, il émet un avertissement d’intégrité. Cela est vrai pour personnaliser les contraintes et les contraintes par défaut hello (comme les contraintes de domaine d’erreur et de mettre à niveau un domaine hello).

Voici un exemple de rapport d’intégrité. Dans ce cas, le rapport d’intégrité de hello est pour l’une des partitions du service hello système. message de contrôle d’intégrité Hello indique hello réplicas de cette partition sont empaquetés temporairement dans les domaines de mise à niveau insuffisants.

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

Voici ce que nous apprend ce message d’intégrité :

1. Tous les réplicas hello eux-mêmes sont sains : chacune a AggregatedHealthState : Ok
2. violation de Hello contrainte de distribution de mise à niveau domaine actuellement en cours. Cela signifie qu’un domaine de mise à niveau particulier compte plus de réplicas que prévu pour cette partition.
3. Le nœud contenant la violation de hello hello réplica à l’origine. Dans ce cas, il est nœud hello portant le nom hello « Node.8 »
4. Si cette partition fait actuellement l’objet d’une mise à niveau (« Currently Upgrading -- false »).
5. Hello stratégie de distribution pour ce service : « Distribution stratégie--compression ». Cela est régie par hello `RequireDomainDistribution` [stratégie de positionnement](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). « Packing » indique que dans ce cas, la distribution de domaine n’était _pas_ obligatoire. Nous savons donc que la stratégie de positionnement n’a pas été spécifiée pour ce service. 
6. Lorsque les rapports hello s’est produite - 8/10/2015 7:13:02 PM

Plus d’informations, comme ce que sont activés en toolet production vous connaissez quelque chose s’est produite et il est également utilisé toodetect vous alerte compétences et interrompre les mises à niveau incorrectes. Dans ce cas, nous voulons toosee si nous pouvons déterminer pourquoi hello Gestionnaire de ressources a toopack des réplicas de hello en hello domaine de mise à niveau. En général de livraison sont transitoire étant nœuds hello Bonjour autres domaines de mise à niveau vers le bas, par exemple.

Supposons que hello Gestionnaire de ressources de Cluster tente de tooplace certains services, mais il ne sont pas toutes les solutions qui fonctionnent. Lorsque les services ne peut pas être placées, il est généralement pour l’une des hello suivant raisons :

1. Une condition transitoire rend impossible tooplace cette instance de service ou d’un réplica correctement
2. configuration requise de la sélection élective du service Hello est inacceptable.

Dans ces cas, les rapports d’intégrité à partir de hello Gestionnaire de ressources de Cluster vous aider à déterminer pourquoi le service de hello ne peut pas être placé. Nous appelons cette séquence d’élimination des processus hello contrainte. Au cours de le, système de hello Guide contraintes hello configuré qui affectent les enregistrements et les service hello qu’elles éliminent. De cette manière lorsque les services ne sont pas en mesure de toobe placée, vous pouvez voir les nœuds qui ont été éliminés et pourquoi.

## <a name="constraint-types"></a>Types de contrainte
Examinons chacune des contraintes différentes de hello dans ces rapports d’intégrité. Vous verrez les contraintes d’intégrité messages toothese connexes lorsque les réplicas ne peuvent pas être placées.

* **ReplicaExclusionStatic** et **ReplicaExclusionDynamic**: ces contraintes indique qu’une solution a été rejetée, car les deux objets de service à partir de hello même partition auriez toobe placé sur hello même nœud. Cette opération n’est pas autorisée, car une défaillance de ce nœud aurait un trop fort impact sur cette partition. ReplicaExclusionStatic et ReplicaExclusionDynamic sont hello presque les mêmes différences de règle et hello importent peu. Si vous voyez une séquence d’élimination de contrainte contenant soit hello ReplicaExclusionStatic ou ReplicaExclusionDynamic une contrainte, hello Gestionnaire de ressources du Cluster pense qu’il n’existe pas de suffisamment de nœuds. Cela nécessite restant toouse des solutions à ces emplacements non valides qui ne sont pas autorisées. Hello autres contraintes dans la séquence de hello seront généralement dites-nous pourquoi les nœuds sont éliminés en premier lieu de hello.
* **PlacementConstraint**: Si vous voyez ce message, cela signifie que nous avons éliminé certains nœuds, car ils ne correspondent pas les contraintes de placement du service hello. Nous avons suivi des contraintes de placement hello actuellement configuré dans le cadre de ce message. Ceci est normal si une contrainte de placement est définie. Toutefois, si contrainte de placement provoque incorrectement trop de nœuds toobe éliminé Voici comment vous noterez.
* **NodeCapacity**: cette contrainte signifie que hello Gestionnaire de ressources de Cluster n’a pas pu placer des réplicas de hello sur hello indiqué nœuds car qui les place sur la capacité.
* **Affinité**: cette contrainte indique que nous n’avons pas pu placer les réplicas hello sur les nœuds hello affecté, car cela provoquerait une violation de contrainte d’affinité hello. Plus d’informations sur la contrainte Affinity, lisez [cet article](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
* **FaultDomain** et **UpgradeDomain**: cette contrainte élimine les nœuds si placement réplica hello sur hello indiqué nœuds provoquerait de livraison dans un domaine de mise à niveau ou de pannes particulier. Plusieurs exemples décrivant cette contrainte sont présentées dans la rubrique de hello sur [mise à niveau d’erreur et de contraintes de domaine et le comportement qui en résulte](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**: ne devrait plus normalement cette contrainte de suppression de nœuds à partir de la solution de hello, car il s’exécute en guise d’optimisation par défaut. Hello préféré contrainte d’emplacement est également présent pendant les mises à niveau. Au cours de la mise à niveau, il est toowhere de précédent de services toomove utilisé lors de la mise à niveau hello a démarré.

## <a name="blocklisting-nodes"></a>Mise des nœuds en liste de blocage
Un autre contrôle d’intégrité message hello Gestionnaire de ressources du Cluster est lorsque les nœuds sont blocklisted. La mise des nœuds en liste de blocage peut être considérée comme une contrainte provisoire qui s’applique automatiquement. Les nœuds sont mis en liste de blocage quand ils subissent des défaillances à répétition pendant le lacement d’instances de ce type de service. Les nœuds sont mis en liste de blocage par type de service, si bien qu’un nœud peut être placé dans une liste de blocage pour un type de service, mais pas pour un autre. 

Vous verrez blocklisting bannir souvent au cours du développement : certains bogue entraîne votre toocrash d’hôte de service au démarrage. Service Fabric tente d’hôte de service hello toocreate plusieurs fois et Échec de hello continue de se produire. Après plusieurs tentatives, nœud de hello obtient blocklisted et hello Gestionnaire de ressources de Cluster va tenter de service de hello toocreate ailleurs. Si cette défaillance conserve se produit sur plusieurs nœuds, il est possible que tous les nœuds de valide hello dans hello cluster finissent bloqué. Blocklisting peut également supprimer des nœuds autant que pas assez peut démarrer correctement mise à l’échelle de hello service toomeet hello souhaité. Vous verrez généralement d’autres erreurs ou avertissements du Gestionnaire de ressources du Cluster de hello indiquant que le service de hello est inférieur à réplica souhaité de hello ou le nombre d’instances, ainsi que les messages de contrôle d’intégrité indiquant le dysfonctionnement hello est qui entraîne un toohello blocklisting en premier lieu de hello.

La mise en liste de blocage n’est pas une condition permanente. Après quelques minutes, nœud de hello est supprimée à partir de la liste de blocage hello et Service Fabric peut réactiver les services hello sur ce nœud. Si les services continuent toofail, nœud de hello est blocklisted pour ce type de service. 

### <a name="constraint-priorities"></a>Priorités de contrainte

> [!WARNING]
> Il n’est pas recommandé de modifier les priorités des contraintes. De plus, cela peut avoir des répercutions défavorables sur votre cluster. Hello sous informations est fourni à titre de référence de priorités de contrainte par défaut hello et leur comportement. 
>

Toutes ces contraintes, vous avez été pensez « bonjour – je pense que les contraintes de domaine d’erreur sont hello plus important dans mon système. Dans l’ordre tooensure hello contrainte de domaine d’erreur n’est pas n’a pas respecté, j’envisage tooviolate autres contraintes. »

Les contraintes peuvent être configurées avec différents niveaux de priorité, Ces composants sont les suivants :

   - « stricte » (0)
   - « souple » (1)
   - « optimisation » (2)
   - « désactivé » (-1). 
   
La plupart des contraintes de hello est configurée en tant que disque durs contraintes par défaut.

Il n’est pas rare de modification de la priorité de hello de contraintes. Il y a eu des fois où les priorités de contrainte nécessaire toochange, généralement toowork autour d’un autre bogue ou un autre comportement qui avait un impact sur les environnement de hello. Généralement une grande souplesse hello de l’infrastructure de priorité de contrainte hello a fonctionné très bien, mais il n’est pas nécessaire de souvent. Plupart du temps hello que tout se situe au niveau de leur priorité par défaut. 

niveaux de priorité Hello ne signifient qu’une contrainte donnée _sera_ violées, ni qu’il est toujours rempli. Les priorités des contraintes définissent l’ordre dans lequel les contraintes sont appliquées. Les priorités définissent les compromis hello lorsqu’il est impossible toosatisfy toutes les contraintes. Généralement, toutes les contraintes de hello peuvent être satisfaites sauf s’il existe situe ailleurs dans l’environnement de hello. Quelques exemples de scénarios qui entraîneront des violations de tooconstraint sont des contraintes en conflit, ou un grand nombre de défaillances simultanées.

Dans des situations avancées, vous pouvez modifier les priorités de contrainte hello. Par exemple, imaginons que vous vouliez tooensure qu’affinité serait toujours violée lors de problèmes de capacité des nœuds toosolve nécessaire. tooachieve, vous pouvez définir la priorité de hello de contrainte d’affinité hello trop « soft » (1) et laisser hello capacité contrainte a la valeur trop « matérielle » (0).

valeurs de priorité par défaut Hello pour des contraintes différentes hello sont indiquées dans hello suivant la configuration :

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

via ClusterConfig.json pour les déploiements autonomes ou Template.json pour les clusters hébergés sur Azure :

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>Contraintes de domaine d’erreur et de domaine de mise à niveau
Hello, Gestionnaire de ressources du Cluster veut services tookeep réparties sur les domaines d’erreur et la mise à niveau. Elle ce modèle en tant que contrainte à l’intérieur du Gestionnaire de ressources Cluster hello moteur. Pour plus d’informations sur la façon dont elles sont utilisées et leur comportement spécifique, consultez l’article de hello sur [configuration de cluster](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).

Hello, Gestionnaire de ressources du Cluster peut-être toopack deux réplicas dans un domaine de mise à niveau dans toodeal d’ordre avec les mises à niveau, les échecs ou les autres violations de contrainte. Dans des domaines d’erreur ou de mise à niveau de compression normalement se produit uniquement lorsqu’il existe plusieurs échecs ou les autres de l’évolution du système hello empêche la sélection élective appropriés. Si vous le souhaitez tooprevent compression même pendant ces situations, vous pouvez utiliser hello `RequireDomainDistribution` [stratégie de positionnement](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). Notez que cela peut avoir des effets secondaires et nuire à la disponibilité et à la fiabilité du service. Pensez-y avant toute décision dans ce sens.

Si l’environnement de hello est correctement configuré, toutes les contraintes sont respectées pleinement, même pendant les mises à niveau. important Hello est que hello vos contraintes observe Gestionnaire de ressources du Cluster. Lorsqu’il détecte une violation il immédiatement le signale et tente de problème de hello toocorrect.

## <a name="hello-preferred-location-constraint"></a>contrainte d’emplacement Hello préféré
Hello PreferredLocation contrainte est un peu différent, car elle a deux différentes utilisations. D’une part, cette contrainte est utilisée pendant les mises à niveau d’applications. Hello, Gestionnaire de ressources de Cluster gère automatiquement cette contrainte pendant les mises à niveau. Il est utilisé tooensure qui une fois la mise à niveau sont terminées réplicas retournent tootheir emplacements initiales. Hello autres hello PreferredLocation contrainte est utilisé pour hello [ `PreferredPrimaryDomain` stratégie de positionnement](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md). Ces deux éléments sont des optimisations et hello PreferredLocation contrainte n’est donc hello seule contrainte défini trop « Optimisation » par défaut.

## <a name="upgrades"></a>Mises à niveau
Hello, Gestionnaire de ressources du Cluster permet également d’applications et mises à niveau de cluster, au cours de laquelle il a deux tâches :

* Assurez-vous que les règles hello du cluster de hello ne sont pas compromis
* Essayez d’atteindre de mise à niveau toohelp hello sans heurts

### <a name="keep-enforcing-hello-rules"></a>Continuer à appliquer les règles de hello
toobe d’essentiel Hello prenant en charge d’est que hello règles – hello stricte les contraintes telles que les contraintes de placement et capacités - sont toujours appliquées pendant les mises à niveau. Les contraintes de placement s’assurent que vos charges de travail s’exécutent uniquement où elles y sont autorisées, notamment pendant les mises à niveau. Quand les services sont très ralentis, les mises à niveau peuvent prendre plus de temps. Lorsque le service de hello ou nœud hello sur qu'elle s’exécute est arrêté pour une mise à jour, il peut y avoir plusieurs options pour où il peut accéder.

### <a name="smart-replacements"></a>Remplacements actifs
Lorsqu’une mise à niveau démarre, hello Gestionnaire de ressources prend un instantané de la disposition actuelle de hello du cluster de hello. Comme chaque domaine de mise à niveau terminée, il tente de services hello tooreturn qui étaient dans cette organisation d’origine tootheir de domaine de mise à niveau. De cette manière il existe au maximum deux transitions d’un service au cours de la mise à niveau hello. Il existe un déplacement hors du nœud de hello affecté et un replacer. Retour hello toohow cluster ou un service qu'où elle était avant la mise à niveau hello garantit également la mise à niveau hello n’affecte pas la mise en page hello du cluster de hello. 

### <a name="reduced-churn"></a>Évolution limitée
Une autre chose qui se produit pendant les mises à niveau est que hello Gestionnaire de ressources du Cluster désactive l’équilibrage. Empêche l’équilibrage empêche réactions inutiles toohello mise à niveau lui-même, comme le déplacement des services dans les nœuds qui ont été vidées pour la mise à niveau hello. Si la mise à niveau de hello en question est une mise à niveau de Cluster, cluster entier de hello n’est pas équilibré au cours de la mise à niveau hello. Vérifications de contraintes restent actives, mouvement uniquement en fonction de hello proactive équilibrage des métriques est désactivée.

### <a name="buffered-capacity--upgrade"></a>Capacité mise en mémoire tampon et mise à niveau
Vous voulez généralement que toocomplete de mise à niveau hello même si le cluster de hello est toofull de contrainte ou de fermeture. Gestion de la capacité de hello du cluster de hello est encore plus importante pendant les mises à niveau que d’habitude. En fonction de hello, nombre de domaines de mise à niveau, entre 5 et 20 pour cent de la capacité de doit être migré lors hello mise à niveau via le cluster de hello. Ce travail a toogo quelque part. Cela est hello où la notion de [mis en mémoire tampon des capacités](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) est utile. La capacité mise en mémoire tampon est respectée en phase de fonctionnement normal. Hello, Gestionnaire de ressources du Cluster peut se remplir des nœuds de la capacité totale de tootheir (consommation de mémoire tampon de hello) pendant les mises à niveau si nécessaire.

## <a name="next-steps"></a>Étapes suivantes
* Démarrer à partir du début de hello et [obtenir une présentation de toohello Gestionnaire de ressources du Cluster Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
