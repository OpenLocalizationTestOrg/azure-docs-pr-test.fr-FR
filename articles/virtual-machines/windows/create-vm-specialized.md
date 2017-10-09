---
title: "aaaCreate une machine virtuelle de Windows à partir d’un disque dur virtuel spécialisé dans Azure | Documents Microsoft"
description: "Créez une machine virtuelle Windows en attachant un disque spécialisé de géré en tant que disque de système d’exploitation hello à l’aide dans le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Créer une machine virtuelle Windows à partir d’un disque spécialisé

Créer une machine virtuelle en attachant un disque spécialisé de géré en tant que disque de système d’exploitation hello à l’aide de Powershell. Un disque spécialisé est une copie du disque dur virtuel (VHD) à partir d’une machine virtuelle existante qui gère les comptes d’utilisateur hello, applications et autres données d’état à partir de votre machine virtuelle d’origine. 

Lorsque vous utilisez un toocreate de disque dur virtuel une machine virtuelle spécialisée, hello nouvelle machine virtuelle conserve le nom de l’ordinateur de hello hello ordinateur virtuel d’origine. D’autres informations spécifiques de l’ordinateur sont également conservées et, dans certains cas, ces informations en double pourraient entraîner des problèmes. Lors de la copie d’une machine virtuelle, vous devez connaître les types d’informations spécifiques de l’ordinateur dont vos applications dépendent.

Deux options s'offrent à vous :
* [Charger un disque dur virtuel](#option-1-upload-a-specialized-vhd)
* [Copier une machine virtuelle Azure existante](#option-2-copy-an-existing-azure-vm)

Cette rubrique vous montre comment toouse des disques gérés. Si vous avez un déploiement hérité qui requiert l’utilisation d’un compte de stockage, voir [Créer une machine virtuelle à partir d’un disque dur virtuel spécialisé dans un compte de stockage](sa-create-vm-specialized.md).

## <a name="before-you-begin"></a>Avant de commencer
Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Option 1 : Charger un disque dur virtuel spécialisé

Vous pouvez télécharger hello que disque dur virtuel à partir d’une machine virtuelle spécialisée créé avec un outil de virtualisation sur site, telles que Hyper-V ou un ordinateur virtuel exporté à partir d’un autre cloud.

### <a name="prepare-hello-vm"></a>Préparer hello machine virtuelle
Si vous avez l’intention toouse hello du disque dur virtuel en tant que-est toocreate un nouvel ordinateur virtuel, vérifiez hello suivant étapes est terminée. 
  
  * [Préparer un tooAzure tooupload de disque dur virtuel Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Ne le faites pas** généraliser hello machine virtuelle à l’aide de Sysprep.
  * Supprimer les outils de virtualisation invité et les agents installés sur hello machine virtuelle (par exemple, les outils VMware).
  * Assurez-vous de hello machine virtuelle est configurée toopull son adresse IP et les paramètres DNS via DHCP. Cela garantit que ce serveur hello Obtient une adresse IP dans le réseau virtuel de hello lors de son démarrage. 


### <a name="get-hello-storage-account"></a>Obtenir le compte de stockage hello
Vous avez besoin d’un stockage compte dans Azure toostore hello téléchargé le disque dur virtuel. Vous pouvez utiliser un compte de stockage existant ou en créer un. 

comptes de stockage disponibles hello tooshow, tapez :

```powershell
Get-AzureRmStorageAccount
```

Si vous voulez toouse un compte de stockage existant, passez toohello [téléchargement hello VHD](#upload-the-vhd-to-your-storage-account) section.

Si vous avez besoin de toocreate un compte de stockage, procédez comme suit :

1. Vous devez nom hello hello du groupe de ressources où le compte de stockage hello doit être créé. toofind tous les groupes de ressources hello qui se trouvent dans votre abonnement, type :
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate un groupe de ressources nommé *myResourceGroup* Bonjour *ouest des États-Unis* région, tapez :

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Créer un compte de stockage nommé *mystorageaccount* dans ce groupe de ressources à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande :
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Télécharger le compte de stockage tooyour hello disque dur virtuel 
Hello d’utilisation [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) conteneur applet de commande tooupload hello VHD tooa dans votre compte de stockage. Cet exemple montre comment les téléchargements hello fichier *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa compte de stockage nommé *mystorageaccount* Bonjour *myResourceGroup* groupe de ressources. fichier de Hello est stocké dans le conteneur hello nommé *mycontainer* et nouveau nom de fichier hello seront *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


En cas de réussite, vous obtenez une réponse qui recherche toothis similaire :

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

Selon votre connexion réseau et la taille de hello de votre fichier de disque dur virtuel, cette commande peut prendre un certain temps toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Créer un disque de managé à partir de hello disque dur virtuel

Créer un disque de managé à partir de hello spécialisé de disque dur virtuel dans votre compte de stockage à l’aide de [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). Cet exemple utilise **myOSDisk1** pour le nom du disque hello, place hello disque dans *StandardLRS* de stockage et utilise *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* comme hello URI pour le disque dur virtuel de la source hello.

Créer un groupe de ressources pour hello nouvelle machine virtuelle.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Créer nouveau disque de système d’exploitation hello de hello téléchargé le disque dur virtuel. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Option 2 : Copier une machine virtuelle Azure existante

Vous pouvez créer une copie d’une machine virtuelle qu’utilise des disques gérés par une capture instantanée de hello machine virtuelle, puis à l’aide de ce toocreate instantané un nouveau gérés disque et une nouvelle machine virtuelle.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Prenez un instantané du disque du système d’exploitation hello

Vous pouvez prendre une capture instantanée d’une machine virtuelle entière (y compris tous les disques) ou d’un seul disque. Hello étapes suivantes vous montrent comment une capture instantanée du disque juste de hello du système d’exploitation de votre machine virtuelle à l’aide de tootake hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) applet de commande. 

Définissez certains paramètres. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Obtenir l’objet d’ordinateur virtuel hello.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Obtenir le nom du disque hello du système d’exploitation.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Créer la configuration de capture instantanée hello. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Prendre un instantané hello.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Si vous envisagez toouse hello instantané toocreate une machine virtuelle qui doit toobe hautement performants, utilisez le paramètre hello `-AccountType Premium_LRS` avec la commande hello AzureRmSnapshot de nouveau. paramètre Hello crée l’instantané d’hello afin qu’il est stocké comme disque Premium gérés. Les disques gérés Premium sont plus chers que les disques gérés Standard. Veillez à ce que vous avez vraiment besoin Premium avant d’utiliser le paramètre hello.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Créer un nouveau disque à partir de l’instantané d’hello

Créer un disque géré à partir de hello à l’aide de la capture instantanée [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). Cet exemple utilise *myOSDisk* pour le nom du disque hello.

Créer un groupe de ressources pour hello nouvelle machine virtuelle.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Définissez le nom du disque hello du système d’exploitation. 

```powershell
$osDiskName = 'myOsDisk'
```

Créer un disque géré de hello.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Créer hello nouvelle machine virtuelle 

Créer la mise en réseau et autres toobe de ressources de machine virtuelle utilisée par hello nouvelle machine virtuelle.

### <a name="create-hello-subnet-and-vnet"></a>Créer le réseau virtuel et le sous-réseau de hello

Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

Créer un sous-réseau de hello. Cet exemple crée un sous-réseau nommé **mySubNet**, dans le groupe de ressources hello **myDestinationResourceGroup**, et les jeux de hello préfixe d’adresse de sous-réseau trop**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Créer un réseau virtuel de hello. Cet exemple définit hello toobe de nom de réseau virtuel **myVnetName**, hello emplacement trop**ouest des États-Unis**, et hello trop de préfixe d’adresse de réseau virtuel de hello**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Créer une règle RDP et groupe de sécurité réseau hello
toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité qui autorise l’accès RDP sur le port 3389. Étant donné que hello du disque dur virtuel pour hello nouvelle machine virtuelle a été créé à partir d’un ordinateur virtuel de spécialisé existant, vous pouvez utiliser un compte d’ordinateur virtuel de source hello pour RDP.

Cet exemple définit hello nom du groupe de sécurité réseau trop**myNsg** et nom de la règle hello RDP trop**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Pour plus d’informations sur les points de terminaison et les règles du groupe de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Créer une adresse IP publique et une carte réseau
tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.

Créer l’adresse IP publique hello. Dans cet exemple, le nom d’adresse IP publique hello est défini trop**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Créer la carte de réseau hello. Dans cet exemple, le nom de carte réseau hello est défini trop**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Nom d’ordinateur virtuel hello et la taille

Cet exemple définit hello nom d’ordinateur virtuel trop*myVM* et la taille de machine virtuelle de hello trop*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Ajouter hello NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Ajouter le disque de hello du système d’exploitation 

Ajouter à l’aide de hello du système d’exploitation disque toohello configuration [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk). Cet exemple définit taille hello du disque de hello trop*128 Go* et attache le disque hello managé comme un *Windows* disque de système d’exploitation.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Machine virtuelle de hello terminée 

Créer à l’aide de machine virtuelle hello [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello les configurations que nous venons de créer.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Si la commande a été exécutée avec succès, vous obtiendrez une sortie similaire à celle-ci :

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Vérifiez que hello que machine virtuelle a été créée.
Vous devez voir hello nouvellement créées VM dans hello [portail Azure](https://portal.azure.com), sous **Parcourir** > **virtuels**, ou à l’aide de hello suivant PowerShell commandes :

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Étapes suivantes
toosign dans tooyour nouvel ordinateur virtuel, parcourir toohello VM Bonjour [portal](https://portal.azure.com), cliquez sur **connexion**et le fichier de bureau à distance ouverte hello. Utilisez les informations d’identification du compte de hello de votre toosign d’ordinateur virtuel d’origine dans la machine virtuelle tooyour. Pour plus d’informations, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md).

