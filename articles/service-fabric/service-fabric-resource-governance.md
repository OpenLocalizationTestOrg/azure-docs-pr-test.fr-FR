---
title: aaaAzure Service Fabric la gouvernance de ressources pour les conteneurs et les Services | Documents Microsoft
description: "Azure Service Fabric vous permet de toospecify les limites de ressources pour les services en cours d’exécution interne ou externes conteneurs."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a>Gouvernance des ressources 

Lorsque plusieurs services en cours d’exécution hello même nœud ou un cluster, il est possible qu’un seul service peut consommer davantage de ressources priver les autres services. Ce problème est référencé tooas hello syndrome du voisin. Service Fabric permet les réservations toospecify hello développeur et les limites par service tooguarantee ressources et également limiter son utilisation des ressources. 

## <a name="resource-governance-metrics"></a>Mesures de la gouvernance des ressources 

Dans Service Fabric, la gouvernance des ressources est prise en charge par [package de service](service-fabric-application-model.md). ressources Hello assignés tooService Package peuvent être réparties entre les packages de code. limites des ressources Hello spécifiés implique également la réservation hello des ressources de hello. Service Fabric prend en charge la spécification des ressources processeur et mémoire par package de service à l’aide de deux [mesures](service-fabric-cluster-resource-manager-metrics.md) intégrées :

* Processeur (nom de métrique `ServiceFabric:/_CpuCores`) : un noyau est un cœur logique qui est disponible sur l’ordinateur hôte hello, et tous les cœurs sur tous les nœuds sont pondérées hello identiques.
* Mémoire (nom de métrique `ServiceFabric:/_MemoryInMB`) : mémoire est exprimée en mégaoctets et mappe toophysical mémoire disponible sur l’ordinateur de hello.

Uniquement les garanties de réservation logicielle sont proposés - hello runtime rejette lors de l’ouverture du nouveau service dépassés des ressources disponibles des packages. Toutefois, si un autre fichier exécutable ou un conteneur est placé sur le nœud de hello, qui peut violer les garanties de réservation d’origine hello.

Pour ces deux mesures, hello [Gestionnaire de ressources du Cluster](service-fabric-cluster-resource-manager-cluster-description.md) effectue le suivi de la capacité totale de cluster, charge hello sur chaque nœud de cluster de hello, et, le reste des ressources de cluster de hello. Ces deux mesures est équivalente tooany autre utilisateur ou une métrique personnalisée et toutes les fonctionnalités existantes peuvent être utilisées avec les :
* Cluster peut être [équilibrées](service-fabric-cluster-resource-manager-balancing.md) en fonction des métriques de toothese deux (comportement par défaut).
* Cluster peut être [défragmentés](service-fabric-cluster-resource-manager-defragmentation-metrics.md) en fonction des métriques de toothese deux.
* Lors de la [description d’un cluster](service-fabric-cluster-resource-manager-cluster-description.md), la capacité mise en mémoire tampon peut être définie pour ces deux mesures.

Le [rapport de charge dynamique](service-fabric-cluster-resource-manager-metrics.md) n’est pas pris en charge pour ces mesures et les charges de ces mesures sont définies lors de la création.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Configuration du cluster pour l’activation de la gouvernance des ressources

La capacité doit être définie manuellement dans chaque type de nœud de cluster de hello comme suit :

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
La gouvernance des ressources est autorisée uniquement sur les services de l’utilisateur, et non sur les services système. Lorsque vous spécifiez la capacité, vous devez désallouer certains cœurs et une partie de la mémoire pour les services système. Pour des performances optimales, hello suivant le paramètre doit également être activé dans le manifeste du cluster hello : 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Spécification de la gouvernance des ressources 

Les limites de gouvernance des ressources sont spécifiés dans le manifeste d’application hello (section ServiceManifestImport), comme indiqué dans hello l’exemple suivant :

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
Dans cet exemple, le package de service ServicePackageA Obtient un cœur sur les nœuds hello où il est placé. Ce package de service contient deux packages de code (CodeA1 et CodeA2), et tous deux spécifient hello `CpuShares` paramètre. proportion de Hello de CpuShares 512:256 divise les noyaux hello entre les deux packages de code hello. Par conséquent, dans cet exemple, CodeA1 obtient deux tiers d’un cœur, CodeA2 Obtient un tiers d’un cœur (et une réservation soft-garantie de hello même). Lorsque les CpuShares ne sont pas spécifiés pour les packages de code, Service Fabric divise cœurs hello équitablement entre eux.

Limites de la mémoire étant absolus, les deux packages de code sont limitées too1024 Mo de mémoire (et une réservation soft-garantie de hello même). Packages de code (conteneurs ou processus) ne sont pas en mesure de tooallocate plus de mémoire que cette limite et de tenter de toodo engendre une exception de mémoire insuffisante. Pour toowork de mise en œuvre de limite de ressource, tous les packages de code au sein d’un package de service doivent avoir des limites de mémoire spécifiées.


## <a name="next-steps"></a>Étapes suivantes
* toolearn plus sur Cluster Gestionnaire de ressources, lire ce [article](service-fabric-cluster-resource-manager-introduction.md).
* toolearn en savoir plus sur le modèle d’application, de packages de service, de packages de code et de toothem de correspondances de réplicas de lire ce [article](service-fabric-application-model.md).
