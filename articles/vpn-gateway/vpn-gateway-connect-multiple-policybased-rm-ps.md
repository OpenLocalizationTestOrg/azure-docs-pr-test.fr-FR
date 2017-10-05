---
title: "Connexion des passerelles VPN Azure à plusieurs périphériques VPN basés sur des stratégies locales : Azure Resource Manager : PowerShell | Microsoft Docs"
description: "Cet article vous guidera tout au long de la configuration d’une passerelle VPN Azure basée sur le routage sur plusieurs périphériques VPN basés sur des stratégies à l’aide d’Azure Resource Manager et de PowerShell."
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
ms.openlocfilehash: 17211379ec61891982a02efca6730ca0da87c1ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-azure-vpn-gateways-to-multiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="09ef7-103">Connecter des passerelles VPN à plusieurs périphériques VPN basés sur des stratégies via PowerShell</span><span class="sxs-lookup"><span data-stu-id="09ef7-103">Connect Azure VPN gateways to multiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="09ef7-104">Cet article vous aidera à configurer une passerelle VPN Azure basée sur le routage pour connecter plusieurs périphériques VPN basés sur des stratégies locales tirant parti des stratégies IPsec/IKE personnalisées sur les connexions VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="09ef7-104">This article helps you configure an Azure route-based VPN gateway to connect to multiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="09ef7-105">À propos des passerelles VPN basées sur le routage et les stratégies</span><span class="sxs-lookup"><span data-stu-id="09ef7-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="09ef7-106">Les périphériques VPN basés sur des stratégies *et* ceux basés sur le routage diffèrent au niveau des sélecteurs de trafic IPsec et de la façon dont ils sont définis sur une connexion :</span><span class="sxs-lookup"><span data-stu-id="09ef7-106">Policy- *vs.* route-based VPN devices differ in how the IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="09ef7-107">Les périphériques VPN **basés sur des stratégies** utilisent des combinaisons de préfixes provenant des deux réseaux pour définir la façon dont le trafic est chiffré/déchiffré via les tunnels IPsec.</span><span class="sxs-lookup"><span data-stu-id="09ef7-107">**Policy-based** VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="09ef7-108">En règle générale, ce modèle est construit sur des pare-feu qui se chargent du filtrage des paquets.</span><span class="sxs-lookup"><span data-stu-id="09ef7-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="09ef7-109">Les fonctions de chiffrement et de déchiffrement de tunnel IPsec sont ajoutées au filtrage des paquets et au moteur de traitement.</span><span class="sxs-lookup"><span data-stu-id="09ef7-109">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>
* <span data-ttu-id="09ef7-110">Les périphériques VPN **basés sur le routage** utilisent des sélecteurs de trafic universels (caractère générique) et laissent les tables de routage/transfert diriger le trafic vers les différents tunnels IPsec.</span><span class="sxs-lookup"><span data-stu-id="09ef7-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="09ef7-111">En règle générale, ce modèle est construit sur des plateformes de routeur où chaque tunnel IPsec est modélisé en tant qu’interface réseau ou VTI (interface virtuelle de tunnel).</span><span class="sxs-lookup"><span data-stu-id="09ef7-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="09ef7-112">Les diagrammes suivants illustrent les deux modèles :</span><span class="sxs-lookup"><span data-stu-id="09ef7-112">The following diagrams highlight the two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="09ef7-113">Exemple de VPN basé sur des stratégies</span><span class="sxs-lookup"><span data-stu-id="09ef7-113">Policy-based VPN example</span></span>
![basé sur des stratégies](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="09ef7-115">Exemple de VPN basé sur le routage</span><span class="sxs-lookup"><span data-stu-id="09ef7-115">Route-based VPN example</span></span>
![basé sur le routage](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="09ef7-117">Prise en charge par Azure des VPN basés sur des stratégies</span><span class="sxs-lookup"><span data-stu-id="09ef7-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="09ef7-118">Actuellement, Azure prend en charge les deux modes de passerelles VPN : les passerelles VPN basées sur le routage et les passerelles VPN basées sur des stratégies.</span><span class="sxs-lookup"><span data-stu-id="09ef7-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="09ef7-119">Les deux modes sont construits sur différentes plateformes internes aux caractéristiques différentes :</span><span class="sxs-lookup"><span data-stu-id="09ef7-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="09ef7-120">**Passerelle VPN basée sur des stratégies**</span><span class="sxs-lookup"><span data-stu-id="09ef7-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="09ef7-121">**Passerelle VPN basée sur le routage**</span><span class="sxs-lookup"><span data-stu-id="09ef7-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="09ef7-122">**Référence SKU de passerelle Azure**</span><span class="sxs-lookup"><span data-stu-id="09ef7-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="09ef7-123">De base</span><span class="sxs-lookup"><span data-stu-id="09ef7-123">Basic</span></span>                       | <span data-ttu-id="09ef7-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="09ef7-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="09ef7-125">**Version IKE**</span><span class="sxs-lookup"><span data-stu-id="09ef7-125">**IKE version**</span></span>          | <span data-ttu-id="09ef7-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="09ef7-126">IKEv1</span></span>                       | <span data-ttu-id="09ef7-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="09ef7-127">IKEv2</span></span>                                    |
| <span data-ttu-id="09ef7-128">**IOPS Connexions S2S**</span><span class="sxs-lookup"><span data-stu-id="09ef7-128">**Max. S2S connections**</span></span> | <span data-ttu-id="09ef7-129">**1**</span><span class="sxs-lookup"><span data-stu-id="09ef7-129">**1**</span></span>                       | <span data-ttu-id="09ef7-130">Basic/Standard : 10</span><span class="sxs-lookup"><span data-stu-id="09ef7-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="09ef7-131">HighPerformance : 30</span><span class="sxs-lookup"><span data-stu-id="09ef7-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="09ef7-132">Avec une stratégie IPsec/IKE personnalisée, vous pouvez désormais configurer les passerelles VPN Azure basées sur le routage pour utiliser des sélecteurs de trafic basés sur les préfixes avec l’option «**PolicyBasedTrafficSelectors**», afin de vous connecter à des périphériques VPN basés sur des stratégies locales.</span><span class="sxs-lookup"><span data-stu-id="09ef7-132">With the custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways to use prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", to connect to on-premises policy-based VPN devices.</span></span> <span data-ttu-id="09ef7-133">Cette fonctionnalité vous permet de vous connecter à partir d’un réseau virtuel Azure et d’une passerelle VPN à plusieurs périphériques VPN/pare-feu basés sur des stratégies locales, en supprimant ainsi la limite d’une connexion unique à partir des passerelles VPN Azure basées sur des stratégies locales.</span><span class="sxs-lookup"><span data-stu-id="09ef7-133">This capability allows you to connect from an Azure virtual network and VPN gateway to multiple on-premises policy-based VPN/firewall devices, removing the single connection limit from the current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="09ef7-134">Pour activer cette connectivité, vos périphériques VPN basés sur des stratégies locales doivent prendre en charge **IKEv2** pour la connexion aux passerelles VPN Azure basées sur le routage.</span><span class="sxs-lookup"><span data-stu-id="09ef7-134">To enable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** to connect to the Azure route-based VPN gateways.</span></span> <span data-ttu-id="09ef7-135">Vérifiez les caractéristiques de votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="09ef7-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="09ef7-136">Les réseaux locaux qui utilisent ce mécanisme pour se connecter via des périphériques VPN basés sur des stratégies ne peuvent se connecter qu’au réseau virtuel Azure ; c’est-à-dire qu’**ils ne peuvent pas transiter vers d’autres réseaux locaux ou virtuels via la même passerelle VPN Azure**.</span><span class="sxs-lookup"><span data-stu-id="09ef7-136">The on-premises networks connecting through policy-based VPN devices with this mechanism can only connect to the Azure virtual network; **they cannot transit to other on-premises networks or virtual networks via the same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="09ef7-137">L’option de configuration fait partie de la stratégie de connexion personnalisée IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="09ef7-137">The configuration option is part of the custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="09ef7-138">Vous devez spécifier la stratégie complète (algorithmes de chiffrement et d’intégrité IPsec/IKE, puissance des clés et durée de vie des associations de sécurité) si vous activez l’option Sélecteur de trafic basé sur des stratégies.</span><span class="sxs-lookup"><span data-stu-id="09ef7-138">If you enable the policy-based traffic selector option, you must specify the complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="09ef7-139">Le diagramme suivant montre pourquoi le routage de transit via la passerelle VPN Azure ne fonctionne pas avec l’option basée sur des stratégies :</span><span class="sxs-lookup"><span data-stu-id="09ef7-139">The following diagram shows why transit routing via Azure VPN gateway doesn't work with the policy-based option:</span></span>

![transit basé sur des stratégies](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="09ef7-141">Comme illustré dans le diagramme, les sélecteurs de trafic de la passerelle VPN Azure vont du réseau virtuel vers chaque préfixe de réseau local, mais les connexions croisées ne sont pas possibles.</span><span class="sxs-lookup"><span data-stu-id="09ef7-141">As shown in the diagram, the Azure VPN gateway has traffic selectors from the virtual network to each of the on-premises network prefixes, but not the cross-connection prefixes.</span></span> <span data-ttu-id="09ef7-142">Par exemple, les sites locaux 2, 3 et 4 peuvent tous communiquer avec VNet1, mais ils ne peuvent pas se connecter entre eux via la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="09ef7-142">For example, on-premises site 2, site 3, and site 4 can each communicate to VNet1 respectively, but cannot connect via the Azure VPN gateway to each other.</span></span> <span data-ttu-id="09ef7-143">Le diagramme montre les sélecteurs de trafic croisés qui ne sont pas disponibles dans cette configuration de la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="09ef7-143">The diagram shows the cross-connect traffic selectors that are not available in the Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="09ef7-144">Configurer des sélecteurs de trafic basés sur des stratégies sur une connexion</span><span class="sxs-lookup"><span data-stu-id="09ef7-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="09ef7-145">Les instructions fournies dans cet article suivent le même exemple que l’article [Configurer la stratégie IPsec/IKE pour des connexions VPN S2S ou de réseau virtuel à réseau virtuel](vpn-gateway-ipsecikepolicy-rm-powershell.md) pour établir une connexion VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="09ef7-145">The instructions in this article follow the same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) to establish a S2S VPN connection.</span></span> <span data-ttu-id="09ef7-146">Cette situation est présentée dans le diagramme suivant :</span><span class="sxs-lookup"><span data-stu-id="09ef7-146">This is shown in the following diagram:</span></span>

![stratégie S2S](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="09ef7-148">Le flux de travail pour activer cette connectivité est le suivant :</span><span class="sxs-lookup"><span data-stu-id="09ef7-148">The workflow to enable this connectivity:</span></span>
1. <span data-ttu-id="09ef7-149">Créez le réseau virtuel, la passerelle VPN et la passerelle de réseau local pour votre connexion entre sites.</span><span class="sxs-lookup"><span data-stu-id="09ef7-149">Create the virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="09ef7-150">Créez une stratégie IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="09ef7-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="09ef7-151">Appliquez la stratégie lorsque vous créez une connexion S2S ou entre deux réseaux virtuels, et **activez les sélecteurs de trafic basés sur des stratégies** sur la connexion</span><span class="sxs-lookup"><span data-stu-id="09ef7-151">Apply the policy when you create a S2S or VNet-to-VNet connection, and **enable the policy-based traffic selectors** on the connection</span></span>
4. <span data-ttu-id="09ef7-152">Si la connexion est déjà créée, vous pouvez appliquer ou mettre à jour la stratégie sur une connexion existante</span><span class="sxs-lookup"><span data-stu-id="09ef7-152">If the connection is already created, you can apply or update the policy to an existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="09ef7-153">Activer des sélecteurs de trafic basés sur des stratégies sur une connexion</span><span class="sxs-lookup"><span data-stu-id="09ef7-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="09ef7-154">Assurez-vous d’avoir terminé la [partie 3 de l’article sur la configuration d’une stratégie IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) avant d’aborder cette section.</span><span class="sxs-lookup"><span data-stu-id="09ef7-154">Make sure you have completed [Part 3 of the Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="09ef7-155">L’exemple suivant utilise les mêmes paramètres et étapes :</span><span class="sxs-lookup"><span data-stu-id="09ef7-155">The following example uses the same parameters and steps:</span></span>

### <a name="step-1---create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="09ef7-156">Étape 1 : création du réseau virtuel, de la passerelle VPN et de la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="09ef7-156">Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-to-your-subscription"></a><span data-ttu-id="09ef7-157">1. Déclarez vos variables et connectez-vous à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="09ef7-157">1. Declare your variables & connect to your subscription</span></span>
<span data-ttu-id="09ef7-158">Dans cet exercice, nous allons commencer par déclarer les variables.</span><span class="sxs-lookup"><span data-stu-id="09ef7-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="09ef7-159">Veillez à les remplacer par vos valeurs lors de la configuration dans un contexte de production.</span><span class="sxs-lookup"><span data-stu-id="09ef7-159">Be sure to replace the values with your own when configuring for production.</span></span>

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
<span data-ttu-id="09ef7-160">Pour utiliser les cmdlets Resource Manager, passez au mode PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09ef7-160">To use the Resource Manager cmdlets, make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="09ef7-161">Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="09ef7-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="09ef7-162">Ouvrez la console PowerShell et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="09ef7-162">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="09ef7-163">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="09ef7-163">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="09ef7-164">2. Créer le réseau virtuel, la passerelle VPN et la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="09ef7-164">2. Create the virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="09ef7-165">L’exemple suivant crée le réseau virtuel, TestVNet1, avec trois sous-réseaux et la passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="09ef7-165">The following example creates the virtual network, TestVNet1 with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="09ef7-166">Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="09ef7-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="09ef7-167">Si vous le nommez autrement, la création de votre passerelle échoue.</span><span class="sxs-lookup"><span data-stu-id="09ef7-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="09ef7-168">Étape 2 : création d’une connexion VPN S2S avec une stratégie IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="09ef7-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="09ef7-169">1. Créez une stratégie IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="09ef7-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09ef7-170">Vous devez créer une stratégie IPsec/IKE afin d’activer l’option « UsePolicyBasedTrafficSelectors » sur la connexion.</span><span class="sxs-lookup"><span data-stu-id="09ef7-170">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="09ef7-171">L’exemple de script suivant crée une stratégie IPsec/IKE avec les paramètres et les algorithmes suivants :</span><span class="sxs-lookup"><span data-stu-id="09ef7-171">The following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="09ef7-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="09ef7-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="09ef7-173">IPsec : AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span><span class="sxs-lookup"><span data-stu-id="09ef7-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="09ef7-174">2. Créez la connexion VPN S2S avec les sélecteurs de trafic basés sur des stratégies et la stratégie IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="09ef7-174">2. Create the S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="09ef7-175">Créez une connexion VPN S2S et appliquez la stratégie IPsec/IKE créée dans l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="09ef7-175">Create an S2S VPN connection and apply the IPsec/IKE policy created in the previous step.</span></span> <span data-ttu-id="09ef7-176">Prenez connaissance de l’utilisation du paramètre supplémentaire « -UsePolicyBasedTrafficSelectors $True ». Il permet d’activer les sélecteurs de trafic basés sur des stratégies sur la connexion.</span><span class="sxs-lookup"><span data-stu-id="09ef7-176">Be aware of the additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on the connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="09ef7-177">Une fois que vous aurez terminé ces étapes, la connexion VPN S2S utilisera la stratégie IPsec/IKE définie et activera sur la connexion les sélecteurs de trafic basés sur des stratégies.</span><span class="sxs-lookup"><span data-stu-id="09ef7-177">After completing the steps, the S2S VPN connection will use the IPsec/IKE policy defined, and enable policy-based traffic selectors on the connection.</span></span> <span data-ttu-id="09ef7-178">Vous pouvez répéter les mêmes étapes pour ajouter davantage de connexions à des périphériques VPN supplémentaires basés sur des stratégies locales à partir de la même passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="09ef7-178">You can repeat the same steps to add more connections to additional on-premises policy-based VPN devices from the same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="09ef7-179">Mettre à jour des sélecteurs de trafic basés sur des stratégies pour une connexion</span><span class="sxs-lookup"><span data-stu-id="09ef7-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="09ef7-180">La dernière section indique comment mettre à jour l’option des sélecteurs de trafic basés sur des stratégies pour une connexion VPN S2S existante.</span><span class="sxs-lookup"><span data-stu-id="09ef7-180">The last section shows you how to update the policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-the-connection"></a><span data-ttu-id="09ef7-181">1. Obtenez la connexion.</span><span class="sxs-lookup"><span data-stu-id="09ef7-181">1. Get the connection</span></span>
<span data-ttu-id="09ef7-182">Commencez par obtenir la ressource de connexion.</span><span class="sxs-lookup"><span data-stu-id="09ef7-182">Get the connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-the-policy-based-traffic-selectors-option"></a><span data-ttu-id="09ef7-183">2. Vérifiez l’option des sélecteurs de trafic basés sur des stratégies.</span><span class="sxs-lookup"><span data-stu-id="09ef7-183">2. Check the policy-based traffic selectors option</span></span>
<span data-ttu-id="09ef7-184">La ligne suivante indique si les sélecteurs de trafic basés sur des stratégies sont utilisés pour la connexion :</span><span class="sxs-lookup"><span data-stu-id="09ef7-184">The following line shows whether the policy-based traffic selectors are used for the connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="09ef7-185">Si la ligne renvoie « **True** », alors les sélecteurs de trafic basés sur des stratégies sont configurés sur la connexion ; sinon, elle indique « **False** ».</span><span class="sxs-lookup"><span data-stu-id="09ef7-185">If the line returns "**True**", then policy-based traffic selectors are configured on the connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-the-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="09ef7-186">3. Mettre à jour les sélecteurs de trafic basés sur des stratégies sur une connexion</span><span class="sxs-lookup"><span data-stu-id="09ef7-186">3. Update the policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="09ef7-187">Une fois que vous avez obtenu la ressource de connexion, vous pouvez activer ou désactiver l’option.</span><span class="sxs-lookup"><span data-stu-id="09ef7-187">Once you obtain the connection resource, you can enable or disable the option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="09ef7-188">Désactiver UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="09ef7-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="09ef7-189">Dans l’exemple suivant, l’option des sélecteurs du trafic basés sur des stratégies est désactivée, mais ne modifie pas la stratégie IPsec/IKE :</span><span class="sxs-lookup"><span data-stu-id="09ef7-189">The following example disables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="09ef7-190">Activer UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="09ef7-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="09ef7-191">Dans l’exemple suivant, l’option des sélecteurs du trafic basés sur des stratégies est désactivée, mais ne modifie pas la stratégie IPsec/IKE :</span><span class="sxs-lookup"><span data-stu-id="09ef7-191">The following example enables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="09ef7-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09ef7-192">Next steps</span></span>
<span data-ttu-id="09ef7-193">Une fois la connexion achevée, vous pouvez ajouter des machines virtuelles à vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="09ef7-193">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="09ef7-194">Consultez [Création d’une machine virtuelle](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour connaître les différentes étapes.</span><span class="sxs-lookup"><span data-stu-id="09ef7-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="09ef7-195">Pour en savoir plus sur les stratégies IPsec/IKE personnalisées, consultez [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configuration d’une stratégie IPsec/IKE pour les connexions VPN S2S ou entre deux réseaux virtuels).</span><span class="sxs-lookup"><span data-stu-id="09ef7-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
