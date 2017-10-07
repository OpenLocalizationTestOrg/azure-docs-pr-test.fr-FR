---
title: aaaUse PowerShell tooresize un ordinateur virtuel Windows Azure | Documents Microsoft
description: "Redimensionner une machine virtuelle de Windows créée dans le modèle de déploiement de gestionnaire de ressources hello, à l’aide d’Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a>Redimensionner une machine virtuelle Windows
Cet article explique comment tooresize une machine virtuelle Windows, créé dans le modèle de déploiement hello Gestionnaire de ressources à l’aide d’Azure Powershell.

Après avoir créé un ordinateur virtuel (VM), vous pouvez faire évoluer hello machine virtuelle vers le haut ou vers le bas en modifiant la taille de machine virtuelle hello. Dans certains cas, vous devez libérer hello VM tout d’abord. Cela peut se produire si la nouvelle taille de hello n’est pas disponible sur le cluster de matériel hello qui héberge actuellement hello machine virtuelle.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Redimensionner une machine virtuelle Windows qui ne se trouve pas dans un groupe à haute disponibilité
1. Liste des tailles de machine virtuelle hello qui sont disponibles sur le cluster de matériel hello où hello ordinateur virtuel est hébergé. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. Si hello souhaité est indiquée, exécutez hello suivant de commandes tooresize hello machine virtuelle. Hello éventuellement taille n’est pas répertoriée, passez toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Hello éventuellement taille n’est pas répertoriée, exécutez hello suivant les commandes toodeallocate hello VM, redimensionner et redémarrez hello machine virtuelle.
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> Hello désallocation de machine virtuelle libère toutes les adresses IP dynamiques affectées toohello machine virtuelle. Hello du système d’exploitation et des disques de données ne sont pas affectées. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Redimensionner une machine virtuelle Windows qui se trouve dans un groupe à haute disponibilité
Si hello nouvelle taille pour une machine virtuelle dans un ensemble de disponibilité n’est pas disponible sur hello matériel cluster héberge actuellement hello machine virtuelle, puis tous les ordinateurs virtuels dans le groupe à haute disponibilité hello devez toobe désalloué tooresize hello machine virtuelle. Vous devrez également peut-être taille de hello tooupdate des autres machines virtuelles disponibilité hello après qu’une machine virtuelle a été redimensionnée. tooresize une machine virtuelle dans un ensemble de disponibilité, effectuez hello comme suit.

1. Liste des tailles de machine virtuelle hello qui sont disponibles sur le cluster de matériel hello où hello ordinateur virtuel est hébergé.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. Si hello souhaité est indiquée, exécutez hello suivant de commandes tooresize hello machine virtuelle. S’il n’est pas répertorié, accédez toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Hello éventuellement taille n’est pas répertoriée, continuez hello suivant les étapes toodeallocate de tous les ordinateurs virtuels dans le groupe à haute disponibilité hello, redimensionnez des machines virtuelles et les redémarrer.
4. Arrêtez tous les ordinateurs virtuels dans le groupe à haute disponibilité hello.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. Redimensionner et redémarrer les machines virtuelles de hello en hello à haute disponibilité.
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a>Étapes suivantes
* Pour une évolutivité supplémentaire, exécutez plusieurs instances de machine virtuelle et augmentez leur taille. Pour plus d’informations, consultez [Mise à l’échelle automatique des machines Windows dans un groupe de machines virtuelles identiques](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

