---
title: "aaaAzure réseaux virtuels et des Machines virtuelles Windows | Documents Microsoft"
description: "Didacticiel : Gérer des réseaux virtuels Azure et des machines virtuelles Windows avec Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Gérer des réseaux virtuels Azure et des machines virtuelles Windows avec Azure PowerShell

Les machines virtuelles Azure utilisent la gestion réseau Azure pour la communication réseau interne et externe. Dans ce didacticiel, vous apprendrez à créer plusieurs machines virtuelles dans un réseau virtuel et à configurer leur connectivité réseau. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créez un réseau virtuel
> * Créer des sous-réseaux de réseau virtuel
> * Contrôler le trafic réseau avec les groupes de sécurité réseau
> * Afficher les règles de trafic en action

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>Créer un réseau virtuel

Un réseau virtuel est une représentation de votre propre réseau dans le cloud de hello. Un réseau virtuel est une isolation logique de hello Azure cloud dédié tooyour abonnement. Au sein d’un réseau virtuel, vous trouverez des sous-réseaux, les règles pour les sous-réseaux toothose de connectivité et des connexions à partir des sous-réseaux toohello hello machines virtuelles.

Avant de pouvoir créer d’autres ressources Azure, vous devez toocreate un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello exemple suivant crée un groupe de ressources nommé *myRGNetwork* Bonjour *EastUS* emplacement :

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Un sous-réseau est une ressource enfant d’un réseau virtuel, et permet de définir des segments d’espaces d’adressage dans un bloc CIDR, à l’aide de préfixes d’adresses IP. Cartes réseau peut être ajoutés toosubnets et tooVMs connecté, en offrant une connectivité pour différentes charges de travail.

Créez un sous-réseau avec [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) :

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Créez un réseau virtuel nommé *myVNet* en utilisant *myFrontendSubnet* avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) :

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Créer une machine virtuelle frontale

Pour une machine virtuelle toocommunicate dans un réseau virtuel, il a besoin d’une interface réseau virtuelle (NIC). Hello *myFrontendVM* est accessible à partir de hello internet, par conséquent, il doit également une adresse IP publique. 

Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) :

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Créez une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) :


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Définir le nom d’utilisateur hello et un mot de passe nécessaire pour le compte d’administrateur hello hello machine virtuelle avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Créer des machines virtuelles hello avec [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [AzureRmVMOperatingSystem de jeu](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface ajouter](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), et [AzureRmVM-nouvelle](/powershell/module/azurerm.compute/new-azurermvm). 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a>Installer le serveur web

Vous pouvez installer IIS sur *myFrontendVM* à partir d’une session Bureau à distance. Vous devez tooget hello adresse IP publique de hello VM tooaccess il.

Vous pouvez obtenir d’adresse IP publique de hello de *myFrontendVM* avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). exemple Hello obtient adresse IP hello *myPublicIPAddress* créé précédemment :

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Notez cette adresse IP : vous en aurez besoin lors des étapes suivantes.

Suivant de hello utilisez commande toocreate une session Bureau à distance avec *myFrontendVM*. Remplacez  *<publicIPAddress>*  avec l’adresse hello que vous avez enregistrée précédemment. Lorsque vous y êtes invité, entrez les informations d’identification de l’hello utilisées lors de la création de hello machine virtuelle.

```
mstsc /v:<publicIpAddress>
``` 

Maintenant que vous avez ouvert une session trop*myFrontendVM*, vous pouvez utiliser une seule ligne de PowerShell tooinstall IIS et activer le trafic web tooallow hello pare-feu local règle. Ouvrez une invite de PowerShell et exécutez hello de commande suivante :

Utilisez [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) extension de script personnalisé hello toorun qui installe le serveur Web IIS de hello :

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Vous pouvez désormais utiliser hello publique IP adresse toobrowse toohello VM toosee hello site IIS.

![Site IIS par défaut](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Gérer le trafic interne

Un groupe de sécurité réseau (NSG) contient une liste de règles de sécurité qui autorisent ou refusent tooa tooresources connecté de trafic réseau réseau virtuel. Groupes de sécurité réseau peuvent être associé à toosubnets ou des cartes réseau attachée tooVMs. Ouvrir ou de fermer tooVMs accès via des ports s’effectue à l’aide de règles de groupe de sécurité réseau. Quand vous avez créé *myFrontendVM*, le port d’entrée 3389 a été automatiquement ouvert pour la connectivité RDP.

La communication interne des machines virtuelles peut être configurée à l’aide d’un groupe de sécurité réseau. Dans cette section, vous apprendrez comment toocreate un sous-réseau supplémentaire Bonjour réseau et affecter un tooallow tooit de groupe de sécurité réseau à une connexion à partir de *myFrontendVM* trop*myBackendVM* sur le port 1433. sous-réseau de Hello est ensuite assigné toohello machine virtuelle lors de sa création.

Vous pouvez limiter le trafic interne trop*myBackendVM* depuis une seule *myFrontendVM* en créant un groupe de sécurité réseau pour le sous-réseau principal de hello. Hello exemple suivant crée une règle de groupe de sécurité réseau nommée *myBackendNSGRule* avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

Ajoutez un groupe de sécurité réseau nommé *myBackendNSG* avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) :

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Ajouter un sous-réseau principal

Ajouter *myBackEndSubnet* trop*myVNet* avec [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a>Créer une machine virtuelle principale

hello toocreate moyen plus simple de Hello machine virtuelle de serveur principal est à l’aide d’une image de SQL Server. Ce didacticiel crée hello machine virtuelle avec le serveur de base de données hello uniquement, mais ne fournit pas d’informations sur l’accès à la base de données hello.

Créez *myBackendNic* :

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Définir le nom d’utilisateur hello et le mot de passe de compte d’administrateur hello hello machine virtuelle avec Get-Credential :

```powershell
$cred = Get-Credential
```

Créez *myBackendVM* :

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

image Hello utilisée a SQL Server est installé, mais n’est pas utilisé dans ce didacticiel. Il est inclus tooshow vous comment vous pouvez configurer de trafic web toohandle de machine virtuelle et une gestion de base de données de machine virtuelle toohandle.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous créé et sécurisé de réseaux Azure en tant que machines de toovirtual connexes. 

> [!div class="checklist"]
> * Créez un réseau virtuel
> * Créer des sous-réseaux de réseau virtuel
> * Contrôler le trafic réseau avec les groupes de sécurité réseau
> * Afficher les règles de trafic en action

Avance toohello toolearn de didacticiel suivant sur l’analyse de protection des données sur des machines virtuelles à l’aide de la sauvegarde Azure. .

> [!div class="nextstepaction"]
> [Sauvegarde de machines virtuelles Windows dans Azure](./tutorial-backup-vms.md)
