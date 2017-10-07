---
title: maintenance de conservation de machine virtuelle AAA pour les machines virtuelles Windows dans Azure | Documents Microsoft
description: "Migration sur place de machines virtuelles pour la préservation des mises à jour en mémoire."
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: b798f0afd9d8dc60ca8a78f7cc77435a0ddc76fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a>Maintenance de préservation pour les machines virtuelles Windows dans Azure

Majorité hello des mises à jour ont aucun toohosted impact sur les machines virtuelles, il existe lorsque toocomponents de mises à jour ou de services conduisent interférence minimale toorunning machines virtuelles (sans redémarrage complet de l’ordinateur virtuel de hello).

Ces mises à jour sont réalisées avec une technologie qui permet la migration dynamique sur place, également appelée « mise à jour avec préservation de la mémoire ». Lors de la mise à jour d’hôte de hello, ordinateur virtuel de hello est placé dans un état « suspendu », en conservant mémoire hello dans la mémoire RAM, tandis que hello hébergeant l’environnement (par exemple, le système d’exploitation sous-jacent) applique les correctifs et mises à jour nécessaires de hello.
Hello ordinateur virtuel est ensuite redémarré dans les 30 secondes en pause.
Après la reprise, l’horloge de l’ordinateur virtuel de hello hello est automatiquement synchronisé.

Pas toutes les mises à jour peuvent être déployés à l’aide de ce mécanisme, mais le délai court instant, déploiement des mises à jour de cette façon considérablement réduit les ordinateurs toovirtual impact.

Les mises à jour multi-instances (machines virtuelles d’un groupe à haute disponibilité) se voient appliquer un seul domaine de mise à jour à la fois.

Certaines applications peuvent être affectées plus que d’autres par ces mises à jour. Les applications qui effectuent le traitement des événements en temps réel, diffusion multimédia en continu ou le transcodage ou un débit élevé, les scénarios de mise en réseau, par exemple, peut-être pas tootolerate conçu une pause deuxième 30. Applications qui s’exécutent sur une machine virtuelle peuvent en savoir plus sur les mises à jour à venir en appelant hello [événements planifiés](../virtual-machines-scheduled-events.md) API Hello [Service de métadonnées Azure](../virtual-machines-instancemetadataservice-overview.md).
