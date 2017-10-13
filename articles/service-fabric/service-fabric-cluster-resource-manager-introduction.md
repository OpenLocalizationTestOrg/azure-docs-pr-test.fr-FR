---
title: "Présentation de Service Fabric Cluster Resource Manager | Microsoft Docs"
description: "Présentation de Service Fabric Cluster Resource Manager."
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
ms.openlocfilehash: fd8d4eea239646a5d42955756e4f57742bb5ee4f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="introducing-the-service-fabric-cluster-resource-manager"></a>Présentation de Service Fabric Cluster Resource Manager
Jusqu’ici, pour gérer des systèmes informatiques ou des services en ligne, il fallait dédier des machines physiques ou virtuelles spécifiques à ces services ou systèmes spécifiques. Les services étaient conçus sous forme de niveaux : un niveau « web » et un niveau « données » ou « stockage ». Les applications comportaient un niveau de messagerie où les demandes étaient transmises ou reçues, ainsi qu’un ensemble de machines dédiées à la mise en cache. Chaque niveau ou type de charge de travail recevait des machines spécifiques dédiées : quelques machines pour la base de données, quelques-unes pour les serveurs web. Si un type particulier de charge de travail entraînait la surchauffe des machines sur lesquelles il était exécuté, alors vous ajoutiez davantage de machines avec cette même configuration à ce niveau. Toutefois, il n’était pas possible d’augmenter facilement toutes les charges de travail. Avec le niveau de données en particulier, vous deviez généralement remplacer les machines par des machines plus grandes. Facile. Si une machine venait à tomber en panne, cette partie de l’application globale s’exécutait alors à une capacité inférieure jusqu’à la restauration de la machine. Toujours aussi facile (mais pas forcément très amusant).

Mais le monde de l’architecture des services et des logiciels a changé. Les applications adoptent souvent une conception de montée en puissance. Il est courant de créer des applications avec des conteneurs ou des microservices (voire les deux). Même si vous ne disposez toujours que de quelques machines, elles n’exécutent pas une seule instance d’une charge de travail. Elles peuvent même exécuter différentes charges de travail à la fois. Vous avez désormais des dizaines de types de services différents (aucun consommant des ressources équivalentes à une machine complète), voire des centaines d’instances différentes de ces services. Chaque instance nommée possède un(e) ou plusieurs instances ou réplicas pour la haute disponibilité (HA). Selon la taille et l’utilisation de ces charges de travail, vous risquez de vous retrouver avec des centaines voire des milliers de machines. 

Tout à coup, la gestion de votre environnement se complique et ne se résume plus à quelques machines dédiées à des types de charges de travail uniques. Vos serveurs sont virtuels et n’ont plus de noms (vous êtes passé des [animaux domestiques (« pets ») au bétail (« cattle »)](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20) , voilà tout). La configuration est désormais axée davantage sur les services que sur les machines. Le matériel dédié à une seule instance d’une charge de travail fait partie du passé. Les services sont eux-mêmes devenus de petits systèmes distribués qui couvrent de nombreux plus petits éléments de machines de grande série.

Étant donné que votre application n’est plus une série de monolithes répartis sur plusieurs niveaux, vous avez maintenant beaucoup plus de combinaisons à gérer. Qui détermine les types ou le nombre de charges de travail pouvant être exécutées sur du matériel spécifique ? Quelles charges de travail fonctionnent bien sur le même matériel, et lesquelles sont en conflit ? Lorsqu’une machine tombe en passe, comment savoir ce qui était en cours d’exécution sur cette machine ? Qui doit veiller à ce que la charge de travail redevienne opérationnelle ? Attendez-vous le retour de la machine (virtuelle ?), ou vos charges de travail basculent-elles automatiquement sur d’autres machines avant de continuer à s’exécuter ? Une intervention humaine est-elle nécessaire ? Qu’en est-il des mises à niveau dans cet environnement ?

En tant que développeurs et opérateurs gérant cet environnement, nous aurons besoin d’aide pour gérer cette complexité. Une stratégie d’embauche massive de personnel dans le seul but de masquer la complexité de la situation n’est probablement pas la bonne solution. Alors que faire ?

## <a name="introducing-orchestrators"></a>Présentation des orchestrators
Un « Orchestrator » est un terme général qui désigne un élément logiciel permettant aux administrateurs de gérer ces types d’environnement. Les Orchestrators sont les composants qui acceptent des requêtes du type « Je souhaiterais exécuter cinq copies de ce service dans mon environnement ». Puis, ils tentent de faire correspondre l’environnement à l’état souhaité, quoi qu’il arrive.

Les Orchestrators (qui ne sont pas des humains) passent à l’action quand une machine tombe en panne ou quand une charge de travail se termine pour une raison inattendue. La plupart des Orchestrators ne se contentent pas de gérer l’échec. La gestion de nouveaux déploiements, des mises à niveau, de la consommation de ressources et de la gouvernance sont quelques-unes de leurs autres fonctions. Tous les Orchestrators se consacrent essentiellement à la maintenance d’un état souhaité de configuration dans l’environnement. Dans l’idéal, vous devez pouvoir dire à un Orchestrator ce que vous souhaitez accomplir et le laisser faire le gros du travail. Aurora sur Mesos, Fleet, Docker Datacenter/Docker Swarm, Kubernetes et Service Fabric sont des exemples d’Orchestrators. Ces Orchestrators sont activement développés pour répondre aux besoins des charges de travail réelles dans des environnements de production. 

## <a name="orchestration-as-a-service"></a>Orchestration en tant que service
Cluster Resource Manager est le composant système qui gère l’orchestration dans Service Fabric. Le travail de Cluster Resource Manager est divisé en trois parties :

1. Application des règles
2. Optimisation de l’environnement
3. Aide des autres processus

Pour découvrir comment fonctionne Cluster Resource Manager, visionnez cette vidéo de la Microsoft Virtual Academy :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>Ce qu’il n’est pas
Les applications de couche N traditionnelles comportent toujours d’un [équilibreur de charge](https://en.wikipedia.org/wiki/Load_balancing_(computing)). Généralement, il s’agissait d’un équilibrage de charge réseau (NLB) ou d’un équilibrage de charge d’application (ALB) suivant son emplacement dans la pile de mise en réseau. Il existe des équilibreurs de charge matériels, comme la gamme BigIP de F5, et d’autres logiciels, comme l’équilibreur de charge réseau Microsoft. Dans d’autres environnements, vous verrez un élément similaire à HAProxy, nginx, Istio ou Envoy dans ce rôle. Dans ces architectures, le travail d’équilibrage de charge consiste à garantir que les charges de travail sans état reçoivent (à peu près) la même quantité de travail. Les stratégies d’équilibrage de charge étaient variées. Certains équilibreurs de charge envoyaient chaque appel distinct vers un serveur différent. D’autres fournissaient l’épinglage/l’adhérence de session. Les équilibreurs de charge les plus avancés utilisent une estimation réelle de la charge ou la création de rapports pour acheminer un appel en fonction de son coût prévu et de la charge de la machine actuelle.

Les équilibreurs de réseau ou les routeurs de messages essayaient de s’assurer que le niveau web/travail restait à peu près équilibré. Les stratégies d’équilibrage de niveau de données étaient différentes et dépendaient du mécanisme de stockage des données. L’équilibrage du niveau de données reposait sur un partitionnement des données, une mise en cache, des vues gérées, des procédures stockées et d’autres mécanismes de stockage spécifiques.

Bien que certaines de ces stratégies présentent un intérêt, Service Fabric Cluster Resource Manager n’a rien à voir avec un équilibreur de charge ou un cache. Un équilibreur de charge réseau équilibre les serveurs frontaux en répartissant leur trafic. Service Fabric Cluster Resource Manager adopte une stratégie différente. Essentiellement, Service Fabric déplace des *services* vers l’emplacement où ils sont les plus significatifs, en attente de trafic ou d’une charge à venir. Par exemple, il peut déplacer des services vers des nœuds qui sont actuellement à froid, car les services qui y sont présents n’effectuent pas beaucoup de travail. Les nœuds peuvent être à froid, car les services qui étaient présents ont été supprimés ou déplacés ailleurs. Autre exemple, Cluster Resource Manager peut également déplacer un service en dehors d’une machine. Peut-être que celle-ci est sur le point d’être mise à niveau ou qu’elle est surchargée en raison d’un pic de consommation par les services qui y sont exécutés. Les besoins en ressources du service peuvent également avoir augmenté. Par conséquent, il n’y a pas suffisamment de ressources sur cette machine pour continuer à l’exécuter. 

Étant donné que Cluster Resource Manager est responsable du déplacement des services, il contient un ensemble de fonctionnalités différentes par rapport à ce que vous trouveriez dans un équilibrage de charge réseau. Les équilibreurs de charge réseau acheminent le trafic réseau à des services déjà présents, même si leur emplacement n’est pas idéal pour l’exécution du service proprement dit. Service Fabric Cluster Resource Manager utilise des stratégies très différentes pour s’assurer que les ressources dans le cluster sont utilisées efficacement.

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur l’architecture et le flux d’informations dans Cluster Resource Manager, consultez [cet article ](service-fabric-cluster-resource-manager-architecture.md)
- Cluster Resource Manager comporte de nombreuses options permettant de décrire le cluster. Pour en savoir plus sur ces mesures, consultez cet article sur la [description d’un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md).
- Pour plus d’informations sur la configuration des services, consultez la rubrique [En savoir plus sur la configuration des services](service-fabric-cluster-resource-manager-configure-services.md) (service-fabric-cluster-resource-manager-configure-services.md).
- Les mesures représentent la façon dont Service Fabric Cluster Resource Manager gère la consommation et la capacité du cluster. Pour en savoir plus sur ces mesures et la façon de les configurer, consultez [cet article](service-fabric-cluster-resource-manager-metrics.md)
- Cluster Resource Manager fonctionne avec les fonctionnalités de gestion de Service Fabric. Pour en savoir plus sur cette intégration, consultez [cet article](service-fabric-cluster-resource-manager-management-integration.md)
- Pour en savoir plus sur la façon dont Cluster Resource Manager gère et équilibre la charge du cluster, consultez l’article sur [l’équilibrage de la charge](service-fabric-cluster-resource-manager-balancing.md)
