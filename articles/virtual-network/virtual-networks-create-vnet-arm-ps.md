---
title: "aaaCreate un réseau virtuel - Azure PowerShell | Documents Microsoft"
description: "Découvrez comment toocreate un virtuel réseau à l’aide de PowerShell."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="f8212-103">Créer un réseau virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8212-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="f8212-104">Azure propose deux modèles de déploiement : Azure Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="f8212-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f8212-105">Microsoft recommande de créer des ressources via le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f8212-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="f8212-106">toolearn en savoir plus sur hello différences entre hello deux modèles, lire hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="f8212-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="f8212-107">Cet article explique comment toocreate un réseau virtuel via le déploiement du Gestionnaire de ressources hello modèle à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8212-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="f8212-108">Vous pouvez également créer un réseau virtuel via le Gestionnaire de ressources à l’aide d’autres outils ou créer un réseau virtuel via le modèle de déploiement classique hello en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="f8212-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8212-109">Portail</span><span class="sxs-lookup"><span data-stu-id="f8212-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="f8212-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8212-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="f8212-111">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="f8212-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="f8212-112">Modèle</span><span class="sxs-lookup"><span data-stu-id="f8212-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="f8212-113">Portail (classique)</span><span class="sxs-lookup"><span data-stu-id="f8212-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="f8212-114">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="f8212-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="f8212-115">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="f8212-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="f8212-116">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f8212-116">Create a virtual network</span></span>

<span data-ttu-id="f8212-117">toocreate étapes d’un réseau virtuel à l’aide de PowerShell, hello complet suivant :</span><span class="sxs-lookup"><span data-stu-id="f8212-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="f8212-118">Installer et configurer Azure PowerShell, en suivant les étapes de hello Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.</span><span class="sxs-lookup"><span data-stu-id="f8212-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="f8212-119">Si nécessaire, créez un groupe de ressources, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f8212-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="f8212-120">Dans le cadre de ce scénario, créez un groupe de ressources appelé *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="f8212-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="f8212-121">Pour plus d’informations sur les groupes de ressources, consultez [Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8212-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="f8212-122">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f8212-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="f8212-123">Créez un réseau virtuel appelé *TestVNet* :</span><span class="sxs-lookup"><span data-stu-id="f8212-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="f8212-124">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f8212-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="f8212-125">Stocker l’objet de réseau virtuel hello dans une variable :</span><span class="sxs-lookup"><span data-stu-id="f8212-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="f8212-126">Vous pouvez combiner les étapes 3 et 4 en exécutant `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="f8212-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="f8212-127">Ajoutez une variable de réseau virtuel nouveau sous-réseau toohello :</span><span class="sxs-lookup"><span data-stu-id="f8212-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="f8212-128">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f8212-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="f8212-129">Répétez l’étape 5 ci-dessus pour chaque sous-réseau souhaité toocreate.</span><span class="sxs-lookup"><span data-stu-id="f8212-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="f8212-130">Hello de commande suivant crée hello *principal* sous-réseau pour le scénario de hello :</span><span class="sxs-lookup"><span data-stu-id="f8212-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="f8212-131">Bien que vous créez des sous-réseaux, ils actuellement existent dans Bonjour tooretrieve utilisé de variable locale Bonjour réseau virtuel que vous créez à l’étape 4 ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f8212-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="f8212-132">toosave tooAzure de modifications hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f8212-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="f8212-133">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f8212-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="f8212-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8212-134">Next steps</span></span>

<span data-ttu-id="f8212-135">Découvrez comment tooconnect :</span><span class="sxs-lookup"><span data-stu-id="f8212-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="f8212-136">Un réseau virtuel tooa de machine virtuelle (VM) en lisant hello [créer une machine virtuelle Windows](../virtual-machines/virtual-machines-windows-ps-create.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="f8212-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="f8212-137">Au lieu de créer un réseau virtuel et un sous-réseau dans les étapes de hello d’articles de hello, vous pouvez sélectionner un réseau virtuel existant et le sous-réseau tooconnect une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f8212-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="f8212-138">Hello des réseaux virtuels tooother de réseau virtuel en lisant hello [connecter des réseaux virtuels](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="f8212-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="f8212-139">Hello réseau virtuel tooan réseau local à l’aide d’un réseau privé virtuel (VPN) site à site ou un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f8212-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="f8212-140">Découvrez comment en lecture hello [connecter un réseau local de tooan de réseau virtuel à l’aide d’un VPN de site à site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) et [lier un circuit ExpressRoute de tooan réseau virtuel](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span><span class="sxs-lookup"><span data-stu-id="f8212-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
