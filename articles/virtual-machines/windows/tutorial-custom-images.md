---
title: "images de machine virtuelle personnalisées aaaCreate avec hello Azure PowerShell | Documents Microsoft"
description: "Didacticiel : créer une image de machine virtuelle personnalisée à l’aide de hello Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Créer une image personnalisée d’une machine virtuelle Azure à l’aide de PowerShell

Les images personnalisées sont comme des images de la Place de marché, sauf que vous les créez vous-même. Images personnalisées peuvent être des configurations toobootstrap utilisés tels que le préchargement des applications, les configurations de l’application et les autres configurations de système d’exploitation. Ce didacticiel explique comment créer votre propre image personnalisée d’une machine virtuelle Azure. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Exécuter Sysprep et généraliser les machines virtuelles
> * Créer une image personnalisée
> * Créer une machine virtuelle à partir d’une image personnalisée
> * La liste de toutes les images hello dans votre abonnement
> * Supprimer une image

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Avant de commencer

étapes Hello ci-dessous décrit en détail comment tootake une machine virtuelle existante et les activer dans personnalisé réutilisable de l’image que vous peuvent utiliser toocreate de nouvelles instances de machine virtuelle.

exemple de hello toocomplete dans ce didacticiel, vous devez disposer d’un ordinateur virtuel existant. Si nécessaire, cet [exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) peut en créer une pour vous. Lorsque le travail didacticiel de hello, remplacez machine virtuelle et groupe de ressources hello noms lorsque cela est nécessaire.

## <a name="prepare-vm"></a>Préparer la machine virtuelle

toocreate une image d’un ordinateur virtuel, vous devez tooprepare hello VM par hello généraliser machine virtuelle, désallocation et puis marque la source de hello machine virtuelle comme généralisé dans Azure.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Généraliser hello virtuelle Windows à l’aide de Sysprep

Sysprep supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image. Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).


1. Connecter l’ordinateur virtuel de toohello.
2. Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur. Basculez hello trop*%windir%\system32\sysprep*, puis exécutez *sysprep.exe*.
3. Bonjour **outil de préparation système** boîte de dialogue, sélectionnez *entrer le système Out-of-Box Experience (OOBE)*et assurez-vous que hello *Generalize* case à cocher est activée.
4. Dans **Options d’arrêt**, sélectionnez *Arrêter*, puis cliquez sur **OK**.
5. Quand Sysprep se termine, il arrête de machine virtuelle de hello. **Ne redémarrez pas hello VM**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Désallouer et marquer hello machine virtuelle comme généralisé

toocreate une image, hello machine virtuelle doit toobe désalloué et marquée comme généralisé dans Azure.

À l’aide de machine virtuelle libérée hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Définir le statut de hello de machine virtuelle de hello trop`-Generalized` à l’aide de [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Création d’image de hello

Vous pouvez désormais créer une image de machine virtuelle de hello à l’aide de [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) et [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage). Hello exemple suivant crée une image nommée *myImage* à partir d’un ordinateur virtuel nommé *myVM*.

Obtenir un ordinateur virtuel de hello. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Créer la configuration de l’image hello.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Créer l’image de hello.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Créer des ordinateurs virtuels à partir de l’image de hello

Maintenant que vous disposez d’une image, vous pouvez créer un ou plusieurs nouveaux ordinateurs virtuels à partir de l’image de hello. Création d’une machine virtuelle à partir d’une image personnalisée est très similaire toocreating une machine virtuelle à l’aide d’une image de Marketplace. Lorsque vous utilisez une image de Marketplace, vous avez tooinformation sur les images de hello, fournisseur d’images, offre, référence (SKU) et version. Avec une image personnalisée, vous devez simplement des ID de hello tooprovide de ressource d’image personnalisée hello. 

Dans hello le script suivant, nous créons une variable *$image* toostore plus d’informations sur l’utilisation d’une image personnalisée hello [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) puis nous les utilisons [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)et spécifiez l’ID de hello à l’aide de hello *$image* variable nous venons de créer. 

script de Hello crée un ordinateur virtuel nommé *myVMfromImage* à partir de notre image personnalisée dans un groupe de ressources nommé *myResourceGroupFromImage* Bonjour *ouest des États-Unis* emplacement.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>Gestion d’image 

Voici quelques exemples de tâches courantes de gestion image et comment toocomplete les à l’aide de PowerShell.

Répertoriez toutes les images par nom.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Supprimez une image. Cet exemple supprime hello image nommée *myOldImage* de hello *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous montré comment créer une image de machine virtuelle. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Exécuter Sysprep et généraliser les machines virtuelles
> * Créer une image personnalisée
> * Créer une machine virtuelle à partir d’une image personnalisée
> * La liste de toutes les images hello dans votre abonnement
> * Supprimer une image

Avance toohello toolearn de didacticiel suivant sur les ordinateurs virtuels comment hautement disponibles.

> [!div class="nextstepaction"]
> [Créer des machines virtuelles hautement disponibles](tutorial-availability-sets.md)



