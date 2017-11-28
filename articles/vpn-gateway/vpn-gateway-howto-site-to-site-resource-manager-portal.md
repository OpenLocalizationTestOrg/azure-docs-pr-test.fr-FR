---
title: "Connecter votre réseau local à un réseau virtuel Azure : VPN site à site : portail | Microsoft Docs"
description: "Étapes de création d’une connexion IPsec entre votre réseau local et un réseau virtuel Azure via l’Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN de site à site à l’aide du portail."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 0dec0d3744f76a06313928197f3a5229290ba32b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a><span data-ttu-id="571e5-104">Création d’une connexion de site à site dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="571e5-104">Create a Site-to-Site connection in the Azure portal</span></span>

<span data-ttu-id="571e5-105">Cet article vous explique comment utiliser le portail Azure pour créer une connexion de passerelle VPN de site à site à partir de votre réseau local vers le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="571e5-105">This article shows you how to use the Azure portal to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="571e5-106">Les étapes mentionnées dans cet article s’appliquent au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="571e5-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="571e5-107">Vous pouvez également créer cette configuration à l’aide d’un autre outil ou modèle de déploiement en sélectionnant une option différente dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="571e5-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="571e5-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="571e5-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="571e5-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="571e5-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="571e5-110">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="571e5-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="571e5-111">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="571e5-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="571e5-112">Une connexion de passerelle VPN de site à site permet de connecter votre réseau local à un réseau virtuel Azure via un tunnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="571e5-112">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="571e5-113">Ce type de connexion requiert un périphérique VPN local disposant d’une adresse IP publique exposée en externe.</span><span class="sxs-lookup"><span data-stu-id="571e5-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="571e5-114">Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="571e5-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="571e5-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="571e5-116">Before you begin</span></span>

<span data-ttu-id="571e5-117">Vérifiez que vous disposez des éléments ci-dessous avant de commencer votre configuration :</span><span class="sxs-lookup"><span data-stu-id="571e5-117">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="571e5-118">Veillez à disposer d’un périphérique VPN compatible et à être entouré d’une personne en mesure de le configurer.</span><span class="sxs-lookup"><span data-stu-id="571e5-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="571e5-119">Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="571e5-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="571e5-120">Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="571e5-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="571e5-121">Cette adresse IP ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="571e5-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="571e5-122">Si vous ne maîtrisez pas les plages d’adresses IP situées dans votre configuration de réseau local, vous devez contacter une personne en mesure de vous aider.</span><span class="sxs-lookup"><span data-stu-id="571e5-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="571e5-123">Lorsque vous créez cette configuration, vous devez spécifier les préfixes des plages d’adresses IP qu’Azure acheminera vers votre emplacement local.</span><span class="sxs-lookup"><span data-stu-id="571e5-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="571e5-124">Aucun des sous-réseaux de votre réseau local ne peut chevaucher les sous-réseaux du réseau virtuel auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="571e5-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span> 

### <span data-ttu-id="571e5-125"><a name="values"></a>Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="571e5-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="571e5-126">Nous utilisons les valeurs suivantes dans les exemples de cet article.</span><span class="sxs-lookup"><span data-stu-id="571e5-126">The examples in this article use the following values.</span></span> <span data-ttu-id="571e5-127">Vous pouvez utiliser ces valeurs pour créer un environnement de test ou vous y référer pour mieux comprendre les exemples de cet article.</span><span class="sxs-lookup"><span data-stu-id="571e5-127">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

* <span data-ttu-id="571e5-128">**Nom du réseau virtuel :** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="571e5-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="571e5-129">**Espace d’adressage :**</span><span class="sxs-lookup"><span data-stu-id="571e5-129">**Address Space:**</span></span> 
  * <span data-ttu-id="571e5-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="571e5-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="571e5-131">10.12.0.0/16 (facultatif pour cet exercice)</span><span class="sxs-lookup"><span data-stu-id="571e5-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="571e5-132">**Sous-réseaux :**</span><span class="sxs-lookup"><span data-stu-id="571e5-132">**Subnets:**</span></span>
  * <span data-ttu-id="571e5-133">FrontEnd : 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="571e5-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="571e5-134">BackEnd : 10.12.0.0/24 (facultatif pour cet exercice)</span><span class="sxs-lookup"><span data-stu-id="571e5-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="571e5-135">**Sous-réseau de passerelle :** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="571e5-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="571e5-136">**Groupe de ressources :** TestRG1</span><span class="sxs-lookup"><span data-stu-id="571e5-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="571e5-137">**Emplacement :** États-Unis de l’Est</span><span class="sxs-lookup"><span data-stu-id="571e5-137">**Location:** East US</span></span>
* <span data-ttu-id="571e5-138">**Serveur DNS**  Facultatif.</span><span class="sxs-lookup"><span data-stu-id="571e5-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="571e5-139">L’adresse IP de votre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="571e5-139">The IP address of your DNS server.</span></span>
* <span data-ttu-id="571e5-140">**Nom de passerelle de réseau virtuel :** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="571e5-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="571e5-141">**Adresse IP publique :** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="571e5-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="571e5-142">**Type de VPN :** Route-based</span><span class="sxs-lookup"><span data-stu-id="571e5-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="571e5-143">**Type de connexion :** Site-to-site (IPsec)</span><span class="sxs-lookup"><span data-stu-id="571e5-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="571e5-144">**Type de passerelle :** VPN</span><span class="sxs-lookup"><span data-stu-id="571e5-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="571e5-145">**Nom de passerelle de réseau local :** Site2</span><span class="sxs-lookup"><span data-stu-id="571e5-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="571e5-146">**Nom de connexion :** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="571e5-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="571e5-147"><a name="CreatVNet"></a>1. Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="571e5-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="571e5-148"><a name="dns"></a>2. Spécifier un serveur DNS</span><span class="sxs-lookup"><span data-stu-id="571e5-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="571e5-149">Aucun DNS n’est nécessaire pour créer une connexion de site à site.</span><span class="sxs-lookup"><span data-stu-id="571e5-149">DNS is not required to create a Site-to-Site connection.</span></span> <span data-ttu-id="571e5-150">Toutefois, si vous souhaitez résoudre les noms des ressources qui sont déployées sur votre réseau virtuel, vous devez spécifier un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="571e5-150">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="571e5-151">Ce paramètre vous permet de spécifier le serveur DNS que vous souhaitez utiliser pour la résolution de noms pour ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="571e5-151">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="571e5-152">Il n'entraîne pas la création d'un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="571e5-152">It does not create a DNS server.</span></span> <span data-ttu-id="571e5-153">Pour plus d’informations sur la résolution de noms pour les machines virtuelles, consultez [Résolution de noms pour les machines virtuelles et instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="571e5-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="571e5-154"><a name="gatewaysubnet"></a>3. Créer le sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="571e5-154"><a name="gatewaysubnet"></a>3. Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="571e5-155"><a name="VNetGateway"></a>4. Créer la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="571e5-155"><a name="VNetGateway"></a>4. Create the VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="571e5-156"><a name="LocalNetworkGateway"></a>5. Créer la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="571e5-156"><a name="LocalNetworkGateway"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="571e5-157">La passerelle de réseau local fait généralement référence à votre emplacement local.</span><span class="sxs-lookup"><span data-stu-id="571e5-157">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="571e5-158">Donnez au site un nom auquel Azure pourra se référer, puis spécifiez l’adresse IP du périphérique VPN local vers lequel vous allez créer une connexion.</span><span class="sxs-lookup"><span data-stu-id="571e5-158">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="571e5-159">Spécifiez également les préfixes d’adresses IP qui seront acheminés via la passerelle VPN vers le périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="571e5-159">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="571e5-160">Les préfixes d’adresses que vous spécifiez sont les préfixes situés sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="571e5-160">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="571e5-161">En cas de modification du réseau ou si vous devez modifier l’adresse IP publique de l’appareil VPN, il est simple de mettre à jour les valeurs ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="571e5-161">If your on-premises network changes or you need to change the public IP address for the VPN device, you can easily update the values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="571e5-162"><a name="VPNDevice"></a>6. Configuration de votre périphérique VPN</span><span class="sxs-lookup"><span data-stu-id="571e5-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="571e5-163">Les connexions site à site vers un réseau local nécessitent un périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="571e5-163">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="571e5-164">Dans cette étape, vous configurez votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="571e5-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="571e5-165">Pour configurer votre périphérique VPN, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="571e5-165">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="571e5-166">Une clé partagée.</span><span class="sxs-lookup"><span data-stu-id="571e5-166">A shared key.</span></span> <span data-ttu-id="571e5-167">Il s’agit de la clé partagée spécifiée lors de la création de la connexion VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="571e5-167">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="571e5-168">Dans nos exemples, nous utilisons une clé partagée basique.</span><span class="sxs-lookup"><span data-stu-id="571e5-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="571e5-169">Nous vous conseillons de générer une clé plus complexe.</span><span class="sxs-lookup"><span data-stu-id="571e5-169">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="571e5-170">L’adresse IP publique de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="571e5-170">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="571e5-171">Vous pouvez afficher l’adresse IP publique à l’aide du portail Azure, de PowerShell ou de l’interface de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="571e5-171">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="571e5-172">Pour rechercher l’adresse IP publique de votre passerelle VPN à l’aide du portail Azure, accédez à **Passerelles de réseau virtuel**, puis cliquez sur le nom de votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="571e5-172">To find the Public IP address of your VPN gateway using the Azure portal, navigate to **Virtual network gateways**, then click the name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="571e5-173"><a name="CreateConnection"></a>7. Créer la connexion VPN</span><span class="sxs-lookup"><span data-stu-id="571e5-173"><a name="CreateConnection"></a>7. Create the VPN connection</span></span>

<span data-ttu-id="571e5-174">Créez la connexion VPN de site à site entre votre passerelle de réseau virtuel et votre périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="571e5-174">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="571e5-175"><a name="VerifyConnection"></a>8. Vérifier la connexion VPN</span><span class="sxs-lookup"><span data-stu-id="571e5-175"><a name="VerifyConnection"></a>8. Verify the VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="571e5-176"><a name="connectVM"></a>Se connecter à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="571e5-176"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="571e5-177"><a name="reset"></a>Réinitialisation d’une passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="571e5-177"><a name="reset"></a>How to reset a VPN gateway</span></span>

<span data-ttu-id="571e5-178">La réinitialisation d’une passerelle VPN Azure est utile si vous perdez la connectivité VPN entre différents locaux sur un ou plusieurs tunnels VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="571e5-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="571e5-179">Dans ce cas, vos périphériques VPN sur site fonctionnent tous correctement, mais ils ne sont pas en mesure d’établir des tunnels IPsec avec les passerelles VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="571e5-179">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="571e5-180">Pour obtenir la procédure, consultez [Réinitialiser une passerelle VPN](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="571e5-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="571e5-181"><a name="resize"></a>Modification d’une référence SKU de passerelle (redimensionnement d’une passerelle)</span><span class="sxs-lookup"><span data-stu-id="571e5-181"><a name="resize"></a>How to change a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="571e5-182">Pour obtenir la procédure permettant de modifier une référence SKU de passerelle, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="571e5-182">For the steps to change a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="571e5-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="571e5-183">Next steps</span></span>

* <span data-ttu-id="571e5-184">Pour plus d’informations sur le protocole BGP, consultez les articles [Vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [Comment configurer BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="571e5-184">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="571e5-185">Pour plus d’informations sur le tunneling forcé, consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement Azure Resource Manager](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="571e5-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="571e5-186">Pour plus d’informations sur les connexions haut actif-actif, consultez [Configuration haute disponibilité pour la connectivité entre les réseaux locaux et la connectivité entre deux réseaux virtuels](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="571e5-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
