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
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="257ea-103">Comment tooload équilibrer les machines virtuelles Windows dans Azure toocreate une application hautement disponible</span><span class="sxs-lookup"><span data-stu-id="257ea-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="257ea-104">L’équilibrage de charge offre un niveau plus élevé de disponibilité en répartissant les demandes entrantes sur plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="257ea-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="257ea-105">Dans ce didacticiel, vous découvrez hello différents composants d’équilibrage de charge Azure hello de distribuer le trafic et fournissant une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="257ea-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="257ea-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="257ea-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="257ea-107">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="257ea-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="257ea-108">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="257ea-109">Créer des règles de trafic pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="257ea-110">Utiliser l’Extension de Script personnalisé de hello toocreate un site IIS de base</span><span class="sxs-lookup"><span data-stu-id="257ea-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="257ea-111">Créer des ordinateurs virtuels et d’attachement d’équilibrage de charge tooa</span><span class="sxs-lookup"><span data-stu-id="257ea-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="257ea-112">Afficher un équilibrage de charge en action</span><span class="sxs-lookup"><span data-stu-id="257ea-112">View a load balancer in action</span></span>
> * <span data-ttu-id="257ea-113">Ajouter et supprimer des machines virtuelles d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="257ea-114">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="257ea-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="257ea-115">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="257ea-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="257ea-116">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="257ea-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="257ea-117">Vue d’ensemble de l’équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="257ea-117">Azure load balancer overview</span></span>
<span data-ttu-id="257ea-118">Un équilibreur de charge Azure est un équilibreur de charge de type Couche 4 (TCP, UDP) qui offre une haute disponibilité en répartissant le trafic entrant entre les machines virtuelles saines.</span><span class="sxs-lookup"><span data-stu-id="257ea-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="257ea-119">Une sonde d’intégrité d’équilibrage de charge surveille un port donné sur chaque machine virtuelle et ne distribue le trafic tooan machine virtuelle opérationnelle.</span><span class="sxs-lookup"><span data-stu-id="257ea-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="257ea-120">Vous définissez une configuration IP frontale qui contient une ou plusieurs adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="257ea-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="257ea-121">Cette configuration IP frontale permet à votre toobe d’applications et d’équilibrage de charge accessible sur Internet de hello.</span><span class="sxs-lookup"><span data-stu-id="257ea-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="257ea-122">Machines virtuelles se connecter tooa équilibrage de charge à l’aide de leur carte réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="257ea-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="257ea-123">toohello du trafic toodistribute machines virtuelles, un pool d’adresses de serveur principal contient des adresses IP de hello d’équilibrage de charge hello virtuelle (NIC) connectées toohello.</span><span class="sxs-lookup"><span data-stu-id="257ea-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="257ea-124">flux de hello toocontrol du trafic, vous définissez des règles d’équilibrage de charge pour les ports et protocoles qui mappent des machines virtuelles de tooyour spécifiques.</span><span class="sxs-lookup"><span data-stu-id="257ea-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="257ea-125">Créer un équilibreur de charge Azure</span><span class="sxs-lookup"><span data-stu-id="257ea-125">Create Azure load balancer</span></span>
<span data-ttu-id="257ea-126">Cette section décrit en détail comment vous pouvez créer et configurer chaque composant d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="257ea-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="257ea-127">Avant de créer un équilibreur de charge, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="257ea-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="257ea-128">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupLoadBalancer* Bonjour *EastUS* emplacement :</span><span class="sxs-lookup"><span data-stu-id="257ea-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="257ea-129">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="257ea-129">Create a public IP address</span></span>
<span data-ttu-id="257ea-130">tooaccess votre application sur hello Internet, vous avez besoin d’une adresse IP publique pour l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="257ea-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="257ea-131">Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="257ea-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="257ea-132">Hello exemple suivant crée une adresse IP publique nommée *myPublicIP* Bonjour *myResourceGroupLoadBalancer* groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="257ea-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="257ea-133">Créer un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-133">Create a load balancer</span></span>
<span data-ttu-id="257ea-134">Créez une adresse IP frontale avec [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="257ea-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="257ea-135">Hello exemple suivant crée une adresse IP de serveur frontal nommée *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="257ea-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="257ea-136">Créez un pool d’adresses principales avec [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="257ea-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="257ea-137">Hello exemple suivant crée un pool d’adresses principales nommé *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="257ea-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="257ea-138">Maintenant, créez équilibrage de charge hello [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="257ea-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="257ea-139">Hello exemple suivant crée un équilibreur de charge nommé *myLoadBalancer* à l’aide de hello *myPublicIP* adresse :</span><span class="sxs-lookup"><span data-stu-id="257ea-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="257ea-140">Créer une sonde d’intégrité</span><span class="sxs-lookup"><span data-stu-id="257ea-140">Create a health probe</span></span>
<span data-ttu-id="257ea-141">tooallow hello équilibrage toomonitor hello l’état de charge de votre application, vous utilisez une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="257ea-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="257ea-142">Sonde d’intégrité Hello dynamiquement ajoute ou supprime des machines virtuelles à partir de la rotation d’équilibrage de charge hello en fonction de leurs contrôles toohealth de réponse.</span><span class="sxs-lookup"><span data-stu-id="257ea-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="257ea-143">Par défaut, un ordinateur virtuel est supprimé de la distribution d’équilibrage de charge hello après deux défaillances consécutives à des intervalles de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="257ea-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="257ea-144">Vous créez une sonde d’intégrité selon un protocole ou une page de vérification d’intégrité spécifique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="257ea-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="257ea-145">Bonjour à l’exemple suivant crée une sonde TCP.</span><span class="sxs-lookup"><span data-stu-id="257ea-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="257ea-146">Vous pouvez également créer des sondes HTTP personnalisées pour des contrôles d’intégrité plus affinés.</span><span class="sxs-lookup"><span data-stu-id="257ea-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="257ea-147">Lorsque vous utilisez une sonde HTTP personnalisée, vous devez créer page vérifier l’intégrité hello, tel que *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="257ea-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="257ea-148">Sonde de Hello doit retourner un **HTTP 200 OK** réponse pour hello charge équilibrage tookeep hello hôte en rotation.</span><span class="sxs-lookup"><span data-stu-id="257ea-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="257ea-149">toocreate une sonde d’intégrité TCP, vous utilisez [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="257ea-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="257ea-150">Hello exemple suivant crée une sonde d’intégrité nommée *myHealthProbe* qui analyse chaque machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="257ea-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="257ea-151">Mettre à jour d’équilibrage de charge hello [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="257ea-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="257ea-152">Créer une règle d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-152">Create a load balancer rule</span></span>
<span data-ttu-id="257ea-153">Une règle d’équilibreur de charge est utilisé toodefine comment le trafic est distribué toohello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="257ea-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="257ea-154">Vous définissez la configuration IP frontale de hello pour le trafic entrant de hello et hello principal pool tooreceive hello du trafic IP, ainsi que les sources requis hello et port de destination.</span><span class="sxs-lookup"><span data-stu-id="257ea-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="257ea-155">toomake que seuls les ordinateurs virtuels sains recevoir du trafic, vous définissez également toouse de sonde d’intégrité hello.</span><span class="sxs-lookup"><span data-stu-id="257ea-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="257ea-156">Créez une règle d’équilibreur de charge avec [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="257ea-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="257ea-157">Hello exemple suivant crée une règle d’équilibreur de charge nommée *myLoadBalancerRule* et équilibre le trafic sur le port *80*:</span><span class="sxs-lookup"><span data-stu-id="257ea-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

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

<span data-ttu-id="257ea-158">Mettre à jour d’équilibrage de charge hello [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="257ea-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="257ea-159">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="257ea-159">Configure virtual network</span></span>
<span data-ttu-id="257ea-160">Avant de déployer des machines virtuelles et tester votre programme d’équilibrage, créer hello prenant en charge des ressources du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="257ea-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="257ea-161">Pour plus d’informations sur les réseaux virtuels, consultez hello [gérer les réseaux virtuels Azure](tutorial-virtual-network.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="257ea-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="257ea-162">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="257ea-162">Create network resources</span></span>
<span data-ttu-id="257ea-163">Créez un réseau virtuel avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="257ea-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="257ea-164">Hello exemple suivant crée un réseau virtuel nommé *myVnet* avec *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="257ea-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

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

<span data-ttu-id="257ea-165">Créez une règle de groupe de sécurité réseau avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), puis un groupe de sécurité réseau avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="257ea-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="257ea-166">Ajouter hello sécurité groupe toohello sous-réseau avec [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) puis mettez à jour de réseau virtuel hello [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="257ea-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="257ea-167">Hello exemple suivant crée une règle de groupe de sécurité réseau nommée *myNetworkSecurityGroup* et l’applique trop*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="257ea-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

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

<span data-ttu-id="257ea-168">Des cartes d’interface réseau virtuelles sont créées avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="257ea-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="257ea-169">Hello exemple suivant crée trois cartes réseau virtuelles.</span><span class="sxs-lookup"><span data-stu-id="257ea-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="257ea-170">(Une carte réseau virtuelle pour chaque ordinateur virtuel que vous créez pour votre application Bonjour suivant les étapes).</span><span class="sxs-lookup"><span data-stu-id="257ea-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="257ea-171">Vous pouvez créer des cartes réseau virtuelles supplémentaires et des machines virtuelles à tout moment et ajoutez-les à équilibrage de charge toohello :</span><span class="sxs-lookup"><span data-stu-id="257ea-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="257ea-172">Créer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="257ea-172">Create virtual machines</span></span>
<span data-ttu-id="257ea-173">tooimprove hello haute disponibilité de votre application, placez vos machines virtuelles dans un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="257ea-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="257ea-174">Créez un groupe à haute disponibilité avec la commande [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="257ea-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="257ea-175">Hello exemple suivant crée un groupe à haute disponibilité nommée *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="257ea-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="257ea-176">Définir un administrateur de nom d’utilisateur et mot de passe pour les machines virtuelles hello avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="257ea-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="257ea-177">Vous pouvez désormais créer VMs hello avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="257ea-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="257ea-178">Bonjour à l’exemple suivant crée trois machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="257ea-178">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="257ea-179">Il prend quelques minutes toocreate et configurer tous les trois machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="257ea-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="257ea-180">Installer IIS avec l’extension de script personnalisé</span><span class="sxs-lookup"><span data-stu-id="257ea-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="257ea-181">Dans un didacticiel précédent sur [comment toocustomize une machine virtuelle Windows](tutorial-automate-vm-deployment.md), vous avez appris comment personnalisation tooautomate avec hello Extension de Script personnalisé pour Windows.</span><span class="sxs-lookup"><span data-stu-id="257ea-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="257ea-182">Vous pouvez utiliser hello même approche tooinstall et configurer IIS sur vos ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="257ea-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="257ea-183">Utilisez [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Extension de Script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="257ea-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="257ea-184">Hello extension exécute `powershell Add-WindowsFeature Web-Server` tooinstall hello serveur Web d’IIS, puis hello de mises à jour *Default.htm* page tooshow hello nom d’hôte de hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="257ea-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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

## <a name="test-load-balancer"></a><span data-ttu-id="257ea-185">Tester l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-185">Test load balancer</span></span>
<span data-ttu-id="257ea-186">Obtenir hello une adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="257ea-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="257ea-187">exemple Hello obtient adresse IP hello *myPublicIP* créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="257ea-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="257ea-188">Vous pouvez entrer ensuite des adresse IP publique de hello dans tooa navigateur.</span><span class="sxs-lookup"><span data-stu-id="257ea-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="257ea-189">site Web de Hello est affichée, notamment le nom d’hôte hello Hello VM cet équilibrage de charge hello distributed tooas trafic Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="257ea-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Site web IIS en cours d’exécution](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="257ea-191">équilibrage de charge toosee hello répartir le trafic entre tous les trois machines virtuelles exécutant votre application, vous pouvez forcer l’actualisation votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="257ea-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="257ea-192">Ajouter et supprimer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="257ea-192">Add and remove VMs</span></span>
<span data-ttu-id="257ea-193">Vous devrez peut-être maintenance tooperform sur hello machines virtuelles exécutant votre application, telles que l’installation des mises à jour du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="257ea-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="257ea-194">toodeal avec une augmentation du trafic tooyour application, vous devrez peut-être tooadd des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="257ea-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="257ea-195">Cette section vous montre comment tooremove ou ajouter une machine virtuelle à partir de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="257ea-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="257ea-196">Supprimer une machine virtuelle à partir de l’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="257ea-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="257ea-197">Obtenir la carte d’interface réseau hello avec [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), puis ensemble hello *LoadBalancerBackendAddressPools* propriété de hello carte réseau virtuelle trop*$null*.</span><span class="sxs-lookup"><span data-stu-id="257ea-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="257ea-198">Enfin, mettez à jour de carte réseau virtuelle de hello. :</span><span class="sxs-lookup"><span data-stu-id="257ea-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="257ea-199">équilibrage de charge toosee hello répartir le trafic entre hello deux autres machines virtuelles exécutant votre application vous pouvez forcer l’actualisation votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="257ea-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="257ea-200">Vous pouvez désormais effectuer la maintenance sur hello machine virtuelle, tels que l’installation des mises à jour du système d’exploitation ou d’effectuer un redémarrage de l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="257ea-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="257ea-201">Ajouter un équilibrage de charge de toohello de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="257ea-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="257ea-202">Après une maintenance de la machine virtuelle, ou si vous avez besoin de la capacité de tooexpand, définissez hello *LoadBalancerBackendAddressPools* propriété du toohello de carte réseau virtuelle hello *BackendAddressPool* de [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="257ea-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="257ea-203">Obtenir l’équilibrage de charge hello :</span><span class="sxs-lookup"><span data-stu-id="257ea-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="257ea-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="257ea-204">Next steps</span></span>

<span data-ttu-id="257ea-205">Dans ce didacticiel, vous créé un équilibreur de charge et attaché tooit de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="257ea-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="257ea-206">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="257ea-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="257ea-207">Crée un équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="257ea-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="257ea-208">Créer une sonde d’intégrité d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="257ea-209">Créer des règles de trafic pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="257ea-210">Utiliser l’Extension de Script personnalisé de hello toocreate un site IIS de base</span><span class="sxs-lookup"><span data-stu-id="257ea-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="257ea-211">Créer des ordinateurs virtuels et d’attachement d’équilibrage de charge tooa</span><span class="sxs-lookup"><span data-stu-id="257ea-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="257ea-212">Afficher un équilibrage de charge en action</span><span class="sxs-lookup"><span data-stu-id="257ea-212">View a load balancer in action</span></span>
> * <span data-ttu-id="257ea-213">Ajouter et supprimer des machines virtuelles d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="257ea-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="257ea-214">Avancer toohello toolearn de didacticiel suivant la mise en réseau de la machine virtuelle toomanage.</span><span class="sxs-lookup"><span data-stu-id="257ea-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="257ea-215">Gérer les machines virtuelles et les réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="257ea-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
