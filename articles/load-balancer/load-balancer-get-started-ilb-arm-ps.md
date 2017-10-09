---
title: "aaaCreate Azure interne l’équilibrage de charge - PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge à l’aide de PowerShell dans le Gestionnaire de ressources"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="ab40a-103">Créer un équilibreur de charge interne à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab40a-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab40a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ab40a-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="ab40a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab40a-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="ab40a-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ab40a-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="ab40a-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="ab40a-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ab40a-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ab40a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ab40a-109">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ab40a-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="ab40a-110">Hello suit explique comment toocreate un interne l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ab40a-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="ab40a-111">Avec Azure Resource Manager, hello éléments toocreate un équilibreur de charge interne sont configurées individuellement, puis combinés toocreate un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="ab40a-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="ab40a-112">Vous devez toocreate et que vous configurez hello suivant objets toodeploy un équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="ab40a-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="ab40a-113">Avant la configuration IP de fin - configurera hello adresse IP privée pour le trafic réseau entrant</span><span class="sxs-lookup"><span data-stu-id="ab40a-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="ab40a-114">Pool d’adresses principales - configure les interfaces réseau hello afin de recevront le trafic à charge équilibrée de hello provenant d’un pool d’adresses IP de serveur frontal</span><span class="sxs-lookup"><span data-stu-id="ab40a-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="ab40a-115">Règles d’équilibrage de charge - source et la configuration du port local pour hello l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="ab40a-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="ab40a-116">Sondes - configure la sonde d’état d’intégrité hello pour les instances de Machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="ab40a-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="ab40a-117">Les règles NAT de trafic entrant - configure l’accès hello port règles toodirectly une des instances de Machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="ab40a-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="ab40a-118">Pour obtenir plus d’informations sur les composants de l’équilibrage de charge avec Azure Resource Manager, consultez la page [Support Azure Resource Manager pour l’équilibrage de charge](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ab40a-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="ab40a-119">Hello étapes suivantes expliquent comment tooconfigure un équilibrage de charge entre les deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ab40a-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="ab40a-120">Le programme d’installation PowerShell toouse Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="ab40a-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="ab40a-121">Assurez-vous que vous avez hello dernière version de production hello module Azure pour PowerShell et disposez de PowerShell le programme d’installation correctement tooaccess votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ab40a-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="ab40a-122">Étape 1</span><span class="sxs-lookup"><span data-stu-id="ab40a-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="ab40a-123">Étape 2</span><span class="sxs-lookup"><span data-stu-id="ab40a-123">Step 2</span></span>

<span data-ttu-id="ab40a-124">Vérifiez les abonnements hello pour le compte de hello</span><span class="sxs-lookup"><span data-stu-id="ab40a-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="ab40a-125">Vous serez invité à tooAuthenticate avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ab40a-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="ab40a-126">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="ab40a-126">Step 3</span></span>

<span data-ttu-id="ab40a-127">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="ab40a-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="ab40a-128">Création d’un groupe de ressources pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="ab40a-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="ab40a-129">Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant)</span><span class="sxs-lookup"><span data-stu-id="ab40a-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="ab40a-130">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="ab40a-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="ab40a-131">Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ab40a-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="ab40a-132">Assurez-vous que toutes les commandes toocreate un équilibrage de charge utilisera hello même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ab40a-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="ab40a-133">Bonjour exemple ci-dessus nous avons créé un groupe de ressources appelé « NRP-RG » et l’emplacement « Ouest des États-Unis ».</span><span class="sxs-lookup"><span data-stu-id="ab40a-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="ab40a-134">Créer un réseau virtuel et une adresse IP privée pour le pool d’adresses IP frontal</span><span class="sxs-lookup"><span data-stu-id="ab40a-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="ab40a-135">Crée un sous-réseau de réseau virtuel de hello et assigne toovariable $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="ab40a-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="ab40a-136">Créez un réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="ab40a-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="ab40a-137">Crée le réseau virtuel de hello et ajoute le réseau virtuel hello sous-réseau toohello d’équilibrage de charge sous-réseau être NRPVNet et assigne toovariable $vnet</span><span class="sxs-lookup"><span data-stu-id="ab40a-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="ab40a-138">Création du pool d’adresses IP frontales et du pool d’adresses principales</span><span class="sxs-lookup"><span data-stu-id="ab40a-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="ab40a-139">Configuration d’un pool d’IP de serveur frontal pour hello entrant charger équilibrage réseau le trafic et principal adresse pool tooreceive hello à charge équilibrée.</span><span class="sxs-lookup"><span data-stu-id="ab40a-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="ab40a-140">Étape 1</span><span class="sxs-lookup"><span data-stu-id="ab40a-140">Step 1</span></span>

<span data-ttu-id="ab40a-141">Créer un pool d’IP front-end à l’aide d’adresse IP privée de hello 10.0.2.5 pour les 10.0.2.0/24 sous-réseau hello qui sera endpoint de trafic réseau entrant hello.</span><span class="sxs-lookup"><span data-stu-id="ab40a-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="ab40a-142">Étape 2</span><span class="sxs-lookup"><span data-stu-id="ab40a-142">Step 2</span></span>

<span data-ttu-id="ab40a-143">Configurer un pool d’adresses principale utilisée tooreceive le trafic entrant à partir du pool d’adresses IP de serveur frontal :</span><span class="sxs-lookup"><span data-stu-id="ab40a-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="ab40a-144">Création des règles d’équilibrage de charge, des règles NAT, de la sonde et de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="ab40a-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="ab40a-145">Après avoir créé le pool d’adresses IP hello frontal et le pool d’adresses principales hello, vous avez besoin des règles de hello toocreate qui appartiendront la ressource de programme d’équilibrage de charge toohello :</span><span class="sxs-lookup"><span data-stu-id="ab40a-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="ab40a-146">Étape 1</span><span class="sxs-lookup"><span data-stu-id="ab40a-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="ab40a-147">exemple Hello ci-dessus crée hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ab40a-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="ab40a-148">Règle NAT qui tout trafic entrant du trafic tooport 3441 passera tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="ab40a-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="ab40a-149">une autre règle NAT qui tout trafic entrant du trafic tooport 3442 passera tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="ab40a-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="ab40a-150">une règle d’équilibreur de charge qui chargera équilibrer tout le trafic entrant sur le port port public 80 toolocal 80 dans le pool d’adresses hello back-end.</span><span class="sxs-lookup"><span data-stu-id="ab40a-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="ab40a-151">une règle d’analyse qui vérifie l’état d’intégrité de hello pour le chemin d’accès « HealthProbe.aspx »</span><span class="sxs-lookup"><span data-stu-id="ab40a-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="ab40a-152">Étape 2</span><span class="sxs-lookup"><span data-stu-id="ab40a-152">Step 2</span></span>

<span data-ttu-id="ab40a-153">Créer un équilibreur de charge hello additionnant tous les objets (les règles NAT, règles d’équilibrage de charge, les configurations de sonde) :</span><span class="sxs-lookup"><span data-stu-id="ab40a-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="ab40a-154">Création d’interfaces réseau</span><span class="sxs-lookup"><span data-stu-id="ab40a-154">Create network interfaces</span></span>

<span data-ttu-id="ab40a-155">Après avoir créé un équilibreur de charge interne hello, vous devez définir les interfaces réseau recevra hello équilibré de charge réseau du trafic entrant, les règles NAT et la sonde.</span><span class="sxs-lookup"><span data-stu-id="ab40a-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="ab40a-156">Dans ce cas, interface de réseau Hello est configuré individuellement et peut être affectée tooa virtuels plus tard.</span><span class="sxs-lookup"><span data-stu-id="ab40a-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="ab40a-157">Étape 1</span><span class="sxs-lookup"><span data-stu-id="ab40a-157">Step 1</span></span>

<span data-ttu-id="ab40a-158">Obtenir les ressources hello virtuels interfaces réseau toocreate réseau et le sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="ab40a-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="ab40a-159">Cette étape crée une interface réseau qui appartiennent toohello pool principal d’équilibrage de charge et associer la première règle NAT de hello pour RDP pour cette interface réseau :</span><span class="sxs-lookup"><span data-stu-id="ab40a-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="ab40a-160">Étape 2</span><span class="sxs-lookup"><span data-stu-id="ab40a-160">Step 2</span></span>

<span data-ttu-id="ab40a-161">Créez une deuxième interface réseau appelée LB-Nic2-BE :</span><span class="sxs-lookup"><span data-stu-id="ab40a-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="ab40a-162">Cette étape crée une deuxième interface réseau, affectation toohello même équilibreur de charge précédent fin pool associant la deuxième règle NAT hello créé pour RDP :</span><span class="sxs-lookup"><span data-stu-id="ab40a-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="ab40a-163">résultat final de Hello affiche suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="ab40a-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="ab40a-164">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="ab40a-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="ab40a-165">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="ab40a-165">Step 3</span></span>

<span data-ttu-id="ab40a-166">Utilisez hello commande Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtuels.</span><span class="sxs-lookup"><span data-stu-id="ab40a-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="ab40a-167">Vous pouvez trouver hello des instructions étape par étape toocreate une machine virtuelle et affecter tooa NIC suivant la documentation de hello : [créer une machine virtuelle de Azure à l’aide de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab40a-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="ab40a-168">Ajouter une interface de réseau hello</span><span class="sxs-lookup"><span data-stu-id="ab40a-168">Add hello network interface</span></span>

<span data-ttu-id="ab40a-169">Si vous disposez déjà d’un ordinateur virtuel créé, vous pouvez ajouter l’interface de réseau de hello avec hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ab40a-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="ab40a-170">Étape 1</span><span class="sxs-lookup"><span data-stu-id="ab40a-170">Step 1</span></span>

<span data-ttu-id="ab40a-171">Charger la ressource de programme d’équilibrage de charge hello dans une variable (si vous n’avez pas encore fait).</span><span class="sxs-lookup"><span data-stu-id="ab40a-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="ab40a-172">variable Hello utilisée est appelée $lb et hello utilisez mêmes noms de ressource de programme d’équilibrage de charge hello créés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ab40a-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="ab40a-173">Étape 2</span><span class="sxs-lookup"><span data-stu-id="ab40a-173">Step 2</span></span>

<span data-ttu-id="ab40a-174">Charge la variable de tooa configuration hello back-end.</span><span class="sxs-lookup"><span data-stu-id="ab40a-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="ab40a-175">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="ab40a-175">Step 3</span></span>

<span data-ttu-id="ab40a-176">Charger l’interface de réseau hello déjà créé dans une variable.</span><span class="sxs-lookup"><span data-stu-id="ab40a-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="ab40a-177">nom de variable de Hello utilisée est la carte réseau de $.</span><span class="sxs-lookup"><span data-stu-id="ab40a-177">hello variable name used is $nic.</span></span> <span data-ttu-id="ab40a-178">nom de l’interface réseau Hello utilisé est hello même à partir de l’exemple hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ab40a-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="ab40a-179">Étape 4</span><span class="sxs-lookup"><span data-stu-id="ab40a-179">Step 4</span></span>

<span data-ttu-id="ab40a-180">Modifier la configuration de serveur principal hello sur l’interface de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="ab40a-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="ab40a-181">Étape 5</span><span class="sxs-lookup"><span data-stu-id="ab40a-181">Step 5</span></span>

<span data-ttu-id="ab40a-182">Enregistrer l’objet d’interface réseau hello.</span><span class="sxs-lookup"><span data-stu-id="ab40a-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="ab40a-183">Après l’ajout d’une interface réseau toohello pool principal d’équilibrage de charge, il commence à recevoir le trafic de réseau basé sur des règles pour cette ressource d’équilibrage de charge d’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="ab40a-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="ab40a-184">Mettre à jour un équilibreur de charge existant</span><span class="sxs-lookup"><span data-stu-id="ab40a-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="ab40a-185">Étape 1</span><span class="sxs-lookup"><span data-stu-id="ab40a-185">Step 1</span></span>
<span data-ttu-id="ab40a-186">À l’aide d’équilibrage de charge hello à partir de l’exemple hello ci-dessus, affecter charge équilibrage objet toovariable $slb à l’aide de Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="ab40a-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="ab40a-187">Étape 2</span><span class="sxs-lookup"><span data-stu-id="ab40a-187">Step 2</span></span>

<span data-ttu-id="ab40a-188">Bonjour l’exemple suivant, vous allez ajouter une règle NAT de trafic entrant via le port 81 dans frontal hello et port 8181 pour la sauvegarde de hello se terminer à équilibrage de charge existante de pool tooan</span><span class="sxs-lookup"><span data-stu-id="ab40a-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="ab40a-189">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="ab40a-189">Step 3</span></span>

<span data-ttu-id="ab40a-190">Enregistrez hello nouvelle configuration à l’aide de Set-AzureLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="ab40a-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="ab40a-191">Supprimer un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="ab40a-191">Remove a load balancer</span></span>

<span data-ttu-id="ab40a-192">Utilisez hello commande Remove-AzureRmLoadBalancer toodelete un équilibreur de charge créé précédemment nommé « NRP kg » dans un groupe de ressources appelé « NRP-RG »</span><span class="sxs-lookup"><span data-stu-id="ab40a-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="ab40a-193">Vous pouvez utiliser hello facultatif commutateur - invite de commandes de Force tooavoid hello pour suppression.</span><span class="sxs-lookup"><span data-stu-id="ab40a-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab40a-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab40a-194">Next steps</span></span>

[<span data-ttu-id="ab40a-195">Configuration d’un mode de distribution d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="ab40a-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ab40a-196">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="ab40a-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
