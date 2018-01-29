---
title: "Exemple de script Azure PowerShell : exporter/copier une capture instantanée en tant que disque dur virtuel vers un compte de stockage dans une autre région | Microsoft Docs"
description: "Exemple de script Azure PowerShell : exporter/copier une capture instantanée en tant que disque dur virtuel vers un compte de stockage dans une autre région"
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
ms.openlocfilehash: be21a891121df1d645b430d87b572cde6c945d61
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-powershell"></a>Exporter/copier des captures instantanées gérées en tant que disque dur virtuel vers un compte de stockage dans une région différente avec PowerShell

Ce script exporte une capture instantanée gérée vers un compte de stockage dans une région différente. Il génère d’abord l’URI SAP de la capture instantanée et l’utilise ensuite pour copier celle-ci vers un compte de stockage dans une autre région. Ce script vous permet de conserver la sauvegarde de vos disques gérés dans une autre région en cas de récupération d’urgence.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes afin de générer un URI SAS pour une capture instantanée gérée et copie cette dernière vers un compte de stockage à l’aide de l’URI SAS. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Remarques |
|---|---|
| [Grant-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | Génère l’URI SAS pour une capture instantanée qui est utilisée pour sa copie dans un compte de stockage. |
| [New-AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Crée un contexte de compte de stockage avec le nom de compte et la clé. Ce contexte peut être utilisé pour effectuer des opérations de lecture/écriture sur le compte de stockage. |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Copie le VHD sous-jacent d’une capture instantanée vers un compte de stockage |

## <a name="next-steps"></a>Étapes suivantes

[Créer un disque managé à partir d’un VHD](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Créer une machine virtuelle à partir d’un disque géré](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Pour plus d’informations sur le module Azure PowerShell, consultez [Documentation Azure PowerShell](/powershell/azure/overview).

Vous trouverez des exemples supplémentaires de scripts PowerShell de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).