---
title: "Connecter des périphériques VPN basée sur des stratégies VPN Azure passerelles toomultiple local : Azure Resource Manager : PowerShell | Documents Microsoft"
description: "Cet article vous guide dans la configuration Azure basée sur un itinéraire VPN passerelle toomultiple basée sur des stratégies VPN des appareils à l’aide du Gestionnaire de ressources Azure et PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="31450-103">Connexion VPN Azure passerelles toomultiple basée sur des stratégies VPN appareils locaux à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="31450-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="31450-104">Cet article vous aidera à configurer un Azure basée sur un itinéraire VPN passerelle tooconnect toomultiple locale basée sur des stratégies des dispositifs VPN tirant parti des stratégies IPsec/IKE personnalisées sur les connexions VPN de S2S.</span><span class="sxs-lookup"><span data-stu-id="31450-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="31450-105">À propos des passerelles VPN basées sur le routage et les stratégies</span><span class="sxs-lookup"><span data-stu-id="31450-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="31450-106">Stratégie - *et* périphériques VPN itinéraire diffèrent dans la manière dont les sélecteurs de trafic IPsec hello sont définis sur une connexion :</span><span class="sxs-lookup"><span data-stu-id="31450-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="31450-107">**Basée sur des stratégies** périphériques VPN utilisent des combinaisons de hello de préfixes à partir de ces deux toodefine réseaux comment le trafic est chiffré/déchiffré via les tunnels IPsec.</span><span class="sxs-lookup"><span data-stu-id="31450-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="31450-108">En règle générale, ce modèle est construit sur des pare-feu qui se chargent du filtrage des paquets.</span><span class="sxs-lookup"><span data-stu-id="31450-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="31450-109">Chiffrement de tunnel IPsec et le déchiffrement sont ajoutés toohello le filtrage de paquets et le moteur de traitement.</span><span class="sxs-lookup"><span data-stu-id="31450-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="31450-110">**Basée sur un itinéraire** périphériques VPN utilisent sélecteurs de trafic pour tout (caractère générique), et permettent de routage/transfert tables les tunnels IPsec toodifferent diriger le trafic.</span><span class="sxs-lookup"><span data-stu-id="31450-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="31450-111">En règle générale, ce modèle est construit sur des plateformes de routeur où chaque tunnel IPsec est modélisé en tant qu’interface réseau ou VTI (interface virtuelle de tunnel).</span><span class="sxs-lookup"><span data-stu-id="31450-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="31450-112">Hello diagrammes suivants mettre en surbrillance deux modèles de hello :</span><span class="sxs-lookup"><span data-stu-id="31450-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="31450-113">Exemple de VPN basé sur des stratégies</span><span class="sxs-lookup"><span data-stu-id="31450-113">Policy-based VPN example</span></span>
![basé sur des stratégies](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="31450-115">Exemple de VPN basé sur le routage</span><span class="sxs-lookup"><span data-stu-id="31450-115">Route-based VPN example</span></span>
![basé sur le routage](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="31450-117">Prise en charge par Azure des VPN basés sur des stratégies</span><span class="sxs-lookup"><span data-stu-id="31450-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="31450-118">Actuellement, Azure prend en charge les deux modes de passerelles VPN : les passerelles VPN basées sur le routage et les passerelles VPN basées sur des stratégies.</span><span class="sxs-lookup"><span data-stu-id="31450-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="31450-119">Les deux modes sont construits sur différentes plateformes internes aux caractéristiques différentes :</span><span class="sxs-lookup"><span data-stu-id="31450-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="31450-120">**Passerelle VPN basée sur des stratégies**</span><span class="sxs-lookup"><span data-stu-id="31450-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="31450-121">**Passerelle VPN basée sur le routage**</span><span class="sxs-lookup"><span data-stu-id="31450-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="31450-122">**Référence SKU de passerelle Azure**</span><span class="sxs-lookup"><span data-stu-id="31450-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="31450-123">De base</span><span class="sxs-lookup"><span data-stu-id="31450-123">Basic</span></span>                       | <span data-ttu-id="31450-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="31450-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="31450-125">**Version IKE**</span><span class="sxs-lookup"><span data-stu-id="31450-125">**IKE version**</span></span>          | <span data-ttu-id="31450-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="31450-126">IKEv1</span></span>                       | <span data-ttu-id="31450-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="31450-127">IKEv2</span></span>                                    |
| <span data-ttu-id="31450-128">**IOPS Connexions S2S**</span><span class="sxs-lookup"><span data-stu-id="31450-128">**Max. S2S connections**</span></span> | <span data-ttu-id="31450-129">**1**</span><span class="sxs-lookup"><span data-stu-id="31450-129">**1**</span></span>                       | <span data-ttu-id="31450-130">Basic/Standard : 10</span><span class="sxs-lookup"><span data-stu-id="31450-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="31450-131">HighPerformance : 30</span><span class="sxs-lookup"><span data-stu-id="31450-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="31450-132">Avec la stratégie IPsec/IKE personnalisée hello, vous pouvez désormais configurer Azure basée sur un itinéraire VPN passerelles toouse basée sur le préfixe sélecteurs de trafic avec l’option «**PolicyBasedTrafficSelectors**», périphériques VPN basée sur des stratégies tooconnect tooon local.</span><span class="sxs-lookup"><span data-stu-id="31450-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="31450-133">Cette fonctionnalité vous permet de tooconnect à partir d’un réseau virtuel Azure et toomultiple de passerelle VPN locale basée sur des stratégies des appareils VPN/pare-feu, suppression de limite de connexion unique hello de hello actuelle Azure basée sur des stratégies les passerelles VPN.</span><span class="sxs-lookup"><span data-stu-id="31450-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="31450-134">tooenable cette connectivité, vos périphériques VPN basée sur des stratégies de local doivent prendre en charge **IKEv2** tooconnect toohello Azure passerelles VPN basée sur un itinéraire.</span><span class="sxs-lookup"><span data-stu-id="31450-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="31450-135">Vérifiez les caractéristiques de votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="31450-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="31450-136">Hello sur des réseaux locaux qui se connectent via des appareils VPN basée sur des stratégies avec ce mécanisme ne peuvent se connecter toohello réseau virtuel Azure ; **qu’ils ne peuvent pas traversent tooother sur des réseaux locaux ou des réseaux virtuels via hello même passerelle VPN Azure**.</span><span class="sxs-lookup"><span data-stu-id="31450-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="31450-137">option de configuration Hello fait partie de la stratégie de connexion IPsec/IKE personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="31450-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="31450-138">Si vous activez l’option de sélecteur hello du trafic basé sur une stratégie, vous devez spécifier la stratégie complète de hello (algorithmes de chiffrement et d’intégrité IPsec/IKE, atouts et durées de vie SA).</span><span class="sxs-lookup"><span data-stu-id="31450-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="31450-139">Hello suivant schéma montre pourquoi le routage de transit via la passerelle VPN Azure ne fonctionne pas avec l’option de hello basée sur des stratégies :</span><span class="sxs-lookup"><span data-stu-id="31450-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![transit basé sur des stratégies](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="31450-141">Comme indiqué dans le diagramme de hello, passerelle VPN Azure de hello a sélecteurs de trafic à partir de tooeach de réseau virtuel hello des préfixes de réseau local hello, mais pas les préfixes de connexion croisée hello.</span><span class="sxs-lookup"><span data-stu-id="31450-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="31450-142">Par exemple, le site local 2, 3 et 4 chacun peuvent communiquer tooVNet1 respectivement, mais ne peut pas se connecter via tooeach passerelle VPN Azure du hello autres.</span><span class="sxs-lookup"><span data-stu-id="31450-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="31450-143">diagramme de Hello montre hello interconnexion sélecteurs de trafic qui ne sont pas disponibles dans une passerelle VPN Azure hello à cette configuration.</span><span class="sxs-lookup"><span data-stu-id="31450-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="31450-144">Configurer des sélecteurs de trafic basés sur des stratégies sur une connexion</span><span class="sxs-lookup"><span data-stu-id="31450-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="31450-145">Hello instructions de ce suivi de l’article hello même exemple, comme décrit dans [stratégie IPsec/IKE configurer pour les connexions S2S ou au réseau](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish une connexion VPN de S2S.</span><span class="sxs-lookup"><span data-stu-id="31450-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="31450-146">Cela est illustré par hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="31450-146">This is shown in hello following diagram:</span></span>

![stratégie S2S](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="31450-148">Hello tooenable de flux de travail cette connectivité :</span><span class="sxs-lookup"><span data-stu-id="31450-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="31450-149">Créer une passerelle de réseau local pour votre connexion intersite, réseau virtuel de hello et passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="31450-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="31450-150">Créez une stratégie IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="31450-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="31450-151">Appliquer la stratégie de hello lorsque vous créez une connexion S2S ou au réseau, et **activer les sélecteurs de trafic basé sur une stratégie hello** sur la connexion de hello</span><span class="sxs-lookup"><span data-stu-id="31450-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="31450-152">Si la connexion de hello existe déjà, vous pouvez appliquer ou mettre à jour la connexion à la stratégie hello tooan existante</span><span class="sxs-lookup"><span data-stu-id="31450-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="31450-153">Activer des sélecteurs de trafic basés sur des stratégies sur une connexion</span><span class="sxs-lookup"><span data-stu-id="31450-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="31450-154">Vérifiez que vous avez effectué [partie 3 sur l’article de stratégie IPsec/IKE configurer hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) pour cette section.</span><span class="sxs-lookup"><span data-stu-id="31450-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="31450-155">Hello suivant montre comment utiliser hello les mêmes paramètres et étapes :</span><span class="sxs-lookup"><span data-stu-id="31450-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="31450-156">Étape 1 : créer le réseau virtuel de hello, passerelle VPN et passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="31450-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="31450-157">1. Déclarez vos variables & connecter tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="31450-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="31450-158">Dans cet exercice, nous allons commencer par déclarer les variables.</span><span class="sxs-lookup"><span data-stu-id="31450-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="31450-159">Être des valeurs de hello tooreplace que par les vôtres lors de la configuration pour la production.</span><span class="sxs-lookup"><span data-stu-id="31450-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="31450-160">toouse hello applets de commande Gestionnaire de ressources, veillez à basculer en mode de tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="31450-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="31450-161">Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="31450-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="31450-162">Ouvrez la console PowerShell et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="31450-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="31450-163">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="31450-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="31450-164">2. Créer le réseau virtuel de hello, passerelle VPN et passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="31450-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="31450-165">Hello, l’exemple suivant crée un réseau virtuel hello, TestVNet1 avec trois sous-réseaux et de passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="31450-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="31450-166">Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="31450-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="31450-167">Si vous le nommez autrement, la création de votre passerelle échoue.</span><span class="sxs-lookup"><span data-stu-id="31450-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="31450-168">Étape 2 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="31450-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="31450-169">1. Créez une stratégie IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="31450-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31450-170">Vous devez toocreate une stratégie IPsec/IKE dans l’ordre tooenable option « UsePolicyBasedTrafficSelectors » sur la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="31450-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="31450-171">Hello exemple suivant crée une stratégie IPsec/IKE avec ces algorithmes et les paramètres :</span><span class="sxs-lookup"><span data-stu-id="31450-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="31450-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="31450-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="31450-173">IPsec : AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span><span class="sxs-lookup"><span data-stu-id="31450-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="31450-174">2. Créer un réseau VPN S2S hello avec sélecteurs de trafic basé sur la stratégie et la stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="31450-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="31450-175">Créer un réseau VPN S2S et appliquer la stratégie IPsec/IKE de hello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="31450-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="31450-176">N’oubliez pas de paramètre supplémentaires hello »-UsePolicyBasedTrafficSelectors $True » qui permet des sélecteurs de trafic de basée sur la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="31450-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="31450-177">Après avoir effectué les étapes de hello, hello réseau VPN S2S utilise hello stratégie IPsec/IKE définie et activer les sélecteurs de trafic de basée sur la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="31450-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="31450-178">Vous pouvez répéter hello même procédure tooadd plusieurs connexions tooadditional basée sur des stratégies VPN appareils locaux à partir de hello même passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="31450-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="31450-179">Mettre à jour des sélecteurs de trafic basés sur des stratégies pour une connexion</span><span class="sxs-lookup"><span data-stu-id="31450-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="31450-180">dernière section de Hello vous montre comment les sélecteurs de trafic basé sur la stratégie tooupdate hello option pour une connexion VPN de S2S existante.</span><span class="sxs-lookup"><span data-stu-id="31450-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="31450-181">1. Obtenir la connexion de hello</span><span class="sxs-lookup"><span data-stu-id="31450-181">1. Get hello connection</span></span>
<span data-ttu-id="31450-182">Obtenir une ressource de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="31450-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="31450-183">2. Hello du trafic basé sur la stratégie de sélecteurs option Vérifier</span><span class="sxs-lookup"><span data-stu-id="31450-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="31450-184">Hello ligne suivante indique si les sélecteurs de hello du trafic basé sur la stratégie sont utilisés pour la connexion de hello :</span><span class="sxs-lookup"><span data-stu-id="31450-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="31450-185">Si la ligne de hello retourne «**True**», puis les sélecteurs de trafic basé sur la stratégie sont configurés sur la connexion de hello ; sinon, elle retourne «**False**. »</span><span class="sxs-lookup"><span data-stu-id="31450-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="31450-186">3. Mettre à jour les sélecteurs de trafic basé sur une stratégie hello sur une connexion</span><span class="sxs-lookup"><span data-stu-id="31450-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="31450-187">Une fois que vous obtenez la ressource de connexion hello, vous pouvez activer ou désactiver l’option de hello.</span><span class="sxs-lookup"><span data-stu-id="31450-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="31450-188">Désactiver UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="31450-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="31450-189">exemple Hello désactive option de sélecteurs hello du trafic basé sur la stratégie, mais laisse hello stratégie IPsec/IKE inchangé :</span><span class="sxs-lookup"><span data-stu-id="31450-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="31450-190">Activer UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="31450-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="31450-191">option de sélecteurs hello du trafic basé sur la stratégie active Hello exemple suivant, mais laisse hello stratégie IPsec/IKE inchangé :</span><span class="sxs-lookup"><span data-stu-id="31450-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="31450-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31450-192">Next steps</span></span>
<span data-ttu-id="31450-193">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="31450-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="31450-194">Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="31450-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="31450-195">Pour en savoir plus sur les stratégies IPsec/IKE personnalisées, consultez [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuration d’une stratégie IPsec/IKE pour les connexions VPN S2S ou entre deux réseaux virtuels).</span><span class="sxs-lookup"><span data-stu-id="31450-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
