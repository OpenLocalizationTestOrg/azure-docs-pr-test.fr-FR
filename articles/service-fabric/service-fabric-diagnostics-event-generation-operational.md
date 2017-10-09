---
title: "aaaAzure Service Fabric opérationnel canal | Documents Microsoft"
description: "Liste complète des fichiers journaux générés dans des clusters de canal opérationnel d’Azure Service Fabric hello."
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
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>Canal opérationnel 

canal opérationnel de Hello se compose des journaux à partir des principales actions effectuées par l’infrastructure de Service sur vos nœuds et que votre cluster. Lorsque « Diagnostics » est activé pour un cluster, hello agent de Diagnostics Windows Azure est déployé sur votre cluster et est par défaut configuré les tooread dans les journaux à partir du canal opérationnel de hello. En savoir plus sur la configuration de hello [agent de Diagnostics Azure](service-fabric-diagnostics-event-aggregation-wad.md) configuration des diagnostics hello toomodify de votre toopick cluster plusieurs journaux ou les compteurs de performance. 

## <a name="operational-channel-logs"></a>Journaux du canal opérationnel 

Voici une liste complète des journaux fournie par l’infrastructure de Service dans le canal opérationnel de hello. 

| EventId | Nom | Source (tâche) | Niveau |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | Informations |
| 25621 | NodeOpenedSuccess | FabricNode | Informations |
| 25622 | NodeOpenedFailed | FabricNode | Informations |
| 25623 | NodeClosing | FabricNode | Informations |
| 25624 | NodeClosed | FabricNode | Informations |
| 25625 | NodeAborting | FabricNode | Informations |
| 25626 | NodeAborted | FabricNode | Informations |
| 29627 | ClusterUpgradeStart | CM | Informations |
| 29628 | ClusterUpgradeComplete | CM | Informations |
| 29629 | ClusterUpgradeRollback | CM | Informations |
| 29630 | ClusterUpgradeRollbackComplete | CM | Informations |
| 29631 | ClusterUpgradeDomainComplete | CM | Informations |
| 23074 | ContainerActivated | Hébergement | Informations |
| 23075 | ContainerDeactivated | Hébergement | Informations |
| 29620 | ApplicationCreated | CM | Informations |
| 29621 | ApplicationUpgradeStart | CM | Informations |
| 29622 | ApplicationUpgradeComplete | CM | Informations |
| 29623 | ApplicationUpgradeRollback | CM | Informations |
| 29624 | ApplicationUpgradeRollbackComplete | CM | Informations |
| 29625 | ApplicationDeleted | CM | Informations |
| 29626 | ApplicationUpgradeDomainComplete | CM | Informations |
| 18566 | ServiceCreated | FM | Informations |
| 18567 | ServiceDeleted | FM | Informations |

## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur global [génération des événements au niveau de plate-forme hello](service-fabric-diagnostics-event-generation-infra.md) dans Service Fabric
* Modification de votre [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) configuration toocollect consigne plus
* [Configuration d’Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) toosee journaux de votre canal opérationnel
