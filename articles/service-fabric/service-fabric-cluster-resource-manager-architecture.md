---
title: "Architecture du Gestionnaire d’aaaResource | Documents Microsoft"
description: "Vue d’ensemble de l’architecture du Gestionnaire de ressources Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>Vue d’ensemble de l’architecture Cluster Resource Manager
Hello, Gestionnaire de ressources du Cluster Service Fabric est un service central qui s’exécute dans un cluster de hello. Il gère l’état de hello souhaité de services hello cluster hello, en particulier avec respect tooresource consommation et toutes les règles de sélection élective. 

ressources de hello toomanage dans votre cluster, hello Gestionnaire de ressources du Cluster Service Fabric doit avoir plusieurs éléments d’information :

- La liste des services existants
- La consommation de ressources actuelle (ou par défaut) de chaque service 
- capacité de cluster restants Hello 
- capacité de Hello de nœuds hello dans un cluster de hello 
- quantité de Hello de ressources consommées sur chaque nœud

la consommation des ressources d’un service donné Hello permettre changer au fil du temps, et les services intéressent généralement plus d’un type de ressource. Dans différents services, il peut s’agir de ressources physiques réelles et de ressources physiques mesurées. Les services peuvent assurer le suivi des mesures physiques comme la consommation de mémoire et de disque. En général, les services peuvent se soucier des mesures logiques, comme « WorkQueueDepth » ou « TotalRequests ». Métriques de logique et physique peut être utilisé dans hello même cluster. Métriques peuvent être partagés entre plusieurs services ou service particulier de tooa spécifique.

## <a name="other-considerations"></a>Autres points à considérer
Hello propriétaires et les opérateurs du cluster de hello peuvent être différents de hello auteurs d’applications et des services ou à un minimum sont hello mêmes personnes port chapeaux différents. Lorsque vous développez votre application, vous avez quelques informations sur les éléments qu’elle nécessite. Vous avez une estimation de hello il consomme des ressources et comment les différents services doivent être déployés. Par exemple, la couche web de hello doit toorun sur les nœuds exposées toohello Internet, alors que les services de base de données hello ne doivent pas. Autre exemple, les services web hello sont probablement contraint par processeur et le réseau, tandis que les soins de services de niveau de données hello en savoir plus sur la consommation de mémoire et de disque. Toutefois, personne hello gérer un incident de site dynamique pour ce service en production ou qui gère un service de mise à niveau toohello a un toodo de travail différent et nécessite des différents outils. 

Cluster de hello et services sont dynamiques :

- nombre de Hello de nœuds de cluster de hello peut augmenter ou diminuer
- Des nœuds présentant des tailles et types différents vont et viennent.
- Des services peuvent être créés ou supprimés, et peuvent modifier leur allocation de ressources ainsi que les règles de placement.
- Mises à niveau ou autres opérations de gestion peuvent restaurer par cluster hello au niveau de l’application hello sur les niveaux de l’infrastructure
- Des échecs peuvent se produire à tout moment.

## <a name="cluster-resource-manager-components-and-data-flow"></a>Composants et flux de données Cluster Resource Manager
Hello, Gestionnaire de ressources du Cluster exige tootrack hello de chaque service et hello la consommation des ressources par chaque objet de service au sein de ces services. Hello, Gestionnaire de ressources du Cluster a deux concepts : les agents qui s’exécutent sur chaque nœud et un service à tolérance de pannes. agents Hello sur chaque nœud de suivi de charge signale à partir des services, d’agrégation et les signaler périodiquement. Hello service Gestionnaire de ressources de Cluster agrège toutes les informations hello des agents de local hello et réagit en fonction de sa configuration actuelle.

Examinons hello suivant schéma :

<center>
![Architecture de l’équilibreur de ressources][Image1]
</center>

Pendant l’exécution, de nombreux changements peuvent se produire. Supposons par exemple, le montant de hello ressources certains services consomment des modifications, certains services échouent, et certains nœuds joint et quitter hello cluster. Toutes les modifications de hello sur un nœud sont agrégées et régulièrement envoyées toohello Gestionnaire de ressources du Cluster service (1,2) où elles sont agrégées à nouveau, analysées et stockées. Après quelques secondes que service examine les modifications hello et détermine si toutes les actions sont nécessaires (3). Par exemple, il peut remarquer que certains nœuds vides ont été ajoutées toohello cluster. Par conséquent, il décide toomove certains nœuds toothose de services. Hello Gestionnaire de ressources du Cluster peut également remarquer qu’un nœud particulier est surchargé, ou que certains services ont a échoué ou est supprimé, la libération de ressources ailleurs.

Nous allons examiner hello suivant schéma et consultez les étapes suivantes. Supposons que ce gestionnaire de ressources du Cluster hello détermine que des modifications sont nécessaires. Il coordonne avec d’autres modifications système services (Gestionnaire de basculement de hello particulier) toomake hello nécessaires. Ensuite, les commandes nécessaires hello sont envoyés toohello des nœuds (4). Par exemple, supposons hello Gestionnaire de ressources remarqué que Node5 a été surchargé et par conséquent décidé Node5 tooNode4 toomove service B. Extrémité hello de reconfiguration de hello (5), le cluster de hello ressemble à ceci :

<center>
![Architecture de l’équilibreur de ressources][Image2]
</center>

## <a name="next-steps"></a>Étapes suivantes
- Hello, Gestionnaire de ressources du Cluster possède de nombreuses options permettant de décrire le cluster de hello. toofind plus d’informations à leur sujet, consultez cet article sur [décrivant un cluster Service Fabric](./service-fabric-cluster-resource-manager-cluster-description.md)
- droits de principal du Gestionnaire de ressources Cluster Hello sont rééquilibrage de cluster de hello et en appliquant des règles de sélection élective. Pour plus d’informations sur la configuration de ces comportements, consultez [Équilibrage de votre cluster Service Fabric](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
