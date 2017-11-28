---
title: "Se connecter à votre tooan de réseau local sur le réseau virtuel Azure : VPN de Site à Site : PowerShell | Documents Microsoft"
description: "Toocreate étapes une connexion IPsec à partir de votre site réseau tooan réseau virtuel Azure sur hello Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN de site à site à l’aide de PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="8bd04-104">Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd04-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="8bd04-105">Cet article explique comment toouse connexion de passerelle PowerShell toocreate un Site à Site VPN à partir de votre site réseau toohello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8bd04-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="8bd04-106">étapes de Hello dans cet article s’appliquent à modèle de déploiement du Gestionnaire de ressources toohello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="8bd04-107">Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="8bd04-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bd04-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8bd04-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="8bd04-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd04-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="8bd04-110">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="8bd04-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="8bd04-111">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="8bd04-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="8bd04-112">Portail Classic (classique)</span><span class="sxs-lookup"><span data-stu-id="8bd04-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="8bd04-113">Une connexion de passerelle VPN de Site à Site est utilisé tooconnect votre site réseau tooan réseau virtuel Azure via un tunnel VPN de IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="8bd04-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="8bd04-114">Ce type de connexion requiert un VPN périphérique local qui a un tooit d’adresse IP publique externe.</span><span class="sxs-lookup"><span data-stu-id="8bd04-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="8bd04-115">Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="8bd04-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="8bd04-117"><a name="before"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8bd04-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="8bd04-118">Vérifiez que vous avez rempli hello suivant des critères avant de commencer votre configuration :</span><span class="sxs-lookup"><span data-stu-id="8bd04-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="8bd04-119">Assurez-vous que vous disposez d’un périphérique VPN compatible et une personne qui est en mesure de tooconfigure il.</span><span class="sxs-lookup"><span data-stu-id="8bd04-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="8bd04-120">Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="8bd04-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="8bd04-121">Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="8bd04-122">Cette adresse IP ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="8bd04-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="8bd04-123">Si vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans configuration du réseau de votre site, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous.</span><span class="sxs-lookup"><span data-stu-id="8bd04-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="8bd04-124">Lorsque vous créez cette configuration, vous devez spécifier hello plage préfixes d’adresse que Azure achemine emplacement local de tooyour.</span><span class="sxs-lookup"><span data-stu-id="8bd04-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="8bd04-125">Aucun des sous-réseaux hello de votre réseau local peuvent se chevauchant avec les sous-réseaux du réseau virtuel hello tooconnect à souhaitées sur.</span><span class="sxs-lookup"><span data-stu-id="8bd04-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="8bd04-126">Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd04-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="8bd04-127">Applets de commande PowerShell sont fréquemment mis à jour et vous en aurez besoin tooupdate votre PowerShell applets de commande tooget hello dernières fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="8bd04-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="8bd04-128">Si vous ne mettez à jour vos applets de commande PowerShell, les valeurs hello spécifiées peuvent échouer.</span><span class="sxs-lookup"><span data-stu-id="8bd04-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="8bd04-129">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur le téléchargement et installation des applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bd04-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="8bd04-130"><a name="example"></a>Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="8bd04-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="8bd04-131">exemples de Hello dans cet article utilisent hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="8bd04-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="8bd04-132">Vous pouvez utiliser ces valeurs de toocreate un environnement de test, ou consultez toothem toobetter comprendre les exemples hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8bd04-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="8bd04-133"><a name="Login"></a>1. Se connecter tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="8bd04-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="8bd04-134"><a name="VNet"></a>2. Créer un réseau virtuel et un sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="8bd04-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="8bd04-135">Si vous n’avez pas de réseau virtuel, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="8bd04-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="8bd04-136">Lorsque vous créez un réseau virtuel, assurez-vous que vous spécifiez des espaces d’adressage hello ne chevauchent pas hello d’espaces d’adressage que vous disposez sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="8bd04-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="8bd04-137"><a name="vnet"></a>toocreate un réseau virtuel et un sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="8bd04-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="8bd04-138">Cet exemple permet de créer un réseau virtuel et un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="8bd04-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="8bd04-139">Si vous disposez déjà d’un réseau virtuel que vous devez tooadd un sous-réseau de passerelle pour voir [tooadd un réseau virtuel tooa sous-réseau passerelle que vous avez déjà créé](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="8bd04-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="8bd04-140">Créez un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="8bd04-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="8bd04-141">Créez votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8bd04-141">Create your virtual network.</span></span>

1. <span data-ttu-id="8bd04-142">Définir les variables de hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="8bd04-143">Créer hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8bd04-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="8bd04-144"><a name="gatewaysubnet"></a>tooadd un réseau virtuel de tooa de sous-réseau de passerelle que vous avez déjà créé</span><span class="sxs-lookup"><span data-stu-id="8bd04-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="8bd04-145">Définir les variables de hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="8bd04-146">Créer un sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="8bd04-147">Définir la configuration hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="8bd04-148">3. <a name="localnet"></a>Créer une passerelle de réseau local hello</span><span class="sxs-lookup"><span data-stu-id="8bd04-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="8bd04-149">passerelle de réseau local Hello fait généralement référence d’emplacement de site tooyour.</span><span class="sxs-lookup"><span data-stu-id="8bd04-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="8bd04-150">Vous attribuez un nom par lequel Azure permettre faire référence tooit, puis spécifier l’adresse IP de hello au site de hello de toowhich de périphérique VPN hello localement, vous allez créer une connexion.</span><span class="sxs-lookup"><span data-stu-id="8bd04-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="8bd04-151">Vous spécifiez également préfixes d’adresses IP hello qui doivent être routés via le périphérique VPN toohello hello VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="8bd04-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="8bd04-152">vous spécifiez les préfixes d’adresse Hello sont des préfixes hello situés sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="8bd04-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="8bd04-153">Si votre réseau local change, vous pouvez facilement mettre à jour les préfixes hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="8bd04-154">Utilisez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="8bd04-154">Use hello following values:</span></span>

* <span data-ttu-id="8bd04-155">Hello *GatewayIPAddress* est l’adresse IP de hello de votre périphérique VPN sur site.</span><span class="sxs-lookup"><span data-stu-id="8bd04-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="8bd04-156">Votre périphérique VPN ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="8bd04-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="8bd04-157">Hello *AddressPrefix* est votre site sur l’espace d’adressage.</span><span class="sxs-lookup"><span data-stu-id="8bd04-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="8bd04-158">tooadd une passerelle de réseau local avec un préfixe d’adresse unique :</span><span class="sxs-lookup"><span data-stu-id="8bd04-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="8bd04-159">tooadd une passerelle de réseau local avec plusieurs préfixes d’adresses :</span><span class="sxs-lookup"><span data-stu-id="8bd04-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="8bd04-160">toomodify les préfixes d’adresse IP de la passerelle de réseau local :</span><span class="sxs-lookup"><span data-stu-id="8bd04-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="8bd04-161">Parfois, les préfixes de votre passerelle de réseau local changent.</span><span class="sxs-lookup"><span data-stu-id="8bd04-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="8bd04-162">Hello vous étapes toomodify votre adresse IP préfixes varient selon que vous avez créé une connexion de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="8bd04-163">Consultez hello [modifier les préfixes d’adresse d’une passerelle de réseau local](#modify) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="8bd04-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="8bd04-164"><a name="PublicIP"></a>4. Demander une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="8bd04-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="8bd04-165">Une passerelle VPN doit avoir une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8bd04-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="8bd04-166">Votre ressource d’adresse IP hello d’abord demander, puis consultez tooit lors de la création de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8bd04-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="8bd04-167">adresse IP de Hello est attribué dynamiquement les ressources toohello lors de la création de la passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="8bd04-168">Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*.</span><span class="sxs-lookup"><span data-stu-id="8bd04-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="8bd04-169">Vous ne pouvez pas demander d’affectation d’adresse IP publique statique.</span><span class="sxs-lookup"><span data-stu-id="8bd04-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="8bd04-170">Toutefois, cela ne signifie pas que l’adresse IP de hello change après que qu’elle a été affectée passerelle VPN de tooyour.</span><span class="sxs-lookup"><span data-stu-id="8bd04-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="8bd04-171">Hello seule fois changements d’adresses IP publiques hello est hello lorsque la passerelle est supprimé et recréé.</span><span class="sxs-lookup"><span data-stu-id="8bd04-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="8bd04-172">Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="8bd04-173">Demander une adresse IP publique qui sera assignée tooyour de réseau virtuel passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="8bd04-174"><a name="GatewayIPConfig"></a>5. Créer la configuration d’adressage IP de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="8bd04-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="8bd04-175">configuration de la passerelle Hello définit le sous-réseau de hello et toouse adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="8bd04-176">Utilisez hello suivant exemple toocreate votre configuration de la passerelle :</span><span class="sxs-lookup"><span data-stu-id="8bd04-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="8bd04-177"><a name="CreateGateway"></a>6. Créer une passerelle VPN de hello</span><span class="sxs-lookup"><span data-stu-id="8bd04-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="8bd04-178">Créer la passerelle VPN de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="8bd04-179">Création d’une passerelle VPN peut prendre jusqu'à too45 minutes ou plus toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8bd04-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="8bd04-180">Utilisez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="8bd04-180">Use hello following values:</span></span>

* <span data-ttu-id="8bd04-181">Hello *- le type de passerelle* pour un Site à Site est configuration *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="8bd04-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="8bd04-182">type de passerelle Hello est toujours configuration toohello spécifique que vous implémentez.</span><span class="sxs-lookup"><span data-stu-id="8bd04-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="8bd04-183">Par exemple, d’autres configurations de passerelle peuvent nécessiter GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8bd04-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="8bd04-184">Hello *- VpnType* peut être *RouteBased* (appelée tooas une passerelle dynamique dans certains documents), ou *basée sur des stratégies* (appelée tooas une passerelle statique dans la documentation ).</span><span class="sxs-lookup"><span data-stu-id="8bd04-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="8bd04-185">Pour plus d’informations sur les types de passerelles VPN, consultez [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="8bd04-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8bd04-186">Sélectionnez hello SKU de passerelle que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="8bd04-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="8bd04-187">Des limites de configuration s’appliquent à certaines références (SKU).</span><span class="sxs-lookup"><span data-stu-id="8bd04-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="8bd04-188">Pour plus d’informations, consultez l’article [Références (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="8bd04-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="8bd04-189">Si vous obtenez une erreur lors de la création de passerelle VPN de hello concernant hello - GatewaySku, vérifiez que vous avez installé la version la plus récente des applets de commande PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="8bd04-190"><a name="ConfigureVPNDevice"></a>7. Configuration de votre périphérique VPN</span><span class="sxs-lookup"><span data-stu-id="8bd04-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="8bd04-191">Réseau local de tooan connexions site à Site requièrent un périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="8bd04-192">Dans cette étape, vous configurez votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="8bd04-193">Lorsque vous configurez votre périphérique VPN, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="8bd04-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="8bd04-194">Une clé partagée.</span><span class="sxs-lookup"><span data-stu-id="8bd04-194">A shared key.</span></span> <span data-ttu-id="8bd04-195">Cela est hello même partagé clé que vous spécifiez lors de la création de votre connexion VPN de Site à Site.</span><span class="sxs-lookup"><span data-stu-id="8bd04-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="8bd04-196">Dans nos exemples, nous utilisons une clé partagée basique.</span><span class="sxs-lookup"><span data-stu-id="8bd04-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="8bd04-197">Nous conseillons de générer un toouse de clé plus complexe.</span><span class="sxs-lookup"><span data-stu-id="8bd04-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="8bd04-198">Hello adresse IP publique de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8bd04-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="8bd04-199">Vous pouvez afficher l’adresse IP publique de hello à l’aide de hello portail Azure, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="8bd04-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="8bd04-200">hello toofind adresse IP publique de votre passerelle de réseau virtuel à l’aide de PowerShell, hello d’utiliser l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8bd04-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="8bd04-201"><a name="CreateConnection"></a>8. Créer la connexion VPN de hello</span><span class="sxs-lookup"><span data-stu-id="8bd04-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="8bd04-202">Ensuite, créez hello VPN de Site à Site connexion entre votre passerelle de réseau virtuel et votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="8bd04-203">Être des valeurs de hello tooreplace que par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="8bd04-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="8bd04-204">clé partagée de Hello doit correspondre à valeur hello que vous avez utilisé pour la configuration de votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="8bd04-205">Notez que hello '-ConnectionType' pour le Site à Site est *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="8bd04-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="8bd04-206">Définir les variables de hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="8bd04-207">Créer la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="8bd04-208">Après quelques instants, hello connexion sera établie.</span><span class="sxs-lookup"><span data-stu-id="8bd04-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="8bd04-209"><a name="toverify"></a>9. Vérifiez la connexion VPN de hello</span><span class="sxs-lookup"><span data-stu-id="8bd04-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="8bd04-210">Il existe quelques façons tooverify votre connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="8bd04-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="8bd04-211"><a name="connectVM"></a>machine virtuelle de tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="8bd04-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="8bd04-212"><a name="modify"></a>Modifier des préfixes d’adresses IP d’une passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="8bd04-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="8bd04-213">Si vous changez de préfixes d’adresses IP hello souhaité routé emplacement local de tooyour, vous pouvez modifier la passerelle de réseau local hello.</span><span class="sxs-lookup"><span data-stu-id="8bd04-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="8bd04-214">Deux ensembles d’instructions vous sont fournis :</span><span class="sxs-lookup"><span data-stu-id="8bd04-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="8bd04-215">instructions Hello que vous choisissez dépendant de si vous avez déjà créé votre connexion de passerelle.</span><span class="sxs-lookup"><span data-stu-id="8bd04-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="8bd04-216"><a name="modifygwipaddress"></a>Modifier l’adresse IP de passerelle hello pour une passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="8bd04-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="8bd04-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8bd04-217">Next steps</span></span>

*  <span data-ttu-id="8bd04-218">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="8bd04-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="8bd04-219">Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="8bd04-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="8bd04-220">Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8bd04-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
