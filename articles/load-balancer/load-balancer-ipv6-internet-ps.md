---
title: "Créer un équilibrage de charge Azure accessible sur Internet avec IPv6 - PowerShell | Microsoft Docs"
description: "Découvrez comment créer un équilibrage de charge accessible sur Internet avec IPv6 à l’aide de PowerShell pour Resource Manager"
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
ms.openlocfilehash: 9d3cd37d3f2912301904b0a35f6fbc978d173079
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="cbcd5-104">Création d’un équilibrage de charge accessible sur Internet avec IPv6 à l’aide de PowerShell pour Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cbcd5-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cbcd5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbcd5-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="cbcd5-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cbcd5-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="cbcd5-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="cbcd5-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="cbcd5-108">Un équilibrage de charge Azure est de type Couche 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="cbcd5-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="cbcd5-109">L’équilibrage de charge offre une disponibilité élevée en distribuant le trafic entrant parmi les instances de service saines dans les services cloud ou les machines virtuelles dans un jeu d’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="cbcd5-110">Azure Load Balancer peut également présenter ces services sur plusieurs ports, plusieurs adresses IP ou les deux.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="cbcd5-111">Exemple de scénario de déploiement</span><span class="sxs-lookup"><span data-stu-id="cbcd5-111">Example deployment scenario</span></span>

<span data-ttu-id="cbcd5-112">Le diagramme suivant illustre la solution d’équilibrage de charge déployée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-112">The following diagram illustrates the load balancing solution being deployed in this article.</span></span>

![Scénario d’équilibreur de charge](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="cbcd5-114">Dans ce scénario, vous allez créer les ressources Azure suivantes :</span><span class="sxs-lookup"><span data-stu-id="cbcd5-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="cbcd5-115">un équilibrage de charge accessible sur Internet avec une adresse IP publique IPv4 et IPv6 ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="cbcd5-116">deux règles d’équilibrage de charge pour mapper les adresses IP virtuelles publiques sur les points de terminaison privés ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-116">two load balancing rules to map the public VIPs to the private endpoints</span></span>
* <span data-ttu-id="cbcd5-117">un groupe à haute disponibilité contenant les deux machines virtuelles ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-117">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="cbcd5-118">deux machines virtuelles ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="cbcd5-119">une interface de réseau virtuel pour chaque machine virtuelle avec des adresses IPv4 et IPv6 affectées ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-the-solution-using-the-azure-powershell"></a><span data-ttu-id="cbcd5-120">Déploiement de la solution à l’aide de Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbcd5-120">Deploying the solution using the Azure PowerShell</span></span>

<span data-ttu-id="cbcd5-121">Les étapes suivantes expliquent comment créer un équilibrage de charge accessible sur Internet à l’aide d’Azure Resource Manager avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="cbcd5-122">Avec Microsoft Azure Resource Manager, chaque ressource est créée et configurée individuellement, puis rassemblées pour créer une ressource.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-122">With Azure Resource Manager, each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="cbcd5-123">Pour déployer un équilibrage de charge, vous devez créer et configurer les objets suivants :</span><span class="sxs-lookup"><span data-stu-id="cbcd5-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="cbcd5-124">Configuration d’adresses IP frontales : contient les adresses IP publiques pour le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="cbcd5-125">Pool d’adresses principales : contient des interfaces réseau (NIC) pour que les machines virtuelles puissent recevoir le trafic réseau de l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="cbcd5-126">Règles d’équilibrage de charge : contient des règles de mappage d’un port public situé sur l’équilibrage de charge pour le pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="cbcd5-127">Règles NAT entrantes : contient des règles de mappage d’un port public situé sur l’équilibrage de charge vers le port d’une machine virtuelle spécifique située dans le pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="cbcd5-128">Sondes : contient les sondes d’intégrité utilisées pour vérifier la disponibilité des instances de machines virtuelles du pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="cbcd5-129">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="cbcd5-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="cbcd5-130">Configurer PowerShell pour utiliser Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cbcd5-130">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="cbcd5-131">Assurez-vous que vous disposez de la dernière version de production du module Microsoft Azure Resource Manager pour PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-131">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="cbcd5-132">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="cbcd5-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="cbcd5-133">À l’invite, entrez vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="cbcd5-134">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-134">Check the subscriptions for the account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="cbcd5-135">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-135">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="cbcd5-136">Créez un groupe de ressources (ignorez cette étape si vous en avez un) :</span><span class="sxs-lookup"><span data-stu-id="cbcd5-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="cbcd5-137">Créez un réseau virtuel et une adresse IP publique pour le pool d’adresses IP frontales</span><span class="sxs-lookup"><span data-stu-id="cbcd5-137">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="cbcd5-138">Créez un réseau virtuel avec un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="cbcd5-139">Créez des ressources d’adresse IP publiques Azure pour le pool d’adresses IP frontales.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-139">Create Azure Public IP address (PIP) resources for the front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="cbcd5-140">L’équilibreur de charge utilise l’étiquette du domaine de l’adresse IP publique en tant que préfixe du nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-140">The load balancer uses the domain label of the public IP as prefix for its FQDN.</span></span> <span data-ttu-id="cbcd5-141">Dans cet exemple, les noms de domaine complets (FQDN) sont *lbnrpipv4.westus.cloudapp.azure.com* et *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-141">In this example, the FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="cbcd5-142">Créer des configurations d’IP frontales et un pool d’adresses principales</span><span class="sxs-lookup"><span data-stu-id="cbcd5-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="cbcd5-143">Créez la configuration d’adresses frontales qui utilise les adresses IP publiques créées.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-143">Create front-end address configuration that uses the Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="cbcd5-144">Créez des pools d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="cbcd5-145">Créer des règles d’équilibreur de charge, des règles NAT, une sonde et un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="cbcd5-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="cbcd5-146">Cet exemple crée les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cbcd5-146">This example creates the following items:</span></span>

* <span data-ttu-id="cbcd5-147">une règle NAT pour transférer l’ensemble du trafic entrant sur le port 443 vers le port 4443 ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-147">a NAT rule to translate all incoming traffic on port 443 to port 4443</span></span>
* <span data-ttu-id="cbcd5-148">une règle d’équilibrage de charge pour équilibrer tout le trafic entrant sur le port 80 vers le port 80 des adresses du pool principal ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-148">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="cbcd5-149">une règle d’équilibrage de charge pour autoriser la connexion RDP aux machines virtuelles sur le port 3389 ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-149">a load balancer rule to allow RDP connection to the VMs on port 3389.</span></span>
* <span data-ttu-id="cbcd5-150">une règle de sonde qui vérifie le statut d’intégrité sur une page nommée *HealthProbe.aspx* ou un service sur le port 8080 ;</span><span class="sxs-lookup"><span data-stu-id="cbcd5-150">a probe rule to check the health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="cbcd5-151">un équilibrage de charge qui utilise tous les objets ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="cbcd5-152">Créez les règles NAT.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-152">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="cbcd5-153">Créer une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-153">Create a health probe.</span></span> <span data-ttu-id="cbcd5-154">Il existe deux façons de configurer une sonde :</span><span class="sxs-lookup"><span data-stu-id="cbcd5-154">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="cbcd5-155">Sonde HTTP</span><span class="sxs-lookup"><span data-stu-id="cbcd5-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="cbcd5-156">Sonde TCP</span><span class="sxs-lookup"><span data-stu-id="cbcd5-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="cbcd5-157">Pour cet exemple, nous allons utiliser les sondes TCP.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-157">For this example, we are going to use the TCP probes.</span></span>

3. <span data-ttu-id="cbcd5-158">Créez une règle d’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="cbcd5-159">Créez l’équilibrage de charge à l’aide des objets créés précédemment.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-159">Create the load balancer using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-the-back-end-vms"></a><span data-ttu-id="cbcd5-160">Créez des cartes réseaux pour les machines virtuelles principales.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-160">Create NICs for the back-end VMs</span></span>

1. <span data-ttu-id="cbcd5-161">Obtenez le réseau virtuel et le sous-réseau du réseau virtuel où les cartes réseau doivent être créées.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-161">Get the Virtual Network and Virtual Network Subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="cbcd5-162">Créez des configurations IP et des cartes réseau pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-162">Create IP configurations and NICs for the VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-the-newly-created-nics"></a><span data-ttu-id="cbcd5-163">Créez des machines virtuelles et affectez-leur les cartes réseau nouvellement créées.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-163">Create virtual machines and assign the newly created NICs</span></span>

<span data-ttu-id="cbcd5-164">Pour plus d’informations sur la création d’une machine virtuelle, consultez la section [Création d’une machine virtuelle Windows à l’aide de Resource Manager et de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="cbcd5-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="cbcd5-165">Créez un groupe à haute disponibilité et un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="cbcd5-166">Créez chaque machine virtuelle et affectez les cartes réseau précédemment créées.</span><span class="sxs-lookup"><span data-stu-id="cbcd5-166">Create each VM and assign the previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type the username and password of the local administrator account."

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

## <a name="next-steps"></a><span data-ttu-id="cbcd5-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cbcd5-167">Next steps</span></span>

[<span data-ttu-id="cbcd5-168">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="cbcd5-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="cbcd5-169">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="cbcd5-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="cbcd5-170">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="cbcd5-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
