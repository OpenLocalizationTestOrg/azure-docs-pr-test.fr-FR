---
title: "Se connecter à votre tooan de réseau local sur le réseau virtuel Azure : VPN de Site à Site : portail | Documents Microsoft"
description: "Toocreate étapes une connexion IPsec à partir de votre site réseau tooan réseau virtuel Azure sur hello Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN Site à Site entre différents locaux à l’aide du portail de hello."
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
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="f9d2a-104">Créer une connexion de Site à Site dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f9d2a-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="f9d2a-105">Cet article vous explique comment toouse hello toocreate portail Azure, une connexion de passerelle VPN de Site à Site à partir de votre toohello de réseau sur site réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="f9d2a-106">étapes de Hello dans cet article s’appliquent à modèle de déploiement du Gestionnaire de ressources toohello.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="f9d2a-107">Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="f9d2a-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9d2a-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f9d2a-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="f9d2a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9d2a-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="f9d2a-110">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="f9d2a-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="f9d2a-111">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="f9d2a-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="f9d2a-112">Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="f9d2a-113">Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="f9d2a-114">Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="f9d2a-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f9d2a-116">Before you begin</span></span>

<span data-ttu-id="f9d2a-117">Vérifiez que vous avez rempli hello suivant des critères avant de commencer votre configuration :</span><span class="sxs-lookup"><span data-stu-id="f9d2a-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="f9d2a-118">Assurez-vous que vous disposez d’un périphérique VPN compatible et une personne qui est en mesure de tooconfigure il.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="f9d2a-119">Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="f9d2a-120">Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="f9d2a-121">Cette adresse IP ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="f9d2a-122">Si vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans configuration du réseau de votre site, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="f9d2a-123">Lorsque vous créez cette configuration, vous devez spécifier hello plage préfixes d’adresse que Azure achemine emplacement local de tooyour.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="f9d2a-124">Aucun des sous-réseaux hello de votre réseau local peuvent se chevauchant avec les sous-réseaux du réseau virtuel hello tooconnect à souhaitées sur.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="f9d2a-125"><a name="values"></a>Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="f9d2a-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="f9d2a-126">exemples de Hello dans cet article utilisent hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="f9d2a-127">Vous pouvez utiliser ces valeurs de toocreate un environnement de test, ou consultez toothem toobetter comprendre les exemples hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="f9d2a-128">**Nom du réseau virtuel :** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="f9d2a-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="f9d2a-129">**Espace d’adressage :**</span><span class="sxs-lookup"><span data-stu-id="f9d2a-129">**Address Space:**</span></span> 
  * <span data-ttu-id="f9d2a-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f9d2a-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="f9d2a-131">10.12.0.0/16 (facultatif pour cet exercice)</span><span class="sxs-lookup"><span data-stu-id="f9d2a-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="f9d2a-132">**Sous-réseaux :**</span><span class="sxs-lookup"><span data-stu-id="f9d2a-132">**Subnets:**</span></span>
  * <span data-ttu-id="f9d2a-133">FrontEnd : 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="f9d2a-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="f9d2a-134">BackEnd : 10.12.0.0/24 (facultatif pour cet exercice)</span><span class="sxs-lookup"><span data-stu-id="f9d2a-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="f9d2a-135">**Sous-réseau de passerelle :** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="f9d2a-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="f9d2a-136">**Groupe de ressources :** TestRG1</span><span class="sxs-lookup"><span data-stu-id="f9d2a-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="f9d2a-137">**Emplacement :** États-Unis de l’Est</span><span class="sxs-lookup"><span data-stu-id="f9d2a-137">**Location:** East US</span></span>
* <span data-ttu-id="f9d2a-138">**Serveur DNS**  Facultatif.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="f9d2a-139">adresse IP de Hello de votre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="f9d2a-140">**Nom de passerelle de réseau virtuel :** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="f9d2a-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="f9d2a-141">**Adresse IP publique :** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="f9d2a-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="f9d2a-142">**Type de VPN :** Route-based</span><span class="sxs-lookup"><span data-stu-id="f9d2a-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="f9d2a-143">**Type de connexion :** Site-to-site (IPsec)</span><span class="sxs-lookup"><span data-stu-id="f9d2a-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="f9d2a-144">**Type de passerelle :** VPN</span><span class="sxs-lookup"><span data-stu-id="f9d2a-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="f9d2a-145">**Nom de passerelle de réseau local :** Site2</span><span class="sxs-lookup"><span data-stu-id="f9d2a-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="f9d2a-146">**Nom de connexion :** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="f9d2a-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="f9d2a-147"><a name="CreatVNet"></a>1. Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f9d2a-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="f9d2a-148"><a name="dns"></a>2. Spécifier un serveur DNS</span><span class="sxs-lookup"><span data-stu-id="f9d2a-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="f9d2a-149">DNS n’est pas requis toocreate un Site à Site connexion.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="f9d2a-150">Toutefois, si vous souhaitez toohave la résolution de noms pour les ressources qui sont déployés tooyour des réseaux virtuels, vous devez spécifier un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="f9d2a-151">Ce paramètre vous permet de spécifier le serveur DNS hello que vous souhaitez toouse pour la résolution de nom pour ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="f9d2a-152">Il n'entraîne pas la création d'un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-152">It does not create a DNS server.</span></span> <span data-ttu-id="f9d2a-153">Pour plus d’informations sur la résolution de noms pour les machines virtuelles, consultez [Résolution de noms pour les machines virtuelles et instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="f9d2a-154"><a name="gatewaysubnet"></a>3. Créez le sous-réseau de passerelle hello</span><span class="sxs-lookup"><span data-stu-id="f9d2a-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="f9d2a-155"><a name="VNetGateway"></a>4. Créer une passerelle VPN de hello</span><span class="sxs-lookup"><span data-stu-id="f9d2a-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="f9d2a-156"><a name="LocalNetworkGateway"></a>5. Créer une passerelle de réseau local hello</span><span class="sxs-lookup"><span data-stu-id="f9d2a-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="f9d2a-157">passerelle de réseau local Hello fait généralement référence d’emplacement de site tooyour.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="f9d2a-158">Vous attribuez un nom par lequel Azure permettre faire référence tooit, puis spécifier l’adresse IP de hello au site de hello de toowhich de périphérique VPN hello localement, vous allez créer une connexion.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="f9d2a-159">Vous spécifiez également préfixes d’adresses IP hello qui doivent être routés via le périphérique VPN toohello hello VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="f9d2a-160">vous spécifiez les préfixes d’adresse Hello sont des préfixes hello situés sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="f9d2a-161">Si vos modifications de réseau local, ou vous avez besoin d’adresse IP publique de toochange hello pour le périphérique VPN de hello, vous pouvez facilement mettre à jour les valeurs hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="f9d2a-162"><a name="VPNDevice"></a>6. Configuration de votre périphérique VPN</span><span class="sxs-lookup"><span data-stu-id="f9d2a-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="f9d2a-163">Réseau local de tooan connexions site à Site requièrent un périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="f9d2a-164">Dans cette étape, vous configurez votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="f9d2a-165">Lorsque vous configurez votre périphérique VPN, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="f9d2a-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="f9d2a-166">Une clé partagée.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-166">A shared key.</span></span> <span data-ttu-id="f9d2a-167">Cela est hello même partagé clé que vous spécifiez lors de la création de votre connexion VPN de Site à Site.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="f9d2a-168">Dans nos exemples, nous utilisons une clé partagée basique.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="f9d2a-169">Nous conseillons de générer un toouse de clé plus complexe.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="f9d2a-170">Hello adresse IP publique de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="f9d2a-171">Vous pouvez afficher l’adresse IP publique de hello à l’aide de hello portail Azure, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="f9d2a-172">toofind hello adresse IP publique de votre passerelle VPN à l’aide de hello portail Azure, accédez trop**les passerelles de réseau virtuel**, puis cliquez sur nom hello de votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="f9d2a-173"><a name="CreateConnection"></a>7. Créer la connexion VPN de hello</span><span class="sxs-lookup"><span data-stu-id="f9d2a-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="f9d2a-174">Créer un réseau VPN hello Site à Site entre votre passerelle de réseau virtuel et votre périphérique VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="f9d2a-175"><a name="VerifyConnection"></a>8. Vérifiez la connexion VPN de hello</span><span class="sxs-lookup"><span data-stu-id="f9d2a-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="f9d2a-176"><a name="connectVM"></a>machine virtuelle de tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="f9d2a-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="f9d2a-177"><a name="reset"></a>Comment tooreset une passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="f9d2a-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="f9d2a-178">La réinitialisation d’une passerelle VPN Azure est utile si vous perdez la connectivité VPN entre différents locaux sur un ou plusieurs tunnels VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="f9d2a-179">Dans ce cas, vos périphériques VPN sur site sont tous les fonctionne correctement, mais sont tooestablish n’a pas pu les tunnels IPsec avec les passerelles VPN Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f9d2a-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="f9d2a-180">Pour obtenir la procédure, consultez [Réinitialiser une passerelle VPN](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="f9d2a-181"><a name="resize"></a>Comment toochange une passerelle de référence (SKU) (redimensionner une passerelle)</span><span class="sxs-lookup"><span data-stu-id="f9d2a-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="f9d2a-182">Les étapes de hello toochange une référence (SKU) de la passerelle, consultez [SKU de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9d2a-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9d2a-183">Next steps</span></span>

* <span data-ttu-id="f9d2a-184">Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="f9d2a-185">Pour plus d’informations sur le tunneling forcé, consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement classique](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="f9d2a-186">Pour plus d’informations sur les connexions haut actif-actif, consultez [Configuration haute disponibilité pour la connectivité entre les réseaux locaux et la connectivité entre deux réseaux virtuels](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="f9d2a-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
