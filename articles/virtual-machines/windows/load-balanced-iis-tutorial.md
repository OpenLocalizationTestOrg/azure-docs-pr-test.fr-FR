---
title: "aaaTutorial - génération d’une application hautement disponible sur les machines virtuelles Azure | Documents Microsoft"
description: "Découvrez comment toocreate une application hautement disponible et sécurisée entre trois machines virtuelles de Windows avec un équilibrage de charge dans Azure"
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
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>Création d’une application à haute disponibilité avec équilibrage de charge sur des machines virtuelles Windows dans Azure

Dans ce didacticiel, vous créez une application hautement disponible est résilient toomaintenance les événements. application Hello utilise un équilibrage de charge, un ensemble de disponibilité et trois Windows virtual machines virtuelles. Ce didacticiel installe IIS, mais vous pouvez utiliser ce didacticiel toodeploy une infrastructure d’application à l’aide hello les mêmes composants haute disponibilité et les recommandations. 

## <a name="step-1---azure-prerequisites"></a>Étape 1 : Conditions préalables pour Azure

toocomplete ce didacticiel, assurez-vous que vous avez installé hello dernières [Azure PowerShell](/powershell/azure/overview) module.

Tout d’abord, connectez-vous à tooyour abonnement Azure avec hello commande de connexion-AzureRmAccount et suivez hello à l’écran.

```powershell
Login-AzureRmAccount
```

Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. Avant de pouvoir créer d’autres ressources Azure, vous devez toocreate un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` région : 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>Étape 2 : Créer un groupe à haute disponibilité

Les machines virtuelles peuvent être créées sur les domaines de mise à jour et d’erreur logiques. Chaque domaine logique représente une partie du matériel de centre de données Azure hello sous-jacent. Lorsque vous créez deux ou plusieurs machines virtuelles, vos ressources de calcul et de stockage sont réparties sur ces domaines. Cette distribution hello la disponibilité de votre application est assurée si un composant matériel a besoin de maintenance. Les groupes à haute disponibilité permettent de définir ces domaines d’erreur et de mise à jour logiques.

Créez un groupe à haute disponibilité avec la commande [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Hello exemple suivant crée un groupe à haute disponibilité nommée `myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>Étape 3 : Créer un équilibreur de charge

Un équilibrage de charge Azure répartit le trafic sur un ensemble de machines virtuelles définies à l’aide de règles d’équilibrage de charge. Une sonde d’intégrité analyse un port donné sur chaque machine virtuelle et ne distribue le trafic tooan machine virtuelle opérationnelle.

### <a name="create-public-ip-address"></a>Création d’une adresse IP publique

tooaccess votre application sur hello Internet, attribuez un équilibreur de charge toohello d’adresse IP publique. Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Hello exemple suivant crée une adresse IP publique nommée `myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>Créer un équilibreur de charge

Créez une adresse IP frontale avec [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Hello exemple suivant crée une adresse IP de serveur frontal nommée `myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

Créez un pool d’adresses principales avec [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Hello exemple suivant crée un pool d’adresses principales nommé `myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Maintenant, créez équilibrage de charge hello [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Hello exemple suivant crée un équilibreur de charge nommé `myLoadBalancer` à l’aide de hello `myPublicIP` adresse :

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>Créer une sonde d’intégrité

tooallow hello équilibrage toomonitor hello l’état de charge de votre application, vous utilisez une sonde d’intégrité. Sonde d’intégrité Hello dynamiquement ajoute ou supprime des machines virtuelles à partir de la rotation d’équilibrage de charge hello en fonction de leurs contrôles toohealth de réponse. Par défaut, un ordinateur virtuel est supprimé de la distribution d’équilibrage de charge hello après deux défaillances consécutives à des intervalles de 15 secondes.

Créez une sonde d’intégrité avec [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Hello exemple suivant crée une sonde d’intégrité nommée `myHealthProbe` qui analyse chaque machine virtuelle :

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>Créer une règle d’équilibreur de charge

Une règle d’équilibreur de charge est utilisé toodefine comment le trafic est distribué toohello machines virtuelles.

Créez une règle d’équilibreur de charge avec [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Hello exemple suivant crée une règle d’équilibreur de charge nommée `myLoadBalancerRule` et équilibre le trafic sur le port `80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

Mettre à jour d’équilibrage de charge hello [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>Étape 4 - Configuration de la mise en réseau

Chaque machine virtuelle a un ou plusieurs virtuel cartes d’interface réseau (NIC) qui se connectent tooa des réseaux virtuels. Ce réseau virtuel est sécurisé de trafic toofilter selon les règles d’accès définies.

### <a name="create-virtual-network"></a>Création d’un réseau virtuel

Tout d’abord, configurez un sous-réseau avec [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Hello exemple suivant crée un sous-réseau nommé `mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooyour de connectivité réseau tooprovide machines virtuelles, créez un réseau virtuel avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello exemple suivant crée un réseau virtuel nommé `myVnet` avec `mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>Configurer la sécurité réseau

Un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) (NSG) Azure contrôle le trafic entrant et sortant pour une ou plusieurs machines virtuelles. Les règles de groupe de sécurité réseau autorisent ou refusent le trafic réseau sur un port ou une plage de ports spécifique. Ces règles peuvent également inclure un préfixe d’adresse source afin que seul le trafic provenant d’une source prédéfinie puisse communiquer avec une machine virtuelle.

tooallow web tooreach de trafic de votre application, créez une règle de groupe de sécurité réseau avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Hello exemple suivant crée une règle de groupe de sécurité réseau nommée `myNetworkSecurityGroupRule`:

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

Créez un groupe de sécurité réseau avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Hello exemple suivant crée un groupe de sécurité réseau nommé `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

Ajouter un sous-réseau de toohello hello réseau sécurité groupe avec [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

Réseau virtuel de mise à jour hello avec [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>Création de cartes d’interface réseau virtuelles

Charger la fonction équilibrages de la ressource de carte réseau virtuelle hello plutôt que hello VM réel. Hello carte réseau virtuelle est l’équilibrage de charge connecté toohello et puis attaché tooa machine virtuelle.

Créez une carte réseau virtuelle avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hello exemple suivant crée trois cartes réseau virtuelles. (Une carte réseau virtuelle pour chaque ordinateur virtuel que vous créez pour votre application Bonjour suivant les étapes) :


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>Étape 5 : Créer les machines virtuelles

Avec tous les hello sous-jacent des composants en place, vous pouvez désormais créer toorun d’ordinateurs virtuels hautement disponible votre application. 

Obtenir le nom d’utilisateur hello et le mot de passe pour le compte d’administrateur hello sur l’ordinateur virtuel de hello avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Créer des machines virtuelles hello avec [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [AzureRmVMOperatingSystem de jeu](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface ajouter](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), et [AzureRmVM-nouvelle](/powershell/module/azurerm.compute/new-azurermvm). Bonjour à l’exemple suivant crée trois machines virtuelles :

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

Il prend plusieurs minutes toocreate et configurer tous les trois machines virtuelles. Hello sonde d’intégrité d’équilibrage de charge détecte automatiquement lors de l’application hello est en cours d’exécution sur chaque machine virtuelle. Une fois que l’application hello est en cours d’exécution, règle d’équilibrage de charge hello démarre le trafic de toodistribute.

### <a name="install-hello-app"></a>Installer l’application hello 

Les extensions de machine virtuelle Azure sont des tâches de configuration de machine virtuelle tooautomate utilisé, l’installation d’applications et la configuration de système d’exploitation de hello. Hello [extension de script personnalisé pour Windows](./../virtual-machines-windows-extensions-customscript.md) est toorun utilisée n’importe quel script PowerShell sur l’ordinateur virtuel de hello. script de Hello peut être stockée dans le stockage Azure, n’importe quel point de terminaison HTTP accessible, ou incorporé dans la configuration de l’extension hello script personnalisé. Lorsque vous utilisez l’extension de script personnalisé hello, l’agent de machine virtuelle Azure hello gère l’exécution du script hello.

Utilisez [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) extension de script personnalisé tooinstall hello. Hello extension exécute `powershell Add-WindowsFeature Web-Server` serveur Web IIS de hello tooinstall :

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>Test de l'application

Obtenir hello une adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). exemple Hello obtient adresse IP hello `myPublicIP` créé précédemment :

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Entrez l’adresse IP publique de hello dans le navigateur web de tooa. Règle de groupe de sécurité réseau hello en place, le site Web IIS de hello par défaut s’affiche. 

![Site IIS par défaut](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>Étape 6 : Tâches de gestion

Vous devrez peut-être maintenance tooperform sur hello machines virtuelles exécutant votre application, telles que l’installation des mises à jour du système d’exploitation. toodeal avec une augmentation du trafic tooyour application, vous devrez peut-être tooadd des machines virtuelles supplémentaires. Cette section vous montre comment tooremove ou ajouter une machine virtuelle à partir de l’équilibrage de charge hello. 

### <a name="remove-a-vm-from-hello-load-balancer"></a>Supprimer une machine virtuelle à partir de l’équilibrage de charge hello

Supprimer une machine virtuelle à partir du pool d’adresses principales hello en réinitialisant la propriété de LoadBalancerBackendAddressPools hello hello carte d’interface réseau.

Obtenir la carte d’interface réseau hello avec [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Définir la propriété de LoadBalancerBackendAddressPools de hello de carte d’interface réseau hello trop NULL comme valeur de $:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

Mise à jour de la carte d’interface réseau hello :

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>Ajouter un équilibrage de charge de toohello de machine virtuelle

Après une maintenance de la machine virtuelle, ou si vous avez besoin de la capacité de tooexpand, ajout hello carte réseau d’un pool d’adresses principales toohello machine virtuelle d’équilibrage de charge hello.

Obtenir l’équilibrage de charge hello :

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

Ajouter un pool d’adresses principales hello hello charge équilibrage toohello carte d’interface réseau :

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

Mise à jour de la carte d’interface réseau hello :

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Étapes suivantes

Exemples – [Exemples de scripts PowerShell pour Machines virtuelles Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
