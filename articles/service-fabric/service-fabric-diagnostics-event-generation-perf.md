---
title: aaaAzure analyse des performances de Service Fabric | Documents Microsoft
description: En savoir plus sur les compteurs de performances pour le suivi et le diagnostic des clusters Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a>Mesures de performances

Métriques doivent être collectées toounderstand hello de performance de votre cluster ainsi que les applications de hello en cours d’exécution qu’il contient. Pour les clusters de l’infrastructure de Service, nous vous recommandons de hello suivant des compteurs de performance de collecte.

## <a name="nodes"></a>Nœuds

Pour les ordinateurs hello dans votre cluster, envisagez de hello suivant toobetter comprendre hello charge sur chaque ordinateur et de rendre le cluster approprié de mise à l’échelle des décisions les compteurs de performance de collecte.

| Catégorie de compteur | Nom de compteur |
| --- | --- |
| PhysicalDisk(per Disk) | Avg. de file d’attente lecture disque |
| PhysicalDisk(per Disk) | Avg. de file d’attente écriture disque |
| PhysicalDisk(per Disk) | Avg. Disk sec/Read |
| PhysicalDisk(per Disk) | Avg. Disk sec/Write |
| PhysicalDisk(per Disk) | Nb d’opérations de lectures de disque/s  |
| PhysicalDisk(per Disk) | Nb d’octets de lecture de disque/s  |
| PhysicalDisk(per Disk) | Nb d’opération d’écriture de disque/s |
| PhysicalDisk(per Disk) | Nb d’octets d’écriture de disque/s |
| Mémoire | Nombre d’octets disponibles |
| PagingFile | % utilisation |
| Processus (total) | % temps processeur |
| Processus (par service) | % temps processeur |
| Processus (par service) | Traitement ID |
| Processus (par service) | Octets privés |
| Processus (par service) | Nombre de threads |
| Processus (par service) | Octets virtuels |
| Processus (par service) | Plage de travail |
| Processus (par service) | Plage de travail - Privée |

## <a name="net-applications-and-services"></a>Applications et services .NET

Collecter hello suivant compteurs si vous déployez un cluster de tooyour services .NET. 

| Catégorie de compteur | Nom de compteur |
| --- | --- |
| .NET CLR Memory (par service) | ID du processus |
| .NET CLR Memory (par service) | Nombre total d’octets dédiés |
| .NET CLR Memory (par service) | Nombre total d’octets réservés |
| .NET CLR Memory (par service) | Nombre d’octets dans tous les tas |
| .NET CLR Memory (par service) | Nombre de collections de génération 0 |
| .NET CLR Memory (par service) | Nombre de collections de génération 1 |
| .NET CLR Memory (par service) | Nombre de collections de génération 2 |
| .NET CLR Memory (par service) | % de temps dans GC |

### <a name="service-fabrics-custom-performance-counters"></a>Compteurs de performances personnalisés de Service Fabric

Service Fabric génère une quantité importante de compteurs de performance personnalisés. Si vous avez hello SDK installé, vous pouvez voir la liste complète de hello sur votre ordinateur Windows dans votre application de l’Analyseur de performances (Démarrer > Analyseur de performances). 

Dans les applications de hello vous déployez tooyour cluster, si vous utilisez Reliable Actors, ajoutez des countes de `Service Fabric Actor` et `Service Fabric Actor Method` catégories (consultez [Service Fabric fiable acteurs Diagnostics](service-fabric-reliable-actors-diagnostics.md)).

Si vous utilisez Reliable Services, nous disposons également de catégories `Service Fabric Service` et `Service Fabric Service Method` desquelles vous devez collecter des compteurs. 

Si vous utilisez des Collections fiable, nous vous recommandons d’ajouter hello `Avg. Transaction ms/Commit` de hello `Service Fabric Transactional Replicator` toocollect la latence moyenne de validation hello par mesure de la transaction.


## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur [génération des événements au niveau de plate-forme hello](service-fabric-diagnostics-event-generation-infra.md) dans Service Fabric
* Collecter des mesures de performances via [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)
