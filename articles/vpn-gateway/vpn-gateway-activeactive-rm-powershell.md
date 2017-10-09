---
title: "Configurer des connexions VPN S2S en mode actif/actif pour des passerelles VPN : Azure Resource Manager : PowerShell | Microsoft Docs"
description: "Cet article vous guide dans la configuration de connexions en mode actif/actif avec des passerelles VPN Azure à l’aide d’Azure Resource Manager et de PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="f412f-103">Configurer des connexions VPN S2S en mode actif/actif avec des passerelles VPN Azure</span><span class="sxs-lookup"><span data-stu-id="f412f-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="f412f-104">Cet article vous assiste hello étapes toocreate actif entre différents locaux et les connexions au réseau à l’aide du modèle de déploiement du Gestionnaire de ressources hello et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f412f-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="f412f-105">À propos des connexions intersites hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="f412f-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="f412f-106">tooachieve haute disponibilité pour intersite et la connectivité de réseau virtuel à réseau virtuel, vous devez déployer plusieurs passerelles VPN et établir plusieurs connexions parallèles entre les réseaux Azure.</span><span class="sxs-lookup"><span data-stu-id="f412f-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="f412f-107">Pour une vue d’ensemble des options de connectivité et de la topologie, voir [Configuration haute disponibilité pour la connectivité entre réseaux locaux et entre réseaux virtuels](vpn-gateway-highlyavailable.md) .</span><span class="sxs-lookup"><span data-stu-id="f412f-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="f412f-108">Cet article fournit des instructions de hello tooset d’un actif entre différents locaux connexion VPN et connexion actif entre deux réseaux virtuels :</span><span class="sxs-lookup"><span data-stu-id="f412f-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="f412f-109">Partie 1 : créer et configurer votre passerelle VPN Azure en mode actif/actif</span><span class="sxs-lookup"><span data-stu-id="f412f-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="f412f-110">Partie 2 : établir des connexions intersites en mode actif/actif</span><span class="sxs-lookup"><span data-stu-id="f412f-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="f412f-111">Partie 3 : établir des connexions de réseau virtuel à réseau virtuel en mode actif/actif</span><span class="sxs-lookup"><span data-stu-id="f412f-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="f412f-112">Partie 4 : mettre à jour une passerelle existante entre les modes actif/actif et actif/passif</span><span class="sxs-lookup"><span data-stu-id="f412f-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="f412f-113">Vous pouvez combiner ces toobuild ensemble une topologie de réseau plus complexe, hautement disponible qui répond à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f412f-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f412f-114">Notez que le mode actif / actif hello utilise hello uniquement après les références (SKU) :</span><span class="sxs-lookup"><span data-stu-id="f412f-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="f412f-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="f412f-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="f412f-116">HigPerformance (pour les anciennes références héritées)</span><span class="sxs-lookup"><span data-stu-id="f412f-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="f412f-117"><a name ="aagateway"></a>Partie 1 : créer et configurer des passerelles VPN en mode actif/actif</span><span class="sxs-lookup"><span data-stu-id="f412f-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="f412f-118">Hello suit va configurer votre passerelle VPN Azure dans les modes actif / actif.</span><span class="sxs-lookup"><span data-stu-id="f412f-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="f412f-119">Hello principales différences entre les passerelles hello actif-actif et de type actif / passif :</span><span class="sxs-lookup"><span data-stu-id="f412f-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="f412f-120">Vous devez toocreate les deux configurations IP de la passerelle avec deux adresses IP publiques</span><span class="sxs-lookup"><span data-stu-id="f412f-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="f412f-121">Vous devez définir indicateur EnableActiveActiveFeature de hello</span><span class="sxs-lookup"><span data-stu-id="f412f-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="f412f-122">passerelle de Hello référence (SKU) doit être VpnGw1, VpnGw2, VpnGw3 ou hautes performances (hérité SKU).</span><span class="sxs-lookup"><span data-stu-id="f412f-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="f412f-123">Hello autres propriétés sont hello même en tant que passerelles d’actif-actif hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="f412f-124">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f412f-124">Before you begin</span></span>
* <span data-ttu-id="f412f-125">Assurez-vous de disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f412f-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="f412f-126">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f412f-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f412f-127">Vous aurez besoin des applets de commande Azure Resource Manager PowerShell tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f412f-128">Consultez [vue d’ensemble de Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="f412f-129">Étape 1 – Créer et configurer le réseau virtuel VNet1</span><span class="sxs-lookup"><span data-stu-id="f412f-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="f412f-130">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="f412f-130">1. Declare your variables</span></span>
<span data-ttu-id="f412f-131">Dans cet exercice, nous allons commencer par déclarer les variables.</span><span class="sxs-lookup"><span data-stu-id="f412f-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="f412f-132">exemple Hello ci-dessous déclare les variables de hello en utilisant les valeurs de hello pour cet exercice.</span><span class="sxs-lookup"><span data-stu-id="f412f-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="f412f-133">Être des valeurs de hello tooreplace que par les vôtres lors de la configuration pour la production.</span><span class="sxs-lookup"><span data-stu-id="f412f-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="f412f-134">Vous pouvez utiliser ces variables si vous exécutez via toobecome d’étapes hello familiarisé avec ce type de configuration.</span><span class="sxs-lookup"><span data-stu-id="f412f-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="f412f-135">Modifier les variables de hello, puis copiez et collez dans votre console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f412f-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="f412f-136">2. Se connecter tooyour abonnement et créer un nouveau groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f412f-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="f412f-137">Veillez à que basculer hello de toouse mode tooPowerShell applets de commande Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="f412f-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="f412f-138">Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f412f-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="f412f-139">Ouvrez la console PowerShell et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="f412f-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="f412f-140">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="f412f-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="f412f-141">3. Créer TestVNet1</span><span class="sxs-lookup"><span data-stu-id="f412f-141">3. Create TestVNet1</span></span>
<span data-ttu-id="f412f-142">exemple Hello ci-dessous crée un réseau virtuel nommé TestVNet1 et trois sous-réseaux, GatewaySubnet appelée un, un frontal appelée et un appelée back-end.</span><span class="sxs-lookup"><span data-stu-id="f412f-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="f412f-143">Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="f412f-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="f412f-144">Si vous le nommez autrement, la création de votre passerelle échoue.</span><span class="sxs-lookup"><span data-stu-id="f412f-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="f412f-145">Étape 2 : créer la passerelle VPN de hello pour TestVNet1 avec le mode actif / actif</span><span class="sxs-lookup"><span data-stu-id="f412f-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="f412f-146">1. Créer des adresses IP publiques hello et des configurations IP de passerelle</span><span class="sxs-lookup"><span data-stu-id="f412f-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="f412f-147">Demande deux public adresses toobe toohello alloué passerelle IP que vous allez créer pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f412f-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="f412f-148">Vous allez également définir les sous-réseaux hello et les configurations IP requis.</span><span class="sxs-lookup"><span data-stu-id="f412f-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="f412f-149">2. Créer la passerelle VPN hello configuration actif-actif</span><span class="sxs-lookup"><span data-stu-id="f412f-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="f412f-150">Créer la passerelle de réseau virtuel hello pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="f412f-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="f412f-151">Notez qu’il existe deux entrées GatewayIpConfig et hello EnableActiveActiveFeature indicateur est défini.</span><span class="sxs-lookup"><span data-stu-id="f412f-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="f412f-152">Création d’une passerelle peut prendre un certain temps (45 minutes ou plus toocomplete).</span><span class="sxs-lookup"><span data-stu-id="f412f-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="f412f-153">3. Obtenir les adresses IP publiques hello passerelle et une adresse IP d’homologue BGP de hello</span><span class="sxs-lookup"><span data-stu-id="f412f-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="f412f-154">Une fois que la passerelle de hello est créée, vous devez tooobtain hello BGP homologue adresseIP sur hello passerelle VPN à Azure.</span><span class="sxs-lookup"><span data-stu-id="f412f-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="f412f-155">Cette adresse est nécessaire tooconfigure hello passerelle VPN à Azure comme une paire BGP pour les appareils de votre VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="f412f-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="f412f-156">Utilisez hello suivant d’applets de commande tooshow hello deux adresses IP publiques allouées pour la passerelle VPN et leurs adresses IP d’homologue BGP correspondantes pour chaque instance de passerelle :</span><span class="sxs-lookup"><span data-stu-id="f412f-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

<span data-ttu-id="f412f-157">commande Hello d’adresses IP publiques de hello pour les instances de passerelle de hello et hello les adresses d’homologation BGP correspondantes sont hello identiques.</span><span class="sxs-lookup"><span data-stu-id="f412f-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="f412f-158">Dans cet exemple, la passerelle de hello machine virtuelle avec l’adresse IP publique de 40.112.190.5 utilisera 10.12.255.4 comme adresse d’homologation BGP, et passerelle hello avec 138.91.156.129 utilisera 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="f412f-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="f412f-159">Ces informations sont nécessaires lorsque vous configurez votre local de la connexion de passerelle d’actif-actif toohello les périphériques VPN.</span><span class="sxs-lookup"><span data-stu-id="f412f-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="f412f-160">passerelle de Hello est illustré dans le diagramme de hello ci-dessous avec toutes les adresses :</span><span class="sxs-lookup"><span data-stu-id="f412f-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![active-active-gateway](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="f412f-162">Une fois hello passerelle créée, vous pouvez utiliser cette actif tooestablish passerelle entre différents locaux ou un réseau à connexion.</span><span class="sxs-lookup"><span data-stu-id="f412f-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="f412f-163">les sections suivantes de Hello guidera hello étapes toocomplete hello exercice.</span><span class="sxs-lookup"><span data-stu-id="f412f-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="f412f-164"><a name ="aacrossprem"></a>Partie 2 : établir une connexion intersite en mode actif/actif</span><span class="sxs-lookup"><span data-stu-id="f412f-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="f412f-165">tooestablish une connexion intersite, vous devez toocreate une passerelle de réseau Local de toorepresent votre périphérique VPN sur site et la passerelle VPN Azure tooconnect hello connexion avec la passerelle de réseau local hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="f412f-166">Dans cet exemple, la passerelle VPN Azure de hello est en mode actif-actif.</span><span class="sxs-lookup"><span data-stu-id="f412f-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="f412f-167">Par conséquent, même s’il n'existe qu’un seul localement le périphérique VPN (passerelle de réseau local) et les ressources d’une seule connexion, les deux instances de passerelle VPN Azure établir les tunnels VPN de S2S avec l’appareil local de hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="f412f-168">Avant de poursuivre, vérifiez que vous avez terminé la [Partie 1](#aagateway) de cet exercice.</span><span class="sxs-lookup"><span data-stu-id="f412f-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="f412f-169">Étape 1 : créer et configurer la passerelle de réseau local hello</span><span class="sxs-lookup"><span data-stu-id="f412f-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="f412f-170">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="f412f-170">1. Declare your variables</span></span>
<span data-ttu-id="f412f-171">Cet exercice continue configuration de hello toobuild hello illustrée.</span><span class="sxs-lookup"><span data-stu-id="f412f-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="f412f-172">Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="f412f-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="f412f-173">Quelques toonote des opérations relatives aux paramètres de passerelle de réseau local hello :</span><span class="sxs-lookup"><span data-stu-id="f412f-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="f412f-174">passerelle de réseau local Hello peut être dans hello identiques ou différents emplacements et les ressources de groupe en tant que passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="f412f-175">Cet exemple montre les différents groupes de ressources, mais dans hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="f412f-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="f412f-176">S’il n'existe qu’une seule unité VPN locale comme indiqué ci-dessus, connexion d’actif-actif hello pouvez travailler avec ou sans protocole BGP.</span><span class="sxs-lookup"><span data-stu-id="f412f-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="f412f-177">Cet exemple utilise le protocole BGP pour la connexion intersite de hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="f412f-178">Si le protocole BGP est activé, préfixe hello vous devez toodeclare pour la passerelle de réseau local hello est adresse d’hôte hello de votre adresse IP d’homologue BGP sur votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="f412f-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="f412f-179">Dans ce cas, il s’agit d’un préfixe /32 de « 10.52.255.253/32 ».</span><span class="sxs-lookup"><span data-stu-id="f412f-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="f412f-180">À titre de rappel, vous devez utiliser différents ASN BGP entre vos réseaux locaux et le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="f412f-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="f412f-181">Si elles sont hello même, vous devez toochange votre ASN VNet si votre périphérique VPN sur site utilise déjà hello ASN toopeer avec d’autres voisins BGP.</span><span class="sxs-lookup"><span data-stu-id="f412f-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="f412f-182">2. Créer la passerelle de réseau local hello pour Site5</span><span class="sxs-lookup"><span data-stu-id="f412f-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="f412f-183">Avant de continuer, vérifiez que vous êtes toujours connectée tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="f412f-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="f412f-184">Créer le groupe de ressources hello s’il n’est pas encore créé.</span><span class="sxs-lookup"><span data-stu-id="f412f-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="f412f-185">Étape 2 : connexion de réseau local et la passerelle de réseau virtuel hello</span><span class="sxs-lookup"><span data-stu-id="f412f-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="f412f-186">1. Obtenir hello deux passerelles</span><span class="sxs-lookup"><span data-stu-id="f412f-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="f412f-187">2. Créer hello TestVNet1 tooSite5 connexion</span><span class="sxs-lookup"><span data-stu-id="f412f-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="f412f-188">Dans cette étape, vous allez créer des connexions de hello de TestVNet1 tooSite5_1 avec cette « propriété » définie trop$ True.</span><span class="sxs-lookup"><span data-stu-id="f412f-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="f412f-189">3. Paramètres VPN et BGP pour votre périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="f412f-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="f412f-190">exemple Hello ci-dessous répertorie les paramètres de hello que vous devrez entrer dans hello section de configuration BGP sur l’appareil VPN local pour cet exercice :</span><span class="sxs-lookup"><span data-stu-id="f412f-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="f412f-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="f412f-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="f412f-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="f412f-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="f412f-193">Préfixes tooannounce : (par exemple) 10.51.0.0/16 et 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f412f-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="f412f-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="f412f-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="f412f-195">Azure réseau virtuel BGP IP 1 : 10.12.255.4 pour tunnel too40.112.190.5</span><span class="sxs-lookup"><span data-stu-id="f412f-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="f412f-196">IP de BGP réseau virtuel Azure 2 : 10.12.255.5 pour tunnel too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="f412f-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="f412f-197">Itinéraires statiques : Destination 10.12.255.4/32, saut suivant hello VPN tunnel interface too40.112.190.5 Destination 10.12.255.5/32, saut suivant hello VPN tunnel interface too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="f412f-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="f412f-198">eBGP sauts multiples : Vérifiez l’option de « sauts multiples » hello pour eBGP est activé sur votre appareil si nécessaire</span><span class="sxs-lookup"><span data-stu-id="f412f-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="f412f-199">connexion de Hello doit être établie après que quelques minutes, de la session d’homologation BGP de hello démarrera une fois établie hello connexion IPsec.</span><span class="sxs-lookup"><span data-stu-id="f412f-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="f412f-200">Cet exemple a configuré jusqu'à présent pas qu’un périphérique VPN local, aboutissant à un diagramme hello indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f412f-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="f412f-202">Étape 3 : deux local VPN des appareils toohello actif VPN passerelle de connexion</span><span class="sxs-lookup"><span data-stu-id="f412f-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="f412f-203">Si vous avez deux périphériques VPN au hello même local réseau, vous pouvez obtenir une redondance double en connexion hello Azure toohello deuxième VPN périphérique de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="f412f-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="f412f-204">1. Créer un deuxième passerelle de réseau local hello pour Site5</span><span class="sxs-lookup"><span data-stu-id="f412f-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="f412f-205">Notez qu’adresse d’homologation BGP pour la passerelle de réseau local hello deuxième adresse IP de passerelle hello et préfixe d’adresse doivent se chevauchent pas avec la passerelle de réseau local précédente hello pour hello même local réseau.</span><span class="sxs-lookup"><span data-stu-id="f412f-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="f412f-206">2. Se connecter hello réseau virtuel et la passerelle hello deuxième réseau local</span><span class="sxs-lookup"><span data-stu-id="f412f-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="f412f-207">Créer des connexions de hello à partir de TestVNet1 tooSite5_2 avec cette « propriété » définie trop$ True</span><span class="sxs-lookup"><span data-stu-id="f412f-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="f412f-208">3. Paramètres VPN et BGP pour votre deuxième périphérique VPN local</span><span class="sxs-lookup"><span data-stu-id="f412f-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="f412f-209">De même, paramètres de hello listes ci-dessous, vous devrez entrer dans périphérique VPN de la deuxième hello :</span><span class="sxs-lookup"><span data-stu-id="f412f-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="f412f-210">Une fois la connexion de hello (tunnels) sont établies, vous aurez deux périphériques VPN redondant et tunnels de connexion de votre réseau local et le Azure :</span><span class="sxs-lookup"><span data-stu-id="f412f-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="f412f-212"><a name ="aav2v"></a>Partie 3 : établir une connexion de réseau virtuel à réseau virtuel en mode actif/actif</span><span class="sxs-lookup"><span data-stu-id="f412f-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="f412f-213">Cette section décrit comment créer une connexion de réseau virtuel à réseau virtuel en mode actif/actif avec le protocole BGP.</span><span class="sxs-lookup"><span data-stu-id="f412f-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="f412f-214">instructions Hello ci-dessous continuent des étapes précédentes de hello répertoriés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f412f-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="f412f-215">Vous devez effectuer [partie 1](#aagateway) toocreate hello passerelle VPN avec protocole BGP et configurer TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="f412f-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="f412f-216">Étape 1 - créer TestVNet2 et hello la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="f412f-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="f412f-217">Il est important toomake que l’espace d’adressage IP hello du nouveau réseau virtuel hello TestVNet2, ne se chevauche pas avec les plages de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f412f-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="f412f-218">Dans cet exemple, les réseaux virtuels hello appartiennent toohello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="f412f-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="f412f-219">Vous pouvez configurer des connexions de réseau virtuel à réseau virtuel entre différents abonnements ; reportez-vous trop[configurer une connexion réseau à](vpn-gateway-vnet-vnet-rm-ps.md) toolearn plus en détail.</span><span class="sxs-lookup"><span data-stu-id="f412f-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="f412f-220">Assurez-vous que vous ajoutez hello »-cette propriété $True » lorsque la création d’hello connexions tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="f412f-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="f412f-221">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="f412f-221">1. Declare your variables</span></span>
<span data-ttu-id="f412f-222">Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="f412f-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="f412f-223">2. Créer TestVNet2 hello nouveau groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f412f-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="f412f-224">3. Créer de passerelle VPN d’actif hello pour TestVNet2</span><span class="sxs-lookup"><span data-stu-id="f412f-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="f412f-225">Demande deux public adresses toobe toohello alloué passerelle IP que vous allez créer pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f412f-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="f412f-226">Vous allez également définir les sous-réseaux hello et les configurations IP requis.</span><span class="sxs-lookup"><span data-stu-id="f412f-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="f412f-227">Créer la passerelle VPN de hello hello comme nombre et hello indicateur de « EnableActiveActiveFeature ».</span><span class="sxs-lookup"><span data-stu-id="f412f-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="f412f-228">Notez que vous devez remplacer la valeur par défaut de hello ASN vos passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="f412f-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="f412f-229">Hello homologations pour hello connectés à des réseaux virtuels doivent être différents tooenable BGP et le routage de transit.</span><span class="sxs-lookup"><span data-stu-id="f412f-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="f412f-230">Étape 2 : se connecter les passerelles TestVNet1 et TestVNet2 hello</span><span class="sxs-lookup"><span data-stu-id="f412f-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="f412f-231">Dans cet exemple, les deux passerelles sont Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="f412f-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="f412f-232">Vous pouvez effectuer cette étape Bonjour même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f412f-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="f412f-233">1. Accéder aux deux passerelles</span><span class="sxs-lookup"><span data-stu-id="f412f-233">1. Get both gateways</span></span>
<span data-ttu-id="f412f-234">Assurez-vous de vous connecter et connectez tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="f412f-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="f412f-235">2. Créer les deux connexions</span><span class="sxs-lookup"><span data-stu-id="f412f-235">2. Create both connections</span></span>
<span data-ttu-id="f412f-236">Dans cette étape, vous allez créer une connexion hello de TestVNet1 tooTestVNet2, hello de TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="f412f-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="f412f-237">Être tooenable que BGP pour les deux connexions.</span><span class="sxs-lookup"><span data-stu-id="f412f-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="f412f-238">Après avoir effectué ces étapes, les connexions hello établit dans quelques minutes et session d’homologation BGP de hello seront d’une fois la connexion de hello au réseau s’est terminée avec redondance double :</span><span class="sxs-lookup"><span data-stu-id="f412f-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="f412f-240"><a name ="aaupdate"></a>Partie 4 : mettre à jour une passerelle existante entre les modes actif/actif et actif/passif</span><span class="sxs-lookup"><span data-stu-id="f412f-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="f412f-241">dernière section de Hello décrivent comment vous pouvez configurer une passerelle VPN Azure existante à partir du mode tooactive active de type actif / passif, ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="f412f-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="f412f-242">Cette section inclut hello étapes tooresize une référence (SKU) hérité (ancienne version) d’une passerelle VPN déjà créée à partir de tooHighPerformance Standard.</span><span class="sxs-lookup"><span data-stu-id="f412f-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="f412f-243">Ces étapes ne mettez pas à niveau un ancien tooone de référence (SKU) hérité de hello nouvelles références SKU.</span><span class="sxs-lookup"><span data-stu-id="f412f-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="f412f-244">Configurer une passerelle de tooactive-active de type actif / passif</span><span class="sxs-lookup"><span data-stu-id="f412f-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="f412f-245">1. Paramètres de passerelle</span><span class="sxs-lookup"><span data-stu-id="f412f-245">1. Gateway parameters</span></span>
<span data-ttu-id="f412f-246">Bonjour à l’exemple suivant convertit une passerelle de type actif / passif une passerelle d’actif-actif.</span><span class="sxs-lookup"><span data-stu-id="f412f-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="f412f-247">Vous devez toocreate une autre adresse IP publique, puis ajoutez une deuxième configuration IP de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="f412f-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="f412f-248">Ci-dessous montre hello paramètres utilisés :</span><span class="sxs-lookup"><span data-stu-id="f412f-248">Below shows hello parameters used:</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="f412f-249">2. Créer une adresse IP publique hello, puis ajouter hello deuxième passerelle IP configuration</span><span class="sxs-lookup"><span data-stu-id="f412f-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="f412f-250">3. Activer la passerelle de hello de mise à jour et en mode actif / actif</span><span class="sxs-lookup"><span data-stu-id="f412f-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="f412f-251">Vous devez définir l’objet de passerelle hello dans la mise à jour réelle PowerShell tootrigger hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="f412f-252">Hello référence (SKU) de la passerelle de réseau virtuel hello doit également être modifié tooHighPerformance (redimensionnée), car il a été créé précédemment comme norme.</span><span class="sxs-lookup"><span data-stu-id="f412f-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="f412f-253">Cette mise à jour peut prendre 30 minutes too45.</span><span class="sxs-lookup"><span data-stu-id="f412f-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="f412f-254">Configurer une passerelle de secours tooactive actif-actif</span><span class="sxs-lookup"><span data-stu-id="f412f-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="f412f-255">1. Paramètres de passerelle</span><span class="sxs-lookup"><span data-stu-id="f412f-255">1. Gateway parameters</span></span>
<span data-ttu-id="f412f-256">Utilisez hello même paramètres comme indiqué ci-dessus, obtenir le nom de hello de hello IP configuration tooremove.</span><span class="sxs-lookup"><span data-stu-id="f412f-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="f412f-257">2. Supprimer la configuration IP de passerelle hello et désactiver le mode actif / actif hello</span><span class="sxs-lookup"><span data-stu-id="f412f-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="f412f-258">De même, vous devez définir objet de passerelle hello dans la mise à jour réelle PowerShell tootrigger hello.</span><span class="sxs-lookup"><span data-stu-id="f412f-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="f412f-259">Cette mise à jour peut prendre too30 trop 45 minutes.</span><span class="sxs-lookup"><span data-stu-id="f412f-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f412f-260">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f412f-260">Next steps</span></span>
<span data-ttu-id="f412f-261">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="f412f-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="f412f-262">Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="f412f-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
