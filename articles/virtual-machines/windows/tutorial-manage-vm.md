---
title: "aaaCreate et gérer des machines virtuelles Windows avec hello module Azure PowerShell | Documents Microsoft"
description: "Didacticiel : créer et gérer des machines virtuelles Windows avec hello module Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>Créer et gérer des machines virtuelles Windows avec hello module Azure PowerShell

Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible. Ce didacticiel traite d’aspects de base du déploiement de machines virtuelles Azure, tels que la sélection d’une taille de machine virtuelle, la sélection d’une image de machine virtuelle et le déploiement d’une machine virtuelle. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer et connecter tooa machine virtuelle
> * Sélectionner et utiliser des images de machine virtuelle
> * Afficher et utiliser des tailles de machine virtuelle spécifiques
> * Redimensionner une machine virtuelle
> * Consulter et comprendre l’état d’une machine virtuelle

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).

## <a name="create-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) commande. 

Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. Un groupe de ressources doit être créé avant les machines virtuelles. Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans hello *EastUS* région. 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

groupe de ressources Hello est spécifié lors de la création ou la modification d’une machine virtuelle, ce qui peut être vu dans ce didacticiel.

## <a name="create-virtual-machine"></a>Create virtual machine

Un ordinateur virtuel doit être connecté tooa des réseaux virtuels. Vous communiquez avec l’ordinateur virtuel de hello à l’aide d’une adresse IP publique via une carte d’interface réseau.

### <a name="create-virtual-network"></a>Création d’un réseau virtuel

Créez un sous-réseau avec [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) :

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

Créez un réseau virtuel avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) :

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>Création d’une adresse IP publique

Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) :

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>Création de la carte réseau

Créez une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) :

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>Création d’un groupe de sécurité réseau

Un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) (NSG) Azure contrôle le trafic entrant et sortant pour une ou plusieurs machines virtuelles. Les règles de groupe de sécurité réseau autorisent ou refusent le trafic réseau sur un port ou une plage de ports spécifique. Ces règles peuvent également inclure un préfixe d’adresse source afin que seul le trafic provenant d’une source prédéfinie puisse communiquer avec une machine virtuelle. tooaccess hello IIS serveur Web que vous installez, vous devez ajouter une règle entrante de groupe de sécurité réseau.

toocreate une règle entrante de groupe de sécurité réseau, utilisez [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig). Hello exemple suivant crée une règle de groupe de sécurité réseau nommée *myNSGRule* qui ouvre le port *3389* pour la machine virtuelle de hello :

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

Créer à l’aide du groupe de sécurité réseau hello *myNSGRule* avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Ajouter un sous-réseau de toohello de groupe de sécurité réseau hello dans le réseau virtuel hello [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

Réseau virtuel de mise à jour hello avec [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Create virtual machine

Lorsque vous créez une machine virtuelle, plusieurs options sont disponibles, comme l’image de système d’exploitation, les informations d’identification d’administration ou le dimensionnement des disques. Dans cet exemple, un ordinateur virtuel est créé avec un nom de *myVM* en cours d’exécution hello dernière version de Windows Server 2016 Datacenter.

Définir le nom d’utilisateur hello et le mot de passe pour le compte d’administrateur hello sur l’ordinateur virtuel de hello avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Créer la configuration initiale de l’ordinateur virtuel hello hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

Ajouter une configuration de machine virtuelle hello système d’exploitation informations toohello avec [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Ajouter la configuration d’ordinateur virtuel hello image informations toohello avec [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

Ajouter hello système d’exploitation disque paramètres toohello configuration d’ordinateur virtuel avec [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

Ajouter hello carte réseau que vous avez créé précédemment toohello configuration d’ordinateur virtuel avec [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Créer la machine virtuelle hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>Se connecter tooVM

Après que le déploiement de hello terminée, créez une connexion Bureau à distance avec l’ordinateur virtuel de hello.

Exécutez hello suivant de commandes tooreturn hello adresse IP publique de l’ordinateur virtuel de hello. Prenez note de cette adresse IP pour pouvoir vous connecter tooit reliées votre navigateur tootest web dans une étape ultérieure.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

La commande suivante de hello utilisation toocreate une session Bureau à distance avec l’ordinateur virtuel de hello. Remplacer l’adresse IP de hello avec hello *publicIPAddress* de votre machine virtuelle. Lorsque vous y êtes invité, entrez les informations d’identification de l’hello utilisées lors de la création d’ordinateur virtuel de hello.

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>Comprendre les images de machine virtuelle

Bonjour Azure marketplace inclut plusieurs images de machine virtuelle qui peuvent être utilisé toocreate un nouvel ordinateur virtuel. Dans les étapes précédentes hello, un ordinateur virtuel a été créé à l’aide d’image de Windows Server 2016-Datacenter hello. Dans cette étape, le module PowerShell de hello est marketplace de hello toosearch utilisé pour les autres images de Windows, qui peut également comme base pour les nouvelles machines virtuelles. Ce processus se compose de recherche de serveur de publication hello, offre et le nom d’image hello (référence Sku). 

Hello d’utilisation [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) commande tooreturn une liste des serveurs de publication de l’image.  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

Hello d’utilisation [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn une liste des offres de l’image. Avec cette commande, hello retourné la liste est filtrée sur le serveur de publication spécifié hello. 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

Hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) commande puis filtre sur tooreturn de nom de serveur de publication et offre hello une liste de noms d’images.

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

Ces informations peuvent être utilisée toodeploy une machine virtuelle avec une image spécifique. Cet exemple définit le nom de l’image hello sur l’objet de machine virtuelle hello. Consultez les exemples précédents toohello dans ce didacticiel pour les étapes de déploiement complet.

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>Comprendre les tailles de machine virtuelle

Une taille de machine virtuelle détermine hello des ressources de calcul tels que le processeur et mémoire GPU apportées virtuels toohello disponibles. Machines virtuelles doivent toobe créé avec une taille appropriée pour hello attendent la charge de travail. Si la charge de travail augmente, une machine virtuelle existante peut être redimensionnée.

### <a name="vm-sizes"></a>Tailles de machine virtuelle

Hello tableau suivant catégorise les tailles en cas d’usage.  

| Type                     | Tailles           |    Description       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Usage général         |DSv2, Dv2, DS, D, Av2, A0-7| Ratio processeur/mémoire équilibré. La solution idéale pour le développement / test et des solutions d’applications et des données toomedium petit.  |
| Optimisé pour le calcul      | Fs, F             | Ratio processeur/mémoire élevé. Convient pour les applications au trafic moyen, les appliances réseau et les processus de traitement par lots.        |
| Mémoire optimisée       | GS, G, DSv2, DS, Dv2, D   | Ratio mémoire/cœur élevé. Idéal pour les bases de données relationnelles, les caches toolarge moyenne et en mémoire analytique.                 |
| Optimisé pour le stockage       | Ls                | Débit de disque et E/S élevés. Idéale pour les bases de données NoSQL, SQL et Big Data.                                                         |
| GPU           | NV, NC            | Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.       |
| Hautes performances | H, A8-11          | Nos machines virtuelles dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA). 


### <a name="find-available-vm-sizes"></a>Rechercher les tailles de machines virtuelles disponibles

toosee une liste des ordinateurs virtuels des tailles disponibles dans une région particulière, utilisez hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) commande.

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>Redimensionner une machine virtuelle

Après avoir déployé une machine virtuelle, il peut être redimensionné tooincrease ou diminuer l’allocation de ressources.

Avant de redimensionner une machine virtuelle, vérifiez si hello taille souhaitée est disponible sur le cluster d’ordinateurs virtuels en cours hello. Hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) commande renvoie une liste de tailles. 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

Si hello souhaité de taille n’est disponible, hello machine virtuelle peut être redimensionnée à partir d’un état sous tension, mais il est redémarré au cours de l’opération de hello.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

Si vous le souhaitez hello taille n’est pas sur le cluster actuel hello, hello VM besoins toobe libérée avant que l’opération de redimensionnement hello peut se produire. Notez que, quand hello VM est sous tension précédent, toutes les données sur le disque temporaire de hello sont supprimées et adresse IP publique de hello modifier, sauf si une adresse IP statique est utilisée. 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>États d’alimentation de la machine virtuelle

Une machine virtuelle Azure peut présenter différents états d’alimentation. Cet état représente état actuel de hello Hello machine virtuelle à partir du point de vue hello de hello hyperviseur. 

### <a name="power-states"></a>États d’alimentation

| État d’alimentation | Description
|----|----|
| Starting | Indique l’ordinateur virtuel de hello est en cours de démarrage. |
| Exécution | Indique que l’ordinateur virtuel hello est en cours d’exécution. |
| En cours d’arrêt | Indique que l’ordinateur virtuel hello est en cours d’arrêt. | 
| Arrêté | Indique que l’ordinateur virtuel hello est arrêté. Notez que les ordinateurs virtuels en état de hello arrêté peut toujours occasionner des frais de calcul.  |
| Libération | Indique que l’ordinateur virtuel hello est désalloué. |
| Libéré | Indique que l’ordinateur virtuel hello est entièrement supprimé du hyperviseur hello mais restent disponibles dans le plan de contrôle hello. Machines virtuelles dans hello désallouée état n’entraînent aucun frais de calcul. |
| - | Indique que l’état de l’alimentation de l’ordinateur virtuel de hello hello est inconnu. |

### <a name="find-power-state"></a>Rechercher un état d’alimentation

état de hello tooretrieve d’un ordinateur virtuel, utilisez hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) commande. Être vraiment toospecify un nom valide pour un ordinateur virtuel et le groupe de ressources. 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

Output:

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>Tâches de gestion

Au cours de hello du cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle. En outre, vous souhaiterez toocreate scripts tooautomate répétitives ou complexes des tâches. À l’aide d’Azure PowerShell, nombreuses tâches courantes de gestion peuvent être exécutées à partir de la ligne de commande hello ou dans des scripts.

### <a name="stop-virtual-machine"></a>Arrêt d’une machine virtuelle

Arrêtez et libérez une machine virtuelle avec [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) :

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

Si vous voulez tookeep hello virtual machine dans un état configuré, utilisez le paramètre de - StayProvisioned de hello.

### <a name="start-virtual-machine"></a>Démarrage d’une machine virtuelle

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>Supprimer un groupe de ressources

La suppression d’un groupe de ressources supprime également toutes les ressources qu’il contient.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous a montré les tâches de base de création et de gestion de machines virtuelles, notamment :

> [!div class="checklist"]
> * Créer et connecter tooa machine virtuelle
> * Sélectionner et utiliser des images de machine virtuelle
> * Afficher et utiliser des tailles de machine virtuelle spécifiques
> * Redimensionner une machine virtuelle
> * Consulter et comprendre l’état d’une machine virtuelle

Avance toohello toolearn de didacticiel suivant sur les disques de machine virtuelle.  

> [!div class="nextstepaction"]
> [Créer et gérer des disques de machine virtuelle](./tutorial-manage-data-disk.md)
