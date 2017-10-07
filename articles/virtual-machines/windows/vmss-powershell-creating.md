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
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="1c5fa-103">Création de jeux de mise à l’échelle de machine virtuelle à l’aide des applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c5fa-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="1c5fa-104">Cet article assiste un exemple de comment toocreate une échelle de machines virtuelles ensemble (mise).</span><span class="sxs-lookup"><span data-stu-id="1c5fa-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="1c5fa-105">Il crée un jeu de mise à l’échelle de trois nœuds, avec la mise en réseau et le stockage associés.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="1c5fa-106">Premières étapes</span><span class="sxs-lookup"><span data-stu-id="1c5fa-106">First Steps</span></span>
<span data-ttu-id="1c5fa-107">Assurez-vous que vous avez installé le module Azure PowerShell plus récent hello, toomake que vous disposez des applets de commande PowerShell hello nécessaires toomaintain et créer des ensembles de la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="1c5fa-108">Passez les outils de ligne de commande toohello [ici](http://aka.ms/webpi-azps) pour hello plus récentes des Modules Azure disponibles.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="1c5fa-109">toofind mise associé à applets de commande, utilisez la chaîne de recherche hello \*mise\*.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="1c5fa-110">Par exemple, _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="1c5fa-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="1c5fa-111">Création d’un jeu de mise à l’échelle de machine virtuelle (VMSS)</span><span class="sxs-lookup"><span data-stu-id="1c5fa-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="1c5fa-112">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="1c5fa-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="1c5fa-113">Créer la mise en réseau (réseau virtuel / sous-réseau)</span><span class="sxs-lookup"><span data-stu-id="1c5fa-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="1c5fa-114">Spécification du sous-réseau</span><span class="sxs-lookup"><span data-stu-id="1c5fa-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="1c5fa-115">Spécification du réseau virtuel (VNET)</span><span class="sxs-lookup"><span data-stu-id="1c5fa-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="1c5fa-116">Créer la ressource IP publique tooAllow accès externe</span><span class="sxs-lookup"><span data-stu-id="1c5fa-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="1c5fa-117">Ce sera lié toohello équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="1c5fa-118">Créer un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="1c5fa-118">Create Load Balancer</span></span>
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

#### <a name="configure-load-balancer"></a><span data-ttu-id="1c5fa-119">Configurer l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="1c5fa-119">Configure Load Balancer</span></span>
<span data-ttu-id="1c5fa-120">Création de la configuration de Pool d’adresse de serveur principal, ce sera partagé par les cartes d’interface réseau de machines virtuelles de hello hello dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="1c5fa-121">Définir le Port de la sonde à charge équilibrée de charge, modifier les paramètres de hello en fonction de votre application.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="1c5fa-122">Créer un pool NAT entrant pour une connexion directe (pas de charge équilibrée) routé toohello machines virtuelles dans l’échelle de hello définies via hello équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="1c5fa-123">Cela est toodemonstrate à l’aide du protocole RDP et ne peut pas être nécessaire dans votre application.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="1c5fa-124">Créer hello règle d’équilibrage de charge, cet exemple montre charge le port 80 demandes d’équilibrage, à l’aide de paramètres hello des étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="1c5fa-125">Créez l’équilibrage de charge avec la configuration.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="1c5fa-126">Vérifiez les paramètres d’équilibrage de charge, vérifiez la charge des configurations de port à charge équilibrée, notez que vous ne verrez pas les règles NAT entrantes jusqu'à ce que hello machines virtuelles dans un ensemble d’échelle hello sont créées.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="1c5fa-127">Configurer et créer hello identiques</span><span class="sxs-lookup"><span data-stu-id="1c5fa-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="1c5fa-128">Notez que cet infrastructure exemple montre comment tooset de distribuer le trafic web de l’échelle sur un ensemble d’échelle hello mais hello Images de machines virtuelles spécifiées ici n’ont pas tous les services web installés.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

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

<span data-ttu-id="1c5fa-129">Lier tooLoad de carte réseau équilibrage et le sous-réseau</span><span class="sxs-lookup"><span data-stu-id="1c5fa-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="1c5fa-130">Créer la configuration du jeu de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="1c5fa-130">Create scale set Config</span></span>

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

<span data-ttu-id="1c5fa-131">Définir la configuration du jeu de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="1c5fa-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="1c5fa-132">Vous venez de créer un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="1c5fa-132">Now you have created hello scale set.</span></span> <span data-ttu-id="1c5fa-133">Vous pouvez tester la connexion toohello machine virtuelle individuelle à l’aide du protocole RDP dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="1c5fa-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
