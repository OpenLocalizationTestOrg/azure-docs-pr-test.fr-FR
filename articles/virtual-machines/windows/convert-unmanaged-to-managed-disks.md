---
title: "aaaConvert un ordinateur virtuel Windows non managé disques toomanaged disques - Azure géré | Documents Microsoft"
description: "Comment tooconvert une machine virtuelle de Windows à partir de disques non managé toomanaged disques à l’aide de PowerShell dans le modèle de déploiement du Gestionnaire de ressources hello"
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
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Convertir une machine virtuelle Windows à partir de disques toomanaged de disques non managé

Si vous avez des machines virtuelles Windows existantes (VM) qui utilisent des disques non managés, vous pouvez convertir les disques de toouse géré de machines virtuelles de hello via hello [disques gérés d’Azure](managed-disks-overview.md) service. Ce processus convertit le disque de hello du système d’exploitation et les disques de données attaché.

Cet article vous montre comment tooconvert machines virtuelles à l’aide d’Azure PowerShell. Si vous avez besoin de tooinstall ou mettre à niveau, consultez [installer et configurer Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Avant de commencer


* Révision [planifier la migration de hello de disques de tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Convertir des machines virtuelles à instance unique
Cette section explique comment des machines virtuelles Azure à partir de non managé à instance unique de tooconvert disques toomanaged disques. (Si vos machines virtuelles sont dans un ensemble de disponibilité, voir section suivante de hello). 

1. Désallouer hello machine virtuelle à l’aide de hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) applet de commande. exemple Hello désalloue hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Convertir les disques de toomanaged hello machine virtuelle à l’aide de hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) applet de commande. Hello suivant convertit des processus hello machine virtuelle précédente, y compris les disques hello du système d’exploitation et les disques de données :

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Démarrer hello machine virtuelle une fois les disques toomanaged hello conversion à l’aide de [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm). Hello après le redémarrage de l’exemple hello VM précédente :

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Convertir des machines virtuelles dans un groupe à haute disponibilité

Si hello machines virtuelles que vous souhaitez tooconvert toomanaged disques se trouvent dans un ensemble de disponibilité, vous devez commencer tooconvert hello disponibilité ensemble tooa géré à haute disponibilité.

1. Convertir hello groupe à haute disponibilité à l’aide de hello [AzureRmAvailabilitySet de mise à jour](/powershell/module/azurerm.compute/update-azurermavailabilityset) applet de commande. Hello, exemple de mises à jour hello groupe à haute disponibilité nommée suivant `myAvailabilitySet` dans le groupe de ressources hello nommé `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Si région hello où se trouve votre jeu de disponibilité possède des domaines d’erreur gérés uniquement 2, mais nombre hello de domaines d’erreur non managé est 3, cette commande affiche une erreur similaire trop « hello spécifié. nombre de domaines d’erreur 3 doit être compris hello compris entre 1 too2. » tooresolve hello d’erreur, too2 de domaine de mise à jour hello pannes et mise à jour `Sku` trop`Aligned` comme suit :

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Désallouer et convertir des machines virtuelles de hello dans hello à haute disponibilité. Hello script suivant libère chaque machine virtuelle à l’aide de hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) applet de commande, il convertit en utilisant [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)et le redémarre à l’aide de [AzureRmVM de début ](/powershell/module/azurerm.compute/start-azurermvm):

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a>Résolution des problèmes

S’il existe une erreur lors de la conversion, ou si un ordinateur virtuel est dans un état d’échec en raison de problèmes dans une conversion précédente, exécutez hello `ConvertTo-AzureRmVMManagedDisk` applet de commande à nouveau. Généralement, une nouvelle tentative simple débloque situation de hello.


## <a name="next-steps"></a>Étapes suivantes

[Convertir des disques gérés standard toopremium](convert-disk-storage.md)

Créez une copie en lecture seule d’une machine virtuelle en utilisant des [captures instantanées](snapshot-copy-managed-disk.md).

