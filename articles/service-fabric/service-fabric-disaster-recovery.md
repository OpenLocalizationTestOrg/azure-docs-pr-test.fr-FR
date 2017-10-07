---
title: "aaaAzure la récupération d’urgence Service Fabric | Documents Microsoft"
description: "Azure Service Fabric offre toodeal nécessaires de fonctionnalités hello avec tous les types de sinistres. Cet article décrit les types de hello de sinistres qui peuvent se produire et comment toodeal avec eux."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Récupération d’urgence dans Azure Service Fabric
Pour fournir une haute disponibilité, il est essentiel que les services puissent survivre à tous les types d’échecs. Ceci est particulièrement important pour les échecs inattendus et hors de votre contrôle. Cet article décrit certains modes d’échec courants qui peuvent aboutir à une situation critique s’ils ne sont pas modélisés et gérés correctement. Il traite également les limitations de risques et les actions tootake si un incident s’est produite quand même. objectif de Hello est toolimit ou éliminer le risque de hello d’interruption ou perte de données lorsqu’ils produisent des échecs, planifiés ou dans le cas contraire, se produisent.

## <a name="avoiding-disaster"></a>Éviter les incidents
Objectif de principal du service Fabric est toohelp modèle de votre environnement et vos services de manière à ce que les types d’échec courants ne sont pas des sinistres. 

En général, il existe deux types de scénarios d’incident/échec :

1. Défaillances matérielles ou logicielles
2. Défaillances opérationnelles

### <a name="hardware-and-software-faults"></a>Défaillances matérielles et logicielles
Les défaillances matérielles et logicielles sont imprévisibles. erreurs toosurvive moyen plus simple de Hello est en cours d’exécution plus de copies du service hello sur lesquelles s’étend au-delà des limites de panne matérielle ou logicielle. Par exemple, si votre service s’exécute uniquement sur un ordinateur particulier, puis hello Échec de qu’un ordinateur est un incident pour ce service. Hello facilement tooavoid cet incident est tooensure hello service est réellement exécuté sur plusieurs ordinateurs. Le test est également Échec de hello tooensure nécessaires d’un ordinateur ne perturbe hello service en cours d’exécution. Planification de la capacité garantit une instance de remplacement peut être créée ailleurs et que la réduction de la capacité ne surcharge pas hello restant des services. Hello même modèle fonctionne indépendamment de ce que vous essayez d’échec de hello tooavoid de. Par exemple, Si vous êtes inquiet de la défaillance de hello d’un réseau SAN, vous exécutez entre plusieurs SAN. Si vous êtes inquiet de la perte de hello d’un rack de serveurs, vous exécutez sur plusieurs racks. Si vous êtes inquiet de la perte de hello des centres de données, votre service doit s’exécuter sur plusieurs régions Azure ou des centres de données. 

Lors de l’exécution dans ce type de mode fractionné, vous êtes toujours de types d’objets toosome de défaillances simultanées, mais seul et même plusieurs échecs d’un type particulier (ex : un échec de liaison réseau ou de la machine virtuelle unique) sont gérées automatiquement (et par conséquent, ne sont plus « urgence »). Service Fabric fournit de nombreux mécanismes pour le développement du cluster de hello et les handles remettant les nœuds ayant échoué et services. Service Fabric permet aussi d’utiliser plusieurs instances de vos services dans l’ordre tooavoid ces types de défaillances non planifiées de tourner en sinistres réels.

Il peut y avoir des raisons pour lesquelles un toospan suffisamment grand déploiement en cours d’exécution sur les échecs n’est pas possible. Par exemple, il peut prendre plus de ressources matérielles que vous n’êtes pas prêt toopay pour toohello relatif des risque d’échouer. Lorsque vous utilisez des applications distribuées, il est possible que des tronçons de communication ou des coûts de réplication d’état supplémentaires vers des sites distants provoquent une latence inacceptable. Votre décision doit être prise en fonction de chaque application. Pour les erreurs de logiciel en particulier, les pannes hello peut être dans le service hello que vous essayez de tooscale. Dans ce cas plus de copies n’empêchent pas d’urgence hello, étant donné que la condition d’échec hello est corrélée à toutes les instances de hello.

### <a name="operational-faults"></a>Défaillances opérationnelles
Même si votre service est fractionné monde hello avec nombreuses redondances, il peut toujours rencontrer événements désastreux. Par exemple, si une personne reconfigure le nom dns de hello pour le service de hello, accidentellement ou supprime le ferme. Par exemple, imaginons que vous disposiez d’un service Service Fabric avec état, et que quelqu’un ait supprimé ce service par inadvertance. Sauf s’il existe certains autres atténuation, ce service et tout état hello qu’il avait est désormais disparu. Ces incidents opérationnels (de type « Désolé… ») nécessitent des mesures d’atténuation des risques et une procédure de récupération différentes de celles employées pour les défaillances inattendues. 

ces types d’erreurs opérationnelles Hello meilleures méthodes tooavoid doivent
1. restreindre l’environnement de toohello accès opérationnel
2. Réaliser un audit strict des opérations dangereuses
3. imposer l’automation, empêcher manuelle ou hors bande apportées et valider les modifications spécifiques par rapport à l’environnement réel de hello avant d’adopter les
4. Faire en sorte que les opérations de destruction ne soient pas définitives. Les opérations non définitives ne sont pas appliquées immédiatement ou peuvent être annulées dans un certain délai.

Service Fabric fournit certains mécanismes tooprevent erreurs opérationnelles, telles que l’insertion [en fonction du rôle](service-fabric-cluster-security-roles.md) contrôle d’accès pour les opérations de cluster. Toutefois, pour éviter la plupart de ces défaillances, des efforts d’organisation et des systèmes supplémentaires sont nécessaires. Service Fabric fournit un mécanisme permettant de survivre aux défaillances opérationnelles, notamment la sauvegarde et la restauration des services avec état.

## <a name="managing-failures"></a>Gestion des défaillances
Hello objectif de Service Fabric est presque toujours la gestion automatique des échecs. Toutefois, dans commande toohandle certains types d’échecs, les services doivent avoir le code supplémentaire. Certains types de défaillances _ne doivent pas_ être gérés automatiquement, pour des raisons de sécurité et de continuité opérationnelle. 

### <a name="handling-single-failures"></a>Gestion des défaillances uniques
Les machines uniques peuvent connaître une défaillance pour diverses raisons. L’origine de la défaillance peut être matérielle, comme dans le cas d’une défaillance de l’alimentation ou du matériel réseau. Certaines défaillances peuvent se situer au niveau du logiciel. Il s’agit notamment des défaillances de hello réelle du système d’exploitation et service hello proprement dit. Service Fabric détecte automatiquement ces types de défaillances, y compris les cas où machine de hello est isolé des autres ordinateurs en raison de problèmes de toonetwork.

Quel type hello du service, l’exécution une seule instance génère un temps d’arrêt de ce service si cette copie unique du code de hello échoue pour une raison quelconque. 

Dans l’ordre toohandle de panne, hello plus simple que vous pouvez effectuer consiste tooensure vos services s’exécutent sur plusieurs nœuds par défaut. Pour les services sans état, il suffit de définir `InstanceCount` sur une valeur supérieure à 1. Pour les services avec état, recommandation minimale de hello est toujours un `TargetReplicaSetSize` et `MinReplicaSetSize` d’au moins 3. Le fait d’exécuter plusieurs copies du code de votre service permet au service de gérer automatiquement les défaillances uniques. 

### <a name="handling-coordinated-failures"></a>Gestion des défaillances multiples
Échecs de coordonnées peuvent se produire dans un cluster dû tooeither planifié ou les échecs d’infrastructure non planifié et les modifications ou les modifications apportées au logiciel planifié. Service Fabric modélise les zones d’infrastructure qui rencontrent des défaillances multiples comme des domaines d’erreur. Les zones qui subissent des modifications logicielles coordonnées sont modélisées comme des domaines de mise à niveau. Pour plus d’informations sur les domaines d’erreur et de mise à niveau, consultez [ce document](service-fabric-cluster-resource-manager-cluster-description.md) qui donne une définition des clusters et explique leur topologie.

Par défaut, Service Fabric prend en compte les domaines d’erreur et de mise à niveau lorsqu’il planifie où vos services doivent s’exécuter. Par défaut, le Service Fabric tente tooensure vos services exécutent à plusieurs domaines d’erreur et de mise à niveau de sorte que si des modifications planifiées ou non se produisent vos services restent disponibles. 

Par exemple, supposons que la défaillance d’une source d’alimentation provoque un rack de machines toofail simultanément. Avec plusieurs copies du service hello perte hello de nombreux ordinateurs en cours d’exécution dans l’échec de domaine d’erreur transforme juste un autre exemple de défaillance unique pour un service donné. C’est pourquoi la gestion des domaines d’erreur sont critique tooensuring haute disponibilité de vos services. Lorsque vous exécutez Service Fabric dans Azure, les domaines d’erreur sont gérés automatiquement. Cela peut ne pas être le cas dans d’autres environnements. Si vous créez votre propre clusters sur site, être toomap sûr et planifier votre mise en page du domaine erreur correctement.

Les domaines de mise à niveau sont utiles pour modéliser les zones où logiciel va toobe mis à niveau en hello même temps. Pour cette raison, les domaines de mise à niveau définissent également souvent des limites de hello où le logiciel est arrêté pendant les mises à niveau. Mises à niveau de l’infrastructure de Service et vos services suivent hello même modèle. Pour plus d’informations sur le déploiement des mises à niveau, les domaines de mise à niveau et modèle de contrôle d’intégrité de Service Fabric hello qui permet d’empêcher des modifications non souhaitées à partir de l’impact sur le cluster de hello et votre service, consultez ces documents :

 - [Mise à niveau de l’application](service-fabric-application-upgrade.md)
 - [Tutoriel sur la mise à niveau des applications](service-fabric-application-upgrade-tutorial.md)
 - [Modèle d’intégrité Service Fabric](service-fabric-health-introduction.md)

Vous pouvez visualiser la mise en page hello de votre cluster à l’aide de la carte de cluster hello fourni dans [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md):

<center>
![Nœuds répartis dans les domaines d’erreur dans Service Fabric Explorer][sfx-cluster-map]
</center>

> [!NOTE]
> Domaines de défaillance, propagée, exécutant plusieurs instances de votre code de service et l’état, de modélisation tooensure de règles de sélection élective vos services s’exécutent sur plusieurs domaines d’erreur et de mise à niveau, et contrôle d’intégrité intégrée sont simplement **certaines** de hello fonctionnalités fournies par l’infrastructure de Service dans les problèmes de fonctionnement normal tookeep order et d’échecs de sinistres se. 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>Gestion des défaillances matérielles ou logicielles simultanées
Nous avons parlé précédemment des défaillances uniques. Comme vous pouvez le voir, sont toohandle facile pour les services avec et sans état simplement en conservant des copies du code de hello (et état) est en cours d’exécution entre les domaines d’erreur et mise à niveau. Les défaillances multiples, simultanées et aléatoires sont également possibles. Il s’agit probablement toolead tooan réel reprise après sinistre.


### <a name="random-failures-leading-tooservice-failures"></a>Défaillances aléatoires tooservice échecs de début
Supposons que le service de hello est un `InstanceCount` de 5 et plusieurs nœuds ces instances en cours d’exécution tout échec à hello même temps. Service Fabric répond à cette situation en créant automatiquement des instances de remplacement sur d’autres nœuds. Il va continuer à créer des remplacements jusqu'à ce que le service de hello est de retour tooits souhaité le nombre d’instances. En un autre exemple, supposons qu’il était un service sans état avec un `InstanceCount`-1, ce qui signifie qu’il fonctionne sur tous les nœuds de cluster de hello valides. Supposons que certaines de ces instances ont été toofail. Dans ce cas, le Service Fabric Remarque que service de hello n’est pas dans son état souhaité et tente d’instances de hello toocreate sur les nœuds hello où ils sont manquants. 

Pour les services avec état situation de hello dépend de si le service de hello est en état persistant ou non. Il dépend également du nombre service hello de réplicas est et le nombre d’échecs. Pour déterminer si un incident s’est produit pour un service avec état et pour gérer cet incident, effectuez les trois étapes suivantes :

1. Déterminez s’il y a eu perte de quorum, ou non
 - Une perte de quorum est à tout moment une majorité des réplicas hello d’un service avec état sont arrêtés à hello même temps, y compris hello principal.
2. Déterminer si la perte de quorum hello est permanente ou non
 - La plupart du temps de hello, les échecs sont transitoires. Les processus sont redémarrés, les nœuds sont redémarrés, les machines virtuelles sont relancées et les partitions réseau sont réparées. Cependant, il arrive que les défaillances soient permanentes. 
    - Pour les services non persistants, la défaillance d’un quorum ou de plusieurs réplicas aboutit _immédiatement_ à une perte de quorum permanente. Lorsque le Service Fabric détecte la perte de quorum dans un service non persistants avec état, il poursuit immédiatement perte de toostep 3 en déclarant (risque). Continuer toodataloss judicieux, car le Service Fabric sait qu’il n’existe aucun point dans l’attente hello réplicas toocome précédent, car même si elles ont été récupérées ils seraient vides.
    - Pour les services persistants avec état, une défaillance d’au moins un quorum de réplicas provoque toostart Service Fabric en attente de hello réplicas toocome précédent et de restauration du quorum. Cela entraîne une interruption de service pour les _écrit_ toohello affectée partition (ou « jeu de réplica ») du service de hello. Cependant, les opérations de lecture sont toujours possibles, avec toutefois une moins bonne garantie de cohérence. Hello est par défaut du délai d’attente de Service Fabric pour toobe quorum restaurée infinie, étant donné que la procédure est un événement de perte (potentiel) et exécute d’autres risques. Substitution de valeur par défaut hello `QuorumLossWaitDuration` valeur n’est possible, mais n’est pas recommandée. À ce stade, tous les efforts doivent plutôt être effectuées hello toorestore réplicas vers le bas. Cela nécessite de mettre des nœuds hello qui sont arrêtés arrière des et de s’assurer qu’ils peuvent remonter lecteurs hello sur leur état permanent de hello local de stockage. Si la perte de quorum hello est provoquée par un échec d’un processus, Service Fabric tente de processus de hello toorecreate automatiquement et redémarrer les réplicas hello qu’ils contiennent. En cas d’échec, Service Fabric signale des erreurs d’intégrité. S’il peuvent être résolus puis les réplicas hello généralement sont revenir. Parfois, cependant, les réplicas hello ne peut pas remettre en. Par exemple, les lecteurs hello tous a peut-être échoué ou physiquement les ordinateurs hello détruit une certaine manière. Dans ces cas-là, nous avons une perte de quorum permanente. tootell toostop de l’infrastructure de Service en attente de hello bas toocome réplicas, un administrateur de cluster doit déterminer quelles partitions dont les services sont affectés et appellent hello `Repair-ServiceFabricPartition -PartitionId` ou ` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)` API.  Cette API permet de spécifier l’ID de hello de hello partition toomove hors service QuorumLoss et en la perte potentielle.

> [!NOTE]
> Il s’agit de _jamais_ safe toouse cette API autre que d’une manière ciblée par rapport à des partitions spécifiques. 
>

3. Déterminez si une perte de données a bien eu lieu et restaurez-les à partir des sauvegardes
  - Lorsque le Service Fabric appelle hello `OnDataLossAsync` méthode, il est toujours dû au fait _suspectée_ perte. L’infrastructure de service permet de s’assurer que cet appel est remis toohello _meilleures_ réplica restant. Il s’agit de tout réplica a progressé hello la plupart des. Hello raison nous dire toujours _suspectée_ perte est qu’il est possible que ce réplica restant hello a effectivement tous les États même hello principal comme lorsqu’il s’est arrêté. Toutefois, sans que toocompare état il, il s’applique pas pour le Service Fabric ou opérateurs tooknow sûr. À ce stade, l’infrastructure de Service sait également hello autres réplicas ne sont pas revenir. Qui a été hello décision lorsque nous avons arrêté en attente de tooresolve de perte de quorum hello lui-même. Hello meilleur plan d’action pour le service de hello est généralement toofreeze et attendre qu’une intervention administrative spécifique. Par conséquent, ce que fait une implémentation classique des hello `OnDataLossAsync` méthode faire ?
  - Tout d’abord, créez une entrée de journal dans laquelle vous indiquerez que `OnDataLossAsync` a été déclenché, puis déclenchez les alertes d’administration nécessaires.
   - Généralement à ce stade, toopause et patientez davantage les décisions et toobe des actions manuelles effectuées. Il s’agit, car même si les sauvegardes sont disponibles, ils peuvent doivent toobe préparée. Par exemple, si les deux services la coordination des informations, ces sauvegardes peut-être toobe modifié dans tooensure de commande une fois la restauration de hello se produit que les informations de hello ces deux services intéressent est cohérent. 
  - Il existe souvent également certaines autres télémétrie ou échappement à partir du service de hello. Ces métadonnées peuvent être contenues dans d’autres services ou dans des journaux. Ces informations peuvent être utilisée toodetermine nécessaire s’il y a tout appel reçu et traité à hello principal qui n’étaient pas présentes dans le réplica spécifique de sauvegarde ou répliquées toothis hello. Ces peut-être toobe toohello relus ou a été ajoutée sauvegarde avant la restauration est possible.  
   - Comparaisons de hello restant toothat d’état du réplica contenu dans toutes les sauvegardes qui sont disponibles. Si hello Service Fabric fiables regroupements puis il existe des outils et des processus disponibles pour ce faire, décrite dans [cet article](service-fabric-reliable-services-backup-restore.md). Hello vise toosee Si état hello dans les réplicas hello est suffisant, ou également le sauvegarde hello est peut-être manquant.
  - Une fois hello sont comparées, et si nécessaire hello restauration terminée, le code de service hello doit retourner true si les modifications d’état ont été apportées. Si les réplicas hello déterminé qu’il a été hello mieux copie disponible de l’état de hello et apporté aucune modification, retourne false. La valeur true indique que les _autres_ réplicas restants peuvent maintenant ne plus être cohérents avec ce réplica. Ils sont donc supprimés et reconstruits à partir de ce réplica. La valeur False indique qu’aucune modification d’état ont été apportées, donc hello autres réplicas peuvent conserver leur. 

Il est extrêmement important que les auteurs du service testent les scénarios de défaillance et de perte de données potentielle avant de déployer les services dans l’environnement de production. tooprotect par rapport à la possibilité de hello de perte, il est important tooperiodically [sauvegarder hello état](service-fabric-reliable-services-backup-restore.md) de n’importe quel de votre magasin de géo-redondant tooa services avec état. Vous devez également vous assurer que vous avez hello capacité toorestore il. Étant donné que les sauvegardes de nombreux services différents sont effectuées à des moments différents, vous devez tooensure qu’après une restauration de vos services ont une vue cohérente de l’autre. Par exemple, prenons le cas où un seul service génère un nombre et elle stocke, puis l’envoie service tooanother qui les stocke également. Après une restauration, vous pouvez découvrir que hello deuxième service n’ayant le numéro de hello mais hello tout d’abord pas, car sa sauvegarde n’a pas inclure cette opération.

Si vous découvrez que hello restant réplicas sont insuffisante toocontinue à partir de dans un scénario de perte, et vous ne pouvez pas reconstruire l’état de service de télémétrie ou d’échappement, fréquence hello de vos sauvegardes détermine votre meilleur objectif de point de récupération (RPO) . Service Fabric fournit de nombreux outils pour tester divers scénarios d’échec, y compris la perte de quorum permanente et la perte de données qui nécessitent une restauration à partir d’une sauvegarde. Ces scénarios sont inclus dans le cadre des outils de testabilité du Service Fabric, gérés par hello erreur Analysis Service. Pour plus d’informations sur ces outils et ces modèles, [cliquez ici](service-fabric-testability-overview.md). 

> [!NOTE]
> Services système peuvent également subir des perte de quorum, avec un impact hello en cours spécifique toohello service en question. Par exemple, une perte de quorum dans le service d’affectation de noms hello a un impact sur résolution de noms, alors que la perte de quorum dans service manager de basculement hello bloque les basculements et la création du nouveau service. Alors que les services de système de Service Fabric hello suivent hello même modèle en tant que vos services de gestion d’état, il est déconseillé que vous devez essayer de toomove leur hors service une perte de Quorum et en la perte potentielle. Hello est recommandé à la place trop[prise en charge de la recherche](service-fabric-support.md) toodetermine une solution qui est ciblé tooyour chaque situation.  Généralement, il est préférable de toosimply attente jusqu'à ce que hello réplicas retournés vers le bas.
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Disponibilité du cluster Service Fabric de hello
En règle générale, le cluster Service Fabric de hello lui-même est un environnement hautement distribué sans point de défaillance. Échec de l’un des nœuds n’engendre pas disponibilité ou des problèmes de fiabilité pour le cluster de hello, principalement car les services de système de Service Fabric hello suivent hello mêmes instructions fournies plus haut : ils toujours s’exécuter avec au moins trois réplicas par défaut et les services système qui sont sans état exécutent tous les nœuds. mise en réseau de l’infrastructure de Service sous-jacent Hello et les couches de détection de défaillance sont entièrement distribuées. La plupart des services système peuvent être reconstruites à partir des métadonnées dans un cluster de hello, ou savoir comment tooresynchronize leur état à partir d’autres emplacements. disponibilité Hello du cluster de hello peut être détournée si obtenir des services système dans quorum perte situations telles que celles décrites ci-dessus. Dans ces cas, vous ne soyez pas en mesure de tooperform certaine opérations sur le cluster de hello à commencer une mise à niveau ou de déploiement de nouveaux services, mais hello cluster lui-même fonctionne toujours. Les services sur déjà en cours d’exécution reste en cours d’exécution dans ces conditions, sauf si elles nécessitent des écritures toohello système services toocontinue fonctionne. Par exemple, si hello Gestionnaire de basculement est une perte de quorum, tous les services continuent toorun, mais tous les services qui échouent ne sera pas en mesure de tooautomatically redémarrage, car cela requiert l’implication hello Hello Gestionnaire de basculement. 

### <a name="failures-of-a-datacenter-or-azure-region"></a>Défaillance d’un centre de données ou d’une région Azure
Dans de rares cas, un centre de données physique peut devenir temporairement indisponible en raison de tooloss de connectivité réseau ou d’alimentation. Dans ce cas, les clusters et services Service Fabric du centre de données ou de la région Azure ne sont plus disponibles. Toutefois, _vos données sont conservées_. Pour les clusters en cours d’exécution dans Azure, vous pouvez afficher les mises à jour sur les pannes sur hello [page d’état Azure][azure-status-dashboard]. Bonjour très improbable d’un centre de données physique est partiellement ou entièrement détruit, tous les clusters Service Fabric hébergés ou les services hello pourraient être perdues. Cela comprend les états non sauvegardés en dehors du centre de données ou de la région.

Il existe deux stratégies différentes pour survivant hello défaillance permanente ou maintenu d’un seul centre de données ou une région. 

1. Exécuter des clusters Service Fabric distincts dans plusieurs régions de ce type et utiliser un mécanisme de basculement et de restauration automatiques entre ces environnements. Ce type de modèle multicluster actif-actif ou actif-passif nécessite du code de gestion et d’opération supplémentaire. Cela requiert également la coordination des sauvegardes à partir des services hello dans un centre de données ou une région afin qu’ils soient disponibles dans d’autres centres de données ou les régions lorsqu’un échec. 
2. Exécuter un cluster Service Fabric qui s’étend sur plusieurs centres de données ou régions. configuration de prise en charge minimale Hello pour ce est trois régions ou centres de données. Hello le nombre recommandé de régions ou des centres de données est de cinq. Cette configuration nécessite une topologie de cluster plus complexe. Toutefois, hello avantage de ce modèle est que la défaillance d’un centre de données ou de région est convertie d’urgence en une défaillance normale. Ces échecs peuvent être gérées par les mécanismes de hello qui fonctionnent pour les clusters dans une seule région. Les domaines d’erreur, les domaines de mise à niveau et les règles de sélection élective de Service Fabric garantissent que les charges de travail sont distribuées de manière à survivre aux défaillances normales. Pour plus d’informations sur les stratégies qui peuvent aider à utiliser les services dans ce type de cluster, lisez cet article sur les [stratégies de sélection élective](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md).

### <a name="random-failures-leading-toocluster-failures"></a>Défaillances aléatoires toocluster échecs de début
Service Fabric a concept hello des nœuds de valeur initiale. Il s’agit des nœuds permettant de maintenir la disponibilité de hello cluster sous-jacent de hello. Ces nœuds aident tooensure hello cluster reste en établissant des baux avec d’autres nœuds et servant de conflits lors de certains types de défaillances du réseau. Si des défaillances aléatoires supprimer une majorité des nœuds de valeur initiale de hello dans un cluster de hello et ils ne sont pas ramenées, cluster de hello s’arrête automatiquement. Dans Azure, les nœuds de la valeur de départ sont automatiquement gérées : elles sont distribuées sur hello disponible domaines d’erreur et mise à niveau, et si un nœud de valeur initiale unique est supprimé du cluster de hello un autre sera créé à la place. 

Dans les clusters Service Fabric autonomes et Azure, hello « Type de nœud principal » est hello qui exécute les semences hello. Lorsque vous définissez un type de nœud principal, Service Fabric automatiquement tirera parti du nombre de hello de nœuds fournis en créant des nœuds de valeur initiale too9 9 réplicas de chacun des services de système de hello. Si un ensemble de défaillances aléatoires prend simultanément à une majorité de ces réplicas de service système, les services système hello passe une perte de quorum, comme décrit ci-dessus. Si une majorité des nœuds de valeur initiale de hello est perdue, cluster de hello arrêtera peu après.

## <a name="next-steps"></a>Étapes suivantes
- Découvrez comment toosimulate diverses défaillances à l’aide de hello [framework de testabilité](service-fabric-testability-overview.md)
- Consultez les autres ressources de récupération d’urgence et de haute disponibilité. Microsoft a publié de nombreuses rubriques d’aide sur ces sujets. Alors que certains de ces documents font référence toospecific techniques pour une utilisation dans d’autres produits, qu’ils contiennent de nombreux meilleures pratiques générales que vous pouvez appliquer dans le contexte de Service Fabric hello ainsi :
  - [Liste de contrôle de disponibilité](../best-practices-availability-checklist.md)
  - [Exécution d’un exercice de récupération d’urgence](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Récupération d’urgence et haute disponibilité pour les applications Azure][dr-ha-guide]
- En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
