---
title: "aaaAzure instantané/copie de l’exportation en tant que compte de stockage de disque dur virtuel tooa dans autre région - exemple de Script PowerShell | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - instantané/copie de l’exportation en tant que compte de stockage de disque dur virtuel tooa dans la même région différente"
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
ms.openlocfilehash: c18ad4fa0bf12033fafe941a807e7b4c8d233a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Exportation ou copier des instantanés gérés en tant que compte de stockage de disque dur virtuel tooa dans autre région avec PowerShell

Ce script exporte un compte de stockage géré instantané tooa dans autre région. Il génère d’abord hello URI SAS d’instantané de hello et utilise ensuite toocopy il compte de stockage tooa dans autre région. Utilisez cette sauvegarde toomaintain de script de vos disques gérés dans autre région pour la récupération d’urgence.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise suivante commandes toogenerate URI SAS pour un Bonjour de capture instantanée ni copie managé d’instantané tooa compte de stockage à l’aide de l’URI SAS. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [Grant-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | Génère l’URI SAS pour un instantané est utilisé toocopy il compte de stockage tooa. |
| [New-AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Crée un contexte de compte de stockage à l’aide de la clé et le nom du compte hello. Ce contexte peut être tooperform utilisé les opérations de lecture/écriture sur le compte de stockage hello. |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Copies hello disque dur virtuel sous-jacent d’un compte de stockage tooa instantané |

## <a name="next-steps"></a>Étapes suivantes

[Créer un disque managé à partir d’un VHD](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Créer une machine virtuelle à partir d’un disque géré](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).

Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
