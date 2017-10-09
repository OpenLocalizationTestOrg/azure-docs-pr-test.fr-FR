---
title: "Se connecter à votre tooan de réseau local sur le réseau virtuel Azure : VPN de Site à Site : CLI | Documents Microsoft"
description: "Toocreate étapes une connexion IPsec à partir de votre site réseau tooan réseau virtuel Azure sur hello Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN de site à site à l’aide de l’interface de ligne de commande (CLI)."
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
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="e32af-104">Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e32af-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="e32af-105">Cet article vous explique comment toouse hello CLI d’Azure toocreate une connexion de passerelle VPN de Site à Site à partir de votre toohello de réseau sur site réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e32af-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="e32af-106">étapes de Hello dans cet article s’appliquent à modèle de déploiement du Gestionnaire de ressources toohello.</span><span class="sxs-lookup"><span data-stu-id="e32af-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="e32af-107">Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="e32af-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e32af-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e32af-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="e32af-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e32af-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="e32af-110">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="e32af-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="e32af-111">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="e32af-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="e32af-113">Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="e32af-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="e32af-114">Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe.</span><span class="sxs-lookup"><span data-stu-id="e32af-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="e32af-115">Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="e32af-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e32af-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e32af-116">Before you begin</span></span>

<span data-ttu-id="e32af-117">Vérifiez que vous avez rempli hello suivant des critères avant de commencer la configuration :</span><span class="sxs-lookup"><span data-stu-id="e32af-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="e32af-118">Assurez-vous que vous disposez d’un périphérique VPN compatible et une personne qui est en mesure de tooconfigure il.</span><span class="sxs-lookup"><span data-stu-id="e32af-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="e32af-119">Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="e32af-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="e32af-120">Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="e32af-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="e32af-121">Cette adresse IP ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="e32af-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="e32af-122">Si vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans configuration du réseau de votre site, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous.</span><span class="sxs-lookup"><span data-stu-id="e32af-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="e32af-123">Lorsque vous créez cette configuration, vous devez spécifier hello plage préfixes d’adresse que Azure achemine emplacement local de tooyour.</span><span class="sxs-lookup"><span data-stu-id="e32af-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="e32af-124">Aucun des sous-réseaux hello de votre réseau local peuvent se chevauchant avec les sous-réseaux du réseau virtuel hello tooconnect à souhaitées sur.</span><span class="sxs-lookup"><span data-stu-id="e32af-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="e32af-125">Vérifiez que vous avez installé la version la plus récente des commandes CLI de hello (version 2.0 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="e32af-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="e32af-126">Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli) et [prise en main Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e32af-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="e32af-127"><a name="example"></a>Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="e32af-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="e32af-128">Vous pouvez utiliser hello suivant de valeurs toocreate un environnement de test, ou consultez les valeurs toothese toobetter comprendre les exemples hello dans cet article :</span><span class="sxs-lookup"><span data-stu-id="e32af-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

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

## <span data-ttu-id="e32af-129"><a name="Login"></a>1. Se connecter tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="e32af-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="e32af-130"><a name="rg"></a>2. Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="e32af-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="e32af-131">Hello exemple suivant crée un groupe de ressources nommé 'TestRG1' dans l’emplacement de 'eastus' hello.</span><span class="sxs-lookup"><span data-stu-id="e32af-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="e32af-132">Si vous avez déjà un groupe de ressources dans la région de hello que vous voulez toocreate votre réseau virtuel, vous pouvez utiliser qu’un à la place.</span><span class="sxs-lookup"><span data-stu-id="e32af-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="e32af-133"><a name="VNet"></a>3. Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e32af-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="e32af-134">Si vous n’avez pas encore un réseau virtuel, créez-le à l’aide de hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create) commande.</span><span class="sxs-lookup"><span data-stu-id="e32af-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="e32af-135">Lorsque vous créez un réseau virtuel, assurez-vous que vous spécifiez des espaces d’adressage hello ne chevauchent pas hello d’espaces d’adressage que vous disposez sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="e32af-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="e32af-136">Hello exemple suivant crée un réseau virtuel nommé « TestVNet1 » et un sous-réseau, 'Subnet1'.</span><span class="sxs-lookup"><span data-stu-id="e32af-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="e32af-137">4. <a name="gwsub"></a>Créez le sous-réseau de passerelle hello</span><span class="sxs-lookup"><span data-stu-id="e32af-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="e32af-138">Pour cette configuration, vous avez également besoin d’un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="e32af-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="e32af-139">passerelle de réseau virtuel Hello utilise un sous-réseau de passerelle qui contient les adresses IP hello qui sont utilisés par les services de la passerelle VPN hello.</span><span class="sxs-lookup"><span data-stu-id="e32af-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="e32af-140">Le sous-réseau de passerelle doit être nommé « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="e32af-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="e32af-141">Si vous choisissez un autre nom, vous créez un sous-réseau, mais Azure ne le traitera pas comme un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="e32af-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="e32af-142">taille de Hello du sous-réseau de passerelle hello que vous spécifiez dépend de configuration de la passerelle VPN hello que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="e32af-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="e32af-143">Bien qu’il soit possible de toocreate un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus grand qui inclut plusieurs adresses en sélectionnant /27 ou /28.</span><span class="sxs-lookup"><span data-stu-id="e32af-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="e32af-144">Permet à l’aide d’un sous-réseau de passerelle supérieure suffisamment IP adresses tooaccommodate futures configurations possibles.</span><span class="sxs-lookup"><span data-stu-id="e32af-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="e32af-145">Hello d’utilisation [créer de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#create) sous-réseau de passerelle commande toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e32af-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="e32af-146"><a name="localnet"></a>5. Créer une passerelle de réseau local hello</span><span class="sxs-lookup"><span data-stu-id="e32af-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="e32af-147">passerelle de réseau local Hello fait généralement référence d’emplacement de site tooyour.</span><span class="sxs-lookup"><span data-stu-id="e32af-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="e32af-148">Vous attribuez un nom par lequel Azure permettre faire référence tooit, puis spécifier l’adresse IP de hello au site de hello de toowhich de périphérique VPN hello localement, vous allez créer une connexion.</span><span class="sxs-lookup"><span data-stu-id="e32af-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="e32af-149">Vous spécifiez également préfixes d’adresses IP hello qui doivent être routés via le périphérique VPN toohello hello VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="e32af-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="e32af-150">vous spécifiez les préfixes d’adresse Hello sont des préfixes hello situés sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="e32af-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="e32af-151">Si votre réseau local change, vous pouvez facilement mettre à jour les préfixes hello.</span><span class="sxs-lookup"><span data-stu-id="e32af-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="e32af-152">Utilisez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="e32af-152">Use hello following values:</span></span>

* <span data-ttu-id="e32af-153">Hello *---adresse ip de passerelle* est l’adresse IP de hello de votre périphérique VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="e32af-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="e32af-154">Votre périphérique VPN ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="e32af-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="e32af-155">Hello *--préfixes d’adresse locale* est des espaces d’adressage de votre site.</span><span class="sxs-lookup"><span data-stu-id="e32af-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="e32af-156">Hello d’utilisation [az réseau local-passerelle créer](/cli/azure/network/local-gateway#create) commande tooadd une passerelle de réseau local avec plusieurs préfixes d’adresses :</span><span class="sxs-lookup"><span data-stu-id="e32af-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="e32af-157"><a name="PublicIP"></a>6. Demander une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="e32af-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="e32af-158">Une passerelle VPN doit avoir une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="e32af-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="e32af-159">Votre ressource d’adresse IP hello d’abord demander, puis consultez tooit lors de la création de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e32af-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="e32af-160">adresse IP de Hello est attribué dynamiquement les ressources toohello lors de la création de la passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="e32af-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="e32af-161">Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*.</span><span class="sxs-lookup"><span data-stu-id="e32af-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="e32af-162">Vous ne pouvez pas demander d’affectation d’adresse IP publique statique.</span><span class="sxs-lookup"><span data-stu-id="e32af-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="e32af-163">Toutefois, cela ne signifie pas que l’adresse IP de hello change après que qu’elle a été affectée passerelle VPN de tooyour.</span><span class="sxs-lookup"><span data-stu-id="e32af-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="e32af-164">Hello seule fois changements d’adresses IP publiques hello est hello lorsque la passerelle est supprimé et recréé.</span><span class="sxs-lookup"><span data-stu-id="e32af-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="e32af-165">Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="e32af-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="e32af-166">Hello d’utilisation [az réseau public-ip créer](/cli/azure/network/public-ip#create) commande toorequest une adresse IP publique dynamique.</span><span class="sxs-lookup"><span data-stu-id="e32af-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="e32af-167"><a name="CreateGateway"></a>7. Créer une passerelle VPN de hello</span><span class="sxs-lookup"><span data-stu-id="e32af-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="e32af-168">Créer la passerelle VPN de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="e32af-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="e32af-169">Création d’une passerelle VPN peut prendre jusqu'à too45 minutes ou plus toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e32af-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="e32af-170">Utilisez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="e32af-170">Use hello following values:</span></span>

* <span data-ttu-id="e32af-171">Hello *--type de passerelle* pour un Site à Site est configuration *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="e32af-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="e32af-172">type de passerelle Hello est toujours configuration toohello spécifique que vous implémentez.</span><span class="sxs-lookup"><span data-stu-id="e32af-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="e32af-173">Pour plus d’informations, consultez [Types de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="e32af-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="e32af-174">Hello *--vpn-type* peut être *RouteBased* (appelée tooas une passerelle dynamique dans certains documents), ou *basée sur des stratégies* (appelée tooas une passerelle statique dans certains documentation).</span><span class="sxs-lookup"><span data-stu-id="e32af-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="e32af-175">Hello est toorequirements spécifique du périphérique hello que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="e32af-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="e32af-176">Pour plus d’informations sur les types de passerelle VPN, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="e32af-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="e32af-177">Sélectionnez hello SKU de passerelle que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="e32af-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="e32af-178">Des limites de configuration s’appliquent à certaines références (SKU).</span><span class="sxs-lookup"><span data-stu-id="e32af-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="e32af-179">Pour plus d’informations, consultez l’article [Références (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="e32af-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="e32af-180">Créer une passerelle VPN de hello à l’aide de hello [créer de passerelle de réseau virtuel de réseau az](/cli/azure/network/vnet-gateway#create) commande.</span><span class="sxs-lookup"><span data-stu-id="e32af-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="e32af-181">Si vous exécutez cette commande à l’aide de hello '--aucune - attente' paramètre, vous ne voyez pas vos commentaires ou la sortie.</span><span class="sxs-lookup"><span data-stu-id="e32af-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="e32af-182">Ce paramètre permet de hello passerelle toocreate en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="e32af-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="e32af-183">Il prend environ 45 minutes toocreate une passerelle.</span><span class="sxs-lookup"><span data-stu-id="e32af-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="e32af-184"><a name="VPNDevice"></a>8. Configuration de votre périphérique VPN</span><span class="sxs-lookup"><span data-stu-id="e32af-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="e32af-185">Réseau local de tooan connexions site à Site requièrent un périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="e32af-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="e32af-186">Dans cette étape, vous configurez votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="e32af-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="e32af-187">Lorsque vous configurez votre périphérique VPN, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="e32af-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="e32af-188">Une clé partagée.</span><span class="sxs-lookup"><span data-stu-id="e32af-188">A shared key.</span></span> <span data-ttu-id="e32af-189">Cela est hello même partagé clé que vous spécifiez lors de la création de votre connexion VPN de Site à Site.</span><span class="sxs-lookup"><span data-stu-id="e32af-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="e32af-190">Dans nos exemples, nous utilisons une clé partagée basique.</span><span class="sxs-lookup"><span data-stu-id="e32af-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="e32af-191">Nous conseillons de générer un toouse de clé plus complexe.</span><span class="sxs-lookup"><span data-stu-id="e32af-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="e32af-192">Hello adresse IP publique de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e32af-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="e32af-193">Vous pouvez afficher l’adresse IP publique de hello à l’aide de hello portail Azure, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="e32af-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="e32af-194">toofind hello adresse IP publique de votre passerelle de réseau virtuel, utilisez hello [liste public-ip de réseau az](/cli/azure/network/public-ip#list) commande.</span><span class="sxs-lookup"><span data-stu-id="e32af-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="e32af-195">Pour faciliter la lecture, la sortie de hello est liste de hello toodisplay mis en forme des adresses IP publiques au format de table.</span><span class="sxs-lookup"><span data-stu-id="e32af-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="e32af-196"><a name="CreateConnection"></a>9. Créer la connexion VPN de hello</span><span class="sxs-lookup"><span data-stu-id="e32af-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="e32af-197">Créer un réseau VPN hello Site à Site entre votre passerelle de réseau virtuel et votre périphérique VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="e32af-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="e32af-198">Payer une attention toute particulière toohello partagé valeur de clé, qui doit correspondre à hello configuré partagé valeur de clé de votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="e32af-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="e32af-199">Créer la connexion hello à l’aide de hello [créer de connexion de vpn de réseau az](/cli/azure/network/vpn-connection#create) commande.</span><span class="sxs-lookup"><span data-stu-id="e32af-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="e32af-200">Après quelques instants, hello connexion sera établie.</span><span class="sxs-lookup"><span data-stu-id="e32af-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="e32af-201"><a name="toverify"></a>10. Vérifiez la connexion VPN de hello</span><span class="sxs-lookup"><span data-stu-id="e32af-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="e32af-202">Si vous souhaitez une autre méthode tooverify toouse votre connexion, consultez [vérifier une connexion de passerelle VPN](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e32af-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="e32af-203"><a name="connectVM"></a>machine virtuelle de tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="e32af-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="e32af-204"><a name="tasks"></a>Tâches courantes</span><span class="sxs-lookup"><span data-stu-id="e32af-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="e32af-205">Cette section contient des commandes courantes qui sont utiles lorsque vous travaillez avec des configurations de site à site.</span><span class="sxs-lookup"><span data-stu-id="e32af-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="e32af-206">Pour hello une liste complète des commandes de mise en réseau CLI, consultez [CLI d’Azure - mise en réseau](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="e32af-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e32af-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e32af-207">Next steps</span></span>

* <span data-ttu-id="e32af-208">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="e32af-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="e32af-209">Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="e32af-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="e32af-210">Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e32af-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="e32af-211">Pour plus d’informations sur le tunneling forcé, consultez [Configuration du tunneling forcé à l’aide du modèle de déploiement classique](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="e32af-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="e32af-212">Pour plus d’informations sur les connexions haut actif-actif, consultez [Configuration haute disponibilité pour la connectivité entre les réseaux locaux et la connectivité entre deux réseaux virtuels](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="e32af-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="e32af-213">Pour obtenir la liste des commandes de mise en réseau de l’interface de ligne de commande Azure, consultez l’article [Interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="e32af-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>