---
title: "Connecter un réseau virtuel à plusieurs sites en utilisant une passerelle VPN et PowerShell : Classic | Microsoft Docs"
description: "Cet article vous guidera pour la connexion de plusieurs sites locaux à un réseau virtuel à l’aide d’une passerelle VPN pour le modèle de déploiement classique."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: bb3129f70f5eeed99d5889226aa6727f675b6217
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="3635e-103">Ajouter une connexion de site à site à un réseau virtuel avec une connexion de passerelle VPN existante (Classic)</span><span class="sxs-lookup"><span data-stu-id="3635e-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3635e-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3635e-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="3635e-105">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="3635e-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="3635e-106">Cet article vous explique comment utiliser PowerShell pour ajouter des connexions de site à site (S2S) à une passerelle VPN qui dispose déjà d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="3635e-106">This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="3635e-107">Pour ce type de connexion, on fait souvent référence à une configuration « multisite ».</span><span class="sxs-lookup"><span data-stu-id="3635e-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="3635e-108">Les étapes de cet article s’appliquent aux réseaux virtuels créés à l’aide du modèle de déploiement Classic (également connu comme le modèle Gestion des services).</span><span class="sxs-lookup"><span data-stu-id="3635e-108">The steps in this article apply to virtual networks created using the classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="3635e-109">Ces étapes ne s’appliquent pas aux configurations de connexion coexistante ExpressRoute/site à site.</span><span class="sxs-lookup"><span data-stu-id="3635e-109">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="3635e-110">Outils et modèles de déploiement</span><span class="sxs-lookup"><span data-stu-id="3635e-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="3635e-111">Nous mettons à jour ce tableau à mesure que de nouveaux articles et des outils supplémentaires sont disponibles pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="3635e-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="3635e-112">Quand un article est disponible, le lien vers cet article est ajouté à ce tableau.</span><span class="sxs-lookup"><span data-stu-id="3635e-112">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="3635e-113">À propos de la connexion</span><span class="sxs-lookup"><span data-stu-id="3635e-113">About connecting</span></span>

<span data-ttu-id="3635e-114">Vous pouvez connecter plusieurs sites locaux à un même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3635e-114">You can connect multiple on-premises sites to a single virtual network.</span></span> <span data-ttu-id="3635e-115">Cela est particulièrement intéressant pour la création de solutions de cloud hybrides.</span><span class="sxs-lookup"><span data-stu-id="3635e-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="3635e-116">La création d’une connexion sur plusieurs sites à votre passerelle de réseau virtuel Azure ressemble à la création d’autres connexions de site à site.</span><span class="sxs-lookup"><span data-stu-id="3635e-116">Creating a multi-site connection to your Azure virtual network gateway is similar to creating other Site-to-Site connections.</span></span> <span data-ttu-id="3635e-117">En fait, vous pouvez utiliser une passerelle VPN Azure existante tant que la passerelle est dynamique (basée sur un itinéraire).</span><span class="sxs-lookup"><span data-stu-id="3635e-117">In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).</span></span>

<span data-ttu-id="3635e-118">Si une passerelle statique est déjà connectée à votre réseau virtuel, vous pouvez changer le type de passerelle en dynamique sans avoir à régénérer le réseau virtuel pour prendre en charge plusieurs sites.</span><span class="sxs-lookup"><span data-stu-id="3635e-118">If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site.</span></span> <span data-ttu-id="3635e-119">Dans ce cas, assurez-vous que votre passerelle VPN locale prend en charge les configurations VPN basées sur un itinéraire.</span><span class="sxs-lookup"><span data-stu-id="3635e-119">Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="3635e-120">![diagramme multi-sites](./media/vpn-gateway-multi-site/multisite.png "multi-sites")</span><span class="sxs-lookup"><span data-stu-id="3635e-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-to-consider"></a><span data-ttu-id="3635e-121">Éléments à prendre en considération</span><span class="sxs-lookup"><span data-stu-id="3635e-121">Points to consider</span></span>

<span data-ttu-id="3635e-122">**Vous ne pouvez pas utiliser le portail pour apporter des modifications à ce réseau virtuel.**</span><span class="sxs-lookup"><span data-stu-id="3635e-122">**You won't be able to use the portal to make changes to this virtual network.**</span></span> <span data-ttu-id="3635e-123">Vous devez apporter des modifications au fichier de configuration réseau au lieu d’utiliser le portail.</span><span class="sxs-lookup"><span data-stu-id="3635e-123">You need to make changes to the network configuration file instead of using the portal.</span></span> <span data-ttu-id="3635e-124">Si vous apportez des modifications dans le portail, ces dernières affectent vos paramètres de référence multisite pour ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3635e-124">If you make changes in the portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="3635e-125">Vous aurez le temps de vous familiariser avec le fichier de configuration réseau au terme de la procédure multisite.</span><span class="sxs-lookup"><span data-stu-id="3635e-125">You should feel comfortable using the network configuration file by the time you've completed the multi-site procedure.</span></span> <span data-ttu-id="3635e-126">Toutefois, si plusieurs personnes travaillent sur la configuration de votre réseau, vous devez vous assurer que tout le monde a connaissance de cette limitation.</span><span class="sxs-lookup"><span data-stu-id="3635e-126">However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation.</span></span> <span data-ttu-id="3635e-127">Cela ne signifie pas que vous ne pouvez pas du tout utiliser le portail.</span><span class="sxs-lookup"><span data-stu-id="3635e-127">This doesn't mean that you can't use the portal at all.</span></span> <span data-ttu-id="3635e-128">Vous pouvez l’utiliser pour toutes les procédures, à l’exception des modifications de configuration de ce réseau virtuel spécifique.</span><span class="sxs-lookup"><span data-stu-id="3635e-128">You can use it for everything else, except making configuration changes to this particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3635e-129">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3635e-129">Before you begin</span></span>

<span data-ttu-id="3635e-130">Avant de commencer la configuration, vérifiez que les conditions suivantes sont remplies :</span><span class="sxs-lookup"><span data-stu-id="3635e-130">Before you begin configuration, verify that you have the following:</span></span>

* <span data-ttu-id="3635e-131">Matériel VPN compatible pour chaque emplacement local.</span><span class="sxs-lookup"><span data-stu-id="3635e-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="3635e-132">Voir [À propos des périphériques VPN pour la connectivité au réseau virtuel](vpn-gateway-about-vpn-devices.md) pour vérifier si l’appareil que vous souhaitez utiliser est bien compatible.</span><span class="sxs-lookup"><span data-stu-id="3635e-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.</span></span>
* <span data-ttu-id="3635e-133">Une adresse IP IPv4 publique exposée en externe pour chaque périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="3635e-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="3635e-134">L’adresse IP ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="3635e-134">The IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="3635e-135">Cela est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3635e-135">This is requirement.</span></span>
* <span data-ttu-id="3635e-136">Vous aurez besoin d’installer la dernière version des applets de commande PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="3635e-136">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3635e-137">Veillez à installer à la fois la version Gestion des services et la version Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3635e-137">Make sure you install the Service Management (SM) version in addition to the Resource Manager version.</span></span> <span data-ttu-id="3635e-138">Pour plus d’informations, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="3635e-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="3635e-139">Un expert en configuration du matériel VPN.</span><span class="sxs-lookup"><span data-stu-id="3635e-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="3635e-140">Vous devez avoir une bonne maîtrise de la façon de configurer votre périphérique VPN ou de collaborer avec quelqu’un disposant des connaissances nécessaires.</span><span class="sxs-lookup"><span data-stu-id="3635e-140">You'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="3635e-141">Les plages d’adresses IP que vous souhaitez utiliser pour votre réseau virtuel (si vous n’en avez pas déjà créé).</span><span class="sxs-lookup"><span data-stu-id="3635e-141">The IP address ranges that you want to use for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="3635e-142">Les plages d’adresses IP pour chacun des sites du réseau local auxquels vous vous connecterez.</span><span class="sxs-lookup"><span data-stu-id="3635e-142">The IP address ranges for each of the local network sites that you'll be connecting to.</span></span> <span data-ttu-id="3635e-143">Vous devez vous assurer que les plages d’adresses IP pour chacun des sites du réseau local auxquels vous souhaitez vous connecter ne se chevauchent ne pas.</span><span class="sxs-lookup"><span data-stu-id="3635e-143">You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap.</span></span> <span data-ttu-id="3635e-144">Dans le cas contraire, le portail ou l’API REST rejette la configuration en cours de chargement.</span><span class="sxs-lookup"><span data-stu-id="3635e-144">Otherwise, the portal or the REST API will reject the configuration being uploaded.</span></span><br><span data-ttu-id="3635e-145">Par exemple, si vous avez deux sites de réseau local contenant la plage d’adresse IP 10.2.3.0/24 et que vous disposez d’un package avec une adresse de destination 10.2.3.3, Azure ne saura pas à quel site envoyer le package, car les plages d’adresses se chevauchent.</span><span class="sxs-lookup"><span data-stu-id="3635e-145">For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping.</span></span> <span data-ttu-id="3635e-146">Pour éviter les problèmes de routage, Azure ne vous permet pas de télécharger un fichier de configuration ayant des plages qui se chevauchent.</span><span class="sxs-lookup"><span data-stu-id="3635e-146">To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="3635e-147">1. Créer un VPN de site à site</span><span class="sxs-lookup"><span data-stu-id="3635e-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="3635e-148">Si vous avez déjà un VPN de site à site avec une passerelle de routage dynamique, bravo !</span><span class="sxs-lookup"><span data-stu-id="3635e-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="3635e-149">Vous pouvez [Exporter les paramètres de configuration de réseau virtuel](#export).</span><span class="sxs-lookup"><span data-stu-id="3635e-149">You can proceed to [Export the virtual network configuration settings](#export).</span></span> <span data-ttu-id="3635e-150">Sinon, procédez ainsi :</span><span class="sxs-lookup"><span data-stu-id="3635e-150">If not, do the following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="3635e-151">Si vous avez déjà un réseau virtuel de site à site, mais que sa passerelle de routage est statique :</span><span class="sxs-lookup"><span data-stu-id="3635e-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="3635e-152">Modifiez le type de passerelle en routage dynamique.</span><span class="sxs-lookup"><span data-stu-id="3635e-152">Change your gateway type to dynamic routing.</span></span> <span data-ttu-id="3635e-153">Un VPN multisite requiert une passerelle de routage dynamique (ou basée sur un itinéraire).</span><span class="sxs-lookup"><span data-stu-id="3635e-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="3635e-154">Pour modifier le type de passerelle, vous devez d’abord supprimer la passerelle existante, puis en créer une nouvelle.</span><span class="sxs-lookup"><span data-stu-id="3635e-154">To change your gateway type, you'll need to first delete the existing gateway, then create a new one.</span></span> <span data-ttu-id="3635e-155">Pour obtenir des instructions, consultez la page [Modification du type de routage VPN de votre passerelle](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="3635e-155">For instructions, see [How to change the VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="3635e-156">Configurez votre nouvelle passerelle et créez votre tunnel VPN.</span><span class="sxs-lookup"><span data-stu-id="3635e-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="3635e-157">Pour obtenir des instructions, consultez [Configuration d’une passerelle VPN dans le portail Azure Classic](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="3635e-157">For instructions, see [Configure a VPN Gateway in the Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="3635e-158">Tout d’abord, changez le type de votre passerelle en dynamique.</span><span class="sxs-lookup"><span data-stu-id="3635e-158">First, change your gateway type to dynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="3635e-159">Si vous n’avez pas de réseau virtuel de site à site :</span><span class="sxs-lookup"><span data-stu-id="3635e-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="3635e-160">Créez votre réseau virtuel de site à site en suivant la procédure décrite dans [Création d’un réseau virtuel avec une connexion VPN de site à site dans le portail Azure Classic](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="3635e-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in the Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="3635e-161">Configurez une passerelle de routage dynamique en suivant la procédure décrite dans [Configuration d’une passerelle VPN](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="3635e-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="3635e-162">Veillez à sélectionner le **routage dynamique** pour le type de passerelle.</span><span class="sxs-lookup"><span data-stu-id="3635e-162">Be sure to select **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="3635e-163"><a name="export"></a>2. Exporter le fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="3635e-163"><a name="export"></a>2. Export the network configuration file</span></span>
<span data-ttu-id="3635e-164">Exportez votre fichier de configuration réseau Azure en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="3635e-164">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="3635e-165">Vous pouvez modifier l’emplacement d’exportation du fichier si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3635e-165">You can change the location of the file to export to a different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-the-network-configuration-file"></a><span data-ttu-id="3635e-166">3. Ouvrir le fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="3635e-166">3. Open the network configuration file</span></span>
<span data-ttu-id="3635e-167">Ouvrez le fichier de configuration réseau que vous avez téléchargé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="3635e-167">Open the network configuration file that you downloaded in the last step.</span></span> <span data-ttu-id="3635e-168">Utilisez l’éditeur xml de votre choix.</span><span class="sxs-lookup"><span data-stu-id="3635e-168">Use any xml editor that you like.</span></span> <span data-ttu-id="3635e-169">Le fichier doit se présenter ainsi :</span><span class="sxs-lookup"><span data-stu-id="3635e-169">The file should look similar to the following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="3635e-170">4. Ajouter plusieurs références de site</span><span class="sxs-lookup"><span data-stu-id="3635e-170">4. Add multiple site references</span></span>
<span data-ttu-id="3635e-171">Lorsque vous ajoutez ou supprimez les informations de référence de site, des modifications de configuration sont apportées à ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="3635e-171">When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="3635e-172">À l’ajout d’une nouvelle référence de site local, Azure crée un nouveau tunnel.</span><span class="sxs-lookup"><span data-stu-id="3635e-172">Adding a new local site reference triggers Azure to create a new tunnel.</span></span> <span data-ttu-id="3635e-173">Dans l’exemple ci-dessous, la configuration du réseau correspond à une connexion de site unique.</span><span class="sxs-lookup"><span data-stu-id="3635e-173">In the example below, the network configuration is for a single-site connection.</span></span> <span data-ttu-id="3635e-174">Enregistrez le fichier une fois que vous avez terminé d’apporter vos modifications.</span><span class="sxs-lookup"><span data-stu-id="3635e-174">Save the file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="3635e-175">Pour ajouter des références de site supplémentaires (créer une configuration multisite), ajoutez simplement des lignes « LocalNetworkSiteRef », comme illustré dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3635e-175">To add additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in the example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-the-network-configuration-file"></a><span data-ttu-id="3635e-176">5. Importer le fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="3635e-176">5. Import the network configuration file</span></span>
<span data-ttu-id="3635e-177">Importez le fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="3635e-177">Import the network configuration file.</span></span> <span data-ttu-id="3635e-178">Lorsque vous importez ce fichier avec les modifications, les nouveaux tunnels sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="3635e-178">When you import this file with the changes, the new tunnels will be added.</span></span> <span data-ttu-id="3635e-179">Les tunnels utilisent la passerelle dynamique que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="3635e-179">The tunnels will use the dynamic gateway that you created earlier.</span></span> <span data-ttu-id="3635e-180">Vous pouvez utiliser la version Classic du portail ou PowerShell pour importer le fichier.</span><span class="sxs-lookup"><span data-stu-id="3635e-180">You can either use the classic portal, or PowerShell to import the file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="3635e-181">6. Télécharger les clés</span><span class="sxs-lookup"><span data-stu-id="3635e-181">6. Download keys</span></span>
<span data-ttu-id="3635e-182">Une fois les tunnels ajoutés, utilisez la cmdlet PowerShell Get-AzureVNetGatewayKey pour obtenir les clés prépartagées IPsec/IKE de chaque tunnel.</span><span class="sxs-lookup"><span data-stu-id="3635e-182">Once your new tunnels have been added, use the PowerShell cmdlet 'Get-AzureVNetGatewayKey' to get the IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="3635e-183">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3635e-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="3635e-184">Si vous préférez, vous pouvez également utiliser l’API REST *Obtenir la clé partagée de la passerelle de réseau virtuel* pour obtenir les clés prépartagées.</span><span class="sxs-lookup"><span data-stu-id="3635e-184">If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="3635e-185">7. Vérifiez vos connexions</span><span class="sxs-lookup"><span data-stu-id="3635e-185">7. Verify your connections</span></span>
<span data-ttu-id="3635e-186">Vérifiez l’état de tunnel multisite.</span><span class="sxs-lookup"><span data-stu-id="3635e-186">Check the multi-site tunnel status.</span></span> <span data-ttu-id="3635e-187">Après avoir téléchargé les clés de chaque tunnel, vérifiez les connexions.</span><span class="sxs-lookup"><span data-stu-id="3635e-187">After downloading the keys for each tunnel, you'll want to verify connections.</span></span> <span data-ttu-id="3635e-188">Utilisez Get-AzureVnetConnection pour obtenir la liste des tunnels de réseau virtuel, comme indiqué dans l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3635e-188">Use 'Get-AzureVnetConnection' to get a list of virtual network tunnels, as shown in the example below.</span></span> <span data-ttu-id="3635e-189">VNet1 est le nom du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="3635e-189">VNet1 is the name of the VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="3635e-190">L’exemple renvoie :</span><span class="sxs-lookup"><span data-stu-id="3635e-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site1' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site2' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="3635e-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3635e-191">Next steps</span></span>

<span data-ttu-id="3635e-192">Pour en savoir plus sur les passerelles VPN, consultez [À propos des passerelles VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="3635e-192">To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
