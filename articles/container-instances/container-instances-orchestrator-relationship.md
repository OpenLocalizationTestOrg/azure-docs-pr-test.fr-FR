---
title: "les Instances de conteneurs aaaAzure et l’Orchestration de conteneur"
description: "En savoir plus sur l’interaction entre Azure Container Instances et les orchestrateurs de conteneurs"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Azure Container Instances et les orchestrateurs de conteneurs

En raison de leur taille réduite et de leur orientation d’application, les conteneurs conviennent parfaitement aux environnements de distribution agiles et aux architectures basées sur les microservices. tâche Hello d’automatiser et de gérer un grand nombre de conteneurs et la façon dont ils interagissent est appelé *orchestration*. Orchestrators de conteneur populaires incluent Kubernetes, contrôleur de domaine/système d’exploitation et Docker Swarm, qui sont disponibles dans hello [Service de conteneur Azure](https://docs.microsoft.com/azure/container-service/).

Les Instances du conteneur Azure fournit des hello base planification des capacités de plateformes d’orchestration, mais il ne couvre pas les services de plus grande valeur hello que ces plateformes fournissent et peuvent en fait être complémentaires avec eux. Cet article décrit l’étendue de hello de ce que les Instances du conteneur Azure gère et le taux de remplissage orchestrators de conteneur peuvent interagir avec lui.

## <a name="traditional-orchestration"></a>Orchestration traditionnelle

définition de la norme Hello d’orchestration inclut hello tâches suivantes :

- **Planification**: étant donné une image de conteneur et une demande de ressource, ordinateur approprié sur le conteneur de hello toorun est introuvable.
- **Affinité/Anti-affinité** : spécifier qu’un ensemble de conteneurs doivent s’exécuter à proximité les uns des autres (à des fins de performances) ou suffisamment éloignés les uns des autres (à des fins de disponibilité).
- **Contrôle d’intégrité** : détecter les échecs de conteneur et les replanifier automatiquement.
- **Basculement**: effectuer le suivi de ce qui s’exécute sur chaque ordinateur et de replanification des conteneurs à partir des nœuds de toohealthy machines ayant échoué.
- **Mise à l’échelle**: ajouter ou supprimer la demande de conteneur instances toomatch, manuellement ou automatiquement.
- **Mise en réseau**: fournir une surcouche réseau pour la coordination des conteneurs toocommunicate sur plusieurs ordinateurs hôtes.
- **Détection du service**: activer des conteneurs toolocate eux automatiquement même si elles déplacement entre des ordinateurs hôtes et modifier les adresses IP.
- **Coordination des mises à niveau de l’application**: gestion d’application de tooavoid de mises à niveau conteneur temps d’arrêt et permettre la restauration si une erreur survient.

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>Orchestration avec Azure Container Instances : une approche en couches

Les Instances du conteneur Azure permet une approche en couches tooorchestration, fournissant tous les hello planification et fonctionnalités de gestion requis toorun un seul conteneur, tout en autorisant des tâches de conteneur de plusieurs plateformes toomanage par-dessus orchestrator.

Étant donné que tous les hello sous-jacent d’infrastructure pour les Instances du conteneur est géré par Azure, une plate-forme orchestrator n’a pas besoin tooconcern lui-même sur la recherche d’un ordinateur hôte approprié sur le toorun un seul conteneur. élasticité Hello du cloud de hello garantit que l’une est toujours disponible. Au lieu de cela, orchestrator de hello peut se concentrer sur les tâches de hello qui simplifient le développement hello de conteneur plusieurs architectures, notamment la mise à l’échelle et de coordonner les mises à niveau.



## <a name="potential-scenarios"></a>Scénarios potentiels

Bien que l’intégration d’orchestrateur avec Azure Container Instances en soit encore à sa phase initiale, nous prévoyons l’émergence de plusieurs environnements différents :

### <a name="orchestration-of-container-instances-exclusively"></a>Orchestration exclusive de Container Instances

Deuxième car elles démarrent rapidement et de facturation par hello, un environnement basé uniquement sur les Instances du conteneur Azure offre tooget de manière plus rapide hello démarré et toodeal avec des charges de travail très variables.

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>Combinaison de Container Instances et de conteneurs sur des machines virtuelles

Pour la durée d’exécution longue stables les charges de travail, en orchestrant des conteneurs dans un cluster de machines virtuelles dédiées seront généralement moins chers que l’exécution des mêmes conteneurs hello avec des Instances de conteneur. Toutefois, les Instances de conteneurs offrent une excellente solution pour développer rapidement et de contraction votre toodeal capacité globale avec inattendue ou de courte durée de vie des pics d’utilisation. Au lieu de la montée en puissance parallèle de nombre hello d’ordinateurs virtuels dans votre cluster, puis déployer des conteneurs supplémentaires sur ces ordinateurs, hello orchestrator peut simplement planifier hello autres conteneurs à l’aide d’Instances de conteneurs et les supprimer lorsqu’elles sont aucun plus nécessaire.

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>Exemple d’implémentation : connecteur Azure Container Instances pour Kubernetes

toodemonstrate comment intégrer les plates-formes d’orchestration conteneur avec les Instances du conteneur Azure, nous avons démarré construction un [exemple de connecteur pour Kubernetes][aci-connector-k8s]. 

Hello connecteur pour Kubernetes imite hello [kubelet] [ kubelet-doc] par l’inscription en tant que nœud avec une capacité illimitée et la distribution de la création de hello de [POD] [ pod-doc] en tant que groupes du conteneur dans les Instances du conteneur Azure. 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

Connecteurs pour les autres orchestrators peut être créés de la même façon intégré à la puissance plateforme primitives toocombine hello orchestrator de hello API avec une fréquence de hello et simplicité de gestion des conteneurs dans les Instances du conteneur Azure.

> [!WARNING]
> Hello connecteur ACI pour Kubernetes est *expérimentale* et ne doit pas être utilisé en production.

## <a name="next-steps"></a>Étapes suivantes

Créer votre premier conteneur avec des Instances de conteneur Azure à l’aide de hello [guide de démarrage rapide](container-instances-quickstart.md).

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/