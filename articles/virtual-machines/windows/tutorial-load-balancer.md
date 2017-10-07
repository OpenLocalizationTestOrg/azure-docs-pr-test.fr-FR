---
title: "aaaHow tooload équilibrer les machines virtuelles Windows Azure | Documents Microsoft"
description: "Découvrez comment la toouse hello Azure charge équilibrage toocreate une application hautement disponible et sécurisée entre trois machines virtuelles de Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Comment tooload équilibrer les machines virtuelles Windows dans Azure toocreate une application hautement disponible
L’équilibrage de charge offre un niveau plus élevé de disponibilité en répartissant les demandes entrantes sur plusieurs machines virtuelles. Dans ce didacticiel, vous découvrez hello différents composants d’équilibrage de charge Azure hello de distribuer le trafic et fournissant une haute disponibilité. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Crée un équilibrage de charge Azure
> * Créer une sonde d’intégrité d’équilibreur de charge
> * Créer des règles de trafic pour l’équilibrage de charge
> * Utiliser l’Extension de Script personnalisé de hello toocreate un site IIS de base
> * Créer des ordinateurs virtuels et d’attachement d’équilibrage de charge tooa
> * Afficher un équilibrage de charge en action
> * Ajouter et supprimer des machines virtuelles d’un équilibreur de charge

Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module. Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).


## <a name="azure-load-balancer-overview"></a>Vue d’ensemble de l’équilibreur de charge Azure
Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines. Une sonde d’intégrité d’équilibrage de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic tooan machine virtuelle opérationnelle.

Vous définissez une configuration IP frontale qui contient une ou plusieurs adresses IP publiques. Cette configuration IP frontale permet à votre toobe d’applications et d’équilibrage de charge accessible sur Internet de hello. 

Machines virtuelles se connecter tooa équilibrage de charge à l’aide de leur carte réseau virtuelle (NIC). toohello du trafic toodistribute machines virtuelles, un pool d’adresses de serveur principal contient des adresses IP de hello d’équilibrage de charge hello virtuelle (NIC) connectées toohello.

flux de hello toocontrol du trafic, vous définissez des règles d’équilibrage de charge pour les ports et protocoles qui mappent des machines virtuelles de tooyour spécifiques.


## <a name="create-azure-load-balancer"></a>Créer un équilibreur de charge Azure
Cette section décrit en détail comment vous pouvez créer et configurer chaque composant d’équilibrage de charge hello. Avant de créer un équilibreur de charge, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupLoadBalancer* Bonjour *EastUS* emplacement :

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>Créer une adresse IP publique
tooaccess votre application sur hello Internet, vous avez besoin d’une adresse IP publique pour l’équilibrage de charge hello. Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress). Hello exemple suivant crée une adresse IP publique nommée *myPublicIP* Bonjour *myResourceGroupLoadBalancer* groupe de ressources :

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>Créer un équilibrage de charge
Créez une adresse IP frontale avec [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig). Hello exemple suivant crée une adresse IP de serveur frontal nommée *myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

Créez un pool d’adresses principales avec [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig). Hello exemple suivant crée un pool d’adresses principales nommé *myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

Maintenant, créez équilibrage de charge hello [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer). Hello exemple suivant crée un équilibreur de charge nommé *myLoadBalancer* à l’aide de hello *myPublicIP* adresse :

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>Créer une sonde d’intégrité
tooallow hello équilibrage toomonitor hello l’état de charge de votre application, vous utilisez une sonde d’intégrité. Sonde d’intégrité Hello dynamiquement ajoute ou supprime des machines virtuelles à partir de la rotation d’équilibrage de charge hello en fonction de leurs contrôles toohealth de réponse. Par défaut, un ordinateur virtuel est supprimé de la distribution d’équilibrage de charge hello après deux défaillances consécutives à des intervalles de 15 secondes. Vous créez une sonde d’intégrité selon un protocole ou une page de vérification d’intégrité spécifique pour votre application. 

Bonjour à l’exemple suivant crée une sonde TCP. Vous pouvez également créer des sondes HTTP personnalisées pour des contrôles d’intégrité plus affinés. Lorsque vous utilisez une sonde HTTP personnalisée, vous devez créer page vérifier l’intégrité hello, tel que *healthcheck.aspx*. Sonde de Hello doit retourner un **HTTP 200 OK** réponse pour hello charge équilibrage tookeep hello hôte en rotation.

toocreate une sonde d’intégrité TCP, vous utilisez [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig). Hello exemple suivant crée une sonde d’intégrité nommée *myHealthProbe* qui analyse chaque machine virtuelle :

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

Mettre à jour d’équilibrage de charge hello [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>Créer une règle d’équilibreur de charge
Une règle d’équilibreur de charge est utilisé toodefine comment le trafic est distribué toohello machines virtuelles. Vous définissez la configuration IP frontale de hello pour le trafic entrant de hello et hello principal pool tooreceive hello du trafic IP, ainsi que les sources requis hello et port de destination. toomake que seuls les ordinateurs virtuels sains recevoir du trafic, vous définissez également toouse de sonde d’intégrité hello.

Créez une règle d’équilibreur de charge avec [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig). Hello exemple suivant crée une règle d’équilibreur de charge nommée *myLoadBalancerRule* et équilibre le trafic sur le port *80*:

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

Mettre à jour d’équilibrage de charge hello [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>Configurer un réseau virtuel
Avant de déployer des machines virtuelles et tester votre programme d’équilibrage, créer hello prenant en charge des ressources du réseau virtuel. Pour plus d’informations sur les réseaux virtuels, consultez hello [gérer les réseaux virtuels Azure](tutorial-virtual-network.md) didacticiel.

### <a name="create-network-resources"></a>Créer des ressources réseau
Créez un réseau virtuel avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Hello exemple suivant crée un réseau virtuel nommé *myVnet* avec *mySubnet*:

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

Créez une règle de groupe de sécurité réseau avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), puis un groupe de sécurité réseau avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup). Ajouter hello sécurité groupe toohello sous-réseau avec [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) puis mettez à jour de réseau virtuel hello [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork). 

Hello exemple suivant crée une règle de groupe de sécurité réseau nommée *myNetworkSecurityGroup* et l’applique trop*mySubnet*:

```powershell
# Create security rule config
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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

Des cartes d’interface réseau virtuelles sont créées avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Hello exemple suivant crée trois cartes réseau virtuelles. (Une carte réseau virtuelle pour chaque ordinateur virtuel que vous créez pour votre application Bonjour suivant les étapes). Vous pouvez créer des cartes réseau virtuelles supplémentaires et des machines virtuelles à tout moment et ajoutez-les à équilibrage de charge toohello :

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a>Créer des machines virtuelles
tooimprove hello haute disponibilité de votre application, placez vos machines virtuelles dans un ensemble de disponibilité.

Créez un groupe à haute disponibilité avec la commande [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Hello exemple suivant crée un groupe à haute disponibilité nommée *myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

Définir un administrateur de nom d’utilisateur et mot de passe pour les machines virtuelles hello avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Vous pouvez désormais créer VMs hello avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Bonjour à l’exemple suivant crée trois machines virtuelles :

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

Il prend quelques minutes toocreate et configurer tous les trois machines virtuelles.

### <a name="install-iis-with-custom-script-extension"></a>Installer IIS avec l’extension de script personnalisé
Dans un didacticiel précédent sur [comment toocustomize une machine virtuelle Windows](tutorial-automate-vm-deployment.md), vous avez appris comment personnalisation tooautomate avec hello Extension de Script personnalisé pour Windows. Vous pouvez utiliser hello même approche tooinstall et configurer IIS sur vos ordinateurs virtuels.

Utilisez [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Extension de Script personnalisé. Hello extension exécute `powershell Add-WindowsFeature Web-Server` tooinstall hello serveur Web d’IIS, puis hello de mises à jour *Default.htm* page tooshow hello nom d’hôte de hello machine virtuelle :

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a>Tester l’équilibreur de charge
Obtenir hello une adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). exemple Hello obtient adresse IP hello *myPublicIP* créé précédemment :

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

Vous pouvez entrer ensuite des adresse IP publique de hello dans tooa navigateur. site Web de Hello est affichée, notamment le nom d’hôte hello Hello VM cet équilibrage de charge hello distributed tooas trafic Bonjour l’exemple suivant :

![Site web IIS en cours d’exécution](./media/tutorial-load-balancer/running-iis-website.png)

équilibrage de charge toosee hello répartir le trafic entre tous les trois machines virtuelles exécutant votre application, vous pouvez forcer l’actualisation votre navigateur web.


## <a name="add-and-remove-vms"></a>Ajouter et supprimer des machines virtuelles
Vous devrez peut-être maintenance tooperform sur hello machines virtuelles exécutant votre application, telles que l’installation des mises à jour du système d’exploitation. toodeal avec une augmentation du trafic tooyour application, vous devrez peut-être tooadd des machines virtuelles supplémentaires. Cette section vous montre comment tooremove ou ajouter une machine virtuelle à partir de l’équilibrage de charge hello.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Supprimer une machine virtuelle à partir de l’équilibrage de charge hello
Obtenir la carte d’interface réseau hello avec [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), puis ensemble hello *LoadBalancerBackendAddressPools* propriété de hello carte réseau virtuelle trop*$null*. Enfin, mettez à jour de carte réseau virtuelle de hello. :

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

équilibrage de charge toosee hello répartir le trafic entre hello deux autres machines virtuelles exécutant votre application vous pouvez forcer l’actualisation votre navigateur web. Vous pouvez désormais effectuer la maintenance sur hello machine virtuelle, tels que l’installation des mises à jour du système d’exploitation ou d’effectuer un redémarrage de l’ordinateur virtuel.

### <a name="add-a-vm-toohello-load-balancer"></a>Ajouter un équilibrage de charge de toohello de machine virtuelle
Après une maintenance de la machine virtuelle, ou si vous avez besoin de la capacité de tooexpand, définissez hello *LoadBalancerBackendAddressPools* propriété du toohello de carte réseau virtuelle hello *BackendAddressPool* de [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

Obtenir l’équilibrage de charge hello :

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous créé un équilibreur de charge et attaché tooit de machines virtuelles. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Crée un équilibrage de charge Azure
> * Créer une sonde d’intégrité d’équilibreur de charge
> * Créer des règles de trafic pour l’équilibrage de charge
> * Utiliser l’Extension de Script personnalisé de hello toocreate un site IIS de base
> * Créer des ordinateurs virtuels et d’attachement d’équilibrage de charge tooa
> * Afficher un équilibrage de charge en action
> * Ajouter et supprimer des machines virtuelles d’un équilibreur de charge

Avancer toohello toolearn de didacticiel suivant la mise en réseau de la machine virtuelle toomanage.

> [!div class="nextstepaction"]
> [Gérer les machines virtuelles et les réseaux virtuels](./tutorial-virtual-network.md)
