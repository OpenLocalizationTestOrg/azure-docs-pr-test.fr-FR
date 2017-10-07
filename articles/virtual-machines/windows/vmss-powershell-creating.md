---
title: "échelle de machines virtuelles d’aaaCreating définit à l’aide des applets de commande PowerShell | Documents Microsoft"
description: "Prise en main de la création et de la gestion de vos premiers jeux de mise à l’échelle de machine virtuelle Azure à l’aide des applets de commande Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a>Création de jeux de mise à l’échelle de machine virtuelle à l’aide des applets de commande PowerShell
Cet article assiste un exemple de comment toocreate une échelle de machines virtuelles ensemble (mise). Il crée un jeu de mise à l’échelle de trois nœuds, avec la mise en réseau et le stockage associés.

## <a name="first-steps"></a>Premières étapes
Assurez-vous que vous avez installé le module Azure PowerShell plus récent hello, toomake que vous disposez des applets de commande PowerShell hello nécessaires toomaintain et créer des ensembles de la mise à l’échelle.
Passez les outils de ligne de commande toohello [ici](http://aka.ms/webpi-azps) pour hello plus récentes des Modules Azure disponibles.

toofind mise associé à applets de commande, utilisez la chaîne de recherche hello \*mise\*. Par exemple, _gcm *vmss*_

## <a name="creating-a-vmss"></a>Création d’un jeu de mise à l’échelle de machine virtuelle (VMSS)
#### <a name="create-resource-group"></a>Créer un groupe de ressources
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a>Créer la mise en réseau (réseau virtuel / sous-réseau)
#### <a name="subnet-specification"></a>Spécification du sous-réseau
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a>Spécification du réseau virtuel (VNET)
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a>Créer la ressource IP publique tooAllow accès externe
Ce sera lié toohello équilibrage de charge.

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a>Créer un équilibreur de charge
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a>Configurer l’équilibrage de charge
Création de la configuration de Pool d’adresse de serveur principal, ce sera partagé par les cartes d’interface réseau de machines virtuelles de hello hello dans un ensemble d’échelle hello.

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

Définir le Port de la sonde à charge équilibrée de charge, modifier les paramètres de hello en fonction de votre application.

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

Créer un pool NAT entrant pour une connexion directe (pas de charge équilibrée) routé toohello machines virtuelles dans l’échelle de hello définies via hello équilibrage de charge. Cela est toodemonstrate à l’aide du protocole RDP et ne peut pas être nécessaire dans votre application.

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

Créer hello règle d’équilibrage de charge, cet exemple montre charge le port 80 demandes d’équilibrage, à l’aide de paramètres hello des étapes précédentes.

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

Créez l’équilibrage de charge avec la configuration.

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

Vérifiez les paramètres d’équilibrage de charge, vérifiez la charge des configurations de port à charge équilibrée, notez que vous ne verrez pas les règles NAT entrantes jusqu'à ce que hello machines virtuelles dans un ensemble d’échelle hello sont créées.

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a>Configurer et créer hello identiques
Notez que cet infrastructure exemple montre comment tooset de distribuer le trafic web de l’échelle sur un ensemble d’échelle hello mais hello Images de machines virtuelles spécifiées ici n’ont pas tous les services web installés.

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

Lier tooLoad de carte réseau équilibrage et le sous-réseau

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

Créer la configuration du jeu de mise à l’échelle

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

Définir la configuration du jeu de mise à l’échelle

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

Vous venez de créer un ensemble d’échelle hello. Vous pouvez tester la connexion toohello machine virtuelle individuelle à l’aide du protocole RDP dans cet exemple :

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
