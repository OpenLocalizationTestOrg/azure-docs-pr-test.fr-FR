---
title: "Se connecter à un site toomultiple de réseau virtuel à l’aide de la passerelle VPN et PowerShell : classique | Documents Microsoft"
description: "Cet article vous guidera dans la connexion réseau virtuel tooa sur site local sites multiples à l’aide d’une passerelle VPN pour le modèle de déploiement classique hello."
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
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="58dcf-103">Ajouter un tooa de connexion de Site à Site réseau virtuel avec une connexion de passerelle VPN existante (classique)</span><span class="sxs-lookup"><span data-stu-id="58dcf-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="58dcf-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="58dcf-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="58dcf-105">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="58dcf-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="58dcf-106">Cet article vous guide tout au long de l’aide de PowerShell tooadd Site à Site (S2S) connexions tooa passerelle VPN qui dispose d’une connexion existante.</span><span class="sxs-lookup"><span data-stu-id="58dcf-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="58dcf-107">Ce type de connexion est souvent tooas auxquels une configuration de « multisite ».</span><span class="sxs-lookup"><span data-stu-id="58dcf-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="58dcf-108">Hello étapes décrites dans cet article s’appliquent les réseaux toovirtual créés à l’aide du modèle de déploiement classique hello (également appelé Service Management).</span><span class="sxs-lookup"><span data-stu-id="58dcf-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="58dcf-109">Ces étapes ne s’appliquent pas à la configuration des connexions coexistence tooExpressRoute/Site à Site.</span><span class="sxs-lookup"><span data-stu-id="58dcf-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="58dcf-110">Outils et modèles de déploiement</span><span class="sxs-lookup"><span data-stu-id="58dcf-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="58dcf-111">Nous mettons à jour ce tableau à mesure que de nouveaux articles et des outils supplémentaires sont disponibles pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="58dcf-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="58dcf-112">Quand un article est disponible, nous lier directement tooit à partir de cette table.</span><span class="sxs-lookup"><span data-stu-id="58dcf-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="58dcf-113">À propos de la connexion</span><span class="sxs-lookup"><span data-stu-id="58dcf-113">About connecting</span></span>

<span data-ttu-id="58dcf-114">Vous pouvez connecter plusieurs sites tooa unique virtuel réseau local.</span><span class="sxs-lookup"><span data-stu-id="58dcf-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="58dcf-115">Cela est particulièrement intéressant pour la création de solutions de cloud hybrides.</span><span class="sxs-lookup"><span data-stu-id="58dcf-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="58dcf-116">Création d’une passerelle de réseau virtuel Azure tooyour connexion multisite est similaire toocreating autres connexions de Site à Site.</span><span class="sxs-lookup"><span data-stu-id="58dcf-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="58dcf-117">En fait, vous pouvez utiliser une passerelle VPN Azure existante, tant que passerelle de hello est dynamique (basé sur l’itinéraire).</span><span class="sxs-lookup"><span data-stu-id="58dcf-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="58dcf-118">Si vous disposez déjà d’un réseau virtuel de passerelle statique tooyour connecté, vous pouvez modifier toodynamic de type hello passerelle sans avoir besoin de réseau virtuel de toorebuild hello dans plusieurs sites de commande tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="58dcf-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="58dcf-119">Avant de modifier le type de routage hello, assurez-vous que votre passerelle VPN locale prend en charge les configurations de VPN basée sur un itinéraire.</span><span class="sxs-lookup"><span data-stu-id="58dcf-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="58dcf-120">![diagramme multi-sites](./media/vpn-gateway-multi-site/multisite.png "multi-sites")</span><span class="sxs-lookup"><span data-stu-id="58dcf-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="58dcf-121">Points tooconsider</span><span class="sxs-lookup"><span data-stu-id="58dcf-121">Points tooconsider</span></span>

<span data-ttu-id="58dcf-122">**Vous ne serez pas réseau virtuel toothis du modifications toomake portail toouse en mesure de hello.**</span><span class="sxs-lookup"><span data-stu-id="58dcf-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="58dcf-123">Vous avez besoin de fichier de configuration réseau toomake modifications toohello au lieu d’utiliser le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="58dcf-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="58dcf-124">Si vous apportez des modifications dans le portail de hello, elles remplaceront vos paramètres de référence multisite pour ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="58dcf-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="58dcf-125">Vous devriez vous sentir à l’aise à l’aide du fichier de configuration de réseau hello par temps de hello vous avez terminé la procédure de plusieurs sites hello.</span><span class="sxs-lookup"><span data-stu-id="58dcf-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="58dcf-126">Toutefois, si vous avez plusieurs personnes travaillent sur la configuration de votre réseau, vous devez toomake assurer que tout le monde connaît cette limitation.</span><span class="sxs-lookup"><span data-stu-id="58dcf-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="58dcf-127">Cela ne signifie pas que vous ne pouvez pas utiliser portal de hello du tout.</span><span class="sxs-lookup"><span data-stu-id="58dcf-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="58dcf-128">Vous pouvez l’utiliser pour tout le reste, à l’exception de renforcement de réseau virtuel particulier toothis configuration modifications.</span><span class="sxs-lookup"><span data-stu-id="58dcf-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="58dcf-129">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="58dcf-129">Before you begin</span></span>

<span data-ttu-id="58dcf-130">Avant de commencer la configuration, vérifiez que vous disposez des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="58dcf-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="58dcf-131">Matériel VPN compatible pour chaque emplacement local.</span><span class="sxs-lookup"><span data-stu-id="58dcf-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="58dcf-132">Vérifiez [sur des périphériques VPN pour la connectivité de réseau virtuel](vpn-gateway-about-vpn-devices.md) tooverify si unité hello que toouse est un élément connu toobe compatible.</span><span class="sxs-lookup"><span data-stu-id="58dcf-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="58dcf-133">Une adresse IP IPv4 publique exposée en externe pour chaque périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="58dcf-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="58dcf-134">adresse IP de Hello ne peut pas se trouver derrière un NAT.</span><span class="sxs-lookup"><span data-stu-id="58dcf-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="58dcf-135">Cela est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="58dcf-135">This is requirement.</span></span>
* <span data-ttu-id="58dcf-136">Vous devez tooinstall hello dernière version de hello applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="58dcf-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="58dcf-137">Assurez-vous que vous installez la version de Service Management (SM) de hello dans la version de gestionnaire de ressources toohello Ajout.</span><span class="sxs-lookup"><span data-stu-id="58dcf-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="58dcf-138">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="58dcf-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="58dcf-139">Un expert en configuration du matériel VPN.</span><span class="sxs-lookup"><span data-stu-id="58dcf-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="58dcf-140">Vous avez toohave un fort comprendre comment tooconfigure votre périphérique VPN ou un travail avec une personne.</span><span class="sxs-lookup"><span data-stu-id="58dcf-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="58dcf-141">plages d’adresses IP Hello que vous souhaitez toouse pour votre réseau virtuel (si vous n’avez pas déjà créé une).</span><span class="sxs-lookup"><span data-stu-id="58dcf-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="58dcf-142">plages d’adresses IP Hello pour chacun des sites de réseau local hello que vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="58dcf-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="58dcf-143">Vous devez toomake que les plages d’adresse IP de hello pour chacun des sites de réseau local hello que vous souhaitez tooconnect toodo pas de chevauchement.</span><span class="sxs-lookup"><span data-stu-id="58dcf-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="58dcf-144">Dans le cas contraire, le portail de hello ou hello API REST rejettera configuration hello en cours de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="58dcf-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="58dcf-145">Par exemple, si vous avez deux sites de réseau local que tous les deux contenir hello IP adresse plage 10.2.3.0/24 et que vous disposez d’un package avec une adresse de destination 10.2.3.3, Azure ne saura pas le site auquel vous souhaitez que les plages d’adresses toosend hello package toobecause hello sont qui se chevauchent.</span><span class="sxs-lookup"><span data-stu-id="58dcf-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="58dcf-146">problèmes de routage tooprevent, Azure n’autorise pas vous tooupload un fichier de configuration qui comporte des plages qui se chevauchent.</span><span class="sxs-lookup"><span data-stu-id="58dcf-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="58dcf-147">1. Créer un VPN de site à site</span><span class="sxs-lookup"><span data-stu-id="58dcf-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="58dcf-148">Si vous avez déjà un VPN de site à site avec une passerelle de routage dynamique, bravo !</span><span class="sxs-lookup"><span data-stu-id="58dcf-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="58dcf-149">Vous pouvez passer trop[exporter les paramètres de configuration de réseau virtuel hello](#export).</span><span class="sxs-lookup"><span data-stu-id="58dcf-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="58dcf-150">Dans le cas contraire, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="58dcf-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="58dcf-151">Si vous avez déjà un réseau virtuel de site à site, mais que sa passerelle de routage est statique :</span><span class="sxs-lookup"><span data-stu-id="58dcf-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="58dcf-152">Modifier votre toodynamic de type de passerelle routage.</span><span class="sxs-lookup"><span data-stu-id="58dcf-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="58dcf-153">Un VPN multisite requiert une passerelle de routage dynamique (ou basée sur un itinéraire).</span><span class="sxs-lookup"><span data-stu-id="58dcf-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="58dcf-154">type de toochange votre passerelle, vous aurez besoin toofirst delete hello existant passerelle, puis créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="58dcf-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="58dcf-155">Pour obtenir des instructions, consultez [comment toochange hello type de routage VPN pour votre passerelle](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="58dcf-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="58dcf-156">Configurez votre nouvelle passerelle et créez votre tunnel VPN.</span><span class="sxs-lookup"><span data-stu-id="58dcf-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="58dcf-157">Pour obtenir des instructions, consultez [configurer une passerelle VPN Bonjour portail classique Azure](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="58dcf-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="58dcf-158">Tout d’abord, modifiez votre toodynamic de type de passerelle routage.</span><span class="sxs-lookup"><span data-stu-id="58dcf-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="58dcf-159">Si vous n’avez pas de réseau virtuel de site à site :</span><span class="sxs-lookup"><span data-stu-id="58dcf-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="58dcf-160">Créer votre réseau virtuel de Site à Site à l’aide de ces instructions : [créer un réseau virtuel avec une connexion VPN de Site à Site Bonjour portail classique Azure](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="58dcf-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="58dcf-161">Configurez une passerelle de routage dynamique en suivant la procédure décrite dans [Configuration d’une passerelle VPN](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="58dcf-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="58dcf-162">Être vraiment tooselect **routage dynamique** pour le type de passerelle.</span><span class="sxs-lookup"><span data-stu-id="58dcf-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="58dcf-163"><a name="export"></a>2. Exporter le fichier de configuration de réseau hello</span><span class="sxs-lookup"><span data-stu-id="58dcf-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="58dcf-164">Exportez votre fichier de configuration réseau Azure en exécutant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="58dcf-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="58dcf-165">Vous pouvez modifier l’emplacement de hello de hello tooexport tooa autre emplacement de fichier si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="58dcf-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="58dcf-166">3. Fichier de configuration de réseau hello ouvert</span><span class="sxs-lookup"><span data-stu-id="58dcf-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="58dcf-167">Ouvrez le fichier de configuration de réseau hello que vous avez téléchargé dans la dernière étape de hello.</span><span class="sxs-lookup"><span data-stu-id="58dcf-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="58dcf-168">Utilisez l’éditeur xml de votre choix.</span><span class="sxs-lookup"><span data-stu-id="58dcf-168">Use any xml editor that you like.</span></span> <span data-ttu-id="58dcf-169">fichier de Hello doit ressembler similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="58dcf-169">hello file should look similar toohello following:</span></span>

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

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="58dcf-170">4. Ajouter plusieurs références de site</span><span class="sxs-lookup"><span data-stu-id="58dcf-170">4. Add multiple site references</span></span>
<span data-ttu-id="58dcf-171">Lorsque vous ajoutez ou supprimez les informations de référence de site, vous apporterez des modifications de configuration toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="58dcf-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="58dcf-172">Ajoutez une nouvelle référence de site locale déclenche toocreate Azure un tunnel.</span><span class="sxs-lookup"><span data-stu-id="58dcf-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="58dcf-173">Dans l’exemple hello ci-dessous, la configuration du réseau hello est pour une connexion de site unique.</span><span class="sxs-lookup"><span data-stu-id="58dcf-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="58dcf-174">Enregistrer le fichier de hello une fois que vous avez terminé d’apporter vos modifications.</span><span class="sxs-lookup"><span data-stu-id="58dcf-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="58dcf-175">références à des sites supplémentaires tooadd (créer une configuration multisite), ajoutez simplement les lignes « LocalNetworkSiteRef » supplémentaires, comme indiqué dans l’exemple hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="58dcf-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="58dcf-176">5. Importer le fichier configuration réseau hello</span><span class="sxs-lookup"><span data-stu-id="58dcf-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="58dcf-177">Importez le fichier de configuration de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="58dcf-177">Import hello network configuration file.</span></span> <span data-ttu-id="58dcf-178">Lorsque vous importez ce fichier avec les modifications de hello, nouveaux tunnels de hello seront ajoutés.</span><span class="sxs-lookup"><span data-stu-id="58dcf-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="58dcf-179">les tunnels Hello utilisera la passerelle dynamique hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="58dcf-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="58dcf-180">Vous pouvez utiliser portail classique de hello ou fichier de hello tooimport PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58dcf-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="58dcf-181">6. Télécharger les clés</span><span class="sxs-lookup"><span data-stu-id="58dcf-181">6. Download keys</span></span>
<span data-ttu-id="58dcf-182">Une fois que les nouveaux tunnels ont été ajoutés, utilisez hello PowerShell applet de commande 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE clés prépartagées pour chaque tunnel.</span><span class="sxs-lookup"><span data-stu-id="58dcf-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="58dcf-183">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58dcf-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="58dcf-184">Si vous préférez, vous pouvez également utiliser hello *Get Virtual Network Gateway Shared Key* tooget de l’API REST hello clés prépartagées.</span><span class="sxs-lookup"><span data-stu-id="58dcf-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="58dcf-185">7. Vérifiez vos connexions</span><span class="sxs-lookup"><span data-stu-id="58dcf-185">7. Verify your connections</span></span>
<span data-ttu-id="58dcf-186">Vérifiez l’état des tunnels multisite hello.</span><span class="sxs-lookup"><span data-stu-id="58dcf-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="58dcf-187">Après avoir téléchargé les clés hello de chaque tunnel, vous souhaiterez tooverify connexions.</span><span class="sxs-lookup"><span data-stu-id="58dcf-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="58dcf-188">Utilisez « Get-AzureVnetConnection' tooget une liste de réseau virtuel tunnels, comme indiqué dans l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="58dcf-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="58dcf-189">VNet1 désigne hello hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="58dcf-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="58dcf-190">L’exemple renvoie :</span><span class="sxs-lookup"><span data-stu-id="58dcf-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
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
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="58dcf-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58dcf-191">Next steps</span></span>

<span data-ttu-id="58dcf-192">toolearn en savoir plus sur les passerelles VPN, consultez [sur les passerelles VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="58dcf-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
