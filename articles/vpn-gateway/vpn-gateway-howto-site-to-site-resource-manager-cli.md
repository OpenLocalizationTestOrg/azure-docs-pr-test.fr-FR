---
title: "Connecter votre réseau local à un réseau virtuel Azure : VPN site à site : interface de ligne de commande | Microsoft Docs"
description: "Étapes de création d’une connexion IPsec entre votre réseau local et un réseau virtuel Azure via l’Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN de site à site à l’aide de l’interface de ligne de commande (CLI)."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 019c5421dc470b18c9087417b93c241cc5730f77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="aa2ee-104">Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="aa2ee-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="aa2ee-105">Cet article vous explique comment utiliser l’interface de ligne de commande Azure pour créer une connexion de passerelle VPN de site à site à partir de votre réseau local vers le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-105">This article shows you how to use the Azure CLI to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="aa2ee-106">Les étapes mentionnées dans cet article s’appliquent au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="aa2ee-107">Vous pouvez également créer cette configuration à l’aide d’un autre outil ou modèle de déploiement en sélectionnant une option différente dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="aa2ee-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa2ee-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="aa2ee-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="aa2ee-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa2ee-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="aa2ee-110">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="aa2ee-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="aa2ee-111">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="aa2ee-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="aa2ee-113">Une connexion de passerelle VPN de site à site permet de connecter votre réseau local à un réseau virtuel Azure via un tunnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="aa2ee-114">Ce type de connexion requiert un périphérique VPN local disposant d’une adresse IP publique exposée en externe.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="aa2ee-115">Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="aa2ee-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="aa2ee-116">Before you begin</span></span>

<span data-ttu-id="aa2ee-117">Vérifiez que vous disposez des éléments ci-dessous avant de commencer votre configuration :</span><span class="sxs-lookup"><span data-stu-id="aa2ee-117">Verify that you have met the following criteria before beginning configuration:</span></span>

* <span data-ttu-id="aa2ee-118">Veillez à disposer d’un périphérique VPN compatible et à être entouré d’une personne en mesure de le configurer.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="aa2ee-119">Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="aa2ee-120">Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="aa2ee-121">Cette adresse IP ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="aa2ee-122">Si vous ne maîtrisez pas les plages d’adresses IP situées dans votre configuration de réseau local, vous devez contacter une personne en mesure de vous aider.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="aa2ee-123">Lorsque vous créez cette configuration, vous devez spécifier les préfixes des plages d’adresses IP qu’Azure acheminera vers votre emplacement local.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="aa2ee-124">Aucun des sous-réseaux de votre réseau local ne peut chevaucher les sous-réseaux du réseau virtuel auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="aa2ee-125">Vérifiez que vous avez installé la dernière version des commandes CLI (versions 2.0 ou ultérieures).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-125">Verify that you have installed latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="aa2ee-126">Pour plus d’informations sur l’installation des commandes CLI, consultez [Install Azure CLI 2.0](/cli/azure/install-azure-cli) (Installer l’interface de ligne de commande Azure 2.0) et [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Prise en main de l’interface de ligne de commande Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-126">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="aa2ee-127"><a name="example"></a>Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="aa2ee-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="aa2ee-128">Vous pouvez utiliser ces valeurs pour créer un environnement de test ou vous y référer pour mieux comprendre les exemples de cet article :</span><span class="sxs-lookup"><span data-stu-id="aa2ee-128">You can use the following values to create a test environment, or refer to these values to better understand the examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="aa2ee-129"><a name="Login"></a>1. Connexion à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="aa2ee-129"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="aa2ee-130"><a name="rg"></a>2. Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="aa2ee-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="aa2ee-131">L’exemple suivant crée un groupe de ressources nommé « TestRG1 » à l’emplacement « eastus ».</span><span class="sxs-lookup"><span data-stu-id="aa2ee-131">The following example creates a resource group named 'TestRG1' in the 'eastus' location.</span></span> <span data-ttu-id="aa2ee-132">Si vous disposez déjà d’un groupe de ressources dans la région où vous souhaitez créer votre réseau virtuel, vous pouvez l’utiliser à la place de l’exemple donné.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-132">If you already have a resource group in the region that you want to create your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="aa2ee-133"><a name="VNet"></a>3. Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="aa2ee-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="aa2ee-134">Si vous n’avez pas de réseau virtuel, créez-en un à l’aide de la commande [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-134">If you don't already have a virtual network, create one using the [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="aa2ee-135">Lorsque vous créez un réseau virtuel, vérifiez que les espaces d’adressage que vous spécifiez ne chevauchent pas les espaces d’adressage de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-135">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="aa2ee-136">L’exemple suivant permet de créer un réseau virtuel nommé « TestVNet1 » et un sous-réseau nommé « Subnet1 ».</span><span class="sxs-lookup"><span data-stu-id="aa2ee-136">The following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="aa2ee-137">4. <a name="gwsub"></a>Créer le sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="aa2ee-137">4. <a name="gwsub"></a>Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="aa2ee-138">Pour cette configuration, vous avez également besoin d’un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="aa2ee-139">La passerelle de réseau virtuel utilise un sous-réseau de passerelle qui contient les adresses IP utilisées par les services de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-139">The virtual network gateway uses a gateway subnet that contains the IP addresses that are used by the VPN gateway services.</span></span> <span data-ttu-id="aa2ee-140">Le sous-réseau de passerelle doit être nommé « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="aa2ee-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="aa2ee-141">Si vous choisissez un autre nom, vous créez un sous-réseau, mais Azure ne le traitera pas comme un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="aa2ee-142">La taille du sous-réseau de passerelle que vous spécifiez dépend de la configuration de la passerelle VPN que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-142">The size of the gateway subnet that you specify depends on the VPN gateway configuration that you want to create.</span></span> <span data-ttu-id="aa2ee-143">Bien qu’il soit possible de créer un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus vaste qui inclut un plus grand nombre d’adresses en sélectionnant /27 ou /28.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-143">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="aa2ee-144">En choisissant un sous-réseau de passerelle plus vaste, vous disposez de suffisamment d’adresses IP pour prendre en charge d’éventuelles configurations futures.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-144">Using a larger gateway subnet allows for enough IP addresses to accommodate possible future configurations.</span></span>

<span data-ttu-id="aa2ee-145">Utilisez la commande [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) pour créer le sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-145">Use the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command to create the gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="aa2ee-146"><a name="localnet"></a>5. Créer la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="aa2ee-146"><a name="localnet"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="aa2ee-147">La passerelle de réseau local fait généralement référence à votre emplacement local.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-147">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="aa2ee-148">Donnez au site un nom auquel Azure pourra se référer, puis spécifiez l’adresse IP du périphérique VPN local vers lequel vous allez créer une connexion.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-148">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="aa2ee-149">Spécifiez également les préfixes d’adresses IP qui seront acheminés via la passerelle VPN vers le périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-149">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="aa2ee-150">Les préfixes d’adresses que vous spécifiez sont les préfixes situés sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-150">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="aa2ee-151">Vous pouvez facilement mettre à jour ces préfixes si votre réseau local change.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-151">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="aa2ee-152">Utilisez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa2ee-152">Use the following values:</span></span>

* <span data-ttu-id="aa2ee-153">La valeur *--gateway-ip-address* est l’adresse IP de votre périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-153">The *--gateway-ip-address* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="aa2ee-154">Votre périphérique VPN ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="aa2ee-155">La valeur *--local-address-prefixes* représente vos espaces d’adressage local.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-155">The *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="aa2ee-156">Utilisez la commande [az network local-gateway create](/cli/azure/network/local-gateway#create) pour ajouter une passerelle de réseau local avec plusieurs préfixes d’adresses :</span><span class="sxs-lookup"><span data-stu-id="aa2ee-156">Use the [az network local-gateway create](/cli/azure/network/local-gateway#create) command to add a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="aa2ee-157"><a name="PublicIP"></a>6. Demander une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="aa2ee-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="aa2ee-158">Une passerelle VPN doit avoir une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="aa2ee-159">Vous commencez par demander la ressource d’adresse IP, puis vous y faites référence lors de la création de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-159">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="aa2ee-160">L’adresse IP est affectée dynamiquement à la ressource lors de la création de la passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-160">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="aa2ee-161">Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="aa2ee-162">Vous ne pouvez pas demander d’affectation d’adresse IP publique statique.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="aa2ee-163">Toutefois, cela ne signifie pas que l’adresse IP change après son affectation à votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-163">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="aa2ee-164">L’adresse IP publique change uniquement lorsque la passerelle est supprimée, puis recréée.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-164">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="aa2ee-165">Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="aa2ee-166">Utilisez la commande [az network public-ip create](/cli/azure/network/public-ip#create) pour demander une adresse IP publique dynamique.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-166">Use the [az network public-ip create](/cli/azure/network/public-ip#create) command to request a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="aa2ee-167"><a name="CreateGateway"></a>7. Créer la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="aa2ee-167"><a name="CreateGateway"></a>7. Create the VPN gateway</span></span>

<span data-ttu-id="aa2ee-168">Créez la passerelle VPN de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-168">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="aa2ee-169">La création d’une passerelle VPN peut prendre 45 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-169">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="aa2ee-170">Utilisez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa2ee-170">Use the following values:</span></span>

* <span data-ttu-id="aa2ee-171">Le paramètre *--gateway-type* pour une configuration de site à site est *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-171">The *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="aa2ee-172">Le type de passerelle dépend toujours de la configuration que vous implémentez.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-172">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="aa2ee-173">Pour plus d’informations, consultez [Types de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="aa2ee-174">Le paramètre *--vpn-type* peut avoir pour valeur *RouteBased* (appelé passerelle dynamique dans certaines documentations) ou *PolicyBased* (appelé passerelle statique dans certaines documentations).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-174">The *--vpn-type* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="aa2ee-175">Le paramètre est spécifique aux exigences du périphérique auquel vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-175">The setting is specific to requirements of the device that you are connecting to.</span></span> <span data-ttu-id="aa2ee-176">Pour plus d’informations sur les types de passerelle VPN, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="aa2ee-177">Sélectionnez la référence SKU de la passerelle que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-177">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="aa2ee-178">Des limites de configuration s’appliquent à certaines références (SKU).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="aa2ee-179">Pour plus d’informations, consultez l’article [Références (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="aa2ee-180">Créez la passerelle VPN à l’aide de la commande [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-180">Create the VPN gateway using the [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="aa2ee-181">Si vous exécutez cette commande à l’aide du paramètre « --no-wait », vous ne voyez aucun commentaire ni sortie.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-181">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="aa2ee-182">Ce paramètre permet à la passerelle d’être créée en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-182">This parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="aa2ee-183">La création d’une passerelle prend environ 45 minutes.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-183">It takes around 45 minutes to create a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="aa2ee-184"><a name="VPNDevice"></a>8. Configuration de votre périphérique VPN</span><span class="sxs-lookup"><span data-stu-id="aa2ee-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="aa2ee-185">Les connexions site à site vers un réseau local nécessitent un périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-185">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="aa2ee-186">Dans cette étape, vous configurez votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="aa2ee-187">Pour configurer votre périphérique VPN, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aa2ee-187">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="aa2ee-188">Une clé partagée.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-188">A shared key.</span></span> <span data-ttu-id="aa2ee-189">Il s’agit de la clé partagée spécifiée lors de la création de la connexion VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-189">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="aa2ee-190">Dans nos exemples, nous utilisons une clé partagée basique.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="aa2ee-191">Nous vous conseillons de générer une clé plus complexe.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-191">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="aa2ee-192">L’adresse IP publique de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-192">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="aa2ee-193">Vous pouvez afficher l’adresse IP publique à l’aide du portail Azure, de PowerShell ou de l’interface de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-193">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="aa2ee-194">Pour trouver l’adresse IP publique de votre passerelle de réseau virtuel, utilisez la commande [az network public-ip list](/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-194">To find the public IP address of your virtual network gateway, use the [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="aa2ee-195">Pour faciliter la lecture, la sortie est mise en forme pour afficher la liste des adresses IP publiques sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-195">For easy reading, the output is formatted to display the list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="aa2ee-196"><a name="CreateConnection"></a>9. Créer la connexion VPN</span><span class="sxs-lookup"><span data-stu-id="aa2ee-196"><a name="CreateConnection"></a>9. Create the VPN connection</span></span>

<span data-ttu-id="aa2ee-197">Créez la connexion VPN de site à site entre votre passerelle de réseau virtuel et votre périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-197">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="aa2ee-198">Soyez particulièrement attentif à la valeur de clé partagée qui doit correspondre à la valeur de clé partagée configurée pour votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-198">Pay particular attention to the shared key value, which must match the configured shared key value for your VPN device.</span></span>

<span data-ttu-id="aa2ee-199">Créez la connexion à l’aide de la commande [az network vpn-connection create](/cli/azure/network/vpn-connection#create).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-199">Create the connection using the [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="aa2ee-200">Après un bref délai, la connexion sera établie.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-200">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="aa2ee-201"><a name="toverify"></a>10. Vérifier la connexion VPN</span><span class="sxs-lookup"><span data-stu-id="aa2ee-201"><a name="toverify"></a>10. Verify the VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="aa2ee-202">Si vous souhaitez utiliser une autre méthode pour vérifier votre connexion, consultez l’article [Vérifier une connexion de passerelle VPN](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-202">If you want to use another method to verify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="aa2ee-203"><a name="connectVM"></a>Se connecter à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="aa2ee-203"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="aa2ee-204"><a name="tasks"></a>Tâches courantes</span><span class="sxs-lookup"><span data-stu-id="aa2ee-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="aa2ee-205">Cette section contient des commandes courantes qui sont utiles lorsque vous travaillez avec des configurations de site à site.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="aa2ee-206">Pour obtenir la liste complète des commandes de mise en réseau CLI, consultez [Networking - az network](/cli/azure/network) (Mise en réseau - az network).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-206">For the full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="aa2ee-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa2ee-207">Next steps</span></span>

* <span data-ttu-id="aa2ee-208">Une fois la connexion achevée, vous pouvez ajouter des machines virtuelles à vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="aa2ee-208">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="aa2ee-209">Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="aa2ee-210">Pour plus d’informations sur le protocole BGP, consultez les articles [Vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [Comment configurer BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-210">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="aa2ee-211">Pour plus d’informations sur le tunneling forcé, consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement Azure Resource Manager](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="aa2ee-212">Pour plus d’informations sur les connexions haut actif-actif, consultez [Configuration haute disponibilité pour la connectivité entre les réseaux locaux et la connectivité entre deux réseaux virtuels](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="aa2ee-213">Pour obtenir la liste des commandes de mise en réseau de l’interface de ligne de commande Azure, consultez l’article [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="aa2ee-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>