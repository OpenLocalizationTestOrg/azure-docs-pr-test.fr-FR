---
title: "aaaAzure exemple de Script PowerShell - créer un disque géré à partir d’un instantané | Documents Microsoft"
description: "Exemple de script Azure PowerShell : Créer un disque géré à partir d’une capture instantanée"
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
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a>Créer un disque géré à partir d’une capture instantanée avec PowerShell

Ce script crée un disque managé à partir d’une capture instantanée. Utiliser toorestore une machine virtuelle à partir de clichés instantanés des disques du système d’exploitation et des données. Créez des disques managés de système d’exploitation et de données à partir des captures instantanées respectives, puis créez une machine virtuelle en joignant les disques managés. Vous pouvez également restaurer les disques de données d’une machine virtuelle existante en joignant les disques de données créés à partir de captures instantanées.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Explication du script

Ce script utilise à la suite de commandes toocreate un disque géré à partir d’un instantané. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [Get-AzureRmSnapshot](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | Obtient les propriétés de capture instantanée.  |
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Crée une configuration de disque qui est utilisée pour la création du disque. Il inclut des Id d’instantané de parent hello, emplacement qui est identique à l’emplacement de hello du type de stockage des instantanés et hello parent de la ressource hello.  |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Crée un disque à partir de la configuration de disque, du nom du disque et du nom de groupe de ressources transmis en tant que paramètres. |


## <a name="next-steps"></a>Étapes suivantes

[Créer une machine virtuelle à partir d’un disque géré](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).

Exemples de script PowerShell supplémentaires de l’ordinateur virtuel se trouvent Bonjour [documentation de Windows Azure VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
