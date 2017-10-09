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
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="03012-103">Création d’une application à haute disponibilité avec équilibrage de charge sur des machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="03012-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="03012-104">Dans ce didacticiel, vous créez une application hautement disponible est résilient toomaintenance les événements.</span><span class="sxs-lookup"><span data-stu-id="03012-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="03012-105">application Hello utilise un équilibrage de charge, un ensemble de disponibilité et trois Windows virtual machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="03012-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="03012-106">Ce didacticiel installe IIS, mais vous pouvez utiliser ce didacticiel toodeploy une infrastructure d’application à l’aide hello les mêmes composants haute disponibilité et les recommandations.</span><span class="sxs-lookup"><span data-stu-id="03012-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="03012-107">Étape 1 : Conditions préalables pour Azure</span><span class="sxs-lookup"><span data-stu-id="03012-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="03012-108">toocomplete ce didacticiel, assurez-vous que vous avez installé hello dernières [Azure PowerShell](/powershell/azure/overview) module.</span><span class="sxs-lookup"><span data-stu-id="03012-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="03012-109">Tout d’abord, connectez-vous à tooyour abonnement Azure avec hello commande de connexion-AzureRmAccount et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="03012-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="03012-110">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="03012-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="03012-111">Avant de pouvoir créer d’autres ressources Azure, vous devez toocreate un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="03012-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="03012-112">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` région :</span><span class="sxs-lookup"><span data-stu-id="03012-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="03012-113">Étape 2 : Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="03012-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="03012-114">Les machines virtuelles peuvent être créées sur les domaines de mise à jour et d’erreur logiques.</span><span class="sxs-lookup"><span data-stu-id="03012-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="03012-115">Chaque domaine logique représente une partie du matériel de centre de données Azure hello sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="03012-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="03012-116">Lorsque vous créez deux ou plusieurs machines virtuelles, vos ressources de calcul et de stockage sont réparties sur ces domaines.</span><span class="sxs-lookup"><span data-stu-id="03012-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="03012-117">Cette distribution hello la disponibilité de votre application est assurée si un composant matériel a besoin de maintenance.</span><span class="sxs-lookup"><span data-stu-id="03012-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="03012-118">Les groupes à haute disponibilité permettent de définir ces domaines d’erreur et de mise à jour logiques.</span><span class="sxs-lookup"><span data-stu-id="03012-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="03012-119">Créez un groupe à haute disponibilité avec la commande [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="03012-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="03012-120">Hello exemple suivant crée un groupe à haute disponibilité nommée `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="03012-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="03012-121">Étape 3 : Créer un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="03012-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="03012-122">Un équilibrage de charge Azure répartit le trafic sur un ensemble de machines virtuelles définies à l’aide de règles d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="03012-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="03012-123">Une sonde d’intégrité analyse un port donné sur chaque machine virtuelle et ne distribue le trafic tooan machine virtuelle opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="03012-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="03012-124">Création d’une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="03012-124">Create public IP address</span></span>

<span data-ttu-id="03012-125">tooaccess votre application sur hello Internet, attribuez un équilibreur de charge toohello d’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="03012-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="03012-126">Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="03012-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="03012-127">Hello exemple suivant crée une adresse IP publique nommée `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="03012-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="03012-128">Créer un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="03012-128">Create load balancer</span></span>

<span data-ttu-id="03012-129">Créez une adresse IP frontale avec [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="03012-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="03012-130">Hello exemple suivant crée une adresse IP de serveur frontal nommée `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="03012-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="03012-131">Créez un pool d’adresses principales avec [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="03012-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="03012-132">Hello exemple suivant crée un pool d’adresses principales nommé `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="03012-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="03012-133">Maintenant, créez équilibrage de charge hello [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="03012-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="03012-134">Hello exemple suivant crée un équilibreur de charge nommé `myLoadBalancer` à l’aide de hello `myPublicIP` adresse :</span><span class="sxs-lookup"><span data-stu-id="03012-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="03012-135">Créer une sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="03012-135">Create health probe</span></span>

<span data-ttu-id="03012-136">tooallow hello équilibrage toomonitor hello l’état de charge de votre application, vous utilisez une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="03012-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="03012-137">Sonde d’intégrité Hello dynamiquement ajoute ou supprime des machines virtuelles à partir de la rotation d’équilibrage de charge hello en fonction de leurs contrôles toohealth de réponse.</span><span class="sxs-lookup"><span data-stu-id="03012-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="03012-138">Par défaut, un ordinateur virtuel est supprimé de la distribution d’équilibrage de charge hello après deux défaillances consécutives à des intervalles de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="03012-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="03012-139">Créez une sonde d’intégrité avec [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="03012-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="03012-140">Hello exemple suivant crée une sonde d’intégrité nommée `myHealthProbe` qui analyse chaque machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="03012-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="03012-141">Créer une règle d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="03012-141">Create load balancer rule</span></span>

<span data-ttu-id="03012-142">Une règle d’équilibreur de charge est utilisé toodefine comment le trafic est distribué toohello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="03012-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="03012-143">Créez une règle d’équilibreur de charge avec [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="03012-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="03012-144">Hello exemple suivant crée une règle d’équilibreur de charge nommée `myLoadBalancerRule` et équilibre le trafic sur le port `80`:</span><span class="sxs-lookup"><span data-stu-id="03012-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="03012-145">Mettre à jour d’équilibrage de charge hello [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="03012-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="03012-146">Étape 4 - Configuration de la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="03012-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="03012-147">Chaque machine virtuelle a un ou plusieurs virtuel cartes d’interface réseau (NIC) qui se connectent tooa des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="03012-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="03012-148">Ce réseau virtuel est sécurisé de trafic toofilter selon les règles d’accès définies.</span><span class="sxs-lookup"><span data-stu-id="03012-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="03012-149">Création d’un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="03012-149">Create virtual network</span></span>

<span data-ttu-id="03012-150">Tout d’abord, configurez un sous-réseau avec [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="03012-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="03012-151">Hello exemple suivant crée un sous-réseau nommé `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="03012-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="03012-152">tooyour de connectivité réseau tooprovide machines virtuelles, créez un réseau virtuel avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="03012-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="03012-153">Hello exemple suivant crée un réseau virtuel nommé `myVnet` avec `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="03012-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="03012-154">Configurer la sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="03012-154">Configure network security</span></span>

<span data-ttu-id="03012-155">Un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) (NSG) Azure contrôle le trafic entrant et sortant pour une ou plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="03012-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="03012-156">Les règles de groupe de sécurité réseau autorisent ou refusent le trafic réseau sur un port ou une plage de ports spécifique.</span><span class="sxs-lookup"><span data-stu-id="03012-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="03012-157">Ces règles peuvent également inclure un préfixe d’adresse source afin que seul le trafic provenant d’une source prédéfinie puisse communiquer avec une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="03012-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="03012-158">tooallow web tooreach de trafic de votre application, créez une règle de groupe de sécurité réseau avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="03012-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="03012-159">Hello exemple suivant crée une règle de groupe de sécurité réseau nommée `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="03012-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

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

<span data-ttu-id="03012-160">Créez un groupe de sécurité réseau avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="03012-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="03012-161">Hello exemple suivant crée un groupe de sécurité réseau nommé `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="03012-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="03012-162">Ajouter un sous-réseau de toohello hello réseau sécurité groupe avec [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="03012-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="03012-163">Réseau virtuel de mise à jour hello avec [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="03012-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="03012-164">Création de cartes d’interface réseau virtuelles</span><span class="sxs-lookup"><span data-stu-id="03012-164">Create virtual network interface cards</span></span>

<span data-ttu-id="03012-165">Charger la fonction équilibrages de la ressource de carte réseau virtuelle hello plutôt que hello VM réel.</span><span class="sxs-lookup"><span data-stu-id="03012-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="03012-166">Hello carte réseau virtuelle est l’équilibrage de charge connecté toohello et puis attaché tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="03012-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="03012-167">Créez une carte réseau virtuelle avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="03012-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="03012-168">Hello exemple suivant crée trois cartes réseau virtuelles.</span><span class="sxs-lookup"><span data-stu-id="03012-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="03012-169">(Une carte réseau virtuelle pour chaque ordinateur virtuel que vous créez pour votre application Bonjour suivant les étapes) :</span><span class="sxs-lookup"><span data-stu-id="03012-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


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

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="03012-170">Étape 5 : Créer les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="03012-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="03012-171">Avec tous les hello sous-jacent des composants en place, vous pouvez désormais créer toorun d’ordinateurs virtuels hautement disponible votre application.</span><span class="sxs-lookup"><span data-stu-id="03012-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="03012-172">Obtenir le nom d’utilisateur hello et le mot de passe pour le compte d’administrateur hello sur l’ordinateur virtuel de hello avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="03012-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="03012-173">Créer des machines virtuelles hello avec [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [AzureRmVMOperatingSystem de jeu](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface ajouter](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), et [AzureRmVM-nouvelle](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="03012-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="03012-174">Bonjour à l’exemple suivant crée trois machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="03012-174">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="03012-175">Il prend plusieurs minutes toocreate et configurer tous les trois machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="03012-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="03012-176">Hello sonde d’intégrité d’équilibrage de charge détecte automatiquement lors de l’application hello est en cours d’exécution sur chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="03012-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="03012-177">Une fois que l’application hello est en cours d’exécution, règle d’équilibrage de charge hello démarre le trafic de toodistribute.</span><span class="sxs-lookup"><span data-stu-id="03012-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="03012-178">Installer l’application hello</span><span class="sxs-lookup"><span data-stu-id="03012-178">Install hello app</span></span> 

<span data-ttu-id="03012-179">Les extensions de machine virtuelle Azure sont des tâches de configuration de machine virtuelle tooautomate utilisé, l’installation d’applications et la configuration de système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="03012-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="03012-180">Hello [extension de script personnalisé pour Windows](./../virtual-machines-windows-extensions-customscript.md) est toorun utilisée n’importe quel script PowerShell sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="03012-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="03012-181">script de Hello peut être stockée dans le stockage Azure, n’importe quel point de terminaison HTTP accessible, ou incorporé dans la configuration de l’extension hello script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="03012-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="03012-182">Lorsque vous utilisez l’extension de script personnalisé hello, l’agent de machine virtuelle Azure hello gère l’exécution du script hello.</span><span class="sxs-lookup"><span data-stu-id="03012-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="03012-183">Utilisez [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) extension de script personnalisé tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="03012-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="03012-184">Hello extension exécute `powershell Add-WindowsFeature Web-Server` serveur Web IIS de hello tooinstall :</span><span class="sxs-lookup"><span data-stu-id="03012-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

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

### <a name="test-your-app"></a><span data-ttu-id="03012-185">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="03012-185">Test your app</span></span>

<span data-ttu-id="03012-186">Obtenir hello une adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="03012-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="03012-187">exemple Hello obtient adresse IP hello `myPublicIP` créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="03012-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="03012-188">Entrez l’adresse IP publique de hello dans le navigateur web de tooa.</span><span class="sxs-lookup"><span data-stu-id="03012-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="03012-189">Règle de groupe de sécurité réseau hello en place, le site Web IIS de hello par défaut s’affiche.</span><span class="sxs-lookup"><span data-stu-id="03012-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![Site IIS par défaut](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="03012-191">Étape 6 : Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="03012-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="03012-192">Vous devrez peut-être maintenance tooperform sur hello machines virtuelles exécutant votre application, telles que l’installation des mises à jour du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="03012-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="03012-193">toodeal avec une augmentation du trafic tooyour application, vous devrez peut-être tooadd des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="03012-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="03012-194">Cette section vous montre comment tooremove ou ajouter une machine virtuelle à partir de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="03012-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="03012-195">Supprimer une machine virtuelle à partir de l’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="03012-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="03012-196">Supprimer une machine virtuelle à partir du pool d’adresses principales hello en réinitialisant la propriété de LoadBalancerBackendAddressPools hello hello carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="03012-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="03012-197">Obtenir la carte d’interface réseau hello avec [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="03012-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="03012-198">Définir la propriété de LoadBalancerBackendAddressPools de hello de carte d’interface réseau hello trop NULL comme valeur de $:</span><span class="sxs-lookup"><span data-stu-id="03012-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="03012-199">Mise à jour de la carte d’interface réseau hello :</span><span class="sxs-lookup"><span data-stu-id="03012-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="03012-200">Ajouter un équilibrage de charge de toohello de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="03012-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="03012-201">Après une maintenance de la machine virtuelle, ou si vous avez besoin de la capacité de tooexpand, ajout hello carte réseau d’un pool d’adresses principales toohello machine virtuelle d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="03012-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="03012-202">Obtenir l’équilibrage de charge hello :</span><span class="sxs-lookup"><span data-stu-id="03012-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="03012-203">Ajouter un pool d’adresses principales hello hello charge équilibrage toohello carte d’interface réseau :</span><span class="sxs-lookup"><span data-stu-id="03012-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="03012-204">Mise à jour de la carte d’interface réseau hello :</span><span class="sxs-lookup"><span data-stu-id="03012-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="03012-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03012-205">Next Steps</span></span>

<span data-ttu-id="03012-206">Exemples – [Exemples de scripts PowerShell pour Machines virtuelles Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="03012-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
