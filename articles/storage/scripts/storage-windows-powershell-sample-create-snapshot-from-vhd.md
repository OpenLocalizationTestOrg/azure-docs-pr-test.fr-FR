---
title: "aaaAzure exemple de Script PowerShell - créer un instantané à partir d’un disque dur virtuel toocreate plusieurs disques gérés identiques dans peu de temps | Documents Microsoft"
description: "Script Azure PowerShell exemple : création d’un instantané à partir d’un disque dur virtuel toocreate plusieurs disques gérés identiques dans peu de temps"
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
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Créer un instantané à partir d’un disque dur virtuel toocreate plusieurs disques gérés identiques dans peu de temps avec PowerShell

Ce script crée une capture instantanée à partir d’un fichier de disque dur virtuel dans un compte de stockage dans le même abonnement ou un abonnement différent. Ce script de tooimport un instantané de tooa de disque dur virtuel (pas généralisé/préparée avec Sysprep) spécialisé et d’utiliser hello instantané toocreate plusieurs disques gérés identiques dans peu de temps. Utilisez-le également pour tooimport un instantané de tooa de disque dur virtuel de données et utilisez hello instantané toocreate plusieurs disques gérés dans peu de temps. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un disque dur virtuel dans un autre abonnement. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Crée une configuration de disque qui est utilisée pour la création du disque. Il inclut le type de stockage, l’emplacement, Id de ressource de compte de stockage hello stockage de disque dur virtuel parent de hello et URI VHD du disque dur virtuel parent de hello. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres. |

## <a name="next-steps"></a>Étapes suivantes

[Créer un disque géré à partir d’une capture instantanée](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Créer une machine virtuelle en attachant un disque géré en tant que disque de système d’exploitation](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).

Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
