---
title: "Connecter votre réseau local à un réseau virtuel Azure : VPN site à site : PowerShell | Microsoft Docs"
description: "Étapes de création d’une connexion IPsec entre votre réseau local et un réseau virtuel Azure via l’Internet public. Ces étapes vous aideront à créer une connexion de passerelle VPN de site à site à l’aide de PowerShell."
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
ms.openlocfilehash: 27f4a8fb9a83b98e99df635bf4c80f6048ce348c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="617ef-104">Créer un réseau virtuel avec une connexion VPN de site à site à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="617ef-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="617ef-105">Cet article vous explique comment utiliser PowerShell pour créer une connexion de passerelle VPN de site à site à partir de votre réseau local vers le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="617ef-105">This article shows you how to use PowerShell to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="617ef-106">Les étapes mentionnées dans cet article s’appliquent au modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="617ef-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="617ef-107">Vous pouvez également créer cette configuration à l’aide d’un autre outil ou modèle de déploiement en sélectionnant une option différente dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="617ef-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="617ef-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="617ef-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="617ef-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="617ef-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="617ef-110">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="617ef-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="617ef-111">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="617ef-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="617ef-112">Portail Classic (classique)</span><span class="sxs-lookup"><span data-stu-id="617ef-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="617ef-113">Une connexion de passerelle VPN de site à site permet de connecter votre réseau local à un réseau virtuel Azure via un tunnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="617ef-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="617ef-114">Ce type de connexion requiert un périphérique VPN local disposant d’une adresse IP publique exposée en externe.</span><span class="sxs-lookup"><span data-stu-id="617ef-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="617ef-115">Pour plus d’informations sur les passerelles VPN, consultez l’article [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="617ef-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Schéma de connexion intersite d’une passerelle VPN site à site](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="617ef-117"><a name="before"></a>Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="617ef-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="617ef-118">Vérifiez que vous disposez des éléments ci-dessous avant de commencer votre configuration :</span><span class="sxs-lookup"><span data-stu-id="617ef-118">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="617ef-119">Veillez à disposer d’un périphérique VPN compatible et à être entouré d’une personne en mesure de le configurer.</span><span class="sxs-lookup"><span data-stu-id="617ef-119">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="617ef-120">Pour plus d’informations sur les périphériques VPN compatibles et la configuration de votre périphérique, consultez l’article [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="617ef-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="617ef-121">Vérifiez que vous disposez d’une adresse IPv4 publique exposée en externe pour votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="617ef-122">Cette adresse IP ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="617ef-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="617ef-123">Si vous ne maîtrisez pas les plages d’adresses IP situées dans votre configuration de réseau local, vous devez contacter une personne en mesure de vous aider.</span><span class="sxs-lookup"><span data-stu-id="617ef-123">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="617ef-124">Lorsque vous créez cette configuration, vous devez spécifier les préfixes des plages d’adresses IP qu’Azure acheminera vers votre emplacement local.</span><span class="sxs-lookup"><span data-stu-id="617ef-124">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="617ef-125">Aucun des sous-réseaux de votre réseau local ne peut chevaucher les sous-réseaux du réseau virtuel auquel vous souhaitez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="617ef-125">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="617ef-126">Installez la dernière version des applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="617ef-126">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="617ef-127">Les applets de commande PowerShell sont fréquemment mises à jour, et vous devez généralement mettre à jour les vôtres pour obtenir les toutes dernières fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="617ef-127">PowerShell cmdlets are updated frequently and you will typically need to update your PowerShell cmdlets to get the latest feature functionality.</span></span> <span data-ttu-id="617ef-128">Si vous ne mettez pas à jour vos applets de commande PowerShell, les valeurs spécifiées peuvent échouer.</span><span class="sxs-lookup"><span data-stu-id="617ef-128">If you don't update your PowerShell cmdlets, the values specified may fail.</span></span> <span data-ttu-id="617ef-129">Pour plus d’informations sur le téléchargement et l’installation des applets de commande PowerShell, voir [How to install and configure Azure PowerShell (Guide pratique d’installation et de configuration d’Azure PowerShell)](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="617ef-129">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="617ef-130"><a name="example"></a>Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="617ef-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="617ef-131">Nous utilisons les valeurs suivantes dans les exemples de cet article.</span><span class="sxs-lookup"><span data-stu-id="617ef-131">The examples in this article use the following values.</span></span> <span data-ttu-id="617ef-132">Vous pouvez utiliser ces valeurs pour créer un environnement de test ou vous y référer pour mieux comprendre les exemples de cet article.</span><span class="sxs-lookup"><span data-stu-id="617ef-132">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

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


## <span data-ttu-id="617ef-133"><a name="Login"></a>1. Connexion à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="617ef-133"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="617ef-134"><a name="VNet"></a>2. Créer un réseau virtuel et un sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="617ef-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="617ef-135">Si vous n’avez pas de réseau virtuel, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="617ef-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="617ef-136">Lorsque vous créez un réseau virtuel, vérifiez que les espaces d’adressage que vous spécifiez ne chevauchent pas les espaces d’adressage de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="617ef-136">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="617ef-137"><a name="vnet"></a>Création d’un réseau virtuel et d’un sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="617ef-137"><a name="vnet"></a>To create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="617ef-138">Cet exemple permet de créer un réseau virtuel et un sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="617ef-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="617ef-139">Si vous disposez déjà d’un réseau virtuel auquel vous devez ajouter un sous-réseau de passerelle, consultez [Pour ajouter un sous-réseau de passerelle à un réseau virtuel que vous avez déjà créé](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="617ef-139">If you already have a virtual network that you need to add a gateway subnet to, see [To add a gateway subnet to a virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="617ef-140">Créez un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="617ef-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="617ef-141">Créez votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="617ef-141">Create your virtual network.</span></span>

1. <span data-ttu-id="617ef-142">Définissez les variables.</span><span class="sxs-lookup"><span data-stu-id="617ef-142">Set the variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="617ef-143">Créez le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="617ef-143">Create the VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="617ef-144"><a name="gatewaysubnet"></a>Pour ajouter un sous-réseau de passerelle à un réseau virtuel que vous avez déjà créé</span><span class="sxs-lookup"><span data-stu-id="617ef-144"><a name="gatewaysubnet"></a>To add a gateway subnet to a virtual network you have already created</span></span>

1. <span data-ttu-id="617ef-145">Définissez les variables.</span><span class="sxs-lookup"><span data-stu-id="617ef-145">Set the variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="617ef-146">Créez le sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="617ef-146">Create the gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="617ef-147">Définissez la configuration.</span><span class="sxs-lookup"><span data-stu-id="617ef-147">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="617ef-148">3. <a name="localnet"></a>Créer la passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="617ef-148">3. <a name="localnet"></a>Create the local network gateway</span></span>

<span data-ttu-id="617ef-149">La passerelle de réseau local fait généralement référence à votre emplacement local.</span><span class="sxs-lookup"><span data-stu-id="617ef-149">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="617ef-150">Donnez au site un nom auquel Azure pourra se référer, puis spécifiez l’adresse IP du périphérique VPN local vers lequel vous allez créer une connexion.</span><span class="sxs-lookup"><span data-stu-id="617ef-150">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="617ef-151">Spécifiez également les préfixes d’adresses IP qui seront acheminés via la passerelle VPN vers le périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-151">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="617ef-152">Les préfixes d’adresses que vous spécifiez sont les préfixes situés sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="617ef-152">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="617ef-153">Vous pouvez facilement mettre à jour ces préfixes si votre réseau local change.</span><span class="sxs-lookup"><span data-stu-id="617ef-153">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="617ef-154">Utilisez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="617ef-154">Use the following values:</span></span>

* <span data-ttu-id="617ef-155">*GatewayIPAddress* est l’adresse IP de votre périphérique VPN local.</span><span class="sxs-lookup"><span data-stu-id="617ef-155">The *GatewayIPAddress* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="617ef-156">Votre périphérique VPN ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="617ef-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="617ef-157">*AddressPrefix* est votre espace d’adressage local.</span><span class="sxs-lookup"><span data-stu-id="617ef-157">The *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="617ef-158">Pour ajouter une passerelle de réseau local avec un préfixe d’adresse unique :</span><span class="sxs-lookup"><span data-stu-id="617ef-158">To add a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="617ef-159">Pour ajouter une passerelle de réseau local avec des préfixes d’adresse multiples :</span><span class="sxs-lookup"><span data-stu-id="617ef-159">To add a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="617ef-160">Pour modifier des préfixes d’adresses IP de votre passerelle de réseau local :</span><span class="sxs-lookup"><span data-stu-id="617ef-160">To modify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="617ef-161">Parfois, les préfixes de votre passerelle de réseau local changent.</span><span class="sxs-lookup"><span data-stu-id="617ef-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="617ef-162">Les étapes à suivre pour modifier vos préfixes d’adresses IP varient selon que vous avez créé une connexion à la passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-162">The steps you take to modify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="617ef-163">Consultez la section [Modifier des préfixes d’adresses IP de votre passerelle de réseau local](#modify) de cet article.</span><span class="sxs-lookup"><span data-stu-id="617ef-163">See the [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="617ef-164"><a name="PublicIP"></a>4. Demander une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="617ef-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="617ef-165">Une passerelle VPN doit avoir une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="617ef-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="617ef-166">Vous commencez par demander la ressource d’adresse IP, puis vous y faites référence lors de la création de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="617ef-166">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="617ef-167">L’adresse IP est affectée dynamiquement à la ressource lors de la création de la passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-167">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="617ef-168">Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*.</span><span class="sxs-lookup"><span data-stu-id="617ef-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="617ef-169">Vous ne pouvez pas demander d’affectation d’adresse IP publique statique.</span><span class="sxs-lookup"><span data-stu-id="617ef-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="617ef-170">Toutefois, cela ne signifie pas que l’adresse IP change après son affectation à votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-170">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="617ef-171">L’adresse IP publique change uniquement lorsque la passerelle est supprimée, puis recréée.</span><span class="sxs-lookup"><span data-stu-id="617ef-171">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="617ef-172">Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="617ef-173">Demandez une adresse IP publique qui sera affectée à votre passerelle VPN de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="617ef-173">Request a Public IP address that will be assigned to your virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="617ef-174"><a name="GatewayIPConfig"></a>5. Créer la configuration de l’adressage IP de la passerelle</span><span class="sxs-lookup"><span data-stu-id="617ef-174"><a name="GatewayIPConfig"></a>5. Create the gateway IP addressing configuration</span></span>

<span data-ttu-id="617ef-175">La configuration de la passerelle définit le sous-réseau et l’adresse IP publique à utiliser.</span><span class="sxs-lookup"><span data-stu-id="617ef-175">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="617ef-176">Utilisez l’exemple suivant pour créer la configuration de votre passerelle :</span><span class="sxs-lookup"><span data-stu-id="617ef-176">Use the following example to create your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="617ef-177"><a name="CreateGateway"></a>6. Créer la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="617ef-177"><a name="CreateGateway"></a>6. Create the VPN gateway</span></span>

<span data-ttu-id="617ef-178">Créez la passerelle VPN de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="617ef-178">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="617ef-179">La création d’une passerelle VPN peut prendre 45 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="617ef-179">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="617ef-180">Utilisez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="617ef-180">Use the following values:</span></span>

* <span data-ttu-id="617ef-181">Le paramètre *-GatewayType* pour une configuration de site à site est *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="617ef-181">The *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="617ef-182">Le type de passerelle dépend toujours de la configuration que vous implémentez.</span><span class="sxs-lookup"><span data-stu-id="617ef-182">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="617ef-183">Par exemple, d’autres configurations de passerelle peuvent nécessiter GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="617ef-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="617ef-184">Le paramètre *-VpnType* peut avoir pour valeur *RouteBased* (appelé passerelle dynamique dans certaines documentations) ou *PolicyBased* (appelé passerelle statique dans certaines documentations).</span><span class="sxs-lookup"><span data-stu-id="617ef-184">The *-VpnType* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="617ef-185">Pour plus d’informations sur les types de passerelles VPN, consultez [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="617ef-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="617ef-186">Sélectionnez la référence SKU de la passerelle que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="617ef-186">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="617ef-187">Des limites de configuration s’appliquent à certaines références (SKU).</span><span class="sxs-lookup"><span data-stu-id="617ef-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="617ef-188">Pour plus d’informations, consultez l’article [Références (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="617ef-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="617ef-189">Si vous obtenez une erreur lors de la création de la passerelle VPN relative au paramètre -GatewaySku, vérifiez que vous avez installé la dernière version des applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="617ef-189">If you get an error when creating the VPN gateway regarding the -GatewaySku, verify that you have installed the latest version of the PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="617ef-190"><a name="ConfigureVPNDevice"></a>7. Configuration de votre périphérique VPN</span><span class="sxs-lookup"><span data-stu-id="617ef-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="617ef-191">Les connexions site à site vers un réseau local nécessitent un périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-191">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="617ef-192">Dans cette étape, vous configurez votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="617ef-193">Pour configurer votre périphérique VPN, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="617ef-193">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="617ef-194">Une clé partagée.</span><span class="sxs-lookup"><span data-stu-id="617ef-194">A shared key.</span></span> <span data-ttu-id="617ef-195">Il s’agit de la clé partagée spécifiée lors de la création de la connexion VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="617ef-195">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="617ef-196">Dans nos exemples, nous utilisons une clé partagée basique.</span><span class="sxs-lookup"><span data-stu-id="617ef-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="617ef-197">Nous vous conseillons de générer une clé plus complexe.</span><span class="sxs-lookup"><span data-stu-id="617ef-197">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="617ef-198">L’adresse IP publique de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="617ef-198">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="617ef-199">Vous pouvez afficher l’adresse IP publique à l’aide du portail Azure, de PowerShell ou de l’interface de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="617ef-199">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="617ef-200">Pour trouver l’adresse IP publique de votre passerelle de réseau virtuel à l’aide de PowerShell, utilisez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="617ef-200">To find the Public IP address of your virtual network gateway using PowerShell, use the following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="617ef-201"><a name="CreateConnection"></a>8. Créer la connexion VPN</span><span class="sxs-lookup"><span data-stu-id="617ef-201"><a name="CreateConnection"></a>8. Create the VPN connection</span></span>

<span data-ttu-id="617ef-202">Créez ensuite la connexion VPN de site à site entre votre passerelle de réseau virtuel et votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-202">Next, create the Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="617ef-203">Assurez-vous de remplacer ces valeurs par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="617ef-203">Be sure to replace the values with your own.</span></span> <span data-ttu-id="617ef-204">La clé partagée doit correspondre à la valeur que vous avez utilisée pour la configuration de votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-204">The shared key must match the value you used for your VPN device configuration.</span></span> <span data-ttu-id="617ef-205">Notez que la valeur « -ConnectionType » pour la connexion de site à site est *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="617ef-205">Notice that the '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="617ef-206">Définissez les variables.</span><span class="sxs-lookup"><span data-stu-id="617ef-206">Set the variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="617ef-207">Créez la connexion.</span><span class="sxs-lookup"><span data-stu-id="617ef-207">Create the connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="617ef-208">Après un bref délai, la connexion sera établie.</span><span class="sxs-lookup"><span data-stu-id="617ef-208">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="617ef-209"><a name="toverify"></a>9. Vérifier la connexion VPN</span><span class="sxs-lookup"><span data-stu-id="617ef-209"><a name="toverify"></a>9. Verify the VPN connection</span></span>

<span data-ttu-id="617ef-210">Il existe différentes façons de vérifier votre connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="617ef-210">There are a few different ways to verify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="617ef-211"><a name="connectVM"></a>Se connecter à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="617ef-211"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="617ef-212"><a name="modify"></a>Modifier des préfixes d’adresses IP d’une passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="617ef-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="617ef-213">Si les préfixes d’adresse IP que vous souhaitez acheminer vers votre emplacement local changent, vous pouvez modifier la passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="617ef-213">If the IP address prefixes that you want routed to your on-premises location change, you can modify the local network gateway.</span></span> <span data-ttu-id="617ef-214">Deux ensembles d’instructions vous sont fournis :</span><span class="sxs-lookup"><span data-stu-id="617ef-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="617ef-215">Les instructions que vous choisissez d’appliquer varient selon que vous avez déjà créé ou non votre connexion à la passerelle.</span><span class="sxs-lookup"><span data-stu-id="617ef-215">The instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="617ef-216"><a name="modifygwipaddress"></a>Modifier l’adresse IP d’une passerelle de réseau local</span><span class="sxs-lookup"><span data-stu-id="617ef-216"><a name="modifygwipaddress"></a>Modify the gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="617ef-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="617ef-217">Next steps</span></span>

*  <span data-ttu-id="617ef-218">Une fois la connexion achevée, vous pouvez ajouter des machines virtuelles à vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="617ef-218">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="617ef-219">Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="617ef-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="617ef-220">Pour plus d’informations sur le protocole BGP, consultez les articles [Vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [Comment configurer BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="617ef-220">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
