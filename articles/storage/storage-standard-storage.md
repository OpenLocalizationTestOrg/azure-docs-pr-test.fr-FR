---
title: "en fonction d’aaaHD économique Standard de stockage et les disques de machine virtuelle Azure | Documents Microsoft"
description: "Présentation du stockage Standard économique et des disques de machine virtuelle gérés et non gérés."
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c454c61254c6b160bdf2cd39ea3319452e3e4898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>Stockage Standard économique et disques de machine virtuelle Azure gérés et non gérés

Le stockage Standard Azure permet une prise en charge fiable et économique des disques des machines virtuelles exécutant des charges de travail non sensibles aux latences. Il prend également en charge les objets blob, les tables, les files d’attente et les fichiers. Avec le stockage Standard, les données de hello sont stockées sur des lecteurs de disque dur (HDD). Lorsque vous utilisez des machines virtuelles, vous pouvez utiliser des disques de stockage Standard pour les scénarios de développement/test et les charges de travail les moins critiques, et des disques de stockage Premium pour les applications de production critiques. Le stockage Standard est disponible dans toutes les régions Azure. 

Cet article se concentrera sur l’utilisation de hello de stockage standard pour les disques de machine virtuelle. Pour plus d’informations sur l’utilisation de hello du stockage avec les objets BLOB, les tables, les files d’attente et les fichiers, reportez-vous à toohello [Introduction tooStorage](storage-introduction.md).

## <a name="disk-types"></a>Types de disque

Il existe deux façons de toocreate de disques standard pour les machines virtuelles Azure :

**Non managée disques**: il s’agit de méthode d’origine hello où vous gérez hello stockage comptes utilisés toostore hello fichiers VHD qui correspondent toohello les disques de machine virtuelle. Les fichiers VHD sont stockés en tant qu’objets blob de pages dans les comptes de stockage. Disques non managés peuvent être jointe tooany taille de machine virtuelle Azure, y compris les machines virtuelles hello qui utilisent principalement le stockage Premium, par exemple hello DSv2 et GS series. Machines virtuelles Azure prend en charge attacher plusieurs disques standards, autorisant jusqu'à to too256 de stockage par machine virtuelle.

[**Les disques Azure géré**](storage-managed-disks-overview.md): cette fonctionnalité gère les comptes de stockage hello utilisés pour les disques de machine virtuelle hello pour vous. Vous spécifiez le type hello (Premium ou Standard) et la taille du disque que vous avez besoin et Azure crée et gère les disques de hello pour vous. Vous n’avez pas tooworry à placer les disques de hello sur plusieurs comptes de stockage dans l’ordre tooensure que vous restez dans les limites d’extensibilité hello pour les comptes de stockage hello--Azure qui gère pour vous.

Même si les deux types de disques sont disponibles, nous recommandons l’utilisation parti de tootake de disques gérés de leurs nombreuses fonctionnalités.

tooget main du stockage Standard de Azure, visitez [commencez gratuitement](https://azure.microsoft.com/pricing/free-trial/). 

Pour plus d’informations sur comment toocreate une machine virtuelle avec des disques gérés, consultez un des hello suivant articles.

* [Créer une machine virtuelle à l’aide de Resource Manager et de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)
* [Créer une VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md)

## <a name="standard-storage-features"></a>Fonctionnalités du stockage Standard 

Examinons quelques-unes des fonctionnalités de hello de stockage Standard. Pour plus d’informations, consultez [Introduction tooAzure stockage](storage-introduction.md).

**Stockage Standard** : le stockage Standard Azure prend en charge les disques Azure, les blobs Azure, le stockage de fichiers Azure, les tables Azure et les files d’attente Azure. services de stockage Standard toouse, commencer par [créer un compte Azure Storage](storage-create-storage-account.md#create-a-storage-account).

**Les disques de stockage standard :** stockage Standard, les disques peuvent être attachés tooall machines virtuelles d’Azure, y compris des machines virtuelles de taille de la série utilisées avec un stockage Premium comme série de DSv2 et GS hello. Un disque de stockage standard peut uniquement être attachée tooone machine virtuelle. Toutefois, vous pouvez attacher un ou plusieurs de ces tooa disques machine virtuelle, de nombre maximal de disques de toohello défini pour cette taille de machine virtuelle. Bonjour suivant la section sur l’extensibilité du stockage Standard et les objectifs de performances, nous allons examiner les spécifications hello plus en détail. 

**Objet blob de pages standard**: objets BLOB de pages Standard sont utilisée toohold disques persistants pour les machines virtuelles et également possible d’accéder directement à l’aide de REST comme d’autres types d’objets BLOB Azure. Les [objets blob de pages](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) sont une collection de pages de 512 octets optimisées pour les opérations de lecture et d’écriture aléatoires. 

**Réplication du stockage :** dans la plupart des régions, les données d’un compte de stockage Standard peuvent être répliquées localement ou géorépliquées entre plusieurs centres de données. Hello quatre types de réplication disponible sont stockage localement redondant (LRS), stockage redondance de Zone (ZRS), stockage géo-redondant (GRS) et stockage géo-redondant d’accès en lecture (RA-GRS). Actuellement, les disques gérés dans le stockage Standard prennent seulement en charge le stockage localement redondant (LRS). Pour plus d'informations, consultez [Réplication Azure Storage](storage-redundancy.md).

## <a name="scalability-and-performance-targets"></a>Cibles de performance et d’évolutivité

Dans cette section, nous allons examiner les cibles d’évolutivité et de performances hello vous devez tooconsider lors de l’utilisation du stockage standard.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>Limites de compte : ne s’applique pas les disques toomanaged

| **Ressource** | **Limite par défaut** |
|--------------|-------------------|
| To par compte de stockage  | 500 To |
| Entrée max.<sup>1</sup> par compte de stockage (régions des États-Unis) | 10 Gbit/s si GRS/ZRS est activé, 20 Gbit/s pour LRS |
| Sortie max.<sup>1</sup> par compte de stockage (régions des États-Unis) | 20 Gbit/s si RA-GRS/GRS/ZRS est activé, 30 Gbit/s pour LRS |
| Entrée max.<sup>1</sup> par compte de stockage (régions d’Europe et d’Asie) | 5 Gbit/s si GRS/ZRS est activé, 10 Gbit/s pour LRS |
| Sortie max.<sup>1</sup> par compte de stockage (régions d'Europe et d'Asie) | 10 Gbit/s si RA-GRS/GRS/ZRS est activé, 15 Gbit/s pour LRS |
| Taux de demandes total (objets de 1 Ko) par compte de stockage | Les too20, les IOPS 000, les entités par seconde ou les messages par seconde |

<sup>1</sup> entrée fait référence à des données tooall (demandes) envoyées compte de stockage tooa. Sortie fait référence à des données tooall (réponses) reçues à partir d’un compte de stockage.

Pour plus d'informations, consultez [Objectifs d'extensibilité et de performances d'Azure Storage](storage-scalability-targets.md).

Si hello a besoin de votre application dépassent les objectifs d’évolutivité hello d’un compte de stockage unique, générez votre application toouse plusieurs comptes de stockage et partitionner vos données sur ces comptes de stockage. Ou bien, vous pouvez disques gérés d’Azure et Azure gère le partitionnement hello et l’emplacement de vos données pour vous.

### <a name="standard-disks-limits"></a>Limites des disques Standard

Contrairement aux disques Premium, les opérations d’entrée/sortie hello par seconde (IOPS) et le débit (bande passante) de disques Standard ne sont pas déployées. Hello performances de disques standards varie en fonction de hello VM taille toowhich hello disque est attaché, non toohello taille du disque de hello. Vous devriez voir tooachieve des toohello limite de performances répertorié dans le tableau hello ci-dessous.

**Limites des disques Standard (gérés et non gérés)**

| **Niveau Machine Virtuelle**            | **Niveau de base - Machine virtuelle** | **Niveau standard - Machine virtuelle** |
|------------------------|-------------------|----------------------|
| Taille maximale du disque          | 4095 Go           | 4095 Go              |
| Max 8 Ko d’E/S par seconde par disque | Des too300         | Des too500            |
| Bande passante maximale par disque | Des too60 Mo/s     | Des too60 Mo/s        |

Si votre charge de travail exige la prise en charge des disques hautes performances à faible latence, vous devez envisager d’utiliser le stockage Premium. visitez d’autres avantages du stockage Premium, tooknow [stockage Premium à hautes performances et des disques de machine virtuelle Azure](storage-premium-storage.md). 

## <a name="snapshots-and-copy-blob"></a>Captures instantanées et copie d’objets blob

toohello service de stockage, les fichiers de disque dur virtuel hello est un objet blob de pages. Vous pouvez prendre des instantanés d’objets BLOB de pages et copiez-les emplacement tooanother, tel qu’un compte de stockage différent.

### <a name="unmanaged-disks"></a>Disques non gérés

Vous pouvez créer [instantanés incrémentiels](storage-incremental-snapshots.md) de disques standard non managé Bonjour même façon que vous utilisez des instantanés de stockage Standard. Nous vous recommandons de créer des instantanés et de puis copiez ces compte de stockage standard géo-redondant tooa instantanés si votre disque source est dans un compte de stockage redondant en local. Pour plus d'informations, consultez [Options de redondance du stockage Azure](storage-redundancy.md).

Si un disque est attaché tooa machine virtuelle, certaines opérations d’API ne sont pas autorisées sur des disques hello. Par exemple, vous ne pouvez pas effectuer une [Copy Blob](/rest/api/storageservices/Copy-Blob) opération sur cet objet blob en tant que disque de hello est attaché tooa machine virtuelle. Au lieu de cela, créez tout d’abord un instantané de cet objet blob à l’aide de hello [objet Blob instantané](/rest/api/storageservices/Snapshot-Blob) reste la méthode d’API, puis effectuer hello [Copy Blob](/rest/api/storageservices/Copy-Blob) Hello de hello instantané toocopy disque attaché. Vous pouvez également détacher un disque de hello et puis effectuez les opérations nécessaires.

toomaintain copies géo-redondant de vos captures instantanées, vous pouvez copier des instantanés à partir d’un compte de stockage standard géo-redondant tooa stockage localement redondant compte à l’aide de AzCopy ou copie d’objets Blob. Pour plus d’informations, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md) et [Copy Blob](/rest/api/storageservices/Copy-Blob).

Pour plus d’informations sur l’exécution d’opérations REST sur les objets blob de pages dans les comptes de stockage Standard, consultez [API REST des services d’Azure Storage](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference).

### <a name="managed-disks"></a>Disques gérés

Un instantané d’un disque géré est une copie en lecture seule de disque géré de hello qui est stocké comme un disque géré standard. Instantanés incrémentiels ne sont pas actuellement pris en charge pour les disques gérés, mais seront prises en charge dans les futures de hello.

Si un disque managé est attaché tooa machine virtuelle, certaines opérations d’API ne sont pas autorisées sur des disques hello. Par exemple, vous ne peut pas générer un tooperform de signature (SAP) d’accès partagé une opération de copie pendant les disque hello attaché tooa machine virtuelle. Au lieu de cela, tout d’abord créer un instantané du disque de hello, puis copier hello d’instantané de hello. Ou bien, vous pouvez détacher un disque de hello et puis générer une opération de copie hello tooperform accès partagé (SAS) de signature.

## <a name="pricing-and-billing"></a>Tarification et facturation

L’utilisation du stockage Standard, hello facturation considérations suivantes s’appliquent :

* Taille des données/disques non gérés du stockage standard 
* Disques gérés Standard
* Captures instantanées du stockage Standard
* Transferts de données sortantes
* Transactions

**Non managée de taille de données et de disques de stockage :** pour les disques non gérés et d’autres données (objets BLOB, tables, files d’attente et fichiers), vous êtes facturé uniquement pour la quantité de hello d’espace que vous utilisez. Par exemple, si vous avez une machine virtuelle dont objet blob de pages est approvisionné comme 127 Go, mais hello machine virtuelle est vraiment uniquement à l’aide de 10 Go d’espace, vous serez facturé pour 10 Go d’espace. Nous prenons en charge le stockage Standard des too8191 Go et des disques non managés Standard des too4095 go. 

**Des disques gérés par :** géré disques sont facturées selon la taille de hello configuré. Si votre disque est approvisionné comme un disque de 10 Go et que vous utilisez uniquement les 5 Go, vous serez encore facturé pour la taille de disposition hello de 10 Go.

**Instantanés**: clichés instantanés des disques standards sont facturés pour une capacité supplémentaire hello utilisée par les instantanés de hello. Pour plus d'informations sur les captures instantanées, consultez [Création d'un instantané d'objet blob](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

**Transferts de données sortantes**: les [transferts de données sortantes](https://azure.microsoft.com/pricing/details/data-transfers/) (données sortant des centres de données Azure) sont facturés en fonction de la bande passante utilisée.

**Transaction** : Azure facture 0,0036 $ par tranche de 100 000 transactions de stockage standard. Les transactions sont en lecture et toostorage des opérations d’écriture.

Pour plus d’informations sur la tarification du stockage Standard, des machines virtuelles et des disques gérés, consultez :

* [Tarification d’Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Tarification des disques gérés](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Prise en charge du service Azure Backup 

Les machines virtuelles avec disques non gérés peuvent être sauvegardées à l’aide de Sauvegarde Azure. [Détails supplémentaires](../backup/backup-azure-vms-first-look-arm.md).

Vous pouvez également utiliser hello service sauvegarde Azure avec disques gérés toocreate un travail de sauvegarde avec les sauvegardes basées sur le temps, restauration facile de machine virtuelle et les stratégies de rétention de sauvegarde. Vous pouvez en savoir plus sur ce point dans [Using Azure Backup service for VMs with Managed Disks](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup) (Utilisation du service Azure Backup pour les machines virtuelles avec disques gérés).

## <a name="next-steps"></a>Étapes suivantes

* [Introduction tooAzure stockage](storage-introduction.md)

* [Créer un compte de stockage](storage-create-storage-account.md)

* [Vue d’ensemble des disques gérés](storage-managed-disks-overview.md)

* [Créer une machine virtuelle à l’aide de Resource Manager et de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Créer une VM Linux à l’aide de hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md)
