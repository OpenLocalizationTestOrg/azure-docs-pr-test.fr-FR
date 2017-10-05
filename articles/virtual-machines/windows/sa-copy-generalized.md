---
title: "Créer une image non managée d’une machine virtuelle généralisée dans Azure | Microsoft Docs"
description: "Créez une image non managé d’une machine virtuelle Windows généralisée à utiliser pour créer plusieurs copies d’une machine virtuelle dans Azure."
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
ms.openlocfilehash: d7f4a9558175835eba9096e6845726f21c7459d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-unmanaged-vm-image-from-an-azure-vm"></a>Comment créer une image de machine virtuelle non managée à partir d’une machine virtuelle Azure

Cet article traite de l’utilisation de comptes de stockage. Nous vous recommandons d’utiliser des disques managés et des images managées plutôt qu’un compte de stockage. Pour plus d’informations, consultez [Capturer une image managée d’une machine virtuelle généralisée dans Azure](capture-image-resource.md).

Cet article vous montre comment utiliser Azure PowerShell pour créer une image d’une machine virtuelle Azure généralisée à l’aide d’un compte de stockage. Vous pouvez ensuite utiliser l’image pour créer une autre machine virtuelle. L’image comprend le disque du système d’exploitation, ainsi que les disques de données attachés à la machine virtuelle. L’image n’inclut pas les ressources du réseau virtuel. Vous devez donc configurer les ressources lorsque vous créez la nouvelle machine virtuelle. 

## <a name="prerequisites"></a>Composants requis
Vous devez disposer d’une installation d’Azure PowerShell version 1.0.x ou ultérieure. Si vous n’avez pas déjà installé PowerShell, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .

## <a name="generalize-the-vm"></a>Généraliser la machine virtuelle 
Cette section vous montre comment généraliser votre machine virtuelle Windows de façon à l’utiliser comme image. La généralisation d’une machine virtuelle supprime toutes les informations personnelles de votre compte, entre autres, et prépare la machine de façon à pouvoir l’utiliser comme image. Pour plus d’informations sur Sysprep, voir [Introduction à l’utilisation de Sysprep](http://technet.microsoft.com/library/bb457073.aspx).

Vérifiez que les rôles serveur exécutés sur la machine sont pris en charge par Sysprep. Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Si vous chargez votre disque dur virtuel sur Azure pour la première fois, vérifiez que vous avez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep. 
> 
> 

Vous pouvez également généraliser une machine virtuelle Linux à l’aide de `sudo waagent -deprovision+user`, puis utiliser PowerShell pour capturer la machine virtuelle. Pour plus d’informations sur l’utilisation de l’interface de ligne de commande pour capturer une machine virtuelle, consultez [Guide pratique pour généraliser et capturer une machine virtuelle Linux à l’aide de l’interface de ligne de commande Azure](../linux/capture-image.md).


1. Connectez-vous à la machine virtuelle Windows
2. Ouvrez la fenêtre d’invite de commandes en tant qu’administrateur. Remplacez le répertoire par **%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.
3. Dans la boîte de dialogue **Outil de préparation du système**, sélectionnez **Entrer en mode OOBE (Out-of-Box Experience)** et vérifiez que la case **Généraliser** est cochée.
4. Dans **Options d’arrêt**, sélectionnez **Arrêter**.
5. Cliquez sur **OK**.
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Une fois l’opération Sysprep terminée, elle arrête la machine virtuelle. 

> [!IMPORTANT]
> Ne redémarrez pas la machine virtuelle tant que vous n’avez pas terminé de télécharger le disque dur virtuel dans Azure ou de créer une image à partir de la machine virtuelle. Si la machine virtuelle est accidentellement redémarrée, exécutez Sysprep pour la généraliser à nouveau.
> 
> 

## <a name="log-in-to-azure-powershell"></a>Connexion à Azure PowerShell
1. Ouvrez Azure PowerShell et connectez-vous à votre compte Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Une fenêtre contextuelle s’ouvre pour vous permettre d’entrer les informations d’identification de votre compte Azure.
2. Obtenez les ID d’abonnement de vos abonnements disponibles.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Définissez l’abonnement approprié à l’aide de l’ID d’abonnement.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a>Libération de la machine virtuelle et définition de l’état sur généralisé
1. Libérez les ressources de la machine virtuelle.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    *L’état* de la machine virtuelle dans le Portail Azure passe de **Arrêté** à **Arrêté (libéré)**.
2. Définissez l’état de la machine virtuelle sur **Généralisé**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Vérifiez l’état de la machine virtuelle. La section **OSState/généralisé** pour la machine virtuelle doit avoir la valeur de **DisplayStatus** définie sur **Machine virtuelle généralisée**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a>Création de l’image

Créez une image de machine virtuelle non gérée dans le conteneur de stockage de destination à l’aide de cette commande. L’image est créée dans le même compte de stockage que la machine virtuelle d’origine. Le paramètre `-Path` enregistre une copie du modèle JSON pour la machine virtuelle source sur votre ordinateur local. Le paramètre `-DestinationContainerName` est le nom du conteneur dans lequel vous souhaitez stocker vos images. Si le conteneur n’existe pas, il est créé pour vous.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Vous pouvez obtenir l’URL de l’image à partir du modèle de fichier JSON. Accédez à la section **resources** > **storageProfile** > **osDisk** > **image** > **uri** pour obtenir le chemin d’accès complet de votre image. L’URL de l’image ressemble a le format suivant : `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
Vous pouvez également vérifier l’URI dans le portail. L’image est copiée dans un conteneur nommé **system** dans votre compte de stockage. 

## <a name="create-a-vm-from-the-image"></a>Créer une machine virtuelle à partir de l’image

Vous pouvez maintenant créer une ou plusieurs machines virtuelles à partir de l’image non managée.

### <a name="set-the-uri-of-the-vhd"></a>Définir l’URI du disque dur virtuel

L’URI du disque dur virtuel à utiliser est au format : https://**moncomptedestockage**.blob.core.windows.net/**monconteneur**/**mondisquedurvirtuel**.vhd. Dans cet exemple, le disque dur virtuel nommé **mondisquedurvirtuel** se trouve dans le compte de stockage **moncomptedestockage** dans le conteneur **monconteneur**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Créez un réseau virtuel
Créez le réseau virtuel et le sous-réseau du [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

1. Créez le sous-réseau. L’exemple suivant crée un sous-réseau nommé **mySubnet** dans le groupe de ressources **myResourceGroup** avec le préfixe d’adresse **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Création du réseau virtuel. L’exemple suivant crée un réseau virtuel nommé **myVnet** à l’emplacement **Ouest des États-Unis** avec le préfixe d’adresse **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Création d'une adresse IP publique et une interface réseau
Pour établir la communication avec la machine virtuelle dans le réseau virtuel, vous avez besoin d’une [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et d’une interface réseau.

1. Créez une adresse IP publique. Cet exemple crée une adresse IP publique nommée **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Créez la carte réseau. Cet exemple crée une carte réseau nommée **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a>Créer le groupe de sécurité réseau et une règle RDP
Pour pouvoir vous connecter à votre machine virtuelle avec le protocole RDP, vous devez disposer d’une règle de sécurité qui autorise l’accès RDP sur le port 3389. 

Cet exemple crée un groupe de sécurité réseau nommé **myNsg** qui contient une règle nommée **myRdpRule** autorisant le trafic RDP sur le port 3389. Pour plus d’informations sur les groupes de sécurité réseau, consultez [Ouverture de ports sur une machine virtuelle dans Azure avec PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a>Créer une variable pour le réseau virtuel
Créez une variable pour le réseau virtuel terminé. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a>Création de la machine virtuelle
Le script PowerShell suivant effectue les configurations de machine virtuelle et utilise l’image non managée comme source de la nouvelle installation.

</br>

```powershell
    # Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-the-vm-was-created"></a>Vérifier que la machine virtuelle a été créée
Lorsque vous avez terminé, vous devez voir la machine virtuelle nouvellement créée dans le [Portail Azure](https://portal.azure.com) sous **Parcourir** > **Machines virtuelles** ou en utilisant les commandes PowerShell suivantes :

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Étapes suivantes
Pour gérer votre nouvelle machine virtuelle avec Azure PowerShell, consultez [Gestion des machines virtuelles Azure à l’aide de modèles Resource Manager et de PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


