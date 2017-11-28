---
title: "Configurer BGP sur des passerelles VPN Azure : Resource Manager : PowerShell | Microsoft Docs"
description: "Cet article vous guide dans la configuration de BGP avec des passerelles VPN Azure à l’aide d’Azure Resource Manager et de PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="30886-103">Comment tooconfigure BGP sur les passerelles VPN Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="30886-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="30886-104">Cet article vous assiste hello étapes tooenable BGP sur une connexion de Site à Site (S2S) VPN intersite et une connexion au réseau à l’aide du modèle de déploiement du Gestionnaire de ressources hello et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30886-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="30886-105">À propos du protocole BGP</span><span class="sxs-lookup"><span data-stu-id="30886-105">About BGP</span></span>
<span data-ttu-id="30886-106">BGP est hello protocole de routage standard couramment utilisé dans hello Internet tooexchange routage et l’accessibilité des informations entre deux ou plusieurs réseaux.</span><span class="sxs-lookup"><span data-stu-id="30886-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="30886-107">Protocole BGP permet les passerelles VPN Azure hello et vos périphériques VPN local, appelés homologues BGP ou voisins, tooexchange « itinéraires » informe les deux passerelles sur la disponibilité de hello et l’accessibilité pour les préfixes toogo via des passerelles de hello ou routeurs impliqués.</span><span class="sxs-lookup"><span data-stu-id="30886-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="30886-108">Protocole BGP peut également activer le routage de transit entre plusieurs réseaux en propageant les itinéraires une passerelle BGP apprend à partir d’un tooall d’homologue BGP autres homologues BGP.</span><span class="sxs-lookup"><span data-stu-id="30886-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="30886-109">Consultez [vue d’ensemble du protocole BGP avec les passerelles VPN Azure](vpn-gateway-bgp-overview.md) pour plus d’informations sur les avantages du protocole BGP et toounderstand hello technique configuration requise et considérations relatives à l’aide du protocole BGP.</span><span class="sxs-lookup"><span data-stu-id="30886-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="30886-110">Prise en main de BGP sur les passerelles VPN Azure</span><span class="sxs-lookup"><span data-stu-id="30886-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="30886-111">Cet article vous guide tout au long de hello de toodo étapes hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="30886-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="30886-112">Partie 1 - Activer BGP sur votre passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="30886-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="30886-113">Partie 2 - Établir une connexion intersite avec BGP</span><span class="sxs-lookup"><span data-stu-id="30886-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="30886-114">Partie 3 - Établir une connexion de réseau virtuel à réseau virtuel avec BGP</span><span class="sxs-lookup"><span data-stu-id="30886-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="30886-115">Chaque partie d’instructions de hello constitue un bloc de construction de base pour activer BGP de la connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="30886-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="30886-116">Si vous effectuez toutes les trois parties, vous créez une topologie de hello comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="30886-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![Topologie BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="30886-118">Vous pouvez combiner des parties de toobuild ensemble un réseau de transit plus complexes, cascade, qui répond à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="30886-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="30886-119"><a name ="enablebgp"></a>Partie 1 : configurer le protocole BGP sur hello passerelle VPN à Azure</span><span class="sxs-lookup"><span data-stu-id="30886-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="30886-120">étapes de configuration Hello configurer hello paramètres BGP de la passerelle VPN Azure de hello comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="30886-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![Passerelle BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="30886-122">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="30886-122">Before you begin</span></span>
* <span data-ttu-id="30886-123">Assurez-vous de disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="30886-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="30886-124">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30886-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="30886-125">Installer les applets de commande Azure Resource Manager PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="30886-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="30886-126">Pour plus d’informations sur l’installation des applets de commande PowerShell hello, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="30886-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="30886-127">Étape 1 – Créer et configurer le réseau virtuel VNet1</span><span class="sxs-lookup"><span data-stu-id="30886-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="30886-128">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="30886-128">1. Declare your variables</span></span>
<span data-ttu-id="30886-129">Dans cet exercice, nous allons commencer par déclarer les variables.</span><span class="sxs-lookup"><span data-stu-id="30886-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="30886-130">Hello exemple suivant déclare les variables hello en utilisant les valeurs de hello pour cet exercice.</span><span class="sxs-lookup"><span data-stu-id="30886-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="30886-131">Être des valeurs de hello tooreplace que par les vôtres lors de la configuration pour la production.</span><span class="sxs-lookup"><span data-stu-id="30886-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="30886-132">Vous pouvez utiliser ces variables si vous exécutez via toobecome d’étapes hello familiarisé avec ce type de configuration.</span><span class="sxs-lookup"><span data-stu-id="30886-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="30886-133">Modifier les variables de hello, puis copiez et collez dans votre console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30886-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="30886-134">2. Se connecter tooyour abonnement et créer un nouveau groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="30886-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="30886-135">toouse hello applets de commande Gestionnaire de ressources, veillez à basculer en mode de tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="30886-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="30886-136">Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="30886-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="30886-137">Ouvrez la console PowerShell et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="30886-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="30886-138">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="30886-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="30886-139">3. Créer TestVNet1</span><span class="sxs-lookup"><span data-stu-id="30886-139">3. Create TestVNet1</span></span>
<span data-ttu-id="30886-140">Hello exemple suivant crée un réseau virtuel nommé TestVNet1 et trois sous-réseaux, GatewaySubnet appelée un, un frontal appelée et un appelée back-end.</span><span class="sxs-lookup"><span data-stu-id="30886-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="30886-141">Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="30886-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="30886-142">Si vous le nommez autrement, la création de votre passerelle échoue.</span><span class="sxs-lookup"><span data-stu-id="30886-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="30886-143">Étape 2 : créer hello passerelle VPN pour TestVNet1 avec des paramètres de protocole BGP</span><span class="sxs-lookup"><span data-stu-id="30886-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="30886-144">1. Créer des configurations IP et le sous-réseau hello</span><span class="sxs-lookup"><span data-stu-id="30886-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="30886-145">Demander une passerelle publique de toohello alloué toobe adresse IP que vous allez créer pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="30886-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="30886-146">Vous allez également définir le sous-réseau de hello requis et les configurations IP.</span><span class="sxs-lookup"><span data-stu-id="30886-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="30886-147">2. Créer la passerelle VPN hello hello en tant que nombre</span><span class="sxs-lookup"><span data-stu-id="30886-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="30886-148">Créer la passerelle de réseau virtuel hello pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="30886-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="30886-149">BGP requiert une basée sur un itinéraire passerelle VPN et également hello Ajout paramètre, - Asn tooset hello ASN (en tant que nombre) pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="30886-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="30886-150">Si vous ne définissez pas de paramètre ASN hello, ASN 65515 est affecté.</span><span class="sxs-lookup"><span data-stu-id="30886-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="30886-151">Création d’une passerelle peut prendre un certain temps (30 minutes ou plus toocomplete).</span><span class="sxs-lookup"><span data-stu-id="30886-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="30886-152">3. Obtenir hello Azure BGP homologue IP adresse</span><span class="sxs-lookup"><span data-stu-id="30886-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="30886-153">Une fois que la passerelle de hello est créée, vous devez tooobtain hello BGP homologue adresseIP sur hello passerelle VPN à Azure.</span><span class="sxs-lookup"><span data-stu-id="30886-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="30886-154">Cette adresse est nécessaire tooconfigure hello passerelle VPN à Azure comme une paire BGP pour les appareils de votre VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="30886-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="30886-155">la dernière commande Hello montre des configurations de protocole BGP correspondantes de hello sur hello passerelle VPN à Azure ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="30886-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="30886-156">Une fois que la passerelle de hello est créée, vous pouvez utiliser cette passerelle tooestablish entre différents locaux ou réseau à connexion avec BGP.</span><span class="sxs-lookup"><span data-stu-id="30886-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="30886-157">Hello sections suivantes guident hello étapes toocomplete hello exercice.</span><span class="sxs-lookup"><span data-stu-id="30886-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="30886-158"><a name ="crossprembbgp"></a>Partie 2 - Établir une connexion intersite avec BGP</span><span class="sxs-lookup"><span data-stu-id="30886-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="30886-159">tooestablish une connexion intersite, vous devez toocreate une passerelle de réseau Local de toorepresent votre périphérique VPN sur site et la passerelle VPN tooconnect hello connexion avec la passerelle de réseau local hello.</span><span class="sxs-lookup"><span data-stu-id="30886-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="30886-160">Lorsqu’il existe des articles qui vous guident tout au long de ces étapes, cet article contient des paramètres de configuration hello des propriétés supplémentaires requis toospecify hello BGP.</span><span class="sxs-lookup"><span data-stu-id="30886-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![BGP pour une connexion intersite](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="30886-162">Avant de poursuivre, vérifiez que vous avez terminé la [Partie 1](#enablebgp) de cet exercice.</span><span class="sxs-lookup"><span data-stu-id="30886-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="30886-163">Étape 1 : créer et configurer la passerelle de réseau local hello</span><span class="sxs-lookup"><span data-stu-id="30886-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="30886-164">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="30886-164">1. Declare your variables</span></span>

<span data-ttu-id="30886-165">Cet exercice continue de configuration de hello toobuild hello illustrée.</span><span class="sxs-lookup"><span data-stu-id="30886-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="30886-166">Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="30886-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="30886-167">Quelques toonote des opérations relatives aux paramètres de passerelle de réseau local hello :</span><span class="sxs-lookup"><span data-stu-id="30886-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="30886-168">passerelle de réseau local Hello peut être dans hello identiques ou différents emplacements et les ressources de groupe en tant que passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="30886-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="30886-169">Cet exemple les montre dans différents groupes de ressources situés dans différents emplacements.</span><span class="sxs-lookup"><span data-stu-id="30886-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="30886-170">préfixe de minimale Hello nécessaire toodeclare pour la passerelle de réseau local hello est l’adresse d’hôte de hello de votre adresse IP d’homologue BGP sur votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="30886-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="30886-171">Dans ce cas, c’est un préfixe /32 de « 10.52.255.254/32 ».</span><span class="sxs-lookup"><span data-stu-id="30886-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="30886-172">À titre de rappel, vous devez utiliser différents ASN BGP entre vos réseaux locaux et le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="30886-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="30886-173">Si elles sont hello même, vous devez toochange votre ASN VNet si votre périphérique VPN sur site utilise déjà hello ASN toopeer avec d’autres voisins BGP.</span><span class="sxs-lookup"><span data-stu-id="30886-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="30886-174">Avant de continuer, assurez-vous que vous êtes toujours connectée tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="30886-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="30886-175">2. Créer la passerelle de réseau local hello pour Site5</span><span class="sxs-lookup"><span data-stu-id="30886-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="30886-176">Être sûr de groupe de ressources hello toocreate s’il n'est pas créé, avant de créer de passerelle de réseau local hello.</span><span class="sxs-lookup"><span data-stu-id="30886-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="30886-177">Notez hello deux des paramètres supplémentaires pour la passerelle de réseau local hello : Asn et BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="30886-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="30886-178">Étape 2 : connexion de réseau local et la passerelle de réseau virtuel hello</span><span class="sxs-lookup"><span data-stu-id="30886-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="30886-179">1. Obtenir hello deux passerelles</span><span class="sxs-lookup"><span data-stu-id="30886-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="30886-180">2. Créer hello TestVNet1 tooSite5 connexion</span><span class="sxs-lookup"><span data-stu-id="30886-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="30886-181">Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooSite5.</span><span class="sxs-lookup"><span data-stu-id="30886-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="30886-182">Vous devez spécifier «-cette propriété $True » tooenable BGP pour cette connexion.</span><span class="sxs-lookup"><span data-stu-id="30886-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="30886-183">Comme indiqué précédemment, il est possible de toohave connexions BGP et non-BGP pour hello même passerelle VPN à Azure.</span><span class="sxs-lookup"><span data-stu-id="30886-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="30886-184">À moins que le protocole BGP est activé dans la propriété de connexion hello, Azure n’active pas BGP pour cette connexion même si les paramètres BGP sont déjà configurés sur les deux passerelles.</span><span class="sxs-lookup"><span data-stu-id="30886-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="30886-185">Hello exemple suivant répertorie les paramètres de hello que vous entrez dans la section de configuration BGP de hello sur l’appareil VPN local pour cet exercice :</span><span class="sxs-lookup"><span data-stu-id="30886-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="30886-186">Hello est établie après quelques minutes et le démarrage de session d’homologation hello BGP une fois établie hello connexion IPsec.</span><span class="sxs-lookup"><span data-stu-id="30886-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="30886-187"><a name ="v2vbgp"></a>Partie 3 - Établir une connexion de réseau virtuel à réseau virtuel avec BGP</span><span class="sxs-lookup"><span data-stu-id="30886-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="30886-188">Cette section ajoute une connexion au réseau avec protocole BGP, comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="30886-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![BGP pour une connexion de réseau virtuel à réseau virtuel](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="30886-190">continue de Hello suivant les instructions des étapes précédentes de hello.</span><span class="sxs-lookup"><span data-stu-id="30886-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="30886-191">Vous devez effectuer [partie I](#enablebgp) toocreate hello passerelle VPN avec protocole BGP et configurer TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="30886-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="30886-192">Étape 1 - créer TestVNet2 et hello la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="30886-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="30886-193">Il est important toomake que l’espace d’adressage IP hello du nouveau réseau virtuel hello TestVNet2, ne se chevauche pas avec les plages de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="30886-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="30886-194">Dans cet exemple, les réseaux virtuels hello appartiennent toohello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="30886-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="30886-195">Vous pouvez configurer les connexions de réseau virtuel à réseau virtuel entre différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="30886-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="30886-196">Pour plus d'informations, voir [Configurer une connexion de réseau virtuel à réseau virtuel](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="30886-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="30886-197">Assurez-vous que vous ajoutez hello »-cette propriété $True » lorsque la création d’hello connexions tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="30886-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="30886-198">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="30886-198">1. Declare your variables</span></span>

<span data-ttu-id="30886-199">Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="30886-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="30886-200">2. Créer TestVNet2 hello nouveau groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="30886-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="30886-201">3. Créer la passerelle VPN de hello pour TestVNet2 avec des paramètres de protocole BGP</span><span class="sxs-lookup"><span data-stu-id="30886-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="30886-202">Demander une publique IP adresse toobe toohello alloué passerelle vous allez créer pour votre réseau virtuel et définissez le sous-réseau de hello requis et les configurations IP.</span><span class="sxs-lookup"><span data-stu-id="30886-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="30886-203">Créer la passerelle VPN hello hello en tant que nombre.</span><span class="sxs-lookup"><span data-stu-id="30886-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="30886-204">Vous devez remplacer la valeur par défaut de hello ASN vos passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="30886-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="30886-205">Hello homologations pour hello connectés à des réseaux virtuels doivent être différents tooenable BGP et le routage de transit.</span><span class="sxs-lookup"><span data-stu-id="30886-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="30886-206">Étape 2 : se connecter les passerelles TestVNet1 et TestVNet2 hello</span><span class="sxs-lookup"><span data-stu-id="30886-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="30886-207">Dans cet exemple, les deux passerelles sont Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="30886-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="30886-208">Vous pouvez effectuer cette étape Bonjour même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30886-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="30886-209">1. Accéder aux deux passerelles</span><span class="sxs-lookup"><span data-stu-id="30886-209">1. Get both gateways</span></span>

<span data-ttu-id="30886-210">Assurez-vous de vous connecter et connectez tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="30886-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="30886-211">2. Créer les deux connexions</span><span class="sxs-lookup"><span data-stu-id="30886-211">2. Create both connections</span></span>

<span data-ttu-id="30886-212">Dans cette étape, vous créer connexion hello de TestVNet1 tooTestVNet2, hello de TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="30886-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="30886-213">Être tooenable que BGP pour les deux connexions.</span><span class="sxs-lookup"><span data-stu-id="30886-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="30886-214">Après avoir effectué ces étapes, hello est établie après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="30886-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="30886-215">session d’homologation BGP de Hello est une fois hello réseau à connexion terminée.</span><span class="sxs-lookup"><span data-stu-id="30886-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="30886-216">Une fois tous les trois parties de cet exercice, vous avez établi hello suivant la topologie du réseau :</span><span class="sxs-lookup"><span data-stu-id="30886-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![BGP pour une connexion de réseau virtuel à réseau virtuel](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="30886-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30886-218">Next steps</span></span>

<span data-ttu-id="30886-219">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="30886-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="30886-220">Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="30886-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
