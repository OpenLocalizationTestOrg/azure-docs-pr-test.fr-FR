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
# <a name="resize-a-windows-vm"></a><span data-ttu-id="af494-103">Redimensionner une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="af494-103">Resize a Windows VM</span></span>
<span data-ttu-id="af494-104">Cet article explique comment tooresize une machine virtuelle Windows, créé dans le modèle de déploiement hello Gestionnaire de ressources à l’aide d’Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="af494-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="af494-105">Après avoir créé un ordinateur virtuel (VM), vous pouvez faire évoluer hello machine virtuelle vers le haut ou vers le bas en modifiant la taille de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="af494-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="af494-106">Dans certains cas, vous devez libérer hello VM tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="af494-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="af494-107">Cela peut se produire si la nouvelle taille de hello n’est pas disponible sur le cluster de matériel hello qui héberge actuellement hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af494-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="af494-108">Redimensionner une machine virtuelle Windows qui ne se trouve pas dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="af494-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="af494-109">Liste des tailles de machine virtuelle hello qui sont disponibles sur le cluster de matériel hello où hello ordinateur virtuel est hébergé.</span><span class="sxs-lookup"><span data-stu-id="af494-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="af494-110">Si hello souhaité est indiquée, exécutez hello suivant de commandes tooresize hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af494-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="af494-111">Hello éventuellement taille n’est pas répertoriée, passez toostep 3.</span><span class="sxs-lookup"><span data-stu-id="af494-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="af494-112">Hello éventuellement taille n’est pas répertoriée, exécutez hello suivant les commandes toodeallocate hello VM, redimensionner et redémarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af494-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
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
> <span data-ttu-id="af494-113">Hello désallocation de machine virtuelle libère toutes les adresses IP dynamiques affectées toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af494-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="af494-114">Hello du système d’exploitation et des disques de données ne sont pas affectées.</span><span class="sxs-lookup"><span data-stu-id="af494-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="af494-115">Redimensionner une machine virtuelle Windows qui se trouve dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="af494-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="af494-116">Si hello nouvelle taille pour une machine virtuelle dans un ensemble de disponibilité n’est pas disponible sur hello matériel cluster héberge actuellement hello machine virtuelle, puis tous les ordinateurs virtuels dans le groupe à haute disponibilité hello devez toobe désalloué tooresize hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af494-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="af494-117">Vous devrez également peut-être taille de hello tooupdate des autres machines virtuelles disponibilité hello après qu’une machine virtuelle a été redimensionnée.</span><span class="sxs-lookup"><span data-stu-id="af494-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="af494-118">tooresize une machine virtuelle dans un ensemble de disponibilité, effectuez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="af494-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="af494-119">Liste des tailles de machine virtuelle hello qui sont disponibles sur le cluster de matériel hello où hello ordinateur virtuel est hébergé.</span><span class="sxs-lookup"><span data-stu-id="af494-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="af494-120">Si hello souhaité est indiquée, exécutez hello suivant de commandes tooresize hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af494-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="af494-121">S’il n’est pas répertorié, accédez toostep 3.</span><span class="sxs-lookup"><span data-stu-id="af494-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="af494-122">Hello éventuellement taille n’est pas répertoriée, continuez hello suivant les étapes toodeallocate de tous les ordinateurs virtuels dans le groupe à haute disponibilité hello, redimensionnez des machines virtuelles et les redémarrer.</span><span class="sxs-lookup"><span data-stu-id="af494-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="af494-123">Arrêtez tous les ordinateurs virtuels dans le groupe à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="af494-123">Stop all VMs in hello availability set.</span></span>
   
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
5. <span data-ttu-id="af494-124">Redimensionner et redémarrer les machines virtuelles de hello en hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="af494-124">Resize and restart hello VMs in hello availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="af494-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af494-125">Next steps</span></span>
* <span data-ttu-id="af494-126">Pour une évolutivité supplémentaire, exécutez plusieurs instances de machine virtuelle et augmentez leur taille. Pour plus d’informations, consultez [Mise à l’échelle automatique des machines Windows dans un groupe de machines virtuelles identiques](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="af494-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

