---
title: "paramètres de métriques et la sélection élective aaaSpecify dans Azure microservices | Documents Microsoft"
description: "Description d’un service Service Fabric en spécifiant des mesures, des contraintes de positionnement et d’autres stratégies de positionnement."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Configuration des paramètres Cluster Resource Manager pour les services Service Fabric
Hello, Gestionnaire de ressources du Cluster Service Fabric permet un contrôle affiné sur les règles hello qui régissent chaque personne désignée de service. Chaque service nommé peut spécifier des règles de la façon dont il doit être allouée dans le cluster de hello. Chaque service nommé peut également définir hello métriques qu’elles souhaitent tooreport, y compris la façon dont ils sont importants toothat service. La configuration des services se décompose en trois tâches :

1. Configuration des contraintes de positionnement
2. Configuration des mesures
3. Configuration des stratégies et des autres règles de positionnement avancées (moins fréquent)

## <a name="placement-constraints"></a>Contraintes de placement
Contraintes de placement sont toocontrol utilisé les nœuds de cluster de hello un service peut s’exécuter sur. Généralement, un particulier nommé l’instance de service ou de tous les services d’un toorun de la contrainte de type donné sur un type de nœud particulier. Les contraintes de placement sont extensibles. Vous pouvez définir n’importe quel jeu de propriétés par type de nœud, puis les sélectionner avec des contraintes lors de la création de services. Vous pouvez également modifier les contraintes de placement d’un service en cours d’exécution. Cela vous permet de toochanges toorespond dans le cluster de hello ou exigences hello du service de hello. propriétés Hello d’un nœud donné peuvent également être mis à jour dynamiquement dans le cluster de hello. Plus d’informations sur les contraintes de placement et comment tooconfigure les trouverez dans [cet article](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Mesures
Métriques sont ensemble hello de ressources qui a besoin d’un service nommé donné. La configuration de mesures d’un service détermine notamment la quantité d’une ressource que chaque réplica avec état ou instance sans état de ce service consomme par défaut. Mesures comprennent également une pondération qui indique l’importance cette métrique d’équilibrage toothat service, en cas de compromis sont nécessaires.

## <a name="advanced-placement-rules"></a>Règles de placement avancées
Il existe d’autres types de règles de placement qui sont utiles dans des scénarios moins courants. Voici quelques exemples :
- Contraintes utiles avec des clusters dispersés géographiquement
- Certaines architectures d’application

La configuration des autres règles de positionnement s’effectue via Corrélations ou Stratégies.

## <a name="next-steps"></a>Étapes suivantes
- Les métriques sont comment hello Gestionnaire de ressources du Cluster Service Fabric gère la consommation et la capacité en cluster de hello. toolearn plus d’informations sur les métriques et comment tooconfigure, extraire [cet article](service-fabric-cluster-resource-manager-metrics.md)
- L’affinité est un mode que vous pouvez configurer pour vos services. Ce n’est pas courant, mais si nécessaire, vous trouverez plus d’informations [ici](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Il existe de règles de positionnement différents qui peuvent être configurées sur votre service toohandle supplémentaires des scénarios. Vous trouverez plus d’informations sur ces différentes stratégies de positionnement [ici](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Démarrer à partir du début de hello et [obtenir une présentation de toohello Gestionnaire de ressources du Cluster Service Fabric](service-fabric-cluster-resource-manager-introduction.md)
- toofind out sur comment hello Gestionnaire de ressources de Cluster gère et équilibre la charge du cluster de hello, consultez l’article de hello sur [équilibrage de charge](service-fabric-cluster-resource-manager-balancing.md)
- Hello, Gestionnaire de ressources du Cluster possède de nombreuses options permettant de décrire le cluster de hello. toofind plus d’informations à leur sujet, consultez cet article sur [décrivant un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
