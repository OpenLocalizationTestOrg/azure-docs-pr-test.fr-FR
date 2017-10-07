---
title: aaaAzure conteneur Instances conteneur de groupes
description: "Découvrez comment fonctionnent les groupes de conteneurs dans Azure Container Instances"
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
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Groupes de conteneurs dans Azure Container Instances

ressources de niveau supérieur Hello dans les Instances du conteneur Azure est un groupe conteneur. Cet article décrit les groupes de conteneurs et les types de scénarios associés.

## <a name="how-a-container-group-works"></a>Fonctionnement d’un groupe de conteneurs

Un conteneur de groupe est une collection de conteneurs obtient planifiées sur hello héberger l’ordinateur et partager un cycle de vie, du réseau local et les volumes de stockage. Il est même concept toohello d’un *pod* dans [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) et [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).

Hello diagramme suivant montre un exemple d’un groupe conteneur qui inclut plusieurs conteneurs.

![Exemple de groupe de conteneurs][container-groups-example]

Notez les points suivants :

- groupe de Hello est planifiée sur un ordinateur hôte unique.
- groupe de Hello expose une adresse IP publique unique, avec un seul port exposé.
- groupe de Hello est constitué de deux conteneurs. Un conteneur est à l’écoute sur le port 80, tandis que hello autres écoute le port 5000.
- groupe de Hello inclut deux partages de fichiers Azure en tant que de montage de volume, et chaque conteneur monte un des partages hello localement.

### <a name="networking"></a>Mise en réseau

Les groupes du conteneur partagent une adresse IP et un espace de noms de port sur cette adresse IP. tooreach de clients externes tooenable un conteneur au sein du groupe de hello, vous devez exposer le port hello sur l’adresse IP de hello et à partir du conteneur de hello. Étant donné que les conteneurs au sein du groupe de hello partagent un espace de noms de port, mappage de port n’est pas pris en charge. Conteneurs au sein d’un groupe peuvent atteindre l’autre via localhost sur hello ports dont ils ont exposés, même si ces ports ne sont pas exposés en externe sur l’adresse IP du groupe hello.

### <a name="storage"></a>Storage

Vous pouvez spécifier toomount volumes externes dans un groupe conteneur. Vous pouvez mapper ces volumes dans les chemins d’accès spécifiques dans des conteneurs individuels hello dans un groupe.

## <a name="common-scenarios"></a>Scénarios courants

Groupes du conteneur multiples sont utiles dans les cas où vous voulez toodivide une seule tâche fonctionnel dans un petit nombre d’images de conteneur, qui peuvent être fournis par différentes équipes et d’avoir des exigences de ressources distinct. Exemples d’utilisation :

- Un conteneur d’applications et un conteneur de journalisation. conteneur de journalisation Hello collecte des journaux de hello et de sortie de métriques par principale de l’application hello et les écrit toolong-terme.
- Une application et un conteneur de surveillance. Hello surveillant conteneur régulièrement rend un tooensure d’application demande toohello qu’il est en cours d’exécution et répond correctement et déclenche une alerte si elle n’est pas.
- Un conteneur servant d’une application web et un conteneur d’extraction de contenu le plus récent à partir du contrôle de code source hello.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[déployer un groupe conteneur multi](container-instances-multi-container-group.md) avec un modèle Azure Resource Manager.

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png