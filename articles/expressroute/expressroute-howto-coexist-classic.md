---
title: "Configuration de connexions ExpressRoute et VPN de site à site pouvant coexister : classique : Azure | Microsoft Docs"
description: "Cet article vous guide dans la configuration d’une connexion VPN de Site à Site qui peut coexister pour le modèle de déploiement classique hello et ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="00ce4-103">Configurer la coexistence de connexions de site à site et ExpressRoute (classique)</span><span class="sxs-lookup"><span data-stu-id="00ce4-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00ce4-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="00ce4-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="00ce4-105">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="00ce4-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="00ce4-106">Ayant la possibilité de hello tooconfigure VPN de Site à Site et ExpressRoute présente plusieurs avantages.</span><span class="sxs-lookup"><span data-stu-id="00ce4-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="00ce4-107">Vous pouvez configurer un VPN de Site à Site comme un chemin d’accès sécurisé de basculement pour ExressRoute, ou utiliser des VPN de Site à Site tooconnect toosites qui ne sont pas connectés via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="00ce4-108">Les deux scénarios dans cet article, nous allons aborder hello étapes tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="00ce4-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="00ce4-109">Cet article concerne le modèle de déploiement classique toohello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="00ce4-110">Cette configuration n’est pas disponible dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="00ce4-111">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="00ce4-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="00ce4-112">Circuits ExpressRoute doivent être préconfigurés avant de suivre les instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="00ce4-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="00ce4-113">Assurez-vous que vous avez suivi les guides hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et [configurer le routage](expressroute-howto-routing-classic.md) avant de suivre les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="00ce4-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="00ce4-114">Limites et limitations</span><span class="sxs-lookup"><span data-stu-id="00ce4-114">Limits and limitations</span></span>
* <span data-ttu-id="00ce4-115">**Le routage de transit n’est pas pris en charge.**</span><span class="sxs-lookup"><span data-stu-id="00ce4-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="00ce4-116">Vous ne pouvez effectuer de routage (via Azure) entre votre réseau local connecté via le réseau VPN de site à site et votre réseau local connecté via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="00ce4-117">**Le routage point à site n’est pas pris en charge.**</span><span class="sxs-lookup"><span data-stu-id="00ce4-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="00ce4-118">Vous ne pouvez pas activer le point-to-site VPN connexions toohello même réseau virtuel qui est connecté tooExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="00ce4-119">Point-to-site VPN et ExpressRoute ne peuvent pas coexister pour hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="00ce4-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="00ce4-120">**Le tunneling forcé ne peut pas être activé sur la passerelle VPN de Site à Site hello.**</span><span class="sxs-lookup"><span data-stu-id="00ce4-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="00ce4-121">Vous pouvez uniquement « forcer » tous les Internet liées au trafic tooyour arrière sur réseau local via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="00ce4-122">**La passerelle de référence de base n’est pas prise en charge.**</span><span class="sxs-lookup"><span data-stu-id="00ce4-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="00ce4-123">Vous devez utiliser une passerelle de base SKU pour les deux hello [passerelle ExpressRoute](expressroute-about-virtual-network-gateways.md) et hello [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="00ce4-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="00ce4-124">**Seule la passerelle VPN basée sur un itinéraire est prise en charge.**</span><span class="sxs-lookup"><span data-stu-id="00ce4-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="00ce4-125">Vous devez utiliser une [passerelle VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) basée sur un itinéraire.</span><span class="sxs-lookup"><span data-stu-id="00ce4-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="00ce4-126">L’**itinéraire statique doit être configuré pour votre passerelle VPN.**</span><span class="sxs-lookup"><span data-stu-id="00ce4-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="00ce4-127">Si votre réseau local est connecté tooboth ExpressRoute et un Site à Site VPN, vous devez disposer un itinéraire statique configuré dans votre toohello de connexion de réseau local tooroute hello Site-à-Site VPN Internet public.</span><span class="sxs-lookup"><span data-stu-id="00ce4-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="00ce4-128">La **passerelle ExpressRoute doit être configurée en premier.**</span><span class="sxs-lookup"><span data-stu-id="00ce4-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="00ce4-129">Vous devez d’abord créer passerelle ExpressRoute de hello avant d’ajouter de la passerelle VPN de Site à Site hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="00ce4-130">Modèles de configuration</span><span class="sxs-lookup"><span data-stu-id="00ce4-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="00ce4-131">Configurer un réseau VPN de site à site comme un chemin d’accès de basculement pour ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="00ce4-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="00ce4-132">Vous pouvez configurer une connexion VPN de site à site en tant que sauvegarde pour ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="00ce4-133">Cela s’applique uniquement toovirtual réseaux lié toohello chemin d’accès d’homologation privée Azure.</span><span class="sxs-lookup"><span data-stu-id="00ce4-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="00ce4-134">Il n’existe aucune solution de basculement basée sur des réseaux VPN pour les services accessibles via les homologations Azure public et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="00ce4-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="00ce4-135">lien principal de hello est toujours Hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="00ce4-136">Flux de données via un chemin d’accès de Site à Site VPN hello uniquement si hello circuit ExpressRoute échoue.</span><span class="sxs-lookup"><span data-stu-id="00ce4-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="00ce4-137">Alors que le circuit ExpressRoute est préférable à VPN de Site à Site lorsque les deux itinéraires sont hello même, Azure utilisera itinéraire de hello plus long préfixe correspondance toochoose hello vers la destination du paquet hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Coexister](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="00ce4-139">Configurer un toosites tooconnect VPN de Site à Site ne pas connecté via ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="00ce4-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="00ce4-140">Vous pouvez configurer votre réseau où certains sites connectent directement tooAzure via le VPN de Site à Site, et certains sites via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexister](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="00ce4-142">Vous ne pouvez pas configurer un réseau virtuel comme un routeur de transit.</span><span class="sxs-lookup"><span data-stu-id="00ce4-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="00ce4-143">En sélectionnant hello étapes toouse</span><span class="sxs-lookup"><span data-stu-id="00ce4-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="00ce4-144">Il existe deux ensembles différents de toochoose procédures à partir de connexions de tooconfigure de commande peuvent coexister.</span><span class="sxs-lookup"><span data-stu-id="00ce4-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="00ce4-145">procédure de configuration Hello que vous sélectionnez dépend si vous disposez d’un réseau virtuel existant que vous souhaitez tooconnect à, ou que vous voulez toocreate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="00ce4-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="00ce4-146">Je ne disposer d’un réseau virtuel et devez toocreate une.</span><span class="sxs-lookup"><span data-stu-id="00ce4-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="00ce4-147">Si vous n’avez pas déjà un réseau virtuel, cette procédure vous guidera création d’un réseau virtuel à l’aide du modèle de déploiement classique hello et la création de nouvelles connexions VPN de Site à Site et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="00ce4-148">tooconfigure, suivez les étapes dans la section de l’article hello hello [toocreate un nouveau réseau virtuel et les connexions de coexistence](#new).</span><span class="sxs-lookup"><span data-stu-id="00ce4-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="00ce4-149">J’ai déjà un réseau virtuel répondant au modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="00ce4-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="00ce4-150">Vous disposez peut-être déjà d’un réseau virtuel avec une connexion VPN de site à site existante ou une connexion ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="00ce4-151">Hello section article [tooconfigure coexsiting les connexions pour un réseau virtuel existant déjà](#add) vous guide dans la suppression de la passerelle de hello et la création de nouvelles connexions VPN de Site à Site et ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="00ce4-152">Notez que lors de la création de nouvelles connexions hello, les étapes de hello doivent être effectuées dans un ordre spécifique.</span><span class="sxs-lookup"><span data-stu-id="00ce4-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="00ce4-153">N’utilisez pas les instructions hello dans d’autres articles de toocreate vos passerelles et les connexions.</span><span class="sxs-lookup"><span data-stu-id="00ce4-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="00ce4-154">Dans cette procédure, la création de connexions peuvent coexister sera requièrent que vous toodelete votre passerelle, puis configurez nouvelles passerelles.</span><span class="sxs-lookup"><span data-stu-id="00ce4-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="00ce4-155">Cela signifie que vous devrez temps mort pour les connexions entre différents locaux pendant que vous supprimez et recréez la passerelle et les connexions, mais vous n’aurez pas toomigrate un de vos machines virtuelles ou services tooa nouveau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="00ce4-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="00ce4-156">Vos machines virtuelles et les services seront toujours en mesure de toocommunicate sortantes via l’équilibrage de charge hello lorsque vous configurez votre passerelle s’ils ne sont donc toodo configuré.</span><span class="sxs-lookup"><span data-stu-id="00ce4-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="00ce4-157"><a name="new"></a>toocreate un nouveau réseau virtuel et la coexistence de connexions</span><span class="sxs-lookup"><span data-stu-id="00ce4-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="00ce4-158">Cette procédure vous guide dans la création d’un réseau virtuel et dans l’établissement de nouvelles connexions de site à site et ExpressRoute appelées à coexister.</span><span class="sxs-lookup"><span data-stu-id="00ce4-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="00ce4-159">Vous devez tooinstall hello dernière version de hello applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="00ce4-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="00ce4-160">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="00ce4-161">Notez que les applets de commande hello que vous allez utiliser pour cette configuration peut être légèrement différente de celle que vous connaissez peut-être.</span><span class="sxs-lookup"><span data-stu-id="00ce4-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="00ce4-162">Applets de commande hello toouse vraiment être spécifié dans ces instructions.</span><span class="sxs-lookup"><span data-stu-id="00ce4-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="00ce4-163">Créez un schéma pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="00ce4-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="00ce4-164">Pour plus d’informations sur le schéma de configuration hello, consultez [schéma de configuration de réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="00ce4-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="00ce4-165">Lorsque vous créez votre schéma, assurez-vous que vous utilisez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="00ce4-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="00ce4-166">sous-réseau de passerelle de Hello pour hello du réseau virtuel doit être /27 ou un préfixe plus court (par exemple, /26 ou /25).</span><span class="sxs-lookup"><span data-stu-id="00ce4-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="00ce4-167">type de connexion de passerelle Hello est « dédié ».</span><span class="sxs-lookup"><span data-stu-id="00ce4-167">hello gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="00ce4-168">Après la création et la configuration de votre fichier de schéma xml, téléchargez les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="00ce4-169">Cette opération crée votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="00ce4-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="00ce4-170">Utilisez hello suivant tooupload de l’applet de commande de votre fichier, en remplaçant la valeur de hello avec vos propres.</span><span class="sxs-lookup"><span data-stu-id="00ce4-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="00ce4-171"><a name="gw"></a>Créez une passerelle ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="00ce4-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="00ce4-172">Être toospecify vraiment hello GatewaySKU comme *Standard*, *hautes performances*, ou *UltraPerformance* et hello le type de passerelle en tant que *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="00ce4-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="00ce4-173">Utilisez hello suivant l’exemple, en remplaçant les valeurs hello pour votre propre.</span><span class="sxs-lookup"><span data-stu-id="00ce4-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="00ce4-174">Lier le circuit ExpressRoute toohello hello ExpressRoute passerelle.</span><span class="sxs-lookup"><span data-stu-id="00ce4-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="00ce4-175">Une fois cette étape terminée, hello entre votre réseau local et le Azure via ExpressRoute, est établie.</span><span class="sxs-lookup"><span data-stu-id="00ce4-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="00ce4-176"><a name="vpngw"></a>Créez ensuite la passerelle VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="00ce4-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="00ce4-177">Hello GatewaySKU doit être *Standard*, *hautes performances*, ou *UltraPerformance* et hello le type de passerelle doit être *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="00ce4-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="00ce4-178">paramètres de passerelle de réseau virtuel hello tooretrieve, y compris l’ID de passerelle hello et adresse IP publique hello, utilisent hello `Get-AzureVirtualNetworkGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="00ce4-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="00ce4-179">Créez une entité de passerelle VPN de site local.</span><span class="sxs-lookup"><span data-stu-id="00ce4-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="00ce4-180">Cette commande ne configure pas votre passerelle VPN locale.</span><span class="sxs-lookup"><span data-stu-id="00ce4-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="00ce4-181">Au lieu de cela, il vous permet de paramètres de la passerelle locale hello tooprovide, telles que des adresses IP publiques de hello et hello localement l’espace d’adressage, afin que hello passerelle VPN Azure peut se connecter tooit.</span><span class="sxs-lookup"><span data-stu-id="00ce4-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="00ce4-182">site local de Hello pour hello VPN de Site à Site n’est pas défini dans le fichier netcfg de hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="00ce4-183">Au lieu de cela, vous devez utiliser ce paramètres de site local cmdlet toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="00ce4-184">Vous ne pouvez pas définir à l’aide du portail ou fichier netcfg de hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="00ce4-185">Utilisez hello suivant l’exemple, en remplaçant les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="00ce4-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="00ce4-186">Si votre réseau local possède plusieurs itinéraires, vous pouvez tous les transmettre sous la forme d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="00ce4-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="00ce4-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="00ce4-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="00ce4-188">paramètres de passerelle de réseau virtuel hello tooretrieve, y compris l’ID de passerelle hello et adresse IP publique hello, utilisent hello `Get-AzureVirtualNetworkGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="00ce4-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="00ce4-189">Consultez hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="00ce4-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="00ce4-190">Configurez votre passerelle VPN locale appareil tooconnect toohello nouveau.</span><span class="sxs-lookup"><span data-stu-id="00ce4-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="00ce4-191">Utilisez les informations de hello que vous avez récupéré à l’étape 6 lors de la configuration de votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="00ce4-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="00ce4-192">Pour plus d’informations sur la configuration du périphérique VPN, consultez la rubrique [Configuration de périphérique VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="00ce4-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="00ce4-193">Passerelle VPN de Site à Site du hello lien sur la passerelle locale toohello Azure.</span><span class="sxs-lookup"><span data-stu-id="00ce4-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="00ce4-194">Dans cet exemple, connectedEntityId est ID de passerelle locale hello, qui se trouve en exécutant `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="00ce4-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="00ce4-195">Vous pouvez trouver virtualNetworkGatewayId à l’aide de hello `Get-AzureVirtualNetworkGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="00ce4-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="00ce4-196">Après cette étape, hello entre votre réseau local et Azure via hello connexion VPN de Site à Site est établie.</span><span class="sxs-lookup"><span data-stu-id="00ce4-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="00ce4-197"><a name="add"></a>connexions de coexsiting tooconfigure pour un réseau virtuel existant</span><span class="sxs-lookup"><span data-stu-id="00ce4-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="00ce4-198">Si vous avez un réseau virtuel existant, vérifiez la taille de sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="00ce4-199">Si le sous-réseau de passerelle hello est /28 ou /29, vous devez tout d’abord supprimer la passerelle de réseau virtuel hello et augmenter la taille de sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="00ce4-200">Hello étapes décrites dans cette section vous indiquent comment toodo qui.</span><span class="sxs-lookup"><span data-stu-id="00ce4-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="00ce4-201">Si le sous-réseau de passerelle hello est /27 ou supérieure et réseau virtuel de hello est connecté via ExpressRoute, vous pouvez ignorer les étapes hello ci-dessous et continuer trop[« Étape 6 : créer une passerelle VPN de Site à Site »](#vpngw) dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="00ce4-202">Lorsque vous supprimez la passerelle existante de hello, votre site local perdrez réseau virtuel de hello connexion tooyour lorsque vous travaillez sur cette configuration.</span><span class="sxs-lookup"><span data-stu-id="00ce4-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="00ce4-203">Vous devez la version la plus récente hello tooinstall Hello applets de commande PowerShell de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="00ce4-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="00ce4-204">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation des applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="00ce4-205">Notez que les applets de commande hello que vous allez utiliser pour cette configuration peut être légèrement différente de celle que vous connaissez peut-être.</span><span class="sxs-lookup"><span data-stu-id="00ce4-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="00ce4-206">Applets de commande hello toouse vraiment être spécifié dans ces instructions.</span><span class="sxs-lookup"><span data-stu-id="00ce4-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="00ce4-207">Supprimer la passerelle hello ExpressRoute ou VPN de Site à Site existante.</span><span class="sxs-lookup"><span data-stu-id="00ce4-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="00ce4-208">Utilisez hello suivant l’applet de commande, en remplaçant les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="00ce4-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="00ce4-209">Exporter le schéma de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="00ce4-209">Export hello virtual network schema.</span></span> <span data-ttu-id="00ce4-210">Utilisez hello suivant l’applet de commande PowerShell, en remplaçant les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="00ce4-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="00ce4-211">Modifier le schéma de fichier de configuration de réseau hello afin que le sous-réseau de passerelle hello est /27 ou un préfixe plus court (par exemple, /26 ou /25).</span><span class="sxs-lookup"><span data-stu-id="00ce4-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="00ce4-212">Consultez hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="00ce4-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="00ce4-213">Si vous n’avez pas suffisamment d’adresses IP dans votre taille de sous-réseau de passerelle de réseau virtuel tooincrease hello, vous devez tooadd plus d’espace d’adressage IP.</span><span class="sxs-lookup"><span data-stu-id="00ce4-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="00ce4-214">Pour plus d’informations sur le schéma de configuration hello, consultez [schéma de configuration de réseau virtuel Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="00ce4-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="00ce4-215">Si votre passerelle précédente était un VPN de Site à Site, vous devez également modifier type de connexion hello trop**dédié**.</span><span class="sxs-lookup"><span data-stu-id="00ce4-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="00ce4-216">À ce stade, vous disposez d’un réseau virtuel sans passerelles.</span><span class="sxs-lookup"><span data-stu-id="00ce4-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="00ce4-217">toocreate nouvelles passerelles et vos connexions, vous pouvez poursuivre [étape 4 : créer une passerelle ExpressRoute](#gw), située dans hello précédant l’ensemble d’étapes.</span><span class="sxs-lookup"><span data-stu-id="00ce4-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00ce4-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00ce4-218">Next steps</span></span>
<span data-ttu-id="00ce4-219">Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="00ce4-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

