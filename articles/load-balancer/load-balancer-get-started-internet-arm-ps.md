---
title: "aaaCreate une côté Azure Internet l’équilibrage de charge - PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate une côté Internet l’équilibrage de charge dans le Gestionnaire de ressources à l’aide de PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="a86bf-103"><a name="get-started"></a>Création d’un équilibrage de charge accessible sur Internet dans Resource Manager à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a86bf-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a86bf-104">Portail</span><span class="sxs-lookup"><span data-stu-id="a86bf-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="a86bf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a86bf-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="a86bf-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="a86bf-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="a86bf-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="a86bf-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="a86bf-108">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="a86bf-109">Vous pouvez également [apprendre comment toocreate une côté Internet l’équilibrage de charge à l’aide du modèle de déploiement classique hello](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a86bf-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="a86bf-110">Déploiement des solutions de hello à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a86bf-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="a86bf-111">Hello procédures suivantes explique comment toocreate une côté Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a86bf-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="a86bf-112">Avec Azure Resource Manager, chaque ressource est créé et configuré individuellement et puis rassembler toocreate un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="a86bf-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="a86bf-113">Vous devez créer et configurer hello suivant objets toodeploy un équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="a86bf-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="a86bf-114">Configuration d’adresses IP frontales : contient les adresses IP publiques (PIP) pour le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="a86bf-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="a86bf-115">Pool d’adresses de serveur principal : contient des interfaces réseau (NIC) pour le trafic réseau tooreceive de hello machines virtuelles à partir de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="a86bf-116">Règles d’équilibrage de charge : contient des règles pour mappent un port public sur le port de tooa d’équilibrage de charge de hello dans un pool d’adresses de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="a86bf-117">Les règles NAT de trafic entrant : contient des règles pour mappent un port public sur le port de tooa d’équilibrage de charge de hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="a86bf-118">Sondes : contient la disponibilité de toocheck les sondes utilisées de contrôle d’intégrité des instances de machine virtuelle dans le pool d’adresses principal hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="a86bf-119">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a86bf-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="a86bf-120">Configuration PowerShell toouse Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="a86bf-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="a86bf-121">Vérifiez que vous avez la dernière version de production hello du module du Gestionnaire de ressources Azure hello pour PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a86bf-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="a86bf-122">Connectez-vous tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a86bf-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="a86bf-123">À l’invite, entrez vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="a86bf-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="a86bf-124">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="a86bf-125">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="a86bf-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="a86bf-126">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a86bf-126">Create a resource group.</span></span> <span data-ttu-id="a86bf-127">(Ignorez cette étape si vous utilisez un groupe de ressources existant.)</span><span class="sxs-lookup"><span data-stu-id="a86bf-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="a86bf-128">Créer un réseau virtuel et une adresse IP publique hello frontal pool d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="a86bf-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="a86bf-129">Créez un sous-réseau et un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="a86bf-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="a86bf-130">Créer une Azure publique ressource d’adresse IP, nommée **adresse IP publique**, toobe utilisé par un pool IP frontal portant le nom DNS de hello **loadbalancernrp.westus.cloudapp.azure.com**. hello commande suivante utilise hello type d’allocation statique.</span><span class="sxs-lookup"><span data-stu-id="a86bf-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a86bf-131">équilibrage de charge Hello utilise le nom de domaine hello de l’adresse IP publique hello en tant que préfixe pour son nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="a86bf-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="a86bf-132">Cela est différent du modèle de déploiement classique de hello, qui utilise le service de cloud computing hello comme hello d’équilibrage de charge nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="a86bf-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="a86bf-133">Dans cet exemple, hello nom de domaine complet est **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="a86bf-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="a86bf-134">Créer un pool d’adresses IP frontales et un pool d’adresses principales</span><span class="sxs-lookup"><span data-stu-id="a86bf-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="a86bf-135">Créer un pool IP frontal nommé **LB-Frontend** qui utilise hello **adresse IP publique** ressource.</span><span class="sxs-lookup"><span data-stu-id="a86bf-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="a86bf-136">Créez un pool d’adresses principales nommé **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="a86bf-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="a86bf-137">Créer des règles NAT, une règle d’équilibreur de charge, une sonde et un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="a86bf-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="a86bf-138">Cet exemple crée hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a86bf-138">This example creates hello following items:</span></span>

* <span data-ttu-id="a86bf-139">Un tootranslate de règle NAT tout le trafic entrant sur le port 3441 tooport 3389</span><span class="sxs-lookup"><span data-stu-id="a86bf-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="a86bf-140">Un tootranslate de règle NAT tout le trafic entrant sur le port 3442 tooport 3389</span><span class="sxs-lookup"><span data-stu-id="a86bf-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="a86bf-141">Un état d’intégrité sonde règle toocheck hello, dans une page nommée **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="a86bf-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="a86bf-142">Un toobalance de règle d’équilibrage de charge tout le trafic entrant sur le port 80 tooport 80 sur hello adresses dans le pool principal de hello</span><span class="sxs-lookup"><span data-stu-id="a86bf-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="a86bf-143">Un équilibreur de charge qui utilise tous les objets ci-dessus</span><span class="sxs-lookup"><span data-stu-id="a86bf-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="a86bf-144">Suivez ces étapes :</span><span class="sxs-lookup"><span data-stu-id="a86bf-144">Use these steps:</span></span>

1. <span data-ttu-id="a86bf-145">Créer des règles NAT hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="a86bf-146">Créer une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="a86bf-146">Create a health probe.</span></span> <span data-ttu-id="a86bf-147">Il existe deux façons tooconfigure une sonde :</span><span class="sxs-lookup"><span data-stu-id="a86bf-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="a86bf-148">Sonde HTTP</span><span class="sxs-lookup"><span data-stu-id="a86bf-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="a86bf-149">Sonde TCP</span><span class="sxs-lookup"><span data-stu-id="a86bf-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="a86bf-150">Créez une règle d’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="a86bf-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="a86bf-151">Créer l’équilibreur de charge hello en utilisant des objets de hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="a86bf-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="a86bf-152">Créer des cartes réseau</span><span class="sxs-lookup"><span data-stu-id="a86bf-152">Create NICs</span></span>

<span data-ttu-id="a86bf-153">Créer des interfaces réseau (ou modifier des modèles existants) et les associer tooNAT règles, des règles d’équilibrage de charge et des sondes :</span><span class="sxs-lookup"><span data-stu-id="a86bf-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="a86bf-154">Obtenir les réseaux virtuels hello et un sous-réseau de réseau virtuel, où les cartes réseau de hello doivent toobe créé.</span><span class="sxs-lookup"><span data-stu-id="a86bf-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="a86bf-155">Créez une carte réseau nommée **être lb-nic1**et l’associer à la première règle NAT de hello et un pool d’adresses de serveur principal premier (et unique) hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="a86bf-156">Créez une carte réseau nommée **être lb-nic2**et l’associer à la deuxième règle NAT hello et un pool d’adresses de serveur principal premier (et unique) hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="a86bf-157">Vérifiez les cartes réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="a86bf-158">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="a86bf-158">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="a86bf-159">Hello d’utilisation `Add-AzureRmVMNetworkInterface` applet de commande tooassign hello NIC toodifferent machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a86bf-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="a86bf-160">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a86bf-160">Create a virtual machine</span></span>

<span data-ttu-id="a86bf-161">Pour des instructions sur la création d’une machine virtuelle et l’attribution d’une carte résau, voir [Création d’une machine virtuelle Azure à l’aide de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a86bf-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="a86bf-162">Ajouter l’équilibrage de charge hello toohello de l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="a86bf-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="a86bf-163">Équilibrage de charge hello de récupérer à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="a86bf-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="a86bf-164">Charger la ressource de programme d’équilibrage de charge hello dans une variable (si vous n’avez pas encore fait).</span><span class="sxs-lookup"><span data-stu-id="a86bf-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="a86bf-165">variable de Hello est appelée **$lb**. Utilisez hello même les noms de ressource d’équilibrage de charge hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="a86bf-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="a86bf-166">Charge la variable de tooa hello configuration principale.</span><span class="sxs-lookup"><span data-stu-id="a86bf-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="a86bf-167">Charger l’interface de réseau hello déjà créé dans une variable.</span><span class="sxs-lookup"><span data-stu-id="a86bf-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="a86bf-168">nom de variable Hello est **$nic**.</span><span class="sxs-lookup"><span data-stu-id="a86bf-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="a86bf-169">Hello nom de l’interface réseau est hello identique à celui de hello exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="a86bf-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="a86bf-170">Modifier la configuration de serveur principal hello sur l’interface de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="a86bf-171">Enregistrer l’objet d’interface réseau hello.</span><span class="sxs-lookup"><span data-stu-id="a86bf-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="a86bf-172">Après l’ajout d’une interface réseau toohello pool principal d’équilibrage de charge, il commence à recevoir le trafic de réseau en fonction des règles d’équilibrage de charge hello pour cette ressource d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="a86bf-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="a86bf-173">Mettre à jour un équilibreur de charge existant</span><span class="sxs-lookup"><span data-stu-id="a86bf-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="a86bf-174">À l’aide de hello charger équilibrage de hello l’exemple précédent, assignez une variable de charge équilibrage objet toohello **$slb** à l’aide de `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="a86bf-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="a86bf-175">Dans l’exemple suivant de hello, vous ajouter une règle NAT entrante--à l’aide du port 81 de pool frontal de hello et port 8181 pour le pool principal de hello--tooan équilibreur de charge existant.</span><span class="sxs-lookup"><span data-stu-id="a86bf-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="a86bf-176">Enregistrer la nouvelle configuration de hello à l’aide de `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="a86bf-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="a86bf-177">Supprimer un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="a86bf-177">Remove a load balancer</span></span>

<span data-ttu-id="a86bf-178">Utilisez la commande hello `Remove-AzureLoadBalancer` toodelete un équilibreur de charge créé précédemment nommé **kg NRP** dans un groupe de ressources appelé **NRP-RG**.</span><span class="sxs-lookup"><span data-stu-id="a86bf-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="a86bf-179">Vous pouvez utiliser le commutateur facultatif de hello **-Force** invite de commandes tooavoid hello pour suppression.</span><span class="sxs-lookup"><span data-stu-id="a86bf-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a86bf-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a86bf-180">Next steps</span></span>

[<span data-ttu-id="a86bf-181">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="a86bf-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="a86bf-182">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="a86bf-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a86bf-183">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="a86bf-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
