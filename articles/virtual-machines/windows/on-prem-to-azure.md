---
title: "aaaMigrate de AWS et d’autres plateformes tooManaged disques dans Azure | Documents Microsoft"
description: "Créez des machines virtuelles dans Azure à l’aide de disques durs virtuels chargés à partir d’autres clouds comme AWS ou d’autres plateformes de virtualisation, et tirez parti d’Azure Managed Disks."
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
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Migrer à partir d’Amazon Web Services (AWS) et d’autres plateformes tooManaged des disques dans Azure

Vous pouvez télécharger les fichiers VHD AWS ou locaux virtualisation solutions tooAzure toocreate machines virtuelles qui tirent parti de disques gérés. Les disques Azure géré exonère hello toomanaging de comptes de stockage pour les machines virtuelles Azure IaaS. Vous avez tooonly spécifier type hello (Premium ou Standard) et la taille du disque que vous avez besoin, et Azure créent et gèrent les disques de hello pour vous. 

Vous pouvez charger des disques durs virtuels généralisés et spécialisés. 
- **Disque dur virtuel généralisé** : supprime toutes les informations de votre compte personnel avec Sysprep. 
- **Spécialisé de disque dur virtuel** -gère les comptes d’utilisateur hello, des applications et autres données d’état à partir de votre machine virtuelle d’origine. 

> [!IMPORTANT]
> Avant de télécharger tout tooAzure de disque dur virtuel, vous devez suivre [préparer un tooAzure tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| Scénario                                                                                                                         | Documentation                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Vous avez une instance AWS EC2 existant que vous impossible, tels que toomigrate tooAzure des disques gérés                                     | [Déplacer un ordinateur virtuel à partir d’Amazon Web Services (AWS) tooAzure](aws-to-azure.md)                           |
| Vous avez une machine virtuelle à partir d’et autre plateforme de virtualisation que vous aimeriez toouse toouse comme une image de toocreate plusieurs machines virtuelles Azure. | [Télécharger un disque dur virtuel généralisé et son utilisation toocreate un nouvelles machines virtuelles dans Azure](upload-generalized-managed.md) |
| Vous avez une VM personnalisée de façon unique que vous aimeriez toorecreate dans Azure.                                                      | [Télécharger un tooAzure spécialisé de disque dur virtuel et créer une machine virtuelle](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Vue d’ensemble des disques gérés

Azure disques gérés simplifie la gestion des ordinateurs virtuels en supprimant les comptes de stockage toomanage hello nécessaire. Managed Disks bénéficie également d’une meilleure fiabilité des machines virtuelles dans un groupe à haute disponibilité. Elle garantit que les disques hello des différentes machines virtuelles dans un ensemble de disponibilité sera suffisamment isolés à partir de chaque autre point unique tooavoid d’échecs. Il place automatiquement les disques de différentes machines virtuelles dans un ensemble de disponibilité dans différentes unités d’échelle de stockage (horodatages) qui limite l’impact hello de pannes d’unité de montée en puissance du stockage uniques dû en raison d’échecs toohardware et logiciels. Selon vos besoins, vous avez le choix entre deux types d’options de stockage : 
 
- Les [disques gérés Premium](../../storage/common/storage-premium-storage.md) sont des supports de stockage basés sur des disques SSD (Solide State Drive) qui assurent de hautes performances et une faible latence pour les machines virtuelles dont les charges de travail nécessitent de nombreuses E/S. Vous pouvez tirer parti de la vitesse de hello et les performances de ces disques par des disques gérés migration tooPremium.  

- [Standard de disques gérés](../../storage/common/storage-standard-storage.md) utiliser le lecteur de disque dur (HDD) en fonction des supports de stockage et les mieux adaptés pour le développement et de Test et d’autres charges de travail peu fréquentes d’accès qui sont moins sensibles tooperformance variabilité.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planifier la migration de hello de tooManaged disques

Cette section vous aide à toomake hello meilleure décision sur les types de machine virtuelle et le disque.


### <a name="location"></a>Lieu

Choisissez un emplacement où Azure Managed Disks est disponible. Si vous migrez des disques gérés tooPremium, vérifiez également que le stockage Premium est disponible dans la région de hello lorsque vous prévoyez de toomigrate à. Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services) .

### <a name="vm-sizes"></a>Tailles de machine virtuelle

Si vous effectuez une migration tooPremium des disques gérés, vous tooupdate hello taille êtes de hello VM tooPremium taille capable de stockage disponible dans la région de hello où se trouve la machine virtuelle. Passez en revue les tailles de machine virtuelle hello qui sont capables de stockage Premium. spécifications de taille de machine virtuelle Azure Hello sont répertoriées dans [tailles des machines virtuelles](sizes.md).
Passez en revue les caractéristiques de performances hello d’ordinateurs virtuels qui fonctionnent avec un stockage Premium et choisissez hello plus approprié taille de machine virtuelle qui convient le mieux à votre charge de travail. Assurez-vous qu’il y suffisamment de bande passante disponible sur votre trafic de disque de machine virtuelle toodrive hello.

### <a name="disk-sizes"></a>Tailles du disque

**Disques gérés Premium**

Il existe trois types de disques gérés Premium qui peuvent être utilisés avec votre machine virtuelle, chacun d’eux présentant des limites d’E/S par seconde et de débit spécifiques. Prendre en compte ces limites lorsque vous choisissez hello le type de disque Premium pour votre machine virtuelle en fonction des besoins de hello de votre application en termes de capacité, les performances, l’évolutivité, et des pics.

| Type de disque Premium  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| Taille du disque           | 128 Go            | 512 Go            | 1024 Go (1 To)    |
| IOPS par disque       | 500               | 2 300              | 5 000              |
| Débit par disque | 100 Mo par seconde | 150 Mo par seconde | 200 Mo par seconde |

**Disques gérés Standard**

Il existe cinq types de disques gérés Standard qui peuvent être utilisés avec votre machine virtuelle. Chacun d’eux dispose d’une capacité différente, mais ils partagent les mêmes limites d’E/S par seconde et de débit. Choisissez le type hello de disques gérés Standard selon les besoins en capacité hello de votre application.

| Type de disque Standard  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| Taille du disque           | 30 Go            | 64 Go            | 128 Go           | 512 Go           | 1024 Go (1 To)   |
| IOPS par disque       | 500              | 500              | 500              | 500              | 500              |
| Débit par disque | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde |

### <a name="disk-caching-policy"></a>Stratégie de mise en cache du disque 

**Disques gérés Premium**

Par défaut, la mise en cache de stratégie est *en lecture seule* pour tous les hello disques de données Premium, et *en lecture-écriture* hello Premium système d’exploitation attaché toohello machine virtuelle. Ce paramètre de configuration est recommandé tooachieve hello des performances optimales IOs de votre application. Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application.

### <a name="pricing"></a>Tarification

Hello de révision [prix des disques gérés](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Tarification de disques gérés de Premium est identique hello les disques Premium non managé. En revanche, la tarification des disques gérés Standard est différente de celle des disques non gérés Standard.


## <a name="next-steps"></a>Étapes suivantes

- Avant de télécharger tout tooAzure de disque dur virtuel, vous devez suivre [préparer un tooAzure tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
