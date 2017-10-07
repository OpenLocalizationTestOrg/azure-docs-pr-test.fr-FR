---
title: aaaMigrate disques de machines virtuelles Azure tooManaged | Documents Microsoft
description: "Migrer des machines virtuelles créées à l’aide de disques non managés dans toouse de comptes de stockage des disques gérés."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Migrer des machines virtuelles Azure tooManaged des disques dans Azure

Des disques gérés Azure simplifie la gestion du stockage en supprimant la nécessité de hello tooseparately gérer les comptes de stockage.  Vous pouvez également migrer votre toobenefit de disques tooManaged machines virtuelles Azure existante à partir d’une meilleure fiabilité des machines virtuelles sur un ensemble de disponibilité. Elle garantit que les disques hello des différentes machines virtuelles dans un ensemble de disponibilité sera suffisamment isolés à partir de chaque autre point unique tooavoid d’échecs. Il place automatiquement les disques de différentes machines virtuelles dans un ensemble de disponibilité dans différentes unités d’échelle de stockage (horodatages) qui limite l’impact hello de pannes d’unité de montée en puissance du stockage uniques dû en raison d’échecs toohardware et logiciels.
Selon vos besoins, vous avez le choix entre deux types d’options de stockage :

- Les [disques gérés Premium](../../storage/common/storage-premium-storage.md) sont des supports basés sur des disques SSD (Solide State Drive) qui assurent de hautes performances et une faible latence pour les machines virtuelles dont les charges de travail nécessitent de nombreuses E/S. Vous pouvez tirer parti de la vitesse de hello et les performances de ces disques par des disques gérés migration tooPremium.

- [Standard de disques gérés](../../storage/common/storage-standard-storage.md) utiliser le lecteur de disque dur (HDD) en fonction des supports de stockage et les mieux adaptés pour le développement et de Test et d’autres charges de travail peu fréquentes d’accès qui sont moins sensibles tooperformance variabilité.

Vous pouvez migrer des disques tooManaged dans les scénarios suivants :

| Migrer...                                            | Lien vers la documentation                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Convertir des machines virtuelles de manière autonome et les machines virtuelles dans un jeu de disponibilité toomanaged des disques   | [Convertir les disques de machines virtuelles toouse géré](convert-unmanaged-to-managed-disks.md) |
| Une seule machine virtuelle à partir de tooResource classique Manager sur des disques gérés     | [Migrer une machine virtuelle unique](migrate-single-classic-to-resource-manager.md)  | 
| Tous les ordinateurs virtuels de hello dans un réseau virtuel à partir de tooResource classique Manager sur des disques gérés     | [Migrer les ressources IaaS classique tooResource Manager](migration-classic-resource-manager-ps.md) , puis [convertir un ordinateur virtuel à partir de disques toomanaged de disques non managé](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Planifier pour la conversion de hello tooManaged disques

Cette section vous aide à toomake hello meilleure décision sur les types de machine virtuelle et le disque.


## <a name="location"></a>Lieu

Choisissez un emplacement où Azure Managed Disks est disponible. Si vous déplacez des disques gérés tooPremium, vérifiez également que le stockage Premium est disponible dans la région de hello lorsque vous prévoyez de toomove à. Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services) .

## <a name="vm-sizes"></a>Tailles de machine virtuelle

Si vous effectuez une migration tooPremium des disques gérés, vous tooupdate hello taille êtes de hello VM tooPremium taille capable de stockage disponible dans la région de hello où se trouve la machine virtuelle. Passez en revue les tailles de machine virtuelle hello qui sont capables de stockage Premium. spécifications de taille de machine virtuelle Azure Hello sont répertoriées dans [tailles des machines virtuelles](sizes.md).
Passez en revue les caractéristiques de performances hello d’ordinateurs virtuels qui fonctionnent avec un stockage Premium et choisissez hello plus approprié taille de machine virtuelle qui convient le mieux à votre charge de travail. Assurez-vous qu’il y suffisamment de bande passante disponible sur votre trafic de disque de machine virtuelle toodrive hello.

## <a name="disk-sizes"></a>Tailles du disque

**Disques gérés Premium**

Il existe sept types de disques gérés Premium qui peuvent être utilisés avec votre machine virtuelle, chacun d’eux présentant des limites d’E/S par seconde et de débit spécifiques. Prenez en compte ces limites lorsque vous choisissez hello le type de disque Premium pour votre machine virtuelle en fonction des besoins de hello de votre application en termes de capacité, les performances, l’évolutivité, et des pics.

| Type de disque Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Taille du disque           | 128 Go| 512 Go| 128 Go| 512 Go            | 1024 Go (1 To)    | 2 048 Go (2 To)    | 4 095 Go (4 To)    | 
| IOPS par disque       | 120   | 240   | 500   | 2 300              | 5 000              | 7500              | 7500              | 
| Débit par disque | 25 Mo par seconde  | 50 Mo par seconde  | 100 Mo par seconde | 150 Mo par seconde | 200 Mo par seconde | 250 Mo par seconde | 250 Mo par seconde |

**Disques gérés Standard**

Il existe sept types de disques gérés Standard qui peuvent être utilisés avec votre machine virtuelle. Chacun d’eux dispose d’une capacité différente, mais ils partagent les mêmes limites d’E/S par seconde et de débit. Choisissez le type hello de disques gérés Standard selon les besoins en capacité hello de votre application.

| Type de disque Standard  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Taille du disque           | 30 Go            | 64 Go            | 128 Go           | 512 Go           | 1024 Go (1 To)   | 2 048 Go (2 To)    | 4 095 Go (4 To)   | 
| IOPS par disque       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Débit par disque | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 

## <a name="disk-caching-policy"></a>Stratégie de mise en cache du disque

**Disques gérés Premium**

Par défaut, la mise en cache de stratégie est *en lecture seule* pour tous les hello disques de données Premium, et *en lecture-écriture* hello Premium système d’exploitation attaché toohello machine virtuelle. Ce paramètre de configuration est recommandé tooachieve hello des performances optimales IOs de votre application. Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application.

## <a name="pricing"></a>Tarification

Hello de révision [prix des disques gérés](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Tarification de disques gérés de Premium est identique hello les disques Premium non managé. En revanche, la tarification des disques gérés Standard est différente de celle des disques non gérés Standard.



## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur les [disques gérés](managed-disks-overview.md)
