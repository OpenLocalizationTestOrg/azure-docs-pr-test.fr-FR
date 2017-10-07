---
title: "aaaAvailability définit le didacticiel pour les machines virtuelles Windows dans Azure | Documents Microsoft"
description: "Découvrez hello disponibilité définit pour les machines virtuelles Windows dans Azure."
documentationcenter: 
services: virtual-machines-windows
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
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Comment à haute disponibilité de toouse

Dans ce didacticiel, vous allez apprendre comment la disponibilité de hello tooincrease et la fiabilité de vos solutions d’ordinateur virtuel sur Azure à l’aide d’une fonctionnalité appelée haute disponibilité. Haute disponibilité vous assurer que hello machines virtuelles que vous déployez sur Azure sont réparties entre plusieurs clusters matérielles isolées. Cela garantit que si une défaillance matérielle ou logicielle dans Azure se produit, qu’un ensemble sous-chemin de vos machines virtuelles est concerné et que votre solution globale resteront disponibles et opérationnels du point de vue hello de vos clients à l’utiliser. 

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un groupe à haute disponibilité
> * Créer une machine virtuelle dans un groupe à haute disponibilité
> * Vérifier les tailles de machines virtuelles disponibles

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Vue d’ensemble des groupes à haute disponibilité

Un ensemble de disponibilité d’est une fonctionnalité de regroupement logique que vous pouvez utiliser dans Azure tooensure que les ressources de machine virtuelle de hello que vous placez qu’il contient sont isolées des autres lorsqu’ils sont déployés dans un centre de données Azure. Azure garantit que machines virtuelles que vous placez dans un ensemble de disponibilité s’exécuter sur plusieurs serveurs physiques hello, le calcul des racks, les unités de stockage et les commutateurs de réseau. Cela garantit que dans le cas de hello d’un problème matériel ou logiciel d’Azure, uniquement un sous-ensemble de vos machines virtuelles est affecté, et continuer à et continuer toobe disponible tooyour clients de votre application globale. À l’aide de la haute disponibilité est une fonctionnalité essentielle de tooleverage toobuild les solutions de cloud fiable.

Prenons l’exemple d’une solution basée sur une machine virtuelle classique dans laquelle vous disposez de 4 serveurs web frontaux et utilisez 2 machines virtuelles principales hébergeant une base de données. Avec Azure, vous souhaiteriez toodefine deux groupes à haute disponibilité avant de déployer vos machines virtuelles : une disponibilité définie pour le niveau de « web » hello et une haute disponibilité pour le niveau de « base de données » hello. Lorsque vous créez une nouvelle machine virtuelle que vous pouvez ensuite spécifier hello groupe à haute disponibilité comme une machine virtuelle de paramètre toohello az Créer commande et Azure automatiquement garantit que machines virtuelles que vous créez au sein de hello disponible hello ensemble sont isolés sur plusieurs ressources de matériel physique. Cela signifie que si le matériel physique hello que votre serveur Web ou les machines virtuelles de serveur de base de données est en cours d’exécution sur a un problème, vous savez que hello autres instances de votre serveur Web et les machines virtuelles de base de données reste en cours d’exécution correctement, car ils sont sur un matériel différent.

Vous devez toujours utiliser des ensembles de disponibilité lorsque vous souhaitez que des solutions toodeploy fiables en fonction de machine virtuelle dans Azure.

## <a name="create-an-availability-set"></a>Créer un groupe à haute disponibilité

Vous pouvez créez un groupe à haute disponibilité avec la commande [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Dans cet exemple, nous avons défini à la fois nombre hello domaines de mise à jour et d’erreur à *2* pour hello groupe à haute disponibilité nommée *myAvailabilitySet* Bonjour *myResourceGroupAvailability*groupe de ressources.

Créez un groupe de ressources.

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>Créer des machines virtuelles dans un groupe à haute disponibilité

Machines virtuelles doivent toobe créé dans hello disponibilité ensemble toomake qu’ils sont correctement distribués sur les matériels hello. Vous ne pouvez pas ajouter un groupe de machines virtuelles tooan disponibilité définie après sa création. 

matériel Hello dans un emplacement est divisée dans les domaines de mise à jour toomultiple et les domaines d’erreur. Un **domaine de mise à jour** est un groupe de machines virtuelles et le matériel physique sous-jacent qui peut être redémarré à hello même temps. Machines virtuelles dans hello même **domaine d’erreur** partager commun, ainsi qu’un commutateur de réseau et de la source power courantes. 

Lorsque vous créez une machine virtuelle à l’aide de la configuration à l’aide [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) vous spécifiez hello haute disponibilité via hello `-AvailabilitySetId` hello toospecify du paramètre d’ID de groupe à haute disponibilité hello.

Créer 2 machines virtuelles avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) groupe à haute disponibilité hello définie.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

Il prend quelques minutes toocreate et configurer les deux ordinateurs virtuels. Lorsque vous avez terminé, vous aurez 2 machines virtuelles sont réparties entre hello matériel sous-jacent. 

## <a name="check-for-available-vm-sizes"></a>Vérifier les tailles de machines virtuelles disponibles 

Vous pouvez ajouter plusieurs machines virtuelles toohello haute disponibilité plus tard, mais vous devez tooknow les tailles de machine virtuelle sont disponibles sur le matériel de hello. Utilisez [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist toutes les tailles disponibles hello sur du matériel de hello du cluster pour hello à haute disponibilité.

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créer un groupe à haute disponibilité
> * Créer une machine virtuelle dans un groupe à haute disponibilité
> * Vérifier les tailles de machines virtuelles disponibles

Avance toohello toolearn de didacticiel suivant sur les machines virtuelles identiques.

> [!div class="nextstepaction"]
> [Créer un groupe de machines virtuelles identiques](tutorial-create-vmss.md)


