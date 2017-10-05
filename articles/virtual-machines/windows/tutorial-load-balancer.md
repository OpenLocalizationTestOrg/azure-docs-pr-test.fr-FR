---
title: "Équilibrage de la charge des machines virtuelles Windows dans Azure | Microsoft Docs"
description: "Découvrez comment utiliser l’équilibreur de charge Azure pour créer une application hautement disponible et sécurisée entre trois machines virtuelles Windows"
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
ms.openlocfilehash: 6738d88d5a0430abaf3855dbf97a618e4c83617f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-windows-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="66e13-103">Équilibrage de la charge des machines virtuelles Windows dans Azure pour créer une application hautement disponible</span><span class="sxs-lookup"><span data-stu-id="66e13-103">How to load balance Windows virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="66e13-104">L’équilibrage de charge offre un niveau plus élevé de disponibilité en répartissant les demandes entrantes sur plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="66e13-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="66e13-105">Dans ce didacticiel, vous allez découvrir les différents composants de l’équilibreur de charge Azure qui répartissent le trafic et fournissent une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="66e13-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="66e13-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="66e13-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="66e13-107">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="66e13-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="66e13-108">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="66e13-109">Créer des règles de trafic pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="66e13-110">Utilisez l’extension de script personnalisé pour créer un site de base IIS</span><span class="sxs-lookup"><span data-stu-id="66e13-110">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="66e13-111">Créer des machines virtuelles et les attacher à un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="66e13-112">Afficher un équilibrage de charge en action</span><span class="sxs-lookup"><span data-stu-id="66e13-112">View a load balancer in action</span></span>
> * <span data-ttu-id="66e13-113">Ajouter et supprimer des machines virtuelles d’un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="66e13-114">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="66e13-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="66e13-115">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="66e13-115">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="66e13-116">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="66e13-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="66e13-117">Vue d’ensemble de l’équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="66e13-117">Azure load balancer overview</span></span>
<span data-ttu-id="66e13-118">Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines.</span><span class="sxs-lookup"><span data-stu-id="66e13-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="66e13-119">Une sonde d’intégrité d’équilibreur de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic que vers une machine virtuelle opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="66e13-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="66e13-120">Vous définissez une configuration IP frontale qui contient une ou plusieurs adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="66e13-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="66e13-121">Cette configuration IP frontale permet d’accéder à votre équilibreur de charge et à vos applications via Internet.</span><span class="sxs-lookup"><span data-stu-id="66e13-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="66e13-122">Les machines virtuelles se connectent à un équilibreur de charge à l’aide de leur carte d’interface réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="66e13-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="66e13-123">Pour distribuer le trafic vers les machines virtuelles, un pool d’adresses principal contient les adresses IP des cartes d’interface réseau virtuelles connectées à l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="66e13-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="66e13-124">Pour contrôler le flux de trafic, vous définissez les règles d’équilibrage de charge pour les ports et les protocoles spécifiques qui correspondent à vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="66e13-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="66e13-125">Créer un équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="66e13-125">Create Azure load balancer</span></span>
<span data-ttu-id="66e13-126">Cette section explique en détail comment vous pouvez créer et configurer chaque composant de l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="66e13-126">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="66e13-127">Avant de créer un équilibreur de charge, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="66e13-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="66e13-128">L’exemple suivant crée un groupe de ressources nommé *myResourceGroupLoadBalancer* dans l’emplacement *EastUS* :</span><span class="sxs-lookup"><span data-stu-id="66e13-128">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="66e13-129">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="66e13-129">Create a public IP address</span></span>
<span data-ttu-id="66e13-130">Pour accéder à votre application sur Internet, vous avez besoin d’une adresse IP publique pour l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="66e13-130">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="66e13-131">Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="66e13-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="66e13-132">L’exemple suivant crée une adresse IP publique nommée *myPublicIP* dans le groupe de ressources *myResourceGroupLoadBalancer* :</span><span class="sxs-lookup"><span data-stu-id="66e13-132">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="66e13-133">Créer un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-133">Create a load balancer</span></span>
<span data-ttu-id="66e13-134">Créez une adresse IP frontale avec [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="66e13-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="66e13-135">L’exemple suivant crée une adresse IP frontale nommée *myFrontEndPool* :</span><span class="sxs-lookup"><span data-stu-id="66e13-135">The following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="66e13-136">Créez un pool d’adresses principales avec [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="66e13-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="66e13-137">L’exemple suivant crée un pool d’adresses principales nommé *myBackEndPool* :</span><span class="sxs-lookup"><span data-stu-id="66e13-137">The following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="66e13-138">Maintenant, créez l’équilibreur de charge avec [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="66e13-138">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="66e13-139">L’exemple suivant créer un équilibrage de charge nommé *myLoadBalancer* avec l’adresse *myPublicIP* :</span><span class="sxs-lookup"><span data-stu-id="66e13-139">The following example creates a load balancer named *myLoadBalancer* using the *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="66e13-140">Créer une sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="66e13-140">Create a health probe</span></span>
<span data-ttu-id="66e13-141">Pour permettre à l’équilibrage de charge de surveiller l’état de votre application, vous utilisez une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="66e13-141">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="66e13-142">La sonde d’intégrité ajoute ou supprime dynamiquement des machines virtuelles de la rotation d’équilibrage de charge en fonction de leur réponse aux vérifications d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="66e13-142">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="66e13-143">Par défaut, une machine virtuelle est supprimée de la distribution d’équilibrage de charge après deux échecs consécutifs à des intervalles de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="66e13-143">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="66e13-144">Vous créez une sonde d’intégrité selon un protocole ou une page de vérification d’intégrité spécifique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="66e13-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="66e13-145">L’exemple suivant permet de créer une sonde TCP.</span><span class="sxs-lookup"><span data-stu-id="66e13-145">The following example creates a TCP probe.</span></span> <span data-ttu-id="66e13-146">Vous pouvez également créer des sondes HTTP personnalisées pour des contrôles d’intégrité plus affinés.</span><span class="sxs-lookup"><span data-stu-id="66e13-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="66e13-147">Lorsque vous utilisez une sonde HTTP personnalisée, vous devez créer la page de contrôle d’intégrité, par exemple *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="66e13-147">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="66e13-148">La sonde doit retourner une réponse **HTTP 200 OK** pour l’équilibreur de charge pour assurer la rotation de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="66e13-148">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="66e13-149">Pour créer une sonde d’intégrité TCP, utilisez [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="66e13-149">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="66e13-150">L’exemple suivant crée une sonde d’intégrité nommée *myHealthProbe* qui surveille chaque machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="66e13-150">The following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="66e13-151">Mettez à jour l’équilibreur de charge avec [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) :</span><span class="sxs-lookup"><span data-stu-id="66e13-151">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="66e13-152">Créer une règle d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-152">Create a load balancer rule</span></span>
<span data-ttu-id="66e13-153">Une règle d’équilibrage de charge est utilisée pour définir la distribution du trafic vers les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="66e13-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="66e13-154">Vous définissez la configuration IP frontale pour le trafic entrant et le pool d’adresses IP principal pour recevoir le trafic, ainsi que le port source et le port de destination requis.</span><span class="sxs-lookup"><span data-stu-id="66e13-154">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="66e13-155">Pour veiller à ce que seules les machines virtuelles saines reçoivent le trafic, vous devez également définir la sonde d’intégrité à utiliser.</span><span class="sxs-lookup"><span data-stu-id="66e13-155">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="66e13-156">Créez une règle d’équilibreur de charge avec [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="66e13-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="66e13-157">L’exemple suivant crée une règle d’équilibreur de charge nommée *myLoadBalancerRule* et équilibre le trafic sur le port *80* :</span><span class="sxs-lookup"><span data-stu-id="66e13-157">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

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

<span data-ttu-id="66e13-158">Mettez à jour l’équilibreur de charge avec [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) :</span><span class="sxs-lookup"><span data-stu-id="66e13-158">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="66e13-159">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="66e13-159">Configure virtual network</span></span>
<span data-ttu-id="66e13-160">Avant de déployer des machines virtuelles et de pouvoir tester votre équilibreur, créez les ressources de réseau virtuel de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="66e13-160">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="66e13-161">Pour plus d’informations sur les réseaux virtuels, consultez le didacticiel [Manage Azure Virtual Networks (Gérer les réseaux virtuels Azure)](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="66e13-161">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="66e13-162">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="66e13-162">Create network resources</span></span>
<span data-ttu-id="66e13-163">Créez un réseau virtuel avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="66e13-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="66e13-164">L’exemple suivant crée un réseau virtuel nommé *myVnet* avec un sous-réseau nommé *mySubnet* :</span><span class="sxs-lookup"><span data-stu-id="66e13-164">The following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="66e13-165">Créez une règle de groupe de sécurité réseau avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), puis un groupe de sécurité réseau avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="66e13-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="66e13-166">Ajoutez le groupe de sécurité réseau au sous-réseau avec [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig), puis mettez à jour le réseau virtuel avec [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="66e13-166">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="66e13-167">L’exemple suivant crée une règle de groupe de sécurité réseau nommée *myNetworkSecurityGroup* et l’applique à *mySubnet* :</span><span class="sxs-lookup"><span data-stu-id="66e13-167">The following example creates a network security group rule named *myNetworkSecurityGroup* and applies it to *mySubnet*:</span></span>

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

# Create the network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply the network security group to a subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update the virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="66e13-168">Des cartes d’interface réseau virtuelles sont créées avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="66e13-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="66e13-169">L’exemple suivant crée trois cartes réseau virtuelles.</span><span class="sxs-lookup"><span data-stu-id="66e13-169">The following example creates three virtual NICs.</span></span> <span data-ttu-id="66e13-170">(Une carte d’interface réseau virtuelle pour chaque machine virtuelle que vous créez pour votre application dans les étapes suivantes).</span><span class="sxs-lookup"><span data-stu-id="66e13-170">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="66e13-171">Vous pouvez créer des machines virtuelles et des cartes d’interface réseau virtuelles supplémentaires à tout moment et les ajouter à l’équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="66e13-171">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="66e13-172">Créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="66e13-172">Create virtual machines</span></span>
<span data-ttu-id="66e13-173">Pour améliorer la haute disponibilité de votre application, placez vos machines virtuelles dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="66e13-173">To improve the high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="66e13-174">Créez un groupe à haute disponibilité avec la commande [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="66e13-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="66e13-175">L’exemple suivant permet de créer un groupe à haute disponibilité nommé *myAvailabilitySet* :</span><span class="sxs-lookup"><span data-stu-id="66e13-175">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="66e13-176">Définissez un nom d’utilisateur administrateur et un mot de passe pour les machines virtuelles avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) :</span><span class="sxs-lookup"><span data-stu-id="66e13-176">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="66e13-177">Vous pouvez maintenant créer les machines virtuelles avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="66e13-177">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="66e13-178">L’exemple suivant crée trois machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="66e13-178">The following example creates three VMs:</span></span>

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

<span data-ttu-id="66e13-179">La création et la configuration des trois machines virtuelles prennent quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="66e13-179">It takes a few minutes to create and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="66e13-180">Installer IIS avec l’extension de script personnalisé</span><span class="sxs-lookup"><span data-stu-id="66e13-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="66e13-181">Dans un didacticiel précédent [How to customize a Windows virtual machine (Personnalisation d’une machine virtuelle Windows)](tutorial-automate-vm-deployment.md), vous avez appris à automatiser la personnalisation des machines virtuelles avec l’extension de script personnalisé pour Windows.</span><span class="sxs-lookup"><span data-stu-id="66e13-181">In a previous tutorial on [How to customize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with the Custom Script Extension for Windows.</span></span> <span data-ttu-id="66e13-182">Vous pouvez utiliser la même approche pour installer et configurer IIS sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="66e13-182">You can use the same approach to install and configure IIS on your VMs.</span></span>

<span data-ttu-id="66e13-183">Utilisez [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) pour installer l’extension de script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="66e13-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="66e13-184">L’extension exécute `powershell Add-WindowsFeature Web-Server` pour installer le serveur web IIS, puis met à jour la page *Default.htm* pour qu’elle affiche le nom d’hôte de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="66e13-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

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

## <a name="test-load-balancer"></a><span data-ttu-id="66e13-185">Tester l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-185">Test load balancer</span></span>
<span data-ttu-id="66e13-186">Obtenez l’adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="66e13-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="66e13-187">L’exemple suivant obtient l’adresse IP pour *myPublicIP* créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="66e13-187">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="66e13-188">Vous pouvez alors entrer l’adresse IP publique dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="66e13-188">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="66e13-189">Le site web s’affiche, avec notamment le nom d’hôte de la machine virtuelle sur laquelle l’équilibreur de charge a distribué le trafic comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="66e13-189">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Site web IIS en cours d’exécution](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="66e13-191">Pour visualiser la distribution de trafic par l’équilibreur de charge sur les trois machines virtuelles exécutant votre application, vous pouvez forcer l’actualisation de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="66e13-191">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="66e13-192">Ajouter et supprimer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="66e13-192">Add and remove VMs</span></span>
<span data-ttu-id="66e13-193">Vous devrez peut-être effectuer la maintenance sur la machine virtuelle exécutant votre application, avec par exemple l’installation des mises à jour du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="66e13-193">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="66e13-194">Pour faire face à une augmentation du trafic vers votre application, vous devrez peut-être ajouter des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="66e13-194">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="66e13-195">Cette section vous indique comment supprimer ou ajouter une machine virtuelle pour l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="66e13-195">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="66e13-196">Supprimer une machine virtuelle de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-196">Remove a VM from the load balancer</span></span>
<span data-ttu-id="66e13-197">Obtenez la carte d’interface réseau avec [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), puis définissez la propriété *LoadBalancerBackendAddressPools* de la carte d’interface réseau virtuelle sur *$null*.</span><span class="sxs-lookup"><span data-stu-id="66e13-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set the *LoadBalancerBackendAddressPools* property of the virtual NIC to *$null*.</span></span> <span data-ttu-id="66e13-198">Pour finir, mettez à jour la carte d’interface réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66e13-198">Finally, update the virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="66e13-199">Pour visualiser la distribution de trafic par l’équilibreur de charge sur les deux machines virtuelles restantes exécutant votre application, vous pouvez forcer l’actualisation de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="66e13-199">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="66e13-200">Vous pouvez maintenant effectuer la maintenance sur la machine virtuelle, avec par exemple l’installation des mises à jour du système d’exploitation ou le redémarrage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66e13-200">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="66e13-201">Ajouter une machine virtuelle à l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-201">Add a VM to the load balancer</span></span>
<span data-ttu-id="66e13-202">Après avoir effectué des opérations de maintenance sur la machine virtuelle ou si vous devez développer sa capacité, définissez la propriété *LoadBalancerBackendAddressPools* de la carte d’interface réseau virtuelle sur le *BackendAddressPool* de [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer) :</span><span class="sxs-lookup"><span data-stu-id="66e13-202">After performing VM maintenance, or if you need to expand capacity, set the *LoadBalancerBackendAddressPools* property of the virtual NIC to the *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="66e13-203">Récupérez l’équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="66e13-203">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="66e13-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66e13-204">Next steps</span></span>

<span data-ttu-id="66e13-205">Ce didacticiel vous a montré comment créer un équilibrage de charge et y attacher des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="66e13-205">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="66e13-206">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="66e13-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="66e13-207">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="66e13-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="66e13-208">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="66e13-209">Créer des règles de trafic pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="66e13-210">Utilisez l’extension de script personnalisé pour créer un site de base IIS</span><span class="sxs-lookup"><span data-stu-id="66e13-210">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="66e13-211">Créer des machines virtuelles et les attacher à un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-211">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="66e13-212">Afficher un équilibrage de charge en action</span><span class="sxs-lookup"><span data-stu-id="66e13-212">View a load balancer in action</span></span>
> * <span data-ttu-id="66e13-213">Ajouter et supprimer des machines virtuelles d’un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="66e13-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="66e13-214">Passez au didacticiel suivant pour découvrir comment gérer la mise en réseau des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="66e13-214">Advance to the next tutorial to learn how to manage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="66e13-215">Gérer les machines virtuelles et les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="66e13-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
