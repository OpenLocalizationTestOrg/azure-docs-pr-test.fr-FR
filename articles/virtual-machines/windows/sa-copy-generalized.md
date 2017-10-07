---
title: "aaaCreate une image non managée d’une machine virtuelle généralisée dans Azure | Documents Microsoft"
description: "Créer une image non managé d’un toocreate toouse de machine virtuelle Windows généralisée plusieurs copies d’une machine virtuelle dans Azure."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Comment toocreate une machine virtuelle non managée de l’image à partir d’une machine virtuelle Azure

Cet article traite de l’utilisation de comptes de stockage. Nous vous recommandons d’utiliser des disques managés et des images managées plutôt qu’un compte de stockage. Pour plus d’informations, consultez [Capturer une image managée d’une machine virtuelle généralisée dans Azure](capture-image-resource.md).

Cet article vous montre comment toouse Azure PowerShell toocreate une image d’une machine virtuelle Azure généralisé à l’aide d’un compte de stockage. Vous pouvez ensuite utiliser hello image toocreate une autre machine virtuelle. image de Hello inclut le disque du système d’exploitation hello et des disques de données hello toohello joint de l’ordinateur virtuel. image de Hello n’inclut pas les ressources de réseau virtuel hello, donc vous devez tooset ces ressources lorsque vous créez hello nouvelle machine virtuelle. 

## <a name="prerequisites"></a>Composants requis
Vous devez toohave Azure PowerShell version 1.0.x ou version plus récente. Si vous n’avez pas déjà installé PowerShell, lisez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour les étapes d’installation.

## <a name="generalize-hello-vm"></a>Généraliser hello machine virtuelle 
Cette section vous montre comment toogeneralize votre machine virtuelle de Windows pour une utilisation en tant qu’image. La généralisation d’un ordinateur virtuel supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image. Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Assurez-vous que les rôles de serveur hello en cours d’exécution sur l’ordinateur de hello sont pris en charge par Sysprep. Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Si vous téléchargez votre tooAzure de disque dur virtuel pour hello première fois, vérifiez que vous disposez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep. 
> 
> 

Vous pouvez généraliser également un VM Linux à l’aide de `sudo waagent -deprovision+user` , puis utilisez PowerShell toocapture hello machine virtuelle. Pour plus d’informations sur l’utilisation de hello CLI toocapture une machine virtuelle, consultez [comment toogeneralize et une machine virtuelle Linux à l’aide de la capture hello CLI d’Azure ](../linux/capture-image.md).


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

## <a name="log-in-tooazure-powershell"></a>Connectez-vous à tooAzure PowerShell
1. Ouvrez Azure PowerShell et connectez-vous à tooyour compte Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Une fenêtre contextuelle s’ouvre pour vous tooenter vos informations d’identification de compte Azure.
2. Obtenir l’ID d’abonnement hello pour vos abonnements disponibles.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Définir l’abonnement approprié de hello à l’aide des ID d’abonnement hello.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Désallouer hello machine virtuelle et de définir hello état toogeneralized
1. Libérer des ressources d’ordinateur virtuel hello.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Hello *état* pour hello VM Bonjour Azure portal passe de **arrêté** trop**arrêté (désallouée)**.
2. Définir le statut de hello de machine virtuelle de hello trop**généralisé**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Vérifier l’état de hello Hello machine virtuelle. Hello **OSState/généralisés** section hello machine virtuelle doit avoir hello **DisplayStatus** défini trop**généralisé de machine virtuelle**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Création d’image de hello

Créer une image de machine virtuelle non gérée dans le conteneur de stockage de destination hello à l’aide de cette commande. Hello image est créée dans hello même compte de stockage comme hello d’ordinateur virtuel d’origine. Hello `-Path` paramètre enregistre une copie du modèle JSON hello pour ordinateur local du tooyour machine virtuelle source hello. Hello `-DestinationContainerName` paramètre désigne hello conteneur hello que vous souhaitez que toohold vos images. Si le conteneur de hello n’existe pas, il est créé pour vous.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Vous pouvez obtenir hello les URL de votre image de modèle de fichier JSON hello. Accédez toohello **ressources** > **storageProfile** > **osDisk** > **image**  >  **uri** section de chemin d’accès complet de hello de votre image. URL de Hello d’image de hello est similaire à : `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
Vous pouvez également vérifier hello URI dans le portail de hello. image de Hello est conteneur tooa copié nommé **système** dans votre compte de stockage. 

## <a name="create-a-vm-from-hello-image"></a>Créer une machine virtuelle à partir de l’image de hello

Vous pouvez désormais créer un ou plusieurs ordinateurs virtuels à partir de l’image de non managé hello.

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
Hello PowerShell suivant termine les configurations d’ordinateur virtuel hello et non managée image en tant que source de hello pour une nouvelle installation de hello.

</br>

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

### <a name="verify-that-hello-vm-was-created"></a>Vérifiez que hello que machine virtuelle a été créée.
Lorsque vous avez terminé, vous devez voir hello nouvellement créé VM dans hello [portail Azure](https://portal.azure.com) sous **Parcourir** > **virtuels**, ou en utilisant hello Commandes PowerShell :

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Étapes suivantes
reportez-vous à votre nouvelle machine virtuelle avec Azure PowerShell, toomanage [gérer des ordinateurs virtuels à l’aide du Gestionnaire de ressources Azure et PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


