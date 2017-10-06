---
title: "aaaAzure Premium et Standard Overview de disques gérés | Documents Microsoft"
description: "Vue d’ensemble de disques de géré Azure, qui gère les comptes de stockage hello pour vous lors de l’utilisation de machines virtuelles Azure"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 70d45226e531b43f2142f2798bdaf40f77f057f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-disks-overview"></a>Vue d’ensemble d’Azure Managed Disks

Des disques gérés Azure simplifie la gestion des disques pour les machines virtuelles Azure IaaS en gérant hello [comptes de stockage](storage-introduction.md) associées aux disques de machine virtuelle hello. Vous avez uniquement de type hello de toospecify ([Premium](storage-premium-storage.md) ou [Standard](storage-standard-storage.md)) et la taille de hello du disque que vous avez besoin et Azure crée et gère les disques de hello pour vous.

## <a name="benefits-of-managed-disks"></a>Avantages des disques managés

Jetons un œil sur quelques-uns des avantages hello obtenir à l’aide de disques gérés, en commençant par cette vidéo de Channel 9, [une meilleure résilience de machine virtuelle Azure avec disques gérés](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>Déploiement de machines virtuelles simple et évolutif

Coulisses de hello, gérée gère le stockage des disques pour vous. Auparavant, vous aviez toocreate stockage comptes toohold hello des disques (fichiers VHD) pour vos machines virtuelles Azure. Lors de la montée en puissance, vous aviez toomake que vous avez créé des comptes de stockage supplémentaires pour que vous n’avez pas dépassent la limite d’IOPS hello pour le stockage avec un de vos disques. Avec la gestion du stockage des disques gérés, vous n’êtes n’est plus limité par les limites de compte de stockage hello (tels que 20 000 IOPS / compte). Vous avez également n’est plus toocopy vos comptes de stockage toomultiple des images personnalisées (fichiers VHD). Vous pouvez les gérer dans un emplacement central, un compte de stockage par région Azure et les utiliser toocreate des centaines d’ordinateurs virtuels dans un abonnement.

Disques gérés vous permettra de toocreate des too10, 000 ordinateurs virtuels **disques** dans un abonnement, ce qui active vous toocreate des milliers de **machines virtuelles** dans un seul abonnement. Également cette fonctionnalité augmente l’évolutivité de hello de [jeux de mise à l’échelle de Machine virtuelle (mise)](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) en vous toocreate des machines virtuelles de tooa mille dans une mise à l’aide d’une image de Marketplace.

### <a name="better-reliability-for-availability-sets"></a>Fiabilité supérieure des groupes à haute disponibilité

Disques gérés fournit une meilleure fiabilité pour la haute disponibilité, en veillant à ce que hello disques de [machines virtuelles dans un ensemble de disponibilité](../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) sont suffisamment isolés les uns des autres tooavoid points de défaillance uniques. Cela en plaçant automatiquement les disques de hello dans les unités d’échelle de stockage différents (horodatages). Si un horodatage échoue en raison de l’erreur toohardware ou logicielle, seules les instances de machine virtuelle hello avec des disques sur ces marqueurs échouent. Par exemple, supposons que vous avez une application en cours d’exécution sur cinq machines virtuelles et les machines virtuelles de hello sont dans un groupe à haute disponibilité. Hello disques pour ces machines virtuelles ne sont pas toutes être stockées dans hello même horodatage, par conséquent, si un tampon tombe en panne, hello autres instances de l’application hello continuent toorun.

### <a name="highly-durable-and-available"></a>Disponibilité et durabilité élevées

Les disques Azure sont conçus pour offrir une disponibilité de 99,999 %. Vous pouvez travailler en toute quiétude en sachant que vous disposez de trois réplicas de vos données, ce qui offre plus de durabilité. Si un ou même de deux réplicas de rencontrer des problèmes, les réplicas hello restants permettent de garantir la persistance de vos données et une tolérance élevée contre les défaillances. Cette architecture a permis à Azure de fournir de façon cohérente une durabilité de classe Entreprise pour les disques IaaS, avec un taux de défaillance annuel inégalé dans le secteur de zéro %. 

### <a name="granular-access-control"></a>Contrôle d’accès granulaire

Vous pouvez utiliser [du contrôle d’accès (RBAC)](../active-directory/role-based-access-control-what-is.md) tooassign des autorisations spécifiques pour un tooone disque géré ou de plusieurs utilisateurs. Gérés disques expose un ensemble d’opérations, y compris en lecture, écriture (créer/mettre à jour), delete et la récupération un [signature d’accès partagé (SAS) URI](storage-dotnet-shared-access-signature-part-1.md) pour le disque de hello. Vous pouvez accorder des accès tooonly hello opérations qu'une personne doit tooperform son travail. Par exemple, si vous ne souhaitez pas un toocopy personne un compte de stockage de disque géré tooa, vous pouvez choisir pas toogrant accès toohello action d’exportation pour ce disque géré. De même, si vous ne souhaitez pas un toouse personne un toocopy URI SAS un disque géré, vous pouvez choisir toogrant pas cette autorisation toohello disque géré.

### <a name="azure-backup-service-support"></a>Prise en charge du service Sauvegarde Azure
Utiliser le service Azure Backup avec disques gérés toocreate un travail de sauvegarde avec les sauvegardes basées sur le temps, restauration facile de machine virtuelle et les stratégies de rétention de sauvegarde. Disques gérés prennent uniquement en charge le stockage localement redondant (LRS) en tant qu’option de réplication hello ; Cela signifie qu’il conserve trois copies des données de salutation au sein d’une seule région. Pour la récupération après sinistre régionale, vous devez sauvegarder vos disques de machines virtuelles dans une autre région à l’aide du [service Azure Backup](../backup/backup-introduction-to-azure-backup.md) et d’un compte de stockage GRS comme archivage de sauvegarde. Actuellement Azure Backup prend en charge les tailles de disque de données des too1TB pour la sauvegarde. Pour en savoir plus sur ce point, consultez [Utilisation du service Sauvegarde Azure pour les machines virtuelles avec Managed Disks](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="pricing-and-billing"></a>Tarification et facturation

Lors de l’utilisation de disques gérés, hello suivant des considérations relatives à la facturation s’appliquent :
* Type de stockage

* Taille du disque

* Nombre de transactions

* Transferts de données sortantes

* Captures instantanées des disques managés (copie intégrale du disque)

Examinons ces éléments de plus près.

**Type de stockage :** Managed Disks propose 2 niveaux de performance : [Premium](storage-premium-storage.md) (disques SSD) et [Standard](storage-standard-storage.md) (disque dur). facturation Hello d’un disque géré varie selon le type de stockage que vous avez sélectionné pour le disque de hello.


**Taille du disque**: facturation de disques gérés dépend de la taille de hello mis en service de disque de hello. Mappages Azure hello toohello taille approvisionnée (arrondi) plus proche de l’option de disques gérés comme spécifié dans les tables hello ci-dessous. Chaque tooone de mappages de disque géré de hello approvisionnés formats pris en charge et est facturée en conséquence. Par exemple, si vous créez un disque géré standard et que vous spécifiez une taille approvisionnée de 200 Go, vous êtes facturé conformément à la tarification de hello type S20 disque hello.

Voici les tailles de disque hello disponible pour un disque géré premium :

| **Disques managés<br> Premium** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Taille du disque        | 32 Go   | 64 Go   | 128 Go  | 512 Go  | 1024 Go (1 To) | 2 048 Go (2 To) | 4 095 Go (4 To) | 


Voici les tailles de disque hello disponible pour un disque géré standard :

| **Disques managés<br> Standard** | **S4** | **S6** | **S10** | **S20** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Taille du disque        | 32 Go   | 64 Go   | 128 Go | 512 Go | 1024 Go (1 To) | 2 048 Go (2 To) | 4 095 Go (4 To) | 


**Nombre de transactions**: vous êtes facturé pour des transactions que vous effectuez sur un disque géré standard hello. Les transactions associées aux disques managés Premium ne sont pas facturées.

**Transferts de données sortantes**: les [transferts de données sortantes](https://azure.microsoft.com/pricing/details/data-transfers/) (données sortant des centres de données Azure) sont facturés en fonction de la bande passante utilisée.

Pour plus d’informations sur la tarification d’Azure Managed Disks, consultez la page [Managed Disks Tarification](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Captures instantanées de disque managé

Une capture instantanée est une copie en lecture seule d’un disque géré qui est stockée comme un disque géré standard par défaut. Avec des captures instantanées, vous pouvez sauvegarder vos disques managés à tout moment dans le temps. Ces instantanés existent indépendamment du disque source de hello et peuvent être utilisé toocreate nouveaux disques gérés. Ils sont facturés en fonction de la taille de hello utilisé. Par exemple, si vous créez un instantané d’un disque géré avec une capacité déployée de 64 Go et la taille des données utilisées de 10 Go, instantané sera facturé uniquement pour la taille des données hello utilisée de 10 Go.  

[Instantanés incrémentiels](storage-incremental-snapshots.md) ne sont actuellement pas pris en charge pour les disques gérés, mais il le sera dans hello futures.

toolearn savoir plus sur comment instantanés toocreate avec des disques gérés, consultez ces ressources :

* [Créer une copie d’un disque dur virtuel stocké en tant que disque géré à l’aide de la fonction Instantanés dans Windows](../virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Créer une copie d’un disque dur virtuel stocké en tant que disque géré à l’aide de la fonction Instantanés dans Linux](../virtual-machines/linux/snapshot-copy-managed-disk.md)


## <a name="images"></a>Images

Managed Disks prend également en charge la création d’une image personnalisée gérée. Vous pouvez créer une image à partir de votre disque dur virtuel (VHD) personnalisé dans un compte de stockage ou directement à partir d’une machine virtuelle généralisée (préparée à l’aide de Sysprep). Capture d’une image unique tous gérés disques associés à une machine virtuelle, y compris les hello du système d’exploitation et des disques de données. Ce permet la création des centaines d’ordinateurs virtuels à l’aide de votre image personnalisée sans hello devez toocopy ou gérer des comptes de stockage.

Pour plus d’informations sur la création d’images, consultez hello suivant des articles :
* [Comment toocapture une image managée d’une machine virtuelle généralisée dans Azure](../virtual-machines/windows/capture-image-resource.md)
* [Comment toogeneralize et une machine virtuelle Linux à l’aide de la capture hello Azure CLI 2.0](../virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Images et captures instantanées

Vous consultez souvent le mot hello « image » utilisée avec des machines virtuelles, et vous voyez à présent « instantanés » ainsi. Il s’agit de différence de hello toounderstand important entre celles-ci. Managed Disks vous permet de saisir une image d’une machine virtuelle généralisée qui a été libérée. Cette image inclut tous les disques attachés de hello toohello machine virtuelle. Vous pouvez utiliser cette image de toocreate un nouvel ordinateur virtuel, et il inclut tous les disques de hello.

Un instantané est une copie d’un disque à hello point dans le temps, qu'elle est récupérée. Il s’applique uniquement tooone disque. Si vous avez une machine virtuelle qui comporte uniquement un seul disque (hello du système d’exploitation), vous pouvez prendre un instantané ou une image et créer une machine virtuelle à partir de la capture instantanée de hello ou d’image de hello.

Que se passe-t-il une machine virtuelle comprend cinq disques agrégés par bande ? Vous pouvez prendre un instantané de chacun des disques de hello, mais ne reconnaît pas dans hello VM d’état hello de disques hello – les instantanés hello savoir uniquement sur un seul disque. Dans ce cas, les instantanés hello devez toobe coordonnée entre eux et qui est actuellement pas en charge.

## <a name="managed-disks-and-encryption"></a>Disques gérés et chiffrement

Il existe deux types de toodiscuss de chiffrement des disques toomanaged de référence. Hello tout d’abord une est stockage Service de chiffrement (SSE), qui est effectuée par le service de stockage hello. Hello seconde est chiffrement de disque Azure, que vous pouvez activer sur hello du système d’exploitation et des disques de données pour vos machines virtuelles.

### <a name="storage-service-encryption-sse"></a>Storage Service Encryption (SSE)

[Chiffrement du Service Azure Storage](storage-service-encryption.md) fournit le chiffrement au repos et protéger votre toomeet données votre organisation engagements de conformité et de sécurité. SSE est activée par défaut pour tous les disques gérés, les instantanés et les Images dans toutes les régions hello où disques gérés est disponible. En commençant au 10 juin 2017, tous les nouveaux disques/instantanés/images et managés écrites tooexisting géré disques de nouvelles données sont automatiquement chiffrées au repos dotées de clés gérés par Microsoft.  Visitez hello [page de FAQ de disques gérés](storage-faq-for-disks.md#managed-disks-and-storage-service-encryption) pour plus d’informations.


### <a name="azure-disk-encryption-ade"></a>Azure Disk Encryption (ADE)

Le chiffrement des disques Azure vous permet de tooencrypt hello du système d’exploitation et des disques de données utilisées par une Machine virtuelle de IaaS. Cela inclut les disques gérés. Pour Windows, les lecteurs de hello sont chiffrés à l’aide de la technologie de chiffrement BitLocker standard. Pour Linux, les disques de hello sont chiffrées à l’aide de la technologie de hello DM-Crypt. Il est intégré à Azure Key Vault tooallow vous toocontrol et gérer des clés de chiffrement de disque hello. Pour plus d’informations, voir [Azure Disk Encryption pour machines virtuelles Windows et Linux IaaS](../security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les disques gérés, reportez-vous à toohello suivant des articles.

### <a name="get-started-with-managed-disks"></a>Bien démarrer avec Managed Disks

* [Créer une machine virtuelle à l’aide de Resource Manager et de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Créer une VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md)

* [Attacher un tooa de disque de données managées machine virtuelle Windows à l’aide de PowerShell](../virtual-machines/windows/attach-disk-ps.md)

* [Ajouter un tooa disque géré Linux VM](../virtual-machines/linux/add-disk.md)

* [Disques managés - Exemples de scripts PowerShell](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Utiliser des disques gérés dans les modèles Azure Resource Manager](storage-using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Comparer les options de stockage Managed Disks

* [Stockage Premium et disques](storage-premium-storage.md)

* [Stockage Standard et disques](storage-standard-storage.md)

### <a name="operational-guidance"></a>Instructions d’utilisation

* [Migrer à partir de AWS et d’autres plateformes tooManaged des disques dans Azure](../virtual-machines/windows/on-prem-to-azure.md)

* [Convertir les disques toomanaged de machines virtuelles Azure dans Azure](../virtual-machines/windows/migrate-to-managed-disks.md)
