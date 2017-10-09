---
title: "équilibrage de charge aaaCreate une côté Azure Internet avec IPv6 - PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate une connecté à Internet l’équilibrage de charge avec IPv6 à l’aide de PowerShell pour le Gestionnaire de ressources"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, équilibreur de charge azure, double pile, adresse ip publique, ipv6 natif, mobile, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="4a1f9-104">Création d’un équilibrage de charge accessible sur Internet avec IPv6 à l’aide de PowerShell pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4a1f9-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a1f9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a1f9-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="4a1f9-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4a1f9-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="4a1f9-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="4a1f9-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="4a1f9-108">Un équilibrage de charge Azure est de type Couche 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="4a1f9-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="4a1f9-109">équilibrage de charge Hello offre une haute disponibilité en répartissant le trafic entrant entre les instances de service intègre dans les services de cloud computing ou les machines virtuelles dans un jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="4a1f9-110">Azure Load Balancer peut également présenter ces services sur plusieurs ports, plusieurs adresses IP ou les deux.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="4a1f9-111">Exemple de scénario de déploiement</span><span class="sxs-lookup"><span data-stu-id="4a1f9-111">Example deployment scenario</span></span>

<span data-ttu-id="4a1f9-112">Hello diagramme suivant illustre dans cet article en cours de déploiement de solutions d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![Scénario d’équilibreur de charge](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="4a1f9-114">Dans ce scénario, vous allez créer hello suivant des ressources Azure :</span><span class="sxs-lookup"><span data-stu-id="4a1f9-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="4a1f9-115">un équilibrage de charge accessible sur Internet avec une adresse IP publique IPv4 et IPv6 ;</span><span class="sxs-lookup"><span data-stu-id="4a1f9-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="4a1f9-116">deux charge équilibrage règles toomap hello VIP toohello privés points de terminaison publics</span><span class="sxs-lookup"><span data-stu-id="4a1f9-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="4a1f9-117">un toothat à haute disponibilité contient des machines virtuelles de hello deux</span><span class="sxs-lookup"><span data-stu-id="4a1f9-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="4a1f9-118">deux machines virtuelles ;</span><span class="sxs-lookup"><span data-stu-id="4a1f9-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="4a1f9-119">une interface de réseau virtuel pour chaque machine virtuelle avec des adresses IPv4 et IPv6 affectées ;</span><span class="sxs-lookup"><span data-stu-id="4a1f9-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="4a1f9-120">Déploiement de solution hello à l’aide de hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a1f9-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="4a1f9-121">Hello suit montrent comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="4a1f9-122">Avec le Gestionnaire de ressources Azure, chaque ressource est créé et configuré individuellement, puis rassembler les toocreate une ressource.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="4a1f9-123">toodeploy un équilibreur de charge, que vous créez et configurez les hello objets suivants :</span><span class="sxs-lookup"><span data-stu-id="4a1f9-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="4a1f9-124">Configuration d’adresses IP frontales : contient les adresses IP publiques pour le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="4a1f9-125">Pool d’adresses principal - contient des interfaces réseau (NIC) pour le trafic réseau tooreceive de hello machines virtuelles à partir de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="4a1f9-126">Règles d’équilibrage de charge - contient des règles de mappage d’un port public sur tooport d’équilibrage de charge hello dans un pool d’adresses de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="4a1f9-127">Les règles NAT de trafic entrant - contient des règles de mappage d’un port public sur le port de tooa d’équilibrage de charge hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="4a1f9-128">Sondes - contient la disponibilité de toocheck les sondes utilisées de contrôle d’intégrité des instances de machines virtuelles dans un pool d’adresses de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="4a1f9-129">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="4a1f9-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="4a1f9-130">Configuration PowerShell toouse Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4a1f9-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="4a1f9-131">Assurez-vous que vous avez la dernière version de production hello du module du Gestionnaire de ressources Azure hello pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="4a1f9-132">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="4a1f9-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="4a1f9-133">À l’invite, entrez vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="4a1f9-134">Vérifiez les abonnements hello pour le compte de hello</span><span class="sxs-lookup"><span data-stu-id="4a1f9-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="4a1f9-135">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="4a1f9-136">Créez un groupe de ressources (ignorez cette étape si vous en avez un) :</span><span class="sxs-lookup"><span data-stu-id="4a1f9-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="4a1f9-137">Créer un réseau virtuel et une adresse IP publique hello frontal pool d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="4a1f9-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="4a1f9-138">Créez un réseau virtuel avec un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="4a1f9-139">Créer des ressources (PIP) pour le pool d’adresses IP frontal hello adresse IP publique d’Azure.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="4a1f9-140">équilibrage de charge Hello utilise le nom de domaine hello de l’adresse IP publique hello en tant que préfixe pour son nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="4a1f9-141">Dans cet exemple, les noms de domaine complets hello sont *lbnrpipv4.westus.cloudapp.azure.com* et *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="4a1f9-142">Créer des configurations d’IP frontales et un pool d’adresses principales</span><span class="sxs-lookup"><span data-stu-id="4a1f9-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="4a1f9-143">Créer la configuration d’adresse frontale qui utilise des adresses IP publiques hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="4a1f9-144">Créez des pools d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="4a1f9-145">Créer des règles d’équilibreur de charge, des règles NAT, une sonde et un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="4a1f9-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="4a1f9-146">Cet exemple crée hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4a1f9-146">This example creates hello following items:</span></span>

* <span data-ttu-id="4a1f9-147">la règle NAT tootranslate tout le trafic entrant sur le port 443 tooport 4443</span><span class="sxs-lookup"><span data-stu-id="4a1f9-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="4a1f9-148">un toobalance de règle d’équilibrage de charge tout le trafic entrant sur le port 80 tooport 80 sur hello adresses dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="4a1f9-149">une charge équilibrage règle tooallow RDP connexion toohello machines virtuelles sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="4a1f9-150">un état d’intégrité sonde règle toocheck hello, dans une page nommée *HealthProbe.aspx* ou un service sur le port 8080</span><span class="sxs-lookup"><span data-stu-id="4a1f9-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="4a1f9-151">un équilibrage de charge qui utilise tous les objets ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="4a1f9-152">Créer des règles NAT hello.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="4a1f9-153">Créer une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-153">Create a health probe.</span></span> <span data-ttu-id="4a1f9-154">Il existe deux façons tooconfigure une sonde :</span><span class="sxs-lookup"><span data-stu-id="4a1f9-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="4a1f9-155">Sonde HTTP</span><span class="sxs-lookup"><span data-stu-id="4a1f9-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="4a1f9-156">Sonde TCP</span><span class="sxs-lookup"><span data-stu-id="4a1f9-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="4a1f9-157">Pour cet exemple, nous allons hello toouse que TCP sondes.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="4a1f9-158">Créez une règle d’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="4a1f9-159">Créer un équilibreur de charge hello à l’aide d’objets de hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="4a1f9-160">Créer des cartes réseau pour hello principal des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="4a1f9-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="4a1f9-161">Obtenir hello réseau virtuel et le sous-réseau de réseau virtuel, où hello cartes réseau doivent toobe créé.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="4a1f9-162">Créer des cartes réseau et les configurations IP pour les machines virtuelles hello.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="4a1f9-163">Créer des ordinateurs virtuels et affecter hello nouvellement créé des cartes réseau</span><span class="sxs-lookup"><span data-stu-id="4a1f9-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="4a1f9-164">Pour plus d’informations sur la création d’une machine virtuelle, consultez la section [Création d’une machine virtuelle Windows à l’aide de Resource Manager et de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4a1f9-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="4a1f9-165">Créez un groupe à haute disponibilité et un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4a1f9-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="4a1f9-166">Créer chaque machine virtuelle et attribuer des cartes réseau de hello précédente créé</span><span class="sxs-lookup"><span data-stu-id="4a1f9-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="4a1f9-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4a1f9-167">Next steps</span></span>

[<span data-ttu-id="4a1f9-168">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="4a1f9-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="4a1f9-169">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="4a1f9-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="4a1f9-170">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="4a1f9-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
