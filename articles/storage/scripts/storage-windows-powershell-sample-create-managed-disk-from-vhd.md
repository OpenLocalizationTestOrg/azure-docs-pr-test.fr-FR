---
title: "aaaAzure exemple de Script PowerShell - créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage dans l’abonnement identiques ou différent | Documents Microsoft"
description: "Exemple de script Azure PowerShell - Créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou dans un abonnement différent"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Créer un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou dans un abonnement différent avec PowerShell

Ce script crée un disque géré à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou un abonnement différent. Utilisez cette tooimport script un spécialisé toocreate (pas généralisé/préparée avec Sysprep) disque dur virtuel toomanaged du système d’exploitation disque un ordinateur virtuel. Utilisez-le également pour tooimport un disque de données toomanaged données disque dur virtuel. 

Ne créez pas plusieurs disques gérés identiques à partir d’un fichier de disque dur virtuel dans un court laps de temps. toocreate des disques gérés à partir d’un fichier de disque dur virtuel, instantané d’objet blob du fichier de disque dur virtuel hello est créé et il est utilisé toocreate géré disques. Instantané d’objet seul blob peut être créé dans une minute qui provoque l’échec de la création de disque toothrottling échéance. tooavoid cette limitation, créer un [instantané managé à partir du fichier de disque dur virtuel hello](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) , puis utilisez hello gérés instantané toocreate plusieurs disques gérés dans peu de temps. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un disque dur virtuel dans un autre abonnement. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Crée une configuration de disque qui est utilisée pour la création du disque. Il inclut le type de stockage, emplacement, Id de ressource de hello compte de stockage où le disque dur virtuel parent de hello est stocké, URI VHD du disque dur virtuel parent de hello. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres. |

## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).

Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
