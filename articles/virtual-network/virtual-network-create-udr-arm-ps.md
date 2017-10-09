---
title: dispositifs de routage et virtuels aaaControl dans Azure - PowerShell | Documents Microsoft
description: "Découvrez comment toocontrol équipements virtuels et de routage à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="0c6a1-103">Créer des itinéraires définis par l’utilisateur à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c6a1-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c6a1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c6a1-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="0c6a1-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="0c6a1-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="0c6a1-106">Modèle</span><span class="sxs-lookup"><span data-stu-id="0c6a1-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="0c6a1-107">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="0c6a1-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="0c6a1-108">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="0c6a1-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="0c6a1-109">Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="0c6a1-110">Veillez à bien comprendre les [modèles et outils de déploiement](../azure-resource-manager/resource-manager-deployment-model.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="0c6a1-111">Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="0c6a1-112">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="0c6a1-113">Vous pouvez également [créer UDRs dans le modèle de déploiement classique hello](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0c6a1-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="0c6a1-114">l’exemple Hello PowerShell commandes ci-dessous attendent un simple environnement déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="0c6a1-115">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer des environnement de test hello en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello Si nécessaire et suivez les instructions hello dans hello portal.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="0c6a1-116">Créer hello UDR pour le sous-réseau frontal de hello</span><span class="sxs-lookup"><span data-stu-id="0c6a1-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="0c6a1-117">table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario hello ci-dessus, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="0c6a1-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="0c6a1-118">Créer un toosend de l’itinéraire utilisé tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toobe routé toohello **FW1** appliance virtuelle (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="0c6a1-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="0c6a1-119">Créer une table de routage nommée **UDR-FrontEnd** Bonjour **westus** région qui contient l’itinéraire de hello.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="0c6a1-120">Créez une variable qui contient hello réseau virtuel où le sous-réseau de hello est.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="0c6a1-121">Dans notre scénario, hello réseau virtuel est nommé **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="0c6a1-122">Table d’itinéraires hello associer créé ci-dessus toohello **frontal** sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="0c6a1-123">sortie Hello pour commande hello ci-dessus montre le contenu de l’objet de configuration de réseau virtuel hello, qui n’existe que sur l’ordinateur hello où vous exécutez PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="0c6a1-124">Vous devez toorun hello **Set-AzureVirtualNetwork** toosave de l’applet de commande tooAzure de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="0c6a1-125">Enregistrer la nouvelle configuration de sous-réseau hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="0c6a1-126">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="0c6a1-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="0c6a1-127">Créer hello UDR pour le sous-réseau principal de hello</span><span class="sxs-lookup"><span data-stu-id="0c6a1-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="0c6a1-128">table d’itinéraires toocreate hello et d’itinéraire nécessaires pour le sous-réseau principal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="0c6a1-129">Créer un toosend de l’itinéraire utilisé tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toobe routé toohello **FW1** appliance virtuelle (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="0c6a1-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="0c6a1-130">Créer une table de routage nommée **UDR-principal** Bonjour **ouest des États-Unis** région qui contient l’itinéraire de hello créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="0c6a1-131">Table d’itinéraires hello associer créé ci-dessus toohello **principal** sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="0c6a1-132">Enregistrer la nouvelle configuration de sous-réseau hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="0c6a1-133">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="0c6a1-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="0c6a1-134">Activer le transfert IP sur FW1</span><span class="sxs-lookup"><span data-stu-id="0c6a1-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="0c6a1-135">le transfert IP tooenable Bonjour carte réseau utilisée par **FW1**, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="0c6a1-136">Créez une variable qui contient les paramètres de hello pour hello carte réseau utilisée par FW1.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="0c6a1-137">Dans notre scénario, hello NIC est nommé **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="0c6a1-138">Activer le transfert IP et enregistrer les paramètres de carte réseau hello.</span><span class="sxs-lookup"><span data-stu-id="0c6a1-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="0c6a1-139">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="0c6a1-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

