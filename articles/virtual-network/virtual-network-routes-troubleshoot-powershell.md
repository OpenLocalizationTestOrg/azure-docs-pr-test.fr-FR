---
title: "itinéraires aaaTroubleshoot - PowerShell | Documents Microsoft"
description: "Découvrez comment tootroubleshoot route dans le modèle de déploiement hello Azure Resource Manager à l’aide d’Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="4cb11-103">Résoudre des problèmes d’itinéraires à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cb11-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4cb11-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4cb11-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="4cb11-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cb11-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="4cb11-106">Si vous rencontrez tooor de problèmes de connectivité réseau à partir de votre Machine virtuelle (VM) Azure, itinéraires affecte votre flux de trafic de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4cb11-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="4cb11-107">Cet article fournit une vue d’ensemble des fonctionnalités des diagnostics pour les itinéraires toohelp dépannage.</span><span class="sxs-lookup"><span data-stu-id="4cb11-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="4cb11-108">Des tables d’itinéraires sont associées aux sous-réseaux, qui s’appliquent à toutes les interfaces réseau de ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4cb11-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="4cb11-109">Hello les types d’itinéraires suivants peut être l’interface de réseau tooeach appliqué :</span><span class="sxs-lookup"><span data-stu-id="4cb11-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="4cb11-110">**Itinéraires système :** par défaut, chaque sous-réseau créé dans un réseau virtuel Azure a des tables d’itinéraires système qui permettent le trafic de réseau virtuel local, le trafic local au moyen de passerelles VPN et le trafic Internet.</span><span class="sxs-lookup"><span data-stu-id="4cb11-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="4cb11-111">Il existe également des itinéraires système pour les réseaux virtuels homologués.</span><span class="sxs-lookup"><span data-stu-id="4cb11-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="4cb11-112">**Itinéraires BGP :** propagées interfaces toonetwork via ExpressRoute ou les connexions VPN site à site.</span><span class="sxs-lookup"><span data-stu-id="4cb11-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="4cb11-113">En savoir plus sur le routage BGP en lisant hello [BGP avec les passerelles VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) et [présentation ExpressRoute](../expressroute/expressroute-introduction.md) articles.</span><span class="sxs-lookup"><span data-stu-id="4cb11-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="4cb11-114">**Itinéraires définis par l’utilisateur (UDR) :** si vous utilisez les dispositifs réseau virtuel ou sont-tunneling forcé réseau local du tooan le trafic via un VPN de site à site, vous pouvez avoir des itinéraires définis par l’utilisateur (UDRs) associés à votre table d’itinéraires de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4cb11-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="4cb11-115">Si vous n’êtes pas familiarisé avec UDRs, lecture hello [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md#user-defined-routes) l’article.</span><span class="sxs-lookup"><span data-stu-id="4cb11-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="4cb11-116">Hello itinéraires différents qui peuvent être appliqués tooa interface de réseau, il peut être difficile toodetermine les itinéraires d’agrégation sont efficaces.</span><span class="sxs-lookup"><span data-stu-id="4cb11-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="4cb11-117">toohelp dépanner la connectivité de réseau d’ordinateurs virtuels, vous pouvez afficher tous les itinéraires effectifs hello pour une interface réseau dans le modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4cb11-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="4cb11-118">À l’aide de flux de trafic d’itinéraires effectifs tootroubleshoot machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4cb11-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="4cb11-119">Cet article utilise hello suivant le scénario comme une tooillustrate exemple comment tootroubleshoot hello effective route pour une interface réseau :</span><span class="sxs-lookup"><span data-stu-id="4cb11-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="4cb11-120">Une machine virtuelle (*VM1*) connecté toohello réseau virtuel (*VNet1*, préfixe : 10.9.0.0/16) échoue tooconnect tooa VM(VM3) dans un réseau virtuel qui vient d’être ressources (*VNet3*, 10.10.0.0/16 du préfixe).</span><span class="sxs-lookup"><span data-stu-id="4cb11-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="4cb11-121">Il y a aucune UDRs ou le protocole BGP n’achemine appliqué tooVM1-NIC1 network interface connectée toohello VM uniquement les itinéraires système sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="4cb11-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="4cb11-122">Cet article explique comment toodetermine hello provoquer d’erreur de connexion hello, à l’aide de la fonctionnalité d’itinéraires effectifs dans un modèle de déploiement de gestion des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb11-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="4cb11-123">Alors que hello exemple utilise uniquement les itinéraires système, hello les mêmes étapes peut être utilisé toodetermine échecs de connexion entrant et sortant sur n’importe quel type d’itinéraire.</span><span class="sxs-lookup"><span data-stu-id="4cb11-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="4cb11-124">Si votre machine virtuelle possède plusieurs cartes réseau attachée, vérifiez itinéraires effectifs pour chacun des hello toodiagnose NIC tooand du problèmes de connectivité de réseau à partir d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4cb11-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="4cb11-125">Afficher les itinéraires effectifs pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4cb11-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="4cb11-126">toosee hello agrégation itinéraires qui sont appliqué tooa machine virtuelle, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="4cb11-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="4cb11-127">Afficher les itinéraires effectifs pour une interface réseau</span><span class="sxs-lookup"><span data-stu-id="4cb11-127">View effective routes for a network interface</span></span>
<span data-ttu-id="4cb11-128">toosee hello agrégation itinéraires qui sont appliqués tooa interface de réseau, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="4cb11-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="4cb11-129">Démarrer un tooAzure de session et de connexion Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4cb11-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="4cb11-130">Si vous n’êtes pas familiarisé avec Azure PowerShell, lire hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.</span><span class="sxs-lookup"><span data-stu-id="4cb11-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="4cb11-131">Hello commande ci-dessous retourne interface réseau tooa tous les itinéraires appliquées nommé *NIC1 de VM1* dans le groupe de ressources hello *RG1*.</span><span class="sxs-lookup"><span data-stu-id="4cb11-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="4cb11-132">Si vous ne connaissez pas nom hello d’une interface réseau, tapez Bonjour commande tooretrieve hello nom de toutes les interfaces réseau dans un group.* de ressources</span><span class="sxs-lookup"><span data-stu-id="4cb11-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="4cb11-133">Hello sortie suivante recherche une sortie similaire toohello chaque hello de sous-réseau itinéraire appliqué toohello à que carte réseau est connectée :</span><span class="sxs-lookup"><span data-stu-id="4cb11-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="4cb11-134">Notez suivant hello dans la sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="4cb11-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="4cb11-135">**Nom**: nom de l’itinéraire effectif de hello peut être vide, sauf mention spéciale, itinéraires définis par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4cb11-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="4cb11-136">**État**: indique l’état de l’itinéraire effectif de hello.</span><span class="sxs-lookup"><span data-stu-id="4cb11-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="4cb11-137">Les valeurs possibles sont « Actif » ou « Non valide ».</span><span class="sxs-lookup"><span data-stu-id="4cb11-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="4cb11-138">**AddressPrefixes**: Spécifie le préfixe d’adresse hello de l’itinéraire effectif de hello en notation CIDR.</span><span class="sxs-lookup"><span data-stu-id="4cb11-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="4cb11-139">**type de tronçon suivant**: indique le saut suivant hello hello donnée d’itinéraire.</span><span class="sxs-lookup"><span data-stu-id="4cb11-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="4cb11-140">Les valeurs possibles sont *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* ou *Null*.</span><span class="sxs-lookup"><span data-stu-id="4cb11-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="4cb11-141">La valeur *Null* pour **nextHopType** dans un itinéraire défini par l’utilisateur peut indiquer un itinéraire non valide.</span><span class="sxs-lookup"><span data-stu-id="4cb11-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="4cb11-142">Par exemple, si **nextHopType** est *VirtualAppliance* et hello network appliance virtuelle machine virtuelle n’est pas dans un état de mise en service en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4cb11-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="4cb11-143">Si **nextHopType** est *VPNGateway* et qu’aucune passerelle mis en service en cours d’exécution dans hello réseau virtuel donné, les itinéraires hello peuvent devenir non valides.</span><span class="sxs-lookup"><span data-stu-id="4cb11-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="4cb11-144">**NextHopIpAddress**: Spécifie l’adresse IP de hello du tronçon suivant de hello de l’itinéraire effectif de hello.</span><span class="sxs-lookup"><span data-stu-id="4cb11-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="4cb11-145">Hello commande ci-dessous retourne les itinéraires hello dans une table tooview plus facile :</span><span class="sxs-lookup"><span data-stu-id="4cb11-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="4cb11-146">Hello de sortie suivant est certaines de sortie hello reçue pour le scénario hello décrit précédemment :</span><span class="sxs-lookup"><span data-stu-id="4cb11-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="4cb11-147">Il n’existe aucun toohello itinéraire répertorié *WestUS-VNet3* réseau virtuel (10.10.0.0/16)** à partir du préfixe *WestUS-VNet1* (préfixe 10.9.0.0/16) dans la sortie de hello à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="4cb11-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="4cb11-148">Comme indiqué dans hello illustration suivante, hello lien d’homologation du réseau virtuel avec hello *WestUS-VNet3* réseau virtuel est Bonjour *Disconnected* état.</span><span class="sxs-lookup"><span data-stu-id="4cb11-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="4cb11-149">lien de Hello bidirectionnel pour hello d’homologation est rompue, qui explique pourquoi VM1 pas pu se connecter tooVM3 Bonjour *WestUS-VNet3* réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="4cb11-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="4cb11-150">Configurez de nouveau un lien VNET Peering bidirectionnel pour les réseaux virtuels *WestUS-VNet1* et *WestUS-VNet3*.</span><span class="sxs-lookup"><span data-stu-id="4cb11-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="4cb11-151">sortie Hello retourné après que le lien d’homologation du réseau virtuel hello est correctement établie :</span><span class="sxs-lookup"><span data-stu-id="4cb11-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="4cb11-152">Après avoir déterminé le problème de hello, vous pouvez ajouter, supprimer, ou modifier des routes et tables d’itinéraires.</span><span class="sxs-lookup"><span data-stu-id="4cb11-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="4cb11-153">Hello du type suivant de commande toosee une liste des commandes hello utilisé toodo ainsi :</span><span class="sxs-lookup"><span data-stu-id="4cb11-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="4cb11-154">Considérations</span><span class="sxs-lookup"><span data-stu-id="4cb11-154">Considerations</span></span>
<span data-ttu-id="4cb11-155">Quelques tookeep choses à l’esprit lorsque vous parcourez la liste hello des itinéraires retourné :</span><span class="sxs-lookup"><span data-stu-id="4cb11-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="4cb11-156">Les itinéraires sont basés sur la correspondance de préfixe la plus longue parmi les itinéraires définis par l’utilisateur, BGP et système.</span><span class="sxs-lookup"><span data-stu-id="4cb11-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="4cb11-157">S’il existe plusieurs itinéraires avec hello même locales correspondent, alors un itinéraire est sélectionné en fonction de son origine dans hello suivant l’ordre :</span><span class="sxs-lookup"><span data-stu-id="4cb11-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="4cb11-158">Itinéraire défini par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4cb11-158">User-defined route</span></span>
  * <span data-ttu-id="4cb11-159">Itinéraire BGP</span><span class="sxs-lookup"><span data-stu-id="4cb11-159">BGP route</span></span>
  * <span data-ttu-id="4cb11-160">Itinéraire système (par défaut)</span><span class="sxs-lookup"><span data-stu-id="4cb11-160">System (Default) route</span></span>
    
    <span data-ttu-id="4cb11-161">Avec les itinéraires effectifs, vous pouvez uniquement afficher les itinéraires effectifs qui correspondent au Gestionnaire de stratégies locales en fonction de tous les itinéraires de disponible hello.</span><span class="sxs-lookup"><span data-stu-id="4cb11-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="4cb11-162">En affichant la manière dont les itinéraires hello sont en réalité évalués pour une carte réseau donnée, il est ainsi beaucoup plus facile tootroubleshoot des itinéraires spécifiques qui affecte la connectivité à partir de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4cb11-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="4cb11-163">Si vous avez UDRs et que vous envoyez appliance virtuelle du trafic tooa réseau (NVA), avec *VirtualAppliance* en tant que **tronçon suivant**, vérifiez que le transfert IP est activé sur le trafic hello réception hello NVA ou les paquets sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="4cb11-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="4cb11-164">Si le tunneling forcé est activé, tout le trafic Internet sortant sera routé tooon local.</span><span class="sxs-lookup"><span data-stu-id="4cb11-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="4cb11-165">RDP/SSH à partir de tooyour Internet que machine virtuelle peut ne pas fonctionne avec ce paramètre, en fonction de comment hello local gère ce trafic.</span><span class="sxs-lookup"><span data-stu-id="4cb11-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="4cb11-166">Le tunneling forcé peut être activé :</span><span class="sxs-lookup"><span data-stu-id="4cb11-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="4cb11-167">si vous utilisez un VPN de site à site, en établissant un itinéraire défini par l’utilisateur avec nextHopType en tant que passerelle VPN ;</span><span class="sxs-lookup"><span data-stu-id="4cb11-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="4cb11-168">si un itinéraire par défaut est annoncé sur BGP.</span><span class="sxs-lookup"><span data-stu-id="4cb11-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="4cb11-169">Pour le réseau virtuel d’homologation du trafic toowork correctement, un itinéraire de système **nextHopType** *VNetPeering* doit exister pour hello homologuer plage de préfixe de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="4cb11-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="4cb11-170">Si un itinéraire de ce type n’existe pas et hello réseau virtuel d’homologation link recherche OK :</span><span class="sxs-lookup"><span data-stu-id="4cb11-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="4cb11-171">Patientez quelques secondes, puis recommencez s’il s’agit d’un lien d’homologation récemment établi.</span><span class="sxs-lookup"><span data-stu-id="4cb11-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="4cb11-172">Occasionnellement dure plus longtemps toopropagate itinéraires tooall hello interfaces réseau présentes dans un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="4cb11-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="4cb11-173">Règles du groupe de sécurité réseau (NSG) affecte les flux de trafic hello.</span><span class="sxs-lookup"><span data-stu-id="4cb11-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="4cb11-174">Pour plus d’informations, consultez hello [résoudre les problèmes des groupes de sécurité réseau](virtual-network-nsg-troubleshoot-powershell.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4cb11-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

