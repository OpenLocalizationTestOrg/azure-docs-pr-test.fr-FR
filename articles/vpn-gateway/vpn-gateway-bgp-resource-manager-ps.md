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
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="56d78-103">Configurer BGP sur des passerelles VPN Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="56d78-103">How to configure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="56d78-104">Cet article vous guide pas à pas dans l’activation de BGP sur une connexion VPN de site à site (S2S) et une connexion de réseau virtuel à réseau virtuel, à l’aide du modèle de déploiement de Resource Manager et de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56d78-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="56d78-105">À propos du protocole BGP</span><span class="sxs-lookup"><span data-stu-id="56d78-105">About BGP</span></span>
<span data-ttu-id="56d78-106">BGP est le protocole de routage standard couramment utilisé sur Internet pour échanger des informations de routage et d’accessibilité entre plusieurs réseaux.</span><span class="sxs-lookup"><span data-stu-id="56d78-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="56d78-107">Il permet aux passerelles VPN Azure et à vos périphériques VPN locaux (appelés voisins ou homologues BGP) d’échanger des « itinéraires » informant les deux passerelles sur la disponibilité et l’accessibilité de ces préfixes à travers les passerelles ou routeurs impliqués.</span><span class="sxs-lookup"><span data-stu-id="56d78-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="56d78-108">Le protocole BGP assure également le routage de transit entre plusieurs réseaux en propageant les itinéraires qu’une passerelle BGP obtient d’un homologue BGP à tous les autres homologues BGP.</span><span class="sxs-lookup"><span data-stu-id="56d78-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span>

<span data-ttu-id="56d78-109">Pour plus d’informations sur les avantages de BGP et les exigences techniques et considérations d’utilisation de BGP, consultez [Vue d’ensemble du protocole BGP avec les passerelles VPN Azure](vpn-gateway-bgp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56d78-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="56d78-110">Prise en main de BGP sur les passerelles VPN Azure</span><span class="sxs-lookup"><span data-stu-id="56d78-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="56d78-111">Cet article détaille les étapes permettant d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="56d78-111">This article walks you through the steps to do the following tasks:</span></span>

* [<span data-ttu-id="56d78-112">Partie 1 - Activer BGP sur votre passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="56d78-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="56d78-113">Partie 2 - Établir une connexion intersite avec BGP</span><span class="sxs-lookup"><span data-stu-id="56d78-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="56d78-114">Partie 3 - Établir une connexion de réseau virtuel à réseau virtuel avec BGP</span><span class="sxs-lookup"><span data-stu-id="56d78-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="56d78-115">Chaque partie des instructions constitue un bloc de base pour activer BGP dans votre connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="56d78-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="56d78-116">Si vous terminez ces trois parties, vous générez la topologie comme sur le diagramme suivant :</span><span class="sxs-lookup"><span data-stu-id="56d78-116">If you complete all three parts, you build the topology as shown in the following diagram:</span></span>

![Topologie BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="56d78-118">Vous pouvez les combiner pour créer un réseau de transit plus complexe, à plusieurs tronçons, qui répond à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="56d78-118">You can combine parts together to build a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="56d78-119"><a name ="enablebgp"></a>Partie 1 – Configurer BGP sur la passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="56d78-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on the Azure VPN Gateway</span></span>
<span data-ttu-id="56d78-120">Les étapes suivantes configurent les paramètres BGP de la passerelle VPN Azure comme indiqué dans le diagramme ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="56d78-120">The configuration steps set up the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span></span>

![Passerelle BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="56d78-122">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="56d78-122">Before you begin</span></span>
* <span data-ttu-id="56d78-123">Assurez-vous de disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="56d78-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="56d78-124">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56d78-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="56d78-125">Installez les applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="56d78-125">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="56d78-126">Pour plus d’informations sur l’installation des applets de commande PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="56d78-126">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="56d78-127">Étape 1 – Créer et configurer le réseau virtuel VNet1</span><span class="sxs-lookup"><span data-stu-id="56d78-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="56d78-128">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="56d78-128">1. Declare your variables</span></span>
<span data-ttu-id="56d78-129">Dans cet exercice, nous allons commencer par déclarer les variables.</span><span class="sxs-lookup"><span data-stu-id="56d78-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="56d78-130">L’exemple suivant déclare les variables avec les valeurs de cet exercice.</span><span class="sxs-lookup"><span data-stu-id="56d78-130">The following example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="56d78-131">Veillez à les remplacer par vos valeurs lors de la configuration dans un contexte de production.</span><span class="sxs-lookup"><span data-stu-id="56d78-131">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="56d78-132">Vous pouvez utiliser ces variables si vous exécutez la procédure pour vous familiariser avec ce type de configuration.</span><span class="sxs-lookup"><span data-stu-id="56d78-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="56d78-133">Modifiez les variables, puis copiez et collez-les dans la console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56d78-133">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="56d78-134">2. Se connecter à votre abonnement et créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="56d78-134">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="56d78-135">Pour utiliser les applets de commande Resource Manager, passez au mode PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56d78-135">To use the Resource Manager cmdlets, Make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="56d78-136">Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="56d78-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="56d78-137">Ouvrez la console PowerShell et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="56d78-137">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="56d78-138">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="56d78-138">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="56d78-139">3. Créer TestVNet1</span><span class="sxs-lookup"><span data-stu-id="56d78-139">3. Create TestVNet1</span></span>
<span data-ttu-id="56d78-140">L’exemple suivant crée un réseau virtuel nommé TestVNet1 et trois sous-réseaux nommés GatewaySubnet, FrontEnd et Backend.</span><span class="sxs-lookup"><span data-stu-id="56d78-140">The following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="56d78-141">Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="56d78-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="56d78-142">Si vous le nommez autrement, la création de votre passerelle échoue.</span><span class="sxs-lookup"><span data-stu-id="56d78-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="56d78-143">Étape 2 – Créer la passerelle VPN de TestVNet1 avec les paramètres BGP</span><span class="sxs-lookup"><span data-stu-id="56d78-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-the-ip-and-subnet-configurations"></a><span data-ttu-id="56d78-144">1. Créer les configurations IP et de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="56d78-144">1. Create the IP and subnet configurations</span></span>
<span data-ttu-id="56d78-145">Demandez l’allocation d’une adresse IP publique à la passerelle que vous allez créer pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="56d78-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="56d78-146">Vous allez également définir les configurations IP et sous-réseau requises.</span><span class="sxs-lookup"><span data-stu-id="56d78-146">You'll also define the required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a><span data-ttu-id="56d78-147">2. Créer la passerelle VPN avec le numéro AS</span><span class="sxs-lookup"><span data-stu-id="56d78-147">2. Create the VPN gateway with the AS number</span></span>
<span data-ttu-id="56d78-148">Créez la passerelle de réseau virtuel pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="56d78-148">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="56d78-149">BGP requiert une passerelle VPN basée sur l’itinéraire ainsi que le paramètre d’ajout, - Asn, pour définir l’ASN (numéro AS) de TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="56d78-149">BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="56d78-150">Si vous ne définissez pas le paramètre ASN, le numéro ASN 65515 est attribué.</span><span class="sxs-lookup"><span data-stu-id="56d78-150">If you do not set the ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="56d78-151">La création d’une passerelle peut prendre un certain temps (30 minutes ou plus).</span><span class="sxs-lookup"><span data-stu-id="56d78-151">Creating a gateway can take a while (30 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a><span data-ttu-id="56d78-152">3. Obtenir l’adresse IP de l’homologue BGP Azure</span><span class="sxs-lookup"><span data-stu-id="56d78-152">3. Obtain the Azure BGP Peer IP address</span></span>
<span data-ttu-id="56d78-153">Une fois la passerelle créée, vous devez obtenir l’adresse IP de l’homologue BGP sur la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="56d78-153">Once the gateway is created, you need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="56d78-154">Cette adresse est nécessaire pour configurer la passerelle VPN Azure comme un homologue BGP pour vos périphériques VPN locaux.</span><span class="sxs-lookup"><span data-stu-id="56d78-154">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="56d78-155">La dernière commande affiche les configurations BGP correspondantes sur la passerelle VPN Azure ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="56d78-155">The last command shows the corresponding BGP configurations on the Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="56d78-156">Une fois la passerelle créée, vous pouvez l’utiliser pour établir une connexion intersite ou de réseau virtuel à réseau virtuel avec BGP.</span><span class="sxs-lookup"><span data-stu-id="56d78-156">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="56d78-157">Les sections suivantes détaillent les étapes à effectuer pour terminer l’exercice.</span><span class="sxs-lookup"><span data-stu-id="56d78-157">The following sections walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="56d78-158"><a name ="crossprembbgp"></a>Partie 2 - Établir une connexion intersite avec BGP</span><span class="sxs-lookup"><span data-stu-id="56d78-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="56d78-159">Pour établir une connexion intersite, vous devez créer une passerelle de réseau local pour représenter votre périphérique VPN local, et une connexion entre la passerelle VPN et la passerelle du réseau local.</span><span class="sxs-lookup"><span data-stu-id="56d78-159">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the VPN gateway with the local network gateway.</span></span> <span data-ttu-id="56d78-160">Bien qu’il existe des articles qui vous guident tout au long de ces étapes, cet article contient les propriétés supplémentaires nécessaires pour spécifier les paramètres de configuration BGP.</span><span class="sxs-lookup"><span data-stu-id="56d78-160">While there are articles that walk you through these steps, this article contains the additional properties required to specify the BGP configuration parameters.</span></span>

![BGP pour une connexion intersite](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="56d78-162">Avant de poursuivre, vérifiez que vous avez terminé la [Partie 1](#enablebgp) de cet exercice.</span><span class="sxs-lookup"><span data-stu-id="56d78-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="56d78-163">Étape 1 - Créer et configurer la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="56d78-163">Step 1 - Create and configure the local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="56d78-164">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="56d78-164">1. Declare your variables</span></span>

<span data-ttu-id="56d78-165">Cet exercice continue à générer la configuration représentée dans le diagramme.</span><span class="sxs-lookup"><span data-stu-id="56d78-165">This exercise continues to build the configuration shown in the diagram.</span></span> <span data-ttu-id="56d78-166">Veillez à remplacer les valeurs par celles que vous souhaitez utiliser pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="56d78-166">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="56d78-167">Quelques points à noter concernant les paramètres de la passerelle de réseau local :</span><span class="sxs-lookup"><span data-stu-id="56d78-167">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="56d78-168">La passerelle de réseau local peut se trouver dans les mêmes emplacement et groupe de ressources que la passerelle VPN ou dans un emplacement et un groupe de ressources différents.</span><span class="sxs-lookup"><span data-stu-id="56d78-168">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="56d78-169">Cet exemple les montre dans différents groupes de ressources situés dans différents emplacements.</span><span class="sxs-lookup"><span data-stu-id="56d78-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="56d78-170">Le préfixe minimum à déclarer pour la passerelle de réseau local est l’adresse IP hôte de votre homologue BGP sur votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="56d78-170">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="56d78-171">Dans ce cas, c’est un préfixe /32 de « 10.52.255.254/32 ».</span><span class="sxs-lookup"><span data-stu-id="56d78-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="56d78-172">À titre de rappel, vous devez utiliser différents ASN BGP entre vos réseaux locaux et le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="56d78-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="56d78-173">S’ils sont identiques, vous devez modifier l’ASN de votre réseau si votre périphérique VPN local utilise déjà cet ASN pour s’homologuer avec d’autres voisins BGP.</span><span class="sxs-lookup"><span data-stu-id="56d78-173">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

<span data-ttu-id="56d78-174">Avant de continuer, assurez-vous que vous êtes toujours connecté à l’abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="56d78-174">Before you continue, make sure you are still connected to Subscription 1.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="56d78-175">2. Créer la passerelle de réseau local pour le site 5</span><span class="sxs-lookup"><span data-stu-id="56d78-175">2. Create the local network gateway for Site5</span></span>

<span data-ttu-id="56d78-176">Veillez à créer le groupe de ressources (si ce n’est déjà fait) avant la passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="56d78-176">Be sure to create the resource group if it is not created, before you create the local network gateway.</span></span> <span data-ttu-id="56d78-177">Remarquez les deux paramètres supplémentaires pour la passerelle de réseau local : Asn et BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="56d78-177">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="56d78-178">Étape 2 - Connecter la passerelle de réseau virtuel et la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="56d78-178">Step 2 - Connect the VNet gateway and local network gateway</span></span>

#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="56d78-179">1. Obtenir les deux passerelles</span><span class="sxs-lookup"><span data-stu-id="56d78-179">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="56d78-180">2. Créer la connexion entre TestVNet1 et Site5</span><span class="sxs-lookup"><span data-stu-id="56d78-180">2. Create the TestVNet1 to Site5 connection</span></span>

<span data-ttu-id="56d78-181">Dans cette étape, vous allez créer la connexion entre TestVNet1 et Site5.</span><span class="sxs-lookup"><span data-stu-id="56d78-181">In this step, you create the connection from TestVNet1 to Site5.</span></span> <span data-ttu-id="56d78-182">Vous devez spécifier « -EnableBGP $True » pour activer le BGP sur cette connexion.</span><span class="sxs-lookup"><span data-stu-id="56d78-182">You must specify "-EnableBGP $True" to enable BGP for this connection.</span></span> <span data-ttu-id="56d78-183">Comme nous l’avons vu, il est possible d’avoir des connexions BGP et non BGP sur la même passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="56d78-183">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span></span> <span data-ttu-id="56d78-184">À moins que BGP ne soit activé dans la propriété de connexion, Azure n’active pas BGP sur cette connexion même si les paramètres BGP sont déjà configurés sur les deux passerelles.</span><span class="sxs-lookup"><span data-stu-id="56d78-184">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="56d78-185">L’exemple ci-dessous répertorie les paramètres que vous devez saisir dans la section de configuration de BGP de votre périphérique VPN local pour cet exercice :</span><span class="sxs-lookup"><span data-stu-id="56d78-185">The following example lists the parameters you enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="56d78-186">La connexion est établie après quelques minutes, et la session d’homologation BGP débute une fois la connexion IPsec établie.</span><span class="sxs-lookup"><span data-stu-id="56d78-186">The connection is established after a few minutes, and the BGP peering session starts once the IPsec connection is established.</span></span>

## <span data-ttu-id="56d78-187"><a name ="v2vbgp"></a>Partie 3 - Établir une connexion de réseau virtuel à réseau virtuel avec BGP</span><span class="sxs-lookup"><span data-stu-id="56d78-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="56d78-188">Cette section ajoute une connexion de réseau virtuel à réseau virtuel avec le protocole BGP, comme illustré dans le diagramme ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="56d78-188">This section adds a VNet-to-VNet connection with BGP, as shown in the following diagram:</span></span>

![BGP pour une connexion de réseau virtuel à réseau virtuel](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="56d78-190">Ces instructions ci-dessous sont la suite des étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="56d78-190">The following instructions continue from the previous steps.</span></span> <span data-ttu-id="56d78-191">Vous devez terminer la [Partie 1](#enablebgp) pour créer et configurer TestVNet1 et la passerelle VPN avec le protocole BGP.</span><span class="sxs-lookup"><span data-stu-id="56d78-191">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="56d78-192">Étape 1 - Créer TestVNet2 et la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="56d78-192">Step 1 - Create TestVNet2 and the VPN gateway</span></span>

<span data-ttu-id="56d78-193">Il est important de s’assurer que l’espace d’adresse IP du nouveau réseau virtuel, TestVNet2, n’empiète sur aucune de vos plages de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="56d78-193">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="56d78-194">Dans cet exemple, les réseaux virtuels appartiennent au même abonnement.</span><span class="sxs-lookup"><span data-stu-id="56d78-194">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="56d78-195">Vous pouvez configurer les connexions de réseau virtuel à réseau virtuel entre différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="56d78-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="56d78-196">Pour plus d'informations, voir [Configurer une connexion de réseau virtuel à réseau virtuel](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="56d78-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="56d78-197">Veillez à ajouter l’argument « -EnableBgp $True » lors de la création de connexions pour activer BGP.</span><span class="sxs-lookup"><span data-stu-id="56d78-197">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="56d78-198">1. Déclarer vos variables</span><span class="sxs-lookup"><span data-stu-id="56d78-198">1. Declare your variables</span></span>

<span data-ttu-id="56d78-199">Veillez à remplacer les valeurs par celles que vous souhaitez utiliser pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="56d78-199">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="56d78-200">2. Créer TestVNet2 dans le nouveau groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="56d78-200">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="56d78-201">3. Créer la passerelle VPN de TestVNet2 avec les paramètres BGP</span><span class="sxs-lookup"><span data-stu-id="56d78-201">3. Create the VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="56d78-202">Demandez l’allocation d’une adresse IP publique à la passerelle que vous allez créer pour votre réseau virtuel et définissez les configurations de sous-réseau et IP requises.</span><span class="sxs-lookup"><span data-stu-id="56d78-202">Request a public IP address to be allocated to the gateway you will create for your VNet and define the required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="56d78-203">Créez la passerelle VPN avec le numéro AS.</span><span class="sxs-lookup"><span data-stu-id="56d78-203">Create the VPN gateway with the AS number.</span></span> <span data-ttu-id="56d78-204">Vous devez substituer la valeur par défaut de l’ASN sur vos passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="56d78-204">You must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="56d78-205">Les ASN des réseaux virtuels connectés doivent être différents pour activer BGP et le routage de transit.</span><span class="sxs-lookup"><span data-stu-id="56d78-205">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="56d78-206">Étape 2 - Connecter les passerelles TestVNet1 et TestVNet2</span><span class="sxs-lookup"><span data-stu-id="56d78-206">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="56d78-207">Dans cet exemple, les deux passerelles sont dans le même abonnement.</span><span class="sxs-lookup"><span data-stu-id="56d78-207">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="56d78-208">Vous pouvez effectuer cette opération dans la même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56d78-208">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="56d78-209">1. Accéder aux deux passerelles</span><span class="sxs-lookup"><span data-stu-id="56d78-209">1. Get both gateways</span></span>

<span data-ttu-id="56d78-210">Veillez à ouvrir une session et à vous connecter à Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="56d78-210">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="56d78-211">2. Créer les deux connexions</span><span class="sxs-lookup"><span data-stu-id="56d78-211">2. Create both connections</span></span>

<span data-ttu-id="56d78-212">Cette étape, vous permet créer la connexion de TestVNet1 à TestVNet2 et de TestVNet2 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="56d78-212">In this step, you create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="56d78-213">Veillez à activer BGP pour les deux connexions.</span><span class="sxs-lookup"><span data-stu-id="56d78-213">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="56d78-214">Une fois ces étapes effectuées, la connexion est établie après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="56d78-214">After completing these steps, the connection is established after a few minutes.</span></span> <span data-ttu-id="56d78-215">La session d’homologation BGP démarre une fois la connexion de réseau virtuel à réseau virtuel établie.</span><span class="sxs-lookup"><span data-stu-id="56d78-215">The BGP peering session is up once the VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="56d78-216">Si vous avez effectué les trois parties de cet exercice, vous avez obtenu une topologie de réseau similaire à la suivante :</span><span class="sxs-lookup"><span data-stu-id="56d78-216">If you completed all three parts of this exercise, you have established the following network topology:</span></span>

![BGP pour une connexion de réseau virtuel à réseau virtuel](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="56d78-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56d78-218">Next steps</span></span>

<span data-ttu-id="56d78-219">Une fois la connexion achevée, vous pouvez ajouter des machines virtuelles à vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="56d78-219">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="56d78-220">Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="56d78-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>