---
title: aaaManage Azure disques avec hello Azure PowerShell | Documents Microsoft
description: "Didacticiel - gérer les disques Azure avec hello Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Gestion des disques Azure avec PowerShell

Machines virtuelles Azure utilisent le système d’exploitation de disques toostore hello machines virtuelles, des applications et des données. Lorsque vous créez une machine virtuelle, il est important toochoose une taille de disque et la charge de travail de configuration approprié toohello attendu. Ce didacticiel décrit le déploiement et la gestion des disques de machine virtuelle. Vous en apprendrez davantage sur les points suivants :

> [!div class="checklist"]
> * Disques de système d’exploitation et disques temporaires
> * Disques de données
> * Disques Standard et Premium
> * Performances des disques
> * Attachement et préparation des disques de données

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Disques Azure par défaut

Création d’une machine virtuelle Azure, deux disques sont automatiquement attaché toohello virtual machine. 

**Disque de système d’exploitation** - disques de système d’exploitation peuvent être dimensionnés des téraoctets de too1 et hôtes hello de système d’exploitation de machines virtuelles.  disque de Hello du système d’exploitation est attribué à une lettre de lecteur de *c:* par défaut. disque Hello mise en cache de la configuration du disque du système d’exploitation hello est optimisé pour les performances du système d’exploitation. disque de Hello du système d’exploitation **ne doivent pas** héberger des applications ou des données. Pour héberger ce type de contenu, utilisez plutôt un disque de données, qui est décrit plus loin dans cet article.

**Disque temporaire** -les disques temporaires utilisent un disque SSD qui se trouve sur hello même hôte Azure en tant que machine virtuelle de hello. Les disques temporaires sont extrêmement performants et peuvent être utilisés pour des opérations telles que le traitement de données temporaires. Toutefois, si hello machine virtuelle est déplacée tooa nouvel hôte, toutes les données stockées sur un disque temporaire sont supprimées. taille de Hello du disque temporaire de hello est déterminé par hello taille de machine virtuelle. Les disques temporaires se voient attribuer la lettre de lecteur *d:* par défaut.

### <a name="temporary-disk-sizes"></a>Tailles du disque temporaire

| Type | Taille de la machine virtuelle | Taille maximale du disque temporaire (Go) |
|----|----|----|
| [Usage général](sizes-general.md) | Séries A et D | 800 |
| [Optimisé pour le calcul](sizes-compute.md) | Série F | 800 |
| [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md) | Séries D et G | 6144 |
| [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md) | Série L | 5630 |
| [GPU](sizes-gpu.md) | Série N | 1 440 |
| [Hautes performances](sizes-hpc.md) | Séries A et H | 2000 |

## <a name="azure-data-disks"></a>Disques de données Azure

Des disques de données supplémentaires peuvent être ajoutés pour installer des applications et stocker des données. Les disques de données doivent être utilisés dans les cas où un stockage des données durable et réactif est souhaité. Chaque disque de données possède une capacité maximale de 1 To. taille de Hello de machine virtuelle de hello détermine le nombre de disques de données peut être attaché tooa machine virtuelle. Pour chaque cœur de la machine virtuelle, deux disques de données peuvent être attachés. 

### <a name="max-data-disks-per-vm"></a>Disques de données max. par machine virtuelle

| Type | Taille de la machine virtuelle | Disques de données max. par machine virtuelle |
|----|----|----|
| [Usage général](sizes-general.md) | Séries A et D | 32 |
| [Optimisé pour le calcul](sizes-compute.md) | Série F | 32 |
| [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md) | Séries D et G | 64 |
| [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md) | Série L | 64 |
| [GPU](sizes-gpu.md) | Série N | 48 |
| [Hautes performances](sizes-hpc.md) | Séries A et H | 32 |

## <a name="vm-disk-types"></a>Type de disque de machine virtuelle

Azure propose deux types de disque.

### <a name="standard-disk"></a>Disque Standard

Le stockage Standard s’appuie sur des disques durs et offre un stockage économique qui n’en est pas moins performant. Les disques Standard constituent la solution idéale pour une charge de travail de développement et de test économique.

### <a name="premium-disk"></a>Disque Premium

Les disques Premium reposent sur un disque SSD à faible latence et hautes performances. Ils conviennent parfaitement aux machines virtuelles exécutant une charge de travail en production. Le stockage Premium prend en charge les machines virtuelles des séries DS, DSv2, GS et FS. Les disques Premium sont fournis dans les trois types (P10, P20, P30), taille hello du disque de hello détermine le type de disque hello. Lors de la sélection, une valeur de hello de taille de disque est arrondie toohello les type suivant. Par exemple, si la taille de hello est sous type de disque de 128 Go hello sera P10, entre 129 et 512 P20 dépasse 512 P30. 

### <a name="premium-disk-performance"></a>Performances du disque Premium

|Type de disque de stockage Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Taille du disque (arrondie) | 128 Go | 512 Go | 1 024 Go (1 To) |
| IOPS par disque | 500 | 2 300 | 5 000 |
Débit par disque | 100 Mo/s | 150 Mo/s | 200 Mo/s |

Tandis que hello au-dessus de table identifie max IOPS par disque, un niveau plus élevé de performances est possible par l’agrégation de plusieurs disques de données. Par exemple, des 64 données disques peuvent être jointes tooStandard_GS5 VM. Si chacun de ces disques est de type P30, vous pouvez atteindre un nombre maximum d’E/S par seconde de 80 000. Pour plus d’informations sur le nombre max. d’E/S par seconde par machine virtuelle, consultez [Tailles des machines virtuelles Linux dans Azure](./sizes.md).

## <a name="create-and-attach-disks"></a>Créer et attacher des disques

exemple de hello toocomplete dans ce didacticiel, vous devez disposer d’un ordinateur virtuel existant. Si nécessaire, cet [exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) peut en créer une pour vous. Lorsque le travail didacticiel de hello, remplacez machine virtuelle et groupe de ressources hello noms lorsque cela est nécessaire.

Créer la configuration initiale hello avec [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig). Bonjour à l’exemple suivant configure un disque qui est la taille de 128 gigaoctets.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Créer un disque de données hello avec hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) commande.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Ordinateur virtuel de Get hello que vous souhaitez tooadd Bonjour données disque toowith Bonjour [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) commande.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Ajouter hello données disque toohello configuration d’ordinateur virtuel avec hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) commande.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Mettre à jour de la machine virtuelle de hello avec hello [AzureRmVM de mise à jour](/powershell/module/azurerm.compute/add-azurermvmdatadisk) commande.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Préparer les disques de données

Une fois qu’un disque a été attaché toohello virtual machine, le système d’exploitation de hello doit toobe configuré toouse hello disque. Hello suivant montre comment toomanually configurer hello premier disque ajouté toohello machine virtuelle. Ce processus peut également être automatisé à l’aide de hello [extension de script personnalisé](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configuration manuelle

Créer une connexion RDP avec l’ordinateur virtuel de hello. Ouvrez PowerShell et exécutez ce script.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous a apporté des connaissances concernant les disques de machine virtuelle, notamment concernant les points suivants :

> [!div class="checklist"]
> * Disques de système d’exploitation et disques temporaires
> * Disques de données
> * Disques Standard et Premium
> * Performances des disques
> * Attachement et préparation des disques de données

Avance toohello toolearn de didacticiel suivant sur l’automatisation de configuration d’ordinateur virtuel.

> [!div class="nextstepaction"]
> [Automatiser la configuration de machine virtuelle](./tutorial-automate-vm-deployment.md)
