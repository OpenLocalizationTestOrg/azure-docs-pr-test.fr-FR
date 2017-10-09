---
title: aaaCreate Azure Service Fabric clusters sur Windows Server et Linux | Documents Microsoft
description: "Clusters service Fabric s’exécutés sur Windows Server et Linux, ce qui signifie que vous devront être en mesure de toodeploy et hôte Service Fabric des applications n’importe où vous pouvez exécuter Windows Server ou Linux."
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Créer des clusters Service Fabric sur un système Windows Server ou Linux
Un cluster Azure Service Fabric est un groupe de machines virtuelles ou physiques connectées au réseau, dans lequel vos microservices sont déployés et gérés. Une machine ou machine virtuelle faisant partie d’un cluster est appelée un nœud de cluster. Clusters peuvent évoluer toothousands de nœuds. Si vous ajoutez le nouveau cluster toohello de nœuds, Service Fabric rééquilibre les réplicas de partition de service hello et les instances sur nombre hello augmentée de nœuds. Améliorent les performances de l’application global et réduit les conflits d’accès toomemory. Si les nœuds hello dans un cluster de hello ne sont pas utilisés efficacement, vous pouvez réduire le nombre de hello de nœuds de cluster de hello. Service Fabric rééquilibrage à nouveau les réplicas de partition hello et instances dans le nombre de hello diminué de nœuds toomake améliorer l’utilisation du matériel hello sur chaque nœud.

L’infrastructure de service permet de créer de hello de clusters Service Fabric sur des machines virtuelles ou des ordinateurs exécutant Windows Server ou Linux. Cela signifie que vous sont en mesure de toodeploy et exécutez des applications de Service Fabric dans n’importe quel environnement où vous avez un ensemble d’ordinateurs Windows Server ou Linux qui sont interconnectés, soit en local, Microsoft Azure ou avec n’importe quel fournisseur de cloud.

## <a name="create-service-fabric-clusters-on-azure"></a>Créer des clusters Service Fabric sur Azure
Création d’un cluster dans Azure s’effectue via une ressource de modèle ou la hello portail Azure. Lecture [créer un cluster Service Fabric à l’aide d’un modèle de gestionnaire de ressources](service-fabric-cluster-creation-via-arm.md) ou [créer un cluster Service Fabric hello portail Azure](service-fabric-cluster-creation-via-portal.md) pour plus d’informations.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Systèmes d’exploitation pris en charge pour les clusters dans Azure
Vous êtes en mesure de toocreate des clusters sur des machines virtuelles exécutant ces systèmes d’exploitation :

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04 (en version préliminaire publique) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Créer des clusters Service Fabric autonomes locaux ou avec n’importe quel fournisseur cloud
L’infrastructure de service fournit un package d’installation pour vous toocreate autonome Service Fabric clusters sur site ou sur n’importe quel fournisseur de cloud

Pour en savoir plus sur la configuration de clusters Service Fabric autonomes sur Windows Server, voir [Création d’un cluster Service Fabric pour Windows Server](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Déploiements cloud ou en local
processus de Hello pour la création d’un cluster Service Fabric local est processus toohello similaire de création d’un cluster d’un cloud de votre choix avec un ensemble de machines virtuelles. Hello étapes initiales tooprovision hello machines virtuelles sont régies par fournisseur de cloud hello ou un environnement local que vous utilisez. Une fois que vous avez un ensemble d’ordinateurs virtuels avec connectivité réseau activée entre eux, puis hello tooset étapes package de Service Fabric hello, modifier les paramètres de cluster hello et exécuter la création du cluster hello et des scripts de gestion sont identiques. Cela garantit que vos connaissances et l’expérience d’exploitation et la gestion des clusters Service Fabric est transférable lorsque vous choisissez tootarget nouveaux environnements d’hébergement.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Avantages de la création de clusters Service Fabric autonomes
* Vous êtes libre toochoose un cloud toohost du fournisseur de votre cluster.
* Applications de service Fabric, une fois écrites, peuvent être exécutées dans plusieurs environnements d’hébergement avec des modifications toono minimale.
* Base de connaissances de la création d’applications de Service Fabric reprend à partir d’un hébergement tooanother d’environnement.
* Expérience d’en cours d’exécution et la gestion de l’infrastructure de Service de clusters transporte sur à partir d’un environnement tooanother.
* Ciblage étendu en termes de clientèle sans contrainte d’environnement d’hébergement.
* Il existe une couche supplémentaire de fiabilité et de la protection contre les pannes, car vous pouvez déplacer des services de hello sur l’environnement de déploiement tooanother si un centre de données ou le fournisseur de cloud a une indisponibilité.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Systèmes d’exploitation pris en charge pour les clusters autonomes
Vous êtes en mesure de toocreate des clusters sur des machines virtuelles ou des ordinateurs qui exécutent ces systèmes d’exploitation :

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (prochainement)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Avantages des clusters Service Fabric sur Azure par rapport aux clusters Service Fabric créés en local
Clusters Service Fabric en cours d’exécution sur Azure offre des avantages sur l’option hello localement, donc si vous n’avez pas besoins spécifiques pour sur lequel vous exécutez vos clusters, puis nous suggérons de les exécuter sur Azure. Sur Azure, nous offrent une intégration avec d’autres fonctionnalités d’Azure et les services, ce qui rend les opérations et la gestion du cluster de hello plus facile et plus fiable.

* **Portail Azure :** portail Azure rend facile toocreate et gérer des clusters.
* **Azure Resource Manager :** utilisation du Gestionnaire de ressources Azure permet une gestion plus simple de toutes les ressources utilisées par le cluster de hello en tant qu’unité et simplifie le suivi des coûts et la facturation.
* **Cluster Service Fabric en tant que ressource Azure :** un cluster Service Fabric est une ressource ARM, que vous pouvez modeler comme d’autres ressources ARM dans Azure.
* **Intégration avec l’Infrastructure Azure** Service Fabric en coordination avec hello sous-jacent d’infrastructure Azure pour le système d’exploitation, réseau et autres mises à niveau tooimprove disponibilité et la fiabilité de vos applications.  
* **Diagnostics :** dans Azure, nous proposons l’intégration d’Azure Diagnostics et de Log Analytics.
* **Montée en puissance automatique :** pour les clusters sur Azure, nous fournir des fonctionnalités intégrées de la mise à l’échelle automatique en raison de tooVirtual machines identiques. Dans les locaux et les autres environnements de cloud computing, vous avez toobuild votre propre fonctionnalité de mise à l’échelle ou d’échelle manuellement à l’aide de hello API qui expose de l’infrastructure de Service de mise à l’échelle de clusters.

## <a name="next-steps"></a>Étapes suivantes

* Créer un cluster sur des machines virtuelles ou des ordinateurs exécutant Windows Server : [Création d’un cluster Service Fabric pour Windows Server](service-fabric-cluster-creation-for-windows-server.md)
* Créer un cluster sur des machines virtuelles ou des ordinateurs exécutant Linux : [Service Fabric sur Linux](service-fabric-linux-overview.md)
* En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)

