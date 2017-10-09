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
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="e34e8-103">Convertir une machine virtuelle Windows à partir de disques toomanaged de disques non managé</span><span class="sxs-lookup"><span data-stu-id="e34e8-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="e34e8-104">Si vous avez des machines virtuelles Windows existantes (VM) qui utilisent des disques non managés, vous pouvez convertir les disques de toouse géré de machines virtuelles de hello via hello [disques gérés d’Azure](managed-disks-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="e34e8-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="e34e8-105">Ce processus convertit le disque de hello du système d’exploitation et les disques de données attaché.</span><span class="sxs-lookup"><span data-stu-id="e34e8-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="e34e8-106">Cet article vous montre comment tooconvert machines virtuelles à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e34e8-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="e34e8-107">Si vous avez besoin de tooinstall ou mettre à niveau, consultez [installer et configurer Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e34e8-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e34e8-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e34e8-108">Before you begin</span></span>


* <span data-ttu-id="e34e8-109">Révision [planifier la migration de hello de disques de tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="e34e8-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="e34e8-110">Convertir des machines virtuelles à instance unique</span><span class="sxs-lookup"><span data-stu-id="e34e8-110">Convert single-instance VMs</span></span>
<span data-ttu-id="e34e8-111">Cette section explique comment des machines virtuelles Azure à partir de non managé à instance unique de tooconvert disques toomanaged disques.</span><span class="sxs-lookup"><span data-stu-id="e34e8-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="e34e8-112">(Si vos machines virtuelles sont dans un ensemble de disponibilité, voir section suivante de hello).</span><span class="sxs-lookup"><span data-stu-id="e34e8-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="e34e8-113">Désallouer hello machine virtuelle à l’aide de hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e34e8-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="e34e8-114">exemple Hello désalloue hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e34e8-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="e34e8-115">Convertir les disques de toomanaged hello machine virtuelle à l’aide de hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e34e8-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="e34e8-116">Hello suivant convertit des processus hello machine virtuelle précédente, y compris les disques hello du système d’exploitation et les disques de données :</span><span class="sxs-lookup"><span data-stu-id="e34e8-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="e34e8-117">Démarrer hello machine virtuelle une fois les disques toomanaged hello conversion à l’aide de [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="e34e8-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="e34e8-118">Hello après le redémarrage de l’exemple hello VM précédente :</span><span class="sxs-lookup"><span data-stu-id="e34e8-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="e34e8-119">Convertir des machines virtuelles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="e34e8-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="e34e8-120">Si hello machines virtuelles que vous souhaitez tooconvert toomanaged disques se trouvent dans un ensemble de disponibilité, vous devez commencer tooconvert hello disponibilité ensemble tooa géré à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e34e8-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="e34e8-121">Convertir hello groupe à haute disponibilité à l’aide de hello [AzureRmAvailabilitySet de mise à jour](/powershell/module/azurerm.compute/update-azurermavailabilityset) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e34e8-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="e34e8-122">Hello, exemple de mises à jour hello groupe à haute disponibilité nommée suivant `myAvailabilitySet` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e34e8-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="e34e8-123">Si région hello où se trouve votre jeu de disponibilité possède des domaines d’erreur gérés uniquement 2, mais nombre hello de domaines d’erreur non managé est 3, cette commande affiche une erreur similaire trop « hello spécifié. nombre de domaines d’erreur 3 doit être compris hello compris entre 1 too2. »</span><span class="sxs-lookup"><span data-stu-id="e34e8-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="e34e8-124">tooresolve hello d’erreur, too2 de domaine de mise à jour hello pannes et mise à jour `Sku` trop`Aligned` comme suit :</span><span class="sxs-lookup"><span data-stu-id="e34e8-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="e34e8-125">Désallouer et convertir des machines virtuelles de hello dans hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e34e8-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="e34e8-126">Hello script suivant libère chaque machine virtuelle à l’aide de hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) applet de commande, il convertit en utilisant [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)et le redémarre à l’aide de [AzureRmVM de début ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="e34e8-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="e34e8-127">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="e34e8-127">Troubleshooting</span></span>

<span data-ttu-id="e34e8-128">S’il existe une erreur lors de la conversion, ou si un ordinateur virtuel est dans un état d’échec en raison de problèmes dans une conversion précédente, exécutez hello `ConvertTo-AzureRmVMManagedDisk` applet de commande à nouveau.</span><span class="sxs-lookup"><span data-stu-id="e34e8-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="e34e8-129">Généralement, une nouvelle tentative simple débloque situation de hello.</span><span class="sxs-lookup"><span data-stu-id="e34e8-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e34e8-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e34e8-130">Next steps</span></span>

[<span data-ttu-id="e34e8-131">Convertir des disques gérés standard toopremium</span><span class="sxs-lookup"><span data-stu-id="e34e8-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="e34e8-132">Créez une copie en lecture seule d’une machine virtuelle en utilisant des [captures instantanées](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="e34e8-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

