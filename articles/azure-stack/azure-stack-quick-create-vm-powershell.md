---
title: "aaaCreate machine virtuelle Windows à l’aide de PowerShell dans la pile de Azure | Documents Microsoft"
description: "Créer une machine virtuelle Windows à l’aide de PowerShell dans Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: de063eae6f0782d8916da991f285a9de6b41def4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a>Créer une machine virtuelle Windows à l’aide de PowerShell dans Azure Stack

Machines virtuelles dans donnent Azure pile hello flexibilité de la virtualisation sans avoir toobuy et de mettre à jour hello matériel physique qui l’exécute. Lorsque vous utilisez des Machines virtuelles, comprenez qu’il existe des différences entre les fonctionnalités de hello qui sont disponibles dans Azure et de la pile d’Azure, consultez le toohello [considérations relatives à des machines virtuelles dans Azure pile](azure-stack-vm-considerations.md) toolearn rubrique sur Ces différences. 

Ce guide des détails à l’aide de PowerShell toocreate machine virtuelle Windows Server 2016 dans la pile de Azure. Vous pouvez exécuter des étapes de hello décrits dans cet article hello Kit de développement Azure pile ou d’un client externe basé sur Windows, si vous êtes connecté via VPN. 

## <a name="prerequisites"></a>Composants requis

1. marketplace d’Azure pile Hello ne contient pas les images hello Windows Server 2016 par défaut. Par conséquent, avant de pouvoir créer un ordinateur virtuel, assurez-vous que cet opérateur de pile de Azure hello [ajoute marketplace d’Azure pile hello Windows Server 2016 image toohello](azure-stack-add-default-image.md). 
2. Pile Azure nécessite une version spécifique du toocreate du module Azure PowerShell et gérer les ressources de hello. Utilisez les étapes hello décrites dans [installer PowerShell pour Azure pile](azure-stack-powershell-install.md) version requise de rubrique tooinstall hello.
3. [Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Un groupe de ressources est un conteneur logique dans lequel les ressources Azure Stack sont déployées et gérées. Utilisez hello suivant le bloc de code toocreate un groupe de ressources. Nous avons affecté des valeurs à toutes les variables de ce document. Vous pouvez les utiliser en l’état ou affecter une valeur différente.  

```powershell
# Create variables toostore hello location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a>Créer des ressources de stockage 

Créer un compte de stockage et une image de stockage conteneur toostore hello Windows Server 2016.

```powershell
# Create variables toostore hello storage account name and hello storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container toostore hello virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a>Création de ressources de mise en réseau

Créez un réseau virtuel, un sous-réseau et une adresse IP publique. Ces ressources sont utilisées tooprovide réseau connectivité toohello virtual machine.  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Créez un groupe de sécurité réseau et une règle de groupe de sécurité réseau

groupe de sécurité réseau Hello sécurise hello virtuels à l’aide de règles de trafic entrants et sortants. Permet de créer une règle de trafic entrant pour le port 3389 tooallow Bureau à distance les connexions entrantes et une règle de trafic entrant pour le trafic web entrant port 80 tooallow.

```powershell
# Create an inbound network security group rule for port 3389
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

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleWWW `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-hello-virtual-machine"></a>Créer une carte réseau pour la machine virtuelle de hello

carte réseau de Hello connecte le sous-réseau de tooa d’ordinateurs virtuels hello, groupe de sécurité réseau et adresse IP publique.

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle

Créez une configuration de machine virtuelle. configuration de Hello inclut des paramètres hello sont utilisées lors du déploiement d’ordinateur virtuel de hello telles que les informations d’identification, de la taille, de l’image de machine virtuelle.

```powershell
# Define a credential object toostore hello username and password for hello virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create hello virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets hello operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create hello virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-toohello-virtual-machine"></a>Connecter l’ordinateur virtuel de toohello

Une fois la machine virtuelle de hello est correctement créé, ouvrir une machine virtuelle de bureau à distance connexion toohello du kit de développement hello ou à partir d’un client externe Windows si vous êtes connecté via VPN. tooremote en machine virtuelle hello que vous avez créé à l’étape précédente de hello, vous avez besoin de son adresse IP publique. Exécutez hello suivant commande tooget hello adresse IP publique de l’ordinateur virtuel de hello : 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
La commande suivante de hello utilisation toocreate une session Bureau à distance avec l’ordinateur virtuel de hello. Remplacez l’adresse IP de hello avec l’adresse IP publique hello de votre machine virtuelle. Lorsque vous y êtes invité, entrez le nom d’utilisateur hello et un mot de passe que vous avez utilisé lors de la création d’ordinateur virtuel de hello.

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-hello-virtual-machine"></a>Supprimer la machine virtuelle de hello

Lorsque vous n’est plus nécessaire, utilisez hello suivant commande tooremove hello groupe de ressources qui contient l’ordinateur virtuel de hello et ses ressources connexes :

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a>Étapes suivantes

toolearn sur le stockage dans la pile d’Azure, consultez toohello [vue d’ensemble du stockage](azure-stack-storage-overview.md) rubrique.

