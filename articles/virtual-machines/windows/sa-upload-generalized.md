---
title: aaaUpload un toocreate de disque dur virtuel generalize plusieurs machines virtuelles dans Azure | Documents Microsoft
description: "Télécharger un généralisée toocreate VHD tooan stockage Azure compte un toouse machine virtuelle Windows avec le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>Télécharger un toocreate de tooAzure de disque dur virtuel généralisé une nouvelle machine virtuelle

Cette rubrique décrit le téléchargement d’un compte de stockage de disque non managé généralisé tooa, puis en créant une nouvelle machine virtuelle à l’aide du disque de hello téléchargé. Toutes les informations de votre compte personnel sont supprimées d’une image de disque dur virtuel généralisé à l’aide de Sysprep. 

Si vous souhaitez toocreate une machine virtuelle à partir d’un disque dur virtuel spécialisée dans un compte de stockage, consultez [créer une machine virtuelle à partir d’un disque dur virtuel spécialisé](sa-create-vm-specialized.md).

Cette rubrique couvre l’utilisation de comptes de stockage, mais nous vous recommandons des clients déplacent des disques gérés toousing à la place. Pour une procédure pas à pas complète tooprepare, télécharger et créer une nouvelle machine virtuelle en utilisant des disques gérés, consultez [créer une machine virtuelle à partir d’un tooAzure de disque dur virtuel téléchargé généralisé à l’aide de disques gérés](upload-generalized-managed.md).



## <a name="prepare-hello-vm"></a>Préparer hello machine virtuelle

Toutes les informations de votre compte personnel sont supprimées d’un disque dur virtuel généralisé à l’aide de Sysprep. Si vous envisagez de toouse hello disque dur virtuel en tant qu’une image de toocreate nouvelles machines virtuelles à partir de, vous devez :
  
  * [Préparer un tooAzure tooupload de disque dur virtuel Windows](prepare-for-upload-vhd-image.md). 
  * Généraliser l’ordinateur virtuel de hello à l’aide de Sysprep

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Généraliser une machine virtuelle Windows avec Sysprep
Cette section vous montre comment toogeneralize votre machine virtuelle de Windows pour une utilisation en tant qu’image. Sysprep supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image. Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Assurez-vous que les rôles de serveur hello en cours d’exécution sur l’ordinateur de hello sont pris en charge par Sysprep. Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Si vous exécutez Sysprep avant de télécharger votre tooAzure de disque dur virtuel pour hello première fois, vérifiez que vous disposez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep. 
> 
> 

1. Se connecter toohello machine virtuelle Windows.
2. Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur. Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.
3. Bonjour **outil de préparation système** boîte de dialogue, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et assurez-vous que hello **Generalize** case à cocher est activée.
4. Dans **Options d’arrêt**, sélectionnez **Arrêter**.
5. Cliquez sur **OK**.
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Quand Sysprep se termine, il arrête de machine virtuelle de hello. 

> [!IMPORTANT]
> Ne redémarrez pas hello machine virtuelle jusqu'à ce que vous avez terminé tooAzure de disque dur virtuel hello téléchargement ou de la création d’une image à partir de la machine virtuelle de hello. Si hello VM obtient accidentellement redémarré, exécutez Sysprep toogeneralize nouveau.
> 
> 


## <a name="upload-hello-vhd"></a>Télécharger hello disque dur virtuel

Téléchargez le compte de stockage Azure tooan hello disque dur virtuel.

### <a name="log-in-tooazure"></a>Connectez-vous à tooAzure
Si vous n’avez pas encore PowerShell version 1.4 ou version ultérieure installé, lire [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

1. Ouvrez Azure PowerShell et connectez-vous à tooyour compte Azure. Une fenêtre contextuelle s’ouvre pour vous tooenter vos informations d’identification de compte Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Obtenir l’ID d’abonnement hello pour vos abonnements disponibles.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Définir l’abonnement approprié de hello à l’aide des ID d’abonnement hello. Remplacez `<subscriptionID>` avec l’ID de hello Hello corriger l’abonnement.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a>Obtenir le compte de stockage hello
Vous avez besoin d’un compte de stockage dans l’image de machine virtuelle Azure toostore hello téléchargé. Vous pouvez utiliser un compte de stockage existant ou en créer un. 

comptes de stockage disponibles hello tooshow, tapez :

```powershell
Get-AzureRmStorageAccount
```

Si vous voulez toouse un compte de stockage existant, passez toohello [image de machine virtuelle téléchargement hello](#upload-the-vm-vhd-to-your-storage-account) section.

Si vous avez besoin de toocreate un compte de stockage, procédez comme suit :

1. Vous devez nom hello hello du groupe de ressources où le compte de stockage hello doit être créé. toofind tous les groupes de ressources hello qui se trouvent dans votre abonnement, type :
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate un groupe de ressources nommé **myResourceGroup** Bonjour **ouest des États-Unis** région, tapez :

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Créer un compte de stockage nommé **mystorageaccount** dans ce groupe de ressources à l’aide de hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) applet de commande :
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a>Démarrer le téléchargement de hello 

Hello d’utilisation [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) conteneur tooa d’images de hello tooupload applet de commande dans votre compte de stockage. Cet exemple montre comment les téléchargements hello fichier **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa compte de stockage nommé **mystorageaccount** Bonjour **myResourceGroup** groupe de ressources. fichier de Hello est placé dans le conteneur hello nommé **mycontainer** et nouveau nom de fichier hello seront **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
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

Cette commande peut prendre du temps en fonction de votre connexion réseau et la taille de hello de votre fichier de disque dur virtuel, toocomplete.


## <a name="create-a-new-vm"></a>Créer une machine virtuelle 

Vous pouvez maintenant utiliser hello téléchargé toocreate de disque dur virtuel une machine virtuelle. 

### <a name="set-hello-uri-of-hello-vhd"></a>Ensemble hello URI de disque dur virtuel de hello

Hello URI pour toouse de disque dur virtuel hello est au format de hello : https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd. Dans cet exemple hello disque dur virtuel nommé **myVHD** est dans un compte de stockage hello **mystorageaccount** dans le conteneur de hello **mycontainer**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Créez un réseau virtuel
Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

1. Créer un sous-réseau de hello. Hello exemple suivant crée un sous-réseau nommé **mySubnet** dans le groupe de ressources hello **myResourceGroup** avec un préfixe d’adresse de hello **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Créer un réseau virtuel de hello. Hello exemple suivant crée un réseau virtuel nommé **myVnet** Bonjour **ouest des États-Unis** emplacement avec un préfixe d’adresse de hello **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Création d'une adresse IP publique et une interface réseau
tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.

1. Créez une adresse IP publique. Cet exemple crée une adresse IP publique nommée **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Créer la carte de réseau hello. Cet exemple crée une carte réseau nommée **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Créer une règle RDP et groupe de sécurité réseau hello
toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité qui autorise l’accès RDP sur le port 3389. 

Cet exemple crée un groupe de sécurité réseau nommé **myNsg** qui contient une règle nommée **myRdpRule** autorisant le trafic RDP sur le port 3389. Pour plus d’informations sur les groupes de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Créez une variable pour le réseau virtuel de hello
Créez une variable pour le réseau virtuel de hello s’est terminée. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Créer hello machine virtuelle
Hello script PowerShell suivant montre comment tooset les configurations d’ordinateur virtuel hello et utilisez hello téléchargé l’image de machine virtuelle en tant que source de hello pour une nouvelle installation de hello.



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a>Vérifiez que hello que machine virtuelle a été créée.
Lorsque vous avez terminé, vous devez voir hello nouvellement créé VM dans hello [portail Azure](https://portal.azure.com) sous **Parcourir** > **virtuels**, ou en utilisant hello Commandes PowerShell :

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Étapes suivantes
reportez-vous à votre nouvelle machine virtuelle avec Azure PowerShell, toomanage [gérer des ordinateurs virtuels à l’aide du Gestionnaire de ressources Azure et PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


