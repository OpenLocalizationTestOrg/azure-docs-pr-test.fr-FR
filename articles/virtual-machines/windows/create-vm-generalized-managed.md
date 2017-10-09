---
title: "aaaCreate machine virtuelle à partir d’une image managée de la machine virtuelle dans Azure | Documents Microsoft"
description: "Créer une machine virtuelle Windows à partir d’une image de machine virtuelle managée généralisée à l’aide d’Azure PowerShell, dans le modèle de déploiement du Gestionnaire de ressources hello."
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Créer une machine virtuelle à partir d’une image gérée

Vous pouvez créer plusieurs machines virtuelles à partir d’une image de machine virtuelle managée dans Azure. Une image de machine virtuelle gérée contient hello informations toocreate nécessaire une machine virtuelle, y compris les disques du système d’exploitation et les données de hello. Hello disques durs virtuels qui composent l’image hello, y compris les disques hello du système d’exploitation et les disques de données, sont stockées en tant que disques gérés. 


## <a name="prerequisites"></a>Composants requis

Vous devez toohave déjà [créé une image de machine virtuelle gérée](capture-image-resource.md) toouse pour la création de hello nouvelle machine virtuelle. 

Assurez-vous que vous disposez des versions les plus récentes des modules de AzureRM.Compute et AzureRM.Network PowerShell hello hello. Ouvrez une invite PowerShell en tant qu’administrateur et exécutez hello suivant commande tooinstall les.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).



## <a name="collect-information-about-hello-image"></a>Collecter des informations sur l’image de hello

Tout d’abord, nous toogather les informations de base sur l’image de hello et créez une variable pour l’image de hello. Cet exemple utilise une image de machine virtuelle gérée nommée **myImage** qui est en hello **myResourceGroup** groupe de ressources dans hello **ouest des États-Unis** emplacement. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Créez un réseau virtuel
Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).

1. Créer un sous-réseau de hello. Cet exemple crée un sous-réseau nommé **mySubnet** avec le préfixe d’adresse de hello **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Créer un réseau virtuel de hello. Cet exemple crée un réseau virtuel nommé **myVnet** avec le préfixe d’adresse de hello **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Création d'une adresse IP publique et une interface réseau

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

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Créer une règle RDP et groupe de sécurité réseau hello

toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité réseau (NSG) qui autorise l’accès RDP sur le port 3389. 

Cet exemple crée un groupe de sécurité réseau nommé **myNsg** qui contient une règle nommée **myRdpRule** autorisant le trafic RDP sur le port 3389. Pour plus d’informations sur les groupes de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Créez une variable pour le réseau virtuel de hello

Créez une variable pour le réseau virtuel de hello s’est terminée. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Obtenir des informations d’identification de hello pour hello machine virtuelle

Hello applet de commande suivante ouvre une fenêtre dans laquelle vous entrerez un toouse nouveau du nom et mot de passe utilisateur en tant que compte d’administrateur local hello pour accéder à distance aux hello machine virtuelle. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Les variables définies pour hello VM name, nom de l’ordinateur et hello taille de machine virtuelle de hello

1. Créer des variables pour nom d’ordinateur virtuel hello et le nom de l’ordinateur. Cet exemple définit le nom de machine virtuelle hello en tant que **myVM** et nom de l’ordinateur en tant que hello **poste de travail**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Définir la taille hello de machine virtuelle de hello. Cet exemple crée une machine virtuelle de taille **Standard_DS1_v2**. Consultez hello [tailles de machine virtuelle](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation pour plus d’informations.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Ajoutez hello nom d’ordinateur virtuel et configuration d’ordinateur virtuel de taille toohello.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Image de machine virtuelle hello ensemble en tant qu’image source pour hello nouvelle machine virtuelle

Définir l’image source de hello à l’aide de code hello d’image de machine virtuelle hello géré.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Définir la configuration du système d’exploitation hello et ajouter de carte réseau de hello.

Entrez le type de stockage de hello (PremiumLRS ou StandardLRS) et la taille de hello du disque du système d’exploitation hello. Cet exemple définit le type de compte hello trop**PremiumLRS**, hello trop de taille de disque**128 Go** et mise en cache disque trop**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Créer hello machine virtuelle

Créer hello nouvelle machine virtuelle à l’aide de la configuration de hello que nous avons généré et stocké dans hello **$vm** variable.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Vérifiez que hello que machine virtuelle a été créée.
Lorsque vous avez terminé, vous devez voir hello nouvellement créé VM dans hello [portail Azure](https://portal.azure.com) sous **Parcourir** > **virtuels**, ou en utilisant hello Commandes PowerShell :

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Étapes suivantes
reportez-vous à votre nouvelle machine virtuelle avec Azure PowerShell, toomanage [créer et gérer des machines virtuelles Windows avec module d’Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

