---
title: aaaIntroducing hello Gestionnaire de ressources du Cluster Service Fabric | Documents Microsoft
description: "Une présentation toohello Gestionnaire de ressources du Cluster Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>Présentation du Gestionnaire de ressources de cluster Service Fabric hello
En règle générale la gestion des systèmes informatiques ou des services en ligne destinée consacrer des ordinateurs physiques ou virtuels toothose spécifiques des services spécifiques ou des systèmes. Les services étaient conçus sous forme de niveaux : un niveau « web » et un niveau « données » ou « stockage ». Applications aurait une couche de messagerie où les demandes passées et l’extraction, ainsi qu’un ensemble de machines des toocaching dédié. Chaque couche ou un type de charge de travail avait tooit dédié des ordinateurs spécifiques : base de données hello obtenu deux ordinateurs dédiés tooit, les serveurs web hello quelques exemples. Si un type particulier de la charge de travail due machines hello sur toorun trop à chaud, puis vous avez ajouté des ordinateurs plus avec ce même niveau de toothat de configuration. Toutefois, pas toutes les charges de travail peuvent être monté en charge facilement : en particulier avec la couche de données hello, vous devez remplacer généralement les ordinateurs avec les machines plus grandes. Facile. Si un ordinateur a échoué, cette partie de hello global d’application s’est exécutée à une capacité inférieure jusqu'à ce que l’ordinateur de hello peut être restauré. Toujours aussi facile (mais pas forcément très amusant).

Désormais, cependant hello world du service et architecture logicielle a changé. Les applications adoptent souvent une conception de montée en puissance. Il est courant de créer des applications avec des conteneurs ou des microservices (voire les deux). Même si vous ne disposez toujours que de quelques machines, elles n’exécutent pas une seule instance d’une charge de travail. Ils peuvent même être en cours d’exécution plusieurs différentes charges de travail à hello même temps. Vous avez désormais des dizaines de types de services différents (aucun consommant des ressources équivalentes à une machine complète), voire des centaines d’instances différentes de ces services. Chaque instance nommée possède un(e) ou plusieurs instances ou réplicas pour la haute disponibilité (HA). En fonction de ces charges de travail et le niveau d’activité sont les tailles hello, vous souhaiterez peut-être vous-même avec des centaines, voire des milliers d’ordinateurs. 

Soudainement gérez votre environnement n’est pas aussi simple que la gestion des types de toosingle dédié quelques machines des charges de travail. Vos serveurs virtuels et ne sont plus ont des noms (vous êtes passé d’états d’esprit [toocattle d’animaux domestiques](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) une fois toutes les). La configuration est inférieure sur les ordinateurs hello et plus d’informations sur les services hello eux-mêmes. Matériel dédié tooa une seule instance d’une charge de travail est en grande partie une chose Hello passées. Les services sont eux-mêmes devenus de petits systèmes distribués qui couvrent de nombreux plus petits éléments de machines de grande série.

Étant donné que votre application n’est plus une série de monolithes réparties sur plusieurs niveaux, vous avez maintenant toodeal de combinaisons plus nombreuses avec. Qui détermine les types ou le nombre de charges de travail pouvant être exécutées sur du matériel spécifique ? Des charges de travail fonctionnent sur hello même matériel et qui sont en conflit ? Lorsqu’une machine tombe en passe, comment savoir ce qui était en cours d’exécution sur cette machine ? Qui doit veiller à ce que la charge de travail redevienne opérationnelle ? Si vous attendez pour la sauvegarde de toocome hello ordinateur (virtuel) ? ou vos charges de travail automatiquement basculer tooother machines et poursuivre l’exécution ? Une intervention humaine est-elle nécessaire ? Qu’en est-il des mises à niveau dans cet environnement ?

En tant que les développeurs et les opérateurs dans cet environnement, nous allons aide toowant gérer cette complexité. A binge d’embauche et la tentative de complexité de hello toohide avec des personnes ne sont probablement pas réponse hello, ainsi que nous faire ?

## <a name="introducing-orchestrators"></a>Présentation des orchestrators
« Orchestrateur » est hello terme général qui désigne un élément logiciel qui permet aux administrateurs de gérer ces types d’environnements. Orchestrators sont des composants hello prennent dans les demandes comme « Je souhaite que les cinq copies de ce service en cours d’exécution dans mon environnement ». Ils tentent toomake hello correspondance hello souhaité état de l’environnement, tous les cas.

Les Orchestrators (qui ne sont pas des humains) passent à l’action quand une machine tombe en panne ou quand une charge de travail se termine pour une raison inattendue. La plupart des Orchestrators ne se contentent pas de gérer l’échec. La gestion de nouveaux déploiements, des mises à niveau, de la consommation de ressources et de la gouvernance sont quelques-unes de leurs autres fonctions. Tous les orchestrators sont essentiellement sur la maintenance d’un état souhaité de configuration dans l’environnement de hello. Vous souhaitez tootell en mesure de toobe orchestrateur ce que vous souhaitez et hello essentiel. Aurora sur Mesos, Fleet, Docker Datacenter/Docker Swarm, Kubernetes et Service Fabric sont des exemples d’Orchestrators. Ces orchestrators sont en cours de besoins de hello toomeet activement développé des charges de travail réelles dans les environnements de production. 

## <a name="orchestration-as-a-service"></a>Orchestration en tant que service
Hello, Gestionnaire de ressources du Cluster est composant du système hello qui gère l’orchestration dans l’infrastructure de Service. les travaux du Gestionnaire de ressources Cluster Hello sont divisée en trois parties :

1. Application des règles
2. Optimisation de l’environnement
3. Aide des autres processus

toosee comment hello Gestionnaire de ressources du Cluster fonctionne, regardez hello suivant vidéo de Microsoft Virtual Academy :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>Ce qu’il n’est pas
Les applications de couche N traditionnelles comportent toujours d’un [équilibreur de charge](https://en.wikipedia.org/wiki/Load_balancing_(computing)). Généralement, c’était un équilibrage de charge réseau (NLB) ou un équilibrage de charge Application (ALB) selon où il sat dans la pile réseau hello. Il existe des équilibreurs de charge matériels, comme la gamme BigIP de F5, et d’autres logiciels, comme l’équilibreur de charge réseau Microsoft. Dans d’autres environnements, vous verrez un élément similaire à HAProxy, nginx, Istio ou Envoy dans ce rôle. Dans ces architectures, tâche hello d’équilibrage de charge est tooensure de charges de travail sans état de réception (à peu près) hello même quantité de travail. Les stratégies d’équilibrage de charge étaient variées. Certains programmes d’équilibrage envoie chaque appel différent tooa autre serveur. D’autres fournissaient l’épinglage/l’adhérence de session. Les équilibreurs plus avancés utilisent estimation de la charge réelle ou tooroute création de rapports, un appel en fonction de son coût prévu charge machine actuelle.

Équilibreurs de réseau ou tooensure routeurs a tenté de message qui hello niveau web/worker est restée à peu près équilibrée. Stratégies d’équilibrage de la couche de données hello étaient différents et dépendant sur un mécanisme de stockage de données hello. L’équilibrage de la couche de données hello reposait sur le partitionnement des données, la mise en cache managés vues, procédures stockées et autres mécanismes spécifiques au magasin.

Alors que certains de ces stratégies sont intéressantes, hello Gestionnaire de ressources du Cluster Service Fabric n’est pas quoi que ce soit comme un équilibrage de charge réseau ou d’un cache. Un équilibreur de charge réseau équilibre les serveurs frontaux en répartissant leur trafic. Hello, Gestionnaire de ressources du Cluster Service Fabric a une autre stratégie. Fondamentalement, le Service Fabric déplace *services* toowhere celles-ci permettent de hello mieux attendu du trafic ou charger toofollow. Par exemple, elle peut déplacer toonodes de services qui sont actuellement à froid, car les services de hello existe-t-il ne font pas de quantité de travail. les nœuds Hello peuvent être à froid, car les services hello qui étaient présentes ont été supprimés ou déplacés ailleurs. Autre exemple, hello Gestionnaire de ressources du Cluster peut également déplacer un service en dehors d’un ordinateur. Par exemple hello ordinateur concerne toobe mis à niveau ou est surchargé en raison de pic tooa la consommation par les services de hello en cours d’exécution sur ce dernier. Alernatively, besoins en ressources du service hello a augmenté. Par conséquent il ne contient pas suffisamment de ressources cette toocontinue ordinateur exécutant. 

Hello, Gestionnaire de ressources du Cluster étant responsable du déplacement des services autour, il contient un toowhat par rapport de fonctionnalités disponibles dans un équilibreur de charge réseau. Il s’agit, car les équilibreurs de charge réseau remettre toowhere de trafic réseau services sont déjà, même si cet emplacement n’est pas idéal pour l’exécution de service hello lui-même. Hello, Gestionnaire de ressources du Cluster Service Fabric utilise fondamentalement différentes stratégies afin de garantir que les ressources hello dans un cluster de hello sont utilisées efficacement.

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur le flux architecture et les informations de hello dans hello Gestionnaire de ressources de Cluster, consultez [cet article](service-fabric-cluster-resource-manager-architecture.md)
- Hello, Gestionnaire de ressources du Cluster possède de nombreuses options permettant de décrire le cluster de hello. toofind plus d’informations sur les métriques, consultez cet article sur [décrivant un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- Pour plus d’informations sur la configuration des services, consultez la rubrique [En savoir plus sur la configuration des services](service-fabric-cluster-resource-manager-configure-services.md) (service-fabric-cluster-resource-manager-configure-services.md).
- Les métriques sont comment hello Gestionnaire de ressources du Cluster Service Fabric gère la consommation et la capacité en cluster de hello. toolearn plus d’informations sur les métriques et comment tooconfigure les extraire [cet article](service-fabric-cluster-resource-manager-metrics.md)
- Hello Gestionnaire de ressources du Cluster fonctionne avec les fonctionnalités de gestion de Service Fabric. toofind plus d’informations sur cette intégration, lire [cet article](service-fabric-cluster-resource-manager-management-integration.md)
- toofind out sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, consultez l’article de hello sur [équilibrage de charge](service-fabric-cluster-resource-manager-balancing.md)
