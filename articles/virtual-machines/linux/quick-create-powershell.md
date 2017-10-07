---
title: "aaaAzure démarrage rapide : créer un PowerShell VM | Documents Microsoft"
description: "Apprenez rapidement à toocreate un les ordinateurs virtuels Linux avec PowerShell"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a>Créer une machine virtuelle Linux avec PowerShell

module d’Azure PowerShell Hello est toocreate utilisé et gérer des ressources Azure à partir de la ligne de commande PowerShell hello ou dans des scripts. Ce guide décrit en détail à l’aide de hello Azure PowerShell module toodeploy une machine virtuelle exécutant Ubuntu server. Une fois que le serveur de hello est déployé, une connexion SSH est créée, et un serveur Web NGINX est installé.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

Ce démarrage rapide nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).

Enfin, une clé SSH publique avec le nom de hello *id_rsa.pub* doit toobe stockée Bonjour *.ssh* répertoire de votre profil utilisateur Windows. Pour plus d’informations sur la création de clés SSH pour Azure, consultez [Création de clés SSH pour Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Connectez-vous à tooyour abonnement Azure avec hello `Login-AzureRmAccount` commande et suivez hello à l’écran.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Créer un groupe de ressources

Créez un groupe de ressources Azure avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a>Création de ressources de mise en réseau

Créez un réseau virtuel, un sous-réseau et une adresse IP publique. Ces ressources tooprovide utilisés de connectivité réseau toohello l’ordinateur virtuel et le connecter toohello internet.

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

Créez un groupe de sécurité réseau et une règle de groupe de sécurité réseau. groupe de sécurité réseau Hello sécurise la machine virtuelle de hello à l’aide des règles de trafic entrants et sortants. Dans ce cas, une règle entrante est créée pour le port 22, qui autorise les connexions SSH. Nous souhaitons également toocreate une règle de trafic entrant pour le port 80, qui autorise le trafic web entrant.

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

Créer une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) pour la machine virtuelle de hello. carte réseau de Hello connecte le sous-réseau de tooa d’ordinateurs virtuels hello, groupe de sécurité réseau et adresse IP publique.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Create virtual machine

Créez une configuration de machine virtuelle. Cette configuration inclut des paramètres hello sont utilisées lors du déploiement d’ordinateur virtuel de hello comme une configuration de machine virtuelle image, la taille et l’authentification.

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

Créer la machine virtuelle hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Connecter toovirtual machine

Après la fin du déploiement de hello, créez une connexion SSH avec l’ordinateur virtuel de hello.

Hello d’utilisation [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) commande tooreturn hello adresse IP publique de l’ordinateur virtuel de hello.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

À partir d’un système avec SSH installé, suivant de hello utilisé la commande tooconnect toohello virtual machine. Si vous travaillez sur Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) peut être utilisé toocreate hello connexion. 

```bash 
ssh <Public IP Address>
```

Lorsque vous y êtes invité, nom d’utilisateur hello est *azureuser*. Si un mot de passe a été entré lors de la création de clés SSH, vous devez tooenter ce également.


## <a name="install-nginx"></a>Installer NGINX

Suivante de hello utilisez bash sources de package tooupdate de script et installer le dernier package de NGINX hello. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a>Page d’accueil de vue hello NGIX

Avec NGINX installé et le port 80 maintenant ouvrir sur votre machine virtuelle à partir de hello Internet, vous pouvez utiliser un navigateur web de votre choix tooview hello par défaut NGINX page d’accueil. Être vraiment toouse hello adresse IP publique vous documenté au-dessus de la page par défaut toovisit hello. 

![Site par défaut NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Supprimer des ressources

Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web. toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Linux.

> [!div class="nextstepaction"]
> [Didacticiels sur les machines virtuelles Azure Linux](./tutorial-manage-vm.md)
